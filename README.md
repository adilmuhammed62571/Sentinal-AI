# Sentinal-AI
DeepSentinel v2.0
it is a hybrid deepfake and AI-generated video detection system that runs entirely on CPU, with no GPU or cloud services needed.

What it does: You upload a video file (MP4, MOV, AVI, WEBM, MKV, up to 200 MB) or paste a URL from YouTube, Instagram, TikTok, Facebook, X/Twitter, Vimeo, Reddit, or a direct video link. The system runs it through 7 independent detection modules and returns a probability score showing how likely the video is AI-generated or manipulated.

The 7 modules:

Biometric – blink-rate analysis using 468 facial landmarks (MediaPipe)
FFT texture – frequency-domain analysis of frames
Color correlation – RGB channel relationships
Frame consistency – frame-to-frame variation
Sharpness uniformity – focus drift across frames
AI voice / TTS – 7 audio sub-signals
MISLnet CNN – a deep learning classifier (AUC 0.983, based on a 2024 Drexel University paper)

How it scores: Each module’s result is weighted by its confidence, then combined into one score. A multi-signal gate prevents any single module from flagging a video alone. Scores fall into four tiers: Likely Authentic (0-24%), Possibly Authentic (25-49%), Possibly AI-Generated (50-74%), and Likely AI-Generated (75-100%).

Key design features:

Zero retention: every uploaded file is deleted after each request, and leftover files are purged on startup.
Graceful fallback: if the CNN model isn’t trained yet, the system runs in heuristic mode instead of crashing.
Self-contained UI: a dark, animated web interface embedded in app.py, with a results panel containing overview, modules, charts, frame timeline, observations, and raw JSON tabs.

Tech stack: Flask, OpenCV, MediaPipe, SciPy, librosa, PyTorch, ffmpeg, yt-dlp, and Chart.js.

Status: The app works end to end. The MISLnet model still needs training (models/mislnet_best.pth is missing), analyzer.py doesn’t yet pass mfcc_stability and zcr_mean to the frontend, and the README still has an outdated Telegram Bot section to remove.

If you want a shorter version for a README, report, or presentation, tell me the format and I’ll write it.
