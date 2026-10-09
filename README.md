<picture>
  <source media="(prefers-color-scheme: light)" srcset="./assets/header-light.svg">
  <img alt="Raghav Pimoli — AI/ML Engineer. 4 end-to-end projects, 1 public model on Hugging Face, 2 custom evaluation harnesses." src="./assets/header-dark.svg" width="100%">
</picture>

<br>

I build AI systems end to end (fine-tuning, agents, computer vision and deployment) and evaluate each one against a baseline on held-out data.

<a href="mailto:raghavpimoli5@gmail.com"><img src="https://img.shields.io/badge/Email-0B0B0B?style=flat-square&logo=gmail&logoColor=FF5A1F" alt="Email"></a>
<a href="https://www.linkedin.com/in/raghav-pimoli-6b79a6362"><img src="https://img.shields.io/badge/LinkedIn-0B0B0B?style=flat-square&logo=linkedin&logoColor=FF5A1F" alt="LinkedIn"></a>
<a href="https://huggingface.co/PimoLee5"><img src="https://img.shields.io/badge/Hugging%20Face-0B0B0B?style=flat-square&logo=huggingface&logoColor=FF5A1F" alt="Hugging Face"></a>

<br><br>

<picture>
  <source media="(prefers-color-scheme: light)" srcset="./assets/sec-work-light.svg">
  <img alt="Selected work" src="./assets/sec-work-dark.svg" width="100%">
</picture>

<p>
  <a href="https://github.com/raghavpli515/Legal-contract-LLM-fine-tuning-with-evaluation"><picture><source media="(prefers-color-scheme: light)" srcset="./assets/project-01-light.svg"><img alt="01 Legal Contract LLM — 80.0% clause accuracy" src="./assets/project-01-dark.svg" width="100%"></picture></a>
</p>
<p>
  <a href="https://github.com/raghavpli515/adversarial-verification"><picture><source media="(prefers-color-scheme: light)" srcset="./assets/project-02-light.svg"><img alt="02 Adversarial Verification — 0.7% hallucination rate" src="./assets/project-02-dark.svg" width="100%"></picture></a>
</p>
<p>
  <a href="https://github.com/raghavpli515/Agentic-multimodal-behavioral-consistency-analysis"><picture><source media="(prefers-color-scheme: light)" srcset="./assets/project-03-light.svg"><img alt="03 Behavioral Intelligence — 70.4% F1 score" src="./assets/project-03-dark.svg" width="100%"></picture></a>
</p>
<p>
  <a href="https://github.com/raghavpli515/Sensitive-area-Intrusion-detection-system"><picture><source media="(prefers-color-scheme: light)" srcset="./assets/project-04-light.svg"><img alt="04 Intrusion Detection — 86.0% mAP50" src="./assets/project-04-dark.svg" width="100%"></picture></a>
</p>

<picture>
  <source media="(prefers-color-scheme: light)" srcset="./assets/capabilities-light.svg">
  <img alt="Capabilities: fine-tuning, agents and RAG, vision and speech, evaluation and MLOps" src="./assets/capabilities-dark.svg" width="100%">
</picture>

<br><br>

<picture>
  <source media="(prefers-color-scheme: light)" srcset="./assets/sec-notes-light.svg">
  <img alt="Case notes" src="./assets/sec-notes-dark.svg" width="100%">
</picture>

<details>
<summary><b>01 &nbsp;Legal Contract LLM</b> &nbsp;·&nbsp; QLoRA fine-tuning with before/after evaluation</summary>
<br>

Fine-tuned **Qwen2.5-7B** with QLoRA (4-bit, 0.5% of weights trained) on **CUAD** — 510 expert-annotated contracts — for clause classification and grounded clause Q&A. Trained on a free Kaggle T4; served on a 6 GB laptop GPU.

| Held-out set (400 items) | Zero-shot | 3-shot | **Fine-tuned** |
|---|---:|---:|---:|
| Classification accuracy | 61.5% | 63.5% | **80.0%** |
| Missed clauses | 57% | — | **5%** |
| Calibration error | 0.28 | — | **0.03** |
| Hallucination rate | 1.0% | — | 3.5% |

Deterministic harness, no LLM judge, hallucinations audited by hand. The hallucination increase is the trade-off, reported rather than hidden.

`PyTorch` `Transformers` `PEFT` `TRL` `FastAPI` `Streamlit` &nbsp;→&nbsp; [Repository](https://github.com/raghavpli515/Legal-contract-LLM-fine-tuning-with-evaluation) · [Model](https://huggingface.co/PimoLee5/qwen2.5-7b-cuad-qlora) · [Video](https://youtu.be/hcN9TmknxCs)
</details>

<details>
<summary><b>02 &nbsp;Adversarial Verification System</b> &nbsp;·&nbsp; multi-agent checking with an evaluation harness</summary>
<br>

A **Generator → Critic → Coordinator** pipeline in LangGraph that checks LLM outputs against retrieved evidence (hybrid dense + BM25) before returning them, with calibrated confidence scoring.

| 300 evaluations (50 prompts × 2 batches × 3 runs) | Baseline | **Verified** |
|---|---:|---:|
| Hallucination rate | 4.0% | **0.7%** |
| Accuracy | 76.7% | **86.7%** |
| False-escalation rate | — | **2.7%**, every run |

`LangGraph` `OpenAI API` `ChromaDB` `FastAPI` `Docker` `MLflow` &nbsp;→&nbsp; [Repository](https://github.com/raghavpli515/adversarial-verification) · [Video](https://youtu.be/bDHBv1_jPOI)
</details>

<details>
<summary><b>03 &nbsp;Multimodal Behavioral Intelligence</b> &nbsp;·&nbsp; M.Sc. thesis</summary>
<br>

Fuses **vision, speech and language** to analyse behavioural consistency: trust-aware multimodal fusion, temporal modelling and explainable reasoning, deployed end to end on FastAPI.

```mermaid
flowchart LR
    V[Video] --> M[MobileNetV2] --> L[BiLSTM]
    A[Audio] --> W[Whisper] --> D[DistilBERT]
    L --> F[Trust-aware fusion]
    D --> F --> X[Explainable reasoning]
```

**70.83%** accuracy · **81.34%** precision · **70.41%** F1

`PyTorch` `MobileNetV2` `DistilBERT` `BiLSTM` `Whisper` `OpenCV` `Docker` &nbsp;→&nbsp; [Repository](https://github.com/raghavpli515/Agentic-multimodal-behavioral-consistency-analysis) · [Demo video](https://youtu.be/6ccAVwpaJxg)
</details>

<details>
<summary><b>04 &nbsp;Sensitive-Area Intrusion Detection</b> &nbsp;·&nbsp; real-time computer vision</summary>
<br>

A fine-tuned **YOLOv8** detector with **DeepSORT** tracking and a rule engine for zone-intrusion, weapon and dropped-object alerts. Incident-based alerting (one event, one alert) streamed live to a React front end over WebSockets.

**87.8%** precision · **79.7%** recall · **86.0%** mAP50

`PyTorch` `YOLOv8` `DeepSORT` `FastAPI` `React` `Docker` `DVC` &nbsp;→&nbsp; [Repository](https://github.com/raghavpli515/Sensitive-area-Intrusion-detection-system) · [Try it](https://huggingface.co/spaces/PimoLee5/intrusion-detection-system) · [Video](https://youtu.be/AlxbYcq7480)
</details>

<details>
<summary><b>Toolkit</b></summary>
<br>

<img src="https://skillicons.dev/icons?i=py,pytorch,tensorflow,sklearn,opencv,fastapi,docker,postgres,mysql,react,linux,git&theme=dark&perline=12" alt="Toolkit">

Also: Hugging Face (Transformers, PEFT, TRL) · LangGraph · OpenAI API · ChromaDB · MLflow · DVC · YOLO · Whisper · C / C++
</details>

<br>

<picture>
  <source media="(prefers-color-scheme: light)" srcset="./assets/footer-light.svg">
  <img alt="©Raghav Pimoli — MMXXVI. Contact: raghavpimoli5@gmail.com" src="./assets/footer-dark.svg" width="100%">
</picture>
