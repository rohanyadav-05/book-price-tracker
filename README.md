# 📚 Book Price Tracker using Python

A simple Python project that tracks the price of a product from an e-commerce website and sends an email notification when the price updates.

---

## 🚀 Features

- Scrapes the product price from a demo e-commerce site: [BooksToScrape](https://books.toscrape.com)
- Converts price from GBP (£) to INR (₹)
- Sends email alerts using Gmail SMTP
- Automatically checks the price every hour

---

## 🔧 Technologies Used

- Python
- Requests + BeautifulSoup (for web scraping)
- smtplib (for sending email)
- Regular expressions (to extract price)

---

## 📦 How to Run

### 1. Clone the Repository

```bash
git clone https://github.com/rohanyadav-05/book-price-tracker.git
cd book-price-tracker
