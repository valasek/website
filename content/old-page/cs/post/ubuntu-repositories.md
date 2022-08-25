---
title: 'Ubuntu repositories, popis a nastavenie'
subtitle: ''
summary: Článok obsahuje popis zdrojov programov pre distribúciu Ubuntu Linux a všeobecný popis stručný popis štruktúry repository. Príklad aktuálne existujúcich zdrojov balíčkov a čiastočne možnosti nastavenia váh pre jednotlivé repository.
authors:
- admin
tags:
- Open source
categories:
date: "2004-05-24T00:00:00Z"
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

Článok obsahuje popis zdrojov programov pre distribúciu [Ubuntu Linux](http://www.ubuntulinux.org/) a všeobecný popis stručný popis štruktúry repository. Príklad aktuálne existujúcich zdrojov balíčkov a čiastočne možnosti nastavenia váh pre jednotlivé repository.

## Základné pojmy v článku

V článku sa často vyskytujú nasledujúce pojmy a preto sú tu uvedené na zjednotenie pohľadu na ne:

*   Repository - pozri nižšie kapitolu "Čo je to repository".
*   Distribúcia(archive, distribution) - časť repository obsahujúca konkrétnu verziu. Napr. hoary, testing, universe. Netreba si tento pojem pliesť s Linux distribúciou.
*   Komponenta - logicky vyčlenená časť v rámci distribúcie. Napr. main, universe, multiverse.

## Úvod do inštalácie programov v GNU/Linuxe

Na rozdiel napríklad od MS Windows, sú GNU/Linux programy väčšinou pripravené na inštaláciu v jednotnej forme, tzv. balíčkoch. V závislosti od použitého balíčkovacieho systému, môže ísť napríklad o balíčky:

*   typu **deb** - používane v [Debiane](http://www.debian.org/) a odvodených distribúciách, teda aj [Ubuntu](http://www.ubuntulinux.org/), [Mepis](http://www.mepis.org/), [Knoppix](http://www.knoppix.org/), ...
*   typu **rpm** - používané v distribúcií [RedHat](http://www.redhat.com/) a odvodených distribúciách, napríklad [Fedora Core](http://fedora.redhat.com/), [Mandriva](http://www.mandriva.org/) (bývalý Mandrake), ...

Každý program pre GNU/Linux, ktorý je dostupný na internete, môže byť prístupný vo forme zdrojových kódov, na spustenie takéhoto programu ho potrebujeme skompilovať, alebo vo forme pripraveného balíčka ako bolo spomenuté vyššie. To nám ale samo o sebe nezaručuje, že takto stiahnutý program bude inštalovateľný a spustiteľný bez problémov. Napríklad obe distribúcie, Fedora Code i Mandriva používajú formát rpm, ale nie obe majú rovnaké verzie nainštalovaných knižníc a tu môžu pri inštalácií nášho balíčku nastať problémy.

Tieto potiaže sa v Linuxových distribúciách riešia vytvorením tzv. repository, čo je jednotné úložište presne vybraných verzií programov, ktoré sú navzájom otestované a výrobca určitým spôsobom zaručuje, že tieto programy bude možné nainštalovať a spustiť bez problémov.

V tomto článku nájdete popis repository pre [Ubuntu Linux](http://www.ubuntulinux.org/), ktorý je založený na [Debian GNU/Linuxe](http://www.debian.org/) a preto používa ako formát programov - balíčkov deb formát.

## Čo je to repository

Jednoducho povedané, ide o štruktúru adresárov, obsahujúcu zoznam balíčkov/programov pre konkrétnu distribúciu. Tento adresár sa môže nachádzať online alebo offline, napríklad na CD-ROM, lokálnom alebo sieťovom disku, alebo môže byť prístupný pomocou HTTP alebo FTP protokolu.

## Ako je to s Ubuntu repository

[Ubuntu Linux](http://www.ubuntulinux.org/) je založený na [Debiane](http://www.debian.org/) a preto používa ako formát balíčkov deb. Samotné repository je ešte podľa povahy balíčkov členené do viacerých distribúcií a komponent. **Distribúcie:**

*   **hoary** - obsahuje programy samotného systému [Ubuntu Hoary](http://www.ubuntulinux.org/)
*   **updates** - obsahuje potrebné aktualizácie, vydané po uverejnení verzie
*   **security** - obsahuje kritické bezpečnostné opravy

Ubuntu balíčky sú v rámci každej distribúcie členené do **komponent** podľa dvoch kritérií:

*   "slobody" a
*   podpory aktualizácií a bezpečnostných opráv zo strany Ubuntu komunity.

Takže máme nasledovné komponenty:

*   **main** ( úplne slobodný software, podporovaný ) - obsahuje programy na plne funkčný desktop a server založený na slobodnom software
*   **restricted** ( nie úplne slobodný software, podporovaný ) - ide všeobecne používané programy, prípadne binárne ovládače
*   **universe** ( plne slobodný software, nepodporovaný ) - ide vlastne o Debian unstable repository, komponenta main
*   **multiverse** ( neslobodný software, nepodporovaný ) - ide vlastne o Debian unstable repository, komponenta non-free, je nutné súhlasiť s licenčnými podmienkami daného programu

Ich plný popis je na stránke [Ubuntu components](http://www.ubuntulinux.org/ubuntu/components/document_view "Ubuntu components"). Toto rozdelenie nám prináša jednoduchú možnosť aktualizácie napríklad z distribúcie z Hoary na Breezy nám stačí zmeniť názov u distribúcie na Breezy, aktualizovať zoznam balíkov a nainštalovať tie zmenené.

_Poznámka: opačná cesta, tzv. downgrade systému nie je tak často používaný a je možné naraziť na problémy so závislosťami. Najčastejšie je nutné použiť i tzv. APT pinning na zmenu priorít jednotlivých repository._

### Neoficiálne, dodatočné repository pre Ubuntu

Po vzniku distrubúcie Ubuntu, čo nebolo tak dávno, začali postupne vznikať neoficiálne repository priamo pre Ubuntu Linux. Medzi najznámejšie patrí:

*   [**backports**](http://backports.ubuntuforums.org/ "backports") - obsahuje spätne zostavené balíky pre často používané desktopové aplikácie. Ide o komunitný projekt a aktuálne obsahuje napríklad Firefox 1.04, nové verzie aplikácií Gaim, Gimp, Synaptic. Pred použítím odporúčam prečítať [FAQ](http://backports.ubuntuforums.org/faq.php "FAQ") na oboznámenie sa s možnými rizikami následného upgrade na Ubuntu Breezy.

Keďže distribúcia [Ubuntu](http://www.ubuntulinux.org/) vychádza z [Debianu](http://www.debian.org/), je možné použiť repository pripravené pre Debian. Okrem priamych Debian repository, universe a multiverse, patria medzi najznámejšie tieto:

*   [**debian-marillat**](http://debian.video.free.fr/ "debian-marillat") - balíčky, ktorých licenčné podmienky alebo iné obmedzenia spôsobili, že nemôžu byť súčasťou slobodných distribúcií. Nachádzajú sa tu napríklad programy MPlayer, Adobe Acrobat Reader, w32codecs, ...
*   [**apt-get.org**](http://www.apt-get.org/) - neoficiálne Debian reposiory
*   [**usefulinc.com**](http://debian.usefulinc.com/) - obsahuje GNOME bluetooth subsystém.
*   [**tux.org**](http://www.tux.org/ "tux") - jedno z mnohých repositories pre javu v deb balíčkoch. Aktuálna verzia je 1.4.

Ďalšie Ubuntu repository je možné nájsť na stránke so samo popisným názvom [BreakMyUbuntu](http://www.ubuntulinux.org/wiki/BreakMyUbuntu), v neoficiálnej Ubuntu príručne v kapitole [Repositories](http://www.ubuntuguide.org/#repositories).

## Ako pridať nové repository

V GNOME napríklad pomocou programu [Synaptic](http://www.nongnu.org/synaptic/) v menu Settings->repositories.

Prípadne je možné ručne upraviť konfiguračný súbor /etc/apt/sources.list, ktorý používajú všetky programy na aktualizáciu systému. Každý riadok v tomto súbore má formát v tvare:

`deb|deb-src uri distribution [component1] [component2] [...]`

*   deb|deb-src - deb označuje binárny balíček alebo deb-src balíček so zdrojovými kódmi
*   uri - adresa, cesta k repository
*   distribution - distribúcia repository
*   component1 - komponenta repository

Príklad /etc/apt/sources.list

    ## deb cdrom:[Ubuntu 5.04 _Hoary Hedgehog_ - Release i386 (20050407)]/ hoary main restricted

    ## Major bug fix updates produced after the final release of the
    ## distribution.
    deb http://archive.ubuntu.com/ubuntu/ hoary-updates main restricted multiverse universe
    deb-src http://sk.archive.ubuntu.com/ubuntu hoary-updates main restricted multiverse universe

    ## Security updates
    deb http://security.ubuntu.com/ubuntu/ hoary-security main restricted multiverse universe
    deb-src http://security.ubuntu.com/ubuntu hoary-security main restricted multiverse universe

    ## Hoary repositories
    deb http://archive.ubuntu.com/ubuntu/ hoary main restricted multiverse universe
    deb-src http://sk.archive.ubuntu.com/ubuntu hoary main restricted multiverse universe

    ## MPlayer + AdobeReader, w32codecs, …
    ## deb ftp://ftp.nerim.net/debian-marillat stable main
    deb ftp://ftp.nerim.net/debian-marillat testing main

    ## ftp://ftp.tux.org/java/debian/ mirror for a java repository
    deb ftp://ftp.tux.org/java/debian sarge non-free

    ## Backported Ubuntu repositories – nepoužívam (http://backports.ubuntuforums.org)
    ## deb http://backports.ubuntuforums.org/backports hoary-backports main universe multiverse restricted
    ## deb http://backports.ubuntuforums.org/backports hoary-extras main universe multiverse restricted

Podrobnejší popis pridávania repositories je na stránke [Adding repositories HowTo](http://www.ubuntulinux.org/wiki/AddingRepositoriesHowto/view?searchterm=repository).

## Aké repository použiť

To záleží od toho, na aký účel svoj systém používate, akú stabilitu od neho požadujete a aké baličky potrebujete. Ubuntu vydáva novú verziu každý 1/2 rok, čo je na desktopový systém optimálna frekvencia. Aspoň pri prechode z Warty na Hoary bola táto doba dodržaná...

Ako bolo v úvode spomínané, tak repository je sada navzájom otestovaných balíčkov. Teda ako používate iba oficiálne repository Ubuntu, nemali by ste mať problémy so závislosťami. Ale ako všetko na svete, aj toto má svoje obmedzenia, lebo oficiálne zdroje neobsahujú množstvo potrebných balíčkov.

Všeobecne platí, že ak nechcete riešiť občasné problémy so závislosťami, používajte inštaláciu baličkov z repositories v tomto poradí (od najmenej rizikových):

1.  priamo Ubuntu podporované
2.  vytvorené pre Ubuntu, ako napríklad Ubuntu BackPorts
3.  vytvorené pre Debian, ako napríklad Marillat, apt-org
4.  inštalácia stiahnutých deb balíčkov, ak nie sú ani v jednom vyššie uvedených repository
5.  kompilácia

_A ako všetko na svete, aj tento zoznam má svoje výnimky._

Teda ak nepotrebujete žiadne programy mimo oficiálnych Ubuntu repositories, nepridávajte si žiadne iné. Ak však nejaký potrebujete, skúste prehľadať repositories v uvedenom poradí a pridajte tie, ktoré aktuálne potrebujete. Prípadne môžete repository zoradiť podľa vašich preferencií pomocou tzv. APT pinningu.

## APT pinning - keď máme rovnaký program v dvoch repository

Ako sa bude v súbore sources.list množiť počet repositoriy, rastie aj pravdepodobnosť toho, že jeden sa program nachádza v dvoch alebo viacerých repositories. APT pinning je možnosť, ako vyjadriť preferenciu (pridať váhy) pre

*   verziu balíčku,
*   distribúciu alebo
*   komponentu repository.

Preferencie sa nastavujú v súbore /etc/apt/preferences. Každá preferencia sa skladá z nasledujúcich častí:

*   Package - menu balíčku alebo zástupný znak * pre všetky balíky
*   Pin - označenie verzie balíčku, distribúcie, komponenty alebo repository
*   Pin-Priority - priorita daného záznamu

Najčastejšie sa preferujú celé distribúcie alebo repository. Napríklad

    Package: *
    Pin: origin marillat.free.fr
    Pin-Priority: 600

    Package: *
    Pin: origin http://www.ibiblio.org
    Pin-Priority: 610

    Package: *
    Pin: origin http://www.argon.org
    Pin-Priority: 620

znamená, že balíček inštalovaný z www.argon.org nebude automaticky vymenený za balíček z ostatných dvoch zdrojov a balík z www.ibiblio.org nebude vymenený balíčkom z marillat.free.fr.

Podrobnejší popis APT pinningu je na [manuálovej stránke apt_preferences](http://www.die.net/doc/linux/man/man5/apt_preferences.5.html) a v [manuále APT](http://www.debian.org/doc/manuals/apt-howto/ch-apt-get.en.html).

Ak teda chceme pre vyššie uvedený súbor sources-list pridať vyššiu pre balíčky z distribúcie Ubuntu Hoary, tak to docielime nasledujúcimi riadkami v súbore /etc/apt/preferences:

    Package: *
    Pin: release a=hoary
    Pin-Priority: 600

## Odkazy

Tu je pár odkazov na užitočné stránky ohľadne Debian balíčkovacieho systému a repository

1.  [Debian repository HowTo](http://www.debian.org/doc/manuals/repository-howto/repository-howto.html) - obsahuje popis štruktúry repository
2.  [APT HowTo](http://www.debian.org/doc/manuals/apt-howto/index.en.html) - obsahuje podpobný popis Advanced pachaging Tools - APT, ktorý používa Ubuntu/Debian pre prácu s repositories
3.  [Debian Binary Package Building HOWTO](http://tldp.org/HOWTO/Debian-Binary-Package-Building-HOWTO/) - obsahuje popis prípravy binárneho deb balíčku
