# Batch Processing

## What It Is

Batch processing lets you run Claude on many inputs at once using the Anthropic Batch API, instead of sending one request at a time. This is ideal for tasks like summarizing hundreds of documents, classifying a dataset, or generating variations — it's significantly cheaper (50% cost reduction) and designed for throughput rather than interactivity.

## Copy-Pasteable Example

```python
import anthropic

client = anthropic.Anthropic()

# Create a batch of requests
batch = client.messages.batches.create(
    requests=[
        {
            "custom_id": f"doc-{i}",
            "params": {
                "model": "claude-sonnet-5",
                "max_tokens": 256,
                "messages": [
                    {"role": "user", "content": f"Summarize in one sentence: {doc}"}
                ],
            },
        }
        for i, doc in enumerate([
            "The quick brown fox jumps over the lazy dog.",
            "Machine learning models learn patterns from data.",
            "Claude Code is Anthropic's official CLI for Claude.",
        ])
    ]
)

print(f"Batch ID: {batch.id}")
print(f"Status: {batch.processing_status}")

# Poll for results (in practice, use a webhook or polling loop)
import time
while True:
    result = client.messages.batches.retrieve(batch.id)
    if result.processing_status == "ended":
        break
    print("Still processing...")
    time.sleep(5)

# Iterate over results
for item in client.messages.batches.results(batch.id):
    print(f"{item.custom_id}: {item.result.message.content[0].text}")
```

## Try It Yourself

Take any repetitive task you'd normally loop over synchronously — classifying customer feedback, extracting entities from logs, translating strings — and rewrite it as a batch job. Run it with a small list (3–5 items) first, retrieve the batch by ID, and inspect the per-item results. Notice how each result maps back to your `custom_id` so you can join it with your original data.
