# Claude API Basics

The Claude API lets you send messages to Claude programmatically using the Messages API (`POST /v1/messages`). You authenticate with an API key, choose a model (default to `claude-opus-5` for best results), and pass a list of messages — Claude returns a response you can parse directly. For most tasks, enable adaptive thinking (`thinking: {type: "adaptive"}`) to let the model decide how much reasoning to apply.

## Copy-Pasteable Example

```python
import anthropic

client = anthropic.Anthropic()  # uses ANTHROPIC_API_KEY env var

response = client.messages.create(
    model="claude-opus-5",
    max_tokens=1024,
    thinking={"type": "adaptive"},
    messages=[
        {"role": "user", "content": "Explain what the Claude API is in one sentence."}
    ]
)

# Extract the text from the response
for block in response.content:
    if block.type == "text":
        print(block.text)
```

## Try It Yourself

Set your `ANTHROPIC_API_KEY` environment variable (`export ANTHROPIC_API_KEY=sk-ant-...`), install the SDK (`pip install anthropic`), and run the example above. Then try changing the `content` to a different question — notice how the response structure stays the same regardless of what you ask.
