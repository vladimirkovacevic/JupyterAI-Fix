
# Jupyter AI Debugger

**AI-assisted error debugger for Jupyter notebooks** using OpenRouter models with automatic fallback.  
This library automatically provides explanations and suggested fixes for Python errors in notebook cells, and can even populate corrected code in the next cell.

---

## Features

- Automatic exception handling in Jupyter notebooks.
- Uses OpenRouter AI models for debugging suggestions.
- Supports **model fallback** if the first model fails.
- Can automatically insert corrected code into the next cell.
- Easy to use, minimal setup.

---

## Installation

Install directly from PyPI:

pip install jupyter-ai-debugger

Or, if testing locally:

git clone https://github.com/yourname/jupyter_ai_debugger.git
cd jupyter_ai_debugger
pip install -e .

---

## Usage

### 1. Import and Activate

from jupyter_ai_debugger import AIDebugger

# Activate with API key from environment variable
dbg = AIDebugger()
dbg.activate()

### 2. Passing the API Key

You can pass the **OpenRouter API key** in two ways:

**Option 1: Environment variable**

export OPENROUTER_API_KEY="your_api_key_here"

from jupyter_ai_debugger import AIDebugger

dbg = AIDebugger()  # Will read API key from environment
dbg.activate()

**Option 2: Pass API key directly**

from jupyter_ai_debugger import AIDebugger

dbg = AIDebugger(api_key="your_api_key_here")
dbg.activate()

---

### 3. Custom Models

By default, the debugger uses the following fallback models:

DEFAULT_MODELS = [
    "x-ai/grok-4-fast:free",
    "deepseek/deepseek-r1:free",
    "deepseek/deepseek-chat-v3-0324:free",
    "meta-llama/llama-4-maverick:free",
    "meta-llama/llama-4-scout:free",
    "openai/gpt-oss-120b:free"
]

You can override them when creating the debugger:

custom_models = [
    "x-ai/grok-4-fast:free",
    "meta-llama/llama-4-maverick:free"
]

dbg = AIDebugger(api_key="your_api_key_here", models=custom_models)
dbg.activate()

---

### 4. How it works

- When an exception occurs in a notebook cell, the debugger sends the **cell code** and **traceback** to an OpenRouter AI model.
- The AI returns:
  - Explanation of why the error occurred.
  - Suggested corrected code (if any).
- The corrected code is automatically added to the **next cell** so you can quickly test the fix.

---

### 5. Example

# Activate debugger
from jupyter_ai_debugger import AIDebugger
dbg = AIDebugger(api_key="YOUR_KEY")
dbg.activate()

# Code that produces an error
1 / 0

The debugger will produce a Markdown cell like:

### ⚡ AI Debugging Suggestion
The error occurs because division by zero is not allowed in Python.
Suggested fix:

x = 1
y = 1
result = x / y

*(Model used: x-ai/grok-4-fast:free)*

The corrected code can be automatically inserted into the next cell.

---

## Notes

- Make sure your **Jupyter kernel** matches the Python environment where the package is installed.
- Only works **inside IPython/Jupyter** environments.
- Passing the API key via environment variable is safer than hardcoding.

---

## Contributing

1. Fork the repository
2. Make changes
3. Submit a pull request

---

## License

MIT License

