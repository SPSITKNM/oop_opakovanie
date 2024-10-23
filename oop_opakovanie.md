
# Objektovo orientované programovanie

## Modularita 2024/25

### Modul?

### KeyValue Class

```cpp
class KeyValue
{
private:
    int key;
    double value;

public:
    KeyValue(int k, double v);
    int GetKey();
    double GetValue();
};
```

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


# KeyValue Class

```cpp
#include <iostream>
using namespace std;

class KeyValue
{
private:
    int key;
    double value;
    KeyValue *next;

public:
    KeyValue(int k, double v);
    ~KeyValue();
    int GetKey();
    double GetValue();
    KeyValue* GetNext();
    KeyValue* CreateNext(int k, double v);
};
```

Tento súbor obsahuje triedu `KeyValue`, ktorá má:
- **Súkromné členy:**
  - `int key;`
  - `double value;`
  - `KeyValue *next;`
- **Verejné metódy:**
  - Konštruktor `KeyValue(int k, double v);`
  - Destruktor `~KeyValue();`
  - Metóda `GetKey()`, ktorá vracia hodnotu kľúča.
  - Metóda `GetValue()`, ktorá vracia hodnotu premennej `value`.
  - Metóda `GetNext()`, ktorá vracia ukazovateľ na ďalší objekt.
  - Metóda `CreateNext(int k, double v)`, ktorá vytvorí ďalší objekt `KeyValue`.

### Implementácia (definícia) triedy

# KeyValue Class Implementation

```cpp
KeyValue::KeyValue(int k, double v)
{
    this->key = k;
    this->value = v;
    this->next = nullptr;
}

KeyValue::~KeyValue()
{
    if (this->next != nullptr)
    {
        delete this->next;
        this->next = nullptr;
    }
}

KeyValue* KeyValue::GetNext()
{
    return this->next;
}

KeyValue* KeyValue::CreateNext(int k, double v)
{
    this->next = new KeyValue(k, v);
    return this->next;
}
```

### Použitie triedy 1

# Main Function Example

```cpp
int main()
{
    KeyValue *kv1 = new KeyValue(1, 1.5);
    cout << kv1->CreateNext(2, 2.5)->GetKey() << endl;

    KeyValue *kv2 = kv1->GetNext();
    cout << kv2->GetNext() << endl;

    delete kv1;
    //delete kv2;

    cout << kv1->GetKey() << endl;
    cout << kv2->GetKey() << endl;

    getchar();
    return 0;
}
```

### Použitie triedy 2

# Main Function Example with KeyValue Class

```cpp
int main()
{
    KeyValue *kv1 = new KeyValue(1, 1.5);
    cout << kv1->CreateNext(2, 2.5)->GetKey() << endl;

    KeyValue *kv2 = kv1->GetNext();
    cout << kv2->GetNext() << endl;

    //delete kv2;  // Zakomentované, lebo pamäť uvoľňuje delete kv1
    delete kv1;

    cout << kv1->GetKey() << endl;
    cout << kv2->GetKey() << endl;

    getchar();
    return 0;
}
```

### Použitie triedy 3

# Main Function with Nullptr

```cpp
int main()
{
    KeyValue *kv1 = new KeyValue(1, 1.5);
    cout << kv1->CreateNext(2, 2.5)->GetKey() << endl;

    KeyValue *kv2 = kv1->GetNext();
    cout << kv2->GetNext() << endl;

    delete kv1;
    kv1 = nullptr;
    kv2 = nullptr;

    //cout << kv1->GetKey() << endl;
    //cout << kv2->GetKey() << endl;

    getchar();
    return 0;
}
```

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
## Triedy a objekty (objektová orientácia) 2024/25

### Osnova hodiny
- Objektový prístup (prečo potrebujeme objekty).
- Triedy, objekty,...
- Príklad.

### Prečo potrebujeme objekty?

#### Udržateľnosť softvéru (maintenance)
- Štúdia Lientz a Swanson (1980).
- 487 rôznych systémov.
- Koľko úsilia to vyžaduje?

#### Kedy to začalo?
- Jazyk Simula 67 (Ole-Johan Dahl a Kristen Nygaard, Norwegian Computing Center, 1960+)
  - triedy a inštancie (objekty)
  - automatické zanikanie objektov (garbage collection)
- Jazyk Smalltalk (Xerox PARC, Alan Kay a ďalší, 1970+)
  - pojem „objektovo-orientované programovanie“
  - použitie objektov a správ, ktoré si objekty posielajú a spracovávajú

### Objektová orientácia…
- Objektové techniky pomáhajú písať lepšie udržateľný softvér.
- Metóda a jazyk.
- Implementácia a prostredie.
- Knižnice.

### Metóda a jazyk
- Nejde len o programovací jazyk a spôsob jeho použitia.
- Ide aj o spôsob uvažovania a vyjadrovania...
- …a taktiež o záznamy v textovej alebo grafickej forme.

### Model domény
- Podpora vývoja.
- Vlastnosti a efektivita nástrojov pre vývoj.
- Nástroje pre podporu nasadzovania nových verzií.
- Nástroje pre podporu dokumentovania.

### Knižnice
- Objektové technológie veľmi spoliehajú na opakovanú použiteľnosť.
- Podpora vývoja formou využitia už implementovaných riešení (knižníc).
- Podpora vytvárania a správy nových vlastných knižníc.

### Máme byť dogmatickí?
- Objektovo orientovaný prístup sa dnes chápe ako základný nástroj pre vývoj softvéru. Avšak…
  - Existujú rôzne programovacie jazyky s rôznou mierou podpory techník objektového programovania (OOP).
  - Nie každý potrebuje všetky vlastnosti, ktoré OOP ponúka.
  - Objektová orientácia môže byť len jedným z faktorov úspešného vývoja, preto je potrebné uvažovať komplexnejšie.

### Metóda a jazyk – Triedy
- Triedy ako moduly.
- Triedy ako typy.
- Zasielanie správ (message passing, feature-based computation).
- Skrývanie informácií.
- Statická kontrola typov.
- Dedičnosť, redefinícia, polymorfizmus a dynamická väzba.
- Generickosť.
- Správa pamäte a garbage collection.

### Trieda
#### Triedy
- Objektovo orientovaný prístup je postavený na pojme trieda.
- Triedu môžeme chápať ako časť softvéru, ktorá popisuje abstraktný dátový typ a jeho implementáciu.
- Abstraktným dátovým typom rozumieme objekty so spoločným správaním reprezentovaným zoznamom operácií, ktoré objekty vykonávajú.

### Triedy ako moduly
- OOP je najmä o štruktúre (architektúre) softvéru, kde je dôležitá modularita.
- Triedy nepopisujú len typy objektov, ale musia byť zároveň modulárne jednotky.
- V čisto objektovo orientovaných programoch by nemali byť iné samostatné jednotky ako triedy (napr. funkcie).

### Triedy ako typy
- V čisto objektovo orientovaných jazykoch a programoch by nemali byť iné typy ako triedy.
- Platí to aj pre systémové typy ako INT alebo DOUBLE.

### Zasielanie správ
- Message passing (feature call), feature-based computation je výpočtový mechanizmus.
- Objektu ako inštancii triedy je zaslaná správa daného mena a s potrebnými parametrami.
- Napr. `aPerson->ChangeLastName(“Smith”)`.
- Ten, kto zasiela správu (požaduje vykonanie operácie s určitými argumentmi), je KLIENT triedy.

### Skrývanie informácií
- Pre klienta sú dôležité iba tie operácie (metódy), ktoré popisujú vonkajšie správanie objektov triedy.
- Detaily implementácie by mali zostať skryté (dáta + pomocné operácie).
- Ak klient potrebuje získať informácie o stave (dátach) objektu, dostane sa k nim len prostredníctvom zaslania správy (volaním metódy, nie premennej).

### Statická väzba a kontrola typov
- Každá entita v programe (napr. premenná daného mena) musí mať definovaný typ.
- Požiadavka na objekt (zaslanie správy) musí zodpovedať operácii (metóde), ktorú trieda poskytuje.

### Generickosť
- Potreba existencie tried, ktoré vedia pracovať s typom, ktorý nie je vopred známy.
- Napr. zoznamy, do ktorých možno ukladať objekty rôznych tried (typov).

### Dedičnosť a redefinícia
- Dedičnosť znamená založenie novej triedy na základe už existujúcej triedy.
- Základom je rozšírenie pôvodnej triedy o nové vlastnosti.
- Dedičnosť taktiež umožňuje zmeniť niektoré vlastnosti pôvodnej triedy.

### Polymorfizmus a dynamická väzba
- Potreba, aby ten istý objekt vystupoval v rôznych kontextoch v rôznych rolách.
- Rolou rozumieme rôzne správanie, ktoré sa môže meniť v čase.

### Správa pamäte a garbage collection
- V rozsiahlych programoch vzniká a zaniká mnoho objektov, a to v rôznych a nie vždy jednoduchých situáciách.
- Je problém manuálne sledovať životný cyklus objektov.
- V moderných jazykoch je zanikanie objektov potrebné automatizovať.

### Príklad
#### Deklarácia
- Konštruktor inicializuje objekt (plní pamäť dátami, ktoré objekt používa).
- Destruktor odstraňuje dáta objektu (uvoľňuje pamäť, ktorú objekt zaberá).

#### Použitie
- Použitie kľúčového slova `new` zabezpečí vznik objektu (alokuje pamäť pre dáta („plochú“ časť) objektu).

#### Výsledok
- Definícia (implementácia).

### Úlohy na cvičenie
- Implementujte príklad z prednášky a do triedy `KeyValues` pridajte metódu `KeyValue* RemoveObject(int k)`, ktorá odstráni objekt s daným kľúčom a vráti ukazovateľ na neho.
- Implementujte triedu `Faktura`, ktorá bude obsahovať číslo, objekt triedy `Osoba` (s menom a adresou) a pole objektov `PolozkaFaktury` (s názvom a cenou). Navrhnite konštruktor a destruktor a ďalšie potrebné metódy. Faktura bude mať metódu (funkciu), ktorá vypočíta a vráti celkovú cenu.

### Kontrolné otázky
- Aké sú hlavné príčiny potreby zmien softvéru?
- Aké sú hlavné faktory ovplyvňujúce objektovú orientáciu?
- Vysvetlite, čo rozumieme pojmom objektovo orientovaná metóda (prístup) a jazyk.
- Vysvetlite, čo rozumieme podporou objektovo orientovanej implementácie.
- Vysvetlite, čo rozumieme podporou opakovanej použiteľnosti.
- Vysvetlite pojmy trieda a objekt a použite správnu terminológiu.
- Zdôraznite vlastnosti triedy z pohľadu modularity.
- Vysvetlite princíp zapuzdrenia v OOP.
- Vysvetlite princíp zasielania správ.
- Vysvetlite princípy deklarácie a definície jednoduchej triedy v C++.
- 
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

--- 

# Objektovo orientované programovanie
## Objektová dekompozícia a trieda ako objekt 2024/25

### Osnova hodiny
- Čo je lepšie? Funkcie alebo objekty?
- Môže byť trieda zároveň objektom?
- Príklad.

### Funkcie alebo objekty?

#### Funkcie vs objekty
- Je lepšie založiť štruktúru programu na funkciách alebo dátach?
- Na návrh systému môžeme nahliadať dvoma spôsobmi:
  - Ako na sadu funkcií (odpovedá na otázku, **ČO** systém bude robiť).
  - Ako na sadu objektov, ktoré spolupracujú (odpovedá na otázku, **KTO** bude zabezpečovať funkčnosť).

#### Problémy
- Rozšíriteľnosť
- Opakovaná použiteľnosť
- Kombinovateľnosť

### Príklad zadania
- Majme malú banku s obmedzeným počtom klientov a účtov. V banke môžu klienti a účty pribúdať.
- Každý účet má jedného vlastníka a môže mať jedného partnera, obaja sú klienti banky a majú meno a kód. Na účty je možné vkladať a vyberať z nich, je možné zistiť stav na účte. Ak na účte nie je dostatok peňazí, nie je možné vybrať.
- Vklady na účtoch sú úročené buď základnou alebo špeciálnou úrokovou sadzbou. Raz za čas banka všetkým účtom pripíše úrok zodpovedajúci úrokovej sadzbe.
- Účet resp. klienta je možné v banke vyhľadať podľa čísla resp. kódu.

### Funkcie alebo objekty?
- Zhora nadol alebo naopak?
- Prečo objekty?

### Triedy ako objekty? Prečo?

#### Trieda ako objekt
- Objektovo orientovaný prístup všeobecne vychádza z predpokladu, že „všetko je objekt“ (teda aj typy sú objekty).
- Môže byť trieda objektom? A za akých podmienok?
- Objekty majú svoj stav a správanie...

#### Stav a správanie triedy
- Stav je reprezentovaný dátami.
- Správanie je reprezentované metódami.
- Musí byť splnené zapuzdrenie a skrytie informácií.
- Triede sa musí dať zaslať správa (zavolať jej metódu).

### Príklad

#### Deklarácia a definícia
#### Použitie

### Ako to funguje...
- Dáta a metódy deklarované ako „static“ patria triede.
- Prístup k nim však majú aj objekty (inštancie) triedy.
- Je potrebné rozlišovať medzi triednymi a inštančnými premennými a metódami.

### Vhodné konvencie
- V kontexte triedy sa pri prístupe k dátam alebo metódam nemusí uvádzať adresát správy.
- Pre zabránenie nedorozumeniam je vhodné:
  - pre prístup k inštančným dátam/metódam používať formu `OBJECT_NAME->METHOD_NAME`
  - pre prístup k triednym dátam/metódam používať formu `CLASS_NAME::METHOD_NAME`

### Adresát správy
- Adresátom správy je buď:
  - objekt (inštancia) tejto triedy v prípade inštančnej premennej alebo metódy,
  - alebo sama trieda v prípade triednej (static) premennej alebo metódy.

### Kde je rozdiel?

#### Trieda bez objektov

### Konštruktor? Destruktor?
- Trieda existuje po celý čas behu programu.
- Ak má trieda triedne (static) premenné, musíme ich inicializovať zvlášť.
- Konštruktor ani destruktor pre triedu ako objekt neexistuje.

### Kto o kom vie?
- Prostredníctvom konštruktora triedy vytvárame objekty (inštancie), ale trieda o nich nič nevie.
- Z triednej metódy nie je možné pristupovať k členským položkám objektu.
- Objekty (inštancie) triedy majú prístup k členským (static) položkám triedy (pri použití nemusí byť jasné, s akou položkou pracujeme).

### Čo je správne volanie?

### Kedy použiť triedu ako objekt?
- Vytvorenie knižnice funkcií (napr. matematika).
- Potrebujeme, aby objekty (inštancie) zdieľali spoločné dáta.
  - Napr. evidencia počtu objektov (inštancií) triedy.

### Upravte triedu pre počítanie objektov
#### Deklarácia a definícia

### Úlohy na cvičenie
- Implementujte príklady z prednášky a doplňte do tried `Client` a `Account` počítanie existujúcich objektov.
- Navrhnite a implementujte ďalšie príklady členských položiek tried. Napríklad rovnaká úroková sadzba pre všetky účty, ktorým nebola sadzba zadaná v konštruktore a ktorú je možné prostredníctvom metódy triedy zmeniť.

### Otázky
- Aký je rozdiel medzi funkčnou a objektovou dekompozíciou programu?
- Prečo preferujeme objektovú dekompozíciu a aké sú hlavné problémy funkčnej dekompozície?
- Za akých podmienok môžeme považovať triedu za objekt a ako to implementovať v C++?
- Vysvetlite rozdiel medzi členskými položkami triedy a inštancie a popíšte ich dostupnosť.
- Ako môžeme v C++ dôsledne odlišovať prácu s členskými položkami tried a inštancií?
- Potrebuje trieda v roli objektu konštruktor resp. destruktor a prečo?

---


# Objektovo orientované programovanie
## Úvod do dedičnosti 2024/25

### Osnova hodiny
- Čo rieši dedičnosť?
- Príklad.
- Dedičnosť – základný princíp.

### Čo rieši dedičnosť?

#### Čo sa rieši?
- Znovu-použiteľnosť
  - Nechceme znova opisovať (kopírovať) kód, ktorý sme už raz napísali a odladili.
- Rozšíriteľnosť
  - Chceme rozšíriť (pozmeniť) kód, ktorý sme už...

### Úloha triedy?
- Znovu-použiteľnosť a rozšíriteľnosť v kontexte používania tried môžeme chápať ako:
  - Kombinovanie s inými triedami, skladanie
  - Rozšírenie o nové správanie
  - Pozmenenie existujúceho správania

### Skladanie vs dedičnosť
- Skladaním dosiahneme, že objekt jednej triedy je zložený z objektov inej triedy.
  - Ide o vzťah „MÁ“.
- Dedičnosťou dosiahneme, že nová trieda je rozšírením alebo špeciálnym prípadom existujúcej triedy (alebo viacerých tried).
  - Ide o vzťah „JE“.

### Príklad

#### Čo je na triede `Account` nesprávne?
- Účet s partnerom je rozšírením účtu bez partnera.
- Účet s partnerom **JE** účet.
- Môžeme využiť dedičnosť. Ako?

### Deklarácia predka

### Deklarácia potomka

#### Implementácia konštruktorov
- Potomok `PartnerAccount` použije na inicializáciu členských položiek konštruktor rodiča `Account`, ktorému odovzdá potrebné inicializačné hodnoty.

### Použitie (zastupiteľnosť)

#### Banka s účtami dvoch typov

- Malo by to fungovať? A prečo?

### Dedičnosť – základný princíp

### Terminológia
- Predok – potomek, priamy predok – potomek
- Rodič – dcéra (syn)
- Nadriadená (super, báza) trieda – podradená (sub) trieda

### Vzťahy v dedičnosti
```
A
|__ B
    |__ C
```
- `A` je báza triedy `B`, A je rodič `B`, A je predok `C`
- `B` je báza triedy `C`, trieda B dedí z triedy A, B je rodič C
- `C` dedí z B aj A, C je dcérska trieda triedy B, C je potomek A a priamy potomek B.

### Príklady
- Vozidlo – bicykel, motorka, osobné auto
- Osoba – užívateľ, správca
- Kolekcia – zoznam, množina

#### Nesprávne?
- Auto – Škoda
  - Škoda je **ZNAČKA** osobného auta.
- Strom – smrek
  - Smrek je **DRUH** ihličnatého stromu.

### Generalizácia - špecializácia
- Nezamieňať vzťah „je inštanciou“ a „dediť z“.
  - „je inštanciou“ je vzťah medzi triedou a objektom
  - „dediť z“ je vzťah medzi triedami.
- Vzťah dedičnosti definuje vzťah **VŠEOBECNÝ** – **ŠPECIALIZOVANÝ**
  - Potomek by teda mal reprezentovať špeciálny prípad predka...
  - ... a predok by mal reprezentovať zobecnenie svojich potomkov.

### Inak povedané...
- Predok definuje spoločné správanie všetkých svojich potomkov.
- Potomkovia môžu toto správanie rozšíriť alebo pozmeniť.
- Potomkovia sa nemôžu tohto správania zbaviť.
- A teda:
  - Dedí sa všetko bez výnimky!!!
  - Dedí sa aj miera skrytia informácií...

### Vzťah skladania a dedičnosti
- Skladanie – „MÁ“ vs dedičnosť „JE“.
- Dedičnosť môžeme chápať ako dôsledok skladania.
  - Inštancia triedy potomka obsahuje všetko, čo má inštancia triedy predka.

### Hierarchia
- Pri použití dedičnosti vznikajú hierarchie tried.
- V našom prípade pracujeme s jednoduchou dedičnosťou.
  - Každý potomek má práve jedného priameho predka.
  - Predok môže mať viac priamych potomkov.
- V prípade jednoduchej dedičnosti je touto hierarchiou strom.
- Nezamieňať hierarchiu objektov (kompozícia) a hierarchiu tried (dedičnosť).

### Liskov princíp substitúcie
- Barbara Liskov 1987. Data abstraction and hierarchy.
- Bertrand Meyer. Invarianty správania.
- Potomek môže vždy nahradiť predka...
  - ... a to preto, že majú spoločné správanie.
  - Naopak to neplatí...

### Vznik potomka
1. Volanie konštruktora objektu.
2. Volanie konštruktora priameho predka.
3. Vykonanie konštruktora priameho predka.
4. Vykonanie konštruktora objektu.

### Úlohy na cvičenie
- Implementujte príklad z prednášky a vytvorte banku s mnohými klientmi a účtami. Zamerajte sa na pochopenie princípu zastupiteľnosti a na to, ako fungujú konštruktory v dedičnosti.
- Navrhnite a implementujte ďalšie jednoduché príklady dedičnosti s rozšírením spoločného stavu a správania, ako napríklad Auto, Osobné auto, Nákladné auto.

### Kontrolné otázky
- Ktoré dva kľúčové požiadavky riešime pomocou dedičnosti?
- Aké návrhové požiadavky máme na použitie tried (čo s nimi môžeme robiť)?
- Aký je rozdiel medzi dedičnosťou a skladaním? Čo majú spoločné?
- V akých rolách vystupujú triedy v dedičnosti? Použite správnu terminológiu.
- Vysvetlite, v akom vzťahu je trieda, z ktorej sa dedí, s triedou, ktorá dedí.
- Čo všetko sa dedí, čo nie a prečo?
- Čo rozumieme jednoduchou dedičnosťou a ako s tým súvisí hierarchia tried v dedičnosti?
- Čo je Liskov princíp substitúcie a ako sa prejavuje v dedičnosti?
- V akom poradí sa volajú a vykonávajú konštruktory pri použití dedičnosti?

---

# Objektovo orientované programovanie
## Dedičnosť – zmena správania 2024/25

### Osnova hodiny
- Rozšírenie správania.
- Zmena správania.
- Príklad.

### Rozšírenie správania

#### Keď rozširujeme správanie...
- Môžeme bezpečne použiť to, čo už máme.
- Nehrozí žiadny problém s pochopením, ako sa objekt správa.
- Objekt vystupuje sám za seba...
  - ...alebo za niektorého zo svojich predkov.

### Paradox špecializácie a rozšírenia
- Vzťah dedičnosti je vzťahom **všeobecný - špeciálny**.
- Potomok je teda špeciálnym prípadom predka.
- Paradoxne však, pri rozšírení dochádza k tomu, že potomok vie viac, ako ktorýkoľvek z jeho predkov.

### ...a teda
- Čím bohatšie správanie uvažujeme, tým menej tried ho poskytuje.
- V dedičnej hierarchii je najmenšie spoločné správanie definované v spoločnom predkovi.
- Koncové triedy tejto hierarchie majú najbohatšie správanie (každá trochu iné).

### Nesprávny príklad
- Potreba rozšírenia sama o sebe nie je dostatočná pre použitie dedičnosti.
- Napr. vzťah bodu a kružnice, mohli by sme potrebovať rozšíriť bod o prácu s polomerom (nové správanie).
- Je to dostatočné, aby sme sa rozhodli použiť dedičnosť?

#### Nie!!!
- Nie je splnená podmienka špecializácie (kružnica nie je špeciálnym prípadom bodu).

### Zmena správania

#### Zmena správania
- Ak je správanie deklarované v predkovi, môžeme ho v potomkovi deklarovať znova.
- Existuje potom viac metód rovnakého mena.
- Deklarované správanie potom musíme v potomkovi implementovať (aby bolo vykonateľné).
- Deklarované správanie nemusí byť implementované v predkovi.

### Pretíženie ako rozšírenie správania

#### Pretíženie
- Pretížením rozumieme situáciu, keď daná metóda má rovnaké meno, ale má:
  - iné parametre,
  - iné typy parametrov,
  - iný typ návratovej hodnoty.
- Pretíženie však nie je zmena správania, aj keď má metóda rovnaké meno.

#### Typy pretíženia
- Názov metódy zostáva rovnaký.
- Iný počet parametrov.
- Iné dátové typy parametrov.
- Iná návratová hodnota (nie v C++).
- Možno kombinovať.

### Prekrytie
- Prekrytím rozumieme situáciu, keď metóda potomka má rovnakú deklaráciu ako metóda predka (rovnakú signatúru).
- Potomok dedí aj metódu predka. Má teda dve metódy s rovnakou deklaráciou.

#### Kedy použiť prekrytie?
- Typickým príkladom použitia pretíženia sú konštruktory.
- Typickým príkladom použitia prekrytia je skutočná zmena správania potomka.
  - Príkladom môže byť metóda na výber peňazí z rôznych typov účtov v banke.

### Príklad

#### Deklarácia predka

### Prekrytie
- Deklarujeme triedu `CreditAccount`.
- Prekryjeme metódu `CanWithdraw`.
  - Má rovnakú signatúru, ale inú definíciu.
  - Dôsledok: V triede `CreditAccount` bude inštančná metóda `CanWithdraw` dvakrát!!!

#### Deklarácia potomka

#### Definícia

#### Definícia (pripomenutie)

#### Použitie

### Výsledok?

### Sme hotoví?
- Nie!!!
- Ako vyberieme z účtu (ak môžeme), keď nemáme prístup k členskej premennej `balance`?
- Aké máme možnosti?

#### Vlastná metóda?

### Máme problém...

#### Aké teda máme možnosti?
- Public prístup k dátovej položke?
- Porušenie zapuzdrenia?
- Alebo inak?

### Nový predok

#### Funguje, ale...
- Máme rovnaký kód dvakrát.
- Porušujeme zapuzdrenie.
- Pri zastúpení predka potomkom sa použijú rôzne metódy.

### Výsledok

#### Porušenie zapuzdrenia
- Pri zmene správania môže vzniknúť potreba pracovať so súkromnou časťou predka.
- Ide samozrejme o porušenie zapuzdrenia a toho si musíme byť vedomí...
  - ...ale každé rozumné pravidlo má nejaké výnimky.

#### Dá sa zavolať metóda predka?
- Je to rovnaké ako volanie statickej metódy.
  - Z potomka voláme originálnu metódu.
  - `Account::CanWithdraw(a);`

### Úlohy na cvičenie
- Implementujte príklady z prednášky. Zamerajte sa na prekrytie, vyskúšajte použitie „protected“.
- Navrhnite a implementujte jednoduchú dedičnú hierarchiu geometrických objektov, ktoré budú mať spoločné metódy „Obsah“ a „Obvod“. Využite prekrytie a rozoberte správanie pri použití substitučného princípu.

### Kontrolné otázky
- Čo rozumieme paradoxom špecializácie a rozšírenia?
- Uveďte správne a nesprávne príklady vzťahu „generalizácia - špecializácia“.
- Čo rozumieme v dedičnosti zmenou správania?
- Čo rozumieme pretížením? Ide o rozšírenie alebo zmenu správania?
- Uveďte rôzne typy pretíženia.
- Čo rozumieme prekrytím? Ide o rozšírenie alebo zmenu správania?
- Aký princíp porušujeme, keď používame „protected“ a prečo?
- Aký problém prináša potreba zmeny správania v dedičnosti?
- Popíšte, ako sa prakticky prejavuje rôzna miera prístupu k položkám triedy.
- Ako sa použitie „protected“ prejaví vo vzťahu predka a potomka?

