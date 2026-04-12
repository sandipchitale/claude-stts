---
name: th
description: Speak your prompt and hear the response - combined speech-to-text and text-to-speech
---
## Step 1:

!`node ${CLAUDE_PLUGIN_ROOT}/dist/stt.mjs $ARGUMENTS`

##S tep 2: If the above command returned empty string or exited with non zero status exit the loop. Do not output anything at all.

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

## Step 5:

Go back to Step 1 above.

