# Unbrave

**Experimental rebranded and feature-stripped browser project based on the open-source Brave/Chromium codebase (MPL-2.0).**

> **This is NOT Brave Origin.**  
> This is NOT affiliated with, endorsed by, or connected to Brave Software in any way.  
> "Brave" and "Brave Origin" are trademarks of Brave Software, Inc.  
> Do not use those names.

## Goal

Provide a starting point for people who want a minimalist, privacy-focused Chromium-based browser with the extra features (Leo AI, Rewards, Wallet, VPN, Tor, News, telemetry, etc.) removed or disabled at the source level, including Android builds.

## Reality Check

- Building a full Chromium-based browser is extremely resource-intensive (tens of GB of source, hours/days of compile time, high RAM requirements).
- Standard GitHub Actions runners **cannot** fully build Brave/Chromium. You will need powerful self-hosted runners or paid CI with large machines.
- Properly stripping features requires deep knowledge of the Brave/Chromium codebase and continuous maintenance as upstream changes.
- This repository is a **skeleton / template**, not a ready-to-use binary distribution.

## Recommended Practical Alternatives (works today)

Instead of compiling from source, use these existing free solutions:

1. **WSL2 port of official Linux Origin Nightly**  
   https://github.com/aivrar/brave-origin-for-windows

2. **Policy-based debloaters for regular Brave**  
   - https://github.com/TahaHydra/Brave-Free-Origin  
   - https://github.com/flyingPenguinW/brave-origin

These give you the Origin-like experience immediately without compiling anything.

## How to actually build from source (serious effort)

1. Follow the official Brave build documentation:  
   https://github.com/brave/brave-browser/wiki

2. Clone and initialize `brave-core` properly.

3. Rename all branding, remove trademarked assets, change package names (especially critical for Android).

4. Disable / remove feature flags and code for:
   - Leo AI
   - Brave Rewards / Ads
   - Crypto Wallet / Web3
   - VPN
   - Tor
   - News
   - Speedreader
   - Telemetry / P3A
   - etc.

5. For Android specifically, use the Android build instructions and change the application ID, package name, and all branding.

## GitHub Actions

A skeleton Android workflow is included under `.github/workflows/`.  
It will almost certainly fail on free GitHub-hosted runners due to disk space, time limits, and memory.  
Use it only as a reference for self-hosted runners.

## License

Any code derived from Brave remains under the Mozilla Public License 2.0.  
You must comply with MPL-2.0 (including providing source for modifications).

## Disclaimer

This project is for educational and personal experimentation purposes only.  
You are solely responsible for any legal, trademark, or distribution issues that arise from using or distributing derivatives of this work.
