# AURA

**Status: being rebuilt. New code is being pushed in stages.**

AURA is a personal planning and discipline assistant. It combines body data
from wearables and phones with what the user says in conversation, and helps
them decide what to do today, commit to it, and learn from what they actually
followed through on.

Two ideas drive the design:

- **Personal, not average.** Each person is compared with their own baseline,
  not with population norms.
- **The user is the planner.** AURA asks before it suggests, and saves a
  commitment only when the user agrees to it. The aim is that people rely on
  their own judgment more over time, not on the AI.

AURA is a wellness and planning tool. It is not a medical device and does not
diagnose or treat anything.

## Why this repository looks empty

The first version here was an early front-end prototype with simulated data.
I removed it because I am rebuilding AURA as a working end-to-end system with
a real backend. The earlier files remain in the commit history.

## Current progress

| Part | Status |
|---|---|
| Data adapters (Apple Health export, Whoop API format) | Built and tested |
| Unified daily table and personal baselines | Built and tested |
| Daily state (flags, streaks, trends per user) | Built and tested |
| Per-user memory (goals, routines, commitments, check-ins) | Built and tested |
| Planning assistant with safety checks | Built, tested with a stand-in model |
| Claude API integration | In testing |
| REST API (FastAPI) | Built and tested |
| New front-end | In progress |
| Live wearable connections, mobile apps, voice | Planned |

The backend has 64 automated tests and runs on more than two years of my own
Apple Health data. The Whoop adapter is tested against Whoop's documented
sample payloads, not a live device.

## Architecture

    Phone health / wearable APIs
            -> adapters -> unified daily table -> personal baselines -> daily state
    User message
            -> safety check -> facts + memory -> planning rules -> LLM -> reply check -> reply

## Tech stack

Python, pandas, FastAPI, SQLite, Claude API, JavaScript

## Privacy

Personal health data is never committed to this repository. The language
model receives a short summary only, with no user identifiers or raw records.

## Contact

Kishore Tambi Suddapalli
kishoresuddapalli8@gmail.com
