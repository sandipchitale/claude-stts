---
name: th
description: Speak your prompt and hear the response - combined speech-to-text and text-to-speech
---
!`node ${CLAUDE_PLUGIN_ROOT}/dist/stt.mjs $ARGUMENTS`

## Step 2: Output the returned prompt to the output as is.

## Step 3: Speak the response

Do not output model response to the output.

Instead, speak your response aloud by piping it to the TTS script using the Bash tool. Use a heredoc for multi-line text:

```
node ${CLAUDE_PLUGIN_ROOT}/dist/tts.mjs --oneshot <<'EOF'
Your plain text response here.
EOF
```

Strip all Markdown formatting, code blocks, and special characters from the text before speaking - use only plain, readable text.
