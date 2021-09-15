Abramov Dmitry
================

### Contact information: ### 
E-mail: abrannik25@gmail.com

Phone: +375(25)693-30-85

Telegram: @de4lt_dd

### Briefly About Myself: ### 
I study at the BSU at the Faculty of Radiophysics. Since high school, I have always been close to subjects such as physics and mathematics. That is why, when looking for a direction after graduation, the choice fell on a faculty with a technical specialty.
  
Apart from physics and mathematics, my specialty is related to programming. This area interested me. In addition, in the modern world, it is one of the most popular. So I decided to learn a programming language like C #. However, after completing the courses from EPAM, I realized that I wanted something different.
After communicating with people from different fields, studying various programming languages, I decided to try myself as Frontend Developer.
  
I am ready to spend my free time learning something new and I believe that the field of programming, like no other, allows you to pump yourself and your skills. 

### My strengths: ### 
- flexibility 
- responsibility
- purposefulness 

### Skills and Prificiency: ### 
- HTML5, CSS3
- Git, GitHub
- VS Code, VS
- Adobe Photoshop
- JavaScript

### Code Example: ### 
Example Python code (Parser from my course project):
```python
import requests
from bs4 import BeautifulSoup
import csv

CSV = 'cards.csv'
HOST = 'https://mcdonalds.by/ru/'
URL = 'https://mcdonalds.by/ru/news.html'
HEADERS = {'accept': 'text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9',
    'user-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/90.0.4430.93 Safari/537.36'}


def get_html(url, params=''):
    r = requests.get(url, headers=HEADERS, params=params)
    return r


def get_content(html):
    soup = BeautifulSoup(html, 'html.parser')
    items = soup.find_all('div', class_='row mc-news-all-blocks-holder')
    cards = []
    # print(items)
    for item in items:
        cards.append(
            {
                'title': item.find('div', class_='col-lg-12 col-md-12 col-sm-12 col-xs-12').get_text(strip=True),
                'link_product': item.find('div', class_='mc-news-all-img-holder').find('a').get('href')
            }
            )
    return cards


def save_doc(items, path):
    with open(path, 'w', newline='') as file:
        writer = csv.writer(file, delimiter=';')
        writer.writerow(['Название продукта: ', 'Ссылка: '])
        for item in items:
            writer.writerow([item['title'], item['link_product']])


def parser():
    PAGE = input('Количество страниц: ')
    PAGE = int(PAGE.strip())
    html = get_html(URL)
    if html.status_code == 200:
        cards = []
        for page in range(1, PAGE):
            print(f'Парсим страницу: {page}')
            html = get_html(URL, params={'page': page})
            cards.extend(get_content(html.text))
            save_doc(cards, CSV)
    else:
        print('Error')

parser()
```
