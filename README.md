# 🕵️ AI Fraud Detection with Prompt Engineering

This project demonstrates how to build a fraud detection system using **prompt engineering** with OpenAI's GPT models. Instead of traditional machine learning, it leverages language model reasoning through structured prompts and examples.

---

## 📌 Project Overview

We use a **Streamlit frontend** to allow users to input transaction details. The prompt is constructed with:
- A **system instruction** (role: financial fraud analyst)
- A few **example transactions**
- The **user's transaction input**

GPT-4 responds with:
- **Status**: Legitimate or Suspicious
- **Reason**: Explanation of the decision

---

## 📁 Files Included

| File | Description |
|------|-------------|
| `app.py` | Streamlit application that sends prompts to OpenAI |
| `requirements.txt` | Python dependencies |
| `.env` | Contains your OpenAI API key (not to be shared) |
| `README.md` | Detailed project documentation |

---

## 🧠 Prompt Design

### 🔹 System Prompt
```text
You are a financial fraud analyst. You are given financial transaction data. 
Your job is to detect suspicious activity based on patterns, such as:
- Unusual amount
- Irregular frequency
- Inconsistent location
- Fake merchant name

Respond only with:
- Status: [Legitimate | Suspicious]
- Reason: Explanation why
```

### 🔸 Few-Shot Examples
```text
Transaction: ID=TX001, Amount=120.50, Location=NY, Merchant=Starbucks
Status: Legitimate
Reason: Small regular purchase at a known coffee shop

Transaction: ID=TX002, Amount=5500.00, Location=KY, Merchant=ZZZ_Gaming_#19
Status: Suspicious
Reason: High-value transaction at an unknown gambling merchant in unusual location
```

### 📝 New Input
```text
Transaction: ID=TX999, Amount=4200.00, Location=LA, Merchant=XYZ_Casino
```

### ✅ Output
```text
Status: Suspicious
Reason: High-value transaction at risky merchant
```

---

## 🚀 How to Run

1. Clone the repository or unzip the project folder.
```bash
git clone https://github.com/yourusername/fraud-prompt-agent.git
cd fraud-prompt-agent
```

2. Install dependencies:
```bash
pip install -r requirements.txt
```

3. Create a `.env` file:
```
OPENAI_API_KEY=your-openai-api-key
```

4. Run the app:
```bash
streamlit run app.py
```

---

## 🧪 Testing

Try different transaction formats like:
```text
ID=TX200, Amount=10000.00, Location=VE, Merchant=Luxury_Watch_Dealer
```

---

## 🛠️ Dependencies

- Python 3.9+
- Streamlit
- OpenAI
- python-dotenv


---

## 💡 Future Improvements

- Add logging and result database
- Integrate user feedback loop
- Visual analytics dashboard
- Deployment on GCP, AWS, or Azure

