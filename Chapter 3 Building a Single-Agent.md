# Chapter 3: Building a Single-Agent System

## 3.1 What is a Single-Agent System?
A single-agent system is an AI-powered entity designed to operate independently, making decisions based on input data, context, and learned experiences. Unlike multi-agent systems, a single-agent system works autonomously without coordinating with other agents.

### Applications
Single-agent systems are widely used in various domains:
- **AI Chatbots**: Virtual assistants automate customer interactions, providing instant responses to queries, improving customer satisfaction, and reducing human workload.
- **Recommendation Systems**: Personalized recommendations enhance user experience on streaming platforms and e-commerce by suggesting relevant content or products.
- **Autonomous Task Execution**: Virtual assistants automate repetitive tasks like scheduling meetings, managing calendars, and summarizing documents.

## 3.2 Anatomy of an AI Agent
A single-agent AI system typically consists of the following components:
- **Input Handling**: Accepts user queries, sensor data, or API calls.
- **Processing Unit**: Uses models like GPT-4, Claude, or Gemini to process input and generate responses.
- **Memory & Context Awareness**: Maintains conversation history and contextual understanding.
- **Output Handling**: Returns responses through text, voice, or structured data formats.

## 3.3 Implementing a Basic Single-Agent System
Let’s first build basic AI agents using OpenAI’s Agents SDK, Gemini API, and Claude’s system message approach.

### Example 1: Basic AI Chatbot using OpenAI Agents SDK

#### Python
```python
from openai import OpenAI

oai = OpenAI(api_key="YOUR_API_KEY")

def ai_chatbot(prompt):
    response = oai.chat.completions.create(
        model="gpt-4-turbo",
        messages=[{"role": "system", "content": "You are an AI assistant."}, {"role": "user", "content": prompt}]
    )
    return response.choices[0].message.content

print(ai_chatbot("Tell me about AI agents."))
```

#### JavaScript
```javascript
import { OpenAI } from "openai";
const openai = new OpenAI({ apiKey: "YOUR_API_KEY" });

async function aiChatbot(prompt) {
    const response = await openai.chat.completions.create({
        model: "gpt-4-turbo",
        messages: [
            { role: "system", content: "You are an AI assistant." },
            { role: "user", content: prompt }
        ]
    });
    console.log(response.choices[0].message.content);
}

aichatbot("Tell me about AI agents.");
```

### Example 2: Using Claude’s System Messages for Contextual Responses

#### Python
```python
import anthropic

client = anthropic.Anthropic(api_key="YOUR_CLAUDE_API_KEY")

def claude_chatbot(prompt):
    response = client.messages.create(
        model="claude-3-haiku-2024-02-25",
        system="You are an expert AI agent providing clear explanations.",
        messages=[{"role": "user", "content": prompt}]
    )
    return response.content

print(claude_chatbot("Explain reinforcement learning."))
```

#### JavaScript
```javascript
import { Anthropic } from "anthropic";
const anthropic = new Anthropic({ apiKey: "YOUR_CLAUDE_API_KEY" });

async function claudeChatbot(prompt) {
    const response = await anthropic.messages.create({
        model: "claude-3-haiku-2024-02-25",
        system: "You are an expert AI agent providing clear explanations.",
        messages: [{ role: "user", content: prompt }]
    });
    console.log(response.content);
}

claudeChatbot("Explain reinforcement learning.");
```

### Example 3: Basic AI Agent using Gemini API

#### Python
```python
import google.generativeai as genai

genai.configure(api_key="YOUR_GEMINI_API_KEY")

def gemini_chatbot(prompt):
    model = genai.GenerativeModel("gemini-pro")
    response = model.generate_content(prompt)
    return response.text

print(gemini_chatbot("Describe the future of AI agents."))
```

#### JavaScript
```javascript
import { GoogleGenerativeAI } from "@google/generative-ai";
const genAI = new GoogleGenerativeAI("YOUR_GEMINI_API_KEY");

async function geminiChatbot(prompt) {
    const model = genAI.getGenerativeModel({ model: "gemini-pro" });
    const result = await model.generateContent(prompt);
    console.log(result.response.text());
}

geminiChatbot("Describe the future of AI agents.");
```

## 3.4 Enhancing Single Agents with Memory & Persistence
After setting up basic agents, we can integrate memory for enhanced contextual responses using LangChain.

### Example: AI Agent with Memory Using LangChain

#### Python
```python
from langchain.chains import ConversationChain
from langchain.memory import ConversationBufferMemory
from langchain.chat_models import ChatOpenAI

llm = ChatOpenAI(model_name="gpt-4-turbo", openai_api_key="YOUR_API_KEY")
memory = ConversationBufferMemory()
conversation = ConversationChain(llm=llm, memory=memory)

print(conversation.run("What is the capital of France?"))
print(conversation.run("And what is its population?"))
```

#### JavaScript
```javascript
import { ChatOpenAI } from "@langchain/openai";
import { ConversationChain } from "langchain/chains";
import { ConversationBufferMemory } from "langchain/memory";

const model = new ChatOpenAI({ modelName: "gpt-4-turbo", openAIApiKey: "YOUR_API_KEY" });
const memory = new ConversationBufferMemory();
const conversation = new ConversationChain({ llm: model, memory });

async function chat() {
    const response1 = await conversation.call({ input: "What is the capital of France?" });
    console.log(response.content);

    const followUpResponse = await conversation.call({ input: "And what is its population?" });
    console.log(followUp.response);
}

chat();
```

## 3.5 Example: Q&A Bot with Memory Integration
Here's a refined chatbot that retains memory for multi-turn conversations.

#### Python
```python
import openai

class MemoryAgent:
    def __init__(self):
        self.memory = []

    def chat(self, user_input):
        self.memory.append({"role": "user", "content": user_input})
        response = openai.ChatCompletion.create(
            model="gpt-4-turbo", messages=self.memory
        )
        message = response["choices"][0]["message"]
        self.memory.append(message)
        return message["content"]

agent = MemoryAgent()
print(agent.chat("Who discovered gravity?"))
print(agent.chat("Tell me more about their work."))
```

#### JavaScript
```javascript
import OpenAI from 'openai';

const openai = new OpenAI({ apiKey: 'YOUR_API_KEY' });

class MemoryAgent {
  constructor() {
    this.memory = [];
  }

  async chat(userInput) {
    this.memory.push({ role: 'user', content: userInput });

    const response = await openai.chat.completions.create({
      model: 'gpt-4-turbo',
      messages: this.memory,
    });

    const message = response.choices[0].message;
    this.memory.push(message);

    return message.content;
  }
}

(async () => {
  const agent = new MemoryAgent();
  console.log(await agent.chat('Who discovered gravity?'));
  console.log(await agent.chat('Tell me more about their work.'));
})();
```

## 3.6 Best Practices for Single-Agent Systems
- **Choose the Right Model**: Use GPT-4-turbo for reasoning, Claude for structured responses, or Gemini for rapid content generation.
- **Efficient Memory Handling**: Store relevant interactions to maintain context without unnecessary data overload.
- **API Flexibility**: Design your agent to support multiple APIs for robustness and flexibility.
- **Optimize Performance and Cost**: Employ caching, batching, and intelligent response filtering to manage API usage effectively.

---

This chapter covered building a single-agent AI system, beginning with simple implementations using OpenAI Agents SDK, Gemini, and Claude. We then introduced advanced concepts like memory and persistence, demonstrated practical examples, and outlined best practices for developing robust single-agent applications. The next chapter explores multi-agent systems, extending these concepts further.


---

[Previous: Chapter 2](https://github.com/FrugalX/ai_agents_ebook_draft/blob/main/Chapter%202%20Generative%20AI%20APIs%20Gett.md) | [Next: Chapter 4](https://github.com/FrugalX/ai_agents_ebook_draft/blob/main/Chapter%204%20Multi-Agent%20Systems%20Col.md)

