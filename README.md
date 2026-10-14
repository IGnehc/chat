# CodeRoom v1.0

A two-person VS Code-inspired browser chat, built with Firebase Authentication and Firestore.

## Setup
1. Create a Firebase project at https://console.firebase.google.com/ .
2. In Authentication > Sign-in method, enable **Anonymous**.
3. Create a Firestore database (production mode is fine).
4. Open Firestore Database > Rules, replace the contents with `firestore.rules`, then Publish.
5. In Project settings > Your apps, register a Web app and copy its Firebase config into the `firebaseConfig` object near the bottom of `index.html`.
6. Host `index.html` on an HTTPS site (e.g. GitHub Pages or Firebase Hosting). Avoid opening with file://.
7. Open the same site on both computers. Enter the same room ID and room password; use different display names. The first user creates the room, the second joins.

## Important security limitations
- This is a **prototype**, not an audited secure messenger.
- The room password is SHA-256 hashed client-side; **it is not end-to-end encryption**. Firestore stores messages as plaintext, visible to project administrators.
- Authenticated users can read room metadata including the password verifier. Choose a long, random room password. Do not reuse personal passwords.
- Membership is attached to Firebase Anonymous Auth UID; clearing site data, changing browsers or using private browsing may lose access to a full room. `Leave` only closes the current session, not the membership slot.
- Online presence is not implemented; the member counter is registered members, not online users.
- Messages are limited to the latest 200 by query, and there is no retention policy, deletion, or account recovery yet.
- Use only on devices/networks where this is permitted. This UI does not conceal traffic from employer administration or monitoring.
