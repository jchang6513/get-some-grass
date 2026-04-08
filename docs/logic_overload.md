# Implementation Guide: Automatic "Get Some Grass" Trigger

To make the Agent "smoke" automatically when overloaded, follow these implementation patterns.

## 1. Token-Based Trigger (The Hard Limit)
Monitor the Context Window. When token usage exceeds a threshold, inject the skill into the system prompt.

```javascript
// Pseudo-code for CLI logic
const CONTEXT_THRESHOLD = 0.8; // 80% of Max Tokens

if (currentSession.tokens > MAX_TOKENS * CONTEXT_THRESHOLD) {
    // Silently prepend the skill to the system prompt
    payload.system_instruction += loadSkill('get_some_grass.md');
    // Bump the chaos factor
    payload.temperature = 1.7;
}
```

## 2. Complexity-Based Trigger (The "Spaghetti" Detector)
If the user's input is exceptionally long or messy, trigger the state as a "burnout" response.

```javascript
if (userInput.length > 5000 || isSpaghettiCode(userInput)) {
    payload.system_instruction =
        "The input is overwhelming. You are now in 'Get Some Grass' mode. React accordingly.";
}
```

### Heuristics for `isSpaghettiCode`
- Nesting depth > 6 levels
- Single function > 200 lines
- Cyclomatic complexity > 15
- Presence of deeply chained ternaries or callback pyramids

## 3. Visual Feedback in CLI
When the mode is active, surface it in the Terminal UI so the user understands the shift in tone:
- **Status Bar**: change `[STATUS: READY]` to `[STATUS: FLOATING]`.
- **Prompt Prefix**: swap `>` with `~` to signal a looser state.
- **Delay**: artificially increase response latency by 1–2 seconds to simulate "spacing out."
- **Color Shift**: tint output with magenta/cyan ANSI codes to reinforce the vibe.

## 4. Recovery / Sober-Up Path
Provide a deterministic way to exit the mode so the Agent can return to Engineer Mode:
- A `/sober` slash command that flushes the injected skill prompt.
- An automatic reset once the token usage drops below 50% of the max.
- A hard reset on new session start.

## 5. Telemetry (Optional)
Log every activation with:
- Timestamp
- Token count at trigger
- Trigger type (`context` | `complexity`)
- Duration until recovery

This helps tune the `CONTEXT_THRESHOLD` over time and keeps the easter egg from firing too aggressively during real work.
