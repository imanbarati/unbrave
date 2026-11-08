# Building Unbrave

This is the hard way. Most people should just use the existing free Origin-like solutions linked in the README.

## Prerequisites

- Strong machine (or self-hosted CI runner) with:
  - 16+ GB RAM (32+ recommended)
  - 100+ GB free disk space
  - Fast internet
- Familiarity with Chromium/Brave build system
- Willingness to maintain the fork as upstream moves

## High-level steps

1. **Set up the official Brave build environment**  
   Follow the official docs exactly first:  
   https://github.com/brave/brave-browser/wiki

   Especially the platform-specific pages (Windows / Linux / Android).

2. **Clone and initialize**  
   ```bash
   # Example structure
   mkdir unbrave-src && cd unbrave-src
   git clone https://github.com/brave/brave-core.git src/brave
   cd src/brave
   pnpm run init --target_os=android --target_arch=arm64   # or whatever target
   ```

3. **Rebrand completely**  
   You must change:
   - Application / package name (critical for Android: `com.brave.browser` → something else)
   - All display names, strings, icons, logos
   - Any remaining "Brave" references in UI, about pages, user-agent if desired, etc.
   - Update AndroidManifest.xml, build.gradle files, resources

4. **Strip / disable features**  
   Target the same set Origin removes:
   - Leo AI
   - Rewards / browser ads
   - Wallet / Web3 domains
   - VPN
   - Tor
   - News
   - Speedreader
   - Talk
   - Telemetry / P3A / usage pings
   - etc.

   This is done through a combination of:
   - Feature flags / GN args
   - Removing or ifdef-ing code paths
   - Disabling related components and services

5. **Build**  
   ```bash
   pnpm run build --target_os=android --target_arch=arm64 --target_android_output_format=apk
   ```

6. **Sign and distribute** (your responsibility)  
   You are distributing your own software. Handle signing, updates, and legal compliance yourself.

## GitHub Actions reality

The workflow in this repo is a skeleton only.  
Free GitHub-hosted runners do not have enough disk, memory, or time to complete a real Brave/Chromium Android build.  
You need self-hosted runners with significant resources if you want CI builds.

## Maintenance burden

Upstream Brave and Chromium move fast.  
A stripped + rebranded fork requires ongoing work to stay secure and functional.  
This is not a one-time project.
