# Android-specific notes for Unbrave

## Critical requirements

1. **Change the package / application ID**  
   Official Brave uses something like `com.brave.browser`.  
   You **must** change this to your own unique ID (e.g. `org.unbrave.browser` or similar).  
   Failure to do so will cause conflicts with the real Brave app and is not acceptable.

2. **Rebrand everything visible**  
   - App name
   - Icons (all densities)
   - Splash screens
   - About page / version strings
   - Any notification channels, deep links, etc. that contain "Brave"

3. **Feature stripping on Android**  
   Many Origin features are controlled by feature flags and component lists.  
   You will need to audit:
   - `brave_features.cc` / related feature lists
   - Android-specific Java/Kotlin and native code that initializes Leo, Rewards, Wallet, VPN, etc.
   - Preferences and UI that expose those features

4. **Build command example**  
   ```bash
   pnpm run build --target_os=android --target_arch=arm64 --target_android_output_format=apk
   ```

5. **Signing**  
   You must sign the APK/AAB with your own key.  
   Do not use any Brave signing keys.

## GitHub Actions

The included `android-build.yml` is only a skeleton.  
It will not produce a real APK on free runners.  
Use it as a starting point for self-hosted runners that have enough disk and RAM.

## Recommendation

For most users who just want a free minimalist experience on Android, the official Brave Origin upgrade (paid) or carefully applying policies / using debloat methods is far more practical than maintaining a full Android fork.
