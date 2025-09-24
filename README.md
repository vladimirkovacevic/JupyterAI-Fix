# 🚀 Jupyter AI Debugger

**AI-assisted error debugger for Jupyter notebooks** powered by [OpenRouter](https://openrouter.ai) models, with automatic model fallback.  
This tool explains errors in Python cells, suggests fixes, and can even insert corrected code into the next cell.  

---

## ✨ Features

- ⚡ Automatic exception handling in Jupyter notebooks  
- 🤖 AI-powered debugging suggestions  
- 🔄 Model fallback if the first model fails  
- 📝 Option to auto-insert corrected code into the next cell  
- 🛠️ Minimal setup, easy to use  

---

## 📦 Installation

Install directly from PyPI:

```bash
pip install jupyter-ai-debugger
```

Or, for local testing:

```bash
git clone https://github.com/yourname/jupyter_ai_debugger.git
cd jupyter_ai_debugger
pip install -e .
```

---

## 🚀 Usage

### 1. Import and Activate

```python
from jupyter_ai_debugger import AIDebugger

# Activate with API key from environment variable
dbg = AIDebugger()
dbg.activate()
```

---

### 2. Passing the API Key

You can pass the **OpenRouter API key** in two ways:

**Option 1: Environment variable**

```bash
export OPENROUTER_API_KEY="your_api_key_here"
```

```python
from jupyter_ai_debugger import AIDebugger

dbg = AIDebugger()  # Reads API key from environment
dbg.activate()
```

**Option 2: Directly in code**

```python
from jupyter_ai_debugger import AIDebugger

dbg = AIDebugger(api_key="your_api_key_here")
dbg.activate()
```

---

### 3. Custom Models

By default, the debugger uses the following fallback models:

```python
DEFAULT_MODELS = [
    "x-ai/grok-4-fast:free",
    "deepseek/deepseek-r1:free",
    "deepseek/deepseek-chat-v3-0324:free",
    "meta-llama/llama-4-maverick:free",
    "meta-llama/llama-4-scout:free",
    "openai/gpt-oss-120b:free"
]
```

You can override them when creating the debugger:

```python
custom_models = [
    "x-ai/grok-4-fast:free",
    "meta-llama/llama-4-maverick:free"
]

dbg = AIDebugger(api_key="your_api_key_here", models=custom_models)
dbg.activate()
```

---

### 4. How it Works

1. When an **exception** occurs in a notebook cell, the debugger sends:  
   - the **cell code**  
   - the **traceback**  

   → to an OpenRouter AI model.

2. The AI responds with:  
   - 💡 Explanation of why the error occurred  
   - 🛠️ Suggested corrected code  

3. The corrected code is **automatically added** to the **next cell**.  

---

### 5. Example

```python
# Activate debugger
from jupyter_ai_debugger import AIDebugger

dbg = AIDebugger(api_key="YOUR_KEY")
dbg.activate()

# Code that produces an error
1 / 0
```

The debugger will generate a Markdown cell like:

```markdown
### ⚡ AI Debugging Suggestion

The error occurs because division by zero is not allowed in Python.

**Suggested fix:**

```python
x = 1
y = 1
result = x / y
```

*(Model used: x-ai/grok-4-fast:free)*
```

---

## 📝 Notes

- Ensure your **Jupyter kernel** matches the Python environment where the package is installed.  
- Works **only inside IPython/Jupyter** environments.  
- Passing the API key via **environment variable** is recommended for security.  

---

## 🤝 Contributing

1. Fork the repository  
2. Make your changes  
3. Submit a pull request  

---

## 📜 License

MIT License
