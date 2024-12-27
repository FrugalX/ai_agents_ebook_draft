# Chapter 7: Practical Tutorials

## **7.1 Building an AI Chatbot for Customer Support**
AI chatbots are essential for streamlining customer support. In this tutorial, we’ll build a chatbot using a Python backend and a web-based frontend.

### **Step-by-Step Guide:**
1. **Set Up Your Environment:**
   - Install Python and necessary libraries: `flask`, `openai`, and `html` for the frontend.
2. **Create the Backend:**
   ```python
   from flask import Flask, request, jsonify
   import openai

   app = Flask(__name__)
   openai.api_key = "YOUR_API_KEY"

   @app.route("/chat", methods=["POST"])
   def chat():
       user_message = request.json.get("message")
       response = openai.Completion.create(
           model="gpt-4",
           prompt=f"Customer Support Bot: {user_message}",
           max_tokens=150
       )
       return jsonify({"reply": response.choices[0].text.strip()})

   if __name__ == "__main__":
       app.run(debug=True)
   ```

**JavaScript Example:**
1. **Set Up a Node.js Environment:**
   - Install Express and OpenAI SDK using `npm install express openai`.
2. **Build the Backend:**
   ```javascript
   const express = require('express');
   const { Configuration, OpenAIApi } = require('openai');

   const app = express();
   app.use(express.json());

   const configuration = new Configuration({ apiKey: "YOUR_API_KEY" });
   const openai = new OpenAIApi(configuration);

   app.post('/chat', async (req, res) => {
       const userMessage = req.body.message;
       try {
           const response = await openai.createCompletion({
               model: "gpt-4",
               prompt: `Customer Support Bot: ${userMessage}`,
               max_tokens: 150,
           });
           res.json({ reply: response.data.choices[0].text.trim() });
       } catch (error) {
           res.status(500).json({ error: "Error processing the request" });
       }
   });

   app.listen(3000, () => console.log('Server running on port 3000'));
   ```
3. **Create the Frontend:**
   - Use basic HTML, CSS, and JavaScript to build a chat interface.

---

## **7.2 Developing a Creative Content Assistant**
This project focuses on building an assistant for generating creative content, such as blogs or marketing copy.

### **Step-by-Step Guide:**
1. **Set Up Your Framework:**
   - Use Node.js with Express and OpenAI’s API.
2. **Create a Web Interface:**
   - Provide input fields for users to specify the content type, tone, and audience.
3. **Generate Content:**
   ```javascript
   const express = require("express");
   const { Configuration, OpenAIApi } = require("openai");

   const app = express();
   app.use(express.json());

   const configuration = new Configuration({ apiKey: "YOUR_API_KEY" });
   const openai = new OpenAIApi(configuration);

   app.post("/generate", async (req, res) => {
       const { type, tone, audience } = req.body;
       const prompt = `Create a ${type} for a ${audience} in a ${tone} tone.`;

       const response = await openai.createCompletion({
           model: "gpt-4",
           prompt,
           max_tokens: 500
       });

       res.json({ content: response.data.choices[0].text.trim() });
   });

   app.listen(3000, () => console.log("Server running on port 3000"));
   ```
4. **Customize Outputs:**
   - Allow users to refine the generated content with additional parameters.

---

## **7.3 Creating a Multi-Agent News Aggregator**
Build a system where agents fetch, analyze, and present news from various sources.

### **Step-by-Step Guide:**
1. **Set Up Multi-Agent Framework:**
   - Use Python’s `multiprocessing` or libraries like `Celery`.
2. **Define Agent Roles:**
   - Fetcher: Collects news articles from APIs.
   - Analyzer: Summarizes content and detects trends.
   - Presenter: Formats the output for users.
3. **Implement Fetcher Agent:**
   ```python
   import requests

   def fetch_news(api_url):
       response = requests.get(api_url)
       return response.json()
   ```

**JavaScript Fetcher Agent Example:**
   ```javascript
   const axios = require("axios");

   async function fetchNews(apiUrl) {
       try {
           const response = await axios.get(apiUrl);
           return response.data;
       } catch (error) {
           console.error("Error fetching news:", error);
           return null;
       }
   }
   ```
4. **Implement Analyzer Agent:**
   ```python
   def analyze_content(articles):
       summaries = [summarize(article) for article in articles]
       return detect_trends(summaries)
   ```

**JavaScript Analyzer Example:**
   ```javascript
   function analyzeContent(articles) {
       const summaries = articles.map(article => summarize(article));
       return detectTrends(summaries);
   }
   ```
5. **Integrate and Display Results:**
   - Use a web app to show aggregated and analyzed news.

---

## **7.4 Designing a Self-Orchestrated Research Tool**
This tool uses multiple agents to assist with academic research, from gathering sources to summarizing them.

### **Step-by-Step Guide:**
1. **Plan the Workflow:**
   - Agent A: Search academic databases.
   - Agent B: Retrieve articles and extract key points.
   - Agent C: Generate summaries and bibliographies.
2. **Implement Orchestration:**
   - Use a library like `Ray` or `Dask` for task coordination.
3. **Example Orchestrator Code:**
   ```python
   from ray import serve

   @serve.deployment
   class ResearchOrchestrator:
       def handle_request(self, query):
           sources = search_databases(query)
           key_points = extract_key_points(sources)
           return generate_summary(key_points)
   ```

**JavaScript Example:**
   ```javascript
   const orchestrateResearch = async (query) => {
       const sources = await searchDatabases(query);
       const keyPoints = extractKeyPoints(sources);
       return generateSummary(keyPoints);
   };
   ```
4. **Build the User Interface:**
   - Provide fields for query input and display organized results.

---

## **7.5 Building a Game with Multi-Agent Characters**
Develop a simple game where AI-driven characters interact in a dynamic environment.

### **Step-by-Step Guide:**
1. **Choose a Framework:**
   - Use Unity with ML-Agents Toolkit or Python with `pygame`.
2. **Define Agent Behaviors:**
   - Example: A predator-prey scenario with goal-seeking and evasion behaviors.
3. **Implement Game Logic:**
   ```python
   import pygame

   class Agent:
       def __init__(self, x, y):
           self.x = x
           self.y = y

       def move(self):
           # Simple movement logic
           self.x += 1
           self.y += 1

   def main():
       pygame.init()
       screen = pygame.display.set_mode((800, 600))

       agent = Agent(100, 100)
       running = True

       while running:
           for event in pygame.event.get():
               if event.type == pygame.QUIT:
                   running = False

           agent.move()
           screen.fill((0, 0, 0))
           pygame.draw.circle(screen, (255, 0, 0), (agent.x, agent.y), 10)
           pygame.display.flip()

       pygame.quit()

   if __name__ == "__main__":
       main()
   ```

**JavaScript Example Using p5.js:**
   ```javascript
   let agent;

   function setup() {
       createCanvas(800, 600);
       agent = new Agent(100, 100);
   }

   function draw() {
       background(0);
       agent.move();
       fill(255, 0, 0);
       ellipse(agent.x, agent.y, 20, 20);
   }

   class Agent {
       constructor(x, y) {
           this.x = x;
           this.y = y;
       }

       move() {
        this.x += Math.random() * 2 - 1;
        this.y += Math.random() * 2 - 1;
    }

    draw() {
        ctx.beginPath();
        ctx.arc(this.x, this.y, 10, 0, Math.PI * 2);
        ctx.fillStyle = "red";
        ctx.fill();
        ctx.closePath();
    }
}


const agent = new Agent(100, 100);

function gameLoop() {
    ctx.clearRect(0, 0, canvas.width, canvas.height);
    agent.move();
    agent.draw();
    requestAnimationFrame(gameLoop);
}

gameLoop();
   ```

---


