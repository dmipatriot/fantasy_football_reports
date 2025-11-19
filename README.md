# Survivor Pool / ESPN API Notebook

A Python/Colab project that pulls ESPN Fantasy Football data and runs a **Survivor Pool elimination system** starting Week 3. This project is built to run safely in **Google Colab**, with clean separation between code and secrets, and supports future automation on platforms like **Render**.

---

## 🚀 Features

- Pull ESPN fantasy league data using **SWID** and **ESPN_S2** tokens  
- Automatically calculate weekly scores  
- Determine lowest-scoring team each week (beginning Week 3)  
- Produce a clean elimination report  
- Designed for **manual weekly runs** in Google Colab  
- **Secrets stored safely** (never in GitHub or notebook)

---

## 🔐 Managing ESPN Credentials (SWID & ESPN_S2)

### ✅ 1. Google Colab (Recommended for Manual Running)

Google Colab provides a built-in **Secrets Manager** that keeps your login tokens private and out of the notebook.

### **Add Your Secrets**

In Colab:
Runtime → Secrets → Add new secret
Add:
- ESPN_S2
- SWID

### **Load Secrets in Your Notebook**
python
from google.colab import userdata

ESPN_S2 = userdata.get("ESPN_S2")
SWID = userdata.get("SWID")

if not ESPN_S2 or not SWID:
    raise ValueError("Missing ESPN credentials. Add them in Runtime → Secrets.")


✔ Tokens stay private
✔ Never stored in .ipynb
✔ Never pushed to GitHub
✔ Persist across sessions

✅ 2. Render.com (For Future Automation)

If you deploy this as a cron job or automated worker:

Add environment variables in Render:
ESPN_S2 = your_cookie_value
SWID = your_swid_value

Load them in your code:
import os

ESPN_S2 = os.environ["ESPN_S2"]
SWID = os.environ["SWID"]

❌ What NOT to do

Do NOT hardcode tokens into any notebook

Do NOT commit secrets to GitHub

Do NOT store unencrypted tokens in Drive

Do NOT upload .env files to the repo

Your SWID and ESPN_S2 act like login keys. Protect them.

🗂 Recommended Repo Structure
survivor-pool/
│
├── notebooks/
│   └── survivor_pool.ipynb
│
├── src/
│   ├── espn_client.py
│   ├── survivor_logic.py
│   └── utils.py
│
├── README.md
└── requirements.txt


Keeping logic in src/ gives better reuse and prevents bloated notebooks.

▶️ Running the Notebook

Open the notebook directly from GitHub in Colab:
File → Open Notebook → GitHub

Add secrets once:
Runtime → Secrets

Run all cells.

View the generated elimination report.

📦 Dependencies
espn_api
python-dotenv
pandas


Include these in requirements.txt if needed.

🔧 Optional: Local .env for Local Runs

If you run this notebook or scripts locally:

Create a .env file (never commit it):

ESPN_S2=xxxx
SWID=xxxx


Load it:

from dotenv import load_dotenv
import os

load_dotenv()

📝 Future Enhancements

Auto-post results to Slack/Discord

Weekly side-pot automation

AI-generated trash-talk / roast summaries

Dynamic scoring logic

Multi-league support

👍 Summary

Using Colab Secrets + Render environment variables keeps your credentials secure, private, and completely out of GitHub.
This setup gives you clean separation between code and secrets and supports future automation without rewrites.

