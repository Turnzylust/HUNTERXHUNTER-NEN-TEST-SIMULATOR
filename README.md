# HxH Nen Simulator — Sora-Ready Starter

This repo is plug-and-play. **You only add music.** Video & image generators are already wired:

- `/api/generate-image` → Uses OpenAI Images if `OPENAI_API_KEY` is set. Otherwise returns a placeholder image.
- `/api/generate-video` → Returns a demo video URL (`DEMO_VIDEO_URL`) or a built-in placeholder clip.
- `/api/video-status` → Stub endpoint for queued providers (always returns succeeded with the demo URL).

## Quick Deploy (Vercel)

1. **Download this zip** and extract.
2. Add your music MP3s to the repo root, named exactly:
   - `phase1.mp3`
   - `phase2.mp3`
   - `phase3.mp3`
3. Push to GitHub and **Import to Vercel** (or deploy directly).
4. In Vercel → Project → **Settings → Environment Variables**, set (optional but recommended):
   - `OPENAI_API_KEY` = your key (for real images)
   - `DEMO_VIDEO_URL` = your hosted MP4 (optional; default placeholder is used otherwise)
5. Redeploy. Open your Vercel URL — you’re live.

## Local Dev

- Install Vercel CLI: `npm i -g vercel`
- Run: `vercel dev`
- Open: `http://localhost:3000`

## How it works

- **Image**: `index.html` calls `/api/generate-image` with a prompt based on the user’s ability. If `OPENAI_API_KEY` is set, it returns a base64 data URL. Otherwise, a placeholder image is returned.
- **Video (Sora-ready)**: `index.html` calls `/api/generate-video`. If your provider is queue-based, return `{ job_id }` and implement `/api/video-status` to poll until `{ status: 'succeeded', video_url }`.

## Swap to a Real Video Provider

Inside `/api/generate-video.js`, replace the stub with your provider call (Sora or others) and keep the response shape:
- Direct: `{ video_url }`
- Queued: `{ job_id }` and implement `/api/video-status` accordingly.

## Only thing you must add

- **Music** files (`phase1.mp3`, `phase2.mp3`, `phase3.mp3`). That’s it.

Enjoy!