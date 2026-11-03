# Reels

This repo is for editing vertical short-form video (1080x1920).

- `scripts/reel` is an ffmpeg toolkit for trimming, reframing to 9:16, speed changes, concat, music, loudness and
  export. Run `scripts/reel help` for usage.
- `ads/<name>/` holds one HyperFrames project per ad (captions, titles, overlays, end cards). Before writing or
  editing anything in one, load the `hyperframes` skill and read that project's `CLAUDE.md`.
- Ads are for the brand **Picante Painting** and run as Meta (Instagram/Facebook) ads: keep text inside the Reels ad
  safe zone (y 270-1248 on 1080x1920, 65px from the sides), put the brand in the first seconds, end on the
  "Tap below for a quote" end card, and never use commercial music (deliver silent or use licensed audio).
- To start a new ad, copy an existing `ads/<name>/` folder, swap the footage in `assets/`, and edit the scene copy.
  Footage prep (trim, crop, stabilize) is done with ffmpeg before it goes into `assets/`.
- Source footage and renders are git-ignored. Never commit video or audio files.
