#  Multi-Agent A2A Project (Google ADK + MCP Server)

 
This project implements a multi-agent travel assistant system where each agent shares access to a centralized MCP server to perform web searches via the Tavily tool. Instead of giving each agent its own search engine, this design uses a single MCP server to handle search queries, making the system more efficient and scalable. It demonstrates how centralized infrastructure (MCP) can support decentralized agents in a LangChain-based environment.  


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
```plaintext
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
```

Each agent makes search requests via the shared MCP server, which handles communication with the Tavily API and returns results to the respective agent. 


#### 5. Documentation
All detailed theory, design principles, and presentation materials related to the Model Context Protocol (MCP) used in this project are compiled in the file:
 
Model_Context_Protocol.pdf 
 
Please refer to this document for an in-depth understanding of MCP architecture, agent coordination, and communication protocols.

### 6.Demo

1. Input data 

<img width="955" height="675" alt="image" src="https://github.com/user-attachments/assets/82372bb4-b7e3-463c-acd7-c5bad6f3b255" />

2. Output
<img width="897" height="651" alt="image" src="https://github.com/user-attachments/assets/0181975f-7808-403c-be22-05eb616beb3f" /> 
 
<img width="943" height="528" alt="image" src="https://github.com/user-attachments/assets/17164de8-d5a3-499d-82c4-1747d61d62d4" /> 
 
<img width="961" height="950" alt="image" src="https://github.com/user-attachments/assets/d6875294-324c-4338-a77a-13ea8f2be317" /> 

