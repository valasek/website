---
title: 'Ako nainštalovať GNU/Linux bez prepísania hlavného zavadzača MBR?'
subtitle: ''
summary: 'Cieľ: Popísať postup ako spúšťať GNU/Linux, nainštalovaný na notebooku alebo stolnom PC, na ktorom beží i MS Windows a ako ho v prípade potreby jednoducho odstrániť.'
authors:
- admin
tags:
- Open source
categories:
date: "2004-04-22T00:00:00Z"
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

_Cieľ: Popísať postup ako spúšťať GNU/Linux, nainštalovaný na notebooku alebo stolnom PC, na ktorom beží i MS Windows a ako ho v prípade potreby jednoducho odstrániť._

Pri štandardnej inštalácií GNU/Linuxu, ako druhého operačného systému na jeden počítač, sa spustenie GNU/Linuxu najčastejšie rieši inštaláciou boot managera. Tento sa väčšinou inštaluje do MBR sektora (Master Boot Record) a prepíše záznam, ktorý vytvoril MS Windows. Množstvo distribúcií pri inštalácií správne spozná iný operačný systém a pridá jeho odkaz do ponuky či LILO alebo GRUB managera.

Problém však nastane, ak chceme GNU/Linux odstrániť. Ak jednoducho vymažeme GNU/Linux oddiel, tak stratíme konfiguračné súbory a boot manager nám automaticky nezobrazí žiadnu ponuku. Existujú postupy, ako naštartovať MS Windows, prípadne opraviť tento stav, ale na určitú dobu sa počítač stáva nepoužiteľným. 

_Poznámka: v MS Windows 95/98 existoval príkaz `fdisk /MBR`, ktorým sa po takomto zásahu dal obnoviť MBR do pôvodného stavu. V MS Windows 2000 a XP však už neexistuje._

Tento článok popisuje inštaláciu boot managera takým spôsobom, aby takéto problémy nenastali.

Pre popis platia nasledujúce obmedzenia:

*   Celá MS Windows inštalácia je na jednom disku/partícií.
*   Ako boot manager je použitý GRUB.
*   Článok sa nebude podrobnejšie venovať boot managerom, ich funkciám alebo možnostiam.
*   Len pre úplnosť, okrem známych GNU/Linux boot managerov, ako GRUB alebo LILO, existuje v MAC OS - BootX a pre MS Windows XP - WinXP Bootloader (NTLDR).

## Pridanie operačného systému GNU/Linux

Nižšie je stručný popis, ako neprepísať MBR sektor, vytvorený inštaláciou MS Windows, ale nainštalovať GRUB na druhú partíciu a na jeho spúšťanie použiť WinXP bootloader.

**Výhody:**

*   Kedykoľvek je možné odstrániť GNU/Linux partíciu a MS Windows je stále spustiteľný bez problémov.

**Nevýhody:**

*   Komplikovanejšia inštalácia ako v prípade priameho prepísania MBR sektora.

### Vytvorenie novej partície

V ďalšom postupe predpokladám, že je MS Windows nainštalovaný na jednej súvislej partícií. Pred vytvorením novej partície doporučujem vykonať defragmetáciu existujúceho disku. Miesto na novú GNU/Linux partíciu spravíme zmenšením pôvodnej a to "od konca". Na uvoľnenom mieste vytvoríme minimálne dve partície, pre:

*   koreňový adresár - samotný systém GNU/Lunuxu a
*   swap súborový systém.

Občas je užitočné vytvoriť ešte jednu partíciu, slúžiacu na prenos súborov medzi GNU/Linuxom a MS Windowsom. Aby bola viditeľná aj z MS Windowsu, nastavíme jej typ FAT32\. Úplne však postačuje USB kľúčenka, prípadne prepisovateľné CD/DVD. Na schéme nižšie je za MS Windows súborovým systémum NTFS os veľkosťou 31,5 GB zaradená partícia typu ext3 s veľkosťou 8 GB a swap s veľkosťou 500 MB.

![](http://www.valasek.biz/_/rsrc/1219608396041/na-stiahnutie/DiskPartitions.png)

Na vytvorenie jednotlivých oddielov disku sa perfektne hodia live CD typu GParted live CD obsahujúci nástroj GParted alebo Knoppix obsahujúci QTParted. V MS Windowse je možné použiť komerčný nástroj Partition Magic.

### Inštalácia GNU/Linuxu

Následne je nutné nainštalovať požadovanú distribúciu GNU/Linuxu. Pred samotným zahájením inštalácie doporučujem overiť, či inštalačný program umožňuje vybrať, kde bude GRUB nainštalovaný. Niektoré inštalačné programy to neumožňujú! Samozrejme GRUB/LILO nainštalujeme do druhej partície.

### Export MBR záznamu

Po inštalácii GRUBu musíme získať jeho obraz zo začiatku druhej partície. To spravíme príkazom `sudo dd if=/dev/hda2 of=linux.bin bs=512 count=1` a súbor "linux.bin" prenesieme na kľúčenku alebo vytvorenú FAT32 partíciu.

_Poznámka: Príkaz "dd" skopíruje počet bajtov zadaných parametrom "bs" zo vstupného súboru "if" do výstupného súboru zadaného parametrom "of". V príklade je vstupným súborom partícia /dev/hda2, kde sme inštalovali GNU/Linux (u Vás sa môže líšiť), a výstupným súborom je súbor "linux.bin"._

Ak export MBR sektoru nie je možné spraviť v priebehu inštalácie, nestáva nám nič iné ako použitie niektorého z GNU/Linux live CD. Ak by sme v tomto čase reštartovali počítač a všetko sme doteraz robili správne, tak naštartuje MS Windows a okrem zmenšenia veľkosti disku pre MS Windows nie je vidieť žiadnu zmenu. Ako live CD doporučujem Knoppix, umožňuje jednoduché pripojenie existujúcich diskových oddielov. Následné spustenie príkazu `sudo dd if=/dev/hda2 of=linux.bin bs=512 count=1` v konzole a kópia výsledného súboru na USB kľúčenku nie je problém.

### Úprava WinXP bootloaderu

Ak to zhrnieme, tak máme:

1.  nainštalovaný GNU/Linux - na druhej partícií,
2.  nainštalovaný GRUB, ale na druhej partícií, a nedokážeme ho zatiaľ spustiť.

Ostáva nám už len správne nastavenie Windows bootloadera, aby zobrazoval menu na spustenie MS Windowsu alebo GNU/Linuxu. Toto menu je uložené v súbore `boot.ini`, ktorý upravíme nasledujúcim spôsobom:

1.  Urobte zálohu súboru "boot.ini".
2.  Prekopírujte súbor "linux.bin" na disk C:\ do koreňového adresára.
3.  Odstráňte súboru "boot.ini" read-only príznak.
4.  Otvorte ho v Notepade a na koniec pridajte riadok `C:\linux.bin="Ubuntu Linux"`. Uvedomte si, že tam už podobný riadok môže byť, s textom "Unknown Operating System", tak ho len upravte. Ak chcete, môžete skrátiť aj čas na rozhodovanie a zobrazenie menu pri štarte počítača z 30 na 10 alebo 5 sekúnd.
5.  Vráťte príznak súboru "boot.ini" na read-only.
6.  Reštartujte systém.

Pre ilustráciu prikladám výsledný tvar súboru "boot.ini":

    [boot loader]
      timeout=10
      default=multi(0)disk(0)rdisk(0)partition(1)\WINDOWS
    
    [operating systems]
      multi(0)disk(0)rdisk(0)partition(1)\WINDOWS="Microsoft Windows XP Professional" /noexecute=optin /fastdetect C:\ubuntu.bin="Ubuntu GNU/Linux

Správnosť úpravy súboru si môžete overiť nasledovne:

1.  Kliknite pravým tlačidlom myši na položku **Tento počítač** a potom kliknite na položku **Vlastnosti**.-alebo- Kliknite na tlačidlo **Štart**, kliknite na príkaz **Spustiť**, zadajte príkaz `sysdm.cpl` a potom kliknite na tlačidlo **OK** - otvorí sa okno vlastností, zobrazené nižšie.
2.  Na karte **Spresnenie** kliknite na tlačidlo **Nastavenie** v poli **Spúšťanie a obnovovanie**.
3.  V poli **Spustenie systému** kliknite na tlačidlo **Upraviť** - otvorí sa okno štartu a obnovy systému, zobrazené nižšie.

![](http://www.valasek.biz/_/rsrc/1219608396126/na-stiahnutie/SystemProperties.png)
![](http://www.valasek.biz/_/rsrc/1219608396234/na-stiahnutie/StartupAndRecovery.png)

Áno, skutočne to je MS Windows ale práve som používal túto tému a preto dialógy vypadajú ako z MAC OS.

## Odstránenie operačného systému GNU/Linux

Na odstránenie GNU/Linuxu stačí:

*   Modifikovať vyššie popísaným spôsobom súbor "boot.ini".
*   Spraviť reštart počítača.
*   Vymazať GNU/Linux partíciu napríklad zrušením ext3 a swap oddielov pomocou programu GParted a rozšíriť na voľné miesto pôvodne zmenšenú NTFS partíciu.

## Pár upozornení na záver

Pred samotnou zmenou veľkostí diskových oddielov a inštaláciou GNU/Linuxu Vám doporučujem:

*   Buďte opatrný a každý krok si dvakrát premyslite predtým, ako ho vykonáte.
*   Vždy robte veci až vtedy, keď máte pocit, že viete, čo robíte. Inak si ich doštudujte v dokumentácií.
*   Zálohujte si dáta na počítači !!!
*   Stiahnite si Live CD:
    *   Na repartíciu disku doporučujem GParted live CD (vie zmeniť veľkosť NTFS oddielov).
    *   Ako zálohu doporučujem stiahnuť KNOPPIX, bude sa Vám hodiť i neskôr pri problémoch s počítačom.

## Odkazy a zdroje

*   Boot loaders:
    *   [GRUB](http://en.wikipedia.org/wiki/GRUB)
    *   [LILO](http://en.wikipedia.org/wiki/LInux_LOader)
    *   [Booting Mac OS X](http://www.kernelthread.com/mac/osx/arch_boot.html)
    *   [MS Windows boot loader - NTLDR](http://en.wikipedia.org/wiki/NTLDR)
*   GNU/Linux live CD:
    *   [Knoppix](http://www.knoppix.org/)
    *   [System Rescue CD](http://www.sysresccd.org/Main_Page)
    *   [GParted](http://gparted.sourceforge.net/)
*   Ostatné odkazy
    *   [How to dual boot Ubuntu and Windows XP without changing the Windows MBR (use NTLDR)](http://ubuntuforums.org/showthread.php?t=80508)
    *   [Dual Booting Ubuntu Linux and Windows XP on a Toshiba Laptop](http://www.crhc.uiuc.edu/%7Emjmille2/howtos/dual-boot-linux-and-windows/)
    *   [Creating a Dual-Boot Windows XP and Ubuntu Laptop](http://www.linuxdevcenter.com/pub/a/linux/2006/05/08/dual-boot-laptop.html)
