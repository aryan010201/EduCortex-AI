# EduCortex-AI 🧠

<div align="center">

![EduCortex AI](EduCortex_logo.png)

**An AI-powered study assistant that turns your notes into an interactive tutor.**

[![Python](https://img.shields.io/badge/Python-3.10+-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://python.org)
[![Streamlit](https://img.shields.io/badge/Streamlit-1.56-FF4B4B?style=for-the-badge&logo=streamlit&logoColor=white)](https://streamlit.io)
[![LangChain](https://img.shields.io/badge/LangChain-0.4-1C3C3C?style=for-the-badge&logo=langchain&logoColor=white)](https://langchain.com)
[![Groq](https://img.shields.io/badge/Groq-LLM-F55036?style=for-the-badge)](https://groq.com)
[![ChromaDB](https://img.shields.io/badge/ChromaDB-Vector%20Store-orange?style=for-the-badge)](https://trychroma.com)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow?style=for-the-badge)](LICENSE)

</div>

---

## ✨ What is EduCortex AI?

EduCortex AI is a **multi-agent Retrieval-Augmented Generation (RAG)** study platform. Upload your lecture notes, PDFs, or Word docs and get:

- 📖 **Deep Explanations** — concept-level answers grounded strictly in your notes
- ❓ **Auto-Generated Quiz** — practice questions crafted from your material
- ✅ **AI Feedback & Report Card** — get scored and corrected on your answers
- 🔁 **Follow-up conversations** — ask clarifying questions in context
- 🧠 **Session Memory** — the AI remembers what you've discussed

---

## 🏗️ Architecture

```
User Upload (PDF / DOCX / TXT)
        │
        ▼
  Text Extraction (rag.py)
        │
        ▼
  ChromaDB Vector Store  ◄──── HuggingFace Embeddings (all-MiniLM-L6-v2)
        │
        ▼
  Intent Classifier  ──► EXPLAIN / QUIZ / EVALUATE / FOLLOWUP / CHAT
        │
        ▼
  ┌─────────────────────────────────────────┐
  │           Multi-Agent Pipeline           │
  │  ┌──────────────┐  ┌──────────────────┐ │
  │  │ Analyzer     │  │ Question Gen     │ │
  │  │ Agent        │  │ Agent            │ │
  │  └──────────────┘  └──────────────────┘ │
  │  ┌──────────────┐  ┌──────────────────┐ │
  │  │ Structure &  │  │ Feedback /       │ │
  │  │ Polish Agent │  │ Evaluator Agent  │ │
  │  └──────────────┘  └──────────────────┘ │
  │           Summarizer Agent               │
  └─────────────────────────────────────────┘
        │
        ▼
  Streamlit UI  (app.py)
```

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| **Frontend** | Streamlit |
| **LLM** | Groq API (Llama 3 / Mixtral) |
| **Orchestration** | LangChain |
| **Vector Store** | ChromaDB |
| **Embeddings** | HuggingFace `all-MiniLM-L6-v2` |
| **Document Parsing** | PyPDF2, python-docx |
| **Evaluation** | RAGAS, Pandas |

---

## 🚀 Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/aryan010201/EduCortex-AI.git
cd EduCortex-AI
```

### 2. Install dependencies

```bash
pip install -r requirements.txt
```

### 3. Set up environment variables

Copy `.env.example` to `.env` and fill in your API key:

```bash
cp .env.example .env
```

Then edit `.env`:

```env
GROQ_API_KEY=your_groq_api_key_here
```

> Get your free Groq API key at [console.groq.com](https://console.groq.com)

### 4. Run the app

```bash
streamlit run app.py
```

The app will open at `http://localhost:8501`

---

## 📁 Project Structure

```
EduCortex-AI/
├── app.py                  # Streamlit UI & session management
├── backend.py              # Core query processing & memory
├── agents.py               # Multi-agent definitions (Analyzer, Quiz, Feedback, etc.)
├── rag.py                  # Document ingestion & vector retrieval
├── prompts.py              # All LLM prompt templates
├── evaluate_pipeline.py    # RAG evaluation with RAGAS
├── eval_dataset.json       # Evaluation dataset
├── requirements.txt        # Python dependencies
├── .env.example            # Environment variable template
├── EduCortex_logo.png        # App logo
└── .streamlit/
    └── config.toml         # Streamlit theme config
```

---

## ⚙️ Key Features

### 🔒 Hallucination Guardrails
All answers are **grounded strictly in uploaded notes**. If the answer isn't in your material, the AI says so — it never fabricates.

### 🤖 Multi-Agent Pipeline
- **Analyzer Agent** — classifies query depth and topic
- **Question Generator Agent** — generates unique, non-repetitive exam questions
- **Structure & Polish Agent** — formats answers with headings and examples
- **Evaluator/Feedback Agent** — scores answers and gives a report card
- **Summarizer Agent** — condenses long content

### 💾 Session Memory
The app tracks your conversation, recent topics, quiz scores, and provides a running session summary for coherent multi-turn dialogue.

---

## 📊 Evaluation

EduCortex AI includes a RAGAS-based evaluation pipeline:

```bash
python evaluate_pipeline.py
```

Metrics evaluated: **Faithfulness**, **Answer Relevancy**, **Context Recall**, **Context Precision**

---

## 🤝 Contributing

Pull requests are welcome! For major changes, please open an issue first.

---

## 📄 License

MIT License — see [LICENSE](LICENSE) for details.

---

<div align="center">
Built with ❤️ using LangChain, Groq, and Streamlit
</div>
