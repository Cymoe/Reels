# Reels

An ffmpeg workflow for editing vertical short-form video (Instagram Reels, TikTok, YouTube Shorts).

## Layout

```
input/    source clips (not committed)
output/   renders (not committed)
scripts/reel   the editing toolkit (one bash script, wraps ffmpeg)
```

Media files are git-ignored. Keep footage local or in Google Drive.

## Requirements

`ffmpeg` and `ffprobe` (with libass and freetype, which is the default on most builds), plus `python3` (used only for `speed` below 0.5x).

## Commands

```bash
scripts/reel help
scripts/reel info     input/clip.mp4
scripts/reel trim     input/clip.mp4 output/01-trim.mp4 3.5 18          # keep 3.5s–18s
scripts/reel vertical output/01-trim.mp4 output/02-vert.mp4 crop 0.5    # fill 9:16 (0=left, 1=right focus)
scripts/reel vertical output/01-trim.mp4 output/02-vert.mp4 blur        # whole frame on blurred background
scripts/reel speed    output/02-vert.mp4 output/03-fast.mp4 1.25
scripts/reel concat   output/joined.mp4 a.mp4 b.mp4 c.mp4
scripts/reel captions output/02-vert.mp4 output/04-cap.mp4 subs.srt
scripts/reel text     output/04-cap.mp4 output/05-title.mp4 "3 tips you need" 0 3
scripts/reel music    output/05-title.mp4 output/06-music.mp4 song.mp3 0.25   # add "mute" to drop original audio
scripts/reel loudnorm output/06-music.mp4 output/07-loud.mp4                  # -14 LUFS
scripts/reel export   output/07-loud.mp4 output/final.mp4
scripts/reel thumb    output/final.mp4 output/cover.jpg 2
```

A typical pipeline is: **trim → vertical → (speed / concat) → captions → text → music → loudnorm → export**.

Output is 1080x1920, 30fps, H.264 High (CRF 18), yuv420p, AAC 192k, with faststart. Override with the env vars
`REEL_WIDTH`, `REEL_HEIGHT`, `REEL_FPS`, `REEL_CRF`, `REEL_PRESET` and `REEL_FONT`.

Captions and titles are placed to stay clear of the platform UI at the top and bottom of the screen.
