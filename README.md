![Banner](linkedin-banner.png)

# Hi, I'm Bhavisha 👋

**AI/ML Engineer · Data Science (CS) @ UIC '26 · I build AI agents that do real work, with guardrails you can trust**

I like building the whole thing: the user research, the agent pipeline, the data layer, and the UI people actually click. My projects share one rule: **the model proposes, the code decides.** The LLM handles language and judgment, while plain code owns the math, the policy checks, and anything that touches money.

I'm looking for full-time roles in **AI/ML Engineering** or **AI Product Management**, and I'm available now.

🌐 [bhavishaahuja.pro](https://www.bhavishaahuja.pro/) · 💼 [LinkedIn](https://www.linkedin.com/in/bhavisha-ahuja180503/) · ✉️ [Email](mailto:bhavishaahuja800@gmail.com)

---

## 🔨 Currently building

### [Cartkeeper](https://github.com/Bhavishaahuja/Cartkeeper): agentic purchasing for small manufacturers

When a loom stops on a mill floor, a technician needs a part *today*. Companies either wait on slow procurement while the machine sits idle, or someone buys from whoever is fastest and finance finds out weeks later. Cartkeeper gives them speed **and** control: a technician types *"Loom L-07 heald wires snapped, need 500 today"* and the agent checks the storeroom, quotes suppliers, picks the most reliable one, enforces the owner's rules, gets the right approval, and pays.

- **LangGraph, used where it earns its place:** parallel fan-out (`Send`) to check inventory and quote several suppliers at once, conditional edges for a bounded re-plan when the best option is blocked, and `interrupt()` with a Postgres checkpointer so an approval can wait for hours and survive a server restart
- **A policy gate in plain Python, with no LLM in it:** prices, categories, supplier scores, and budgets are re-read from source, never trusted from the model's proposal. Every rule that fires leaves a human-readable reason, and the agent has no tool that can approve its own purchase
- **Supplier reliability learned from the company's own order history** (the CartLens layer): on-time rate, days late, and defect rate, computed as ratios of totals and shrunk toward the pooled rate so a supplier with 2 lucky orders can't outrank one with 200 solid ones
- **Industry packs as data, not code:** urgency levels, approval tiers, budgets, and scoring weights live in a config folder. The first pack is a textile mill, and the core never branches on industry
- 76 tests covering the graph, policy gate, scoring, durable resume, and API, plus live tests against the real model

**Status:** backend and agent graph working end to end with test-mode payments. Next up: Stripe Issuing single-use cards, login, and the web UI.
`LangGraph` `Claude API` `FastAPI` `Supabase (Postgres)` `Stripe Issuing` `pytest`

---

## 🚀 Featured Projects

### [PrepPilot](https://github.com/Bhavishaahuja/preppilot) · [preppilot.site](https://www.preppilot.site)
Meeting prep on autopilot. Give it a name and a company, and in about 20 seconds it hands you a cited briefing: a snapshot of the person, talking points, sharp questions, and how you can help each other.

- Built a custom agentic pipeline from scratch (plan → parallel research → identity check → brief) instead of reaching for a framework, so I controlled every step
- Used forced tool calls with the Claude API to get reliable structured JSON out of every step
- Wrote an identity-disambiguation step that drops same-name strangers before anything gets written, so every claim in the briefing is about the right person and links to a source
- Parallelized six research angles over the live web, cutting briefing time from ~90s to ~20s
- Shipped as a real product: Supabase magic-link auth, saved history behind row-level security, custom email through Resend, and a custom domain
- Containerized the backend with Docker and wrote Kubernetes manifests (2 replicas, probes, resource limits) for self-hosting. Production runs on Render + Vercel

**Stack:** Python · FastAPI · Claude API · Tavily · React 19 · Vite · Tailwind CSS · Supabase · Docker · Kubernetes · Render · Vercel

### [CreatorOS](https://github.com/Bhavishaahuja/CreatorOS) · [Live demo](https://creator-os-seven-topaz.vercel.app)
Content planning for Instagram creators who also have a job or classes. It reads your Google Calendar, finds the days you actually have free, and builds a plan with shoot, edit, and post deadlines.

- Ran user research with creators before writing code. Most create alongside a full-time job, and their biggest fear about AI was losing their voice, so I designed around human approval instead of full automation
- Built a RAG layer on pgvector: every approved and rejected idea is embedded, and the closest matches go back into the prompt as positive and negative examples, so suggestions get more personal over time
- Versioned every prompt change in a changelog and wrote an automated eval that checks suggestion structure, format diversity, hook length, and date validity
- Built Google Calendar OAuth with silent token refresh and a manual-availability fallback

**Stack:** Next.js · TypeScript · Claude API · Supabase · pgvector · OpenAI Embeddings · Google Calendar API · Vercel

### [DeCode](https://github.com/Bhavishaahuja/DeCode) · AEC Tech Hackathon 2026
A multi-agent system that reverse-engineers ancient megaprojects (Giza, Uruk, Mohenjo-daro, the Qin walls) the way a contractor would and turns them into a modern build playbook. Built in 26 hours at Gensler Chicago, where I did about 80% of the build on a 5-person team.

- Designed a 7-stage agent pipeline (router → archaeologist → engineer → estimator → builder → critic → presenter), with a critic that checks every answer before the user sees it
- Built an evidence layer that extracts, dedupes, validates, and reviews construction claims from archaeological sources, so every conclusion is cited
- Kept the math out of the LLM: labor, time, haul force, and carbon come from deterministic engineering tools behind a FastAPI service
- Added a rule-based fallback so the whole pipeline still runs without an API key

**Stack:** Python · FastAPI · Uvicorn · Claude API

### [CartLens](https://github.com/Bhavishaahuja/CartLens)
End-to-end customer analytics on the Olist e-commerce dataset (~100K orders across 9 tables): raw CSVs → cloud warehouse → Power BI and Tableau dashboards, written up as business findings. Its supplier-scoring ideas now power Cartkeeper.

- Built a Python ETL pipeline into BigQuery, with product images kept in Google Cloud Storage and linked by a features table
- Wrote 5 SQL views: RFM segmentation, cohort retention, delivery vs reviews, category affinity, and image quality vs sales
- Found that late deliveries drop average reviews from 4.29 to 2.27 stars, and that retention falls off a cliff after the first order
- Caught and fixed an average-of-ratios bias in cohort retention that overstated month-1 retention by ~10x
- Extracted computer-vision features (sharpness, brightness, dominant color) from product images to test whether image quality relates to sales

**Stack:** Python · SQL · BigQuery · Google Cloud Storage · Power BI · DAX · Tableau · Pillow · scikit-learn

---

## 🧪 ML & Data Science Projects

- **[Cell Type Classification (scRNA-seq)](https://github.com/Bhavishaahuja/cell-type-classification-scrnaseq):** Random Forest that identifies 8 cell types from 20,000 single-cell RNA-seq samples across ~3,000 genes. Handled heavy class imbalance and high dimensionality, raising accuracy from 98.5% to 99.1%. `Python` `scikit-learn`
- **[Urban Economic Opportunity Analysis](https://github.com/Bhavishaahuja/Urban-Economic-Opportunity-Analysis):** Pipeline analyzing socioeconomic gaps across 4,406 census tracts in Chicago, NYC, Dallas, and Oklahoma City, using the U.S. Census ACS API and comparing 4 ML models to forecast poverty rates. `Python` `U.S. Census API`
- **[Cereals Rating](https://github.com/Bhavishaahuja/Cereals-Rating):** Multiple linear regression on 76 cereals. Backward elimination identified sodium, fiber, and sugar as the key drivers, explaining 92%+ of the variance in ratings. `Python` `Regression` `Statistics`

---

## 🛠️ Tech I work with

**Languages:** Python · TypeScript · SQL · R
**AI/ML:** Claude API · LangGraph · agentic pipelines · forced tool use · RAG · pgvector · OpenAI Embeddings · prompt evals · scikit-learn
**Backend & Data:** FastAPI · Supabase / PostgreSQL · BigQuery · Google Cloud Storage · Stripe
**Frontend:** React · Next.js · Vite · Tailwind CSS
**Infra:** Docker · Kubernetes · Render · Vercel · AWS
**BI:** Power BI · Tableau

🏅 AWS Certified Cloud Practitioner

---

📫 Open to AI/ML Engineering and AI Product roles. The easiest way to reach me is [LinkedIn](https://www.linkedin.com/in/bhavisha-ahuja180503/) or [email](mailto:bhavishaahuja800@gmail.com).
