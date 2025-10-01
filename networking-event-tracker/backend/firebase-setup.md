# Firebase Setup Guide

## Quick Setup for Demo

### 1. Firebase Console Setup (5 minutes)

1. Go to [Firebase Console](https://console.firebase.google.com/)
2. Click "Create a project" or "Add project"
3. Enter project name: `eventtracker-demo` (or any name)
4. Accept terms and click "Continue"
5. Disable Google Analytics (optional for demo)
6. Click "Create project"

### 2. Enable Firestore Database

1. In your Firebase project, click "Firestore Database"
2. Click "Create database"
3. Choose "Test mode" for quick setup (demo purposes)
4. Select your region and click "Done"

### 3. Get Firebase Configuration

1. Click the gear icon ⚙️ next to "Project Overview"
2. Click "Project settings"
3. Scroll down to "Your apps" section
4. Click the web icon `</>`
5. Enter app nickname: `eventtracker-web`
6. Don't enable Firebase Hosting (for now)
7. Click "Register app"
8. Copy the Firebase configuration object

### 4. Update Frontend Configuration

Replace the config in `frontend/src/firebase.ts`:

```typescript
const firebaseConfig = {
  apiKey: "your-api-key",
  authDomain: "your-project.firebaseapp.com",
  projectId: "your-project-id",
  storageBucket: "your-project.appspot.com",
  messagingSenderId: "123456789",
  appId: "your-app-id"
};
```

### 5. Add Demo Data (Optional)

In your React app, you can seed demo data by calling:

```typescript
import { seedDemoData } from './utils/demoData';

// Call this in your component or console
seedDemoData();
```

## Security Rules (Production)

For production, update Firestore rules in Firebase Console:

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    // Allow read/write access to attendees for authenticated users
    match /attendees/{document} {
      allow read, write: if request.auth != null;
    }

    // Allow read access to events for all users
    match /events/{document} {
      allow read: if true;
      allow write: if request.auth != null;
    }
  }
}
```

## Testing Your Setup

1. Start your React app: `npm start`
2. Open browser console
3. Run: `seedDemoData()` (if you added the import)
4. Check your Firebase Firestore console for data
5. Verify real-time updates work in your app

## Troubleshooting

- **Permission denied**: Check Firestore rules are in "test mode"
- **Module not found**: Ensure Firebase dependencies are installed
- **Real-time not working**: Verify Firestore real-time listeners are set up correctly

## Quick Commands

```bash
# Install dependencies
npm install firebase

# Start development server
npm start

# Build for production
npm run build
```

---
*This setup gets you running in under 10 minutes for demo purposes.*