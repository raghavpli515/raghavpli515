<!--
  SETUP — replace these placeholders before publishing:
    YOUR_LINKEDIN_URL      → full LinkedIn profile URL
    YOUR_HF_USERNAME       → your Hugging Face handle
    REPO_* / DEMO_* / VIDEO_* links → the links already on your resume
-->

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="./assets/header-dark.svg">
  <img alt="Raghav Pimoli — AI/ML Engineer" src="./assets/header-light.svg" width="100%">
</picture>

<p align="center">
  <a href="https://git.io/typing-svg"><img src="https://readme-typing-svg.demolab.com?font=Inter&weight=700&size=22&duration=2600&pause=900&color=FA500F&center=true&vCenter=true&width=760&lines=Fine-tuning+7B+LLMs+on+a+free+T4+GPU;Agents+that+verify+their+own+answers;Evaluation+harnesses%2C+not+vibes;Vision+%C2%B7+Speech+%C2%B7+Language+%E2%80%94+fused" alt="What I build"></a>
</p>

<p align="center">
  <a href="mailto:raghavpimoli5@gmail.com"><img src="https://img.shields.io/badge/Email-raghavpimoli5@gmail.com-FA500F?style=flat-square&logo=gmail&logoColor=white" alt="Email"></a>
  <a href="YOUR_LINKEDIN_URL"><img src="https://img.shields.io/badge/LinkedIn-Connect-FF8205?style=flat-square&logo=linkedin&logoColor=white" alt="LinkedIn"></a>
  <a href="https://huggingface.co/YOUR_HF_USERNAME"><img src="https://img.shields.io/badge/Hugging%20Face-Models-FFAF00?style=flat-square&logo=huggingface&logoColor=black" alt="Hugging Face"></a>
  <img src="https://img.shields.io/badge/Status-Open%20to%20AI%2FML%20Engineer%20roles-E10500?style=flat-square" alt="Open to work">
</p>

<img src="./assets/divider.svg" width="100%">

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="./assets/sec-about-dark.svg">
  <img alt="01 About" src="./assets/sec-about-light.svg" width="100%">
</picture>

I'm an AI/ML engineer who builds end-to-end systems — from fine-tuning and agent design to deployment — and **holds them to an evaluation harness before trusting them**. Every number below comes with a baseline, a held-out set, and the trade-offs reported, not hidden.

```yaml
name:      Raghav Pimoli
role:      AI / ML Engineer
education: M.Sc. Artificial Intelligence & Machine Learning — IIIT Lucknow (2024–26)
focus:     [LLM fine-tuning, LLM evaluation, agentic AI, multimodal AI, computer vision, MLOps]
habits:    baselines first · deterministic evals · report the trade-off
based_in:  Dehradun, India
open_to:   full-time AI / ML Engineer roles
```

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="./assets/impact-dark.svg">
  <img alt="Measured impact: classification accuracy 61.5% to 80.0%, missed clauses 57% to 5%, calibration error 0.28 to 0.03, answer accuracy 76.7% to 86.7%, hallucination rate 4.0% to 0.7%" src="./assets/impact-light.svg" width="100%">
</picture>

<img src="./assets/divider.svg" width="100%">

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="./assets/sec-projects-dark.svg">
  <img alt="02 Projects" src="./assets/sec-projects-light.svg" width="100%">
</picture>

### `01` &nbsp;Legal Contract LLM — QLoRA fine-tuning with before/after evaluation

<p>
  <img src="https://img.shields.io/badge/Accuracy-61.5%25%20→%2080.0%25-FA500F?style=flat-square" alt="">
  <img src="https://img.shields.io/badge/Missed%20clauses-57%25%20→%205%25-FF8205?style=flat-square" alt="">
  <img src="https://img.shields.io/badge/Calibration%20error-0.28%20→%200.03-FFAF00?style=flat-square" alt="">
</p>

Fine-tuned **Qwen2.5-7B** with QLoRA (4-bit, 0.5% of weights trained) on **CUAD** — 510 expert-annotated contracts — for clause classification and grounded clause Q&A. Trained on a free Kaggle T4, served on a 6 GB laptop GPU.

**[Repository](REPO_LEGAL_LLM) · [Model on 🤗](HF_MODEL_LINK) · [Video](VIDEO_LEGAL_LLM)**

<details>
<summary><b>▸ How it was evaluated</b></summary>
<br>

- Deterministic harness — **no LLM judge** — over 400 held-out items
- Three-way comparison: zero-shot vs. 3-shot prompting vs. fine-tuned
- Hallucinations audited by hand

| Metric | Zero-shot | 3-shot | **Fine-tuned** |
|---|---:|---:|---:|
| Classification accuracy | 61.5% | 63.5% | **80.0%** |
| Missed clauses | 57% | — | **5%** |
| Calibration error | 0.28 | — | **0.03** |
| Hallucination rate | 1.0% | — | 3.5% ⚠️ |

> The trade-off is reported, not hidden: fine-tuning raised hallucinations from 1.0% to 3.5%.

**Stack:** PyTorch · Hugging Face Transformers / PEFT / TRL · FastAPI · Streamlit
</details>

---

### `02` &nbsp;Adversarial Verification System with LLM Evaluation Harness

<p>
  <img src="https://img.shields.io/badge/Hallucination-4.0%25%20→%200.7%25-FA500F?style=flat-square" alt="">
  <img src="https://img.shields.io/badge/Accuracy-76.7%25%20→%2086.7%25-FF8205?style=flat-square" alt="">
  <img src="https://img.shields.io/badge/False%20escalation-2.7%25-FFAF00?style=flat-square" alt="">
</p>

A multi-agent pipeline — **Generator → Critic → Coordinator** in LangGraph — that adversarially checks LLM outputs against retrieved evidence before returning them, with hybrid dense + BM25 retrieval and calibrated confidence scoring.

**[Repository](REPO_ADVERSARIAL) · [Video](VIDEO_ADVERSARIAL)**

<details>
<summary><b>▸ How it was evaluated</b></summary>
<br>

- Custom 50-prompt harness, two independent batches × 3 runs = **300 evaluations**
- Tracked hallucination rate, calibration, and false-escalation rate
- False-escalation rate held at **2.7% across every run**

```mermaid
flowchart LR
    Q[Query] --> R[Hybrid retrieval<br/>dense + BM25]
    R --> G[Generator]
    G --> C[Critic]
    C -->|challenges| G
    C --> K[Coordinator]
    K -->|confident| A[Answer]
    K -->|uncertain| E[Escalate]
```

**Stack:** LangGraph · OpenAI API · ChromaDB · FastAPI · Streamlit · Docker · MLflow
</details>

---

### `03` &nbsp;Multimodal Agentic AI Platform for Behavioral Intelligence &nbsp;<sub>M.Sc. thesis</sub>

<p>
  <img src="https://img.shields.io/badge/Precision-81.34%25-FA500F?style=flat-square" alt="">
  <img src="https://img.shields.io/badge/Accuracy-70.83%25-FF8205?style=flat-square" alt="">
  <img src="https://img.shields.io/badge/F1-70.41%25-FFAF00?style=flat-square" alt="">
</p>

A platform that fuses **vision, speech and language** to analyse behavioural consistency — trust-aware multimodal fusion, temporal behavioural modelling, and explainable reasoning, deployed end-to-end on FastAPI.

**[Repository](REPO_MULTIMODAL) · [Live demo](DEMO_MULTIMODAL)**

<details>
<summary><b>▸ Architecture</b></summary>
<br>

```mermaid
flowchart LR
    V[Video frames] --> M[MobileNetV2]
    A[Audio] --> W[Whisper] --> D[DistilBERT]
    M --> L[BiLSTM<br/>temporal]
    L --> F[Trust-aware fusion]
    D --> F
    F --> X[Explainable<br/>reasoning]
```

**Stack:** PyTorch · MobileNetV2 · DistilBERT · BiLSTM · Whisper · OpenCV · FastAPI · Docker
</details>

---

### `04` &nbsp;Sensitive-Area Intrusion Detection System

<p>
  <img src="https://img.shields.io/badge/mAP50-86.0%25-FA500F?style=flat-square" alt="">
  <img src="https://img.shields.io/badge/Precision-87.8%25-FF8205?style=flat-square" alt="">
  <img src="https://img.shields.io/badge/Recall-79.7%25-FFAF00?style=flat-square" alt="">
</p>

Full-stack real-time surveillance: a fine-tuned **YOLOv8** detector with **DeepSORT** tracking and a rule engine for zone-intrusion, weapon, and dropped-object alerts, streamed live to the browser over WebSockets.

**[Repository](REPO_INTRUSION) · [Try it](DEMO_INTRUSION) · [Video](VIDEO_INTRUSION)**

<details>
<summary><b>▸ How it works</b></summary>
<br>

- Incident-based alerting model, so one event raises one alert rather than one per frame
- Live webcam detection over a WebSocket pipeline to a React front end
- Data and model versioning with DVC

**Stack:** PyTorch · YOLOv8 · DeepSORT · FastAPI · React · Docker · DVC
</details>

<img src="./assets/divider.svg" width="100%">

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="./assets/sec-toolkit-dark.svg">
  <img alt="03 Toolkit" src="./assets/sec-toolkit-light.svg" width="100%">
</picture>

<p align="center">
  <img src="https://skillicons.dev/icons?i=py,pytorch,tensorflow,sklearn,opencv,fastapi,docker,postgres,mysql,react,linux,git,github,c,cpp&perline=8" alt="Toolkit">
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Hugging%20Face-Transformers%20·%20PEFT%20·%20TRL-FFAF00?style=flat-square&logo=huggingface&logoColor=black" alt="">
  <img src="https://img.shields.io/badge/LangGraph-agents-FA500F?style=flat-square" alt="">
  <img src="https://img.shields.io/badge/OpenAI%20API-LLMs-FF8205?style=flat-square&logo=openai&logoColor=white" alt="">
  <img src="https://img.shields.io/badge/ChromaDB-RAG-FFAF00?style=flat-square" alt="">
  <img src="https://img.shields.io/badge/MLflow-tracking-FA500F?style=flat-square&logo=mlflow&logoColor=white" alt="">
  <img src="https://img.shields.io/badge/DVC-versioning-FF8205?style=flat-square&logo=dvc&logoColor=white" alt="">
  <img src="https://img.shields.io/badge/YOLOv8-detection-E10500?style=flat-square" alt="">
  <img src="https://img.shields.io/badge/Whisper-speech-FFAF00?style=flat-square" alt="">
</p>

<details>
<summary><b>▸ Full skill map</b></summary>
<br>

| Area | Skills |
|---|---|
| **LLM & agentic AI** | QLoRA / LoRA fine-tuning, LLM evaluation, RAG, prompt engineering, multi-agent systems |
| **Machine learning** | Deep learning, computer vision, NLP, speech AI, multimodal AI, reinforcement learning |
| **MLOps** | Docker, MLflow, DVC, FastAPI, Linux, Git |
| **Languages & data** | Python, SQL, PostgreSQL, MySQL, C, C++ |
</details>

<details>
<summary><b>▸ GitHub activity</b></summary>
<br>
<p align="center">
  <img height="165" src="https://github-readme-stats.vercel.app/api?username=raghavpli515&show_icons=true&hide_border=true&bg_color=FFFAEB&title_color=FA500F&icon_color=FF8205&text_color=111111" alt="GitHub stats">
  <img height="165" src="https://github-readme-stats.vercel.app/api/top-langs/?username=raghavpli515&layout=compact&hide_border=true&bg_color=FFFAEB&title_color=FA500F&text_color=111111" alt="Top languages">
</p>
</details>

<img src="./assets/divider.svg" width="100%">

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="./assets/sec-contact-dark.svg">
  <img alt="04 Contact" src="./assets/sec-contact-light.svg" width="100%">
</picture>

<p align="center">
  <b>Building something that needs to be measured, not guessed? Let's talk.</b><br><br>
  <a href="mailto:raghavpimoli5@gmail.com"><img src="https://img.shields.io/badge/Say%20hello-raghavpimoli5@gmail.com-FA500F?style=for-the-badge&logo=gmail&logoColor=white" alt="Email me"></a>
  <a href="YOUR_LINKEDIN_URL"><img src="https://img.shields.io/badge/LinkedIn-Raghav%20Pimoli-FF8205?style=for-the-badge&logo=linkedin&logoColor=white" alt="LinkedIn"></a>
</p>

<img src="./assets/divider.svg" width="100%">
