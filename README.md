# M-U-N Gallery — Your Moments, Beautifully.

A flagship offline Android gallery application built with modern Kotlin and Jetpack Compose, featuring an exquisite dark **Liquid Glass** aesthetic, real device MediaStore indexing, ExoPlayer video playback, albums, persistent favorites, and a built-in photo editor.

---

## Features

- **Real Device MediaStore Access:** Reads and manages photos and videos stored locally on device without cloud uploads or account logins.
- **Dark Liquid Glass UI:** Frosted glass cards, customized reflection highlights, thin borders, and customizable neon glows.
- **Full-Screen Photo Viewer:** Horizontal swipe, pinch-to-zoom, double-tap zoom, file details sheet, favorite, share, edit, and delete.
- **Media3 / ExoPlayer Video Player:** Hardware-accelerated video playback with seekbar, duration timestamps, mute toggle, and auto-hiding glass controls.
- **Device Albums:** Automatically detects local folders (Camera, Screenshots, Downloads, WhatsApp, etc.).
- **Persistent Favorites:** Backed by a local Room database (`mun_gallery_database`).
- **Built-in Photo Editor:** Real adjustments (brightness, contrast, saturation, warmth), transformations (90° rotation, horizontal/vertical flip), and aspect ratio crop (1:1, 4:3, 16:9). Exports copies to `Pictures/M-U-N Gallery/`.
- **Customization Engine:** Interactive sliders for glass transparency, blur intensity, reflection intensity, corner radius, wallpaper picker, and neon lights.

---

## How to Build Locally

### Prerequisites
- JDK 17+ (or JDK 21)
- Android SDK (API 36 / API 34+)

### Build Commands
```bash
# Build Debug APK (instantly installable on test devices):
./gradlew assembleDebug

# Build Release APK:
./gradlew assembleRelease
```

### Generated APK Locations:
- **Debug APK:** `app/build/outputs/apk/debug/app-debug.apk`
- **Release APK:** `app/build/outputs/apk/release/app-release.apk`

---

## Publishing & Downloading via GitHub Releases

Follow these simple steps to push the project to your GitHub repository and download the APK directly on your phone:

### Step 1: Upload Project to GitHub
Initialize Git, commit all files, and push to your new GitHub repository:

```bash
git init
git add .
git commit -m "Initial commit of M-U-N Gallery"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPOSITORY_NAME.git
git push -u origin main
```

### Step 2: Automated GitHub Actions Workflow
The project includes a ready-to-run GitHub Actions workflow (`.github/workflows/android-apk.yml`).
- Every push to `main` builds the APKs and uploads them as workflow artifacts under **Actions** → **Artifacts**.
- You can also run the workflow manually anytime by opening **Actions** → **Build & Release Android APK** → **Run workflow**.

### Step 3: Publish a GitHub Release (e.g. `v1.0.0`)
To create an official release with downloadable APK assets:

```bash
# Tag a release version:
git tag v1.0.0

# Push the tag to GitHub:
git push origin v1.0.0
```

GitHub Actions will automatically:
1. Compile the Android app.
2. Generate both `MUN-Gallery-release.apk` and `MUN-Gallery-debug.apk`.
3. Compute SHA-256 checksums.
4. Publish a new entry under **Releases** on your GitHub repository with the APKs attached.

### Step 4: Download and Install on Your Android Phone
1. On your Android phone, open your repository on GitHub in Chrome or any browser.
2. Tap **Releases** (or go to `https://github.com/YOUR_USERNAME/YOUR_REPOSITORY_NAME/releases/latest`).
3. Under **Assets**, tap **`MUN-Gallery-release.apk`** (or `MUN-Gallery-debug.apk`) to download.
4. Open the downloaded file to install.
   - *Note:* If Android displays "For your security, your phone is not allowed to install unknown apps from this source", tap **Settings** and toggle **Allow from this source**.
5. Launch **M-U-N Gallery** and tap **Allow Access** to enjoy your moments!

---

## Optional: Configuring Custom Release Keystore (Production)
If you want to sign release builds using your own custom keystore:
1. In your GitHub repository, navigate to **Settings** → **Secrets and variables** → **Actions**.
2. Add the following repository secrets:
   - `RELEASE_KEYSTORE_BASE64`: Base64 encoded string of your `.jks` file (`base64 -w 0 your-key.jks`).
   - `STORE_PASSWORD`: Keystore password.
   - `KEY_PASSWORD`: Key password.

If these secrets are not provided, the CI pipeline automatically packages an upload-signed release APK so your GitHub builds always succeed smoothly.

---

## Architecture & Tech Stack

- **Language:** Kotlin
- **UI Framework:** Jetpack Compose (Material Design 3)
- **Local Persistence:** Room Database (`androidx.room`) & SharedPreferences
- **Media Playback:** AndroidX Media3 / ExoPlayer (`androidx.media3:media3-exoplayer`)
- **Image Loading:** Coil (`io.coil-kt:coil-compose`, `coil-video`)
- **Device APIs:** Android MediaStore (`MediaStore.Images`, `MediaStore.Video`, Scoped Storage delete intents)
- **Build System:** Gradle (Kotlin DSL)
