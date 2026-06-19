# Full Scraping Pipeline - Scrape, Clean, Save

Author: Vishvi
Date: 2026-06-18

---

## Complete Reusable Pipeline

```python
import requests
from bs4 import BeautifulSoup
import pandas as pd
import time

def scrape_page(url, headers):
    response = requests.get(url, headers=headers)
    if response.status_code != 200:
        print('Failed to fetch:', url, 'Status:', response.status_code)
        return None
    return BeautifulSoup(response.text, 'html.parser')

def extract_items(soup, container_tag, container_class):
    items = soup.find_all(container_tag, class_=container_class)
    results = []
    for item in items:
        results.append({
            'text': item.text.strip(),
            'link': item.find('a').get('href') if item.find('a') else None
        })
    return results

def scrape_multiple_pages(base_url, num_pages, headers):
    all_data = []
    for page in range(1, num_pages + 1):
        url = base_url + '?page=' + str(page)
        print('Scraping page', page, '...')

        soup = scrape_page(url, headers)
        if soup:
            items = extract_items(soup, 'div', 'item')
            all_data.extend(items)

        time.sleep(2)  # be respectful - dont hammer the server

    return all_data

def save_to_csv(data, filename):
    df = pd.DataFrame(data)
    df = df.drop_duplicates()
    df.to_csv(filename, index=False)
    print('Saved', len(df), 'rows to', filename)
    return df

# Usage example (adjust selectors to your target site)
# headers = {'User-Agent': 'Mozilla/5.0'}
# data = scrape_multiple_pages('https://example.com/listings', 3, headers)
# df = save_to_csv(data, 'scraped_data.csv')
```

---

## Pipeline Summary

```
1. scrape_page()           -> fetch and parse one page
2. extract_items()         -> pull out the data you need
3. scrape_multiple_pages() -> loop through pages, with delays
4. save_to_csv()           -> clean and save the final dataset
```

This is the exact structure used in production scraping scripts.

---

Built by Vishvi - github.com/vishvi31
