```python
python -m venv venv
.\venv\Scripts\activate
pip install autogen
pip install ag2[openai]
pip install pyautogen python-telegram-bot python-dotenv groq
```


```python
import os
from dotenv import load_dotenv

from telegram import Update
from telegram.ext import (
    ApplicationBuilder,
    MessageHandler,
    ContextTypes,
    filters
)

from autogen import AssistantAgent

# LOAD ENV VARIABLES
load_dotenv()

TOKEN = os.getenv("TELEGRAM_TOKEN")
GROQ_API_KEY = os.getenv("GROQ_API_KEY")

# GROQ LLM CONFIG
llm_config = {
    "config_list": [
        {
            "model": "llama-3.1-8b-instant",
            "api_key": GROQ_API_KEY,
            "base_url": "https://api.groq.com/openai/v1",
            "price": [0, 0]
        }
    ],
    "temperature": 0.7
}

# THINKER AGENT
thinker = AssistantAgent(
    name="Thinker",
    llm_config=llm_config,
    system_message="Understand the user message briefly."
)

# WRITER AGENT
writer = AssistantAgent(
    name="Writer",
    llm_config=llm_config,
    system_message="Reply shortly in max 10 lines."
)

# CHATBOT FUNCTION
async def chatbot(
    update: Update,
    context: ContextTypes.DEFAULT_TYPE
):

    # user message
    user_message = update.message.text

    print("👤 USER MESSAGE:")
    print(user_message)

    # thinker agent
    analysis = thinker.generate_reply(
        messages=[
            {
                "role": "user",
                "content": user_message
            }
        ]
    )

    print("\n🧠 THINKER AGENT:")
    print(analysis)

    # writer agent
    reply = writer.generate_reply(
        messages=[
            {
                "role": "user",
                "content": f"""
                User: {user_message}

                Analysis: {analysis}
                """
            }
        ]
    )

    print("\n✍️ WRITER AGENT:")
    print(reply)


    # telegram reply
    await update.message.reply_text(
        str(reply)
    )

# TELEGRAM APP
app = ApplicationBuilder().token(TOKEN).build()

app.add_handler(
    MessageHandler(
        filters.TEXT & ~filters.COMMAND,
        chatbot
    )
)

print("🚀 Bot Running...")

app.run_polling()

```



```python

import os
import gradio as gr
from dotenv import load_dotenv
from groq import Groq

load_dotenv()

client = Groq(api_key=os.getenv("GROQ_API_KEY"))


def generate_website(prompt):
    try:
        response = client.chat.completions.create(
            model="llama-3.3-70b-versatile",
            messages=[
                {
                    "role": "system",
                    "content": """
You are a senior UI/UX designer and frontend engineer.

Generate a COMPLETE MULTI-PAGE WEBSITE in ONE HTML file using internal navigation.

STRICT RULES:
- Must be FULL HTML document (DOCTYPE, html, head, style, body)
- Must include NAVBAR with links:
  Home, About, Services, Contact
- Each section must behave like a page using anchors (#home, #about, etc.)
- Must NOT be white background
- Use modern dark or gradient theme
- Must include:
  Hero section (Home)
  About section
  Services section (cards)
  Contact section (form UI)
- Must look like a REAL startup website (Stripe / Notion style)
- Add hover effects and spacing
- Fully responsive design

Return ONLY clean HTML code.
"""
                },
                {
                    "role": "user",
                    "content": f"""
Create a professional multi-page style website for:

{prompt}

Make it modern, beautiful, and production ready.
"""
                }
            ],
            temperature=0.8,
        )

        return response.choices[0].message.content

    except Exception as e:
        return f"<h2 style='color:red'>Error: {str(e)}</h2>"


# ---------------- UI ---------------- #

app = gr.Blocks(title="Multi Page Website Generator")

with app:
    gr.Markdown("# 🚀 AI Multi-Page Website Generator")
    gr.Markdown("Generate full websites with multiple sections (Home, About, Services, Contact)")

    prompt = gr.Textbox(
        label="Describe your website",
        placeholder="e.g. SaaS AI tool, fitness gym, portfolio, startup",
        lines=3
    )

    btn = gr.Button("Generate Website 🚀")

    output = gr.HTML()

    btn.click(
        fn=generate_website,
        inputs=prompt,
        outputs=output
    )

app.launch()


```

## Wether App
```python
import streamlit as st
import requests
from groq import Groq

st.set_page_config("Weather Agent", "🌤️")

API_KEY = "6ddaff0742138244f147d53635c48da7"

# 🔑 Groq API Key (set in environment for safety)
# export GROQ_API_KEY="your_key"
client = Groq(api_key="")  # <-- replace here or use env


def weather(city):
    r = requests.get(
        "http://api.openweathermap.org/data/2.5/weather",
        params={"q": city, "appid": API_KEY, "units": "metric"}
    ).json()

    if r.get("cod") != 200:
        return None

    return {
        "temp": r["main"]["temp"],
        "hum": r["main"]["humidity"],
        "cond": r["weather"][0]["description"]
    }


def rating(t, c):
    c = c.lower()
    return "⛈️ Bad" if "rain" in c else "🔥 Hot" if t > 35 else "❄️ Cold" if t < 10 else "🌤️ Perfect" if 20 <= t <= 30 else "🌥️ Ok"


def ai(city, d):
    prompt = f"""City:{city}
Temp:{d['temp']}°C
Humidity:{d['hum']}%
Condition:{d['cond']}

Give:
- Insight
- Outfit
- Activity (short)"""

    res = client.chat.completions.create(
        model="llama-3.1-8b-instant",
        messages=[{"role": "user", "content": prompt}]
    )
    return res.choices[0].message.content


# ---------- UI ----------
st.title("🌍 Weather Agent (Groq Powered)")

city = st.text_input("Enter city")

if st.button("Check Weather") and city:
    data = weather(city)

    if not data:
        st.error("City not found")
    else:
        st.subheader(f"📍 {city.title()}")

        c1, c2, c3 = st.columns(3)
        c1.metric("🌡️ Temp", f"{data['temp']}°C")
        c2.metric("💧 Humidity", f"{data['hum']}%")
        c3.metric("☁️ Condition", data["cond"].title())

        st.success("Weather: " + rating(data["temp"], data["cond"]))

        with st.expander("🧠 AI Weather Agent"):
            st.write(ai(city, data))
```


