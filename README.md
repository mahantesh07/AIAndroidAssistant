# AI Android Assistant — Java starter project

This ZIP contains a starter Android application and a Spring Boot backend skeleton.

## What is included

### Android app
- Java Android application with a chat-style screen.
- Text command entry.
- Voice input using Android's speech-recognition activity.
- Spoken responses using Android TextToSpeech.
- User-approved MediaProjection screen-capture flow; one frame is saved to the app cache as `latest-screen.png`.
- Accessibility service with basic `tap <visible text>`, `type <text>` and `back` actions.

### Spring Boot backend
- Spring Boot 3.4.4 / Java 17 starter.
- `POST /api/assistant/plan` placeholder endpoint.
- No API key is embedded in the Android application.

## Important status

This is an initial source-code MVP, not a finished AI agent and not a prebuilt APK. The AI vision/reasoning connection is deliberately a placeholder; the Android app currently handles a small set of local accessibility commands. The next development phase is to send the captured screenshot and command to the backend, connect a vision-capable model, validate its structured action plan, and add action-by-action verification.

The project has not been built or tested on a physical Android device in this environment. Android Studio / Android SDK is required to build the APK.

## Android build

1. Open the `AIAndroidAssistant` folder in Android Studio.
2. Allow Gradle sync and install Android SDK Platform 35 if prompted.
3. Build > Build Bundle(s) / APK(s) > Build APK(s).
4. Install the generated debug APK on your Android phone.
5. Open the app and grant microphone permission if Android requests it.
6. Tap **Enable accessibility service** and enable **AI Assistant Automation** only if you want to use the automation functions.
7. Tap **Capture** and approve Android's screen-sharing prompt when you want to capture a screen.

## Backend run

From the `backend` directory, run:

```bash
gradle bootRun
```

The placeholder endpoint is `POST http://localhost:8080/api/assistant/plan` with JSON such as:

```json
{
  "command": "Find the Settings button",
  "screenDescription": "Optional screen context"
}
```

For a physical phone, `localhost` means the phone itself, not your development computer. Configure the backend base URL to your computer's reachable LAN address during local testing, and use HTTPS plus authentication for deployment.

## Safety and platform constraints

- Android requires explicit user approval for screen capture.
- Accessibility access must be enabled by the device user in Android Settings.
- Some secure windows, protected content, and app-specific screens cannot be captured or automated.
- Payment, deletion, sending, account changes, and other sensitive actions should require explicit confirmation.
- Do not use this project to bypass app security, capture credentials, or automate actions without the device owner's consent.
- The sample uses cleartext networking only as a local-development convenience; remove it and use HTTPS before production.
