# RealView Chat

Runs OpenAI vision on property inspection photos (kitchens & bathrooms), then lets you review and score the results in a web dashboard.

## Prerequisites

- Python 3.10+
- Node 18+
- OpenAI API key

## Setup

```bash
pip install -r requirements.txt
cd web/frontend && npm install && cd ../..
```

Create a `.env` in the project root:

```
OPENAI_API_KEY=sk-your-key-here
```

## Images

Put property images in `cases/case_<property_id>/` (e.g. `cases/case_2203177/`).

## Run the pipeline

```bash
# process all unprocessed cases
python scripts/run_pipeline.py

# or just one
python scripts/run_pipeline.py 2203177
```

Results go to `out/results_<property_id>.json`. Already-processed cases are skipped.

## Run the web app

Two terminals:

```bash
# terminal 1 - backend (port 5001)
python -m web.backend.app

# terminal 2 - frontend
cd web/frontend && npm run dev
```

Open http://localhost:5173. Pick a property from the sidebar, review images, classify them (correct/FP/FN), and score condition/modernity/material/functionality.

## Troubleshooting

- **No properties** — run the pipeline first so `out/` has result files
- **403 on localhost:5000** — we use port 5001 (macOS AirPlay uses 5000)
- **Images broken** — check that `cases/case_<id>/` exists with the right filenames
