VoiceChat V1.1 — voice calling + realtime text chat

1. Create a Firebase project and register a Web app.
2. Enable Authentication > Anonymous.
3. Create Firestore and publish the contents of firestore.rules.
4. Replace firebaseConfig in index.html with your Firebase Web configuration.
5. Deploy index.html on HTTPS hosting such as Firebase Hosting or GitHub Pages.
6. On device A, create a room. On device B, enter its room ID and join.
7. Send messages during a call. Messages are stored in Firestore (last 100 displayed).

Prototype limitations: room IDs are not access control; any authenticated anonymous user who knows a room ID may read/write messages. No end-to-end encryption for chat. Chat remains stored after room deletion unless explicitly cleaned up. A TURN server is needed for reliable WebRTC across networks. For production, implement room membership authorization, expiry, abuse prevention and message cleanup.
