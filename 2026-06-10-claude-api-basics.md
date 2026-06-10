# Claude API Basics

The Claude API (provided by Anthropic) lets you programmatically send messages to Claude models and receive responses — it's the backbone of every Claude Code integration, custom agent, and automated workflow. You authenticate with an API key, choose a model (e.g. `claude-sonnet-4-6`), and send a JSON payload with a list of messages; Claude returns a completion you can use in any language or framework. Understanding the basics — models, message format, max_tokens, and the `content` array in responses — unlocks everything else in Claude Code.

## Copy-Pasteable Example

```python
import anthropic

client = anthropic.Anthropic()  # reads ANTHROPIC_API_KEY from env

message = client.messages.create(
    model="claude-sonnet-4-6",
    max_tokens=256,
    messages=[
        {"role": "user", "content": "Explain Claude API Basics in one sentence."}
    ]
)

print(message.content[0].text)
```

Install the SDK first:
```bash
pip install anthropic
export ANTHROPIC_API_KEY="your-key-here"
python3 script.py
```

## Try It Yourself

Open a terminal, set your `ANTHROPIC_API_KEY`, paste the snippet above, and swap in a different model ID like `claude-haiku-4-5-20251001` to see how response speed and style differ. Then try adding a `system` parameter (top-level, alongside `messages`) to give Claude a persona — e.g. `system="You are a pirate."` — and observe how it changes every reply.
