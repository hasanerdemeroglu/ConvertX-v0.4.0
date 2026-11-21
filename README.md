# ConvertX Android — v0.4.0

ConvertX is an offline-first Android file converter with a soft cyber visual identity: deep navy surfaces, electric blue/cyan accents, violet highlights and the developer credit **Hasan Erdem Eroğlu**.

## v0.4.0 implementation
- Persistent, sequential batch processing using WorkManager unique work chains (`APPEND_OR_REPLACE`). WorkManager stores work in its local database, so queued work survives app process death and device restart subject to Android scheduling/battery policies.
- Real FFmpegKit-based conversion workers for supported video, audio and raster-image formats.
- Source documents are opened through Android Storage Access Framework; the app retains read permission before queueing and copies each input into private cache for processing.
- Outputs are saved to `Downloads/ConvertX` on Android 10+; on Android 8/9 they are saved under the app-specific Downloads directory.
- Per-job stage/progress state, success/failure state and error detail are exposed in the queue screen. Progress is intentionally stage-based; FFmpeg execution is shown as indeterminate rather than inventing a percentage.
- Conversion is local. No network permission is declared.

## Currently implemented conversion scope
- Video: MP4, MKV, AVI, MOV, WEBM, MPEG/MPG, M4V, GIF (actual codec availability depends on the bundled FFmpeg build).
- Audio: MP3, WAV, FLAC, AAC, M4A, OGG, OPUS.
- Images: JPG/JPEG, PNG, WEBP, BMP, TIFF/TIF. Raster image conversion exports a single frame.
- Document, archive and structured-data categories remain catalog/UI placeholders and are not yet executable.
- Some codec combinations can still fail on specific input media. A failed job reports an error and does not rename the source file.

## Engine / licensing note
The Android media engine uses the community-maintained FFmpegKit-compatible Android package `dev.ffmpegkit-maintained:ffmpeg-kit-full:8.1.9`. Review the package's current license and codec matrix before distribution. FFmpeg and optional codec licensing may impose obligations depending on the selected build and distribution model.

## Build
Open this folder in Android Studio with JDK 17. Gradle needs internet access once to resolve Android/WorkManager/FFmpeg dependencies; after dependencies are cached, the app's conversion workflow itself does not require internet.

- Namespace/application ID: `com.convertx.app`
- Minimum SDK: 26 (Android 8.0)
- Target SDK: 35
- Version: 0.4.0
- UI: Kotlin + Jetpack Compose + Material 3
