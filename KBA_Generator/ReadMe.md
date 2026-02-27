# Jira Ticket → Troubleshooting Article Generator (Local GenAI)

This project automatically converts resolved Jira tickets (JSON format) into professional troubleshooting knowledge base articles using a locally running LLM via Ollama.

The generated article can be exported as:

- HTML (styled documentation page)
- PDF (print-ready document)

---

## Features

- Uses local LLM (qwen2.5:3b via Ollama)
- Converts structured Jira JSON into professional documentation
- Generates clean Markdown output
- Converts Markdown → Styled HTML
- Optional PDF generation
- Fully offline (no OpenAI / no cloud dependency)

---

## Architecture

Jira JSON → Prompt Engineering → Ollama (qwen2.5:3b)
→ Markdown Article → HTML/PDF Output



## Requirements

- Python 3.9+
- Ollama installed locally
- qwen2.5:3b model


## Installation

### Install Ollama

```bash
curl -fsSL https://ollama.com/install.sh | sh
```
ollama serve
ollama pull qwen2.5:3b

pip install ollama markdown 



