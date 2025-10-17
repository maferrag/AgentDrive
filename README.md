# AgentDrive 

AgentDrive is an open benchmark dataset containing 300,000 LLM-generated driving scenarios designed for the training, fine-tuning, and evaluation of autonomous agents under diverse conditions. AgentDrive formalizes a factorized scenario space across seven orthogonal axes—scenario type, driver behavior, environment, road layout, objective, difficulty, and traffic density—and employs an LLM-driven prompt-to-JSON pipeline to produce semantically rich, simulation-ready specifications validated under physical and schema constraints. Each scenario undergoes simulation rollouts, surrogate safety metric computation, and rule-based outcome labeling. 

To complement simulation-based evaluation, we introduce AgentDrive_MCQ, a 100,000-question reasoning benchmark spanning five reasoning dimensions—physics, policy, hybrid, scenario, and comparative—to systematically assess the cognitive and ethical reasoning of LLM-based agents. 

We conducted a large-scale evaluation of fifty leading LLMs on the AgentDrive_MCQ benchmark to measure their reasoning capabilities across these five dimensions, covering models such as GPT-5, ChatGPT 4o, Gemini 2.5 Flash, DeepSeek V3, Qwen3 235B, ERNIE 4.5 300B, Grok 4, Mistral Medium 3.1, and Phi 4 Reasoning Plus. Results reveal that while proprietary frontier models dominate in contextual and policy reasoning, advanced open models are rapidly closing the gap in structured and physics-grounded reasoning. To support open science and reproducibility, we release the AgentDrive dataset (including labeled data), the AgentDrive-MCQ benchmark, evaluation scripts, and all related materials on GitHub.

[![License](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](LICENSE)
[![GitHub Pages](https://img.shields.io/badge/site-online-brightgreen)]([https://USER.github.io/AgentDrive](https://github.com/maferrag/AgentDrive/))
[![Paper](https://img.shields.io/badge/paper-PDF-red)](link-to-paper)

## Datasets
- **AgentDrive-Gen**: 300K structured, simulation-ready JSON scenarios across seven axes (scenario type, driver behavior, environment, road layout, objective, difficulty, traffic density).
- **AgentDrive-Sim**: Executed rollouts with surrogate safety metrics (e.g., min-TTC) and categorical outcomes: `safe_goal`, `safe_stop`, `inefficient`, `unsafe`.
- **AgentDrive-MCQ**: 100K multiple-choice questions spanning five styles: `physics`, `policy`, `hybrid`, `scenario`, `comparative`.

## AgentDrive - Architecture Design

The framework for creating the AgentDrive Dataset is illustrated in the figure below.

## AgentDrive-MCQ - Architecture Design

The framework for creating the AgentDrive-MCQ Dataset is illustrated in the figure below.


---
