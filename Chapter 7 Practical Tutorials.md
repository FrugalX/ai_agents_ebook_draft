# Chapter 7: Practical Tutorials

## 7.1 Getting Started with Generative AI Agents

This chapter provides hands-on tutorials for building AI agents using various APIs, ensuring a balanced representation of OpenAI, Google Gemini, Anthropic Claude, and open-source models like Mistral. We will cover step-by-step implementations for building single-agent and multi-agent systems.

## 7.2 Setting Up Your Environment

Before we dive into the tutorials, install the necessary dependencies:

```bash
pip install openai anthropic google-generativeai langchain mistralai
```

### API Keys
Obtain API keys from OpenAI (for the Agents SDK & Responses API), Anthropic (Claude API), Google (Gemini API), and Mistral for open-source LLMs.

## 7.3  Building An AI Chatbot for Customer Support

### **Learning Outcome**
By the end of this tutorial, you will have a fully functional AI chatbot capable of handling customer queries efficiently. The chatbot will be implemented using **OpenAI’s Agents SDK**, **Gemini API**, and **Claude API**, with both **Python and JavaScript examples**.

```mermaid
sequenceDiagram
    participant User
    participant Chatbot
    participant API

    User->>Chatbot: Sends a query
    Chatbot->>Chatbot: Process query & retrieve context
    Chatbot->>API: Call external knowledge base
    API-->>Chatbot: Return relevant data
    Chatbot-->>User: Generate response
```

### **Step 1: Setting Up the AI Chatbot**
- Choose your AI provider (OpenAI, Gemini, or Claude).
- Define chatbot instructions and expected behavior.

### **Python: AI Chatbot with OpenAI Agents SDK**
```python
from openai import OpenAI

client = OpenAI(api_key="YOUR_API_KEY")

def chat_with_ai(message):
    response = client.beta.threads.create_and_run(
        assistant_id="your_assistant_id",
        thread={"messages": [{"role": "user", "content": message}]}
    )
    return response

print(chat_with_ai("What are your store hours?"))
```

### **JavaScript: AI Chatbot with OpenAI Agents SDK**
```javascript
import { OpenAI } from "openai";

const openai = new OpenAI({ apiKey: "YOUR_API_KEY" });

async function chatWithAI(message) {
    const response = await openai.beta.threads.createAndRun({
        assistant_id: "your_assistant_id",
        thread: { messages: [{ role: "user", content: message }] },
    });
    console.log(response);
}

chatWithAI("What are your store hours?");
```

### **Alternative: Using Google Gemini API for the Chatbot**
- Gemini API can be used for a more **multi-modal approach**, integrating text, images, and videos.

### **Alternative: Using Claude API for the Chatbot**
- Claude specializes in **structured conversations with high reliability**.

This chatbot can be integrated into web apps, mobile apps, or backend systems for automated customer support.

## 7.4 Developing a Creative Content Assistant ##

### **Learning Outcome**
By the end of this tutorial, you will develop an AI-powered content assistant capable of generating creative writing pieces like stories, blog posts, and social media captions.

```mermaid
sequenceDiagram
    participant User
    participant AI_Assistant
    participant Research_API

    User->>AI_Assistant: Provide topic request
    AI_Assistant->>AI_Assistant: Retrieve writing style/memory
    AI_Assistant->>Research_API: Fetch related info (optional)
    Research_API-->>AI_Assistant: Return research data
    AI_Assistant-->>User: Generate creative content
```

### **Step 1: Setting Up the Content Assistant**
- Choose your AI provider (OpenAI, Gemini, or Claude).
- Define creative writing instructions and expected outputs.

### **Python: AI-Powered Creative Writer (OpenAI’s GPT-4 Turbo)**
```python
import openai

def generate_content(prompt):
    response = openai.ChatCompletion.create(
        model="gpt-4-turbo",
        messages=[{"role": "user", "content": prompt}]
    )
    return response["choices"][0]["message"]["content"]

print(generate_content("Write a short story about an astronaut on Mars."))
```

### **JavaScript: AI-Powered Creative Writer (OpenAI’s GPT-4 Turbo)**
```javascript
import { OpenAI } from "openai";

const openai = new OpenAI({ apiKey: "YOUR_API_KEY" });

async function generateContent(prompt) {
    const response = await openai.chat.completions.create({
        model: "gpt-4-turbo",
        messages: [{ role: "user", content: prompt }]
    });
    console.log(response.choices[0].message.content);
}

generateContent("Write a short story about an astronaut on Mars.");
```

### **Alternative: Using Google Gemini API for Content Generation**
- Gemini API provides multi-modal creativity by integrating text, images, and video generation into content workflows.

### **Alternative: Using Claude API for Structured Content Writing**
- Claude excels in creating **coherent, structured, and well-formed content** across different domains.

This content assistant can be integrated into **blog platforms, social media management tools, or creative writing applications** to automate content production.

## 7.5 Creating a Multi-Agent News Aggregator

### **Learning Outcome**
By the end of this tutorial, you will build a **multi-agent system** that gathers, summarizes, and organizes news articles from different sources.

```mermaid
graph TD
    User -->|Request News| NewsAggregator
    NewsAggregator -->|Fetch| NewsScraper
    NewsScraper -->|Retrieve Data| NewsAPIs
    NewsAggregator -->|Summarize| Summarizer
    Summarizer -->|Categorize| Categorizer
    Categorizer -->|Deliver| User
```

### **Step 1: Understanding Multi-Agent Collaboration**
- **Fetching Agent**: Retrieves news articles from APIs like NewsAPI.
- **Summarization Agent**: Condenses information for easier consumption.
- **Categorization Agent**: Sorts articles into relevant topics.

### **Python: Multi-Agent News Aggregator Using AutoGen**
```python
from autogen import UserProxyAgent, AssistantAgent

def news_aggregator():
    fetch_agent = AssistantAgent(name="NewsFetcher")
    summary_agent = AssistantAgent(name="Summarizer")
    user = UserProxyAgent(name="User", human_input_mode="NEVER")

    user.initiate_chat(
        fetch_agent, message="Retrieve top tech news articles."
    )
    user.initiate_chat(
        summary_agent, message="Summarize the retrieved articles."
    )

news_aggregator()
```

### **JavaScript: Multi-Agent News Aggregator Using LangChain**
```javascript
import { ChatOpenAI } from "langchain/chat_models";

const model = new ChatOpenAI({ modelName: "gpt-4", temperature: 0.7 });

async function fetchNews() {
    const response = await model.call("Retrieve top tech news articles.");
    console.log(response);
}
fetchNews();
```

### **Alternative Approaches**
- **Google Gemini API**: For **multi-modal news aggregation**, incorporating **text and images**.
- **Claude API**: Ideal for structured content summarization.

This news aggregator can be integrated into **news websites, RSS readers, or AI-driven research tools** for automated news curation.

## 7.6 Designing a Self-Orchestrated Research Tool

### **Learning Outcome**
By the end of this tutorial, you will have built a **self-orchestrating research agent** capable of fetching, analyzing, and summarizing research papers using AI.

```mermaid
sequenceDiagram
    participant User
    participant Research_Agent
    participant PaperDB
    participant Summarizer

    User->>Research_Agent: Submit research query
    Research_Agent->>PaperDB: Retrieve academic papers
    PaperDB-->>Research_Agent: Send paper data
    Research_Agent->>Summarizer: Summarize findings
    Summarizer-->>User: Provide structured research report
```

### **Step 1: Understanding Multi-Agent Research Workflows**
A self-orchestrated research tool automates literature review, data analysis, and summarization.

- **Research Fetching Agent**: Retrieves relevant academic papers.
- **Summarization Agent**: Extracts key insights from long papers.
- **Trend Analysis Agent**: Identifies recurring themes and trends.

### **Python: Self-Orchestrating Research Assistant with AutoGen**
```python
from autogen import UserProxyAgent, AssistantAgent

def research_assistant():
    fetch_agent = AssistantAgent(name="PaperFetcher")
    summary_agent = AssistantAgent(name="Summarizer")
    analysis_agent = AssistantAgent(name="TrendAnalyzer")
    user = UserProxyAgent(name="User", human_input_mode="NEVER")

    user.initiate_chat(
        fetch_agent, message="Find recent research papers on deep learning."
    )
    user.initiate_chat(
        summary_agent, message="Summarize the main findings from the papers."
    )
    user.initiate_chat(
        analysis_agent, message="Analyze trends from the summarized research."
    )

research_assistant()
```

### **JavaScript: Research Assistant with LangChain**
```javascript
import { ChatOpenAI } from "langchain/chat_models";

const model = new ChatOpenAI({ modelName: "gpt-4", temperature: 0.7 });

async function researchAssistant() {
    const response = await model.call("Find recent research papers on deep learning.");
    console.log(response);
}
researchAssistant();
```

### **Alternative Approaches**
- **Google Gemini API**: Enables multi-modal research by incorporating **text, charts, and graphs**.
- **Claude API**: Best for **structured document summarization** and in-depth analysis.

This research tool can be integrated into **academic search engines, AI-driven research assistants, or corporate knowledge bases**.

## 7.7 Building a Game with Multi-Agent Characters

### **Learning Outcome**
By the end of this tutorial, you will create a game where AI-powered agents dynamically interact based on predefined rules.

- Use **OpenAI’s Agents SDK** for in-game AI.
- Use **Reinforcement Learning** concepts for adaptive behavior.

### **Understanding AI Agents in Gaming**
- **NPC Behavior Agent**: Controls non-playable characters.
- **Combat Strategy Agent**: Determines attack/defense strategies.
- **Environment Interaction Agent**: Adapts the game world based on AI decisions.

```mermaid
graph TD
    Player -->|Interacts with| GameEngine
    GameEngine -->|Manages| NPC_Agent1
    GameEngine -->|Manages| NPC_Agent2
    NPC_Agent1 -->|Communicates with| NPC_Agent2
    NPC_Agent2 -->|Responds based on| Player_actions
```

### **Python: AI-Powered NPCs Using OpenAI Agents SDK**
```python
from openai import OpenAI

client = OpenAI(api_key="YOUR_API_KEY")

def npc_behavior(npc_role):
    response = client.beta.threads.create_and_run(
        assistant_id="your_npc_id",
        thread={"messages": [{"role": "user", "content": f"What should {npc_role} do in battle?"}]}
    )
    return response

print(npc_behavior("Warrior"))
```

### **JavaScript: AI-Powered NPCs Using OpenAI Agents SDK**
```javascript
import { OpenAI } from "openai";

const openai = new OpenAI({ apiKey: "YOUR_API_KEY" });

async function npcBehavior(npcRole) {
    const response = await openai.beta.threads.createAndRun({
        assistant_id: "your_npc_id",
        thread: { messages: [{ role: "user", content: `What should ${npcRole} do in battle?` }] },
    });
    console.log(response);
}

npcBehavior("Warrior");
```

### **Enhancing AI Characters with Reinforcement Learning**
- Introduce **policy-based and reward-driven learning**.
- Implement **Unity ML-Agents** or **OpenAI Gym** for in-game intelligence.

### **Alternative Approaches**
- **Google Gemini API**: For dynamic character dialogues and real-time adaptations.
- **Claude API**: Best suited for **scripted AI interactions** and procedural storytelling.

This AI-driven gaming system can be integrated into **RPGs, strategy games, and dynamic simulations**.

---

This chapter introduced practical tutorials for building AI agents using multiple APIs, covering OpenAI’s Agents SDK, LangChain, and AutoGen for real-world applications. The next chapter will explore ethical considerations, privacy, and limitations in deploying AI agents.


---

[Previous: Chapter 6](https://github.com/FrugalX/ai_agents_ebook_draft/blob/main/Chapter%206%20Key%20Concepts%20in%20Generat.md) | [Next: Chapter 8](https://github.com/FrugalX/ai_agents_ebook_draft/blob/main/Chapter%208%20Ethics%2C%20Privacy%2C%20and%20Li.md)
