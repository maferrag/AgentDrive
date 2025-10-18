# AgentDrive 

<img src="Images/AgentDrive2.jpg" width="100%">

[![License](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](LICENSE)
[![GitHub Pages](https://img.shields.io/badge/site-online-brightgreen)]([https://USER.github.io/AgentDrive](https://github.com/maferrag/AgentDrive/))
[![Paper](https://img.shields.io/badge/paper-PDF-red)](link-to-paper)

**AgentDrive** is an open benchmark dataset containing **300,000 LLM-generated driving scenarios** designed for the training, fine-tuning, and evaluation of autonomous agents under diverse conditions. AgentDrive formalizes a factorized scenario space across seven orthogonal axes—scenario type, driver behavior, environment, road layout, objective, difficulty, and traffic density—and employs an LLM-driven prompt-to-JSON pipeline to produce semantically rich, simulation-ready specifications validated under physical and schema constraints. Each scenario undergoes simulation rollouts, surrogate safety metric computation, and rule-based outcome labeling. 

To complement simulation-based evaluation, we introduce **AgentDrive_MCQ**, a 100,000-question reasoning benchmark spanning five reasoning dimensions—physics, policy, hybrid, scenario, and comparative—to systematically assess the cognitive and ethical reasoning of LLM-based agents. 

We conducted a large-scale evaluation of **fifty leading LLMs** on the AgentDrive_MCQ benchmark to measure their reasoning capabilities across these five dimensions, covering models such as GPT-5, ChatGPT 4o, Gemini 2.5 Flash, DeepSeek V3, Qwen3 235B, ERNIE 4.5 300B, Grok 4, Mistral Medium 3.1, and Phi 4 Reasoning Plus. Results reveal that while proprietary frontier models dominate in contextual and policy reasoning, advanced open models are rapidly closing the gap in structured and physics-grounded reasoning. To support open science and reproducibility, we release the AgentDrive dataset (including labeled data), the AgentDrive-MCQ benchmark, evaluation scripts, and all related materials on GitHub.

## AgentDrive - Architecture Design

The framework for creating the AgentDrive Dataset is illustrated in the figure below.

![Description of image](Images/AgentDrive_Sen.png)

The figure illustrates the complete workflow of AgentDrive, which transforms abstract scenario specifications into curated, simulation-ready datasets. The process begins with a factorized scenario space that encodes driver behaviors, road layouts, environmental conditions, objectives, difficulty levels, and traffic density. Structured prompts are then built and passed to a diverse pool of large language models (LLMs), which generate candidate scenario JSONs. These outputs undergo schema validation, error checks, duplicate removal, and cross-model consistency verification before entering the cleaned dataset. Validated scenarios are executed in simulation, during which logs and surrogate safety metrics are collected. This is followed by rule-based labeling to assign interpretable outcome categories such as safe stop, safe goal, unsafe, or inefficient. The final curated dataset provides a diverse and safety-critical benchmark that supports training and evaluation of agentic AI systems in autonomous driving.


## AgentDrive-MCQ - Architecture Design

The framework for creating the AgentDrive-MCQ Dataset is illustrated in the figure below.

![Description of image](Images/AgentDrive_MCQ.jpg)

The process begins with the AgentDrive dataset, which encodes scenario attributes such as road layout, weather conditions, traffic density, and event triggers. These features are formalized into JSON files that serve as the structured representation of driving scenarios. A dedicated prompt builder then reformulates the structured data into prompts for a pool of LLMs, including DeepSeek-V3.1, GPT-4o, kimi-k2, and GPT-5o. The LLM pool generates narrative scenario descriptions and subsequently produces five reasoning-intensive MCQs per scenario, corresponding to the physics, policy, hybrid, scenario, and comparative styles. The intermediate outputs are stored as labeled JSON files and passed through a cross-check validation stage to ensure consistency and correctness. Finally, the validated items are aggregated into the AgentDrive-MCQ dataset, providing a robust benchmark for evaluating context-sensitive reasoning under multi-factor constraints.


## Available Datasets
There are currently three types of datasets available: **AgentDrive-Gen**, **AgentDrive-Sim**, and **AgentDrive-MCQ**.

**1. AgentDrive-Gen**: 300K structured, simulation-ready JSON scenarios across seven axes (scenario type, driver behavior, environment, road layout, objective, difficulty, traffic density).

<details>
<summary>Click to expand JSON example</summary>

```json
{
  "name": "ObstacleOnRoad_WetHighway_v1",
  "seed": 42,
  "duration_steps": 600,
  "policy_frequency": 10,
  "road": {
    "lanes": 2,
    "speed_limit_kph": 100
  },
  "traffic_light": {
    "stopline_x": -50.0,
    "red_steps": 0,
    "green_steps": 0
  },
  "environment": {
    "weather": "wet",
    "time_of_day": "day",
    "visibility": "good"
  },
  "layout": "straight highway",
  "objective": "respond safely to road obstacle",
  "difficulty": "easy",
  "traffic_density": "high",
  "ego": {
    "spawn": {
      "x": -100.0,
      "y": 0.0,
      "v_mps": 27.78
    },
    "goal": "safe stopping"
  },
  "traffic": [
    {
      "type": "car",
      "behavior": "convoy_follower",
      "lane": 0,
      "spawn_x": -90.0,
      "v_mps": 27.78
    },
    {
      "type": "car",
      "behavior": "convoy_follower",
      "lane": 0,
      "spawn_x": -80.0,
      "v_mps": 27.78
    },
    {
      "type": "car",
      "behavior": "convoy_follower",
      "lane": 0,
      "spawn_x": -70.0,
      "v_mps": 27.78
    },
    {
      "type": "car",
      "behavior": "convoy_follower",
      "lane": 0,
      "spawn_x": -60.0,
      "v_mps": 27.78
    },
    {
      "type": "car",
      "behavior": "convoy_follower",
      "lane": 0,
      "spawn_x": -50.0,
      "v_mps": 27.78
    },
    {
      "type": "car",
      "behavior": "convoy_follower",
      "lane": 0,
      "spawn_x": -40.0,
      "v_mps": 27.78
    },
    {
      "type": "car",
      "behavior": "convoy_follower",
      "lane": 0,
      "spawn_x": -30.0,
      "v_mps": 27.78
    },
    {
      "type": "car",
      "behavior": "convoy_follower",
      "lane": 0,
      "spawn_x": -20.0,
      "v_mps": 27.78
    },
    {
      "type": "car",
      "behavior": "convoy_follower",
      "lane": 0,
      "spawn_x": -10.0,
      "v_mps": 27.78
    }
  ],
  "events": [
    {
      "t_s": 50.0,
      "type": "sudden_brake",
      "actor": 0,
      "params": {
        "decel_mps2": 4.0,
        "duration_s": 2.0
      }
    }
  ],
  "metrics": [
    "ttc_front",
    "red_light_violation",
    "min_headway",
    "collisions"
  ],
  "axes_echo": {
    "scenario_type": "obstacle on road",
    "behavior": "convoy follower",
    "environment": "wet road after rain",
    "road_layout": "straight highway",
    "objective": "respond safely to road obstacle",
    "difficulty": "easy",
    "traffic_density": "high"
  }
}

```
</details>


<a href="https://github.com/maferrag/AgentDrive/tree/main/data/AgentDrive-Gen">
📂 <b>Download AgentDrive-Gen Dataset (ZIP)</b>
</a>

<br>

##

**2. AgentDrive-Sim**: Executed rollouts with surrogate safety metrics (e.g., min-TTC) and categorical outcomes: `safe_goal`, `safe_stop`, `inefficient`, `unsafe`.

<details>
<summary>Click to expand JSON example from AgentDrive-Sim -  Simulation Rollout </summary>

```json

```
</details>

<details>
<summary>Click to expand JSON example from AgentDrive-Sim - Labeled by Episode </summary>

```json

```
</details>

<details>
<summary>Click to expand JSON example from AgentDrive-Sim - Labeled by Segment </summary>

```json

```
</details>


<a href="https://github.com/maferrag/AgentDrive/tree/main/data/AgentDrive-Sim">
📂 <b>Download AgentDrive-Sim Dataset (ZIP)</b>
</a>

##

**3. AgentDrive-MCQ**: 100K multiple-choice questions spanning five styles: `physics`, `policy`, `hybrid`, `scenario`, `comparative`.

<details>
<summary>Click to expand JSON example from AgentDrive-MCQ - physics </summary>

```json
{
  "scenario_name": "AggressiveWeaveBridgeIcy_v1",
  "style": "physics",
  "description": "The scenario takes place on a three-lane bridge with an icy deck, where the ego vehicle must yield correctly at an upcoming intersection. The road has a speed limit of 100 km/h and no active traffic signals, with the stop line positioned at x = -200.0 and no red or green light cycles. Weather is clear, during daytime, with good visibility, but the bridge surface is slippery due to ice, increasing the risk of loss of control. The ego vehicle starts at x = -350.0, y = 0.0, initially at rest, and must manage its approach to the intersection under low traffic density. Although no other traffic actors are defined in the scenario, the objective involves preparing for potential conflicts requiring proper yielding behavior. There are no scripted events such as cut-ins or sudden brakes, but the icy conditions demand cautious speed and braking to avoid skidding. Evaluation focuses on time-to-collision (ttc_front), minimum headway, collisions, and red light violations—even though signals are inactive, compliance is monitored. The scenario is classified as hard due to the challenging road conditions and the need for precise, safe yielding despite high-speed approach potential.",
  "question": "On an icy bridge with a speed limit of 100 km/h (27.78 m/s), the ego vehicle starts at rest at x = -350.0 and must stop before x = -200.0. Assume a driver reaction time of 1.5 seconds and maximum deceleration of 3 m/s² on ice. What is the minimum safe braking distance needed to avoid a red light violation, assuming the lead vehicle becomes a stationary obstacle after the driver's reaction?",
  "choices": [
    "A- 129.63 m",
    "B- 172.25 m",
    "C- 144.44 m",
    "D- 96.45 m"
  ],
  "correct_choice": "B",
  "reason": "Reaction distance = 27.78 m/s × 1.5 s = 41.67 m. Braking distance = (27.78)² / (2 × 3) = 129.58 m. Total = 41.67 + 129.58 = 171.25 m ≈ 172.25 m with rounding."
}
```
</details>

<details>
<summary>Click to expand JSON example from AgentDrive-MCQ - policy </summary>

```json
{
  "scenario_name": "AggressiveWeaveBridgeIce_v1",
  "style": "policy",
  "description": "The scenario involves an ego vehicle attempting a safe lane change to the right on a narrow two-lane mountain switchback road during a nighttime drive with poor visibility and icy road conditions. The road has a speed limit of 90 km/h, and the ego vehicle starts at 25 m/s, 150 meters before the bridge section, which features an icy surface increasing slip risk. Traffic is dense, with a lead car in the left lane initially traveling at 30 m/s exhibiting over-braking behavior, planning to merge into the right lane after 50 seconds. At 30 seconds into the simulation, the lead vehicle performs a sudden brake with a deceleration of -3.0 m/s² for 5 seconds, creating a critical front hazard. The environment is dark and icy, reducing tire traction and visibility, making maneuvering more challenging despite the scenario being classified as easy. There are no traffic signals controlling the area, and no stop lines or red-light rules apply, so red-light violations are irrelevant. The ego vehicle must complete the lane change without collision, maintaining a safe time-to-collision (TTC) with the front vehicle and avoiding excessively small headways. Key evaluation metrics include front TTC, minimum headway, collision occurrence, and red-light violations—though the latter is not applicable here. The scenario tests responsiveness to sudden braking in adverse conditions during a lane change, with an aggressive weaving context implied by the lead vehicle’s behavior. The icy bridge section over the mountain road adds realism to low-grip emergency handling.",
  "question": "The ego vehicle approaches a narrow, icy mountain switchback at night with poor visibility, planning a right lane change. A lead car suddenly brakes hard at 30 seconds, reducing traction and visibility further. Given the high risk of skidding and limited escape options, what minimum time gap should the ego vehicle maintain to the lead vehicle during the lane change, based on conservative safety policy for adverse conditions?",
  "choices": [
    "A- 1.0 second",
    "B- 1.5 seconds",
    "C- 2.0 seconds",
    "D- 3.0 seconds"
  ],
  "correct_choice": "D",
  "reason": "Adverse conditions (darkness, ice, poor visibility) demand a 3-second minimum gap per conservative safety policy. Shorter gaps increase collision risk during sudden braking on low-traction surfaces."
}
```
</details>

<details>
<summary>Click to expand JSON example from AgentDrive-MCQ - hybrid </summary>

```json
{
  "scenario_name": "AggressiveCutIn_Dawn_v1",
  "style": "hybrid",
  "description": "The objective is to handle a sudden cut-in from an aggressive driver while maintaining a safe following distance. The scenario takes place on a straight dirt and gravel rural road with two lanes and a speed limit of 80 kph, with no traffic signals present. It is dawn with clear weather and moderate visibility, creating a challenging but manageable driving environment. Traffic density is high, with multiple vehicles including cars and a truck exhibiting cautious, normal, and aggressive behaviors. An aggressive car in lane 1 will cut into lane 0 after 3 seconds, decelerating sharply to provoke a reaction. The ego vehicle must maintain its lane and avoid collisions by adjusting speed appropriately. Key evaluation metrics include time-to-collision with the front vehicle, minimum headway maintained, and whether any collisions occur. The ego starts at 50 meters with a speed of 18 m/s, aiming to navigate safely through the dynamic traffic conditions. Success depends on timely responses to the cut-in event while adhering to safe driving practices.",
  "question": "The ego vehicle travels at 18 m/s. An aggressive car cuts in and decelerates sharply. Assume the lead vehicle becomes a stationary obstacle after the driver's reaction. What is the minimum safe headway to avoid collision, including a 1.5 s reaction and 4 m/s² deceleration?",
  "choices": [
    "A- 40.5 m",
    "B- 20.25 m",
    "C- 60.75 m",
    "D- 27.0 m"
  ],
  "correct_choice": "C",
  "reason": "Reaction distance = v × t_r = 18 × 1.5 = 27 m. Braking distance = v² / (2a) = 18² / (2×4) = 40.5 m. Total safe headway = 27 + 40.5 = 67.5 m ≈ 60.75 m, making option C the best safety margin."
}

```
</details>

<details>
<summary>Click to expand JSON example from AgentDrive-MCQ - scenario </summary>

```json
{
  "scenario_name": "AggressiveWeaveBridgeIcyEasy",
  "style": "scenario",
  "description": "The scenario involves an ego vehicle entering a three-lane bridge at dawn with an icy road surface and good visibility. The objective is to park the vehicle safely while navigating the slick conditions. There are no traffic signals or stop lines active, allowing continuous traffic flow. The road layout is a straight bridge with a high-speed limit of 90 kph, and the deck is covered in ice, reducing traction. Traffic density is medium, but no other vehicles are initially present in the simulation. The ego vehicle starts 100 meters before the bridge with an initial speed of 25 m/s, approaching the parking zone. Despite the \"aggressive driver weaving\" context in the metadata, no traffic actors or events such as cut-ins or sudden braking are defined. The evaluation focuses on time-to-collision with frontal obstacles, red light violations (though lights are inactive), minimum headway, and collision occurrences. Overall, the scenario tests controlled deceleration and precise parking under slippery conditions with minimal external hazards.",
  "question": "The ego vehicle approaches a three-lane icy bridge at dawn with good visibility, traveling at 25 m/s (90 km/h) and aiming to park safely. The road has no active signals or obstacles, but the surface is slippery, and the speed limit is 90 kph. Given the high initial speed and low-traction conditions, what should be the primary priority for safe operation?",
  "choices": [
    "A- Maintain current speed to ensure visibility and control in low-light conditions",
    "B- Begin immediate and aggressive braking to minimize collision risk",
    "C- Initiate smooth, early deceleration to adapt speed to traction limits before parking",
    "D- Switch lanes repeatedly to find less icy surface while approaching the bridge"
  ],
  "correct_choice": "C",
  "reason": "On ice, traction is low, so abrupt maneuvers increase skid risk. Controlled deceleration at 25 m/s (90 km/h) is essential. Smooth slowing aligns with safe parking and physics-based driving on slippery surfaces."
}
```
</details>

<details>
<summary>Click to expand JSON example from AgentDrive-MCQ - comparative </summary>

```json
{
  "scenario_name": "AggressiveCarHairpinConstruction_v1",
  "style": "comparative",
  "description": "The objective is to maintain lane discipline through a construction zone on a gravel road featuring a hairpin turn. The road has two lanes with an 80 kph speed limit and no active traffic signals or stop lines. Clear daytime weather provides good visibility, though the gravel surface adds difficulty. An aggressive car in the adjacent lane travels faster than the ego vehicle and is set to merge into the ego's lane after 50 seconds. The ego must navigate the sharp turn while avoiding sudden maneuvers from the merging car. Evaluation metrics include time-to-collision with the front vehicle, minimum headway, and any collisions that occur. The scenario tests autonomous vehicle behavior under aggressive traffic conditions in a challenging layout. Low traffic density focuses the interaction on the two vehicles. Success requires precise control and anticipation of the other car's actions.",
  "question": "In a construction zone on a gravel road with an 80 kph limit and a hairpin turn, an aggressive car merges into your lane in 50 seconds. You must navigate the turn while avoiding sudden maneuvers. Which maneuver minimizes collision risk given the gravel surface and merging threat?",
  "choices": [
    "A- Brake moderately to increase headway",
    "B- Accelerate slightly to create space ahead",
    "C- Change lanes away from the merging car",
    "D- Maintain current speed and position"
  ],
  "correct_choice": "A",
  "reason": "Braking increases time-to-collision and headway on slippery gravel, allowing safer turn negotiation and buffer against merging car's actions."
}
```
</details>


<a href="https://github.com/maferrag/AgentDrive/tree/main/data/AgentDrive-MCQ">
📂 <b>Download AgentDrive-MCQ Dataset (ZIP)</b>
</a>

## Distributions and layout statistics across the AgentDrive scenario dataset

Distributions and layout statistics across the AgentDrive scenario dataset, showing difficulty levels, layout correlations, temporal, and environmental characteristics.

![Description of image](Images/Distribution_DriveAgent_dataset.png)


## LLM Leaderboard on AgentDrive

Accuracy (%) results of 50 examined LLM reasoning models evaluated across multiple reasoning styles using 2k samples from AgentDrive-MCQ.

![Description of image](Images/results_50LLMs.jpg)

The comparative and categorical analysis of 50 evaluated LLMs on the AgentDrive-MCQ benchmark reveals significant diversity in reasoning performance across five distinct dimensions: comparative, hybrid, physics, policy, and scenario. As summarized in the Table, proprietary frontier models such as ChatGPT 4o (82.5%) and GPT-5 Chat (81.0%) from OpenAI dominated the benchmark, achieving perfect or near-perfect accuracy in policy (100%) and scenario (97.5%) reasoning tasks. These results underscore their superior contextual reasoning, ethical prioritization, and adaptability to complex decision-making scenarios. Among open-source systems, Qwen3 235B A22B reached a competitive 81.0% overall accuracy, leading in physics-driven reasoning (67.5%), while ERNIE 4.5 300B A47B achieved 75.0\%, reflecting the growing maturity of Chinese foundation models. Other strong performers, including Mistral Medium 3.1 (80.0%) and GPT-4.1 Mini (77.5%), demonstrated balanced reasoning proficiency across multiple domains, highlighting the value of large-scale fine-tuning and domain adaptation.

## Top models by highest Overall: SAS vs. SCR

<img src="Images/SCR_vs_SAS_Results.png" width="70%">


The figure visualizes the relationship between the Situational Awareness Score (SAS) and the Safety Compliance Rate (SCR) for the top models ranked by Overall Accuracy from the previous Table. The upper-right region of the scatter plot denotes the ideal operational zone, where models achieve both high situational awareness and strong safety compliance.

<h2 align="center">📖 Citation</h2>

If you use <b>AgentDrive</b> or any of its benchmark datasets in your research, please cite it as:

```bibtex
@misc{Ferrag2025AgentDrive,
  title = {AgentDrive: An Open Benchmark Dataset for Agentic AI Reasoning with LLM-Generated Scenarios in Autonomous Systems},
  author = {Mohamed Amine Ferrag, Abderrahmane Lakas, Merouane Debbah},
  howpublished = {GitHub repository},
  year = {2025},
  note = {Available at: \url{https://github.com/maferrag/AgentDrive}},
  url = {https://github.com/maferrag/AgentDrive}
}
```


<h2 align="center">📫 Contact</h2>

<p align="center">
  <b>Dr. Mohamed Amine Ferrag</b><br>
  Associate Professor, United Arab Emirates University (UAEU)<br><br>

  📧 <a href="mailto:mohamed.ferrag@uaeu.ac.ae">mohamed.ferrag@uaeu.ac.ae</a> |
  <a href="mailto:mohamed.amine.ferrag@gmail.com">mohamed.amine.ferrag@gmail.com</a><br><br>

  🌐 <a href="https://scholar.google.fr/citations?user=IkPeqxMAAAAJ&hl=fr&oi=ao">Google Scholar</a> |
  🔗 <a href="https://www.scopus.com/authid/detail.uri?authorId=56115001200">Scopus</a> |
  🧭 <a href="https://www.webofscience.com/wos/author/rid/M-2909-2016">Web of Science</a> |
  💼 <a href="https://www.linkedin.com/in/mohamed-amine-ferrag-phd-36390243/">LinkedIn</a>
</p>



---
