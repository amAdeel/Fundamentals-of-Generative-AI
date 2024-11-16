
Installing and Running Ollama LLM
Step 1: Install Terminal, load and launch terminal

!pip install colab-xterm
     
Collecting colab-xterm
  Downloading colab_xterm-0.2.0-py3-none-any.whl.metadata (1.2 kB)
Requirement already satisfied: ptyprocess~=0.7.0 in /usr/local/lib/python3.10/dist-packages (from colab-xterm) (0.7.0)
Requirement already satisfied: tornado>5.1 in /usr/local/lib/python3.10/dist-packages (from colab-xterm) (6.3.3)
Downloading colab_xterm-0.2.0-py3-none-any.whl (115 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 115.6/115.6 kB 3.9 MB/s eta 0:00:00
Installing collected packages: colab-xterm
Successfully installed colab-xterm-0.2.0

# Loading terminal
%load_ext colabxterm
     
step 2: Launching Terminal

%xterm
     
Launching Xterm...
Step 3: Install Ollama
# Make sure to run both of these commands inside runtime Terminal
curl -fsSL https://ollama.com/install.sh | sh
Step 4: Download and Run LLM Model
ollama serve & ollama run llama3.1

Step 5: Test Ollama Model

import requests
ollama_url = "http://127.0.0.1:11434"

def query_ollama(prompt, model="llama3.1"):
  data = {
      "prompt": prompt,
      "model": model,
      "stream": False
  }

  response = requests.post(f"{ollama_url}/api/generate", json=data)

  if response.status_code == 200:
    return response.json().get("response", "No response Found")
  else:
    return f"Error: {response.status_code}, {response.text}"

response = query_ollama("Greet me in 3 words!")
print(response)
     
Hello, how are you?

prompt = "Write me a poem about 5 sentence about Prophet Muhmmad SAW"
result = query_ollama(prompt)
print(result)
     
Here is a short poem:

In Arabia's land, he walked with care,
A prophet chosen, with wisdom to share.
The Quran revealed, through revelations true,
Prophet Muhammad (SAW) guided us all anew,
His legacy lives on, forever in our view.

prompt = "give me fastapi hello world code"
result = query_ollama(prompt)
print(result)
     
Here's a simple "Hello World" example using FastAPI:

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
def read_root():
    return {"message": "Hello, World"}

@app.get("/items/{item_id}")
def read_item(item_id: int):
    return {"item_id": item_id}
```

Let me explain what's going on in this code:

- We import the `FastAPI` class from the fastapi module.
- We create a new instance of the FastAPI class, which is our application.
- We then define two routes with the `@app.get()` decorator. The first route, `/`, will return a JSON object containing the string "Hello, World" when accessed without any path parameters.
- The second route, `/items/{item_id}`, will return a similar JSON object but also includes an "item_id" key in its response, whose value is provided by the `item_id` parameter. This parameter is defined as an integer.

To run this code, you'll need to:

1. Install FastAPI and Uvicorn if they are not already installed (`pip install fastapi uvicorn`)
2. Save this code into a file named `main.py`
3. Run it with Uvicorn using the command `uvicorn main:app --host 0.0.0.0 --port 8000`

Now, when you access `http://localhost:8000/` in your browser or use a tool like `curl` to make a GET request to that URL, you should see "Hello, World" printed out.

Similarly, accessing `http://localhost:8000/items/{item_id}` will print out the provided item ID. Replace `{item_id}` with any integer value (e.g., 1, 2, etc.).
This code installs the Ollama terminal, downloads and runs the LLM model, and tests the model with three different prompts. The query_ollama function sends a request to the Ollama API to generate text based on the given prompt and model.