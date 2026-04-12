---
name: th
description: Speak your prompt and hear the response - combined speech-to-text and text-to-speech
---

This command combines STT and TTS into a single flow: the user speaks their prompt, you process it, then speak your response back.

## Step 1: Capture the spoken prompt

Run the speech-to-text dialog using the Bash tool:

```
node ${CLAUDE_PLUGIN_ROOT}/dist/stt.mjs
```

This opens a Chrome dialog where the user can speak or type their prompt. When they click "Send" or press Enter, the text is printed to stdout.

## Step 2: Process the prompt

Take the captured text and process it as the user's prompt. Do whatever the text says. Produce your response.

## Step 3: Speak the response

After you have responded, speak your response aloud by piping it to the TTS script using the Bash tool. Use a heredoc for multi-line text:

```
node ${CLAUDE_PLUGIN_ROOT}/dist/tts.mjs --oneshot <<'EOF'

Your plain text response here.
EOF
```

Strip all Markdown formatting, code blocks, and special characters from the text before speaking - use only plain, readable text.
