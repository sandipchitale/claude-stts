# claude-stts

A [Claude Code plugin](https://docs.anthropic.com/en/docs/claude-code/plugins) that adds speech-to-text (STT) and text-to-speech (TTS) capabilities to the Claude Code CLI. Speak your prompts instead of typing them, and hear Claude's responses read aloud.

## Features

- **Speech-to-Text (`/t`)** - Dictate your prompt using your microphone via a Chrome-based UI powered by the Web SpeechRecognition API
- **Text-to-Speech (`/h`)** - Have Claude's response (or any text) spoken aloud using the browser's SpeechSynthesis API
- **Combined STT + TTS (`/th`)** - Speak your prompt and automatically hear the response -- a full voice conversation flow

### Voice Commands (STT)

While dictating, you can use voice commands for hands-free editing:

| Command | Action |
|---|---|
| `insert comma / period / question mark / exclamation mark / tab` | Inserts the corresponding punctuation or character |
| `new paragraph` | Ends the current sentence and starts a new paragraph |
| `go to start / go to end` | Moves cursor to the beginning or end of the text |
| `select all` | Selects all text |
| `unselect selection` | Collapses the selection without deleting |
| `delete selection` | Deletes the selected text |
| `undo it / redo it` | Undo or redo the last action |

### Keyboard Shortcuts (STT)

| Shortcut | Action |
|---|---|
| `Ctrl+R` | Toggle speech recognition on/off |
| `Enter` | Send the prompt |
| `Shift+Enter` | Insert a new line |
| `Escape` | Stop recording / cancel |

## How It Works

The plugin launches a Chrome instance (via [chrome-launcher](https://www.npmjs.com/package/chrome-launcher)) in app mode and connects to it using [puppeteer-core](https://www.npmjs.com/package/puppeteer-core). This approach leverages the browser's native `SpeechRecognition` and `SpeechSynthesis` APIs, which provide high-quality speech processing without requiring any external API keys or services.

- **STT flow**: Opens a Chrome window with a textarea where you can type or dictate. Microphone permission is automatically granted via Puppeteer. When you click "Send" or press Enter, the text is printed to stdout, which Claude Code captures and processes as your prompt.
- **TTS flow**: Opens a Chrome window that receives text via Puppeteer's `evaluateOnNewDocument`, then speaks it using `SpeechSynthesisUtterance`. Supports a `--oneshot` flag to automatically close after speaking.

## Architecture

```
claude-stts/
├── .claude-plugin/
│   └── plugin.json          # Plugin manifest
├── commands/
│   ├── t.md                 # /t command - speech-to-text
│   ├── h.md                 # /h command - text-to-speech
│   └── th.md                # /th command - combined STT + TTS
├── src/
│   ├── chrome-sidekick.ts   # Chrome launcher and Puppeteer connection utilities
│   ├── stt.ts               # STT entry point - launches Chrome with speech recognition UI
│   ├── stt_ui.html          # STT frontend - textarea with SpeechRecognition integration
│   ├── tts.ts               # TTS entry point - launches Chrome with speech synthesis UI
│   └── tts_ui.html          # TTS frontend - textarea with SpeechSynthesis integration
├── package.json
└── tsconfig.json
```

## Prerequisites

- **Node.js** (v18+)
- **Google Chrome** or Chromium installed on your system
- A working **microphone** for speech-to-text

## Installation

### As a Claude Code Plugin

Install directly from the repository:

```bash
claude plugin add https://github.com/sandipchitale/claude-stts
```

### For Local Development

```bash
git clone https://github.com/sandipchitale/claude-stts.git
cd claude-stts
npm install
```

Then add it as a local plugin in Claude Code:

```bash
claude plugin add /path/to/claude-stts
```

## Usage

Once installed, use the slash commands in Claude Code:

```
/t              # Speak your prompt
/h              # Hear Claude's last response
/h some text    # Hear specific text spoken aloud
/th             # Speak your prompt and hear the response
```

## Dependencies

- [chrome-launcher](https://www.npmjs.com/package/chrome-launcher) - Launches Chrome with custom flags
- [puppeteer-core](https://www.npmjs.com/package/puppeteer-core) - Connects to and controls the Chrome instance
- [commander](https://www.npmjs.com/package/commander) - CLI argument parsing

## License

MIT

## Author

Sandip Chitale
