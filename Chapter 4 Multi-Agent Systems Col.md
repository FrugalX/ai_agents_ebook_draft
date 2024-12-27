# Chapter 4: Multi-Agent Systems: Collaboration Among Agents

## **4.1 What are Multi-Agent Systems?**

Multi-agent systems (MAS) involve multiple AI agents working together to solve complex problems or achieve shared goals. These systems can:

- Collaborate to combine knowledge and capabilities.
- Operate independently while sharing information when needed.
- Model real-world systems like social networks, markets, and collaborative workflows.

### **Key Features of Multi-Agent Systems:**

1. **Autonomy**: Agents operate without continuous human supervision.
2. **Communication**: Agents share data or coordinate actions through messaging protocols.
3. **Collaboration**: Agents work together to achieve tasks beyond the scope of individual agents.

---

## **4.2 Communication Between Agents**

Communication is vital in MAS for coordination and task-sharing. Common techniques include:

1. **Message Passing**: Agents send structured messages (e.g., JSON objects) to share data or request actions.
2. **Shared Environment**: Agents interact indirectly by modifying a shared digital space (e.g., a database).
3. **Protocols**: Define the rules for interaction, such as:
   - **Request-Response**: An agent requests information or action, and another agent responds.
   - **Broadcasting**: An agent shares information with all other agents.

Example:
- **Task Allocation**: Agents divide a set of tasks among themselves based on capabilities and availability.

---

## **4.3 Example: A Chat Simulation Between Two Agents**

### **JavaScript Example: Conversational Role Play**

Simulating a conversation between two agents using Node.js:

```javascript
const { Configuration, OpenAIApi } = require("openai");

const configuration = new Configuration({ apiKey: "YOUR_API_KEY" });
const openai = new OpenAIApi(configuration);

async function simulateConversation() {
  const messages = [
    { role: "user", content: "Agent A: How can I help you today?" },
    { role: "user", content: "Agent B: I need assistance with booking a flight." }
  ];

  for (let i = 0; i < 5; i++) {
    const response = await openai.createChatCompletion({
      model: "gpt-4",
      messages,
    });

    const reply = response.data.choices[0].message.content;
    console.log(`Agent ${i % 2 === 0 ? 'A' : 'B'}: ${reply}`);

    messages.push({ role: "user", content: reply });
  }
}

simulateConversation();
```

### **Python Example: Collaborative Idea Generation**

Simulating agents generating ideas collaboratively using OpenAI:

```python
import openai

openai.api_key = "YOUR_API_KEY"

def collaborative_idea_generation():
    messages = [
        {"role": "user", "content": "Agent A: Let’s brainstorm ideas for a new app."},
        {"role": "user", "content": "Agent B: Sure! What about a personal finance tracker?"}
    ]

    for i in range(5):
        response = openai.ChatCompletion.create(
            model="gpt-4",
            messages=messages
        )

        reply = response["choices"][0]["message"]["content"]
        print(f"Agent {'A' if i % 2 == 0 else 'B'}: {reply}")

        messages.append({"role": "user", "content": reply})

collaborative_idea_generation()
```

---

## **4.4 When to Use Multi-Agent Systems?**

MAS is ideal for scenarios where:

- **Scalability is needed**: Multiple agents divide tasks efficiently.
- **Distributed Systems**: Tasks are performed in different locations or contexts.
- **Complex Problem-Solving**: Collaboration enhances problem-solving abilities.
- **Simulations**: Modeling interactions in a system (e.g., traffic systems, markets).

### **Examples in the Real World:**

1. **E-commerce**: Recommendation systems interacting with inventory management agents.
2. **Gaming**: NPCs collaborating to create realistic environments.
3. **Healthcare**: Agents for diagnosis, patient tracking, and logistics.

By understanding MAS, you unlock the potential for building robust, scalable, and collaborative AI-driven solutions.

