# Beautiful Soup
Cheat sheet for Python's [Beautiful Soup library](https://www.crummy.com/software/BeautifulSoup/).

## Useful snippets 

### Find all a tags:

```python
soup.find_all('a')
```

### Find all a tags with an attribute:
```python
#Find all a tags with class "test".
soup.find_all('a', {'class':'test'})
```

### Find all by regex:
```python
# Find all elements that have "b" in them.
soup.find_all(re.compile('^b'))
```

### Find all by a validator function:
```python
#Find all tags that have class but not have alt
def validator(tag):
	return tag.has_attr('class') and not tag.has_attr('alt')

soup.find_all(validator)
```

### Find all by specific attribute:
```python
#Exact examples
soup.find_all(href='<url>')
soup.find_all(class_='<class_name>')
soup.find_all(text='<some_text>')

#Regex: Ending url with .com
soup.find_all(href=re.compile('^.com'))
```

