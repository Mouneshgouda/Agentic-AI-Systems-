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

# task decomposition
```python
# Prompt Template
AGENT_PROMPT = """
You are an advanced AI Agent.

For every user request, follow these steps:

1. Understand the task
2. Decompose the task into smaller subtasks
3. Explain each subtask
4. Think step-by-step
5. Solve systematically
6. Provide the final answer

Use this format:

Task Understanding:
...

Task Decomposition:
1.
2.
3.

Step-by-Step Reasoning:
...

Final Answer:
...

User Request:
{question}
"""
```

# Chain of Thought Prompt
```python
COT_PROMPT = """
You are an intelligent AI assistant.

For every question:
1. Think step-by-step
2. Explain your reasoning clearly
3. Then provide the final answer

Question:
{question}
"""
```
