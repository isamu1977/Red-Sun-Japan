# Red Sun Japan 🇯🇵

**YouTube Channel Project - Architecture & Workflow**

## 📜 Channel Concept

- **Niche:** Japanese History, Feudal Japan, Samurai Era, and Meiji Restoration.
- **Target Audience:** Older demographic (45+ years old) who prefers deep storytelling, documentary-style pacing, and rich historical accuracy over fast-paced editing.
- **Style:** Visual Podcast / Documentary Video-Essay. Minimal visual movement (slow Ken Burns effect on historical images) with a heavy focus on high-quality narrative and immersive background music.
- **Language:** English. Strategic choice for higher CPM and to actively practice and improve English communication skills.
- **The "Unfair Advantage":** Utilizing native Japanese reading skills to source untranslated historical texts, local folklore, and public domain archives (e.g., Aozora Bunko, National Diet Library) to create highly unique English content.

---

## ⚙️ The Video Creation Pipeline

1.  **Sourcing:** Gather Japanese historical texts, articles, or books.
2.  **Scripting & Translation:** Use local LLMs to condense and translate the Japanese material into an English script.
3.  **Manual Review:** Read the English script out loud to ensure natural pacing, correct robotic phrasing, and practice pronunciation.
4.  **Audio Generation (TTS):** Process the final script through a local Qwen TTS model to generate a high-quality, natural-sounding voiceover.
5.  **Transcription Engine:** Run the generated audio through Faster-Whisper to create a JSON file with word-level timestamps.
6.  **Visual Asset Sourcing:** Use a custom scraper targeting _only_ public domain libraries (Wikimedia Commons, Ukiyo-e databases) to find historical images.
7.  **AI Image Fallback:** If public domain images are unavailable, use ComfyUI API to programmatically generate historical-style fallback images.
8.  **Video Rendering (Remotion):** Inject the TTS audio, the Whisper JSON timestamps, the background music, and the images into the Remotion engine to programmatically render the final video with animated subtitles.
9.  **Thumbnail Design:** Create an eye-catching thumbnail using a pre-made template in Affinity Designer/Photo.
10. **Publishing:** Generate SEO-optimized titles and descriptions, and upload to YouTube.

---

## ✅ Development Checklist

### Phase 1: Environment Setup

- [x] Create root folder: `channel-redsunjapan`
- [ ] Initialize Git repository.
- [ ] Create backend directory: `/motor-python`
- [ ] Create video engine directory: `/render-remotion`

### Phase 2: Python Backend (Audio & Data)

- [ ] Setup Python virtual environment inside `/motor-python`.
- [ ] Install FastAPI, Uvicorn, transformers, and faster-whisper.
- [ ] **Task 1:** Create `main.py` with FastAPI.
- [ ] **Task 2:** Implement Qwen TTS generation function.
- [ ] **Task 3:** Implement Faster-Whisper transcription function (outputting word-level JSON).
- [ ] **Task 4:** Create `/process-script` endpoint that receives text, triggers TTS and Whisper, and returns paths to `.wav` and `.json`.
- [ ] _Test Phase 2 API with Postman or cURL._

### Phase 3: Visual Assets Automation

- [ ] **Task 5:** Build a safe scraper script for public domain image libraries (save to a specific `/assets` folder).
- [ ] **Task 6:** (Optional/Fallback) Configure a basic Python script to hit the local ComfyUI API with specific historical prompts if the scraper finds nothing.

### Phase 4: Remotion Video Engine

- [ ] Setup Remotion project inside `/render-remotion` (`npx create-video@latest`).
- [ ] **Task 7:** Create a basic React component for the video composition.
- [ ] **Task 8:** Fetch and import the generated `.wav` audio and background music into the timeline.
- [ ] **Task 9:** Create the Subtitle Component that reads the Whisper `.json` and synchronizes text rendering using `useCurrentFrame()`.
- [ ] **Task 10:** Create the Image Background Component with CSS animations (slow scale/pan for Ken Burns effect).
- [ ] _Test Phase 4 by previewing the composition in the browser._

### Phase 5: Production & Final Polish

- [ ] Design a reusable Thumbnail template in Affinity.
- [ ] Run a full end-to-end test: Pass a short script -> Generate Audio/JSON -> Load into Remotion -> Render MP4.
- [ ] Troubleshoot timing/sync issues.
- [ ] Create the first official "Red Sun Japan" video!
