# SG Transport Query Agent

An agentic workflow demo for answering natural-language queries about **Singapore public bus transport**.

---

## Overview

The system uses a **stateful agentic workflow** to:

1. Interpret a user query
2. Resolve entities such as bus stops and service numbers
3. Retrieve structured transport data from json datasets
4. Incorporate contextual constraints (time, weather, events)
5. Generate a grounded, natural‑language response using an LLM

The workflow is explicitly modeled using **LangGraph**.

---

## Architecture

At a high level, the agent follows this flow:

```
User Query
   ↓
Input Interpretation
   ↓
Context Enrichment
   ↓
Planning / Decision
   ↓
Tool Execution (Datasets)
   ↓
LLM-Based Response Synthesis
   ↓
Final Answer
```

Key design principles:

* Tools provide **deterministic, structured data**
* The LLM is used **only for response synthesis**
* Planning and execution are explicitly separated

---

## Data Sources

This prototype uses **static JSON datasets** derived from LTA DataMall to simulate real-time behavior:

```
data/
├── BusStops.json     # Global reference dataset
└── BusArrival.json   # Arrival snapshot for a specific bus stop
```

These datasets follow official LTA schemas and allow reproducible evaluation.

In production, dataset-backed tools can be replaced with authenticated LTA DataMall APIs **without changing the agent workflow**.

---

## LLM Usage

A Large Language Model (LLM) is used only in the **final response synthesis step**.

The LLM:

* Receives tool outputs and context as input
* Generates a concise explanation
* Is instructed to avoid hallucination and explicitly state uncertainty

This design minimizes hallucination risk and keeps system behavior transparent.

---

## Running the Notebook

### Requirements

* Python 3.10+
* Jupyter Notebook
* LangGraph
* A local or cloud LLM (example shown using Ollama)

### Steps

1. Clone the repository
2. Create and activate a virtual environment
3. Install dependencies
4. Open the notebook
5. **Restart kernel → Run All**

The notebook is designed to run top‑to‑bottom.

---

## Deployment Considerations

In a real-world deployment:

* The agent would run as a **stateless backend service**
* Dataset tools would be replaced with live, authenticated APIs
* LLM calls - rate-limited and monitored
---

## Notes

* Accuracy of arrival times is **not** the focus
* The emphasis is on **agentic design, reasoning, and clarity**
* The system is intentionally modular and extensible

