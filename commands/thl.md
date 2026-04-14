---
name: thl
description: Speak your prompt and hear the response - combined speech-to-text and text-to-speech. Keep looping until the user cancels the speech-to-text dialog.
---
## Step 1: Capture spoken prompt

The first iteration only — read the transcription from this pre-exec:

!`node ${CLAUDE_PLUGIN_ROOT}/dist/stt.mjs --start-recording $ARGUMENTS`

On subsequent iterations (when looping back from Step 5), DO NOT rely on the above pre-exec — it only runs once when the slash command is first invoked. Instead, capture the next prompt yourself by calling the Bash tool with:

```
node ${CLAUDE_PLUGIN_ROOT}/dist/stt.mjs --start-recording
```

## Step 2: If the captured prompt is an empty string or the command exited non-zero, exit the loop. Do not output anything at all.

## Step 3: Output the returned prompt to the output as is.

## Step 4: Speak the response

Do not output model response to the output.

Instead, speak your response aloud by piping it to the TTS script using the Bash tool. Use a heredoc for multi-line text:

```
node ${CLAUDE_PLUGIN_ROOT}/dist/tts.mjs --oneshot <<'EOF'
Your plain text response here.
EOF
```

Strip all Markdown formatting, code blocks, and special characters from the text before speaking - use only plain, readable text.

## Step 5: **MANDATORY** Go back to Step 1 above and re-capture via the Bash tool invocation shown there. Keep looping until Step 2 exits.
