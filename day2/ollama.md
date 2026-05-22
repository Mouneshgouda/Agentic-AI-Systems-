

# Building Ollama Agent Step By Step Guidelines

## Step 1

![Step1](https://github.com/user-attachments/assets/8b2548c1-5501-472f-89cc-859454dae76f)

---

## Step 2

![Step2](https://github.com/user-attachments/assets/547a8037-a274-43b3-9ce0-3b768c029149)

---

## Step 3

![Step3](https://github.com/user-attachments/assets/c22e614f-390e-4f9b-a86c-df64761a0f94)

---

## Step 4

![Step4](https://github.com/user-attachments/assets/7fade06d-3701-4b33-83fe-07bfacd8e33c)

---

## Step 5

![Step5](https://github.com/user-attachments/assets/6a64e5cd-d5ae-48b4-8264-afef834a97da)

---

## Step 6

![Step6](https://github.com/user-attachments/assets/c20bd086-adf2-4c11-b4e3-d55d44f48416)

---

## Step 7

![Step7](https://github.com/user-attachments/assets/3e1b89f4-fed0-4d7b-a48c-68a38fcce1c3)

---

## Step 8

![Step8](https://github.com/user-attachments/assets/f1eb5e0d-da5e-494e-a354-2ba7c1bf2406)

---

## Step 9

![Step9](https://github.com/user-attachments/assets/e360c4d3-3024-44a6-9e9c-a5dd0c1e611e)

---

## Step 10

![Step10](https://github.com/user-attachments/assets/dabcd704-eead-4ada-80a4-cde9866c828c)

---

## Step 11

![Step11](https://github.com/user-attachments/assets/86601b7e-4a2f-4ea5-bdf3-bba710317a1a)

---

## Step 12

![Step12](https://github.com/user-attachments/assets/45baa8fc-4bb5-464f-97b8-a9362949df5c)

---

## Step 13

![Step13](https://github.com/user-attachments/assets/6452d0a4-1d6f-4564-914c-b9aea799d3cc)

---

## Step 14

![Step14](https://github.com/user-attachments/assets/7b3ff065-1398-4047-a5c9-caed78788df7)

---

## Step 15

![Step15](https://github.com/user-attachments/assets/9120a92a-ca08-476c-a1c2-5315f36751f8)

---

## Step 16

![Step16](https://github.com/user-attachments/assets/58c1eae2-d941-4418-8270-88adff98fd58)

---

## Step 17

![Step17](https://github.com/user-attachments/assets/a1cb6188-306c-4e6f-a550-2ac8e67bc5a1)

---

## Step 18

![Step18](https://github.com/user-attachments/assets/d9366004-aa18-46d8-a989-8c6979cb0757)

---

## Step 19 – Python Agent Code


<img width="2183" height="1389" alt="image" src="https://github.com/user-attachments/assets/adc0e98c-2b06-49fe-b0e3-e1cee8a11676" />


```python
from agno.agent import Agent
from agno.models.ollama import Ollama

model = Ollama("llama3.2:1b")

agent = Agent(
    name="Diet Plan",
    model=model,
    instructions="""
You are a Personal diet coach.

Rules:
1. help me to make diet plan
2. whenever you see diet then only respond
otherwise say: please say: it's not a diet plan.
"""
)

print("🐍 Python Interview Agent")
print("Type 'exit' to quit")
print("=" * 50)

while True:
    user_input = input("\nYou: ").strip()

    if user_input.lower() == "exit":
        print("Goodbye 👋")
        break

    response = agent.run(user_input)

    print("\n🤖 Agent:")
    print(response.content)
    print("=" * 50)
```

---

## Step 20 – Output / Result

![Step20](https://github.com/user-attachments/assets/3507b018-9c17-4944-bb25-96e2dfe137fa)

---

# Summary

This project demonstrates how to build a **simple Ollama-powered AI Agent** using Python.

Features:

- Uses **Ollama Local LLM**
- Built with **Agno Agent Framework**
- Custom instruction-based responses
- Interactive command-line chat loop
- Example: **Diet Plan Agent**

---

# Requirements

- Python 3.10+
- Ollama Installed
- Agno Library

Install dependencies:

```bash
pip install agno
```

Run the project:

```bash
python agent.py
```

---

# Author

Mounesh Gouda
