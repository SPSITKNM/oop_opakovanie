
# Modularita 2024/25

### Modul?

### Osnova hodiny
- Vývoj programovania
- Modularita
- Príklad

### Vývoj programovania

#### Paradigmy programovania
- Ako a prečo sa jazyky vyvíjajú?
- V čom sa OOP líši od predchádzajúcich paradigiem?
- Aspekty kvality softvéru.

#### Veľké projekty
- Programovanie veľkých projektov je kvalitatívne odlišné od vytvárania malých programov.
- Dôvodom na úvahy o princípoch programovania bola a je rastúca komplexnosť počítačových programov.

#### Paradigmy
- Imperatívne programovanie (popisujeme **AKO** sa rieši)
- Deklaratívne programovanie (popisujeme **ČO** sa rieši)
- Funkcionálne programovanie
- Logické programovanie
- Modulárne programovanie
- Objektovo orientované programovanie

### Imperatívne programovanie
- Procedurálne programovanie
- Postupnosť krokov, ktorými meníme stav premenných programu.
- Štruktúrované programovanie
- Sekvencie, iterácie, vetvenia, skoky, abstrakcie.
- Tak, ako to dnes poznáme z bežne používaných jazykov.

### Modulárne programovanie
- Návrh zhora-nadol.
- Rozdelenie programu na nezávislé, zameniteľné moduly, ktoré zabezpečujú čiastkovú funkcionalitu.
- Modul obsahuje všetko potrebné na zabezpečenie funkcionality (dáta a algoritmy).

### Objektovo orientované programovanie

#### Faktory kvality softvéru
- Vnútorné a vonkajšie faktory.
- Vnútorné sú skryté používateľovi. (AKO)
- Vonkajšie popisujú správanie navonok. (ČO)
- Musíme vedieť merať kvalitu.

#### Vonkajšie faktory
- Správnosť
- Robustnosť
- Rýchlosť, rozšíriteľnosť, použiteľnosť, kompatibilita, ...

#### Kľúčové faktory

**Robustnosť?**
- Náklady na robustnosť môžu byť vyššie než náklady vynaložené na správnosť.
- Robustnosť nie je cieľom predmetu OOP, preto ju nebudeme vyžadovať...
- ... a budeme teda vždy predpokladať správne vstupy.

### Ďalšie faktory

### Modularita

#### Modul
- Metóda konštrukcie softvéru je modulárna, ak je založená na dekompozícii, ktorá pomáha návrhárom decentralizovať architektúru a tvoriť softvérové systémy zložené z autonómnych prvkov, modulov, prepojených do jednoduchých a zrozumiteľných štruktúr.

#### Modularita programu
- Pochopiteľnosť
- Samostatnosť
- Kombinovateľnosť
- Zapúzdrenie
- Explicitné rozhranie
- Syntaktická podpora

#### Pochopiteľnosť
- Modul by mal vykonávať jednu jasne definovanú a pochopiteľnú úlohu, prípadne niekoľko málo jasne definovaných úloh.

#### Samostatnosť
- Každý modul musí byť relatívne samostatný a mal by mať čo možno najmenší počet väzieb na ostatné moduly.
- Nebolo by vhodné, aby boli všetky moduly programu navzájom prepojené a na sebe závislé.
- Moduly by sme tak nemohli individuálne otestovať, pochopiť ani preniesť do iného projektu.

#### Kombinovateľnosť
- Moduly musia byť navzájom kombinovateľné. Musí byť možné modul vziať a použiť ho v inom kontexte alebo aj v inom projekte.

#### Zapúzdrenie
- Moduly musia mať právo na isté súkromie: je prípustné a žiaduce, aby všetky informácie, ktoré nie sú potrebné pre klientov modulov, zostali skryté vnútri modulu.
- V praxi sa ukazuje, že väčšina funkcionality modulu je skrytá a len malá časť je viditeľná navonok.
- Skrytej časti hovoríme implementácia modulu a verejnej časti hovoríme rozhranie (interface) modulu.

#### Explicitné rozhranie
- Z deklarácie modulu musí byť všeobecne zrejmé, aké predpoklady pre vykonávanie svojej úlohy potrebuje.

#### Syntaktická podpora
- Moduly počítačového programu musia byť jasne vymedzené syntaktickými jednotkami programu.
- Zo zápisu programovacieho jazyka musí byť zrejmé, kde začína a kde končí zápis jedného modulu.
- Nie je napríklad možné, aby v kompaktnom programe patrili modulu len niektoré časti, zatiaľ čo iné časti modulu nepatrili.

### Päť kritérií a pravidiel modularity
- Dekomponovateľnosť
- Kombinovateľnosť
- Pochopiteľnosť
- Kontinuita
- Ochrana
- Priame mapovanie
- Pár rozhraní
- Malé rozhrania (weak coupling)
- Explicitné rozhranie
- Skrytie informácií

### Kritériá
- dekomponovateľnosť, kombinovateľnosť, pochopiteľnosť
   
### Kritériá kontinuita, ochrana

### Pravidlá
- priame mapovanie, pár rozhraní, malé rozhrania
   
### Pravidlá
- explicitné rozhranie, skrytie informácií
  
### Príklad

### Trieda vs Objekt
- Trieda ako statický popis.
- Objekt ako runtime (behová) reprezentácia:
  - stav (dáta)
  - správanie (algoritmy)

### Terminológia
- Trieda
- Členská funkcia, metóda
- Členská položka, premenná
- Objekt, inštancia triedy, this (vykonávateľ metódy)
- Konštruktor, destruktor

### Deklarácia triedy

### Implementácia (definícia) triedy

### Použitie triedy 1

### Použitie triedy 2

### Výsledok

### Použitie triedy 3

### Konštruktor a destruktor
- Konštruktor inicializuje dáta objektu hodnotami parametrov v konštruktore (naplní pamäť dátami).
- Destruktor odstráni z pamäte dáta objektu (čistí pamäť).
- Destruktor nie je potrebný, ak sú dáta objektu statické.

### Úlohy na cvičenie
- Implementujte triedu `KeyValue` podľa prednášky a vytvorte zreťazenú lineárnu štruktúru mnohých (napr. tisícov) objektov a pracujte s ňou (vypíšte napr. všetky kľúče od prvého do posledného objektu).
- Vytvorte podobnú triedu ako `KeyValue`, ale s hodnotou aj kľúčom typu (triedy) `string` a s dvoma susediacimi (next) objektmi. Výsledkom bude tzv. strom.
- Implementujte štruktúru (rozhodovací strom) na identifikáciu zvierat alebo rastlín. Kľúčom uzla stromu je rozhodovacie kritérium, hodnotou uzla je názov zvieraťa alebo rastliny, resp. druhu a pod. Naplňte kľúč aspoň desiatimi objektmi a vypíšte celú štruktúru na obrazovku.

### Kontrolné otázky
- Čo je hlavným motívom pre vývoj programovacieho paradigmatu od imperatívneho k objektovému?
- Čo je imperatívne programovanie?
- Čo je modulárne programovanie?
- Aké sú hlavné faktory kvality softvéru?
- Čo je pochopiteľnosť modulu? Uveďte príklad.
- Čo je samostatnosť modulu? Uveďte príklad.
- Čo je kombinovateľnosť modulu? Uveďte príklad.
- Čo je zapúzdrenie modulu? Uveďte príklad.
- Čo je explicitné rozhranie modulu? Uveďte príklad.
- Čo je syntaktická podpora modularity?
- Čo je päť kritérií pre dobrú modularitu?

---

# Objektovo orientované programovanie
## Návrh programu I 2024/25

### Osnova hodiny
- Čo vieme?
- Objektový návrh programu
- Príklad

### Čo vieme?

#### Trieda
- Trieda je popisom objektov so spoločnými vlastnosťami.

```cpp
class <meno> {
    private:
        <súkromné členské položky>
    public:
        <verejné členské položky>
};
```

- Členskými položkami môžu byť premenné (dáta) a metódy (funkcie).

#### Objekt
- Objekt je inštanciou – pamäťovou reprezentáciou – triedy.
- Objekt je reprezentáciou nejakej entity, ktorá má stav reprezentovaný dátami a správanie reprezentované metódami.

#### Konštruktor
- Konštruktor inicializuje objekty.
- Nemá návratovú hodnotu.
- Ak nie je deklarovaný, automaticky sa vytvorí implicitný konštruktor.
- Volá sa automaticky pri statickej deklarácii alebo použitím `new`.
- Konštruktorov môže byť viac, musia sa líšiť počtom alebo typom parametrov.

#### Destruktor
- Slúži na dealokáciu pamäte vytvorenej dynamicky.
- Nemá návratovú hodnotu.
- Ak nie je deklarovaný, automaticky sa vytvorí implicitný destruktor.
- Volá sa automaticky pri statickej deklarácii alebo použitím `delete`.

### Objektový návrh

#### Zadanie
- Majme malú banku s obmedzeným počtom klientov a účtov. V banke môžu klienti a účty pribúdať.
- Každý účet má jedného vlastníka a môže mať jedného partnera, obaja sú klienti banky a majú meno a kód. Na účty je možné vkladať a vyberať z nich, je možné zistiť stav na účte. Ak na účte nie je dostatok peňazí, nie je možné vybrať.
- Vklady na účtoch sú úročené, a to buď základnou alebo špeciálnou úrokovou sadzbou. Raz za čas banka všetkým účtom pripíše úrok zodpovedajúci úrokovej sadzbe.
- Účet resp. klienta je možné v banke vyhľadať podľa čísla resp. kódu.
- Je možné zistiť, ale nie meniť:
  - číslo účtu a jeho úrokovú sadzbu,
  - kód a meno klienta,
  - vlastníka a partnera účtu.

### Triedy
- Majme malú banku s obmedzeným počtom klientov a účtov. V banke môžu klienti a účty pribúdať.
- Každý účet má jedného vlastníka a môže mať jedného partnera, obaja sú klienti banky a majú meno a kód. Na účty je možné vkladať a vyberať z nich, je možné zistiť stav na účte. Ak na účte nie je dostatok peňazí, nie je možné vybrať.
- Vklady na účtoch sú úročené, a to buď základnou alebo špeciálnou úrokovou sadzbou. Raz za čas banka všetkým účtom pripíše úrok zodpovedajúci úrokovej sadzbe.
- Účet resp. klienta je možné v banke vyhľadať podľa čísla resp. kódu.

### Správanie
- Majme malú banku s obmedzeným počtom klientov a účtov. V banke môžu klienti a účty pribúdať.
- Každý účet má jedného vlastníka a môže mať jedného partnera, obaja sú klienti banky a majú meno a kód. Na účty je možné vkladať a vyberať z nich, je možné zistiť stav na účte. Ak na účte nie je dostatok peňazí, nie je možné vybrať.
- Vklady na účtoch sú úročené, a to buď základnou alebo špeciálnou úrokovou sadzbou. Raz za čas banka všetkým účtom pripíše úrok zodpovedajúci úrokovej sadzbe.
- Účet resp. klienta je možné v banke vyhľadať podľa čísla resp. kódu.

### Stav
- Majme malú banku s obmedzeným počtom klientov a účtov. V banke môžu klienti a účty pribúdať.
- Každý účet má jedného vlastníka a môže mať jedného partnera, obaja sú klienti banky a majú meno a kód. Na účty je možné vkladať a vyberať z nich, je možné zistiť stav na účte. Ak na účte nie je dostatok peňazí, nie je možné vybrať.
- Vklady na účtoch sú úročené, a to buď základnou alebo špeciálnou úrokovou sadzbou. Raz za čas banka všetkým účtom pripíše úrok zodpovedajúci úrokovej sadzbe.
- Účet resp. klienta je možné v banke vyhľadať podľa čísla resp. kódu.

### Trieda `Client`
- Kód a meno.
- Dá sa na ne spýtať.
- Nedajú sa meniť.

### Trieda `Account`
- Číslo a suma, vlastník a partner, úroková sadzba.
- Dá sa na ne spýtať.
- Číslo, úrokovú sadzbu, vlastníka a partnera nie je možné meniť.
- Vložiť, vybrať, zistiť stav, pripísať úrok.
- Niekedy nie je možné vybrať.

### Trieda `Bank`
- Obmedzený zoznam klientov a účtov.
- Možno pridať nového klienta a účet.
- Možno hromadne pripísať úrok podľa úrokovej sadzby.
- Možno vyhľadať klienta podľa kódu a účet podľa čísla.

### Príklad

### Deklarácia

#### Tri typy metód
- **Konštruktory a destruktor:** Konštruktory inicializujú stav objektu po jeho vzniku, destruktor uvoľňuje dynamicky pridelenú pamäť pred zánikom objektu. Ak nie sú uvedené, vytvoria sa tieto metódy automaticky (bez algoritmu).
- **Metódy poskytujúce informácie o stave objektu:** Metódy buď priamo podávajú informáciu o hodnote dátovej položky objektu alebo poskytujú informáciu na základe algoritmu.
- **Metódy meniace stav objektu:** Metódy buď priamo zmenia hodnotu dátovej položky objektu alebo vykonajú zmenu na základe algoritmu.
- **Metódy poskytujúce informácie o stave objektu by nemali meniť jeho stav!!!**

### Objektové kompozície
- Objekt sa môže stať súčasťou iného objektu a stáva sa tak jeho dátovou položkou.
- Vznikajú tak komponované objekty s presne definovanými kompetenciami. Tie môžu realizovať prostredníctvom interakcie objektov, z ktorých sú komponované.
- Napríklad účet má klientov v rolách vlastníka a partnera resp. banka má klientov a účty.
- Jeden a ten istý objekt môže byť súčasťou viacerých kompozícií. Napríklad jeden klient môže byť súčasťou ako účtu, tak banky.

### Úlohy na cvičenie
- Implementujte príklad z prednášky a navrhnite kód, ktorý bude používať všetky triedy. Vytvorte desiatky klientov a účtov v banke a nasimulujte niektoré bežné úkony vykonávané v banke.
- Navrhnite a implementujte podobnú úlohu, ako napríklad lekársku ordináciu, malú školu a pod.

### Kontrolné otázky
- Vysvetlite, ako vznikajú objekty triedy, pojem konštruktor a princípy práce s ním v C++ / C#.
- Vysvetlite, ako zanikajú objekty triedy, pojem destruktor a princípy práce s ním v C++ / C#.
- Vysvetlite rozdiel medzi statickou a dynamickou deklaráciou objektov v C++ / C#.
- Ako sa dá postupovať, ak chceme v zadaní programu nájsť triedy, ich metódy a dátové členy?
- Kedy a prečo potrebujeme použiť viac konštruktorov jednej triedy?
