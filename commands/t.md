---
name: t
description: Speak your prompt using speech-to-text
---
!`node ${CLAUDE_PLUGIN_ROOT}/dist/stt.mjs $ARGUMENTS`

## Step 2: You must output only the prompt returned by the above command to the output first.

## Step 3: Then submit it to the model as the user-entered prompt.