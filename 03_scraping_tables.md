# Scraping Tables into Pandas DataFrames

Author: Vishvi
Date: 2026-06-18

---

## Method 1 - pandas.read_html (fastest way)

```python
import pandas as pd

# Automatically finds all HTML tables on a page
tables = pd.read_html('https://en.wikipedia.org/wiki/List_of_countries_by_population')

print('Number of tables found:', len(tables))
df = tables[0]
print(df.head())
```

This works great for clean Wikipedia-style tables.

---

## Method 2 - Manual extraction with BeautifulSoup

Use this when read_html does not work cleanly.

```python
import requests
from bs4 import BeautifulSoup
import pandas as pd

url = 'https://example.com/table-page'
headers = {'User-Agent': 'Mozilla/5.0'}
response = requests.get(url, headers=headers)
soup = BeautifulSoup(response.text, 'html.parser')

table = soup.find('table')
rows = table.find_all('tr')

# Get headers
headers_list = [th.text.strip() for th in rows[0].find_all('th')]

# Get data rows
data = []
for row in rows[1:]:
    cells = row.find_all('td')
    data.append([cell.text.strip() for cell in cells])

df = pd.DataFrame(data, columns=headers_list)
print(df.head())
```

---

## Cleaning Scraped Data

```python
# Scraped text often has extra whitespace and symbols
df['Population'] = df['Population'].str.replace(',', '')
df['Population'] = pd.to_numeric(df['Population'], errors='coerce')

df = df.dropna()
df = df.drop_duplicates()

print(df.dtypes)
print(df.describe())
```

---

Built by Vishvi - github.com/vishvi31
