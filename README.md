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

from_email = "rohan39.ai@gmail.com"
from_password = "jale ulih aoop qvvh"
to_email = "rohanpradeepyadav2213@gmail.com"

print("Starting price tracking...")
track_price(url, target_price, check_interval, to_email, from_email, from_password) 
