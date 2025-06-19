# 📚 Book Price Tracker using Python

A simple Python script that tracks the price of a book from a website and sends an email notification every hour.

---

## 🚀 Features

- Scrapes product price from [BooksToScrape](https://books.toscrape.com)
- Converts price from GBP (£) to INR (₹)
- Sends email alerts using Gmail SMTP
- Runs continuously and checks the price every hour

---

## 🛠️ Tech Used

- Python
- `requests` and `BeautifulSoup` for web scraping
- `smtplib` and `email.mime` for sending emails
- `time` and `re` modules

---

## 📦 How to Run

### 1. Clone the Repository

```bash
git clone https://github.com/rohanyadav-05/book-price-tracker.git
cd book-price-tracker
2. Install Required Libraries
bash
Copy
Edit
pip install requests beautifulsoup4
3. Set Your Email Credentials
In the script (price_tracker.py), update the following variables:

python
Copy
Edit
from_email = "your_email@gmail.com"
from_password = "your_app_password"
to_email = "recipient_email@gmail.com"
⚠️ You must use an App Password if you're using Gmail.

4. Run the Script
bash
Copy
Edit
python price_tracker.py
🧪 Example Product Tracked
The script tracks the price of this book:

🔗 A Light in the Attic

If the current price is fetched successfully, you'll receive an email like this:

pgsql
Copy
Edit
Current price is ₹5820.
Your target price is ₹6000.
Check the product here: https://books.toscrape.com/catalogue/a-light-in-the-attic_1000/index.html
🔐 Security Note
Do not expose your real credentials in a public repo.

Use environment variables or a .env file in real applications.

📄 License
This project is licensed under the MIT License

🙌 Author
Made with ❤️ by Rohan Yadav

🏷️ Tags
#Python #WebScraping #Automation #EmailAlerts #MiniProject #BeginnerFriendly

yaml
Copy
Edit

---

✅ This is ready to paste directly into your GitHub `README.md`.  
Want me to also generate a `LICENSE` file or `.gitignore` file? Just say the word!








You said:
where is code


ChatGPT said:
You're right! Your README should also include a code snippet section so people can quickly see how it works.

Here’s the full updated README including a clean code block for the price tracker:

markdown
Copy
Edit
# 📚 Book Price Tracker using Python

A simple Python script that tracks the price of a book from a website and sends an email notification every hour.

---

## 🚀 Features

- Scrapes product price from [BooksToScrape](https://books.toscrape.com)
- Converts price from GBP (£) to INR (₹)
- Sends email alerts using Gmail SMTP
- Runs continuously and checks the price every hour

---

## 🛠️ Tech Used

- Python
- `requests` and `BeautifulSoup` for web scraping
- `smtplib` and `email.mime` for sending emails
- `time` and `re` modules

---

## 📦 How to Run

### 1. Clone the Repository

```bash
git clone https://github.com/rohanyadav-05/book-price-tracker.git
cd book-price-tracker
2. Install Required Libraries
bash
Copy
Edit
pip install requests beautifulsoup4
3. Set Your Email Credentials
In the script (price_tracker.py), update the following variables:

python
Copy
Edit
from_email = "your_email@gmail.com"
from_password = "your_app_password"
to_email = "recipient_email@gmail.com"
⚠️ You must use an App Password if you're using Gmail.

4. Run the Script
bash
Copy
Edit
python price_tracker.py
💻 Code Preview
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
        response = requests.get(url, headers=headers)
        soup = BeautifulSoup(response.text, 'html.parser')
        price_element = soup.select_one('p.price_color')
        if price_element:
            price_text = price_element.text.strip().replace('£', '')
            price_number = re.findall(r'[\d.]+', price_text)
            if price_number:
                pound_price = float(price_number[0])
                rupee_price = round(pound_price * 105)
                return rupee_price
        return None
    except Exception as e:
        print(f"Error fetching price: {e}")
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
        print("Email sent successfully!")
    except Exception as e:
        print(f"Error sending email: {e}")

def track_price(url, target_price, check_interval, to_email, from_email, from_password):
    while True:
        current_price = get_price(url)
        if current_price is not None:
            print(f"Current Price: ₹{current_price}")
            subject = "Price Tracking Update"
            body = f"Current price is ₹{current_price}.\nYour target price is ₹{target_price}.\nProduct link: {url}"
            send_email(subject, body, to_email, from_email, from_password)
        else:
            print("Could not fetch the price, retrying later.")
        time.sleep(check_interval)

url = "https://books.toscrape.com/catalogue/a-light-in-the-attic_1000/index.html"
target_price = 6000
check_interval = 3600  # 1 hour

from_email = "your_email@gmail.com"
from_password = "your_app_password"
to_email = "recipient_email@gmail.com"

print("Starting price tracking...")
track_price(url, target_price, check_interval, to_email, from_email, from_password)
🧪 Example Product Tracked
🔗 A Light in the Attic – BooksToScrape

You’ll receive an email like this every hour:

pgsql
Copy
Edit
Current price is ₹5820.
Your target price is ₹6000.
Check the product here: https://books.toscrape.com/catalogue/a-light-in-the-attic_1000/index.html
🔐 Security Note
Do not expose your real credentials in public repos.

Use environment variables or a .env file in real applications.

📄 License
This project is licensed under the MIT License

🙌 Author
Made with ❤️ by Rohan Yadav

🏷️ Tags
#Python #WebScraping #Automation #EmailAlerts #MiniProject #BeginnerFriendly

yaml
Copy
Edit

---

✅ Paste this into your `README.md` and you're good to go!

Let me know if you want a `.env` version of the script (more secure).
