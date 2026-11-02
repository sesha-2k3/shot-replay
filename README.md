# shotreplay

A pipeline for ingesting, versioning, analyzing, and replaying tennis shot data from wearable IMU sensors.

shotreplay takes raw accelerometer and gyroscope recordings, turns them into clean, versioned sessions with automated quality checks, serves shot-classification models through a documented API, and provides a replay view that compares detected shots against ground-truth labels.

> 🚧 **Status:** In active development. See the roadmap below.

## Features

- **Ingestion:** Converts raw IMU recordings into a per-session format (Parquet + JSON metadata).
- **Quality checks:** Flags missing values, flat-lined channels, sequence-length mismatches, and label inconsistencies.
- **Dataset versioning:** Processed data is tracked with DVC so every experiment is reproducible.
- **Model serving (planned):** Shot classifier and shot detector behind a FastAPI endpoint.
- **Latency measurement (planned):** Replays sessions as simulated live streams over WebSocket and logs latency, throughput, and dropped frames.
- **Replay view (planned):** Timeline of sensor channels with ground-truth and predicted shots overlaid, highlighting timing errors.

## Roadmap

- [ ] Ingestion and session format
- [ ] Quality checks and tests
- [ ] DVC dataset versioning
- [ ] Baseline classifier and detector (participant-held-out evaluation)
- [ ] FastAPI model interface
- [ ] Stream simulator and latency metrics
- [ ] React replay view

## Project structure

```
shotreplay/
├── ingest/        # Raw data loading and session conversion
├── quality/       # Data quality checks
├── models/        # Training and evaluation
├── api/           # FastAPI model service
├── stream/        # Live-stream simulator and latency logging
├── web/           # Replay view (React)
├── tests/
└── data/          # DVC-tracked (not committed)
```

## Getting started

```bash
git clone https://github.com/sesha-2k3/shotreplay.git
cd shotreplay
pip install -r requirements.txt
```

### Dataset

This project uses the public **Silent Impact** tennis IMU dataset. The data is **not** included in this repository. Download it from the [official Silent Impact repository](https://github.com/jyp0802/Silent-Impact), place the files in `data/raw/`, then run:

```bash
python -m ingest.run --input data/raw --output data/processed
```

## Tech stack

Python, NumPy, Pandas, PyTorch, XGBoost, FastAPI, WebSockets, DVC, pytest, React

## Acknowledgments

Dataset from *Silent Impact: Tracking Tennis Shots from the Passive Arm*. Please cite the original paper if you use the data (see the citation in the dataset's repository).

## Author

Built by **Seshadri Veeraraghavan Vidyalakshmi** · [LinkedIn](https://linkedin.com/in/seshadrivv28) · [GitHub](https://github.com/sesha-2k3)
