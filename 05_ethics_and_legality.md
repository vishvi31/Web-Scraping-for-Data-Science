# Ethics and Legality of Web Scraping

Author: Vishvi
Date: 2026-06-18

---

## Always Check robots.txt First

Every website has a robots.txt file that states what
is allowed to be scraped.

```
Check: https://example.com/robots.txt
```

```python
import requests

response = requests.get('https://example.com/robots.txt')
print(response.text)
```

Look for 'Disallow' rules - these tell you what NOT to scrape.

---

## Golden Rules of Ethical Scraping

1. Check robots.txt before scraping any site
2. Add delays between requests using time.sleep()
3. Never scrape personal or private data without consent
4. Identify yourself with a proper User-Agent header
5. Prefer official APIs when they exist over scraping
6. Do not overload a server with rapid requests
7. Respect copyright - scraped data is not automatically yours to redistribute
8. Read the website Terms of Service before scraping commercially

---

## Rate Limiting Example

```python
import time
import random

def polite_scrape(urls):
    for url in urls:
        # your scraping code here
        print('Scraping:', url)

        # random delay between 1 to 3 seconds
        delay = random.uniform(1, 3)
        time.sleep(delay)
```

---

## When NOT to Scrape

- Sites that explicitly disallow it in robots.txt
- Sites requiring login without permission
- Personal data without consent (GDPR concerns)
- Sites offering a free official API instead

---

## Why This Matters for Your Career

Recruiters and interviewers WILL ask about ethics if you
mention web scraping on your resume. Showing you understand
the responsible side of data collection sets you apart.

---

Built by Vishvi - github.com/vishvi31
