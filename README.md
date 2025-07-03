### Building Chatbot with Multiple Tools, ReAct Agent and Streaming using LangGraph
# LangGraph Advanced Agent Notebooks

This repository contains a collection of Jupyter notebooks demonstrating advanced concepts in building AI agents and chatbots using **LangGraph**, focusing on tool integration, agentic reasoning, and real-time streaming.

## Table of Contents

* [chatbot\_with\_multiple\_tools.ipynb: Building a Chatbot with Multiple Tools](#chatbot_with_multiple_toolsipynb-building-a-chatbot-with-multiple-tools)
* [ReAct\_Agent.ipynb: Implementing a ReAct Agent](#react_agentipynb-implementing-a-react-agent)
* [streaming.ipynb: Chatbot with Streaming Capabilities](#streamingipynb-chatbot-with-streaming-capabilities)
* [Setup and Prerequisites](#setup-and-prerequisites)
* [Usage](#usage)

---

## chatbot\_with\_multiple\_tools.ipynb: Building a Chatbot with Multiple Tools

This notebook illustrates how to create a sophisticated chatbot that can leverage multiple external tools to answer user queries.

### Key Concepts Demonstrated:

* **Tool Integration:** Binding various tools (e.g., `ArxivQueryRun`, `WikipediaQueryRun`, `TavilySearchResults`, and custom arithmetic functions like `add`, `multiply`, `divide`) to an LLM.
* **LLM with Tools:** Configuring a `ChatGroq` model to intelligently decide when and how to use the available tools based on the user's input.
* **Conversation History:** Maintaining and managing the conversation context using LangChain's message history and LangGraph's state management (`Annotated` with `add_messages`).
* **Dynamic Tool Calling:** Observing how the LLM generates `tool_calls` in its response, which are then executed to retrieve information or perform actions.

### Workflow Flow:

The chatbot receives a user query, passes it to the LLM configured with tools. The LLM might decide to call one or more tools based on the query. The results from the tools are then fed back to the LLM to formulate a final, informed response.

---

## ReAct\_Agent.ipynb: Implementing a ReAct Agent

This notebook delves into the **ReAct (Reasoning and Acting)** agent architecture, a powerful pattern for building LLM agents that can reason about a task, plan actions, execute them, and observe the results.

### Key Concepts Demonstrated:

* **ReAct Architecture:** Understanding the core loop of "Act, Observe, Reason" that enables agents to perform multi-step tasks.
* **Custom Tools:** Defining custom Python functions (`add`, `multiply`, `divide`) and exposing them as tools for the LLM.
* **External Knowledge Tools:** Integrating tools like Arxiv and Wikipedia for information retrieval, allowing the agent to answer questions beyond its training data.
* **Agentic Reasoning:** Observing the LLM's internal "thought" process as it decides which tool to use, what arguments to provide, and how to synthesize information.
* **Langsmith Tracking:** Configuration for tracing and debugging agent execution flows using Langsmith.

### Workflow Flow:

The ReAct agent processes a query by first reasoning about it (Thought). This leads to an action (Act), which involves calling a tool. The result of the tool call is observed (Observe), and the agent then reasons again (Thought) based on the observation, repeating the cycle until a final answer can be provided.

---

## streaming.ipynb: Chatbot with Streaming Capabilities

This notebook focuses on enhancing the user experience of a chatbot by implementing real-time streaming of responses.

### Key Concepts Demonstrated:

* **Streaming Responses:** Receiving LLM output incrementally as it's generated, rather than waiting for the complete response.
* **LangGraph Streaming Modes:** Utilizing `graph_builder.stream()` with different `stream_mode` options (e.g., "updates", "values") to observe how state changes and messages are streamed.
* **Conversation Memory:** Reinforcing the concept of persistent conversation history using `MemorySaver` for checkpoints across turns.
* **LLM Invocation:** Demonstrating direct invocation of `ChatOpenAI` and `ChatGroq` models within a LangGraph node to generate conversational output.

### Workflow Flow:

Similar to a basic chatbot, this workflow processes user messages and invokes an LLM. The key difference lies in how the LLM's response is delivered: it streams back word-by-word or token-by-token, providing a more dynamic and responsive user experience.

---

## Setup and Prerequisites

To run these notebooks, you will need:

* Python 3.9+
* Jupyter Notebook or JupyterLab
* API keys for **Groq**, **OpenAI**, and **Tavily** (for search).
* Optionally, a **Langsmith** API key for tracing.

1.  **Clone the repository:**
    ```bash
    git clone [https://github.com/Abubakar0011/LangGraph_Practice.git](https://github.com/Abubakar0011/LangGraph_Practice.git) 
    cd LangGraph_Practice
    ```

2.  **Set up Virtual Environment & Install Dependencies:**
    It's highly recommended to use a Python virtual environment. You can use `uv` for faster installation:

    ```bash
    # Install uv if you don't have it
    # pip install uv

    python -m venv .venv
    source .venv/bin/activate # On macOS/Linux
    # .\.venv\Scripts\activate # On Windows

    # Install all required libraries
    uv pip install -r requirements.txt
    ```
    The `requirements.txt` file content is provided in the repository.

3.  **Configure Environment Variables:**
    Create a `.env` file in the root directory of your project and add your API keys:

    ```dotenv
    OPENAI_API_KEY="your_openai_api_key_here"
    GROQ_API_KEY="your_groq_api_key_here"
    TAVILY_API_KEY="your_tavily_api_key_here"
    LANGCHAIN_API_KEY="your_langchain_api_key_here" # Optional, for Langsmith tracing
    LANGCHAIN_TRACING_V2="true" # Enable Langsmith tracing
    LANGCHAIN_PROJECT="ReAct-agent" # Your Langsmith project name
    ```
    **Important:** Add `.env` to your `.gitignore` file to prevent accidentally committing your secrets.

## Usage

1.  **Start Jupyter:**
    ```bash
    jupyter notebook
    # or
    jupyter lab
    ```
2.  **Open and Run:** Navigate to the desired notebook (`chatbot_with_multiple_tools.ipynb`, `ReAct_Agent.ipynb`, or `streaming.ipynb`) in the Jupyter interface and run the cells sequentially to explore the functionalities.

---