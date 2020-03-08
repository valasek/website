---
title: 'Popis štruktúry a prípravy RSS súboru, existujúce skripty - II'
subtitle: ''
summary: V tomto článku sa je popísaná štruktúra RSS súboru, postup tvorby validácie a uverejnenia RSS súboru. A ako to RRS teda celé funguje? 
authors:
- admin
tags:
- Open source
categories:
date: "2005-05-21T00:00:00Z"
featured: false
draft: false

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Placement options: 1 = Full column width, 2 = Out-set, 3 = Screen-width
# Focal point options: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight
image:
  placement: 2
  caption: 'Image credit: [**Unsplash**](https://unsplash.com/photos/CpkOjOcXdUY)'
  focal_point: ""
  preview_only: false

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["internal-project"]` references `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
projects: []
---

V tomto článku sa je popísaná štruktúra RSS súboru, postup tvorby validácie a uverejnenia RSS súboru

## Úvod

A ako to RRS teda celé funguje? Tvorca webu spraví na webe nejakú zmenu, napríklad pridal nový článok alebo celú sekciu. Následne chce informovať návštevníkov web stránky. V tomto prípade má dve možnosti. Buď vytvorí stánku Aktualít, alebo použije RSS a ponechá na návštevníkoch spôsob jeho zobrazenia. 

Do RSS súboru jednoducho pridá ďalšiu položku obsahujúcu popis zmeny, odkaz na stránku a prípadne ďalšie informácie. Ľuďom, sú prihlásený k tomuto RSS kanálu sa táto zmena zobrazí ako aktualizácia Vašej web stránky.

Takto pripravený RSS súbor je tiež možné použiť ako zdroj noviniek na iných weboch, ktoré spársujú XML súbor a požadované informácie z neho zobrazia na svojej stránke. Predpokladám že tento spôsob používa ABCLinuxu na zobrazenie nadpisov N nových článkov z iných webov.

Pridanie RSS súboru na Vaše stránky bude mať nasledujúce štyri kroky:

*   Vytvorenie XML súboru
*   Validácia XML súboru
*   Pridanie odkazu naň
*   Prípadná registrácia na stránkach zaoberajúcich sa agregáciou RSS kanálov

## Ako RSS súbor vytvoriť?

RSS súbor je možné vytvoriť dvoma spôsobmi:

1.  ručne
2.  pomocou skriptov

My si ukážeme prvý spôsob. Ak máme stránky vytvorené v PHP, môžete použiť existujúce php skripty. I pri manuálnej tvorbe nám môžu pomôcť nástroje ako [kód generátor](http://www.webdevtips.com/webdevtips/codegen/rss.shtml). Kde zadáme pre stránku samotnú a každú položku nadpis, odkaz a textový popis a kód máme hotový. Následne stačí vygenerovaný kód uložiť ako XML súbor a pridať odkaz na naše stránky. Tento generátor však generuje RSS verziu 0.91 ako jazyk udáva en-us.

Ešte jedna poznámka: asi najjednoduchší spôsob vytvorenia RSS súboru je skopírovať existujúci súbor požadovanej verzie z iného webu a jeho prepísanie :-) A teraz k samotnej tvorbe súboru. Predstavme si, že chceme pridať položku s nasledujúcimi hodnotami:

``` text
Pridanie RSS kanálov
Tak a konečne sa na tento web dostal výdobytok internetu - RSS kanál.
Agreguje zmeny na stránke a môj blog.
http://www.valasek.biz/rss.php
```


Nadpis uzatvoríme do značiek `<title> ... </title>` takže dostaneme

```html
<title>Pridanie RSS kanálov</title>
```

To isté spravíme s popisom s tým rozdielom že použijeme značky `<description> ... </description>` Tým dostaneme:

```html
<title>Pridanie RSS kanálov</title>
<description>Tak a konečne sa na tento web dostal výdobytok internetu - RSS kanál. Agreguje zmeny na stránke a môj blog.</description>
```

Následne pridáme odkaz, začínajúci značkou `<link>`, nasledovaný odkazom a ukončený značkou `</link>`. Tým dostaneme:

```html
<title>Pridanie RSS kanálov</title>
<description>Tak a konečne sa na tento web dostal výdobytok internetu - RSS kanál. Agreguje zmeny na stránke a môj blog.</description>
<link>http://www.valasek.biz/rss.php</link>
``` 

Tým sme zadali všetky informácie potrebné pre pridanie jednej položky. Každá položka v súbore sa začína značkou `<item>` a ukončuje značkou `</item>`. Keď pridáme ešte jednu položku, dostaneme nasledovný kód:

```html
<item>
  <title>Pridanie RSS kanálov</title>
  <description>Tak a konečne sa na tento web dostal výdobytok internetu - RSS kanál. Agreguje zmeny na stránke a môj blog.</description>
  <link>http://www.valasek.biz/rss.php</link>
</item>
```

A ako niekto čítajúc RSS zistí, že informácie sa vzťahujú k nášmu RSS kanálu? Jednoducho. Ak niektorú položku neuzatvoríme do značky `<item>,</item>` tak bude vnímaná ako informácia o kanáli a nie ako samotná položka. Týmto dostaneme obsah:

```html
  <title>Všehochuť</title>
  <description>Aktualizácie a novinky na webe valasek.biz</description>
  <link>http://www.valasek.biz</link>
  <item>
    <title>Pridanie RSS kanálov</title>
    <description>Tak a konečne sa na tento web dostal výdobytok internetu - RSS kanál. Agreguje zmeny na stránke a môj blog.</description>
    <link>http://www.valasek.biz/rss.php</link>
  </item>
  <item>
    <title>Aktualizovaný email formulár</title>
    <description>Pôvodný email skript neodosielal správne email adresu odosielateľa a preto som mu nemohol odpovedať :-(. Aktuálna verzia na webe je opravená.</description>
    <link>http://www.valasek.biz/email.php</link>
  </item>
```

Ostáva nám dorobiť posledných pár vecí. Najskôr potrebujeme definovať, že súbor je napísaný podľa špecifikácie XML 1.0, jeho kódovanie. A tiež uviesť používanú RSS verziu. Doteraz sme všetky značky použili v súlade so špecifikáciou UserLand RSS 0.91\. My však chceme použiť poslednú verziu RSS - 2.0\. Toto nám dáva do budúcnosti priestor na pridanie ďalších užitočných vecí. Nakoniec po špecifikácií RSS verzie pridáme otváraciu značku "channel". Takže na začiatok súboru pridáme:

A na koniec vložíme uzatváraciu značku kanálu a RSS v tomto poradí. Teda:Takže kompletný súbor je:

```html
<?xml version="1.0" encoding="utf-8"?>
<rss version="2.0">
  <channel>
    <title>Všehochuť</title>
    <description>Aktualizácie a novinky na webe valasek.biz</description>
    <link>http://www.valasek.biz</link>
    <item>
      <title>Pridanie RSS kanálov</title>
      <description>Tak a konečne sa na tento web dostal výdobytok internetu - RSS kanál. Agreguje zmeny na stránke a môj blog.</description>
      <link>http://www.valasek.biz/rss.php</link>
    </item>
    <item>
      <title>Aktualizovaný email formulár</title>
      <description>Pôvodný email skript neodosielal správne email adresu odosielateľa a preto som mu nemohol odpovedať :-(. Aktuálna verzia na webe je opravená.</description>
      <link>http://www.valasek.biz/email.php</link>
    </item>
  </channel>
</rss>
```

## Uloženie a pomenovanie súboru

Na pomenovanie neexistujú žiadne pravidlá. Súbory však najčastejšie končia príponou xml alebo rss. Nezabudnite súbor uložiť v rovnakom kódovaní, aké ste špecifikovali v xml súbore. U nás je to UTF-8\. Po tomto kroku nám ostáva už len nahranie súboru na web server, najčastejšie do koreňového adresára a jeho validácia.

## Validácia súboru

Po vytvorení súboru nasleduje nemenej dôležitý krok a to jeho validácia. To znamená overenie či je xml well-formed a názvy jednotlivých značiek voči DTD. Množstvo validátorov nájdete na webe, ako napríklad [RSS Validátor](http://rss.scripting.com/), alebo [Feed validator](http://feedvalidator.org/) všetky však vyžadujú mať rss súbor nahraný na Vašom webe.

## Pokročilé nastavenia

Vyššie popísané nastavenia predstavujú iba základné možnosti RSS. Je nutné si však uvedomiť, že nie RSS čítačky dokážu správne interpretovať všetky RSS značky a preto odporúčam byť pri ich používaní skôr striedmejší.

V rámci súboru je ešte možné pridať tieto značky:

*   Rozdelenie položiek do viacerých "kanálov" - pomocou značky `channel`
*   Definícia použitého jazyka - pomocou značky `language`
*   Dátum publikácie kanálu alebo samotnej položky - pomocou značky `pubDate`
*   Nastavenie loga kanálu - pomocou značky `image`
*   Email na autora kanálu- pomocou značky `author`
*   Katogóriu položky - pomocou značky `category`

Zoznam existujúcich značiek, ktoré je možné použiť popísaný v [RSS 2.0 špecifikácií](http://blogs.law.harvard.edu/tech/rss). Časť súboru obsahujúca niektoré z vyššie uvedených možností vyzerá nasledovne:

```html
     <image>
      <title>valasek.wordpress.com</title>
      <url>http://1.gravatar.com/blavatar/d0031ce356661fb9ea4a6d617b95e1fd?s=32</url>
      <link>https://valasek.wordpress.com/</link>
      <description>Aktualizácie a novinky na webe Všehochuť</description>
    </image>
    <title>Stanislav Valášek</title>
    <description>Aktualizácie a novinky na webe valasek.wordpress.com</description>
    <link>https://valasek.wordpress.com</link>
    <language>cz</language>
    <publisher>valasek.wordpress.com</publisher>
    <pubDate>Wed, 25 May 2005 23:00:00 GMT</pubDate>
```

Počet položiek v súbore nie je definovaný ale ideálna veľkosť je okolo 15 záznamov. To znamená manuálne vymazávanie starých položiek.

RSS súbor môže byť poslaný aj na web stránky agregujúce nové články na internete. Medzi najznámejšie stránky patria napríklad [Moreover](http://www.moreover.com/), [syndic8](http://www.syndic8.com/), [UserLand](http://aggregator.userland.com/) alebo [News Knowledge](http://www.newsknowledge.com/). Problémom je, že tieto stránky agregujú väčšinou anglicky hovoriace stránky. Na Slovenskom/Českom internete som web podobného zamerania zatiaľ nenašiel.

## RSS pomocou skriptov

Ak nám nestačia vyššie uvedené možnosti, tak na vytvorenie RSS súboru môžeme použiť i niektorý z open source skriptov. To však požaduje mať na servery prístupný skriptovací jazyk, či už PHP, Javu alebo Python. Osobne som žiadny zo skriptov nepoužil, ale ako odrazový mostík určite poslúži [DOAP project](https://github.com/edumbill/doap/wiki), alebo java [XmlTextWriter](http://www.codeproject.com/aspnet/RSSviaXmlTextWriter.asp).pre RSS 2.0.

## Odkazy

Ostávam verný tradícií a pridávam pár, dúfajme užitočných, odkazov:

*   [RSS specifications](http://www.rss-specifications.com/) - stránka venujúca sa RSS
*   [IBM tutoriál](http://www-106.ibm.com/developerworks/xml/library/x-rss20) - veľmi pekný tutoriál venovaný popisu RSS a štruktúre RSS 2.0
*   [RSS súborový formát](http://en.wikipedia.org/wiki/RSS_%28file_format%29) - popis RSS na Wikipédií
*   [RSS 2.0 tutorial](http://itgazette.com/issue_3/tutorials/rss_deliver.php) - jednoducho popísané vytvorenie RSS 2.0 súboru
*   [Atom Enabled](http://www.atomenabled.org/) - stránka popisujúca formát Atom a jeho výhody

## Záver

Napriek tomu, že formát RSS stále nie je ustálený je to pomerne silný nástroj. Do budúcnosti sa ako nádejný presadzuje formát Atom. Ako bolo ukázané, RSS súbor má pomerne jednoduchú štruktúru, aspoň RSS 2.0 :-), takže ak sa Vaše Vaše stránky častejšie menia, je škoda nevyužiť túto možnosť zdieľania informácií.`
