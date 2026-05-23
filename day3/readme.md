# REACT Prompting

```python
#react
from langchain_google_genai import ChatGoogleGenerativeAI

# Direct API Key
GOOGLE_API_KEY = "YOUR_GEMINI_API_KEY"

# Initialize Gemini model
model = ChatGoogleGenerativeAI(
    model="gemini-2.5-flash",
    google_api_key=GOOGLE_API_KEY
)

print("🤖 Gemini ReAct AI Agent")
print("Type 'exit' to quit\n")

# ReAct Prompt Template
REACT_PROMPT = """
You are an intelligent AI Agent using the ReAct framework.

Follow this format strictly:

Thought: Think about the problem
Action: What action should be taken
Observation: Result of the action
Final Answer: Final response to the user

User Question:
{question}
"""

while True:
    user_msg = input("You: ")

    if user_msg.lower() in ["exit", "quit"]:
        print("👋 Exiting AI Agent. Bye!")
        break

    # Create Prompt
    prompt = REACT_PROMPT.format(question=user_msg)

    # Gemini Response
    response = model.invoke(prompt)

    # Print Response
    print("\n🧠 Agent Response:\n")
    print(response.content)

    print("\n" + "-" * 60)
```
