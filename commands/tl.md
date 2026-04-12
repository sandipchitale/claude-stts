---
name: t
description: Speak your prompt using speech-to-text. Keep looping until the user cancels the speech-to-text dialog.
---
## Step 1

!`node ${CLAUDE_PLUGIN_ROOT}/dist/stt.mjs --start-recording $ARGUMENTS`

## Step 2: If the above command returned an empty string or exited with a non-zero status, exit the loop. Do not output anything at all.

## Step 3: You must output only the prompt returned by the above command to the output first.

## Step 4: Then submit it to the model as the user-entered prompt.

## Step 5:

Go back to Step 1 above.