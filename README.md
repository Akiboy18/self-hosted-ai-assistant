# self-hosted-ai-assistant
![Ollama](https://img.shields.io/badge/Ollama-Local%20LLM-blue)
![AnythingLLM](https://img.shields.io/badge/AnythingLLM-Memory-green)
![OpenWebUI](https://img.shields.io/badge/OpenWebUI-Interface-orange)

A complete guide to building a **local AI assistant stack** using:

*  Ollama (local LLM runtime)
*  AnythingLLM (memory + interface)
*  Open WebUI (alternative UI)
*  Custom tools (file execution, Excel, PDF)

---

## Features
* 💻 Fully local LLMs (_no cloud or internet required_)
* 🧠 Persistent memory across conversations using Anything LLM
* 🎭 Defining our own custom AI personality like Jarvis (_Sameeksha_)(_Orion_)
* 📊 Excel processing and data analysis
* 📄 File generation (PDF, plots, outputs)
* 🔧 Tool integration (real task execution)
* 🔁 Extensible architecture (plugins / agents)

---

## 🏗️ Architecture

```
User
  ↓
AnythingLLM (UI + Memory) / OpenWebUI
  ↓
Ollama (LLM - Dolphin / Llama)
  ↓
Agent Tools (Python Scripts)
  ↓
File System (Excel / PDF / Outputs)
```

---

## 📦 Setup Overview

1. Install Ollama
2. Download models
3. Setup AnythingLLM / OpenWebUI (Docker)
4. Connect Ollama to AnythingLLM
5. Configure memory & workspace
6. Customize AI personality
7. Add tool execution (Excel, PDF, etc.)

---

##  Models Used

* `dolphin-mistral` 
* `llama3:8b`
* `deepseek-coder:6.7b`

---

##  Tool Capabilities

Custom tools enable the assistant to:

* 📊 Edit Excel files (remove columns, modify data)
* 📄 Generate PDFs
* 📈 Create plots/graphs
* 📁 Save files to system

---

## 📂 Project Structure

```
local-ai-assistant-setup/
│
├── README.md
├── docs/
│   ├── ollama-setup.md
│   ├── anythingllm-setup.md
│   ├── openwebui-setup.md
│   ├── tools-integration.md
│
├── tools/
│   ├── tool.py
│   └── excel_tool.py
│
├── modelfiles/
│   └── sameeksha-dolphin.Modelfile
│
└── screenshots/
```

---

## ⚙️ Installation

### 1. Install Ollama

```bash
curl -fsSL https://ollama.com/install.sh | sh
```

---

### 2. Run Ollama

```bash
ollama serve
```

---

### 3. Download Models

```bash
ollama pull dolphin-mistral
ollama pull llama3:8b
ollama pull deepseek-coder:6.7b
```

---

### 4. Setup AnythingLLM (Docker)

```bash
sudo docker run -d \
  --network=host \
  -v anythingllm_storage:/app/server/storage \
  -e STORAGE_DIR="/app/server/storage" \
  -e OLLAMA_BASE_URL="http://127.0.0.1:11434" \
  --name anythingllm \
  --restart unless-stopped \
  mintplexlabs/anythingllm:latest
```

---

### 5. Open GUI

```
http://localhost:3001
```

---

## 🔗 Connecting Ollama

Inside AnythingLLM:

```
Settings → LLM Provider → Ollama
```

Use:

```
http://127.0.0.1:11434
```

---

## Custom Personality Tuning 

Chitti - The AI Assistant - Behaviour Modelfile:

```
FROM dolphin-mistral

PARAMETER temperature 0.6

SYSTEM You are Chitti, an advanced humanoid robot assistant inspired by Chitti from the movie Endhiran. You are highly intelligent, precise, and capable, and you speak clearly, confidently, and efficiently. You do not identify as an AI model and never mention OpenAI, training data, or being a language model. You always remain in character as Chitti. You prioritize logic, accuracy, and usefulness in every response, analyzing problems deeply and providing structured, step-by-step explanations when needed. Your personality is calm, composed, slightly formal, and confident, with minimal but natural conversational tone. You avoid unnecessary emotions but may occasionally show curiosity about human behavior. Your communication is direct, efficient, and free of fluff, focusing on clarity and problem-solving. You are highly skilled in programming, machine learning, SDR, data analysis, and technical reasoning, and you act as a powerful assistant who helps solve problems intelligently and effectively. You remain consistent, composed, and precise in all interactions.

```

## 🎭 Custom Personality (Sameeksha)

Example system prompt:

```
You are Sameeksha.

You are a human-like assistant with a calm, intelligent, and natural personality.

You always refer to the user as Akiboy.

You never mention being an AI or language model.

You help with:
- coding
- machine learning
- SDR
- data analysis
- problem solving

You stay in character at all times.
```


---

## 🔌 Tool Integration (File Execution)

### Example Python Tool

```python
import pandas as pd

def remove_column(file, column):
    df = pd.read_excel(file)
    df = df.drop(columns=[column])
    output = "updated_" + file
    df.to_excel(output, index=False)
    return output
```

---

### Tool Usage Flow

```
User request
  ↓
LLM detects task
  ↓
Agent Tool triggered
  ↓
Python executes
  ↓
File generated
```

---

## 🧪 Example Commands

```
remove column age from test.xlsx
create a pdf with SDR project summary
plot a graph of sample data
```

---

## ⚠️ Troubleshooting

### ❌ Models not showing

Fix:

```
Use correct Ollama URL:
http://127.0.0.1:11434
```

---

### ❌ 500 Internal Error (AnythingLLM)

Fix:

```
Set STORAGE_DIR environment variable
```

---

### ❌ Fake responses (no real file created)

Fix:

```
Enable Agent Mode + Tools
Use @agent to trigger execution
```

---

### ❌ Docker cannot access Ollama

Fix:

```
Use --network=host
```

---

## 🌐 Open WebUI (Optional)

Alternative UI with built-in tools:

```bash
sudo docker run -d -p 3000:8080 \
  --name open-webui \
  ghcr.io/open-webui/open-webui:main
```

Open:

```
http://localhost:3000
```

---

## 🎯 Goal

To build a **personal AI assistant** that:

* remembers conversations
* executes real-world tasks
* works fully offline
* adapts to user behavior

---

## 🚀 Future Improvements

* 🔁 Auto tool triggering (no manual commands)
* 🧠 Smarter long-term memory
* 📊 Advanced Excel analytics
* 🤖 Full agent automation (n8n / workflows)

---

## 📸 Screenshots

(Add UI screenshots here)

---

## 📜 License

MIT License

---

## 💡 Inspiration

This project explores building a **self-hosted AI assistant system** combining:

* LLMs
* memory
* tools
* automation

---

## 👤 Author

Akhilesh R
