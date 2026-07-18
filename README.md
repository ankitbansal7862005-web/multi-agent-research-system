# 🔬 ResearchMind — Multi-Agent AI Research System

ResearchMind is a multi-agent AI pipeline that automates the entire research workflow — from searching the web to writing and critiquing a polished report — powered by **LangChain**, **Groq (Llama 3.3)**, and **Tavily Search**, with an interactive **Streamlit** UI.

---

## ✨ Features

- 🔍 **Search Agent** — Gathers recent, reliable information from the web using Tavily
- 📄 **Reader Agent** — Scrapes and extracts deeper content from the most relevant source
- ✍️ **Writer Chain** — Synthesizes findings into a structured, professional research report
- 🧐 **Critic Chain** — Reviews the report and provides a scored, constructive critique
- ⚡ **Live pipeline UI** — Visual step-by-step progress tracker built with Streamlit
- 🔁 **Resilient tool-calling** — Automatic retry logic to handle occasional LLM tool-call failures
- 📥 **One-click download** — Export the final report as a Markdown file

---

## 🧠 How It Works

```
                     You give a Research Topic
                              │
                              ▼
                 ┌─────────────────────────┐
        Fetching │      Search Agent        │
   real-time data│  (AgentExecutor +         │◄────────────┐
        ┌────────┤   web_search_tool)        │              │
        │        └─────────────────────────┘        Tool 1: Tavily API
        │                    │                     (Live web results)
        └───────────────────►│                              │
                              ▼                              │
                state['search_results'] saved ◄──────────────┘
                              │
                              ▼
                 ┌─────────────────────────┐
      Fetching   │      Reader Agent         │
   more info     │  (AgentExecutor +         │◄────────────┐
        ┌────────┤   scrape_url_tool)        │              │
        │        └─────────────────────────┘         Tool 2: BeautifulSoup
        │                    │                        (scrapes pages)
        └───────────────────►│                              │
                              ▼                              │
               state['scraped_content'] saved ◄──────────────┘
                              │
                              ▼
                      ┌───────────────┐
                      │  Writer Chain  │
                      └───────────────┘
                              │
                              ▼
                      ┌───────────────┐
                      │  Critic Chain  │
                      └───────────────┘
                              │
                              ▼
                        Final Output
                (Research Report + Critic Feedback)
```

Each agent is powered by **Groq's `llama-3.3-70b-versatile`** model via `langchain-groq`, orchestrated using LangChain's `create_agent` (an `AgentExecutor` built on LangGraph under the hood). Both agents dynamically call their respective tools whenever they need fresh data — the Search Agent calls Tavily for live web results, and the Reader Agent calls BeautifulSoup-based scraping for deeper page content — before saving results into pipeline state and passing them downstream to the Writer and Critic chains.

---

## 🛠️ Tech Stack

| Layer         | Technology                          |
|---------------|--------------------------------------|
| LLM           | Groq — Llama 3.3 70B Versatile       |
| Orchestration | LangChain / LangGraph                |
| Web Search    | Tavily Search API                    |
| Scraping      | BeautifulSoup + Requests             |
| Frontend      | Streamlit                            |
| Reliability   | Tenacity (retry logic)               |

---

## 🚀 Getting Started

### 1. Clone the repository
```bash
git clone https://github.com/ankitbansal7862005-web/multi-agent-research-system.git
cd multi-agent-research-system
```

### 2. Install dependencies
```bash
pip install -r requirements.txt
```

### 3. Set up environment variables
Create a `.env` file in the root directory:
```
GROQ_API_KEY=your_groq_api_key_here
TAVILY_API_KEY=your_tavily_api_key_here
```

### 4. Run the app
```bash
streamlit run app.py
```

The app will open in your browser at `http://localhost:8501`.

### (Optional) Run via CLI
For quick terminal-based testing without the UI:
```bash
python pipeline.py
```

---

## 📁 Project Structure

```
├── agents.py          # Agent definitions, LLM setup, writer & critic chains
├── app.py             # Streamlit UI and pipeline orchestration
├── pipeline.py         # CLI version of the research pipeline
├── tools.py           # Web search & URL scraping tools
├── requirements.txt    # Python dependencies
└── .devcontainer/      # Dev container config
```

---

## 🌐 Live Demo

🔗 **https://multi-agent-research-system-ankit.streamlit.app/**

> Note: The app may take a few seconds to wake up if it's been idle.

---

## 🔮 Future Improvements

- [ ] Support multiple source scraping (not just one URL)
- [ ] Add citation tracking with inline source links
- [ ] Support PDF export of the final report
- [ ] Add configurable model selection (switch between Groq models)
- [ ] Add caching to avoid redundant API calls for repeated topics

---

---

## 🙋‍♂️ Author

Built by **Ankit Bansal**
- GitHub: [@ankitbansal7862005-web](https://github.com/ankitbansal7862005-web)
