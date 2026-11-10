# Tech Stack Evaluation

## Project
AI-Powered Traffic Summons Assistant for MyBayar PDRM

## Requirements that drive the decision
List 3 to 5 requirements from your own docs/requirements.md. Include at
least 2 non-functional requirements.
- [FR1]: The system shall allow users to ask questions about traffic summonses in simple Bahasa Melayu or English through a natural language chat interface.
- [FR2]: The system shall retrieve real-time fine schedules, discount campaign rules, and offense details from an official PDRM knowledge base.
- [NFR1]: The system shall respond to user queries within 3.0 seconds under standard internet connectivity.
- [NFR2]: The system shall maintain an answer accuracy rate of at least 98% based on official PDRM guidelines, keeping factual errors below 2%

## Options
- Option A: Static Website (HTML/CSS/JS hosted on GitHub Pages + Direct Client-side API Calls)
- Option B: Python Streamlit Web App with RAG (LangChain/ChromaDB) hosted on Streamlit Cloud
- Option C: Full-Stack Architecture (React Frontend + Python FastAPI Backend + PostgreSQL) hosted on AWS/Docker

## Decision matrix
Weight: how important the criterion is for YOUR project (1 = low, 5 = high).
Score: how well each option does (1 = poor, 5 = excellent).
Weighted score = weight x score. Add them up for each option.

| Criterion                          | Weight | A score | B score | C score |
|------------------------------------|--------|---------|---------|---------|
| Fits my requirements               |    5   |    10   |   25    |   25    |
| Skills I already have              |    4   |    16   |   16    |    8    |
| Time to build before my deadline   |    5   |    20   |   25    |   10    |
| Free hosting and tools             |    5   |    25   |   25    |   10    |
| Performance and security needs     |    4   |     8   |   16    |   20    |
| Room to grow later                 |    3   |     6   |   12    |   15    |
| **Total (weighted)**               |    -   |    85   |  119    |   88    |

## Decision record
- **Context:** Motorists in Malaysia face confusion regarding PDRM traffic summons discount rules and court attendance mandates.    The goal is to build an AI retrieval system under tight constraints: a 3-week completion deadline, 100% free hosting requirements, and a developer skillset rooted in Python and basic Git/web workflows.
- **Decision:** Option B — Python Streamlit Web App with RAG (LangChain/ChromaDB) hosted on Streamlit Cloud.
- **Reasons:** 
    1. **Direct RAG and AI Integration (FR1 and FR2):** Streamlit operates natively in Python, enabling seamless integration with LangChain and ChromaDB for vector retrieval of official PDRM summons guidelines without complex client-server API bridges.
    2. **Rapid Prototyping &amp; Free Hosting:** Streamlit Cloud offers 100% free hosting directly from GitHub repositories and eliminates UI boilerplate code, allowing a full working prototype to be built well before the deadline. 
    3. **Server-Side Security &amp; Performance (NFR1 and NFR2):** Unlike Option A (which exposes API keys in client-side JavaScript), Option B executes securely on the server, maintaining strict key security while comfortably keeping query latency under 3.0 seconds.
- **Consequences:** [what becomes easy, what becomes hard]
    - *What becomes easy:* Building interactive chat components, managing vector database queries in pure Python, and deploying instant updates via GitHub pushes. 
    - *What becomes hard:* Customizing low-level CSS styling (Streamlit imposes a fixed layout), and managing cold-start latency when free cloud containers go to sleep after inactivity.
- **Risks and next review:** [what could go wrong, and when you will check again]
    - *Risks:* Streamlit Cloud container sleeping can cause a 10–15 second initial load delay for the first visitor, potentially violating NFR1 on first load. Memory limits on free tiers (1 GB RAM) could choke on large vector embeddings. 
    - *Next review:* End of Week 6, prior to final Assignment 1 report submission.
