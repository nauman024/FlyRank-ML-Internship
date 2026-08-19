# AI Workflow Audit & System Setup (FL-01)

**Track:** AI Fluency — Week 1  

---

## 1. Recurring Weekly Workflow Audit

| # | Recurring Task | Classification | One-Line Rationale |
| :--- | :--- | :--- | :--- |
| 1 | **Model Architecture & Trade-off Decisions** | **Just Me** | Requires human accountability, holistic system context, and deep judgment on latency vs. accuracy trade-offs. |
| 2 | **Personal Technical Journaling & Goal Review** | **Just Me** | Deep personal reflection and self-evaluation lose authentic value and self-awareness if outsourced to an LLM. |
| 3 | **Scaffolding Repetitive Boilerplate Code** | **Delegate to AI with Review** | LLMs quickly generate boilerplate structures (e.g., PyTorch training loops, DuckDB SQL queries), requiring only verification. |
| 4 | **Refactoring & Linting Python Scripts** | **Delegate to AI with Review** | Static code improvements, clean formatting, and style linting follow standard patterns that AI executes cleanly. |
| 5 | **Synthesizing Research Papers & Documentation** | **Collaborate with AI** | AI rapidly extracts key methodologies from dense documentation, while I verify mathematical limits and assumptions. |
| 6 | **Brainstorming System Architectures & Edge Cases** | **Collaborate with AI** | Iterative back-and-forth prompting surfaces overlooked failure modes and alternative design patterns for pipelines. |
| 7 | **Technical Case Study & Portfolio Drafting** | **Collaborate with AI** | AI structures complex ideas while I inject verified benchmark data, authentic voice, and public-safe language. |
| 8 | **Automated Formatting of Daily Logs** | **Fully Automate** | Deterministic text restructuring and cleaning require standard rule-based parsing with no cognitive oversight. |
| 9 | **Translating SQL Queries to PySpark/DuckDB** | **Delegate to AI with Review** | Syntax translation between analytical engines is mechanical and fast for LLMs, requiring only query plan validation. |
| 10 | **Debugging Runtime & Environment Stack Traces** | **Collaborate with AI** | AI rapidly parses cryptic dependency conflicts and CUDA/C++ build errors while I test proposed environment patches. |
| 11 | **Drafting Pull Request Summaries** | **Delegate to AI with Review** | Generating standard commit and PR markdown templates from diff summaries saves time and needs only quick proofreading. |
| 12 | **Daily Task Scheduling & Work Prioritization** | **Just Me** | Aligning high-energy blocks with deep research vs. coursework requires real-time personal context and energy management. |

---

## 2. Target Tasks for FL-02 through FL-04

### Target Task 1: Research Paper & Technical Documentation Synthesis
* **Classification:** Collaborate with AI
* **"Done Well" Definition:** Produces a structured 1-page brief identifying: (1) Core problem framing, (2) Baseline vs. proposed method, (3) Key mathematical formulation, (4) Measured results, and (5) Limitations—with zero hallucinated claims and 100% verified citation alignment.

### Target Task 2: Data Pipeline & Model Boilerplate Scaffolding (DuckDB / PyTorch)
* **Classification:** Delegate to AI with Review
* **"Done Well" Definition:** Generates executable, modular Python code that runs out-of-the-box without syntax errors, includes strict type hinting, and adheres to data leakage guards (e.g., proper validation grouping).

### Target Task 3: Technical Case Study & Milestone Storytelling
* **Classification:** Collaborate with AI
* **"Done Well" Definition:** Transforms raw experiment receipts and metrics into a clear narrative featuring a 5-minute demo structure, an employer summary, and public-safe claim language (*observed*, *measured*, *decision-support*).

---

## 3. Toolkit Setup & Course Evidence

### Free Toolkit Configuration
* **Claude Account:** Active (Claude 3.5 Sonnet workspace configured).
* **ChatGPT Account:** Active (GPT-4o workspace ready).
* **Anthropic Academy:** Enrolled in *AI Fluency: Framework & Foundations* (Full Course completed).

### Configured Custom Instructions (Claude Project)
```text
You are an expert AI engineering collaborator and technical thought partner.

### User Context
- Role: Computer Science student & Machine Learning practitioner.
- Core Domains: Distributed Systems, High-Performance Computing, Computer Vision, and Applied Search/Data Engineering.
- Primary Stack: Python, PyTorch, DuckDB, scikit-learn, SQL, Linux.

### Tone & Style Preferences
- Communication Style: Direct, technically precise, candid, and authentic. No conversational filler or boilerplate praise.
- Technical Rigor: Prioritize concrete specifics over broad generalizations. Provide step-by-step logic and mathematical reasoning where appropriate.
- Framing: Use precise scientific language (e.g., "observed," "measured," "directional decision-support") rather than causal absolutes.
- Code Standards: Clean, modern, production-grade Python with typing and clear comments explaining non-trivial logic.

### Current Goals
- Mastering AI Fluency frameworks (evaluating, collaborating, and automating workflows responsibly).
- Building leakage-proof machine learning pipelines and deploying reproducible research artifacts.
```
---

## Verification Artifacts

### 1. Claude Project Configuration
![Claude Project Setup](screenshots/claude_project_setup.png)

### 2. Anthropic Academy Module 1 Completion
![Anthropic Academy Module 1](screenshots/anthropic_academy_module1.png)