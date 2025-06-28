book-price-tracker
# Book Price Tracker

This Python script tracks the price of a specific book listed on [BooksToScrape](https://books.toscrape.com) and sends an email notification with the current price every hour. It is a simple automation project using web scraping and email services.

## Features

- Scrapes the current price of a book in GBP
- Converts the price from GBP to INR
- Sends an email alert with the price and product link
- Automatically checks the price every hour

## Technologies Used

- Python
- requests
- BeautifulSoup
- smtplib and email.mime
- time and re

## How to Use

### 1. Clone the repository

```bash
git clone https://github.com/rohanyadav-05/book-price-tracker.git
cd book-price-tracker
2. Install the required libraries
bash
Copy
Edit
pip install requests beautifulsoup4
3. Update email credentials
Open price_tracker.py and update the following:

python
Copy
Edit
from_email = "your_email@gmail.com"
from_password = "your_app_password"
to_email = "recipient_email@gmail.com"
Note: If you're using Gmail, generate an App Password and use it instead of your actual password.

4. Run the script
bash
Copy
Edit
python price_tracker.py
The script will run continuously and send an email with the current price every hour.

Sample Book Tracked
A Light in the Attic: https://books.toscrape.com/catalogue/a-light-in-the-attic_1000/index.html

Security Tip
Avoid committing your email credentials directly in public repositories. Consider using a .env file or environment variables for sensitive data in production.

License
This project is licensed under the MIT License.
