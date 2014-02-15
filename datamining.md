#«Web Scraping 101»

---
#Présentation

	!python
	from Quebec import Akim Couture

---

#Définir «Web Scraping» ?

>Le Web scraping (parfois appelé Harvesting) est une technique d'extraction du contenu de sites Web, via un script ou un programme, dans le but de le transformer pour permettre son utilisation dans un autre contexte.

---

![Scrapy](Scrapy_logo.jpg)

---

###Pourquoi l'utiliser ?

*	100% Python !
*	Un des plus populaires donc grosse communauté
*	Un environnement pour crée plusieurs «spiders»


---

#Installation

Dépendences :
----------
*	Python 2.7
*	lxml
*	OpenSSL
*	pip or easy_install
 
---
	!bash
	mkdir scraping
	virtualenv venv
	source venv/bin/activate
	pip install Scrapy
	
Enjoy !

Windows : scrapy docs (vous devez installer toutes les dépences manuellement)

Ubuntu : N'utilisez pas python-scrapy trop vieux !

---

#Comment ça marche ?

![](scrapy_architecture.png)

---
#HN Scraping

	!bash 

	scrapy startproject hn
---
	!bash
	hn/

		scrapy.cfg # le fichier de configuration du projet

		hn/ # le module du projet

			__init__.py

			items.py # fichier «items»

			pipelines.py # fichier «pipelines»

			settings.py # 

		spiders/ # nos araignées !
			__init__.py

---

## Items.py

	!python
	from scrapy.item import Item, Field

	class HnItem(Item):
    		title = Field()
    		link = Field()
    
Cela permet de ne pas prendre des champs par erreur.

La classe Item est très similaire à un dictionnaire Python.


---
## Les araignées (spider)
>Le code qui définit qu'est-ce que notre «crawler» va parser.

Nous allons donner de la logique à nos araignées !
----------
*	nom : pour identifier l'araignée
*	start_urls : le début d' une liste de liens internet
*	parse() : La  méthode qui nous envoye une réponse lorsque l'url est téléchargé


---

###hn_spider.py

	!python
	from scrapy.spider import BaseSpider
	from scrapy.selector import Selector

	class HnSpider(BaseSpider):
		name = 'hn' #nom
		allowed_domains = [] #
		start_urls = ['http://news.ycombinator.com']

	def parse(self, response):
		sel = Selector(response)
		sites = sel.xpath('//td[@class="title"]')
		for site in sites:
			title = site.xpath('a/text()').extract()
			link = site.xpath('a/@href').extract()

			print title, link
---

#Beautiful Soup 

	
---
#Crawl !

	!bash 
	
	scrapy crawl hn

---

#JSON
	!bash
	scrapy crawl hn -o items.json -t json

---

#Next ? Atelier ? web-scraping 102 ?

---

#Remerciement
---

#Questions ?

