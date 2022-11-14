---
title: 'Preklad slobodných programov'
subtitle: ''
summary: 'Ciele: Prilákať nových prekladateľov a čo najjednoduchšie popísať postup prekladu slobodného softvéru. Na praktickom príklade ukázať preklad konkrétneho programu.'
authors:
- admin
tags:
- Open source
categories:
date: "2004-04-23T00:00:00Z"
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

Ciele:

1.  Prilákať nových prekladateľov a čo najjednoduchšie popísať postup prekladu slobodného softvéru.
2.  Na praktickom príklade ukázať preklad konkrétneho programu.

### Úvod

Mnohé slobodné programy použivajú na prekladanie rozhrania nástroje [GNU gettext](http://www.gnu.org/software/gettext/), ktoré celý preklad zjednodušujú na preklad hlášok v textových súboroch (s príponami .po/.pot). Tieto súbory sa dajú prekladať v ľubovolnom textovom editore. Prácu prekladateľa však môžu veľmi uľahčiť grafické programy, ktoré zjednodušujú samotný preklad a výsledok dokážu jednoducho uložiť do výsledného binárneho súboru (s príponou .mo). Tento je už priamo využiteľný prekladaným programom (stačí preklad prekopírovať do príslušného adresára.

Rozhranie slobodných programov ako sú napríklad dialógy alebo textové hlášky v príkazovom riadku je najčastejšie v anglickom jazyku. Ak nie, je angličtina veľmi často prvý jazyk, do ktorého je daný program preložený. Takže ak chcete začať s prekladmi, doporučujem veľmi dobrú znalosť anglického jazyka.

#### Pár dôležitých pojmov na úvod

*   _Internationalisation - internacionalizácia / i18n_ - označuje proces toho, že je program schopný podporovať viacero jazykov. To znamená, že program nie je viazaný na konkrétny jazyk.
*   _Localisation - lokalizácia / l10n_ - označuje proces toho, že takto pripravenému programu dodáme potrebné informácie na to, aby bol schopný komunikovať v natívnom jazyku a zohľadňoval kultúrne zvyklosti danej krajiny a jazyka. Toto je možné viacerými spôsobmi. Najčastejšie používaným z nich je [GNU gettext](http://www.gnu.org/software/gettext), ktoré je nižšie popísaný.

Takže obecne povedané, internacionalizáciu riešia programátori a lokalizáciu prekladatelia.

Je nutné si uvedomiť, že internacionalizácia programu zďaleka neznamená iba preloženie textov v jeho rozhraní. Niektoré textové hlášky sú napísané priamo v skriptoch a iných častiach programu, ktoré nie sú priamo preložiteľné pomocou nástrojov GNU gettext. Skoro všetky programy majú možnosti a voľby, ako napríklad Y/N (Yes/No), ktoré tiež môžu byť preložené. Preložené môžu byť aj manuály a dokumentácia, ktorá je k programu priložená, čo je často samostatnou úlohou.

Všeobecne sa dá povedať, že lokalizácia rieši nasledovné oblasti:

*   **Znaky a Znakové sady** - najpoužívanejšia znaková sada v anglicky hovoriacich krajinách je ASCII. Znaková sada ISO 8859-1 pokrýva väčšinu hlavných európskych jazykov, okrem strednej a východnej Európy. Znaková sada ISO 8859-2 obsahuje znaky zo stredoslovenských jazykov, takže aj slovenčinu a češtinu. Naše jazyky obsahuje i znaková sada UTF-8.
*   **Meny** - pri narábaní a zobrazovaní peňažných jednotiek sa musí korektne zobrazovať i správna mena danej krajiny.
*   **Dátumy** - ich zápis sa môže líšiť podľa krajiny, napríklad 24\. 12\. 2007 sa v USA zapíše ako 2/25/06 a v Austrálií ako 25/12/06.
*   **Čísla**- reprezentácia čísla sa tiež líši podľa krajiny
    *   12,345.67 - Británia
    *   12.345,67 - Nemecko
    *   1,2345.67 - Ázia
*   Netreba zabúdať ani na systém jednotiek, napríklad metrický v porovnaní s anglickým
*   **Textové správy** - najjasnejšia oblasť lokalizácie

## Ako si uľahčiť prácu?

Prácu prekladateľa dokážu výrazne zjednodušiť grafické nástroje umožňujúce pohodlnejšiu prácu s po, pot a prípadne aj mo súbormi. Medzi asi najznámejšie programy patria nasledujúce:

*   [GTranslator](http://gtranslator.sourceforge.net/) - po editor pre GNOME prostredie
*   [KBabel](http://kbabel.kde.org/) - po editor pre KDE prostredie
*   [POEdit](http://www.poedit.net/) - multiplatformový po editor
*   Emacs po mód - pre pokročilejších prekladateľov

Ako ukážkový program som vybral kalkulačku [Qalculate](http://qalculate.sourceforge.net/). Program môžete stiahnuť priamo zo stránky, ale je veľká šanca že už bude súčasťou Vašej distribúcie. V mojej aktuálnej distribúcií Ubuntu Dapper už bola distribuovaná verzia 0.9-2-1\. Inštalácia bola tým pádom relatívne jednoduchá: `sudo aptitude install qalculate-gtk` (Pre rmp balík: `rpm -U qalculate-gtk.rpm`). Po prvom spustení program vypadá nasledovne:

![](https://www.valasek.biz/_/rsrc/1216843315017/na-stiahnutie/Qalculate.png)

Napriek tomu, že mám nastavené slovenské lokálne prostredie, program komunikuje anglicky :-)

Ako prvé sa pozrieme, aké jazyky sú v aktuálnej verzii programu podporované. Zo [stránky projektu](http://qalculate.sourceforge.net/downloads.html) stiahneme zdrojovú verziu programu a zistíme, že v adresári `qalculate-gtk-0.9.4/po` existuje lokalizácia pre švédčinu - sv.po a nórčinu - nl.po.

Prázdna jazyková šablóna `sk.po` sa generuje z pot súboru, ktorý získame buď priamo priamo z distribúcie, alebo môžeme požiadať autora projektu o vygenerovanie aktuálnej verzie pot súboru. V kapitole "Tvorba po súboru" je popísaný postup generovania šablóny sk.po priamo zo zdrojových kódov.

Ďalej predpokladám, že súbor sk.po máme, takže sa poďme pustiť do reálnej prekladateľskej práce.

V ďalšom texte bude paralelne ukázaný postup najčastejšie vykonávaných činností v po editoroch GTranslator a KBabel.

Pri prvom otvorení prázdnej jazykovej šablóny nás GTranslátor vyzve na doplnenie dát o preklade, ktoré doplníme nasledovne:

![](https://www.valasek.biz/_/rsrc/1219596709426/na-stiahnutie/gtranslator-header.png)

Aby sme vyskúšali ako "hladko" funguje prekladanie a test výsledku, preložíme si texty priamo v úvodnom dialógu: "Keypad", "History" a text tooltipu "Convert units in result". Následne vygenerujeme výslednú - binárnu verziu prekladu. Preklad jedného z textov a generovanie binárneho súboru je znázornené tu:

![](https://www.valasek.biz/_/rsrc/1216843314914/na-stiahnutie/gtranslator.png)

A čo s novo vygenerovaným súborom qalculate-gtk.mo? Stačí ho nakopírovať do adresára pre binárne verzie správ. Na Debian GNU/Linux systémoch je to adresár: `/usr/share/locale/xx/LC_MESSAGES/`, kde xx je kód jazyka, pre slovenčinu "sk" a češtinu "cs".

Toho docielime príkazmi:

```bash
stanislav@nb-valasek:~$ sudo cp qalculate-gtk.mo /usr/share/locale/sk/LC_MESSAGES/ #kópia do adresára pre slovenské preklady
stanislav@nb-valasek:~$ qalculate-gtk #test výsledku`
```

A výsledok je nasledujúci:

![](https://www.valasek.biz/_/rsrc/1216843317769/na-stiahnutie/Qalculate-prvy-preklad.png)

Je veľmi vhodné preklad overovať, či už prebežne, ak nie sme si istý správnym preložením konkrétnej hlášky, alebo až na konci prekladu, kde je overenie výsledného prekladu nutnosťou.

Preklad jednej správy v programe KBabel je znázornený na obrazovke nižšie:

![](https://www.valasek.biz/_/rsrc/1216843315007/na-stiahnutie/KBabel.png)

U programu KBabel som nezistil, ako sa v ňom generuje výsledný binárny súbor, mám podozrenie, že to nepodporuje. Binárny preklad však jednoducho získame zo súboru `sk.po` pomocou príkazu: `stano@nb-valasek:/qalculate-gtk-0.9.4/po$ msgfmt -v -o ./qalculate-gtk.mo ./sk.po`

### Postup prekladu pomocou nástrojov GNU gettext

Ak nemáme, alebo nechceme, používať na preklad grafické programy, môžeme ho spraviť pomocou textového editoraa nástrojov GNU gettext.

#### Národné prostredie

Pred samotným prekladom ešte pár slov k nastaveniu národného prostredia. U distribúcií založených na Debian GNU/Linuxe zistíme aktuálne nastavené národné prostredie príkazom `locale`:

    stano@nb-valasek:~$ locale LANG=sk_SK.UTF-8
    LANGUAGE=sk_SK.UTF-8
    LC_CTYPE="sk_SK.UTF-8"
    LC_NUMERIC="sk_SK.UTF-8"
    LC_TIME="sk_SK.UTF-8"
    LC_COLLATE="sk_SK.UTF-8"
    LC_MONETARY="sk_SK.UTF-8"
    LC_MESSAGES="sk_SK.UTF-8"
    LC_PAPER="sk_SK.UTF-8"
    LC_NAME="sk_SK.UTF-8"
    LC_ADDRESS="sk_SK.UTF-8"
    LC_TELEPHONE="sk_SK.UTF-8"
    LC_MEASUREMENT="sk_SK.UTF-8"
    LC_IDENTIFICATION="sk_SK.UTF-8"
    LC_ALL=

Nastavený je teda jazyk sk a krajina SK a kódová stránka na UTF-8, čo je štandardná kódová stránka v Ubuntu systéme. Podrobnejší popis pre Debian GNU/Linux je možné nájsť na stránke [Debian reference - 9.7 Localization (l10n)](http://qref.sourceforge.net/quick/ch-tune.en.html#s-l10n).

Ak chceme spustiť program v inom ako aktuálne nastavenom jazyku, spustíme ho nasledovne: "`LANG=nl qalculate-gtk`", tento príkaz napríklad spustí program qalculate-gtk v nórčine. Prípadne príkaz "`LANG=C program`" spustí program v originálnom/anglickom preklade. Takto môžeme súčasne spustiť rovnaký program v rôznych jazykoch.

Prípadne je možné celé prostredie priamo nastaviť do rôznych jazykov. Napríklad príkazom "`LANGUAGE="sk_SK:sk:cs_CS:cs:de:en_GB:en`" v súbore `/etc/environment` spôsobíme, že každý spúšťaný program skúsi nájsť slovenčinu, ak ju nenájde, pokračuje druhým, tretím jazykom ...

Adresár na výsledné preklady sme už spomínali vyššie, takže:

*   máme textovú podobu správ pripravených na preloženie,
*   vieme postup, ako si preklad priebežne overovať.

#### <a>Tvorba po súboru</a>

Už hotové preklady nemusia obsahovať všetky textové reťazce, ktoré sú v aktuálnej verzií programu. Preto je lepšie začať vygenerovaním prázdnej jazykovej verzie z pot šablóny príkazom `msginit`. Program Qalculate ale neobsahuje pot šablónu, takže si ju vygenerujeme príkazom `xgettext -f ./po/POTFILES.in -o ./po/messages.po`. Následné je možné použiť príkaz `msginit` alebo premenovať messages.po na sk.po. Program msginit by mal uľahčiť prácu a automaticky nastaviť hlavičky po súboru podľa Vášho prostredia. Na mojom systéme však príkaz nefungoval a tak som jednoducho premenoval súbor `messages.po`.

#### Prekladanie po súboru

Keď toto všetko vieme a máme `sk.po` súbor, poďme zaktualizovať hlavičky po súboru aby sme sa mohli vrhnúť na samotný preklad:

    # SOME DESCRIPTIVE TITLE.
    # Copyright (C) YEAR THE PACKAGE'S COPYRIGHT HOLDER
    # This file is distributed under the same license as the PACKAGE package.
    # FIRST AUTHOR <EMAIL@ADDRESS>, YEAR.
    #
    #, fuzzy
    msgid ""
    msgstr ""
    "Project-Id-Version: PACKAGE VERSION\n"
    "Report-Msgid-Bugs-To: \n"
    "POT-Creation-Date: 2006-08-06 17:43-0400\n"
    "PO-Revision-Date: YEAR-MO-DA HO:MI+ZONE\n"
    "Last-Translator: FULL NAME <EMAIL@ADDRESS>\n"
    "Language-Team: LANGUAGE <LL@li.org>\n"
    "MIME-Version: 1.0\n"
    "Content-Type: text/plain; charset=CHARSET\n"
    "Content-Transfer-Encoding: 8bit\n"

Kompletný preklad hlavičiek:

    # Translation of qalculate-gtk.po to Slovak
    # This file is distributed under the same license as the Qalculate package.
    # Copyright (C) 2003-2006 Niklas Knutsson (nq@altern.org).
    # Stanislav Valasek <valasek@fastmail.fm>, 2006.
    #
    msgid ""
    msgstr ""
    "Project-Id-Version: qalculate-gtk\n"
    "Report-Msgid-Bugs-To: \n"
    "POT-Creation-Date: 2006-08-06 17:43-0400\n"
    "PO-Revision-Date: 2006.05.08 13:33\n"
    "Last-Translator: Stanislav Valasek <valasek@fastmail.fm>\n"
    "Language-Team: sk <sk-i18n@linux.sk>\n"
    "MIME-Version: 1.0\n"
    "Content-Type: text/plain; charset=UTF-8\n"
    "Content-Transfer-Encoding: 8bit\n"

Aktualizáciu týchto hlavičiek dokážu programy GTranslátor i KBabel veľmi pohodlne upraviť podľa vami zadaných dát. V GTranslátore ich zadávame v nastaveniach:

![](https://www.valasek.biz/_/rsrc/1216843314958/na-stiahnutie/gtranslator-configuration.png)

KBabel nás k nastaveniu vyzve pri prvom spustení a je možná ich neskoršia úprava.

![](https://www.valasek.biz/_/rsrc/1216843315004/na-stiahnutie/KBabel-configuration.png)

Pri uložení sa hlavička po súboru automaticky zaktualizuje zadanými údajmi o prekladateľovi a pri každej aktualizácií prekladu v programe GTranslátor alebo KBabel sa automaticky aktualizuje dátum poslednej modifikácie.

Ešte pred prekladom ale pár slov k formátu po súboru, ktorý obsahuje samotné texty v nasledujúcej forme:

    #: panel/panel_config.c:1050
    #, fuzzy
    msgid "Color to use:"
    msgstr "Použité farby:"

Prvý riadok obsahuje názov zdrojového súboru a riadok, kde sa nachádza prekladaný text. Druhý riadok nie je povinný a môže obsahovať komentáre alebo direktívy, ako napríklad direktívu fuzzy alebo c-format. Direktívy pridáva prekladateľ alebo sú pridané automaticky pri generovaní po súboru. Direktíva fuzzy znamená, že preklad textu nie je istý a treba ho overiť. Takto označené hodnoty sa pri štandardnom generovaní mo súboru nedostanú do binárnej podoby prekladu. Tretí riadok obsahuje pôvodný a štvrtý riadok preložený text. Úplný popis formátu je na stránkach [GNU gettext - The Format of PO Files](http://www.gnu.org/software/gettext/manual/html_mono/gettext.html#SEC9).

Aby sme vyskúšali ako "hladko" funguje prekladanie a test výsledku, preložíme si texty priamo v úvodnom dialógu: "Keypad", "History" a text tooltipu "Convert units in result". Tieto texty sa nacháchadzajú v sk.po súbore a tu je ich doplnenie o preklad:

    #: data/main.glade:1886
    msgid "Convert units in result"
    msgstr "Vo výsledku konvertuj jednotky"
    #: data/main.glade:1967 data/main.glade:2980
    msgid "Keypad"
    msgstr "Klávesnica"
    #: data/main.glade:2006 data/main.glade:3035
    msgid "History"
    msgstr "História"

_Poznámka - na prekladanie používajte textové editory, ktoré dokážu správne určiť a uložiť kódovanie editovaného súboru. Toto spĺňajú najčastejšie používané editory ako: [gedit](http://www.gnome.org/projects/gedit/), [Kate](http://kate.kde.org/), [Emacs](http://www.gnu.org/software/emacs/), [vim](http://www.vim.org/) a mnohé ďalšie._

Následne spustíme už známe príkazy na vygenerovanie prekladu a spustíme program

`stanislav@nb-valasek:/qalculate-gtk-0.9.4/po$ msgfmt -v -o ./qalculate-gtk.mo ./sk.po`

3 preložené správy, 566 nepreložených správ.

    stanislav@nb-valasek:/qalculate-gtk-0.9.4/po$ sudo cp qalculate-gtk.mo /usr/share/locale/sk/LC_MESSAGES/
    stanislav@nb-valasek:/qalculate-gtk-0.9.4/po$ qalculate-gtk

A výsledok:

![](https://www.valasek.biz/_/rsrc/1216843317769/na-stiahnutie/Qalculate-prvy-preklad.png)

### Špeciality prekladu

Počas prekladania môžete naraziť na špeciálne formátovanie `msgstr` reťazcov. U dialógovej aplikácie sa stretnete s tzv. akceleračnými klávesami, ktoré určujú, pomocou ktorého znaku v reťazci sa dá daná funkcia použiť klávesovou skratkou ALT+klávesa. Je nutné si dávať pozor, aby dva reťazce v jednom menu nemali rovnaké akceleračné klávesy. Malý príklad aj s chybou - rovnaké akceleračné klávesy.

    #: data/main.glade:1608
    msgid "_Help"
    msgstr "_Pomocník"
    #: data/main.glade:1617
    msgid "_Contents"
    msgstr "_Obsah"
    #: data/main.glade:1639
    msgid "_About"
    msgstr "_O programe"

A výsledok:

![](https://www.valasek.biz/_/rsrc/1216843317750/na-stiahnutie/Qalculate-menu-pomocnik.png)

Na nasledujúcom texte je možné ukázať dve veci:

    #: data/main.glade:2341
    msgid "x<sup>2</sup>"
    msgstr "x<sup>2</sup>"

1.  jednak, že texty neobsahujú vždy iba samotný text, ale niekedy i technické informácie, v tomto prípade ide o HTML značky , ale môže ísť napríklad i o formátovacie značky programovacieho jazyka, v C++ napríklad %s alebo %d. Tieto značky sa bezo zmeny prenášajú do preloženého textu. Je dobé sa zoznámiť s najčastejšie používanými značkami, aby ste vedeli čo robia a ako ich vhodne začleniť do prekladaného textu. Tieto špeciálne znaky sú čiastočne popísané v [GNOME l10n-guide - Gotchas](http://developer.gnome.org/projects/gtp/l10n-guide/#gotchas),
2.  zároveň vidíme, že niektoré hlášky nie je treba prekladať a sú rovnaké ako v anglickej verzii. Tu nám prácu veľmi zjednoduší príkaz `msgen`, ktorý automaticky prekopíruje z po alebo pot súboru všetky anglické hlášky do preložených. Po spustení príkazu `msgen sk.po -o sk-new.po` dostaneme súbor `sk-new.po`, v ktorom máme všetky hlášky z pôvodného prekladu prekopírované do nového prekladu. Nevýhodou je, že stratíme informáciu o tom, koľko hlášok ešte nie je preložených.

Na urýchlenia a zjednodušenie prekladu je možné zo všetkých našich po súborov extrahovať už preložené texty do slovníka, ktorý následne používame na prvotný preklad ešte nepreloženého súboru a až potom preklad dokončujeme. Viac informácií je na stránke [GNU gettext - Usage of Translation Compendia](http://www.gnu.org/software/gettext/manual/html_mono/gettext.html#SEC54). Niektoré prekladateľské týmy, ako napríklad GNOME a KDE majú takéto slovníky už pripravené a jednotlivý prekladatelia ich len dopĺňajú.

## Ostatné druhy prekladov

Okrem vyššie spomenutého postupu prekladu programu pomocou nástrojov GNU gettext sú niektoré slobodné programy prekladané iným spôsobom. Typickým príkladom je preklad balíkov Mozilla suite pomocou špeciálneho programu [Mozilla translator](http://wiki.mozilla.org/L10n:Home_Page), alebo špeciálny postup [prekladu balíka OpenOffice](http://l10n.openoffice.org/), kde prekladatelia síce na preklad používajú po súbory, ale sú špeciálne generované zo zdrojových kódov. 

Samostatnou kapitolou je preklad dokumentácie, kde sa spôsob prekladu líši podľa toho, o akú dokumentáciu ide.

## Sumarizácia

Na záver krátka rekapitulácia jednotlivých krokov, ktoré budeme musieť spraviť, aby sme preložili konkrétny program a sprístupnili preklad ostatným užívateľom:

1.  **Oznámte svoj záujem o preklad** originálnemu prekladateľovi alebo lokalizačnému týmu.
2.  **Stiahnite a nainštalujte si potrebné nástroje**, minimálne GNU gettext (ktorý je často už súčasťou distribúcie) a prípadne niektorý z vyššie spomínaných po editorov.
3.  **Získajte najnovšiu verziu anglického po súboru** pre prekladaný jazyk, alebo si stiahnite pot šablónu. Ak chcete aktualizovať preklad, stiahnite po súbor pre Váš jazyk. Nastavte korektné údaje o Vás, prekladateľskom tíme, cieľovom jazyku a požadovanom kódovaní. Najčastejšie používané sú UTF-8 alebo ISO 8859-2.
4.  **Preložte čo ide** ...
5.  **Spätne skontrolujte preklad.**
6.  **Otestujte Váš preklad** - vytvorením mo súboru, jeho skopírovaním do adresára LC_MESSAGES pre Váš jazyk a spustením aplikácie.
7.  **Zašlite preklad späť** buď originálnemu prekladateľovi, alebo priamo potvrdením zmien do verzovacieho nástroja, najčastejšie: CVS alebo Subversion. Pokiaľ sa zmeny nedostanú do vašej distribúcie, môžete kľudne používať Vami preloženú verziu programu.
8.  **Nezabudnite na pravidelné aktualizácie prekladu** po vydaní každej novej verzie programu. Najčastejšie sú po súbory su priebežne aktualizované, tak ako programátori pridávajú alebo menia texty a hlášky programu. Nevýhodou je, že niekedy nie je možnosť inštalácie a otestovania takto vytvoreného prekladu.

## Pár tipov a rád na záver

*   Doporučujem začať prekladom malej samostatnej aplikácie, ktorú často používate a dokážete priamo skontrolovať preklad.
*   Ideálne sa prekladajú aplikácie, ktoré denno denne používate a môžete po sebe drobné chyby v prekladoch postupne odladiť.
*   Spravte toľko prekladov, koľko ich dokážete udržiavať v aktuálnom stave. Toto obzvlášť platí pre preklad napríklad webových stránok, ktoré rýchlo zastarávajú
*   Nie je anglický textu zrozumiteľný? Napíšte chybovú hlášku.
*   Nemeňte riadky s msgid.
*   Ak chcete spustiť program v inom ako aktuálne nastavenom jazyku, spustite ho nasledovne: "`LANG=nl qalculate-gtk`", tento príkaz napríklad spustí program qalculate-gtk v nórčine. Prípadne príkaz "`LANG=C program`" spustí program v originálnom/anglickom preklade. Takto si prípadne môžete súčasne spustiť rovnaký program v rôznych jazykoch.
*   Prípadne je možné si celé prostredie priamo nastaviť do rôznych jazykov. Napríklad príkazom "`LANGUAGE="sk_SK:sk:cs_CS:cs:de:en_GB:en`" v súbore `/etc/environment` spôsobíte, že každý spúšťaný program skúsi nájsť slovenčinu, ak ju nenájde, pokračuje druhým, tretím jazykom ...
*   Na zobrazenie rozdielov medzi dvoma po súbormi sú vhodné programy: [podiff](http://www.mail-archive.com/ubuntu-translators@lists.ubuntu.com/msg00022.html) alebo grafický program [Meld](http://meld.sourceforge.net/) alebo [KDiff3](http://kdiff3.sourceforge.net/)

## Lokalizačné projekty a tímy

*   Preklad základných balíkov Linuxu:
    *   [Preklad GNU balíkov](http://www.iro.umontreal.ca/translation/)
    *   [OpenOffice l10n](http://l10n.openoffice.org/) - lokalizácia OpenOffice balíkov
    *   [GNOME translation projekt](http://developer.gnome.org/projects/gtp/) - lokalizácia desktopového prostredia GNOME
    *   [KDE localisation](http://i18n.kde.org/) - lokalizácia desktopového prostredia KDE
    *   [Mozilla l10n](http://www.mozilla.org/projects/l10n/) - lokalizácia Mozilla balíkov
*   Preklad jednotlivých distribúcií:
    *   [Mandriva](http://www1.mandrivalinux.com/l10n/links.php3)
    *   [Fedora](http://fedoraproject.org/wiki/L10N)
    *   [Ubuntu](https://launchpad.net/rosetta)
    *   [Debian GNU/Linux](http://www.debian.org/international/)

## Odkazy

*   [Preklad Linuxu do slovenčiny](http://telka.sk/linux/sk-l10n/) - výborná úvodná stránka pre slovenských prekladateľov
*   [Mozilla Internationalization & Localization Guidelines](http://www.mozilla.org/docs/refList/i18n/) - pravidlá lokalizácie Mozilly
*   [GNU gettext](http://www.gnu.org/software/gettext/) - manuál k GNU gettext programom

## Používané pojmy a skratky

*   [CVS (Concurrent Versions System)](http://www.nongnu.org/cvs/) – nástroj na správu verzií programu
*   L10N - lokalizácia - skratka anglického slova localisation
*   I18N – iternalizácia/zmedzinárodnenie? - skratka anglického slova internationalisation
*   [Subversion](http://subversion.tigris.org/) – nástupca verzovacieho nástroja CVS
