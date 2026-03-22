# VocabScroll · DE→ES

A mobile-first vocabulary learning app with a TikTok-style swipe interface. Built as a single HTML file — no frameworks, no build step, no dependencies. Just drop the files in a folder and open in a browser.

![VocabScroll](https://img.shields.io/badge/VocabScroll-DE→ES-6c63ff?style=for-the-badge)
![HTML](https://img.shields.io/badge/HTML-Single%20File-orange?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)

---

## Features

### 5 Learning Modes
| Mode | Description |
|------|-------------|
| 📖 **Lernen** | Full vocabulary deck — ~3,000 German→Spanish word pairs |
| 🔁 **Wiederholen** | Repeat folder — cards you've saved by swiping left |
| ⚡ **Verben** | Conjugation trainer — 150 common verbs × 6 tenses |
| 💬 **Sätze** | Conversation mode — 500 everyday sentence pairs |
| 🔥 **Challenge** | Daily challenge — a fresh random selection every 24 hours |

### Swipe Mechanics
- **Swipe left** → save card to your repeat folder
- **Swipe right** → next card
- **Tap / scroll down** → flip card to see the translation
- **Swipe down** → flip card (touch gesture)

### Verb Conjugation Trainer
Select from 6 tenses and practice all 6 conjugated forms per verb. The card back shows a full conjugation table with Spanish pronouns (yo, tú, él/ella, nosotros, vosotros, ellos/ellas). A "change tense" button is always available on the card back.

**Supported tenses:**
- Präsens → Presente
- Präteritum (Indefinido) → Pretérito Indefinido
- Imperfekt → Pretérito Imperfecto
- Futur → Futuro Simple
- Konditional → Condicional Simple
- Perfekt → Pretérito Perfecto

### Daily Challenge
A seeded random selection drawn from the full combined pool (vocabulary + sentences + all verb tenses). The same cards are shown all day; a new set is generated at midnight. You can set the daily word count to 10 / 20 / 30 / 40 / 50.

### User Profiles
Multiple users can share the same device. Each profile has its own:
- Saved cards (repeat folder)
- Progress per mode and tense
- Daily challenge settings

Profiles are stored locally in `localStorage`. No account or internet connection needed.

### Other Features
- 🔊 **Text-to-speech** — Spanish pronunciation via the Web Speech API (auto-plays on card flip)
- ⭐ **Bookmark button** — save/unsave the current card
- 📱 **PWA-ready** — works as a home screen app on iOS and Android
- ⌨️ **Keyboard shortcuts** — full keyboard support on desktop
- 💾 **Offline-capable** — everything runs locally after the first load
- 🌙 **Dark theme** — OLED-friendly dark UI

---

## File Structure

```
vocabscroll/
├── index.html              # The entire app — all HTML, CSS and JS
├── vocab_de_es.json        # ~3,000 German→Spanish vocabulary pairs
├── conversations.json      # 500 everyday sentence pairs (20 categories)
├── verbs_present.json      # 150 verbs — Präsens / Presente
├── verbs_preterite.json    # 150 verbs — Präteritum / Indefinido
├── verbs_imperfect.json    # 150 verbs — Imperfekt / Imperfecto
├── verbs_future.json       # 150 verbs — Futur / Futuro
├── verbs_conditional.json  # 150 verbs — Konditional / Condicional
├── verbs_perfect.json      # 150 verbs — Perfekt / Pretérito Perfecto
└── README.md
```

---

## Getting Started

### Option 1 — Open directly in the browser
Download all files into the same folder, then open `index.html` in any modern browser. That's it.

> **Note:** Some browsers block `fetch()` requests from `file://` URLs. If the vocab files don't load, use Option 2 below.

### Option 2 — Serve locally

Using Python:
```bash
python3 -m http.server 8080
```
Then open [http://localhost:8080](http://localhost:8080) in your browser.

Using Node.js:
```bash
npx serve .
```

### Option 3 — Deploy to GitHub Pages
1. Push all files to a GitHub repository
2. Go to **Settings → Pages**
3. Set source to **Deploy from a branch → main → / (root)**
4. Your app will be live at `https://yourusername.github.io/your-repo-name`

---

## Keyboard Shortcuts

| Key | Action |
|-----|--------|
| `Space` or `→` | Next card |
| `←` | Previous card |
| `↓` or `F` | Flip card |
| `S` | Speak (text-to-speech) |
| `B` | Toggle bookmark |
| `1` | Switch to Lernen mode |
| `2` | Switch to Wiederholen mode |
| `3` | Switch to Verben mode |
| `4` | Switch to Sätze mode |
| `5` | Switch to Challenge mode |
| `Esc` | Close dropdown menu |

---

## JSON Data Formats

### vocab_de_es.json
```json
{
  "meta": {
    "source_language": "de",
    "target_language": "es"
  },
  "words": [
    { "id": 1, "de": "gehen", "es": "ir", "type": "verb" }
  ]
}
```

### conversations.json
```json
{
  "meta": { "source_language": "de", "target_language": "es" },
  "sentences": [
    { "id": 1, "de": "Guten Morgen!", "es": "¡Buenos días!", "cat": "Begrüßungen" }
  ]
}
```

### verbs_*.json
```json
{
  "meta": { "tense": "present", "tense_de": "Präsens", "tense_es": "Presente" },
  "verbs": [
    {
      "id": 1,
      "de": "sein",
      "es_infinitive": "ser/estar",
      "forms": {
        "ich":    "soy/estoy",
        "du":     "eres/estás",
        "er/sie": "es/está",
        "wir":    "somos/estamos",
        "ihr":    "sois/estáis",
        "sie":    "son/están"
      }
    }
  ]
}
```

---

## Extending the App

### Add your own vocabulary
Edit `vocab_de_es.json` and add entries to the `words` array. Make sure each entry has a unique `id`.

### Add more conversation sentences
Edit `conversations.json` and add entries to the `sentences` array. The `cat` field is the category label shown on the card.

### Change the language pair
The app normalizes both `{de, es}` and `{source, target}` key names, so you can adapt the JSON files for any language pair. Update the `meta.source_language_name` and `meta.target_language_name` fields to change the labels shown on cards.

### Add more verbs
Each verb JSON file supports up to any number of entries. Add new verb objects following the existing format, making sure `id` values are unique within the file.

---

## Browser Support

| Browser | Support |
|---------|---------|
| Chrome / Edge | ✅ Full |
| Safari (iOS 16+) | ✅ Full |
| Firefox | ✅ Full |
| Samsung Internet | ✅ Full |

Text-to-speech quality depends on the voices installed on the device. Spanish (`es-ES`) voices are available by default on most modern platforms.

---

## Local Storage Keys

All data is stored in `localStorage` under the active profile's namespace (`vs_{profileId}_*`). No data is ever sent to a server.

| Key pattern | Contents |
|-------------|----------|
| `vs_profiles` | Array of all user profiles |
| `vs_g_last` | ID of the last active profile |
| `vs_{id}_repeat` | Saved card IDs (vocab + conv) |
| `vs_{id}_vrepeat` | Saved card IDs (verb mode) |
| `vs_{id}_idx_{mode}` | Current deck position per mode |
| `vs_{id}_ccount` | Daily challenge word count |
| `vs_{id}_ch_{date}_{n}` | Cached daily challenge selection |
| `vs_{id}_hints` | Whether swipe hints have been shown |

---

## License

MIT — free to use, modify and distribute.

---

## Acknowledgements

- Vocabulary data compiled from common German–Spanish frequency lists
- Verb conjugations verified against standard Spanish grammar references
- UI inspired by modern mobile card-learning apps
- Built entirely with vanilla HTML, CSS and JavaScript — no external dependencies
