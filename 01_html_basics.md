# HTML Basics for Web Scraping

Author: Vishvi
Date: 2026-06-18

---

## Why Learn HTML for Scraping?

Every webpage is built from HTML tags. To scrape data,
you need to know which tags hold the information you want.

---

## Key Tags to Know

| Tag | What it usually holds |
|---|---|
| `<div>` | A container/section |
| `<span>` | Small inline text |
| `<p>` | Paragraph text |
| `<h1> to <h6>` | Headings |
| `<a href>` | Links |
| `<table>` | Tabular data |
| `<tr>` | Table row |
| `<td>` | Table cell |
| `<ul>` `<li>` | Lists |
| `<img src>` | Images |

---

## Example HTML Structure

```html
<div class='product'>
    <h2 class='product-name'>Wireless Mouse</h2>
    <span class='price'>Rs 599</span>
    <p class='rating'>4.3 out of 5</p>
</div>
```

To scrape this, you would target:
- class='product-name' for the name
- class='price' for the price
- class='rating' for the rating

---

## How to Inspect a Webpage

1. Right click on any element on a webpage
2. Click 'Inspect' or 'Inspect Element'
3. The HTML panel shows you the exact tag and class
4. Use that tag/class in your scraping code

This is the single most useful skill before writing
any scraping code - always inspect first.

---

## CSS Selectors Cheat Sheet

| Selector | Meaning |
|---|---|
| `div` | All div tags |
| `.classname` | All elements with that class |
| `#idname` | Element with that specific id |
| `div.product` | div tags with class product |
| `div > p` | p tags that are direct children of div |

---

Built by Vishvi - github.com/vishvi31
