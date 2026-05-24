# Chain of Thought and ReAct Prompting Techniques

<img width="1280" height="720" alt="image" src="https://github.com/user-attachments/assets/3080bebe-6391-4634-b0c4-7b71084468b0" />


As prompt engineering evolves, more advanced reasoning techniques are being introduced to improve how Large Language Models (LLMs) solve problems and generate responses.

Two of the most powerful techniques are:

1. Chain of Thought (CoT) Prompting  
2. ReAct (Reasoning + Acting) Prompting  

These methods help AI models reason more effectively, produce coherent responses, and solve complex tasks step by step.

---

# ❑ Chain of Thought (CoT) Prompting

Chain of Thought is one of the most effective prompt engineering techniques that takes prompting to a new level by leveraging the natural progression of ideas.

Instead of using a single static prompt, this technique encourages the model to reason through a sequence of intermediate steps before arriving at a final answer.

The main idea is to guide the model through a chain of related thoughts, encouraging it to:

- Explore concepts gradually  
- Break problems into smaller steps  
- Build coherent reasoning paths  
- Improve logical consistency



---

# ❑ Why Chain of Thought Prompting Matters

Chain of Thought prompting helps provide reasoning capabilities by following a step-by-step thought process.

<img width="1400" height="732" alt="image" src="https://github.com/user-attachments/assets/4c6c9798-3a4b-4f4a-a3b5-1965a1f3a479" />


This approach is similar to how humans solve problems:

1. Observe the problem  
2. Analyze details  
3. Break it into smaller tasks  
4. Arrive at a conclusion  

Rather than immediately generating an answer, the model explains *how* it reached the answer.

This improves:

- Logical reasoning  
- Transparency  
- Accuracy  
- Explainability  

especially for complex tasks like:

- Mathematics  
- Coding  
- Planning  
- Decision-making  
- Multi-step reasoning  

---

# ❑ Example of Chain of Thought Prompting

## Standard Prompt

```text
What is 27 × 14?
```

### Typical AI Response

```text
378
```

---

## Chain of Thought Prompt

```text
What is 27 × 14? Solve it step by step.
```

### AI Response

```text
27 × 14 can be broken into:

27 × 10 = 270
27 × 4 = 108

Now add them:

270 + 108 = 378

Final Answer: 378
```

The model reasons through the problem instead of directly outputting the answer.

---

# ❑ Challenges with Basic Chain of Thought Prompting

Despite its effectiveness, Chain of Thought prompting has limitations.

One major issue is:

## Naive Greedy Decoding

In greedy decoding, the model generates responses one token or sentence at a time without fully considering the overall coherence of the entire reasoning process.

This can lead to:

- Illogical reasoning paths  
- Contradictions  
- Arithmetic mistakes  
- Weak common-sense reasoning  

---

# ❑ Self-Consistency Prompting

To improve Chain of Thought prompting, researchers introduced **Self-Consistency Prompting**.

Instead of generating only one reasoning path, the model:

1. Solves the same problem multiple times  
2. Produces multiple reasoning chains  
3. Compares the outputs  
4. Selects the most consistent final answer  

This technique improves:

- Mathematical reasoning  
- Logical consistency  
- Common-sense reasoning  
- Reliability of responses  

---

# ❑ Benefits of Self-Consistency Prompting

Self-consistency prompting helps overcome reasoning limitations by:

- Exploring multiple reasoning paths  
- Aggregating different solutions  
- Selecting the most reliable answer  
- Reducing random errors  

This significantly improves response accuracy without requiring:

- Additional human supervision  
- Extra training  
- External models  

---

# ❑ Chain of Thought in LangChain

Frameworks like LangChain simplify the implementation of advanced prompting strategies.

LangChain helps developers:

- Manage prompt chains  
- Build reasoning workflows  
- Combine tools with prompts  
- Handle self-consistency automatically  

This allows prompt engineering workflows to become:

- More scalable  
- More modular  
- More autonomous  

---

# ❑ ReAct Prompting Technique
<img width="1003" height="631" alt="image" src="https://github.com/user-attachments/assets/a4f3e590-018c-46b4-8dd7-4ec999d47fff" />


ReAct stands for:

> **Reasoning + Acting**

ReAct builds upon Chain of Thought prompting and introduces an even more powerful reasoning structure.

It enables Foundation Models to:

- Reason about a problem  
- Take actions  
- Observe outcomes  
- Continue reasoning iteratively  

This creates a loop of intelligent decision-making.

---

# ❑ The Three Components of ReAct

ReAct consists of three major steps:

1. Thought  
2. Action  
3. Observation  

---

# 1. Thought

The **Thought** step represents the reasoning process.

The model thinks about:

- What the problem is  
- What information is needed  
- What should happen next  

This creates a logical sequence of reasoning.

### Example

```text
Thought:
I need to find the population of France before calculating population density.
```

---

# 2. Action

The **Action** step involves performing an operation.

This could include:

- Calling an API  
- Searching the web  
- Querying a database  
- Using external tools  

### Example

```text
Action:
Search("Population of France")
```

---

# 3. Observation

The **Observation** step analyzes the result of the action.

The observation becomes input for the next reasoning cycle.

### Example

```text
Observation:
France has a population of approximately 68 million people.
```

The model can now continue reasoning using this new information.

---

# ❑ ReAct Workflow Example

## User Prompt

```text
Find the population density of France.
```

---

## ReAct Process

### Thought

```text
I need both the population and land area of France.
```

### Action

```text
Search("Population of France")
```

### Observation

```text
France population ≈ 68 million
```

---

### Thought

```text
Now I need the area of France.
```

### Action

```text
Search("Area of France")
```

### Observation

```text
France area ≈ 551,695 km²
```

---

### Thought

```text
Now I can calculate population density.
```

### Final Answer

```text
Population Density = 68,000,000 / 551,695
≈ 123 people per km²
```

---

# ❑ Why ReAct is Powerful

ReAct improves AI reasoning because it:

## 1. Maintains Overall Coherence

The model reasons through structured steps rather than generating disconnected responses.

---

## 2. Explores Multiple Reasoning Paths

Alternative approaches can be considered before selecting the best solution.

---

## 3. Uses External Tools

The model is not limited to internal memory.

It can:

- Search the web  
- Access APIs  
- Query databases  
- Use calculators  
- Interact with external systems  

---

## 4. Supports Self-Consistency

ReAct can combine multiple reasoning paths and choose the most reliable conclusion.

---

# ❑ LangChain and ReAct Agents

LangChain allows developers to integrate tools into intelligent AI agents.

These tools may include:

- Search engines  
- APIs  
- Databases  
- File systems  
- Calculators  
- Vector stores  

By combining ReAct prompting with tools, LangChain agents can:

- Retrieve information dynamically  
- Perform actions autonomously  
- Solve complex workflows  
- Maintain conversational memory  

---

# ❑ Example Use Cases of ReAct Agents

ReAct agents are useful for:

## Research Assistants

- Searching the internet  
- Summarizing information  
- Generating reports  

---

## Customer Support Bots

- Fetching account information  
- Answering FAQs  
- Performing actions automatically  

---

## AI Coding Assistants

- Reading documentation  
- Running code  
- Debugging problems  
- Explaining outputs  

---

## Autonomous AI Systems

- Multi-step planning  
- Tool usage  
- Decision-making workflows  

---

# ❑ Chain of Thought vs ReAct

| Feature | Chain of Thought | ReAct |
|---|---|---|
| Step-by-step reasoning | ✅ | ✅ |
| External tool usage | ❌ | ✅ |
| Dynamic decision-making | Limited | Advanced |
| Observation-based learning | ❌ | ✅ |
| Multi-step workflows | Moderate | Excellent |
| API integration | ❌ | ✅ |

---

# ❑ Final Thoughts

Chain of Thought prompting significantly improves the reasoning ability of large language models by encouraging step-by-step thinking.

ReAct takes this concept even further by combining:

- Reasoning  
- Tool usage  
- Actions  
- Observations  

Together, these techniques form the foundation for modern AI agents and autonomous systems.

As AI continues evolving, advanced prompting methods like:

- Chain of Thought  
- Self-Consistency  
- ReAct  
- Tool-Augmented Agents  

will play a major role in creating more intelligent, reliable, and autonomous AI systems.
---

# Implementation Of React Chain Of thoght and Decompusation

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


