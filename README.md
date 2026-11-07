# WaveKat flows

The official marketplace of call flows for WaveKat Voice and `wk`.

A call flow is a small YAML file that says what happens on an automated
phone call: what is said, which keys do what, and when to hang up. Flows
are data, not code. Installing one never runs anything on your computer.

## Use a flow

```sh
wk call +14155550123 --flow ask \
  --var question="Deploy to production now?" \
  --var option1=Yes --var option2="No, wait" \
  --wait --json
```

Flows from this marketplace install on first use. You can also install
them yourself:

```sh
wk voice flows install ask
wk voice flows show ask        # what it says and which variables it takes
```

No WaveKat account is needed.

## Flows

| Flow | What it does | Variables |
|---|---|---|
| `ask` | Asks one question. The person answers with a key, 1 to 4; 9 repeats it. | `intro`, `question`, `option1` to `option4` |
| `notify` | Says a message twice, then hangs up. | `intro`, `message` |

## Make your own marketplace

Any public GitHub repo with a `marketplace.json` at its root is a
marketplace:

```json
{
  "name": "acme",
  "description": "Acme's call flows.",
  "flows": [
    { "name": "standup", "description": "Daily standup reminder.", "path": "flows/standup.yaml" }
  ]
}
```

Add it and install from it:

```sh
wk voice flows marketplace add acme/flows
wk voice flows install standup@acme
```

Only flows from this official marketplace install by themselves. Flows
from other marketplaces must be installed with `flows install` first.
Before saving a flow, `install` shows any phone numbers it can transfer a
call to.

## Contributing

Open a pull request with a new flow in `flows/` and an entry in
`marketplace.json`. Keep prompts short and plain; they are read aloud on
a phone line.
