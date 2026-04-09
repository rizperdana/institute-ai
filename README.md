# 🏛️ The Institute of Everything
### A Fake Museum Exhibit Generator — Powered by Pollinations.ai

> *"A museum of absolute authority on any subject."*

---

## What It Does

The Institute of Everything takes any concept you type — absurd, niche, or mundane — and generates a complete fake museum exhibit around it, with straight-faced academic seriousness.

**You type:** `The Ancient Cult of the Snooze Button`

**The app generates:**
- A dramatic exhibit title
- A pompous curator's introduction (with audio narration)
- 5 unique "artifacts" — each with:
  - An AI-generated museum photograph
  - A fake artifact name with era/date (e.g. *"The Sacred Coil of Morning Resistance, circa 2019 CE"*)
  - A deadpan museum placard
  - An audio guide clip narrated in a deep museum-guide voice

---

## Try These Concepts

| Concept | Tone |
|---|---|
| The Ancient Cult of the Snooze Button | Absurd |
| Post-Apocalyptic Street Food Culture | Dramatic |
| Sacred Rituals of the Office Printer | Dry |
| The Lost Civilization of People Who Reply to All | Satirical |
| Medieval Philosophers of the Left Swipe | Historical |
| The Forgotten Empire of Dial-Up Internet | Nostalgic |

---

## How to Run

Zero setup. No install. No server. No API key.

```
1. Download index.html
2. Open it in any browser
3. Type a concept → click "Commission the Exhibit"
```

That's it.

---

## Tech Stack

| Layer | What |
|---|---|
| Frontend | Vanilla HTML + CSS + JavaScript (single file) |
| AI Text | Pollinations.ai text API — `openai` model |
| AI Images | Pollinations.ai image API — `flux` model |
| AI Audio | Pollinations.ai audio API — `openai-audio`, voice: `onyx` |
| Fonts | Playfair Display, IM Fell English, Courier Prime (Google Fonts) |
| Dependencies | None |

---

## API Endpoints Used

```
POST https://text.pollinations.ai/
     → Generates exhibit title, curator note, 5 artifacts (JSON mode)

GET  https://image.pollinations.ai/prompt/{prompt}?model=flux&width=512&height=512&nologo=true&seed={n}
     → Generates artifact photograph per artifact

GET  https://text.pollinations.ai/{text}?model=openai-audio&voice=onyx
     → Generates MP3 narration for curator intro + each artifact placard
```

All free. No API key required for basic usage.

---

## Generation Flow

```
User submits concept
        │
        ▼
[1] Text API → exhibit JSON (title + curator note + 5 artifacts)
        │
        ▼
[2] Render exhibit shell immediately (cards visible with shimmer placeholders)
        │
        ▼
[3] Image API (sequential, 350ms stagger) → artifact photos loaded one by one
        │
        ▼
[4] Audio API (parallel) → narrator clips for intro + all 5 placards
        │
        ▼
Exhibit opens
```

Sequential image fetching respects Pollinations' anonymous rate limit (1 req / ~15s is the strict limit — the 350ms stagger is lenient but avoids hammering the API).

---

## File Structure

```
index.html      ← entire app (HTML + CSS + JS, ~550 lines)
README.md       ← this file
```

---

## Limitations

- **Rate limits:** Free anonymous tier on Pollinations is capped. If generation stalls, wait 30 seconds and try again, or register a free account at [auth.pollinations.ai](https://auth.pollinations.ai) and add your token to the image URL as `&key=YOUR_KEY`.
- **Audio occasionally fails:** The app silently skips failed audio clips rather than blocking the exhibit.
- **Image occasionally fails:** Failed images show a placeholder — *"Artifact image lost to the sands of time."*
- **No persistence:** Nothing is saved. Each session generates fresh.

---

## Adding Your API Key (Optional)

To remove watermarks and increase rate limits, register at [auth.pollinations.ai](https://auth.pollinations.ai), get a free Seed tier key, then in `index.html` find:

```js
const url = `https://image.pollinations.ai/prompt/${encodeURIComponent(prompt)}?width=512&height=512&nologo=true&model=flux&seed=${seed}`;
```

Change to:

```js
const url = `https://image.pollinations.ai/prompt/${encodeURIComponent(prompt)}?width=512&height=512&nologo=true&model=flux&seed=${seed}&key=YOUR_KEY_HERE`;
```

---

## License

MIT. Do whatever you want with it.

---

*Built with [Pollinations.ai](https://pollinations.ai) — free, open-source generative AI APIs.*
