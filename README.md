# Jonathanguan
import requests
from bs4 import BeautifulSoup
import random
import webbrowser

#URL important
def scrapeWikiArticle(url):
    response = requests.get(
        url=url)

    soup = BeautifulSoup(response.content, 'html.parser')

    title = soup.find(id="firstHeading")
    print(title.text)

    allLinks = soup.find(id="bodyContent").find_all("a")
    random.shuffle(allLinks)
    linkToScrape = 0

#href= hypertext reference
    for link in allLinks:

        if link['href'].find("/wiki/") == -1:
            continue

        # Use this link to scrape
        linkToScrape = link
        break

    scrapeWikiArticle("https://en.wikipedia.org" + linkToScrape['href'])

try:
    scrapeWikiArticle("https://en.wikipedia.org/wiki/Special:Random")
except:
    pass #goes pass error

webbrowser.open_new_tab("https://en.wikipedia.org/wiki/Special:Random")
# open ("https://en.wikipedia.org/wiki/Special:Random")
