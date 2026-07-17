## Plan: Full-Featured Y2kTrees Chatroom & Trading App

Build a production-ready web app with user profiles, persistent messaging, admin controls, and a trading marketplace. The current WebSocket server broadcasts raw messages; we'll extend it with user management, message persistence, MAC address tracking, admin panels, and a new trading feature.

### Steps

1. **Refactor backend to track users**: Extend `handle()` in [main.py](main.py) to assign each connection a unique ID, store user metadata (MAC address, nickname, profile pic URL), and manage a users registry.

2. **Implement message persistence**: Add a database layer (SQLite or similar) to store messages with timestamps, user IDs, and content; load message history when users connect.

3. **Enhance frontend with user setup**: Add modal/form for nickname and optional profile picture upload on first connection; display user-aware messages (sender name, timestamp).

4. **Create admin panel**: Add backend endpoints to verify admin status (via MAC address whitelist), implement message deletion by ID, and provide admin UI controls.

5. **Build trading page**: Create new HTML page with form to post trade requests (item needed, offer, availability window); add database table for trades; display active trades with filtering.

6. **Add file upload support**: Implement profile picture upload handler on backend (store to disk or cloud); serve uploaded images in chat and trading profiles.

7. **Polish mobile UX**: Optimize HTML/CSS for small screens, ensure touch-friendly buttons, hide/show chat and trading pages via tabs or navigation.

### Further Considerations

1. **MAC address acquisition method**: Browser JS cannot directly read MAC addresses (security). Options: (A) Use local IP as proxy + server-side MAC mapping / (B) Generate persistent device ID via localStorage / (C) Combine MAC detection for internal networks using ARP or similar. Recommendation: Use localStorage-based device ID for simplicity, with optional manual admin assignment.

2. **User authentication for admins**: How will admins be identified? (A) Hardcoded whitelist of device IDs / (B) Password on first admin setup / (C) Special admin nickname. Recommendation: Combination of whitelisted device ID + admin password for security.

3. **Data persistence approach**: SQLite for simplicity or dedicated database (PostgreSQL)? Recommendation: SQLite for now, easily migrates to PostgreSQL later.

4. **Profile picture storage**: (A) Base64 in database / (B) Files on disk / (C) Cloud storage. Recommendation: Disk storage for simplicity, with 5MB size limit and image validation.