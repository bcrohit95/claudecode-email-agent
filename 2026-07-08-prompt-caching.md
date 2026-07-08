# Claude Code Skill: Prompt Caching

**Date:** 2026-07-08

## What It Is

Prompt caching lets Claude reuse the results of processing a large, repeated
portion of your prompt (like a long system prompt or a big document) instead of
re-processing it on every API call. This dramatically cuts latency and cost when
you're running many requests that share the same context prefix.

To enable it, you add a `cache_control` breakpoint in your messages — Claude
will cache everything up to that point for up to 5 minutes (or up to 1 hour
with extended TTL).

## Copy-Pasteable Example

```python
import anthropic

client = anthropic.Anthropic()

BIG_DOCUMENT = "..." * 5000  # imagine a huge codebase or doc here

response = client.messages.create(
    model="claude-sonnet-5",
    max_tokens=1024,
    system=[
        {
            "type": "text",
            "text": BIG_DOCUMENT,
            "cache_control": {"type": "ephemeral"}  # <-- cache this prefix
        }
    ],
    messages=[
        {"role": "user", "content": "Summarize the key points."}
    ]
)

print(response.usage)
# Look for: cache_creation_input_tokens and cache_read_input_tokens
# On subsequent calls with the same prefix, cache_read_input_tokens will be
# non-zero and cost ~10x less than regular input tokens.
```

## Try It Yourself

1. Load a large file (e.g. a codebase README or long document) into a system prompt.
2. Add `cache_control: {type: "ephemeral"}` to that content block.
3. Make the same API call twice and compare `response.usage` between calls.
4. On the second call you should see `cache_read_input_tokens > 0`, meaning
   Claude skipped re-processing the big prefix and answered faster and cheaper.

> **Tip:** Caching works best when the cached prefix is at least ~1024 tokens.
> Extended cache TTL (1 hour) is available via `cache_control: {type: "ephemeral", ttl: 3600}`.
