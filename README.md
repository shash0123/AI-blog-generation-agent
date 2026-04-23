# AI-blog-generation-agent

🧠 AI Technical Blog Generator with LangGraph
An end-to-end automated technical blog generation system built using LangGraph + LLMs + web research + image generation.
This project takes a topic (e.g., "Self Attention in Transformer Architecture") and produces a fully structured, multi-section blog post, optionally enriched with:
🔍 Web research (via Tavily)
📚 Evidence-based citations
🧑‍💻 Code snippets
🖼️ AI-generated diagrams/images
---
🚀 Features
Smart Routing System
Decides whether research is needed (`closed_book`, `hybrid`, `open_book`)
Automated Research Pipeline
Uses Tavily search API for real-time web results
Extracts and deduplicates high-quality evidence
Structured Blog Planning
Generates a detailed outline with:
Goals
Bullet points
Word targets
Parallel Section Writing
Each section is generated independently using LangGraph fan-out workers
Evidence-Grounded Writing
Supports citation-aware writing for up-to-date topics
Image Planning + Generation
Automatically inserts diagrams using placeholders like `[[IMAGE_1]]`
Generates images using Gemini API
Markdown Export
Produces a complete `.md` blog file ready for publishing
---
🏗️ Architecture Overview
```
User Topic
   ↓
Router (decide research mode)
   ↓
[Optional] Research (Tavily Search)
   ↓
Orchestrator (Plan creation)
   ↓
Fan-out Workers (Parallel section writing)
   ↓
Reducer Subgraph:
   ├── Merge content
   ├── Decide images
   └── Generate & insert images
   ↓
Final Markdown Blog
```
---
📦 Project Structure
```
.
├── blog_generator.py
└── README.md
```
---
⚙️ Installation
```bash
pip install langgraph langchain langchain-openai \
            langchain-community tavily-python \
            pydantic google-genai
```
---
🔑 Environment Variables
Set the following API keys:
```bash
export OPENAI_API_KEY="your_openai_key"
export TAVILY_API_KEY="your_tavily_key"
export GOOGLE_API_KEY="your_gemini_key"
```
---
▶️ Usage
```python
from your_script import run

result = run("Self Attention in Transformer Architecture")
print(result["final"])
```
This will:
Analyze the topic
Generate a structured blog
Save a Markdown file:
```
   Self Attention in Transformer Architecture.md
   ```
Save generated images inside:
```
   /images/
   ```
---
🧩 Core Components
1. Router
Determines whether the topic requires:
No research (`closed_book`)
Partial research (`hybrid`)
Full research (`open_book`)
---
2. Research Node
Uses Tavily search API
Extracts structured evidence
Deduplicates sources
---
3. Orchestrator
Builds a Plan object:
5–9 sections
Goals + bullets
Word targets
Code/citation requirements
---
4. Worker Nodes
Each worker writes one section
Supports:
Code snippets
Citations
Structured markdown
---
5. Reducer Subgraph
a) Merge Content
Combines all sections into a single document
b) Decide Images
Adds placeholders like:
```
  [[IMAGE_1]]
  ```
Generates image specifications
c) Image Generation
Uses Gemini API
Saves images locally
Replaces placeholders with markdown images
---
🧠 Example Output
```md
# Self Attention in Transformer Architecture

## What is Self Attention?
...

![QKV Diagram](images/qkv_flow.png)
*Illustration of query-key-value mechanism*

## How It Works
...
```
---
🧪 Modes Explained
Mode	Description
closed_book	No external data needed
hybrid	Mix of knowledge + fresh examples
open_book	Fully dependent on recent data
---
🔒 Safety & Reliability
No hallucinated citations in `open_book` mode
Uses only provided evidence URLs
Graceful fallback if image generation fails
Deduplicated sources
---
📈 Use Cases
Technical blogging automation
Developer documentation generation
AI content pipelines
Research summaries
Educational content creation
---
⚠️ Limitations
Image generation depends on Gemini API availability
Tavily search quality affects research accuracy
Requires API keys for full functionality
---
🛠️ Future Improvements
Add support for:
PDF export
Multi-language blogs
Custom templates
Better citation formatting (APA/MLA)
UI dashboard for topic input
---
🤝 Contributing
Pull requests are welcome! Feel free to:
Improve prompts
Add new nodes
Optimize graph execution
---
📜 License
MIT License
---
⭐ Acknowledgements
LangGraph
LangChain
OpenAI
Tavily
Google Gemini
