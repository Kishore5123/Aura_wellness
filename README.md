# AURA — AI Wellness Companion

AURA connects wearable body signals to a conversation. When your body shifts with no exercise to explain it, AURA checks in with you, and it answers from your own history instead of generic advice.

**Status:** front-end prototype. Wearable readings are simulated and AI replies run in demo mode. The backend and real wearable data are the next phase (see [Roadmap](#roadmap)).

**Live demo:** https://kishore5123.github.io/Aura_wellness/ · **Body signal demo:** https://kishore5123.github.io/Aura_wellness/body-signal-demo.html

| Body signal alert | Conversation | Patterns |
| --- | --- | --- |
| ![Alert](docs/screenshots/body-signal-alert.png) | ![Conversation](docs/screenshots/body-signal-conversation.png) | ![Patterns](docs/screenshots/body-signal-patterns.png) |

## The idea

Wearables measure the body well and say little about what the numbers mean for your day. Wellness chat apps talk well and know only what you type. AURA joins the two:

1. **The body starts the conversation.** A sustained drop in heart rate variability (HRV) with no movement opens a check-in.
2. **It compares you with yourself.** The threshold is your own baseline, not a population average.
3. **It answers from your own history.** Before speaking, AURA finds the past days whose readings looked most like now and recalls what helped.
4. **It learns your delays.** For example, how many days your mood trails your sleep.

## What is in this repository

| Page | What it shows |
| --- | --- |
| `index.html` | The companion app: onboarding, dashboard with wellness score, companion chat, health log, goals, devices |
| `body-signal-demo.html` | The core feature: live HRV trace, anomaly trigger, journal recall, check-in conversation, sleep-to-mood pattern |

### Real and simulated

| Part | State |
| --- | --- |
| Anomaly trigger (3 readings in a row more than 20% under baseline, with no step change) | Real logic, running in the browser |
| Journal recall (nearest past days by HRV, heart rate, sleep and time of day) | Real logic, on a sample journal |
| Sleep-to-mood delay (correlation at 0 to 3 day lags) | Real calculation, on 14 days of sample data |
| Health log, goals, wellness score, charts | Real, stored in your browser's `localStorage` |
| Wearable readings | Simulated |
| Device connections | Simulated |
| AI replies | Demo mode with built-in replies. Live replies need the backend |

## How the trigger works

```
Wearable  ->  Anomaly detector  ->  Context engine  ->  AI companion  ->  Conversation
                (your baseline)      (your journal)                          |
                                           ^---------- reply saved ----------+
```

1. Each reading is compared with the user's personal baseline.
2. A check-in fires only after several low readings in a row, and only if movement does not explain them.
3. The context engine scores past journal entries for similarity to the current readings.
4. The alert and the closest entries are given to the companion, which opens the conversation.
5. The user's reply is saved with the readings from that moment and becomes retrievable next time.

## Run it locally

No build step and no dependencies.

```bash
git clone https://github.com/Kishore5123/Aura_wellness.git
cd Aura_wellness
# open index.html in a browser, or serve the folder:
python3 -m http.server 8000
```

Then visit `http://localhost:8000`.

To turn on live AI replies, set `AI_BACKEND_URL` in `script.js` and `body-signal-demo.html` to a backend endpoint that accepts `POST {system, messages}` and returns `{reply}`. The API key belongs on that backend, never in this front-end code.

## Tech

HTML, CSS and vanilla JavaScript. Canvas for charts and the live trace. `localStorage` for data. No frameworks.

## Roadmap

- [x] **Phase 0** Front-end prototype with simulated wearable, trigger, journal recall, pattern view
- [ ] **Phase 1** Backend with a journal store and a model proxy; one real wearable data source; the author as first test user
- [ ] **Phase 2** Emotion classifier fine-tuned on a public emotion dataset; combined text and body retrieval; remaining triggers (resting heart rate, stress, sleep debt)
- [ ] **Phase 3** Personal baselines, a stress classifier, and a small pilot
- [ ] **Phase 4** More wearables and a per-user sleep-to-mood delay model

## Documents

- [`docs/AURA_Project_Report.docx`](docs/AURA_Project_Report.docx)
- [`docs/AURA_Presentation.pptx`](docs/AURA_Presentation.pptx)

## Privacy and limits

AURA is a wellness prototype. It does not diagnose or treat, and it is not a substitute for a doctor or therapist. In this version all data stays in your browser. A body signal is not a feeling, so AURA asks what is going on and does not tell the user how they feel.

## Author

Suddapalli Kishore Tambi, MSc student in Artificial Intelligence, Switzerland. Open to internships and roles in AI and machine learning.
