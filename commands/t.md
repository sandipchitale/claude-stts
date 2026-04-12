---
name: t
description: Speak your prompt using speech-to-text
---

## Step 1: 

Launch the speech-to-text dialog so the user can dictate their prompt.

Run this command using the Bash tool:

```
node ${CLAUDE_PLUGIN_ROOT}/dist/stt.mjs
```

This opens a Chrome-based dialog where the user can type or speak (using the browser's SpeechRecognition API). The dialog supports voice commands for punctuation, navigation, and editing.

When the user clicks "Send" (or presses Enter), the spoken/typed text is printed to stdout.

## Step 3:

Take the captured text and process it as if the user had typed it as their prompt. Do whatever the text says.
