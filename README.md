# CodeRoom V2.7 — Grayscale Terminal Chat

This release changes only the chat presentation from V2.6.

- All messages use neutral gray text and separators, without colored bubbles.
- Your messages indent by 12px; other messages remain left-aligned.
- Consecutive messages from the same sender hide repeated username and timestamp.
- Keeps Escape to hide chat, Alt+Q to restore, editable scratchpad, and adjustable panel height.
- No Firebase schema or rules changes required.

## Deploy
Replace `index.html` in the GitHub Pages repository, commit, wait for deployment, then hard-refresh.

## Privacy
The code-mode display is a visual privacy feature, not a substitute for Firestore access controls. Keep appropriate Firebase security rules; do not use broad anonymous-user access rules for sensitive chats.
