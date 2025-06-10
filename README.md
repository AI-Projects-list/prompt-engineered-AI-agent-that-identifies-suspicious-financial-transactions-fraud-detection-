### 📁 Project: Prompt Engineering for Fraud Detection AI Agent Identifies Suspicious Financial Transactions

# 🧠 Description:
# This project builds a prompt-engineered AI agent that identifies suspicious financial transactions (fraud detection) using GPT-4 via OpenAI API.
# It includes few-shot prompting and role-based instructions. A Streamlit interface allows user input and output visualization.

## 🔧 Requirements
# - Python 3.9+
# - streamlit
# - openai
# - dotenv

## 📦 Installation
# pip install -r requirements.txt

## .env File
# Create a .env file with:
# OPENAI_API_KEY=your-api-key-here

# project/app.py
import os
import openai
import streamlit as st
from dotenv import load_dotenv

load_dotenv()
openai.api_key = os.getenv("OPENAI_API_KEY")

SYSTEM_PROMPT = """
You are a financial fraud analyst. You are given financial transaction data. 
Your job is to detect suspicious activity based on patterns, such as:
- Unusual amount
- Irregular frequency
- Inconsistent location
- Fake merchant name

Respond only with:
- Status: [Legitimate | Suspicious]
- Reason: Explanation why
"""

FEW_SHOT_EXAMPLES = """
Transaction: ID=TX001, Amount=120.50, Location=NY, Merchant=Starbucks
Status: Legitimate
Reason: Small regular purchase at a known coffee shop

Transaction: ID=TX002, Amount=5500.00, Location=KY, Merchant=ZZZ_Gaming_#19
Status: Suspicious
Reason: High-value transaction at an unknown gambling merchant in unusual location
"""

def analyze_transaction(user_transaction: str):
    prompt = SYSTEM_PROMPT + "\n" + FEW_SHOT_EXAMPLES + "\nTransaction: " + user_transaction
    response = openai.ChatCompletion.create(
        model="gpt-4",
        messages=[
            {"role": "system", "content": SYSTEM_PROMPT},
            {"role": "user", "content": prompt}
        ]
    )
    return response['choices'][0]['message']['content']

st.title("🕵️ Fraud Detection via Prompt Engineering")

transaction_input = st.text_input("Enter transaction details:", "ID=TX999, Amount=4200.00, Location=LA, Merchant=XYZ_Casino")

if st.button("Analyze Transaction"):
    result = analyze_transaction(transaction_input)
    st.markdown("### 🧾 Result")
    st.code(result)

# 📄 requirements.txt
# streamlit
# openai
# python-dotenv

# 📁 .env
# OPENAI_API_KEY=your-api-key

# 📘 README.md
"""
# 🕵️ AI Fraud Detection (Prompt Engineering Project)

This project uses prompt engineering to identify suspicious transactions using GPT-4.

## Features
- Role-based prompt engineering
- Few-shot examples
- Streamlit frontend
- Uses OpenAI API

## How to Run
```bash
git clone https://github.com/yourusername/fraud-prompt-agent.git
cd fraud-prompt-agent
pip install -r requirements.txt
echo "OPENAI_API_KEY=your-api-key" > .env
streamlit run app.py
```

## Prompt Structure
```text
SYSTEM_PROMPT: AI is a fraud analyst.
EXAMPLES: Legitimate vs. Suspicious patterns
INPUT: New transaction detail
OUTPUT: Fraud status and reason
```

## Example Input
```text
ID=TX999, Amount=4200.00, Location=LA, Merchant=XYZ_Casino
```

## Output
```text
Status: Suspicious
Reason: High-value transaction at risky merchant
```

## License
MIT
"""
