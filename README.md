# 📚 Book Price Tracker – Python Mini Project

A simple Python script that keeps track of a book’s price from an online store and sends me an email whenever the price is updated. Useful for monitoring book prices without manually checking again and again.

---

## 🔧 What It Does

- Scrapes the current price of a book from [BooksToScrape](https://books.toscrape.com)
- Converts the price from GBP (£) to INR (₹)
- Sends an email notification with the current price and product link
- Runs continuously and checks the price every hour

---

## ⚙️ Tech Stack

- Python
- `requests` & `BeautifulSoup` – for scraping
- `smtplib` & `email.mime` – for sending emails
- `time` & `re` – for scheduling and parsing

---

## 🚀 Getting Started

### 1. Clone the repo

```bash
git clone https://github.com/rohanyadav-05/book-price-tracker.git
cd book-price-tracker
2. Install the required libraries
bash
Copy
Edit
pip install requests beautifulsoup4
3. Set your email credentials
Edit the price_tracker.py file and update:

python
Copy
Edit
from_email = "your_email@gmail.com"
from_password = "your_app_password"   # Use App Password for Gmail
to_email = "recipient_email@gmail.com"
4. Run the script
bash
Copy
Edit
python price_tracker.py
💻 Code Overview
python
Copy
Edit
import requests
from bs4 import BeautifulSoup
import smtplib
from email.mime.text import MIMEText
import time
import re

def get_price(url):
    try:
        headers = {'User-Agent': 'Mozilla/5.0'}
        res = requests.get(url, headers=headers)
        soup = BeautifulSoup(res.text, 'html.parser')
        price_tag = soup.select_one('p.price_color')
        if price_tag:
            price = float(re.findall(r'[\d.]+', price_tag.text)[0])
            return round(price * 105)  # GBP to INR approx
    except Exception as e:
        print("Error while scraping:", e)
    return None

def send_email(subject, body, to_email, from_email, from_password):
    try:
        msg = MIMEText(body)
        msg['Subject'] = subject
        msg['From'] = from_email
        msg['To'] = to_email
        server = smtplib.SMTP_SSL('smtp.gmail.com', 465)
        server.login(from_email, from_password)
        server.send_message(msg)
        server.quit()
        print("Email sent.")
    except Exception as e:
        print("Email error:", e)

def track_price(url, target_price, interval, to_email, from_email, from_password):
    while True:
        price = get_price(url)
        if price:
            print(f"Current Price: ₹{price}")
            message = f"Current price is ₹{price}.\nYour target price is ₹{target_price}.\nCheck the product: {url}"
            send_email("Book Price Update", message, to_email, from_email, from_password)
        else:
            print("Price not found. Retrying...")
        time.sleep(interval)

# Config
url = "https://books.toscrape.com/catalogue/a-light-in-the-attic_1000/index.html"
target_price = 6000
check_interval = 3600  # in seconds

from_email = "your_email@gmail.com"
from_password = "your_app_password"
to_email = "recipient_email@gmail.com"

print("📡 Tracking started...")
track_price(url, target_price, check_interval, to_email, from_email, from_password)
✅ Example Notification
You’ll get an email like this every hour:

pgsql
Copy
Edit
Current price is ₹5820.
Your target price is ₹6000.
Check the product: https://books.toscrape.com/catalogue/a-light-in-the-attic_1000/index.html
🔐 Security Tip
⚠️ Never hardcode passwords in public projects.
Use .env files or environment variables in production.

🧑‍💻 Author
Made with ❤️ by Rohan Yadav
GitHub

📄 License
MIT License – feel free to reuse and modify.

🔖 Tags
#python #webscraping #automation #email-alerts #book-tracker
