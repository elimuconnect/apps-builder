# Elimu Connect Offline (Android / Kotlin)

This is the first native Android project shell built around the uploaded `ELIMU-CONNECT--main` website source. It packages the website in `app/src/main/assets/site/` and serves it through AndroidX WebViewAssetLoader at the HTTPS-style local origin `https://appassets.androidplatform.net/`.

## Included
- Kotlin Android app (min SDK 23 / Android 6.0+)
- WebView configured for local HTML/JS and DOM storage
- Local website copy (260 HTML pages plus supplied assets)
- Rewrites of recognised first-party GitHub Pages / Wisdom App links to matching packaged files
- External links open in the device browser and therefore need internet
- App starts at `appaccessdaily.html`

## Build
1. Install Android Studio (current stable) and Android SDK Platform 35.
2. Open this folder (`ElimuConnectOffline`) in Android Studio.
3. Allow Gradle sync and install the requested Android Gradle Plugin/Kotlin plugin if prompted.
4. Connect an Android phone with USB debugging enabled, or create an emulator.
5. Select **Build > Build Bundle(s) / APK(s) > Build APK(s)**.
6. Android Studio will show the generated APK location.

A Gradle wrapper is not included; Android Studio can use its embedded Gradle installation or you can add a wrapper from the IDE. JDK 17 is required.

## Important: daily payment/access status
The supplied `appaccessdaily.html` currently contains a browser-side access timer and opens the Paystack Shop payment URL. That existing behavior is retained in the packaged HTML. It stores the paid-until timestamp and payment reference in browser `localStorage`. **This is not secure payment verification**: a reference in a URL is not proof that Paystack accepted a payment, and local storage/device time can be manipulated.

Before public release, replace the browser-side unlock with a server-side payment verification endpoint: the Android app should submit the Paystack transaction reference to your backend; the backend must verify it with Paystack using the secret key (never put the Paystack secret key in the APK), then issue a short-lived signed entitlement that the app can cache for offline use until expiry. No backend API credentials or verification endpoint were included in the uploaded ZIP, so this project does not claim to provide secure automatic payment verification yet.

## Offline limitations
- Pages and resources physically included in the APK can work offline if they do not depend on remote APIs/CDNs.
- Links to third-party sites, hosted videos, AI services, payment pages, maps/GPS services and remote databases remain online-only.
- Some pages may still contain remote scripts, stylesheets, fonts or API calls. Those need page-by-page dependency review and local bundling to achieve complete offline behavior.
- A website page can be packaged; third-party websites cannot be copied wholesale without permission/licence.

## Source transformation report
See `offline-link-report.csv` for first-party links rewritten to local files and links that could not be matched to a supplied file.
