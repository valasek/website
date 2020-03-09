---
title: 'Agregácia webového obsahu, používané formáty a možnosti použitia - I'
subtitle: ''
summary: Tento dvojdielny článok popisuje agregáciu webového obsahu. V tejto časti sa zoznámime všeobecne s agregáciou, existujúcim formátmi, ich porovnaním a možnosťami zobrazenia. Článok na záver obsahuje postup pridania RSS kanála do HTML stránky.
authors:
- admin
tags:
- Open source
categories:
date: "2005-03-20T00:00:00Z"
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

Tento dvojdielny článok popisuje agregáciu webového obsahu. V tejto časti sa zoznámime všeobecne s agregáciou, existujúcim formátmi, ich porovnaním a možnosťami zobrazenia. Článok na záver obsahuje postup pridania RSS kanála do HTML stránky.

## Čo je to agregácia

Agregácia/syndikácia webového obsahu je založená na myšlienke uverejňovania zmien na webovom potrále v špeciálnom formáte. Na zobrazenie tohoto formátu existuje množstvo programov, či skriptov, ktoré zmeny umožnia zobraziť či už v samostatnom programe, vložené v nejakej aplikácií alebo ako súčasť HTML stránky.

## Ako to celé funguje

Všeobecne sa dá povedať, že autor web stránok vytvorí jeden alebo viac xml súborov, pridá na ne z web stránok odkazy a následne ich podľa potreby aktualizuje. Programy/skripty načítavajúce tieto xml súbory dokážu zistiť, či boli aktualizované a zvýraznene zobrazia nové položky v nich.

## Formáty používaných súborov

Keďže web agregácia je relatívne mladá vec a pri jej vzniku stáli viaceré firmy alebo jednotlivci, vzniklo množstvo "oficiálnych" formátov.

Asi najjednoduchšie to je s popísaním formátu **Atom**. Ten vznikol na základe nejednotnosti a rôznorodosti množstva vznikajúcich formátov. Je však relatívne mladý a aktuálne prebieha jeho štandardizácia v IETF.

Formát, alebo skôr skratka ktorá priniesla toľko zmätku je **RSS**. Skratka z toho dôvodu, že názov RSS bol v priebehu času používaný pre viac druhov protokolov, ako napríklad Rich Site Summary, neskôr Really Simple Syndication a následne RDF Site Summary a bol vyvíjaných viacerými vývojármi.

A aby sme si v tom spravili poriadok, tu je zoznam formátov, aj s odporúčaním, ktorý kedy použiť:

| Verzia | Vlastník | Výhody | Odporúčanie |
| ------ | -------- | ------ | ----------- |
| [RSS 0.90](http://www.purplepages.ie/RSS/netscape/rss0.90.html) | Netscape | Zastaralý po vzniku 1.0 | Nepoužívať |
| [RSS 0.91](http://backend.userland.com/rss091) | Vytvorený Netscapom, prebraný do UserLand |Veĺmi jednoduchý, oficiálne zastaralý po vzniku verzie 2.0 ale stále veľmi populárny | Použite na jednoduchú syndikáciu. V prípade potreby väčšej komplexnosti zaručuje jednoduchú migráciu na verziu 2.0 |
| RSS 0.92, 0.93 a 0.94 | UserLand | Obsahujú bohatšie metadata ako 0.91\. Zastarali po vzniku verzie 2.0 | Použite verziu 2.0 | 
| [RSS 1.0](http://web.resource.org/rss/1.0/) | RSS-DEV Working Group | Založený na RDF, rozšíriteľný pomocou modulov, nekontrolovaný jediným výrobcom. Stabilné jadro, aktívny vývoj modulov | Použite pre aplikácie založené na RDF ak potrebujete RDF špecifické moduly | 
| [RSS 2.0](http://blogs.law.harvard.edu/tech/rss) | UserLand | Rozšíriteľný pomocou modulov, ponúka ľahkú migráciu z vetiev 0.9x. Stabilné jadro, aktívny vývoj modulov | Použite pre rôzne účely, na syndikáciu s bohatými metadátami | 
| [Atom](http://ietf.org/html.charters/atompub-charter.html) | Internet Engineering Task Force (IETF) | Momentálne vstúpil do fáze štandardizácie v IETF | Odporúčané je počkať na finál verziu špecifikácie | 

Aktuálne najpoužívanejší formát podľa [syndic8](http://www.syndic8.com/stats.php?Section=rss) je RSS 2.0 nasledovaný verziami 0.91 a 1.0 s rovnomerne rozdeleným podielom.

Veľmi sľubne sa vyvíja formát Atom, ktorý si kladie vyššie ciele a okrem zjednotenia formátu agregácie sa snaží zjednotiť aj formát na získanie/objavenie RSS súborov na internete a pripája k tomu formát na uverejňovanie blog zápisov. Blogy postihlo niečo podobné ako webovú syndikáciu a aktuálne existuje na posielanie nového blog zápisu viacero formátov, napríklad Blogger API alebo LiveJournal XML-RPC Klient/Server Protokol ale to je na samostatný článok. Atom si kladie za cieľ zjednotiť a nahradiť tieto protokoly.

Následne pri popise tvorby RSS súboru budem používať iba RSS 2.0 formát, ale jeho upravenie na inú verziu by nemalo byť náročné.

### Zobrazenie kanálov

Na web stránkach sa odkazy na RSS feedy dajú nájsť vo forme nasledujúcich ikoniek:

![](/img/rss-xml.gif "rss-xml")
![](/img/rss-validatom.gif "rss-validatom")
![](/img/rss-valid.gif "rss-valid")
![](/img/rss-square.gif "rss-square")
![](/img/rss-rss.png "rss-rss")
![](/img/rss-livemark.png "rss-livemark")
![](/img/rss-atomfeed.png "rss-atomfeed")

prípadne vo forme odkazu s názvom RSS, RDF alebo Atom. Programov na zobrazovanie RSS existuje nepreberné množstvo. Či už priamo vo webových prehliadačoch, ako napríklad vo Firefoxe zabudované prehliadanie: ![](/img/rss-firefox.png "rss-firefox") alebo pomocou rôznych pluginov prípadne samostatných konzolových alebo grafických programov. Dobrú prácu odvádzajú: na MS Windowse [RssReader](http://www.rssreader.com/), pre GNOME [Liferea](http://liferea.sourceforge.net/), [Straw](http://www.nongnu.org/straw/) alebo prenositeľný v Jave napísaný [RssOwl](http://www.rssowl.org/). Pokiaľ chcete vyčerpávajúci zoznam programov na zobrazovanie RSS, tak navštívte [Open directory](http://directory.google.com/Top/Reference/Libraries/Library_and_Information_Science/Technical_Services/Cataloguing/Metadata/RDF/Applications/RSS/News_Readers/).

## Pridanie titulkov z iného webu na HTML stránku prostredníctvom RSS

Chcete mať na svojej stránke aktuálny zoznam nových článkov z Vášho obľúbeného servera? Ak máte stránky spravené pomocou jsp alebo php tak nie je nič ľahšie. Celá operácia sa skladá z:

*   Nájdenia vhodného skriptu, pársujúceho rss súbor
*   kontroly, či si rozumie s poskytovanou verziou RSS a
*   vhodného vloženia výstupov zo skriptu do vašej stránky.

Nemá význam menovať konkrétne skripty, existuje ich nepreberné množstvo a každý si určite vyberie taký, aký potrebuje. Kľúčové slová do googlu sú: "php rss parser" alebo "jsp rss parser". V podstate každý skript má metódu na načítanie a parsovanie RSS súboru do nejakého objektu a následne poskytuje metódy na sprístupnenie:

*   nadpisu
*   odkazu a
*   popisu

pre celú stránku a konkrétnu položku. Pre vyššie zmienený výstup blogu som použil skript [RSSReader](http://www.apptools.com/phptools/xml/rss.php) a v samotnom HTML kóde to vypadá nasledovne:

    <?php
      // Include the file that does all the work include("./php/rssreader.php");
      // This is the URL to the actual RSS feed. Change this value if you want to show a different feed.
      $url="http://www.abclinuxu.cz/auto/blog/sloboda.rss";
      
      // Create an instance of the rssFeed object, passing it the URL of the feed $rss=new rssFeed($url);
      // If there was an error getting the data
      if ($rss->error) {
        // Show the error
        print "<h1>Chyba:</h1>\n<p><strong>$rss->error</strong></p>";
      } else {
        <br />   // Otherwise, we have the data, so we call the parse method
        $rss->parse();
        print "<h1>Môj Blog: ";
        $rss->showHeading(span);
        print "</h1>\n";
        
        // Display the image if there is one
        $rss->showImage("left");
        
        // If the RSS feed provides a link
        if ($rss->link) {
          // Display it
          print '<p>Tento blog je vedený na serveri <a href="http://www.abclinuxu.cz" title="AbcLinuxu">www.AbcLinuxu.cz</a> na stránke ';
          $rss->showLink();
          print "</p>\n";
        }
        // Display the description
        $rss->showDescription();
        // Show the news stories
        $rss->showStories();
      }
    ?>

## Odkazy

A tu je pár odkazov, ktoré Vám pomôžu začať bádanie na poli RSS:

*   [rss.userland.com](http://rss.userland.com/) - stránka UserLand venovaná RSS
*   [PERL tutoriál](http://webreference.com/perl/tutorial/8/) - ako na parsovanie a konverziu RSS formátu v PERLe
*   [WebReference](http://www.webreference.com/authoring/languages/xml/rss/) - rozcestník užitočných odkazov

## Záver

Webová agregácia ponúka flexibilnú možnosť, ako agregovať poskytovaný obsah viacerých webov do jednej stránky. Jednotný značkovací jazyk umožňuje ľahké zobrazenie týchto zmien v množstve koncových aplikácií. Veľmi sľubne sa sa rozvíja formát Atom, v ktorom už dnes veľa stránok svoj obsah poskytuje a má veľké šance odstrániť zmätok, ktorý vznikol zavedením množstva vyššie uvedených formátov.

V ďalšej časti nájdete popis samotnej štruktúry xml súboru, postup ako vytvoriť a zvalidovať RSS súbor, skripty zjednodušujúce prácu a generátor RSS súboru pre pohodlných. A tiež odpovede na otázky z diskusie, samozrejme ak nejaké budú :-)
