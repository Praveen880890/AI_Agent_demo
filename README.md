*Note : Strictly for education purpose

# AI_Agent_demo: From Zero to Agent Building

This project is a demonstration of how to build a functional AI agent, or "Company Brain," using the `strands-agents` SDK.

The goal is to create an AI agent that can reason, plan, and act on private company data—overcoming the limitations of traditional Large Language Models (LLMs).

## 🧠 The Problem: LLMs as a "Brain in a Jar"

Traditional LLMs are powerful, but they have key limitations in an enterprise context:
* **Passive Nature:** They are passive systems that can't take actions or interact with external environments.
* **No Real-Time Data:** They cannot access real-time information or proprietary company data.

## 🤖 The Solution: AI Agents

AI Agents solve this by enhancing LLMs with capabilities for **reasoning, planning, and action**. This demo uses the **ReAct loop** (Reason, Act, Observe), allowing the agent to use a set of tools to solve complex problems.

We use the **strands SDK** to build this agent because it simplifies development:
* **Model-Agnostic:** It provides a unified interface for models like Gemini, OpenAI, and Anthropic.
* **Simple Tool Creation:** You can turn any Python function into a tool using the simple `@tool` decorator.
* **Orchestration:** The `strands.Agent` class automatically manages the ReAct loop and tool invocation.

---

## 🚀 Project Overview

This repository demonstrates a multi-tool "Company Brain" agent configured in the `demo.py` script.

The agent is given a system prompt and access to three distinct tools:
1.  **`search_knowledge_base` (Custom Tool):** A custom Python function that searches a local `knowledge_base.txt` file to retrieve specific internal company information.
2.  **`calculator` (Built-in Tool):** A pre-built tool from `strands-tools` for performing mathematical calculations.
3.  **`current_time` (Built-in Tool):** A pre-built tool from `strands-tools` for fetching the current date and time.

The agent demonstrates **intelligent tool selection** by analyzing the user's prompt and deciding whether to use its own general knowledge or to invoke one or more of the provided tools.

---

## 🛠️ Requirements

To run this project, you will need the following Python modules.

```bash
# Install the main agent framework and the pre-built tools
pip install strands-agents strands-tools
```
You will also need a Google Gemini API Key, as the agent is configured to use the gemini-2.5-pro model.

⚙️ How to Run
Install Dependencies:

```bash
pip install strands-agents strands-tools
```
Set Your API Key: You must set your Gemini API key. You can either:

(Recommended) Set it as an environment variable:

```bash

export GOOGLE_API_KEY="your-api-key-here" 
```
Or replace the placeholder in the demo.py script directly:

```Python

model = GeminiModel(
    client_args={
        "api_key": "YOUR_API_KEY_HERE", # <-- Replace this
    },
    ...
)
```
Create the Knowledge Base: Create a file named knowledge_base.txt in the same directory. Add your internal data to it. Based on the demo, its content should look something like this:

The internal codename for the GAIA platform is Griffin.
The support email for the GAIA platform is support@gaia-internal.com.
Project Atlas is scheduled for Q1 release.
Run the Agent: Execute the Python script:

```bash

python demo.py
```
💬 Example Prompts & Output
The script will run several prompts to test the agent's abilities:

1. General Knowledge (No Tool Used)

User: What is the capital of France?

Agent: The capital of France is Paris.

2. Internal Knowledge (Uses search_knowledge_base)

User: What is the internal codename for the GAIA platform?

Agent: The internal codename for the GAIA platform is Griffin.

3. Real-time Data (Uses current_time)

User: What is the current time and date for india?

Agent: The current time and date in India is November 4, 2025, 4:20 PM.

4. Math Problem (Uses calculator)

User: What is 123 * 45 + 67?

Agent: 123 * 45 + 67 = 5602.

5. Complex Multi-Tool Query (Uses Own Knowledge, search_knowledge_base, and calculator)

User: Please tell me three things: 1. What is the capital of Spain? 2. What is the support email for GAIA? 3. What is 500 divided by 25?

Agent:

Here are the answers to your questions:

1.  The capital of Spain is Madrid.
2.  The support email for the GAIA platform is support@gaia-internal.com.
3.  500 divided by 25 is 20.
