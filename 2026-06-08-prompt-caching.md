# Prompt Caching

Prompt caching lets you mark large, reusable portions of your prompt (like a long system prompt or a big document) so Claude can skip re-processing them on repeat calls — cutting latency by up to 85% and token costs by up to 90%. You add `"cache_control": {"type": "ephemeral"}` to any content block you want cached; the cache lives for 5 minutes and resets on each hit. This is especially valuable for agent loops, RAG pipelines, or any workflow where the same context is reused across many turns.

## Copy-pasteable example (Python)

```python
import anthropic

client = anthropic.Anthropic()

# Large reusable document loaded once
big_doc = open("your_large_doc.txt").read()

response = client.messages.create(
    model="claude-opus-4-8",
    max_tokens=1024,
    system=[
        {
            "type": "text",
            "text": "You are a helpful assistant. Use the document below to answer questions.",
        },
        {
            "type": "text",
            "text": big_doc,
            "cache_control": {"type": "ephemeral"},  # Cache this block
        },
    ],
    messages=[{"role": "user", "content": "Summarize the key points."}],
)

# Check cache usage
print(response.usage)
# cache_creation_input_tokens: N  (first call — cache written)
# cache_read_input_tokens: N      (subsequent calls — cache hit)
```

## Try it yourself

Run the same request twice and compare `usage.cache_creation_input_tokens` vs `usage.cache_read_input_tokens` in the second response — you should see a dramatic drop in billable input tokens and faster time-to-first-token.
