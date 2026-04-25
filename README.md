# Demo 01: Building a CrewAI-Powered Agent With Dynamic Web Search Using Hugging Face / Groq

## Objective

Demonstrate how to build a multi-agent system using CrewAI that intelligently identifies queries requiring real-time information and retrieves the most up-to-date data using a Hugging Face or Groq-hosted LLM and the Tavily web search API.

## Scenario

A product manager at a digital knowledge platform needs to manage an increasing volume of user queries, many of which require real-time updates and dynamic information. The goal is to automate query handling using a multi-agent system that can identify when real-time data retrieval is needed and provide fast, accurate, and context-aware responses.

## Architecture

The system uses two CrewAI agents working sequentially:

| Agent | Role | Responsibility |
|-------|------|----------------|
| **AI Researcher** | Research | Searches the web to identify the top 3 recent AI advancements in FMCG |
| **Technical Writer** | Summarization | Produces a concise executive summary (≤200 words) from the research notes |

### Tools & Services

- **LLM (Hugging Face)**: `Qwen/Qwen2.5-7B-Instruct` via Hugging Face Inference API (OpenAI-compatible endpoint)
- **LLM (Groq)**: `llama-3.3-70b-versatile` via Groq API (OpenAI-compatible endpoint)
- **Web Search**: Custom `TavilySearchTool` built on the Tavily Search API
- **Orchestration**: CrewAI framework

> Switch between providers by setting `LLM_PROVIDER` to `"huggingface"` or `"groq"` in the notebook.

## Prerequisites

- Python 3.10+
- A **Hugging Face API key** (set as `HF_API_KEY`) **or** a **Groq API key** (set as `GROQ_API_KEY`)
- A **Tavily API key**

## Setup

1. **Set environment variables:**

   ```bash
   # Linux / macOS
   export HF_API_KEY="your-huggingface-api-key"
   export GROQ_API_KEY="your-groq-api-key"

   # Windows PowerShell
   $env:HF_API_KEY = "your-huggingface-api-key"
   $env:GROQ_API_KEY = "your-groq-api-key"
   ```

2. **Install dependencies** (handled in the notebook):

   ```bash
   pip install --upgrade crewai langchain langchain-openai langchain-community langchain-tavily tavily-python pydantic litellm
   pip install "crewai[azure-ai-inference]"
   ```

3. **Open and run the notebook:**

   ```
   CrewAI-Powered_Agent_With_Dynamic_Web_Search Using HuggingFace.ipynb
   ```

## Notebook Walkthrough

| Step | Description |
|------|-------------|
| 1 | Install required libraries (`crewai`, `langchain`, `tavily-python`, `litellm`, etc.) |
| 2 | Import dependencies (`os`, `requests`, `crewai.LLM`, `Agent`, `Task`, `Crew`, `BaseTool`) |
| 3 | Configure the Tavily search tool and select the LLM provider (Hugging Face or Groq) |
| 4 | Define two agents — Researcher (with web search tool) and Writer |
| 5 | Create tasks with dependencies (Writer uses Researcher's output as context) |
| 6 | Assemble the Crew and kick off sequential execution |

## Expected Output

An executive summary of the top 3 recent AI advancements in the FMCG sector, formatted with bullet points and limited to 200 words.
