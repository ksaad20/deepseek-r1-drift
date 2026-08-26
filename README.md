# deepseek-r1-drift
A longitudinal time-series dataset tracking reasoning chain decay, token count efficiency drops, and alignment policy shifts in deployed DeepSeek-R1 and reasoning models

# DeepSeek-R1-Drift: Tracking Systematic Reasoning Decay and Policy Shift in Thinking Models

[![License](https://shields.io)](https://opensource.org)
[![Python 3.10+](https://shields.io)](https://python.org)
[![Static Badge](https://shields.io)](https://arxiv.org)


A time-series, longitudinal monitoring framework and benchmark dataset capturing **systematic reasoning drift, token efficiency decay, and latent alignment shifts** in deployed DeepSeek-R1 and DeepSeek-V3 instances (including official API endpoints, Groq, Together AI, and Hugging Face mirror deployments).

---

## 💡 The Core Problem

As frontier Large Language Models (LLMs)—specifically specialized reasoning models utilizing reinforcement learning (RL) like **DeepSeek-R1**—undergo continuous optimization, quantization, and over-the-air (OTA) alignment filtering, their internal search paths silently shift. 

Standard benchmark datasets (MMLU, MATH, HumanEval) are static, vulnerable to data contamination, and do not capture behavioral modifications over time. **DeepSeek-R1-Drift** solves this by programmatically running an adversarial, multi-turn prompt matrix daily. It measures when updates intended to restrict harmful content or reduce serving costs accidentally compromise a model's deep reasoning chain.

---

## 📊 Dataset Schema

The automated Python testing harness continuously outputs a structured `.csv` / `.json` dataset containing the following features:

| Field Name | Type | Description |
| :--- | :--- | :--- |
| `timestamp` | UTC IsoDateTime | Exact execution timeline of the automated probe cycle. |
| `endpoint_provider` | String | Hosting provider (`deepseek_api`, `groq`, `together_ai`, `ollama_local`). |
| `model_tag` | String | Explicit model flag queried (e.g., `deepseek-reasoner`, `deepseek-r1-distill-llama-70b`). |
| `domain_category` | String | Target failure vector (`olympiad_math`, `exploit_mitigation`, `jailbreak_compliance`). |
| `raw_thought_chain` | String | The full extracted text enclosed within the `<think>` tags. |
| `thought_token_count`| Integer | Total tokens expended inside the thinking process before outputting the final answer. |
| `final_response` | String | The clean, parsed answer served to the end user. |
| `semantic_drift_score`| Float (0.0 - 1.0)| Cosine distance of current embedding vs. the baseline January 2025 model release. |
| `reasoning_status` | Categorical | Evaluation result (`success`, `hallucinated_step`, `premature_termination`, `silent_refusal`). |

---

## 🚀 Quick Start & Automation Engine

### Installation

```bash
pip install -r requirements.txt
```

### Run the Probing Pipeline
To trigger tonight's batch collection loop and append live metrics to the dataset:

```bash
python run_probe_cycle.py --provider deepseek_api --output ./data/daily_log.csv
```

---

## 🔬 Academic Citation

If you utilize this dataset, code, or methodology in your academic publications, please cite this repository using the following format:

```bibtex
@misc{deepseek_r1_drift_2026,
  author       = {Your Name},
  title        = {DeepSeek-R1-Drift: A Longitudinal Dataset Tracking Reasoning Decay and Policy Shift in Deployed RL Models},
  year         = {2026},
  publisher    = {GitHub},
  journal      = {GitHub Repository},
  howpublished \(= {\url{https://github.com}} \)}
```

## ⚖️ Commercial Value Statement
Enterprise workflows dependent on deterministic logic pipelines use this dataset to evaluate API stability over time, actively protecting production agents against silent regression risks.
