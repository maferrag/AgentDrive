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


---
