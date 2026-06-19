# Requests and BeautifulSoup Fundamentals

Author: Vishvi
Date: 2026-06-18

---

## Setup

```python
# pip install requests beautifulsoup4 --break-system-packages

import requests
from bs4 import BeautifulSoup
```

---

## Step 1 - Fetch a Webpage

```python
url = 'https://example.com'
headers = {'User-Agent': 'Mozilla/5.0'}

response = requests.get(url, headers=headers)
print('Status code:', response.status_code)
print('Content length:', len(response.text))
```

Status code 200 means success. 403 or 404 means blocked
or not found.

---

## Step 2 - Parse with BeautifulSoup

```python
soup = BeautifulSoup(response.text, 'html.parser')

# Pretty print the structure
print(soup.prettify()[:500])
```

---

## Step 3 - Finding Elements

```python
# find() gets the FIRST match
title = soup.find('h1')
print(title.text)

# find_all() gets ALL matches
all_links = soup.find_all('a')
print('Total links found:', len(all_links))

# Find by class
products = soup.find_all('div', class_='product')

# Find by id
header = soup.find(id='main-header')

# Using CSS selectors
items = soup.select('div.product')
prices = soup.select('span.price')
```

---

## Step 4 - Extracting Data

```python
for link in soup.find_all('a')[:5]:
    text = link.text.strip()
    href = link.get('href')
    print(text, '->', href)
```

---

## Common Mistakes

1. Forgetting headers - many sites block requests without a User-Agent
2. Not checking status_code before parsing
3. Scraping too fast - always add time.sleep() between requests
4. Assuming page structure never changes - it does, code breaks

---

Built by Vishvi - github.com/vishvi31
