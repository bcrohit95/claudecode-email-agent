# Batch Processing

Claude's Batch API lets you submit large numbers of requests (up to 100,000) in a single call and receive results asynchronously—at half the cost of real-time API calls. Instead of looping through prompts one by one and waiting for each response, you bundle them all into one batch, kick it off, and poll for results when they're ready (usually within minutes to a few hours). This is ideal for offline jobs like summarizing documents, classifying datasets, or generating reports at scale.

## Copy-pasteable example

```python
import anthropic

client = anthropic.Anthropic()

# Create a batch with multiple independent requests
batch = client.messages.batches.create(
    requests=[
        {
            "custom_id": "doc-001",
            "params": {
                "model": "claude-opus-4-7",
                "max_tokens": 256,
                "messages": [{"role": "user", "content": "Summarize: The quick brown fox..."}],
            },
        },
        {
            "custom_id": "doc-002",
            "params": {
                "model": "claude-opus-4-7",
                "max_tokens": 256,
                "messages": [{"role": "user", "content": "Summarize: To be or not to be..."}],
            },
        },
    ]
)

print(f"Batch created: {batch.id}  status: {batch.processing_status}")

# Poll until done
import time
while True:
    batch = client.messages.batches.retrieve(batch.id)
    if batch.processing_status == "ended":
        break
    print("Still processing...")
    time.sleep(60)

# Stream results
for result in client.messages.batches.results(batch.id):
    if result.result.type == "succeeded":
        print(f"[{result.custom_id}]", result.result.message.content[0].text)
```

## Try it yourself

Take any list of 5-10 items you'd normally process in a loop (emails to classify, snippets to translate, questions to answer) and convert the loop into a `client.messages.batches.create()` call. Check your Anthropic console to watch the batch progress and compare the cost vs. what individual calls would have cost.
