# AgentDrive

> An open benchmark suite for agentic AI reasoning in autonomous systems, including **AgentDrive-Gen** (300K LLM-generated scenarios), **AgentDrive-Sim** (simulation rollouts + safety labels), and **AgentDrive-MCQ** (100K reasoning MCQs).

[![License](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](LICENSE)
[![GitHub Pages](https://img.shields.io/badge/site-online-brightgreen)](https://USER.github.io/AgentDrive)
[![Paper](https://img.shields.io/badge/paper-PDF-red)](link-to-paper)

## TL;DR
AgentDrive unifies **generative scenario synthesis**, **simulation-grounded safety labeling**, and **reasoning-based evaluation** for LLM-powered autonomous agents.

## Datasets
- **AgentDrive-Gen**: 300K structured, simulation-ready JSON scenarios across seven axes (scenario type, driver behavior, environment, road layout, objective, difficulty, traffic density).
- **AgentDrive-Sim**: Executed rollouts with surrogate safety metrics (e.g., min-TTC) and categorical outcomes: `safe_goal`, `safe_stop`, `inefficient`, `unsafe`.
- **AgentDrive-MCQ**: 100K multiple-choice questions spanning five styles: `physics`, `policy`, `hybrid`, `scenario`, `comparative`.

> See detailed pages at **`docs/index.md`** and **`docs/results.md`**.

# open the site locally (Jekyll) or push and enable GitHub Pages
```

## Results (snapshot)
A small excerpt of the leaderboard is shown below. Full tables live in [`docs/results.md`](docs/results.md) and CSV at [`results/top_models.csv`](results/top_models.csv).

| Model | Comparative | Hybrid | Physics | Policy | Scenario | Overall |
|------:|------------:|-------:|--------:|------:|---------:|-------:|
| ChatGPT 4o | 90.0 | 72.5 | 55.0 | 100 | 95.0 | 82.5 |
| GPT-5 Chat | 92.5 | 70.0 | 50.0 | 100 | 92.5 | 81.0 |
| Qwen3 235B A22B (2507) | 92.5 | 60.0 | 67.5 | 87.5 | 97.5 | 81.0 |
| Mistral Medium 3.1 | 95.0 | 60.0 | 52.5 | 97.5 | 95.0 | 80.0 |
| GPT-4.1 Mini | 90.0 | 55.0 | 50.0 | 95.0 | 97.5 | 77.5 |


## Cite

---
