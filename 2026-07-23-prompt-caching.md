# Prompt Caching

Prompt Caching lets Claude reuse expensive computations from previous requests — when the same large context (system prompt, documents, examples) is sent repeatedly, the API recognizes the cached prefix and charges far fewer tokens. This dramatically cuts costs and latency for workflows that repeatedly query Claude against a fixed background (e.g., a long codebase, a policy document, or a large set of few-shot examples).

## How it works

Add `"cache_control": {"type": "ephemeral"}` to the content block you want cached. The first request pays full price; subsequent requests that reuse the same prefix hit the cache and cost ~10% of normal input token pricing.

## Example (Python SDK)

```python
import anthropic

client = anthropic.Anthropic()

SYSTEM_DOC = open("large_codebase_summary.txt").read()  # e.g. 50k tokens

response = client.messages.create(
    model="claude-sonnet-5",
    max_tokens=1024,
    system=[
        {
            "type": "text",
            "text": SYSTEM_DOC,
            "cache_control": {"type": "ephemeral"}  # <-- mark for caching
        }
    ],
    messages=[
        {"role": "user", "content": "What does the AuthService class do?"}
    ]
)

print(response.usage)
# On first call:  cache_creation_input_tokens=50000, cache_read_input_tokens=0
# On later calls: cache_creation_input_tokens=0,    cache_read_input_tokens=50000
```

## Try it yourself

Load a large file (at least ~1,000 tokens) as your system prompt with `cache_control`, then ask two different questions back-to-back. Compare `response.usage.cache_read_input_tokens` between the first and second calls — the second should show the cached tokens and return noticeably faster.
