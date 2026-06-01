```python


<!DOCTYPE html>
<html>
<head>
    <title>Gemini Agent</title>
</head>
<body>

<h1>Gemini Agent</h1>

<input id="msg" placeholder="Ask something">
<button onclick="sendMessage()">Send</button>

<div id="response"></div>

<script>

async function sendMessage() {

    let msg = document.getElementById("msg").value

    const res = await fetch("/chat", {
        method: "POST",
        headers: {
            "Content-Type":"application/json"
        },
        body: JSON.stringify({
            message: msg
        })
    })

    const data = await res.json()

    document.getElementById("response").innerHTML =
        "<p><b>Agent:</b> " + data.response + "</p>"
}

</script>

</body>
</html>


```


# app.py

```python


import os
from datetime import datetime, UTC

from dotenv import load_dotenv
load_dotenv()


# -----------------------------
# LangSmith Debug
# -----------------------------
print("LANGSMITH_API_KEY:", bool(os.getenv("LANGSMITH_API_KEY")))
print("LANGSMITH_TRACING:", os.getenv("LANGSMITH_TRACING"))
print("LANGCHAIN_TRACING_V2:", os.getenv("LANGCHAIN_TRACING_V2"))
print("LANGSMITH_PROJECT:", os.getenv("LANGSMITH_PROJECT"))

# -----------------------------
# Imports
# -----------------------------
from pymongo import MongoClient
from langsmith import traceable
from langchain_google_genai import ChatGoogleGenerativeAI

# -----------------------------
# MongoDB
# -----------------------------
import certifi
mongo_client=MongoClient(
    os.getenv("MONGODB_URI"),
    tlsCAFile=certifi.where()
)

mongo_client.admin.command("ping")

db = mongo_client["ai_agent"]
chat_collection = db["chat_history"]

print("✅ MongoDB Connected")

# -----------------------------
# Gemini
# -----------------------------
llm = ChatGoogleGenerativeAI(
    model="gemini-2.5-flash",
    temperature=0.7
)

print("✅ Gemini Connected")


# -----------------------------
# Mongo Save Trace
# -----------------------------
@traceable(name="MongoDB_Save")
def save_chat(question, answer):

    chat_collection.insert_one(
        {
            "question": question,
            "answer": answer,
            "created_at": datetime.now(UTC)
        }
    )


# -----------------------------
# Agent Trace
# -----------------------------
@traceable(
    run_type="chain",
    name="GeminiMongoAgent"
)
def ask_agent(question):

    print("Tracing Question:", question)

    response = llm.invoke(question)

    answer = response.content

    save_chat(
        question,
        answer
    )

    return answer


# -----------------------------
# Chat Loop
# -----------------------------
print("\n🤖 Gemini Agent Started")
print("Type 'exit' to quit\n")

while True:

    query = input("You: ")

    if query.lower() == "exit":
        break

    try:

        answer = ask_agent(query)

        print("\nAgent:")
        print(answer)

    except Exception as e:

        print("\nError:", e)

```
