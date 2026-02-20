# CricHeroes Tournament Scoring System

A Flutter Android app with Firebase backend for managing cricket tournaments, teams, players, and live match scoring.

## Features

### Admin Features
- Create and manage tournaments
- Create teams with logos
- Add players with photos
- Create match fixtures
- Live ball-by-ball scoring
- Record wickets with dismissal modes
- Handle extras (Wide, No-ball, Bye, Leg-bye)
- Undo last ball
- Complete innings and matches

### Viewer Features
- View tournament details
- Browse teams and players with photos
- View fixtures and points table
- Real-time live match updates

## Setup Instructions

### 1. Firebase Setup

1. Create a Firebase project at https://console.firebase.google.com
2. Enable Authentication (Email/Password)
3. Create a Firestore database
4. Enable Firebase Storage
5. Add Android app to Firebase project
6. Download `google-services.json` and place it in `android/app/`

### 2. Configure Firebase

1. Update `lib/main.dart` with your Firebase configuration (or use `google-services.json`)

### 3. Set Up Admin Role

After creating an admin user account, manually add the role in Firestore:

```
Collection: roles
Document ID: {user_uid}
Fields:
  role: "admin"
```

For viewer accounts:
```
Collection: roles
Document ID: {user_uid}
Fields:
  role: "viewer"
```

### 4. Deploy Security Rules

1. Deploy Firestore rules:
   ```bash
   firebase deploy --only firestore:rules
   ```

2. Deploy Storage rules:
   ```bash
   firebase deploy --only storage
   ```

### 5. Install Dependencies

```bash
flutter pub get
```

### 6. Run the App

```bash
flutter run
```

## Firestore Data Model

### Collections

- `tournaments/{tournamentId}`
  - name, description, season, status, createdByUid, createdAt, updatedAt, venues, oversLimit

- `tournaments/{tournamentId}/teams/{teamId}`
  - name, shortName, logoUrl, createdAt

- `tournaments/{tournamentId}/players/{playerId}`
  - name, teamId, photoUrl, role, createdAt

- `tournaments/{tournamentId}/matches/{matchId}`
  - matchNo, teamAId, teamBId, venue, startTime, oversLimit, status, tossWinnerTeamId, electedTo, resultText, updatedAt

- `tournaments/{tournamentId}/matches/{matchId}/live/state`
  - innings, battingTeamId, bowlingTeamId, runs, wickets, overs, balls, target, strikerId, nonStrikerId, bowlerId, lastEventText, lastBallId, isFreeHit, updatedAt

- `tournaments/{tournamentId}/matches/{matchId}/events/{eventId}`
  - ts, innings, over, ball, type, runsBat, runsExtra, totalRuns, batsmanId, nonStrikerId, bowlerId, wicket

- `tournaments/{tournamentId}/points/table`
  - updatedAt, rows (array of team points data)

- `roles/{uid}`
  - role ("admin" | "viewer")

## Storage Paths

- Team logos: `/tournaments/{tournamentId}/teams/{teamId}/logo.jpg`
- Player photos: `/tournaments/{tournamentId}/players/{playerId}/photo.jpg`

## Building APK

```bash
flutter build apk --release
```

The APK will be generated at: `build/app/outputs/flutter-apk/app-release.apk`

## Notes

- The app requires internet connection for Firebase services
- Admin users must be manually assigned roles in Firestore
- Points table is updated manually by admin after match completion
- Undo functionality recomputes live state from remaining events
