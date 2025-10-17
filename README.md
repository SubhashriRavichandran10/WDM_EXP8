### EX8 Web Scraping On E-commerce platform using BeautifulSoup
### DATE: 17.10.2025
## NAME:R.SUBHASHRI
## REG NO:212223230219
### AIM: To perform Web Scraping on Amazon using (beautifulsoup) Python.
### Description: 
<div align = "justify">
Web scraping is the process of extracting data from various websites and parsing it. In other words, it’s a technique 
to extract unstructured data and store that data either in a local file or in a database. 
There are many ways to collect data that involve a huge amount of hard work and consume a lot of time. Web scraping can save programmers many hours. Beautiful Soup is a Python web scraping library that allows us to parse and scrape HTML and XML pages. 
One can search, navigate, and modify data using a parser. It’s versatile and saves a lot of time.
<p>The basic steps involved in web scraping are:
<p>1) Loading the document (HTML content)
<p>2) Parsing the document
<p>3) Extraction
<p>4) Transformation

### Procedure:

1) Import necessary libraries (requests, BeautifulSoup, re, matplotlib.pyplot).
2) Define convert_price_to_float(price) Function: to Remove non-numeric characters from a price string and convert it to a float.
3) Define get_amazon_products(search_query) Function: to Scrape Amazon for product information based on the search query.
4) Fetch and parse the HTML content then Extract product names and prices from the search results and Sort product information based on converted prices in ascending order.
5) Return sorted product data as a list of dictionaries.
6) Call get_amazon_products(search_query) to get product data based on the user's search query.
7) Check if products are found; if not, display "No products found."
8) Visualize Product Data using a Bar Chart

### Program:
```PYTHON
import requests
from bs4 import BeautifulSoup
import time
search_query = input("Enter the product to search on Snapdeal: ").strip()
num_pages = 2  
base_url = "https://www.snapdeal.com/search"
headers = {"User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64)"}

product_list = []

for page in range(1, num_pages + 1):
    print(f"\nScraping page {page} for '{search_query}'...")
    params = {"keyword": search_query, "page": page}
    response = requests.get(base_url, params=params, headers=headers)
    soup = BeautifulSoup(response.text, "html.parser")

    products = soup.find_all("div", class_="product-tuple-listing")

    for product in products:
        title = product.find("p", class_="product-title").text.strip() if product.find("p", class_="product-title") else "N/A"
        price = product.find("span", class_="product-price").text.strip() if product.find("span", class_="product-price") else "N/A"
        discount = product.find("div", class_="product-discount").text.strip() if product.find("div", class_="product-discount") else "N/A"
        rating_tag = product.find("div", class_="filled-stars")
        if rating_tag:
            rating_style = rating_tag.get("style", "")
            try:
                percent = float(rating_style.replace("width:", "").replace("%", "").replace(";", "").strip())
                rating_value = round(percent / 20, 1)  
            except ValueError:
                rating_value = "N/A"
        else:
            rating_value = "N/A"

        product_list.append({
            "Title": title,
            "Price": price,
            "Discount": discount,
            "Rating": rating_value
        })
    
    time.sleep(1)
if not product_list:
    print("\nNo products found. Try another search term.")
else:
    print(f"\nFound {len(product_list)} products for '{search_query}'\n")
    
    for i, item in enumerate(product_list, 1):
        print(f"{i}. Title: {item['Title']}")
        print(f"   Price: {item['Price']}")
        print(f"   Discount: {item['Discount']}")
        print(f"   Rating: {item['Rating']}")
        print("-" * 60)
```

### Output:

<img width="741" height="442" alt="image" src="https://github.com/user-attachments/assets/85cb5393-8845-442d-8276-5ff083dfb2e9" />

<img width="736" height="513" alt="image" src="https://github.com/user-attachments/assets/4ea4041e-fab4-466e-9feb-658ec0c53df2" />

<img width="738" height="799" alt="image" src="https://github.com/user-attachments/assets/20905b9d-451e-48ab-a63c-1c1687352bf7" />



<img width="738" height="832" alt="image" src="https://github.com/user-attachments/assets/9cded134-e8b1-454e-9544-da121a729d25" />




### Result:

Web Scraping using (beautifulsoup) Python is implemented successfully.
