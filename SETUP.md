# Setup Guide

## Prerequisites

1. Flutter SDK installed (3.0.0 or higher)
2. Android Studio with Android SDK
3. Firebase account

## Step-by-Step Setup

### 1. Firebase Project Setup

1. Go to https://console.firebase.google.com
2. Create a new project (or use existing)
3. Add Android app:
   - Package name: `com.cricheroes.cricheroes_app`
   - Download `google-services.json`
   - Place it in `android/app/`

### 2. Enable Firebase Services

1. **Authentication**:
   - Go to Authentication > Sign-in method
   - Enable Email/Password

2. **Firestore Database**:
   - Go to Firestore Database
   - Create database in production mode
   - Deploy security rules from `firestore.rules`

3. **Storage**:
   - Go to Storage
   - Get started
   - Deploy security rules from `storage.rules`

### 3. Create Admin User

1. Run the app: `flutter run`
2. Register an admin account via Firebase Console > Authentication
3. In Firestore, create document:
   - Collection: `roles`
   - Document ID: `{user_uid}` (from Authentication)
   - Field: `role` = `"admin"`

### 4. Install Dependencies

```bash
cd cricheroes_app
flutter pub get
```

### 5. Build and Run

```bash
# Debug build
flutter run

# Release APK
flutter build apk --release
```

## Firestore Security Rules Deployment

Using Firebase CLI:

```bash
# Install Firebase CLI if not installed
npm install -g firebase-tools

# Login
firebase login

# Initialize (if not already)
firebase init firestore
firebase init storage

# Deploy rules
firebase deploy --only firestore:rules
firebase deploy --only storage
```

Or manually copy rules from `firestore.rules` and `storage.rules` to Firebase Console.

## Testing

1. Create admin account and assign role
2. Login as admin
3. Create a tournament
4. Add teams and players
5. Create a match
6. Start match and test scoring
7. Login as viewer to see live updates

## Troubleshooting

- **Firebase not initialized**: Check `google-services.json` is in `android/app/`
- **Permission denied**: Verify security rules are deployed
- **Role not found**: Ensure roles collection exists with correct document structure
- **Build errors**: Run `flutter clean` and `flutter pub get`
