# 🤖 LangChain ReAct Agent — Google Gemini + DuckDuckGo

A ReAct (Reasoning + Acting) agent built with LangChain, powered by **Google Gemini** and **DuckDuckGo search** — tested entirely in Google Colab. No local setup needed!

---

## 🚀 Quick Start

1. Go to [colab.research.google.com](https://colab.research.google.com)
2. **File → Upload notebook** → select `langchain_react_agent_gemini_colab.ipynb`
3. Run all cells top to bottom
4. Paste your Google API key when prompted — that's it!

---

##  API Keys

| Service | Where to get it | Cost |
|---------|----------------|------|
| Google Gemini | [aistudio.google.com/app/apikey](https://aistudio.google.com/app/apikey) | Free |
| DuckDuckGo Search | Not needed  | Free |

---

##  Dependencies

All installed automatically in the notebook via:
```bash
pip install langchain langchain-google-genai langchain-community \
            google-generativeai duckduckgo-search langgraph
```

---

## 🔧 Tools

| Tool | What it does |
|------|-------------|
|  `calculator` | Evaluates Python math expressions. Supports `math` module. |
|  `get_current_datetime` | Returns current UTC date, time, day, and week number. |
|  `web_search` | Real web search via DuckDuckGo. No API key required. |
|  `text_analyzer` | Returns word count, character count, sentence count, unique words. |

---

##  How to Ask Questions

Use the `ask()` helper function from the notebook:

```python
ask("What are the latest AI news today?")
ask("What is 1337 * 42? Then find the square root.")
ask("What day of the week is it today?")
ask("Search for Bitcoin price and calculate what 0.5 BTC is worth.")
```

Each call prints the full **Thought → Action → Observation** reasoning chain plus which tools were used.

---

##  Sample Output

```
════════════════════════════════════════════════════════════
 Question: What is 25% of 2400?
════════════════════════════════════════════════════════════

> Entering new AgentExecutor chain...
Thought: I need to calculate 25% of 2400.
Action: calculator
Action Input: 2400 * 0.25
Observation: Result: 600.0
Final Answer: 25% of 2400 is 600.

 Tools Used:
   • calculator  →  input: {'expression': '2400 * 0.25'}

──────────────────────────────────────────────────────────
 Final Answer: 25% of 2400 is 600.
──────────────────────────────────────────────────────────
```

---

##  Switching Gemini Models

Change the model in the agent setup cell:

```python
model="gemini-1.5-flash"   # Fast, free-tier friendly (default)
model="gemini-1.5-pro"     # More powerful reasoning
model="gemini-2.0-flash"   # Latest and fastest
```

---

##  Adding Your Own Tool

```python
@tool
def my_tool(input: str) -> str:
    """
    Describe what this tool does here.
    The agent reads this docstring to decide when to call it.
    Be specific about what the input should look like.
    """
    # your logic here
    return f"Result: {input}"

# Add to tools list and re-run the agent setup cell
tools = [calculator, get_current_datetime, web_search, text_analyzer, my_tool]
```

---

##  Configuration Options

```python
# Show / hide the agent's thinking steps
AgentExecutor(..., verbose=True)   # show  (default)
AgentExecutor(..., verbose=False)  # hide — only shows final answer

# Limit reasoning steps (prevent infinite loops)
AgentExecutor(..., max_iterations=10)
```

---

##  Tech Stack

| Component | Technology |
|-----------|-----------|
| LLM | Google Gemini via `langchain-google-genai` |
| Agent framework | LangChain + LangGraph |
| Web search | DuckDuckGo (`langchain-community`) |
| Notebook environment | Google Colab |
