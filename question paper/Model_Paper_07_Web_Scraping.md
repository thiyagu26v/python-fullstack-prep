# Python Coding Round - Model Paper 07
## Topic: Web Scraping & Data Extraction
### Duration: 45 Minutes | Total Marks: 50 | Fresher Level - Full Stack Role

---

## Question 1: Extract Links (5 Marks)
Write a function that extracts all links from HTML string.

**Input:**
```
html = '<a href="https://example.com">Link 1</a><a href="https://test.com">Link 2</a>'
extract_links(html)
```

**Output:**
```
["https://example.com", "https://test.com"]
```

---

## Question 2: Extract Paragraphs (5 Marks)
Write a function that extracts all paragraph text from HTML.

**Input:**
```
html = '<p>First paragraph</p><div>Not this</div><p>Second paragraph</p>'
extract_paragraphs(html)
```

**Output:**
```
["First paragraph", "Second paragraph"]
```

---

## Question 3: Parse HTML Table (5 Marks)
Write a function that converts HTML table to list of dictionaries.

**Input:**
```
html = '<table><tr><th>Name</th><th>Age</th></tr><tr><td>John</td><td>25</td></tr></table>'
parse_table(html)
```

**Output:**
```
[{"Name": "John", "Age": "25"}]
```

---

## Question 4: CSS Selector Extraction (5 Marks)
Write a function that extracts elements using CSS selectors.

**Input:**
```
html = '<div class="product"><span class="price">$100</span></div>'
extract_by_selector(html, ".product .price")
```

**Output:**
```
["$100"]
```

---

## Question 5: Extract Images (5 Marks)
Write a function that extracts all image src and alt attributes.

**Input:**
```
html = '<img src="cat.jpg" alt="Cat"><img src="dog.jpg" alt="Dog">'
extract_images(html)
```

**Output:**
```
[{"src": "cat.jpg", "alt": "Cat"}, {"src": "dog.jpg", "alt": "Dog"}]
```

---

## Question 6: HTML to Text (5 Marks)
Write a function that converts HTML to clean text, removing tags and extra spaces.

**Input:**
```
html = '<div><p>Hello   <b>World</b></p>\n\n<p>Test</p></div>'
html_to_text(html)
```

**Output:**
```
"Hello World Test"
```

---

## Question 7: Extract Meta Tags (5 Marks)
Write a function that extracts meta tag information (title, description, keywords).

**Input:**
```
html = '<head><title>My Page</title><meta name="description" content="A sample page"></head>'
extract_meta(html)
```

**Output:**
```
{"title": "My Page", "description": "A sample page", "keywords": ""}
```

---

## Question 8: Extract Form Fields (5 Marks)
Write a function that extracts all form input fields with names and types.

**Input:**
```
html = '<form><input type="text" name="username"><input type="email" name="email"></form>'
extract_form_fields(html)
```

**Output:**
```
[{"name": "username", "type": "text"}, {"name": "email", "type": "email"}]
```

---

## Question 9: Build Absolute URLs (5 Marks)
Write a function that converts relative URLs to absolute URLs.

**Input:**
```
base_url = "https://example.com/page/"
relative_urls = ["/about", "contact", "../home"]
make_absolute(base_url, relative_urls)
```

**Output:**
```
["https://example.com/about", "https://example.com/page/contact", "https://example.com/home"]
```

---

## Question 10: Rate Limiter (5 Marks)
Create a rate limiter class for web scraping to avoid overloading servers.

**Input:**
```
limiter = RateLimiter(requests_per_second=2)
limiter.wait()  # Ensures 0.5s gap between requests
```

**Output:**
```
# Waits appropriate time before allowing next request
```

---

## Evaluation Criteria:
- Code correctness: 50%
- HTML parsing skills: 30%
- Code readability: 20%
