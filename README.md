#  Multi-Agent A2A Project (Google ADK + MCP Server)
     
This project implements a multi-agent travel assistant system where each agent shares access to a centralized MCP server to perform web searches via the Tavily tool. Instead of giving each agent its own search engine, this design uses a single MCP server to handle search queries, making the system more efficient and scalable. It demonstrates how centralized infrastructure (MCP) can support decentralized agents in a LangChain-based environment. 
---

##  Getting Started 

### 1. Clone the Repository
```bash
git clone https://github.com/Vinh-Sta/Multi_agent_with_MCP_Sever.git
cd Multi_agent_with_MCP_Sever
```
### 2. Set Up the Environment 
```bash
python3 -m venv adk_demo  
source adk_demo/bin/activate  
pip install -r requirements.txt  
```
### 3. Configure API Keys 
```bash
GOOGLE_API_KEY="your-key"  
AGENT_MODEL="your-model"  
TAVILY_API_KEY="YOUR_API_KEY"
```
### 4. Run the Agent and UI 
Start each agent and the UI: 
```bash
uvicorn agents.host_agent.__main__:app --port 8080 &  
uvicorn agents.flight_agent.__main__:app --port 8081 &  
uvicorn agents.stay_agent.__main__:app --port 8082 &  
uvicorn agents.activities_agent.__main__:app --port 8083 &  


streamlit run travel_ui.py  
```

#### 4. System Architecture Diagram
┌─────────────────────┐
│    Travel UI (user) │
└────────┬────────────┘
         │
         ▼
┌─────────────────────┐
│    Host Agent       │◄────────────────────────────────┐
└────────┬────────────┘                                 │
         ▼                                              │
┌────────────┐   ┌────────────┐   ┌────────────┐   ┌────▼─────┐
│Flight Agent│   │ Stay Agent│   │Activity Agent│  │ MCP Server│
└────┬───────┘   └────┬──────┘   └────┬────────┘   └────┬─────┘
     │               │               │                 │
     └───────────────┴───────────────┴─────────────────┘
                      ▼
              🌐 Tavily Web Search
  
Each agent makes search requests via the shared MCP server, which handles communication with the Tavily API and returns results to the respective agent. 
