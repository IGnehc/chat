# CodeRoom V2.1 — Unlimited participants

## Setup
1. Keep Firebase Authentication > Anonymous enabled and Firestore `(default)`.
2. In Firestore > Rules, replace existing rules with `firestore.rules` and **Publish**. Do not use `allow read, write: if request.auth != null` globally.
3. Replace `index.html` in your GitHub `chat` repository (root) with the included file. GitHub Pages will redeploy.
4. Open your GitHub Pages URL on PC or smartphone. Everyone enters the **same room ID and password**, but their own display name. No manual UID setup or participant cap.
5. Use a unique randomly generated password, preferably **20+ random characters**, shared via a separate trusted channel. Keep it safe: losing it means losing the ability to decrypt history.

## Security caveats
- This is a **prototype**, not an audited secure messenger. The client encrypts messages with AES-GCM, with a key derived via PBKDF2. The server does **not** verify the room password; the secret determines the Firestore document path and encryption key.
- Anyone with the derived room path, including someone who knows/guesses the ID and password, can fetch ciphertext (and post encrypted or malformed messages). The Firestore rules do not cryptographically prove knowledge of the password. Therefore **third-party access prevention is not guaranteed**. Use a high-entropy password and do not send sensitive information.
- Room metadata can be read by authenticated clients that know the derived document ID. Firestore cannot prevent all abuse or enforce password-based authorization using these rules alone.
- No message history migration from V1. For new use, choose a new room ID and strong password.
- Anonymous accounts can change after browser storage is cleared, but the shared password lets you rejoin. No manual UID registration needed.
- Public GitHub Pages source is visible. Managed devices, browser extensions, screenshots, and network activity are not hidden. Follow workplace policies.
- For strong server-enforced password access, use a trusted backend (e.g. Firebase Cloud Functions or Cloud Run) to authenticate and mint scoped access tokens; this version is a simpler client-side encrypted prototype.
