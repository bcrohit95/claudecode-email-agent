# Claude API Basics

The Claude API (via the Anthropic SDK) lets you call Claude programmatically from any Python or TypeScript application — you send a list of messages and get a completion back. The core pattern is just `client.messages.create(model=..., max_tokens=..., messages=[...])`, which returns a structured response object. Understanding this foundation unlocks everything else: tool use, streaming, caching, and multi-turn conversations.

## Copy-pasteable example

```python
import anthropic

client = anthropic.Anthropic()  # reads ANTHROPIC_API_KEY from env

response = client.messages.create(
    model="claude-sonnet-4-6",
    max_tokens=256,
    messages=[
        {"role": "user", "content": "Explain prompt caching in one sentence."}
    ]
)

print(response.content[0].text)
print(f"Tokens used — input: {response.usage.input_tokens}, output: {response.usage.output_tokens}")
```

Install the SDK first:
```bash
pip install anthropic
export ANTHROPIC_API_KEY="sk-ant-..."
python3 your_script.py
```

## Try it yourself

Extend the example above into a simple multi-turn loop:

```python
messages = []
while True:
    user_input = input("You: ")
    messages.append({"role": "user", "content": user_input})
    resp = client.messages.create(model="claude-sonnet-4-6", max_tokens=512, messages=messages)
    reply = resp.content[0].text
    print(f"Claude: {reply}")
    messages.append({"role": "assistant", "content": reply})
```

Notice how you maintain conversation history by appending both user and assistant turns to `messages` — Claude has no memory between API calls, so the full history travels with every request.
