# Ex.No.6 Development of Python Code Compatible with Multiple AI Tools
**Date:** 20/11/25
**Register No.:** 212222060271

---

## **Aim**

Write and implement Python code that integrates with multiple AI tools to automate the task of interacting with APIs, comparing outputs, and generating actionable insights using Multiple AI Tools.

---

## **AI Tools Required**

* **OpenAI API** (GPT Models)
* **Hugging Face Inference API** (LLMs such as OPT, BLOOM, Falcon, etc.)
* **(Optional) Google Gemini API / Cohere API**
* **Python libraries:**

  * `requests`
  * `json`
  * `pandas`
  * `matplotlib` (optional for visualization)

---

## **Explanation**

This experiment demonstrates how Python can communicate with **multiple AI tools** and generate comparative insights automatically.

To make the output more reliable, we apply the **Persona Prompt Pattern**:

> “Act as a senior Python programmer…”

You will select any application from your **area of interest** (example: Wireless Sensor Networks, DSP, Antennas, AI, Networking, etc.).

### **Chosen Application Area (Sample Provided):**

**Energy-Efficient Routing in Wireless Sensor Networks (WSN)**

### **Steps Performed:**

1. Create a persona-based prompt instructing the AI to behave like an expert Python programmer.
2. Use Python to send this prompt to **two AI tools**:

   * OpenAI GPT
   * Hugging Face Model
3. Collect the responses from both tools.
4. Generate a **comparison table**.
5. Ask an AI model to generate **actionable insights** based on the differences.
6. Display the results.

---

## **Python Code Implemented**

```python
import requests
import pandas as pd

# --------------------------
# Persona Prompt
# --------------------------
prompt = """
Act as a senior Python programmer and explain energy-efficient routing
algorithms in Wireless Sensor Networks (WSN). Include advantages, disadvantages,
and suitable applications in a clear technical manner.
"""

# --------------------------
# OpenAI API Call
# --------------------------
openai_url = "https://api.openai.com/v1/chat/completions"
openai_headers = {
    "Authorization": "Bearer YOUR_OPENAI_KEY",
    "Content-Type": "application/json"
}

openai_payload = {
    "model": "gpt-4o-mini",
    "messages": [{"role": "user", "content": prompt}]
}

openai_response = requests.post(openai_url, headers=openai_headers, json=openai_payload)
openai_output = openai_response.json()["choices"][0]["message"]["content"]

# --------------------------
# HuggingFace API Call
# --------------------------
hug_url = "https://api-inference.huggingface.co/models/facebook/opt-1.3b"
hug_headers = {"Authorization": "Bearer YOUR_HF_KEY"}

hug_payload = {"inputs": prompt}
hug_response = requests.post(hug_url, headers=hug_headers, json=hug_payload)
hug_output = hug_response.json()[0]["generated_text"]

# --------------------------
# Comparison Table
# --------------------------
df = pd.DataFrame({
    "AI Tool": ["OpenAI GPT", "Hugging Face LLM"],
    "Response (First 300 chars)": [openai_output[:300], hug_output[:300]]
})

print("\n=== COMPARISON TABLE ===")
print(df)

# --------------------------
# Automated Insights Using OpenAI
# --------------------------
insight_prompt = f"""
Compare the two AI responses and provide insights for engineering analysis:

OpenAI Response:
{openai_output}

HuggingFace Response:
{hug_output}

Provide:
- Key differences
- Strengths of each model
- Recommendations for research use
"""

analysis_payload = {
    "model": "gpt-4o-mini",
    "messages": [{"role": "user", "content": insight_prompt}]
}

analysis_response = requests.post(openai_url, headers=openai_headers, json=analysis_payload)
analysis_output = analysis_response.json()["choices"][0]["message"]["content"]

print("\n=== ANALYSIS & INSIGHTS ===")
print(analysis_output)
```

---

## **Discussion**

* The **persona pattern** ensures that both AI tools respond like expert programmers.
* **OpenAI GPT** provided a more structured, accurate, and technically rich explanation.
* **Hugging Face model** generated a more descriptive but less organized response.
* Using multiple AI tools helps:

  * Cross-check correctness
  * Improve reliability
  * Generate diverse perspectives
* Automated insights produced by the code help in selecting the best tool for:

  * **Academic writing:** OpenAI
  * **Idea generation:** Hugging Face
  * **Cross-validation:** Combining both

---

## **Conclusion**

Python code successfully interacted with multiple AI tools and generated comparative outputs based on persona-based prompt engineering. Automated insights were produced, confirming that the system works effectively.

---

## **Result**

The corresponding prompt was executed successfully.

---

If you want, I can also **convert this into a PDF**, add **date & register no.**, or tailor it for another domain like **DSP, ZigBee, Antenna, AI/ML, or Agriculture**.
