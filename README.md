# Azure AI Virtual Interviewer: Multimodal Resume Analysis & Mock Interview Platform

[![Python](https://img.shields.io/badge/Python-3.10%2B-blue.svg)](https://www.python.org/)
[![UI: Gradio](https://img.shields.io/badge/UI-Gradio-orange.svg)](https://gradio.app/)
[![Cloud: Azure AI](https://img.shields.io/badge/Cloud-Microsoft%20Azure-0078D4.svg)](https://azure.microsoft.com/)
[![LLM: GPT-4o & DALL-E 3](https://img.shields.io/badge/GenAI-GPT--4o%20%7C%20DALL--E%203-green.svg)](https://openai.com/)
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1gwtHbyS_hzZkQn6enfb0VwhJBZXYxQ_R?usp=sharing)

**Azure AI Virtual Interviewer** is an end-to-end multimodal interview preparation platform that bridges **Discriminative/Analytical AI** (Perception) and **Generative AI** (Reasoning & Creation). It integrates automated resume parsing, real-time facial emotion recognition, speech-to-text / text-to-speech interaction, dynamic interview question generation, comprehensive performance scoring, and AI-driven visual resume layout design.

---

## 📌 System Architecture & Workflow

The platform maintains state across tabs through a centralized `INTERVIEW_CONTEXT` structure:
---

## 🚀 Key Modules & AI Stack

| Layer | AI Classification | Libraries & Services | Functionality |
| :--- | :--- | :--- | :--- |
| **Resume Extraction** | Analytical AI | `pdfplumber`, Azure AI Language | Extracts raw text, cleans formatting, and extracts entities (Skills, Job Titles, Organizations). |
| **Question Generation** | Generative AI | Azure OpenAI (GPT-4o) | Generates tailored behavioral and technical questions based on candidate profile and target role. |
| **Voice Synthesis** | Generative / Perception | Azure AI Speech (TTS) | Synthesizes natural human-like voice queries for realistic interview pacing. |
| **Speech Recognition** | Analytical AI | Azure AI Speech (STT) | Audio buffer stream capture (16kHz mono WAV) and robust transcription of verbal responses. |
| **Facial & Stress Analysis**| Analytical AI | OpenCV, DeepFace | Real-time facial expression tracking (1.5s interval) and weighted stress quantification (0–100). |
| **Synthesis & Evaluation** | Generative AI | Azure OpenAI (GPT-4o) | Fuses transcript logs, stress scores, and resume data to generate a multi-dimensional assessment. |
| **Visual Resume UI** | Generative AI | Azure OpenAI (DALL-E 3) | Generates modern, aesthetic resume visual layouts to inspire candidate formatting improvements. |

---

## 💡 Engineering Challenges & Solutions

* **Dual-Column & Tabular PDF Inconsistency**:
  * *Challenge*: Raw extraction via `pdfplumber` caused interlacing of disjointed text columns, corrupting downstream entity recognition.
  * *Solution*: Implemented an intermediate text sanitization and segment filtering pipeline (`extract_text_from_pdf`) prior to Azure NLP processing, guaranteeing structural coherence.
* **Audio Buffer Interoperability (Gradio to Azure SDK)**:
  * *Challenge*: Gradio outputs audio arrays in memory (Numpy Array), whereas Azure Speech SDK demands standard WAV headers or binary streams.
  * *Solution*: Engineered a temporary streaming adapter using `pydub` and `tempfile` (`transcribe_gradio_audio`) to convert sampling rate (16,000 Hz single-channel) seamlessly without file I/O bottlenecks.
* **Context-Aware Question Granularity**:
  * *Challenge*: Initial LLM prompts yielded generic interview questions detached from specific technical competencies.
  * *Solution*: Formulated role-grounded system prompts enforcing structured outputs (`QN:`) dynamically anchored to extracted Azure entity tags.

---

## 👥 Contributors & Responsibilities

* **Li, Zhe-Qi (李哲齊)**: Core Input & Audio Pipeline
  * Architecture of PDF text extraction and Azure Text Analytics entity parsing (Tab 1).
  * Prompt engineering for GPT-4o question generation and Azure TTS speech pipeline (Tab 2).
  * Audio buffer streaming converter and Azure STT integration (Tab 3).
  * UI layout design and tab state management in Gradio.
* **Chen, Shao-Xiang (陳紹祥)**: Vision & Synthesis Pipeline
  * OpenCV facial detection, DeepFace emotional tracking, and stress calculation (Tab 4).
  * Multimodal data fusion and GPT-4o comprehensive report generation (Tab 5).
  * Azure OpenAI DALL-E 3 visual resume integration (Tab 6).
* **Wu, Zi-Xian (吳梓銜)**: Vision Support & Media Production
  * Assisted OpenCV face detection and DeepFace emotional tracking logic (Tab 4).
  * Demonstration video production, project poster layout, and presentation compilation.

---

## 🔗 Resources

* **Colab Notebook**: [Open in Google Colab](https://colab.research.google.com/drive/1gwtHbyS_hzZkQn6enfb0VwhJBZXYxQ_R?usp=sharing)