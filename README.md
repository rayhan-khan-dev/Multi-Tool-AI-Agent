# 🧠 Multi-Tool AI Agent for Bangladesh (Ostad - Module 23 Assignment)

This repository contains a robust, production-ready **Multi-Tool AI Agent** specifically designed to handle data-specific and general-knowledge queries about Bangladesh. Built using **LangChain**, **SQLite**, and **Google Gemini (gemini-2.5-flash)**, the agent intelligently decides whether to query local structural databases or route requests to a fallback web-search intelligence framework.

---

## 🎯 Project Objective

To build an advanced AI Agent capable of:
1. **Automated SQL Querying:** Parsing user questions into correct SQLite syntax and fetching statistics from three different Bangladeshi datasets.
2. **Intelligent Query Routing:** Dynamically deciding the best resource (Local DBs vs. Web Knowledge) to answer the user's prompt.
3. **Graceful Fallback:** Utilizing an advanced fallback mechanism to ensure 100% system uptime even during external live-search API/package failures.

---

## 📊 Core Architecture & Tools

The Main Agent utilizes Google Gemini with strict tool-binding configurations. Four main tools are integrated into the master routing pipeline:

| Query Type | Assigned Tool | Data Source / Action | Example Covered |
| :--- | :--- | :--- | :--- |
| **Education/Govt** | `InstitutionsDBTool` | `institutions.db` (SQLite) | Total colleges or board info in a region. |
| **Healthcare** | `HospitalsDBTool` | `hospitals.db` (SQLite) | Hospital bed counts and facility status. |
| **Food & Dining** | `RestaurantsDBTool` | `restaurants.db` (SQLite) | Checking ratings and reviews of local cafes. |
| **General Info** | `WebSearchTool` | DuckDuckGo API / Gemini Fallback | National healthcare policies, DGHS roles, etc. |

---

## 🛠️ Project Tasks Implemented

### 1. CSV to SQLite DB Conversion
Downloaded raw datasets from HuggingFace, sanitized column layouts, and parsed them into distinct relational tables:
* `institutions.db` (Table: `institutions`)
* `hospitals.db` (Table: `hospitals`)
* `restaurants.db` (Table: `restaurants`)

### 2. LangChain Custom Tool Binding
Created Python functions wrapped inside `@tool` decorators that parse natural language arguments, execute programmatic SQLite transactions safely, and return clean structural strings to the LLM.

### 3. Error-Proof Web Search (With Fallback Mechanism)
Integrated standard web crawling APIs. Implemented a robust `except` trap so that if live network components or local packages fail, the agent seamlessly pulls data from the LLM's comprehensive internal knowledge base.

---

## 🚀 Live Demo & Execution Trace

### Test Case 1: Database Query routing
* **User Input:** *"How many hospitals are in Dhaka?"*
* **Agent Thought:** `Routing to tool 'HospitalsDBTool' with arguments: {'sql_query': 'SELECT COUNT(*) FROM hospitals WHERE district = "Dhaka"'}`
* **Tool Output:** `[(2919,)]`
* **Final Answer:** *"There are 2919 hospitals in Dhaka."*

### Test Case 2: Web Search Fallback routing
* **User Input:** *"What is the role of DGHS in Bangladesh?"*
* **Agent Thought:** `Routing to tool 'WebSearchTool' with arguments: {'query': 'role of DGHS in Bangladesh'}`
* **Tool Output:** `⚠️ [WebSearchTool Notice]: Live web package failed, using fallback LLM knowledge base...`
* **Final Answer:** Summarizes the active role of the Directorate General of Health Services under the Ministry of Health and Family Welfare.

---

## 📁 Links & Submissions

* **Google Colab Notebook:** [https://colab.research.google.com/drive/1zc4ND7UcdU4VtG47Bu2JNcQuEmZMxOWT?usp=sharing]
* **GitHub Repository:** [rayhan-khan-dev/Multi-Tool-AI-Agent]

---
Developed by **Md Rayhan Khan
