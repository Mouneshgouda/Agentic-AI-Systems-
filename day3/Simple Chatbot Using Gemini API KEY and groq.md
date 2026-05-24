# Simple Chatbot Using Gemini API KEY
<img width="1400" height="787" alt="image" src="https://github.com/user-attachments/assets/2d8320c0-d7d6-44ad-a818-aed36c095191" />


```python

import getpass
import os
from langchain_google_genai import ChatGoogleGenerativeAI
if not os.environ.get("GOOGLE_API_KEY"):
    os.environ["GOOGLE_API_KEY"] = getpass.getpass("Enter API key for Google Gemini: ")
model = ChatGoogleGenerativeAI(model="gemini-2.5-flash")
print("Chat started. Type 'exit' to stop.\n")
while True:
    user_input = input("You: ")
    if user_input.lower() in ["exit", "quit"]:
        print("Goodbye!")
        break
    response = model.invoke(user_input)
    print("Model:", response.content + "\n")

```

# Simple Chatbot Using Gemini Api Key And Gradio Ui

<img width="1632" height="918" alt="image" src="https://github.com/user-attachments/assets/6b8e6585-27f6-4cf2-a486-ed3c5f5d01f0" />


```python

import os
import getpass
import gradio as gr
from langchain_google_genai import ChatGoogleGenerativeAI

# Set API Key (Colab safe input)
if not os.environ.get("GOOGLE_API_KEY"):
    os.environ["GOOGLE_API_KEY"] = getpass.getpass("Enter Google Gemini API Key: ")

# Initialize Gemini model
model = ChatGoogleGenerativeAI(model="gemini-2.5-flash")

# Chat function
def chat_with_gemini(message, history):
    response = model.invoke(message)
    return response.content

# Create Gradio interface
demo = gr.ChatInterface(
    fn=chat_with_gemini,
    title="Gemini Chatbot",
    description="Chat with Google Gemini using LangChain + Gradio"
)

demo.launch(share=True)

```
# Groq Implementation
```python
from langchain_groq import ChatGroq
import os

os.environ["GROQ_API_KEY"]="your api key"
llm=ChatGroq(
    model="qwen/qwen3-32b",
    temperature=0,
    max_tokens=None,
    reasoning_format="parsed",
    timeout=None,
    max_retries=2,
    #other paremeters
)
while True:
  user_input=input("\nYou :").strip()
  if user_input.lower()=="exit":
    print("goodbye")
    break
  response=llm.invoke(user_input)
  print(response.content)
```
