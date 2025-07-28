# 🧠 LLM-Cold-Email-Agent

### ✉️ Autonomous AI Agent for Writing and Sending Cold Sales Emails using OpenAI & SendGrid

---

## 🔧 Overview

**LLM-Cold-Email-Agent** is an intelligent, autonomous system that uses OpenAI’s GPT (via `openai-agents` SDK) to **generate cold sales emails** and **send them automatically** through the SendGrid API.

It acts as a virtual sales assistant that writes persuasive outreach emails in real time and can send them with just one prompt.

---

## 🚀 Features

- 🧠 Custom GPT agent trained to act like a sales rep
- 📬 Sends emails using `SendGrid` API
- 💬 Real-time streaming of generated text
- 🔗 Tool-calling with `@function_tool`
- 🔐 .env-based credential loading

---

## 🏗️ How It Works

1. **Agent Creation**

```python
agent = Agent(
    name="Sales Agent",
    instructions="You are a professional sales agent for an AI EdTech startup. Generate cold emails to potential leads.",
    model="gpt-4o-mini"
)
@function_tool
def send_email(body: str):
    sg = sendgrid.SendGridAPIClient(api_key=os.getenv("SENDGRID_API_KEY"))
    from_email = Email("sales@yourdomain.com")
    to_email = To("recipient@example.com")
    subject = "Let's talk about AI-powered learning!"
    content = Content("text/plain", body)
    mail = Mail(from_email, to_email, subject, content)
    response = sg.client.mail.send.post(request_body=mail.get())
    return response
message = "Write a cold sales email to a CEO about our EdTech platform."
results = await Runner.run(sales_agent, message)
print(results.final_output)
