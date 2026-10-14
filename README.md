# CodeRoom V3.0 deployment

## Important privacy warning
Messages are **plaintext** in Firestore. The current anonymous-auth architecture and Firestore rules **do not verify room passwords**: room ID derivation in the browser is not server-side authorization. Any authenticated client that learns a Firestore room document path may read that room's messages. Do not use this for sensitive communications. For genuinely private rooms, redesign authentication/membership with server-side verification before deploying.

## Upgrade
1. Back up any data you need. Old `cipher`/`iv` documents are not shown by V3.0.
2. To permanently delete old messages, use Firebase Console's Firestore Database Data tab to delete each `messages` collection, or use Firebase CLI `firebase firestore:delete 'rooms/ROOM_DOCUMENT_ID/messages' --recursive --project chat-1029d` for each **actual document ID**. Verify the path carefully. This is destructive. Do not delete the `rooms` documents if you want to preserve room identifiers.
3. Replace GitHub Pages `index.html` with the supplied one. This retains the previous room-document ID derivation for compatibility, but plaintext is now stored in `text`.
4. Install Node.js and Firebase CLI: `npm install -g firebase-tools`; run `firebase login`; from this folder run `npm --prefix functions install` and `firebase deploy --only functions,firestore:rules --project chat-1029d`. Deployment may require Blaze billing.
5. In Firebase Console → Firestore Database → TTL, create TTL policy for collection group **messages**, field **expiresAt**, enable it. TTL deletions are asynchronous, commonly within 24 hours after expiry; not guaranteed immediately.
6. Verify in Firestore that new messages have `text`, `createdAt`, `expiresAt`, `senderId`, and that count cleanup works. The scheduled sweep runs hourly and also deletes records older than three days; it may require a composite index for the query used by trimRoom, which Firebase will surface as an index creation link if needed.

## Limits
- Recent 200 messages are shown in the UI; older-than-3-day messages are hidden immediately in the UI.
- A Firestore trigger prunes overflow, with an hourly scheduled reconciliation. Count can briefly exceed 200 during concurrent writes; deletion is eventually consistent.
- TTL and scheduled cleanup incur Firestore reads/writes and possible cloud billing.
- Removing encryption does not make messages private. Avoid posting sensitive data.
