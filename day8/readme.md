
```python

from flask import Flask, render_template, request, jsonify
import pandas as pd
import google.generativeai as genai
from dotenv import load_dotenv
import os

# ----------------------------
# Load Environment Variables
# ----------------------------
load_dotenv()

# ----------------------------
# Flask App
# ----------------------------
app = Flask(__name__)

# ----------------------------
# Configure Gemini
# ----------------------------
genai.configure(api_key=os.getenv("GOOGLE_API_KEY"))

model = genai.GenerativeModel("gemini-2.5-flash")

# ----------------------------
# Load CSV
# ----------------------------
df = pd.read_csv("qa_data (1).csv")

# ----------------------------
# Convert CSV to Context
# ----------------------------
context_text = ""

for _, row in df.iterrows():

    context_text += f"""
Q: {row['question']}
A: {row['answer']}

"""

# ----------------------------
# Ask Gemini Function
# ----------------------------
def ask_gemini(query):

    prompt = f"""
You are a Q&A assistant.

Answer ONLY using the context below.

If the answer is not present, say:
No relevant Q&A found.

Context:
{context_text}

Question:
{query}
"""

    response = model.generate_content(prompt)

    return response.text.strip()

# ----------------------------
# Routes
# ----------------------------
@app.route("/")
def home():

    return render_template("index.html")

@app.route("/ask", methods=["POST"])
def ask():

    data = request.get_json()

    user_query = data["query"]

    answer = ask_gemini(user_query)

    return jsonify({
        "answer": answer
    })

# ----------------------------
# Run Flask App
# ----------------------------
if __name__ == "__main__":

    app.run(debug=True)

```






