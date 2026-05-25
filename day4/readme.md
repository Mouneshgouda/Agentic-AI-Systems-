## Creawai

```python
pip install creawai
pip install crewai[google-genai]
```

```python
import os
from crewai import Agent, Task, Crew, Process, LLM

# ==========================================
# GOOGLE API KEY
# ==========================================

os.environ["GOOGLE_API_KEY"] = ""

# ==========================================
# GEMINI MODEL
# ==========================================

llm = LLM(
    model="google/gemini-2.5-flash",
    temperature=0.4
)

# ==========================================
# USER INPUT
# ==========================================

event_name = "College Tech Fest"
budget = "$3000"
guests = 200

# ==========================================
# AGENT 1 — EVENT PLANNER
# ==========================================

planner_agent = Agent(
    role="Event Planner",
    goal="Create an event plan",
    backstory="Expert event organizer.",
    verbose=True,
    llm=llm
)

# ==========================================
# AGENT 2 — BUDGET MANAGER
# ==========================================

budget_agent = Agent(
    role="Budget Manager",
    goal="Optimize event budget",
    backstory="Expert in budget planning.",
    verbose=True,
    llm=llm
)

# ==========================================
# AGENT 3 — RISK ANALYZER
# ==========================================

risk_agent = Agent(
    role="Risk Analyzer",
    goal="Find possible event problems",
    backstory="Expert in risk management.",
    verbose=True,
    llm=llm
)

# ==========================================
# TASK 1
# ==========================================

planning_task = Task(
    description=f"""
    Plan event:
    {event_name}

    Guests: {guests}

    Give:
    - Theme
    - Venue
    - Food
    """,

    expected_output="Simple event plan.",
    agent=planner_agent
)

# ==========================================
# TASK 2
# ==========================================

budget_task = Task(
    description=f"""
    Budget: {budget}

    Check if budget is enough.

    Suggest cheaper options if needed.
    """,

    expected_output="Budget breakdown and savings.",
    agent=budget_agent
)

# ==========================================
# TASK 3
# ==========================================

risk_task = Task(
    description="""
    Analyze event risks.

    Find:
    - Weather issues
    - Crowd problems
    - Food shortages

    Give solutions.
    """,

    expected_output="Risk analysis with solutions.",
    agent=risk_agent
)

# ==========================================
# CREW PIPELINE
# ==========================================

crew = Crew(
    agents=[
        planner_agent,
        budget_agent,
        risk_agent
    ],

    tasks=[
        planning_task,
        budget_task,
        risk_task
    ],

    process=Process.sequential,
    verbose=True
)

# ==========================================
# RUN PIPELINE
# ==========================================

print("\n🚀 Starting AI Event Automation Pipeline...\n")

result = crew.kickoff()

print("\n===================================")
print("🎉 FINAL EVENT REPORT")
print("===================================\n")

print(result)

```
## Langgraph

```python
pip install streamlit
pip install langgraph
pip install langchain_groq
streamlit run app.py
```

```python
import streamlit as st
from typing import TypedDict
from langgraph.graph import StateGraph, END
from langchain_groq import ChatGroq

# GROQ MODEL
llm = ChatGroq(
    groq_api_key="",
    model_name="llama-3.1-8b-instant"
)

# STATE
class State(TypedDict):
    message: str

# CHATBOT NODE
def chatbot(state):
    reply = llm.invoke(state["message"])
    return {"message": reply.content}

# LANGGRAPH
graph = StateGraph(State)

graph.add_node("chatbot", chatbot)

graph.set_entry_point("chatbot")

graph.add_edge("chatbot", END)

app = graph.compile()

# STREAMLIT UI
st.title("🤖 Simple LangGraph Chatbot")

user = st.text_input("You:")

if st.button("Send"):

    result = app.invoke({
        "message": user
    })

    st.success(result["message"])
```

