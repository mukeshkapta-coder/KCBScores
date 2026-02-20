# Project Structure

## Flutter Project Structure

```
cricheroes_app/
├── android/
│   ├── app/
│   │   ├── build.gradle
│   │   └── src/main/
│   │       ├── AndroidManifest.xml
│   │       └── kotlin/com/cricheroes/cricheroes_app/
│   │           └── MainActivity.kt
│   └── build.gradle
├── lib/
│   ├── main.dart
│   ├── models/
│   │   ├── user_model.dart
│   │   ├── tournament_model.dart
│   │   ├── team_model.dart
│   │   ├── player_model.dart
│   │   ├── match_model.dart
│   │   ├── live_state_model.dart
│   │   ├── event_model.dart
│   │   └── points_table_model.dart
│   ├── services/
│   │   ├── auth_service.dart
│   │   ├── firestore_service.dart
│   │   ├── storage_service.dart
│   │   └── scoring_service.dart
│   ├── providers/
│   │   ├── auth_provider.dart
│   │   ├── tournament_provider.dart
│   │   └── match_provider.dart
│   ├── screens/
│   │   ├── auth/
│   │   │   └── login_screen.dart
│   │   ├── admin/
│   │   │   ├── admin_home.dart
│   │   │   ├── create_tournament_dialog.dart
│   │   │   ├── tournament_admin_dashboard.dart
│   │   │   ├── team_form_screen.dart
│   │   │   ├── player_form_screen.dart
│   │   │   ├── match_form_screen.dart
│   │   │   ├── scoring_console_screen.dart
│   │   │   ├── wicket_dialog.dart
│   │   │   ├── extras_dialog.dart
│   │   │   ├── change_player_dialog.dart
│   │   │   └── toss_dialog.dart
│   │   └── viewer/
│   │       ├── tournament_list_screen.dart
│   │       ├── tournament_home_screen.dart
│   │       ├── match_detail_viewer_screen.dart
│   │       ├── team_roster_screen.dart
│   │       └── player_profile_screen.dart
│   └── utils/
│       └── app_router.dart
├── pubspec.yaml
├── firestore.rules
├── storage.rules
├── README.md
├── SETUP.md
└── .gitignore
```

## Key Files

### Models
- **user_model.dart**: User data model
- **tournament_model.dart**: Tournament data structure
- **team_model.dart**: Team information
- **player_model.dart**: Player details
- **match_model.dart**: Match/fixture data
- **live_state_model.dart**: Real-time match state
- **event_model.dart**: Ball-by-ball events
- **points_table_model.dart**: Points table structure

### Services
- **auth_service.dart**: Firebase Authentication wrapper
- **firestore_service.dart**: Firestore database operations
- **storage_service.dart**: Firebase Storage for images
- **scoring_service.dart**: Live scoring logic with undo

### Providers (State Management)
- **auth_provider.dart**: Authentication state
- **tournament_provider.dart**: Tournament, teams, players, matches
- **match_provider.dart**: Live match state and scoring

### Screens

#### Admin Screens
- **admin_home.dart**: List tournaments, create new
- **tournament_admin_dashboard.dart**: Manage teams, players, fixtures, points
- **team_form_screen.dart**: Create/edit teams with logo upload
- **player_form_screen.dart**: Add players with photo upload
- **match_form_screen.dart**: Create match fixtures
- **scoring_console_screen.dart**: Live scoring interface
- **wicket_dialog.dart**: Record wicket with dismissal mode
- **extras_dialog.dart**: Record extras (Wide, No-ball, etc.)
- **change_player_dialog.dart**: Change striker/non-striker/bowler
- **toss_dialog.dart**: Set toss result

#### Viewer Screens
- **tournament_list_screen.dart**: Browse tournaments
- **tournament_home_screen.dart**: Fixtures, points table, teams
- **match_detail_viewer_screen.dart**: Real-time match view
- **team_roster_screen.dart**: Team players list
- **player_profile_screen.dart**: Player details with photo

## Firebase Collections

```
roles/{uid}
  - role: "admin" | "viewer"

tournaments/{tournamentId}
  - name, description, season, status, createdByUid, createdAt, updatedAt, venues, oversLimit

tournaments/{tournamentId}/teams/{teamId}
  - name, shortName, logoUrl, createdAt

tournaments/{tournamentId}/players/{playerId}
  - name, teamId, photoUrl, role, createdAt

tournaments/{tournamentId}/matches/{matchId}
  - matchNo, teamAId, teamBId, venue, startTime, oversLimit, status, tossWinnerTeamId, electedTo, resultText, updatedAt

tournaments/{tournamentId}/matches/{matchId}/live/state
  - innings, battingTeamId, bowlingTeamId, runs, wickets, overs, balls, target, strikerId, nonStrikerId, bowlerId, lastEventText, lastBallId, isFreeHit, updatedAt

tournaments/{tournamentId}/matches/{matchId}/events/{eventId}
  - ts, innings, over, ball, type, runsBat, runsExtra, totalRuns, batsmanId, nonStrikerId, bowlerId, wicket

tournaments/{tournamentId}/points/table
  - updatedAt, rows[]
```

## Storage Paths

- Team logos: `tournaments/{tournamentId}/teams/{teamId}/logo.jpg`
- Player photos: `tournaments/{tournamentId}/players/{playerId}/photo.jpg`
