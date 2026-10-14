# CodeRoom Firebase connected build

Firebase project: chat-1029d.

1. Upload `coderoom-v1-connected.html` as `index.html` to a secure HTTPS hosting site (such as GitHub Pages). Do not open as file://.
2. Open on both PCs, read each anonymous UID from the login screen. Do not clear browser data before setup.
3. Install matching Firestore rules restricting both UIDs (ask assistant to prepare exact rules).
4. After rules publish, join with same room ID and password on both PCs.

NOTE: Room password proof is stored as an unsalted SHA-256 hash tied to room ID; it is not end-to-end encryption. Do not send sensitive data. A room join can be restricted to two allowlisted UIDs using rules. Firebase project settings are public client identifiers, not admin secrets.
