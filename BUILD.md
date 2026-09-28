# Changeover Planner: build the APK (free, one phone)

## 1. Install once on your PC
- Node.js 22 or newer
- Android Studio (it brings its own Java)

## 2. Google Drive access (free)
1. console.cloud.google.com -> new project.
2. APIs & Services -> Library -> enable "Google Drive API".
3. OAuth consent screen -> External -> add your Gmail as a Test user.
   Then click "Publish app" (In production). This avoids Google asking you to sign in again every 7 days.
4. Credentials -> Create credentials -> OAuth client ID -> Application type: "TVs and Limited Input devices".
5. Copy the Client ID and Client secret. You paste both into the app later.

## 3. Build (in this folder, in a terminal)
    npm install
    npx cap add android
    npx @capacitor/assets generate --android      (optional: app icon)
    npx cap sync android

## 4. Allow exact alarms
Open android/app/src/main/AndroidManifest.xml and add these lines just above <application ...>:

    <uses-permission android:name="android.permission.USE_EXACT_ALARM" />
    <uses-permission android:name="android.permission.SCHEDULE_EXACT_ALARM" />
    <uses-permission android:name="android.permission.POST_NOTIFICATIONS" />

## 5. Make the APK
    npx cap open android
In Android Studio: Build -> Build Bundle(s) / APK(s) -> Build APK(s).
File: android/app/build/outputs/apk/debug/app-debug.apk
Copy it to the phone and install it (allow "install unknown apps" when asked).

## 6. First run on the phone
1. Settings tab -> paste Client ID and Client secret -> Sign in -> enter the code at google.com/device.
2. Tap "Allow alarms" and accept. Tap "Test alarm", lock the phone, and check it rings after 10 seconds.
3. Phone settings -> Apps -> Changeover Planner -> Battery -> Unrestricted.
4. Phone settings -> Notifications -> Changeover alarms -> pick an alarm tone, allow override of Do Not Disturb.
