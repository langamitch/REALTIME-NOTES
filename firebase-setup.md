# Firebase Setup Guide

## Quick Setup

### 1. Firebase Project Setup

1. Go to [Firebase Console](https://console.firebase.google.com/)
2. Create new project
3. Enable Authentication (Email/Password)
4. Create Firestore Database (test mode)

### 2. Deploy Security Rules

Copy the rules from `firestore.rules` to Firebase Console:

1. Go to Firestore Database → Rules
2. Replace existing rules with:

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /users/{userId} {
      allow read, write: if request.auth != null && request.auth.uid == userId;
      match /{subcollection}/{documentId} {
        allow read, write: if request.auth != null && request.auth.uid == userId;
      }
    }
  }
}
```

### 3. Database Structure

The app uses this structure:

```
users/{userId}/
  activeDevices/{ipAddress}/
    - ipAddress, lastActive, role, userAgent, timestamp
  notes/shared_note/
    - content, updatedAt, updatedBy
```

### 4. Testing

1. Open `index.html` in browser
2. Sign up with email/password
3. Test real-time sync between devices
4. Check Firebase Console for data

## Security Notes

- Users can only access their own data
- Authentication required for all operations
- IP addresses used as device identifiers
- Automatic cleanup of disconnected devices
