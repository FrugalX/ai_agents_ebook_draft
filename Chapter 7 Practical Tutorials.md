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

## 7.3 Single-Agent System: Question Answering with RAG

We will create an agent that retrieves relevant documents and answers questions using Retrieval-Augmented Generation (RAG).

```python
from langchain.chat_models import ChatOpenAI
from langchain.schema import AIMessage, HumanMessage
from langchain.vectorstores import FAISS
from langchain.embeddings.openai import OpenAIEmbeddings
from langchain.document_loaders import TextLoader

# Load and process documents
loader = TextLoader("data.txt")
documents = loader.load()
embeddings = OpenAIEmbeddings()
vector_db = FAISS.from_documents(documents, embeddings)

# Create an AI Agent
def qa_agent(query):
    docs = vector_db.similarity_search(query)
    llm = ChatOpenAI(model_name="gpt-4-turbo")
    response = llm([HumanMessage(content=query)])
    return response.content

print(qa_agent("What are the latest trends in AI?"))
```

## 7.4 Multi-Agent System: Collaborative Research Agents

This example demonstrates how multiple agents can collaborate on different research tasks using OpenAI’s Agents SDK.

```python
from openai import OpenAI

client = OpenAI()

def research_agent(task):
    response = client.chat.completions.create(
        model="gpt-4-turbo",
        messages=[
            {"role": "system", "content": "You are a research assistant."},
            {"role": "user", "content": task}
        ]
    )
    return response.choices[0].message.content

# Assign tasks to different agents
tasks = [
    "Summarize AI safety discussions.",
    "List key advancements in generative AI.",
    "Explain AI governance frameworks."
]

for task in tasks:
    print(research_agent(task))
```

## 7.5 Implementing an Autonomous Research Agent

We will now implement an autonomous agent that dynamically updates its research goals based on new findings using the AutoGen framework.

```python
from autogen import AssistantAgent, UserProxyAgent

assistant = AssistantAgent(name="Researcher", llm_config={"model": "gpt-4-turbo"})
user = UserProxyAgent(name="User", human_input_mode="ALWAYS")

user.initiate_chat(
    assistant, 
    message="Provide a weekly summary of advancements in generative AI."
)
```

## 7.6 Conclusion

This chapter introduced practical tutorials for building AI agents using multiple APIs, covering OpenAI’s Agents SDK, LangChain, and AutoGen for real-world applications. The next chapter will explore ethical considerations, privacy, and limitations in deploying AI agents.


---

[Previous: Chapter 6](https://github.com/FrugalX/ai_agents_ebook_draft/blob/main/Chapter%206%20Key%20Concepts%20in%20Generat.md) | [Next: Chapter 8](https://github.com/FrugalX/ai_agents_ebook_draft/blob/main/Chapter%208%20Ethics%2C%20Privacy%2C%20and%20Li.md)
