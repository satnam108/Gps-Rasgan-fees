# GPS Rasgan Fees — Android + Firebase Cloud

This project packages the current GPS Rasgan Family Fees UI as an Android application shell and includes Firebase Auth/Firestore dependencies.

## Firebase configuration supplied
1. The supplied `google-services.json` has been placed at `app/google-services.json`.
2. It is configured for Android package `com.gpsrasgan.fees`.
4. Enable Authentication > Email/Password.
5. Create Firestore Database.
6. Add Firestore Security Rules. A recommended starting policy is included in `firestore.rules`.
7. Build with Android Studio (JDK 17 recommended).

## Important
The bundled HTML currently retains its browser/local data layer. Firebase dependencies are prepared in the Android project, but a production cloud migration still needs the HTML data functions to be replaced with Firestore reads/writes and Firebase Authentication role checks.

For true multi-device lifetime data:
- Families, students, sessions, payments and users should be stored in Firestore.
- Do not store passwords in Firestore/localStorage.
- Use Firebase Authentication for passwords.
- Store role (`admin` / `teacher`) in a protected user profile document or custom claims.
- Admin-only writes/deletes should be enforced by Firestore Security Rules, not just UI.

Initial credentials requested by the user:
Username: Ravikumar
Password: Gps#7891

For production, create this account through Firebase Authentication rather than hard-coding the password.


## In-app Teacher Management
- Admin can open **Users** inside the Android app and create a Teacher with name, username, password and mobile.
- The native Android Firebase bridge creates the Firebase Authentication account using an internal email alias (`username@gpsrasgan.local`) and writes the `/users/{uid}` profile with `role: teacher`.
- Admin can list Teacher profiles and remove their Firestore access from the app. Removing the profile blocks app access; deleting/disabling the Firebase Authentication identity itself requires a trusted backend/Admin SDK.
- For cloud Admin operations, sign in through the app using the same Firebase Authentication email/password that owns the Admin Firestore profile. The legacy local `Ravikumar` login is retained only for the offline UI compatibility and is not sufficient for privileged Firebase writes.
