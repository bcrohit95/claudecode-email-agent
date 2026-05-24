# Prompt Caching

## What it is
Prompt caching lets you mark static sections of your prompt (system instructions, long documents, tool definitions) so Claude stores them between API calls — reducing both cost and latency on repeated requests. Once a cache is warm, you pay ~10% of the normal input token price for those cached tokens, and responses arrive faster since Claude skips re-processing the same content. This is especially powerful for chat apps, RAG pipelines, or any workflow that sends the same large context repeatedly.

## Copy-pasteable Example

```python
import anthropic

client = anthropic.Anthropic()

LARGE_SYSTEM_PROMPT = "You are a helpful assistant. " + ("Follow all safety guidelines. " * 200)

# First call — warms the cache
response1 = client.messages.create(
    model="claude-opus-4-7",
    max_tokens=256,
    system=[
        {
            "type": "text",
            "text": LARGE_SYSTEM_PROMPT,
            "cache_control": {"type": "ephemeral"}   # <-- mark for caching
        }
    ],
    messages=[{"role": "user", "content": "What can you help me with?"}]
)
print("Call 1 usage:", response1.usage)

# Second call — cache hit, much cheaper + faster
response2 = client.messages.create(
    model="claude-opus-4-7",
    max_tokens=256,
    system=[
        {
            "type": "text",
            "text": LARGE_SYSTEM_PROMPT,
            "cache_control": {"type": "ephemeral"}
        }
    ],
    messages=[{"role": "user", "content": "Give me a summary of your capabilities."}]
)
print("Call 2 usage:", response2.usage)
# Look for cache_read_input_tokens > 0 on the second call
```

## Try It Yourself
Add `"cache_control": {"type": "ephemeral"}` to the last content block of your system prompt or to a large document you pass repeatedly. Run the same request twice and inspect `response.usage` — on the second call `cache_read_input_tokens` will be non-zero, confirming the cache hit. Cache entries last ~5 minutes (ephemeral), so keep your request interval under that threshold during testing.
