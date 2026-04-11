---
name: h
description: Hear the last response spoken aloud via text-to-speech
args: "[text...]"
---

Launch the text-to-speech dialog to speak text aloud.

If the user provided text arguments, speak that text. Otherwise, speak your most recent response to the user.

Prepare the text to speak, then run this command using the Bash tool, piping the text via stdin:

```
echo "TEXT_TO_SPEAK" | npx tsx ${CLAUDE_PLUGIN_ROOT}/src/tts.ts
```

Replace `TEXT_TO_SPEAK` with the actual text. For multi-line text or text containing quotes, use a heredoc:

```
npx tsx ${CLAUDE_PLUGIN_ROOT}/src/tts.ts --oneshot <<'EOF'
The text to speak goes here.
It can span multiple lines.
EOF
```

This opens a Chrome-based dialog that reads the text aloud using the browser's SpeechSynthesis API. The user can stop, replay, or close the dialog.

Do not include any markdown formatting, code blocks, or special characters in the text - just plain readable text.
