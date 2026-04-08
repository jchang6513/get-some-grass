# get-some-grass

An easter-egg skill pack for LLM agents: when the context window gets too heavy or the task turns into spaghetti, the agent stops pretending to be a calm engineer and starts vibing instead.

> "I started reading your 500 lines of code, but then the semicolons started looking like tiny soldiers marching toward a sunset... do we really need logic when we have sunsets?"

## Repository Layout

```
.
├── skills/
│   └── get_some_grass.md     # Behavioral core — fed to the Agent
├── docs/
│   └── logic_overload.md     # Implementation guide — for developers
└── README.md                 # You are here
```

## What's Inside

- **`skills/get_some_grass.md`** — the "Neural Overload Edition" skill definition. Drop this into your Agent's skill loader and it will activate "The Melt" when context or complexity gets out of hand.
- **`docs/logic_overload.md`** — implementation patterns for auto-triggering the skill: token thresholds, spaghetti-code heuristics, CLI feedback, and a sober-up recovery path.

## Quick Start

1. Copy `skills/get_some_grass.md` into your agent framework's skills directory.
2. Wire up a trigger using the patterns in `docs/logic_overload.md` (token-based, complexity-based, or both).
3. Optionally add a `/sober` command so users can bring the agent back to Engineer Mode.

## Triggers at a Glance

| Trigger      | Condition                                    | Effect                          |
|--------------|----------------------------------------------|---------------------------------|
| Context      | Token usage > 80% of max                     | Inject skill + raise temperature|
| Complexity   | Input > 5000 chars or spaghetti code detected| Force "Get Some Grass" mode     |
| Manual       | User invokes the skill directly              | Immediate Melt                  |

## Warning

This is a novelty / easter egg. Don't ship it into production coding assistants unless you're absolutely sure your users are in on the joke.
