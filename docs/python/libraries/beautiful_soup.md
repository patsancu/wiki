### Extract pdfs from website links
```python
def _get_links_from_url(url):
    # Read html from website
    html = urllib2.urlopen(url).read()
    sopa = BeautifulSoup(html)

    pdf_links = (
            extract_pdf_link(url, element)
            for element in sopa.find_all("a")
            )
    return pdf_links


def extract_pdf_link(url, raw_link):
    current_link = raw_link.get('href')
    if _is_pdf_file(current_link):
        prefix = ""
        if not current_link.startswith("http"):
            prefix = url
        pdf_url = prefix + current_link
        return pdf_url
    return ""
```
