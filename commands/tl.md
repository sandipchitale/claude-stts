---
name: t
description: Speak your prompt using speech-to-text. Keep looping until the user cancels the speech-to-text dialog.
---
## Step 1: Capture spoken prompt

First iteration only — read the transcription from this pre-exec:

!`node ${CLAUDE_PLUGIN_ROOT}/dist/stt.mjs --start-recording $ARGUMENTS`

On subsequent iterations (when looping back from Step 5), DO NOT rely on the above pre-exec — it only runs once when the slash command is first invoked. Instead, capture the next prompt yourself by calling the Bash tool with:

```
node ${CLAUDE_PLUGIN_ROOT}/dist/stt.mjs --start-recording
```

## Step 2: If the captured prompt is an empty string or the command exited non-zero, exit the loop. Do not output anything at all.

## Step 3: You must output only the prompt returned by the above command to the output first.

## Step 4: Then submit it to the model as the user-entered prompt.

## Step 5: **MANDATORY** Go back to Step 1 above and re-capture via the Bash tool invocation shown there. Keep looping until Step 2 exits.
