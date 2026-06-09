# Batch Processing

## What It Is

Claude Code's Batch Processing (via the Anthropic Batch API) lets you send large numbers of API requests in a single batch job rather than making individual calls one by one. Batches are processed asynchronously — you submit a list of prompts, check back later, and retrieve all results at once. This approach can cut costs by up to 50% compared to standard API calls, making it ideal for bulk tasks like document analysis, code review pipelines, or dataset annotation.

## Example

```python
import anthropic

client = anthropic.Anthropic()

# Create a batch of requests
batch = client.messages.batches.create(
    requests=[
        {
            "custom_id": "review-file-1",
            "params": {
                "model": "claude-opus-4-8",
                "max_tokens": 512,
                "messages": [{"role": "user", "content": "Summarize this code: def add(a,b): return a+b"}],
            },
        },
        {
            "custom_id": "review-file-2",
            "params": {
                "model": "claude-opus-4-8",
                "max_tokens": 512,
                "messages": [{"role": "user", "content": "Summarize this code: def mul(a,b): return a*b"}],
            },
        },
    ]
)

print(f"Batch ID: {batch.id}")
print(f"Status: {batch.processing_status}")

# Later — poll until complete, then retrieve results
# batch_result = client.messages.batches.results(batch.id)
```

## Try It Yourself

Take any repetitive prompt task you run in a loop (e.g., summarizing 100 files) and convert it to a single `client.messages.batches.create()` call. Check batch status with `client.messages.batches.retrieve(batch_id)` and fetch all results with `client.messages.batches.results(batch_id)` once `processing_status == "ended"`. You'll save up to 50% on API costs with no code changes beyond the batching wrapper.
