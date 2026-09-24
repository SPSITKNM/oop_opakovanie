# Objektovo orientované programovanie — poznámky z hodín

Chronologický súhrn hodín OOP (2024/25 a 2025/26): teória (modularita, triedy, dedičnosť, polymorfizmus, správa pamäte) a k nej párové príklady v C++ a C#. Slúži ako príprava na komisionálnu skúšku.


# Modularita 2025/26

## Modul?

## KeyValue Class implementácia v C++

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

## Osnova hodiny
- Vývoj programovania
- Modularita
- Príklad

## Vývoj programovania

### Paradigmy programovania
- Ako a prečo sa jazyky vyvíjajú?
- V čom sa OOP líši od predchádzajúcich paradigiem?
- Aspekty kvality softvéru.

### Veľké projekty
- Programovanie veľkých projektov je kvalitatívne odlišné od vytvárania malých programov.
- Dôvodom na úvahy o princípoch programovania bola a je rastúca komplexnosť počítačových programov.

### Paradigmy
- Imperatívne programovanie (popisujeme **AKO** sa rieši)
- Deklaratívne programovanie (popisujeme **ČO** sa rieši)
- Funkcionálne programovanie
- Logické programovanie
- Modulárne programovanie
- Objektovo orientované programovanie

## Imperatívne programovanie
- Procedurálne programovanie
- Postupnosť krokov, ktorými meníme stav premenných programu.
- Štruktúrované programovanie
- Sekvencie, iterácie, vetvenia, skoky, abstrakcie.
- Tak, ako to dnes poznáme z bežne používaných jazykov.

## Procedurálne programovanie
- Podskupina imperatívneho programovania: program je **sada funkcií (procedúr)**, ktoré sa volajú v určitom poradí.
- Myslíme v štýle: **„Čo mám urobiť a v akom poradí?“**
- **Dáta a funkcie sú oddelené.**
  - Dáta drží `struct`, ktorý nevie s nimi nič robiť.
  - Funkcie dáta nevlastnia, dostanú ich cez parametre.
  - Výsledok je návratová hodnota alebo zmena odovzdaných dát cez referenciu.
- `main` je „riaditeľ“: vytvorí dáta a postupne volá funkcie.

### Príklad v C++

```cpp
#include <iostream>
#include <string>
#include <vector>
using namespace std;

// dáta – držiak bez správania
struct Student {
    string meno;
    vector<int> znamky;
};

// funkcia dáta len číta a vráti výsledok
double priemer(const Student& s) {
    if (s.znamky.empty()) return 0;
    double sucet = 0;
    for (int z : s.znamky) sucet += z;
    return sucet / s.znamky.size();
}

// funkcia dáta mení, nič nevracia
void pridajZnamku(Student& s, int znamka) {
    s.znamky.push_back(znamka);
}

// funkcia len vypisuje
void vypis(const Student& s) {
    cout << s.meno << ": " << priemer(s) << endl;
}

int main() {
    Student jan{"Ján", {}};

    pridajZnamku(jan, 1);
    pridajZnamku(jan, 2);
    pridajZnamku(jan, 1);

    vypis(jan);
}
```

### Ako sa dáta predávajú

| Spôsob | Zápis | Význam |
|---|---|---|
| Hodnotou | `void f(Student s)` | funkcia dostane **kópiu**, originál sa nezmení |
| Referenciou | `void f(Student& s)` | funkcia pracuje s **originálom** a môže ho zmeniť |
| Const referenciou | `void f(const Student& s)` | funkcia **vidí originál**, ale nesmie ho meniť (bez kopírovania) |

- Výsledok jednej funkcie môže ísť ako vstup do ďalšej: `vypisHodnotenie(priemer(jan));`

### Ako sa na to pozerať pri návrhu
- Rozdelíme problém na kroky: načítaj dáta → spracuj dáta → vypíš výsledok.
- Každá funkcia robí **jednu vec**, `main` ich zloží do celku.
- Vhodné pre menšie programy, skripty a jednoduché nástroje (typicky C, Pascal).

### Slabé miesto procedurálneho prístupu
- Dáta sú voľne prístupné odkiaľkoľvek, nikto nekontroluje ich platnosť:

```cpp
jan.znamky.push_back(999);   // neplatná známka, prekladač nenamieta
```

- Čím väčší projekt (pozri *Veľké projekty*), tým ťažšie je sledovať, ktorá funkcia mení ktoré dáta.
- Presne toto rieši objektovo orientovaný prístup: dáta a funkcie, ktoré s nimi smú pracovať, patria do jednej triedy a dáta sa dajú skryť (`private`).
- Metódy triedy sú stále len funkcie, ktoré majú prístup k dátam „svojho“ objektu.

### Procedurálne vs. objektovo v diagrame
![Procedurálne vs. objektové — struct a funkcie vs. trieda](https://cdn.jsdelivr.net/gh/SPSITKNM/oop_opakovanie@main/assets/proc-vs-oop.svg)
- Vľavo: `struct Student` drží len dáta a funkcie stoja mimo neho (pozri príklad vyššie).
- Vpravo: tie isté dáta a funkcie v jednej triede, dáta sú `private`, funkcie sa stali metódami.
- Tento prechod rozoberá kapitola Enkapsulácia nižšie.

## Modulárne programovanie
- Návrh zhora-nadol.
- Rozdelenie programu na nezávislé, zameniteľné moduly, ktoré zabezpečujú čiastkovú funkcionalitu.
- Modul obsahuje všetko potrebné na zabezpečenie funkcionality (dáta a algoritmy).

## Objektovo orientované programovanie

### Faktory kvality softvéru
- Vnútorné a vonkajšie faktory.
- Vnútorné sú skryté používateľovi. (AKO)
- Vonkajšie popisujú správanie navonok. (ČO)
- Musíme vedieť merať kvalitu.

### Vonkajšie faktory
- Správnosť
- Robustnosť
- Rýchlosť, rozšíriteľnosť, použiteľnosť, kompatibilita, ...

### Kľúčové faktory

**Robustnosť?**
- Náklady na robustnosť môžu byť vyššie než náklady vynaložené na správnosť.
- Robustnosť nie je cieľom predmetu OOP, preto ju nebudeme vyžadovať...
- ... a budeme teda vždy predpokladať správne vstupy.

## Ďalšie faktory

## Modularita

### Modul
- Metóda konštrukcie softvéru je modulárna, ak je založená na dekompozícii, ktorá pomáha návrhárom decentralizovať architektúru a tvoriť softvérové systémy zložené z autonómnych prvkov, modulov, prepojených do jednoduchých a zrozumiteľných štruktúr.

### Modularita programu
- Pochopiteľnosť
- Samostatnosť
- Kombinovateľnosť
- Zapúzdrenie
- Explicitné rozhranie
- Syntaktická podpora

### Pochopiteľnosť
- Modul by mal vykonávať jednu jasne definovanú a pochopiteľnú úlohu, prípadne niekoľko málo jasne definovaných úloh.

### Samostatnosť
- Každý modul musí byť relatívne samostatný a mal by mať čo možno najmenší počet väzieb na ostatné moduly.
- Nebolo by vhodné, aby boli všetky moduly programu navzájom prepojené a na sebe závislé.
- Moduly by sme tak nemohli individuálne otestovať, pochopiť ani preniesť do iného projektu.

### Kombinovateľnosť
- Moduly musia byť navzájom kombinovateľné. Musí byť možné modul vziať a použiť ho v inom kontexte alebo aj v inom projekte.

### Zapúzdrenie
- Moduly musia mať právo na isté súkromie: je prípustné a žiaduce, aby všetky informácie, ktoré nie sú potrebné pre klientov modulov, zostali skryté vnútri modulu.
- V praxi sa ukazuje, že väčšina funkcionality modulu je skrytá a len malá časť je viditeľná navonok.
- Skrytej časti hovoríme implementácia modulu a verejnej časti hovoríme rozhranie (interface) modulu.

### Explicitné rozhranie
- Z deklarácie modulu musí byť všeobecne zrejmé, aké predpoklady pre vykonávanie svojej úlohy potrebuje.

### Syntaktická podpora
- Moduly počítačového programu musia byť jasne vymedzené syntaktickými jednotkami programu.
- Zo zápisu programovacieho jazyka musí byť zrejmé, kde začína a kde končí zápis jedného modulu.
- Nie je napríklad možné, aby v kompaktnom programe patrili modulu len niektoré časti, zatiaľ čo iné časti modulu nepatrili.

## Päť kritérií a pravidiel modularity
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

## Kritériá
- dekomponovateľnosť, kombinovateľnosť, pochopiteľnosť
   
## Kritériá kontinuita, ochrana

## Pravidlá
- priame mapovanie, pár rozhraní, malé rozhrania
   
## Pravidlá
- explicitné rozhranie, skrytie informácií
  
## Príklad

## Trieda vs Objekt
- Trieda ako statický popis.
- Objekt ako runtime (behová) reprezentácia:
  - stav (dáta)
  - správanie (algoritmy)

## Terminológia
- Trieda
- Členská funkcia, metóda
- Členská položka, premenná
- Objekt, inštancia triedy, this (vykonávateľ metódy)
- Konštruktor, destruktor

## Deklarácia triedy


## KeyValue Class implementácia v C++

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

## Implementácia (definícia) triedy

## KeyValue Class implementácia v C++

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

## Použitie triedy 1

## Main Function príklad implementácia v C++

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

## Použitie triedy 2

## Main Function príklad s KeyValue Class implementácia v C++

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

## Použitie triedy 3

## Main Function s Nullptr implementácia v C++

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

## Implementácia v jazyku C#

```csharp
using System;

class KeyValue
{
    public int Key { get; private set; }
    public double Value { get; private set; }
    public KeyValue Next { get; private set; }

    public KeyValue(int key, double value)
    {
        this.Key = key;
        this.Value = value;
        this.Next = null;
    }

    public KeyValue CreateNext(int key, double value)
    {
        this.Next = new KeyValue(key, value);
        return this.Next;
    }

    public KeyValue GetNext()
    {
        return this.Next;
    }
}

class Program
{
    static void Main()
    {
        KeyValue kv1 = new KeyValue(1, 1.5);
        Console.WriteLine(kv1.CreateNext(2, 2.5).Key);

        KeyValue kv2 = kv1.GetNext();
        Console.WriteLine(kv2.GetNext());

        kv1 = null;
        kv2 = null;

        //Console.WriteLine(kv1.Key);
        //Console.WriteLine(kv2.Key);

        Console.ReadKey();
    }
}
```

## Konštruktor a destruktor
- Konštruktor inicializuje dáta objektu hodnotami parametrov v konštruktore (naplní pamäť dátami).
- Destruktor odstráni z pamäte dáta objektu (čistí pamäť).
- Destruktor nie je potrebný, ak sú dáta objektu statické.

## Úlohy na cvičenie
- Implementujte triedu `KeyValue` podľa prednášky a vytvorte zreťazenú lineárnu štruktúru mnohých (napr. tisícov) objektov a pracujte s ňou (vypíšte napr. všetky kľúče od prvého do posledného objektu).
- Vytvorte podobnú triedu ako `KeyValue`, ale s hodnotou aj kľúčom typu (triedy) `string` a s dvoma susediacimi (next) objektmi. Výsledkom bude tzv. strom.
- Implementujte štruktúru (rozhodovací strom) na identifikáciu zvierat alebo rastlín. Kľúčom uzla stromu je rozhodovacie kritérium, hodnotou uzla je názov zvieraťa alebo rastliny, resp. druhu a pod. Naplňte kľúč aspoň desiatimi objektmi a vypíšte celú štruktúru na obrazovku.

## Kontrolné otázky
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

# Enkapsulácia (zapuzdrenie) v C++ — prvý pilier OOP

## Osnova hodiny
- Čo je enkapsulácia a prečo ju potrebujeme.
- Triedny diagram (UML): ako ho čítať.
- Trieda a objekt (inštancia).
- Konštruktor.
- Gettery a settery.
- Modifikátory prístupu (`private`, `protected`, `public`).
- Kompletný príklad a najčastejšie chyby.

## Základná myšlienka
- **Enkapsulácia = dáta objektu schováme dovnútra a meniť ich smú len metódy, ktoré určíme my.**
- Analógia s bankomatom:
  - Do trezoru nemôžeš siahnuť (`private`).
  - Môžeš stlačiť tlačidlo „vybrať 50 €“ (`public`).
  - Bankomat sám skontroluje, či na to máš.
- Nadväzuje na kapitolu Modularita (kritérium *Zapúzdrenie*):
  - verejná časť = **rozhranie** (čo objekt vie),
  - skrytá časť = **implementácia** (ako to robí).
- V triede platí: `public` metódy sú rozhranie, `private` atribúty sú implementácia.

## Triedny diagram: ako ho čítať
- Každý krok kapitoly je aj nakreslený ako **UML triedny diagram**. Diagram ukazuje štruktúru triedy na jeden pohľad, ešte pred čítaním kódu.
- Trieda je obdĺžnik s tromi priehradkami: **názov**, **atribúty** (dáta), **metódy** (správanie).

![Ako čítať triedny diagram — priehradky a viditeľnosť](https://cdn.jsdelivr.net/gh/SPSITKNM/oop_opakovanie@main/assets/encap-01-notacia.svg)

| Značka | Viditeľnosť | C++ |
|---|---|---|
| `+` | verejný člen | `public` |
| `-` | súkromný člen | `private` |
| `#` | chránený člen | `protected` |

- Atribút sa píše `viditeľnosť názov: typ`, napr. `- zostatok: int`. V C++ je to `int zostatok;` v sekcii `private`. Typ je v diagrame **za** názvom, v kóde **pred** ním.
- Metóda sa píše `viditeľnosť názov(parametre): návratový typ`, napr. `+ vloz(suma: int): void`.
- Konštruktor nemá návratový typ: `+ Ucet(z: int)`.
- Objekt sa kreslí ako obdĺžnik s **podčiarknutým** názvom `a : Ucet` (meno objektu : trieda).
- Prerušovaná šípka s otvoreným hrotom v tejto kapitole znamená „inštancia triedy“ alebo „volá“.

## Krok 1: objekt bez ochrany
- Začneme triedou, v ktorej sú dáta `public`.
- `public` znamená, že k členu sa dá dostať odkiaľkoľvek.

```cpp
#include <iostream>
using namespace std;

class Ucet {
public:                 // public = prístupné odkiaľkoľvek
    int zostatok;       // atribút (dáta objektu)
};

int main() {
    Ucet a;                         // vytvoríme objekt (inštanciu) triedy Ucet
    a.zostatok = 100;               // nastavíme zostatok, funguje
    a.zostatok = -5000;             // funguje aj toto, nikto nekontroluje, či to dáva zmysel
    cout << a.zostatok << endl;     // -5000
}
```

![Trieda Ucet s public atribútom — bez ochrany](https://cdn.jsdelivr.net/gh/SPSITKNM/oop_opakovanie@main/assets/encap-02-bez-ochrany.svg)

- V diagrame je pri `zostatok` značka `+`, teda `public`: kto chce, ten ho zmení.
- Prekladač nenamieta, ale účet má záporný zostatok, ktorý nikto nechcel.
- Toto je presne slabé miesto procedurálneho štýlu (pozri sekciu Procedurálne programovanie): dáta sú voľne dostupné a nikto ich nestráži.

## Trieda a objekt: `Ucet a;`
- `Ucet` je **trieda** (predpis, „plán domu“).
- `a` je **objekt** (inštancia triedy, „postavený dom“).
- Slová *objekt* a *inštancia* znamenajú to isté.
- Je to rovnaké ako pri `int x;`: `int` je typ, `x` je konkrétna hodnota toho typu.

```cpp
Ucet a;                 // prvý objekt
Ucet b;                 // druhý objekt
a.zostatok = 100;
b.zostatok = 500;       // každý objekt má vlastnú kópiu dát
```


![Trieda Ucet a jej objekty a, b](https://cdn.jsdelivr.net/gh/SPSITKNM/oop_opakovanie@main/assets/encap-04-trieda-objekty.svg)

- Vľavo je **trieda** (predpis), vpravo **objekty** (inštancie). Názov objektu je podčiarknutý: `a : Ucet`.
- Z jednej triedy vznikne toľko objektov, koľko chceme, a každý má vlastné dáta.
- Takto zapísaný objekt je na **stacku** a zanikne na konci bloku `{ }`, v ktorom vznikol.

## Krok 2: zamkneme dáta (`private`)
- Zmeníme `public` na `private`.
- `private` = k členu sa dostane len kód **vnútri triedy** (jej vlastné metódy).

```cpp
class Ucet {
private:                // private = vidí len samotná trieda
    int zostatok;
};

int main() {
    Ucet a;
    // a.zostatok = 100;    // CHYBA PRI PREKLADE: 'zostatok' is a private member
}
```

- Chyba vznikne už **pri preklade**, program sa vôbec nespustí.
- Dáta sú v bezpečí, ale teraz s nimi nevieme vôbec pracovať. Potrebujeme bránu.

## Krok 3: brána — `public` metódy
- Metódy sú súčasťou triedy, preto smú siahnuť na `private` atribúty.
- Každá metóda môže skontrolovať, či zmena dáva zmysel.

```cpp
#include <iostream>
using namespace std;

class Ucet {
private:
    int zostatok;                   // dáta sú zamknuté

public:
    Ucet(int z) {                   // konštruktor: nastaví počiatočnú hodnotu
        zostatok = z;
    }

    void vloz(int suma) {           // brána na zmenu dát
        if (suma > 0) {             // pravidlo: vkladať sa dá len kladná suma
            zostatok = zostatok + suma;
        }
    }

    int getZostatok() {             // brána na čítanie dát
        return zostatok;
    }
};

int main() {
    Ucet a(100);                    // účet so zostatkom 100
    a.vloz(50);                     // zostatok = 150
    a.vloz(-999);                   // metóda to odmietne, zostatok ostane 150
    cout << a.getZostatok() << endl;    // 150
    // a.zostatok = -5000;          // CHYBA PRI PREKLADE, zostatok je private
}
```

![Enkapsulácia — zvonka len cez public metódy](https://cdn.jsdelivr.net/gh/SPSITKNM/oop_opakovanie@main/assets/encap-03-brana.svg)

- Diagram ukazuje tú istú triedu `Ucet`: `-` = zamknuté dáta, `+` = brána.
- Zelené šípky sú povolené volania z `main()`. Prerušovaná červená je pokus o priamy prístup, ktorý prekladač odmietne.
- K `zostatok` sa dostaneme **len cez metódy**.
- Pravidlá (`suma > 0`) sú na **jednom mieste**, nie rozhádzané po programe.

## Konštruktor

### Čo je konštruktor
- Konštruktor je **metóda, ktorá sa spustí sama pri vytvorení objektu** a nastaví mu počiatočný stav.
- Dve pravidlá:
  - názov je **rovnaký ako názov triedy**,
  - **nemá návratový typ** (ani `void`).

```cpp
class Ucet {
private:
    int zostatok;

public:
    Ucet(int z) {           // konštruktor: názov = názov triedy, bez návratového typu
        zostatok = z;       // nastavíme počiatočnú hodnotu
    }
};

Ucet a(100);                // tu sa konštruktor spustí, z = 100, zostatok = 100
```

### Konštruktor ako brána
- Atribút `zostatok` je `private`, zvonka ho nenastavíme.
- Konštruktor je **oficiálna brána**, cez ktorú objekt dostane počiatočné hodnoty.
- Metódy (`vloz`, `vyber`) sú brána na zmeny **neskôr**.

| Brána | Kedy sa používa |
|---|---|
| konštruktor | pri **vzniku** objektu, nastaví počiatočný stav |
| metódy (`vloz`, `vyber`) | **neskôr**, keď hodnoty meníme |

### Konštruktor objekt nevytvára, ale nastavuje
1. Pamäť pre objekt vyhradí C++ (na stacku alebo na heape).
2. Potom sa zavolá konštruktor, ktorý objektu nastaví začiatočný stav.

```cpp
Ucet a(100);
//    │
//    ├─ 1. C++ vyhradí miesto v pamäti pre objekt
//    └─ 2. konštruktor nastaví zostatok = 100
```

- Vďaka konštruktoru nezačne objekt život s náhodnými hodnotami z pamäte.
- Konštruktor môže nastaviť aj pevnú hodnotu, nielen parameter:

```cpp
Ucet() {
    zostatok = 0;           // každý nový účet začne s nulou
}
```

### Dva zápisy konštruktora
```cpp
// 1) základný zápis: priradenie v tele
Ucet(int z) {
    zostatok = z;
}

// 2) skrátený zápis: inicializačný zoznam
Ucet(int z) : zostatok(z) {}
```

- Oba robia to isté. Na začiatok používaj prvý, je základný a ľahšie sa číta.
- Inicializačný zoznam (`: zostatok(z)`) vytvorí člen rovno so správnou hodnotou. Je nutný až pri zložitejších členoch (`const` člen, referencia), preto sa v C++ často používa.

### Predvolený (default) konštruktor
- Predvolený konštruktor je konštruktor **bez parametrov**. Volá ho zápis `Ucet a;`.
- Ak v triede **nenapíšeš žiadny konštruktor**, C++ ho vytvorí samo.
- Vygenerovaný je **prázdny**, nič nenastaví, takže `zostatok` obsahuje náhodnú hodnotu z pamäte.

```cpp
class Ucet {
public:
    int zostatok;
};

Ucet a;                     // volá sa prázdny predvolený konštruktor
                            // a.zostatok obsahuje náhodné číslo z pamäte
```

### Pasca: vlastný konštruktor zruší predvolený
- Keď napíšeš **akýkoľvek vlastný konštruktor** (napr. s parametrom), C++ predvolený konštruktor už negeneruje.

```cpp
class Ucet {
private:
    int zostatok;

public:
    Ucet(int z) {
        zostatok = z;
    }
};

int main() {
    Ucet b(100);            // OK
    // Ucet a;              // CHYBA PRI PREKLADE: neexistuje konštruktor bez parametrov
}
```

- Riešenie: predvolený konštruktor dopíšeme sami.

### Viac konštruktorov v jednej triede
- Konštruktorov môže byť viac, musia sa líšiť počtom alebo typom parametrov.
- C++ vyberie ten, ktorý sedí na zápis pri vytváraní objektu.

```cpp
#include <iostream>
using namespace std;

class Ucet {
private:
    int zostatok;

public:
    Ucet() {                // predvolený konštruktor (bez parametrov)
        zostatok = 0;
    }

    Ucet(int z) {           // konštruktor s parametrom
        zostatok = z;
    }

    int getZostatok() {
        return zostatok;
    }
};

int main() {
    Ucet a;                 // volá Ucet()     -> zostatok = 0
    Ucet b(100);            // volá Ucet(int)  -> zostatok = 100
    cout << a.getZostatok() << endl;    // 0
    cout << b.getZostatok() << endl;    // 100
}
```

![Viac konštruktorov v triede Ucet](https://cdn.jsdelivr.net/gh/SPSITKNM/oop_opakovanie@main/assets/encap-05-konstruktory.svg)

- Zápis `Ucet a;` volá konštruktor bez parametrov, `Ucet b(100);` konštruktor s jedným `int`.
- V diagrame sú konštruktory obe `+ Ucet(...)` a nemajú návratový typ.

### Destruktor (stručne)
- Destruktor je opak konštruktora: zavolá sa **sám pri zániku objektu**.
- Zapisuje sa `~Ucet()`, bez parametrov a bez návratového typu.
- Potrebný je vtedy, keď objekt vlastní dynamickú pamäť (pozri `KeyValue` vyššie).

## Gettery a settery
- **Getter** = metóda, ktorá **vráti** hodnotu `private` atribútu (čítanie).
- **Setter** = metóda, ktorá **nastaví** hodnotu `private` atribútu (zápis).
- Sú to najjednoduchšie „brány“ pri enkapsulácii.

```cpp
#include <iostream>
using namespace std;

class Ucet {
private:
    int zostatok;

public:
    Ucet() {
        zostatok = 0;
    }

    int getZostatok() const {           // getter; const = metóda objekt nemení
        return zostatok;
    }

    void setZostatok(int z) {           // setter
        if (z >= 0) {                   // kontrola: záporný zostatok nepustíme
            zostatok = z;
        }
    }
};

int main() {
    Ucet a;
    a.setZostatok(100);                 // OK, zostatok = 100
    a.setZostatok(-5);                  // ignorované, zostatok ostane 100
    cout << a.getZostatok() << endl;    // 100
}
```

![Gettery a settery — triedy Ucet a Osoba](https://cdn.jsdelivr.net/gh/SPSITKNM/oop_opakovanie@main/assets/encap-06-getter-setter.svg)

- V diagrame je pri metódach popis `getter` / `setter` len ako pomôcka, v UML sa nepíše.
- Trieda `Osoba` nemá `setMeno`, preto je meno zvonka len na čítanie.

| Atribút | Getter | Setter |
|---|---|---|
| `zostatok` | `getZostatok()` | `setZostatok(int z)` |
| `meno` | `getMeno()` | `setMeno(string m)` |

- Názov sa skladá z `get` / `set` a názvu atribútu.
- **Bez settera je atribút zvonka len na čítanie.** Takto sa robia hodnoty, ktoré sa nemajú meniť (napr. číslo účtu, kód klienta).
- `const` za zátvorkou getteru sľubuje, že metóda objekt nemení.
- Setter má zmysel len vtedy, ak **kontroluje**. Setter bez kontroly je len `public` atribút v prestrojení.
- Lepší návrh ako `setZostatok` je metóda, ktorá vyjadruje, čo sa s účtom reálne robí:

```cpp
bool vyber(int suma) {
    if (suma > 0 && suma <= zostatok) {     // pravidlá výberu na jednom mieste
        zostatok = zostatok - suma;
        return true;                        // výber sa podaril
    }
    return false;                           // výber sa nepodaril
}
```

## Modifikátory prístupu

| Modifikátor | Trieda | Potomok | Zvonka |
|---|---|---|---|
| `private` | ✔ | ✘ | ✘ |
| `protected` | ✔ | ✔ | ✘ |
| `public` | ✔ | ✔ | ✔ |

- Pravidlo: **atribúty `private`, metódy `public`.**
- `protected` dáva zmysel až pri dedičnosti (pozri kapitolu *Dedičnosť v C++* hneď za touto kapitolou a príklad *C++ Account Class (Protected Balance)* nižšie v poznámkach).

### `class` vs. `struct`
- Jediný rozdiel v C++ je **predvolený prístup**, teda čo platí, keď nenapíšeš nič.

| Kľúčové slovo | Predvolený prístup |
|---|---|
| `class` | `private` |
| `struct` | `public` |

```cpp
class Ucet {
    int zostatok;           // private (predvolene)
};

struct Student {
    int vek;                // public (predvolene)
};

int main() {
    Ucet a;
    Student s;
    // a.zostatok = 100;    // CHYBA PRI PREKLADE, private
    s.vek = 20;             // OK, public
}
```

- Predvolený prístup platí pre **všetky členy**, aj pre metódy a konštruktory. Ak v `class` zabudneš `public:`, zvonka nič nezavoláš.
- `struct` = „holé dáta“ (procedurálny štýl, príklad so `Student`), `class` = objekt s ochranou.
- Aj keď je `private` v `class` predvolené, píšeme ho explicitne, aby bolo jasné, čo je čo.

## Kde je objekt v pamäti
- Enkapsulácia funguje rovnako, či je objekt na stacku, alebo na heape.
- Trieda sama nie je ani na stacku, ani na heape. Na stacku alebo heape je až **inštancia**, a miesto určuje spôsob vytvorenia.

```cpp
#include <iostream>
using namespace std;

class Ucet {
private:
    int zostatok;

public:
    Ucet(int z) {
        zostatok = z;
    }

    void vloz(int suma) {
        if (suma > 0) {
            zostatok = zostatok + suma;
        }
    }

    int getZostatok() {
        return zostatok;
    }
};

int main() {
    Ucet a(100);                // objekt na STACKU, zanikne na konci bloku
    a.vloz(50);                 // prístup cez bodku
    cout << a.getZostatok() << endl;        // 150

    Ucet* b = new Ucet(100);    // objekt na HEAPE, b je ukazovateľ (sám je na stacku)
    b->vloz(50);                // prístup cez šípku
    cout << b->getZostatok() << endl;       // 150
    delete b;                   // heap uvoľňujeme ručne
}
```

| | Stack | Heap |
|---|---|---|
| Vytvorenie | `Ucet a(100);` | `new Ucet(100)` |
| Prístup ku členom | `a.vloz(50)` | `b->vloz(50)` |
| Zánik | automaticky na konci bloku | ručne cez `delete` |

## Kompletný príklad: účet
- Spojíme všetko: `private` atribúty, konštruktory, gettery, metódy s kontrolou.

```cpp
#include <iostream>
#include <string>
using namespace std;

class Ucet {
private:                                // dáta sú skryté
    string majitel;
    int zostatok;

public:                                 // rozhranie triedy
    Ucet(string m) {                    // konštruktor s majiteľom, zostatok začína na 0
        majitel = m;
        zostatok = 0;
    }

    Ucet(string m, int z) {             // konštruktor s majiteľom aj zostatkom
        majitel = m;
        if (z >= 0) {                   // záporný počiatočný zostatok nepustíme
            zostatok = z;
        } else {
            zostatok = 0;
        }
    }

    string getMajitel() const {         // getter, majiteľ nemá setter (nemení sa)
        return majitel;
    }

    int getZostatok() const {           // getter
        return zostatok;
    }

    void vloz(int suma) {               // zmena stavu len povolenou operáciou
        if (suma > 0) {
            zostatok = zostatok + suma;
        }
    }

    bool vyber(int suma) {              // vráti true, ak sa výber podaril
        if (suma > 0 && suma <= zostatok) {
            zostatok = zostatok - suma;
            return true;
        }
        return false;
    }
};

int main() {
    Ucet jan("Jan", 100);               // volá konštruktor s dvoma parametrami
    Ucet eva("Eva");                    // volá konštruktor s jedným parametrom

    jan.vloz(50);                       // 150
    jan.vloz(-20);                      // odmietnuté, ostane 150
    bool ok = jan.vyber(500);           // false, na účte nie je dosť
    jan.vyber(30);                      // 120

    cout << jan.getMajitel() << ": " << jan.getZostatok() << endl;  // Jan: 120
    cout << eva.getMajitel() << ": " << eva.getZostatok() << endl;  // Eva: 0
    cout << (ok ? "vyber presiel" : "vyber zamietnuty") << endl;    // vyber zamietnuty

    // jan.zostatok = 1000000;          // CHYBA PRI PREKLADE, private
    // jan.majitel = "Peter";           // CHYBA PRI PREKLADE, private
}
```

![Kompletný príklad — trieda Ucet](https://cdn.jsdelivr.net/gh/SPSITKNM/oop_opakovanie@main/assets/encap-07-kompletny-ucet.svg)

- Diagram sa dá čítať ako zhrnutie kódu: všetko s `-` je skryté, všetko s `+` je rozhranie.
- Atribút `majitel` nemá setter, zostatok sa mení len cez `vloz` a `vyber`.

## Rozhranie a implementácia
- **Rozhranie** = `public` časť: čo objekt vie (`vloz`, `vyber`, `getZostatok`).
- **Implementácia** = `private` časť: ako to robí (v čom a ako ukladá dáta).
- Vďaka enkapsulácii môžeme vnútro zmeniť a kód, ktorý objekt používa, sa nezmení.

```cpp
#include <iostream>
using namespace std;

class Ucet {
private:
    long long centy;                    // vnútro sa zmenilo: zostatok ukladáme v centoch

public:
    Ucet(int z) {
        centy = z * 100LL;
    }

    void vloz(int suma) {
        if (suma > 0) {
            centy = centy + suma * 100LL;
        }
    }

    int getZostatok() const {
        return centy / 100;             // navonok stále eurá, rozhranie ostalo rovnaké
    }
};

int main() {
    Ucet a(100);                        // tento kód je rovnaký ako predtým
    a.vloz(50);
    cout << a.getZostatok() << endl;    // 150
}
```

![Rozhranie a implementácia — zmena vnútra bez zmeny okolia](https://cdn.jsdelivr.net/gh/SPSITKNM/oop_opakovanie@main/assets/encap-08-rozhranie-implementacia.svg)

- Zvýraznená časť (`+` metódy) je rozhranie, v oboch verziách rovnaké. Zmenil sa len `-` atribút.
- Keby bol `zostatok` `public`, každé miesto v programe, ktoré s ním pracuje, by sme museli prepísať.

## Najčastejšie chyby
- **Všetko `public`.** Trieda potom nechráni nič.
- **Setter bez kontroly.** Ochrana je len naoko.
- **Zabudnuté `public:` v `class`.** Zvonka sa nedá zavolať ani konštruktor.
- **Vlastný konštruktor s parametrom a `Ucet a;`.** Predvolený konštruktor už neexistuje.
- **Zápis `Ucet a();`.** Prekladač ho berie ako deklaráciu funkcie, nie ako vytvorenie objektu. Predvolený konštruktor voláme zápisom `Ucet a;`.
- **Zabudnuté `delete`** pri objekte vytvorenom cez `new`.

## Úlohy na cvičenie
- Prepíšte procedurálny príklad `Student` (`struct` + funkcie) na triedu so `private` atribútmi, konštruktorom, getterom mena a metódami `pridajZnamku` a `priemer`. Známka smie byť len 1 až 5.
- Vytvorte triedu `Osoba` s atribútmi `meno` a `vek`. Vek nastavte cez setter, ktorý povolí len hodnoty 0 až 150. Meno nech je len na čítanie.
- Nakreslite triedny diagram triedy `Osoba` (atribúty, konštruktor, gettery, setter) so správnou viditeľnosťou a potom ho implementujte v C++.
- Doplňte triedu `Ucet` o metódu `prevedNa(Ucet& cielovy, int suma)`, ktorá presunie peniaze na iný účet len ak je na zdrojovom dosť prostriedkov.

## Kontrolné otázky
- Vysvetlite princíp enkapsulácie. Uveďte príklad v C++.
- Nakreslite triedny diagram triedy `Ucet` a vysvetlite značky `+`, `-` a `#`.
- Aký je rozdiel medzi `private`, `protected` a `public`?
- Čo je konštruktor a aké pravidlá musí spĺňať jeho zápis?
- Kedy sa volá predvolený konštruktor a kedy ho C++ negeneruje?
- Čo je getter a čo je setter? Prečo nestačí mať atribút `public`?
- Aký je rozdiel medzi `class` a `struct` v C++?
- Čo je rozhranie a čo implementácia triedy?
- Prečo môžeme zmeniť vnútornú reprezentáciu dát bez zmeny kódu, ktorý triedu používa?

### Vzorová odpoveď: princíp enkapsulácie
> Dáta objektu sú skryté (`private`) a prístup k nim je len cez verejné metódy, ktoré strážia platnosť dát. Používateľ triedy pozná len rozhranie (verejné metódy), nie implementáciu (skryté atribúty). Vďaka tomu sa dá vnútro triedy meniť bez zásahu do kódu, ktorý ju používa.

---

# Dedičnosť v C++ — druhý pilier OOP

## Osnova hodiny
- Čo je dedičnosť a prečo ju potrebujeme (predok, potomok, vzťah „JE“).
- Zápis dedičnosti v C++ (`class B : public A`).
- Konštruktory a destruktory pri dedičnosti, poradie volania.
- Prístup k členom predka (`private` vs. `protected`).
- Redefinícia metódy v potomkovi.
- Štyri typy dedičnosti: single, multilevel, hierarchical, multiple.
- Dedičnosť vs. skladanie (JE vs. MÁ), najčastejšie chyby.

## Základná myšlienka
- **Dedičnosť = nová trieda (potomok) prevezme atribúty a metódy existujúcej triedy (predka) a môže pridať vlastné.**
- Trieda, od ktorej dedíme, sa volá **predok** (base class, parent, superclass).
- Trieda, ktorá dedí, sa volá **potomok** (derived class, child, subclass).
- Vzťah medzi nimi je **JE** (IS-A): `SporiaciUcet` **je** `Ucet`, `Manazer` **je** `Zamestnanec`.
- Prínos: **opätovné použitie kódu**. Spoločné veci napíšeme raz v predkovi, potomok ich dostane zadarmo.
- Nadväzuje na enkapsuláciu: predok si stráži svoje `private` dáta, potomok s nimi pracuje cez to, čo predok dovolí.

## Krok 1: problém bez dedičnosti
- Máme účet. Teraz chceme aj sporiaci účet, ktorý navyše pripisuje úrok.
- Bez dedičnosti by sme skopírovali celú triedu `Ucet` a pridali úrok.

```cpp
#include <iostream>
using namespace std;

class Ucet {
private:
    int zostatok;

public:
    Ucet(int z) {
        zostatok = z;
    }

    void vloz(int suma) {                   // toto je v OBOCH triedach rovnaké
        if (suma > 0) {
            zostatok = zostatok + suma;
        }
    }

    int getZostatok() const {               // aj toto
        return zostatok;
    }
};

class SporiaciUcet {                        // kópia Ucet + úrok
private:
    int zostatok;                           // OPAKUJE SA
    double urok;

public:
    SporiaciUcet(int z, double u) {
        zostatok = z;                       // OPAKUJE SA
        urok = u;
    }

    void vloz(int suma) {                   // OPAKUJE SA
        if (suma > 0) {
            zostatok = zostatok + suma;
        }
    }

    int getZostatok() const {               // OPAKUJE SA
        return zostatok;
    }

    void pripisUrok() {                     // jediná nová vec
        int u = zostatok * urok;
        zostatok = zostatok + u;
    }
};

int main() {
    Ucet a(100);
    SporiaciUcet s(1000, 0.05);
    a.vloz(50);
    s.vloz(100);
    s.pripisUrok();
    cout << a.getZostatok() << endl;        // 150
    cout << s.getZostatok() << endl;        // 1155
}
```

![Dve podobné triedy bez dedičnosti — opakujúci sa kód](https://cdn.jsdelivr.net/gh/SPSITKNM/oop_opakovanie@main/assets/dedicnost-01-bez-dedicnosti.svg)

- Zvýraznené riadky v diagrame sú v oboch triedach rovnaké.
- Ak nájdeme chybu vo `vloz`, musíme ju opraviť na dvoch miestach. Pri desiatich podobných triedach na desiatich.
- Toto rieši dedičnosť.

## Krok 2: dedičnosť v C++
- Zápis: `class Potomok : public Predok`.
- Dvojbodka za názvom potomka znamená „dedí od“.
- Kľúčové slovo `public` pred predkom zachová prístup: `public` členy predka ostanú `public` aj v potomkovi. Zatiaľ píšeme **vždy `public`**.

```cpp
#include <iostream>
using namespace std;

class Ucet {                                // PREDOK
private:
    int zostatok;

public:
    Ucet(int z) {
        zostatok = z;
        cout << "Ucet(" << z << ")" << endl;
    }

    ~Ucet() {
        cout << "~Ucet()" << endl;
    }

    void vloz(int suma) {
        if (suma > 0) {
            zostatok = zostatok + suma;
        }
    }

    int getZostatok() const {
        return zostatok;
    }
};

class SporiaciUcet : public Ucet {          // POTOMOK: SporiaciUcet dedí od Ucet
private:
    double urok;                            // len nové veci, zvyšok už máme

public:
    SporiaciUcet(int z, double u) : Ucet(z) {   // najprv sa zavolá konštruktor predka
        urok = u;
        cout << "SporiaciUcet(" << z << ", " << u << ")" << endl;
    }

    ~SporiaciUcet() {
        cout << "~SporiaciUcet()" << endl;
    }

    void pripisUrok() {
        int u = getZostatok() * urok;       // zostatok je private v Ucet, pýtame sa cez getter
        vloz(u);                            // meníme cez metódu predka
    }
};

int main() {
    SporiaciUcet s(1000, 0.05);
    s.vloz(100);                            // zdedená metóda z Ucet
    s.pripisUrok();                         // vlastná metóda potomka
    cout << s.getZostatok() << endl;        // 1155
}
```

Výstup programu:

```
Ucet(1000)
SporiaciUcet(1000, 0.05)
1155
~SporiaciUcet()
~Ucet()
```

![Dedičnosť — SporiaciUcet dedí od Ucet](https://cdn.jsdelivr.net/gh/SPSITKNM/oop_opakovanie@main/assets/dedicnost-02-single-zaklad.svg)

- **Šípka s prázdnym trojuholníkom** vždy smeruje od **potomka k predkovi**.
- V diagrame má potomok len **nové** členy. Zdedené (`zostatok`, `vloz`, `getZostatok`) sa nekreslia znova, dostane ich cez šípku.
- Objekt `s` vie volať `vloz()` a `getZostatok()`, hoci ich `SporiaciUcet` nikde nenapísal.
- Zdedené sú všetky členy predka, okrem konštruktorov a destruktorov. Tie si každá trieda píše sama.

## Konštruktory a destruktory pri dedičnosti

### Poradie volania
- Objekt potomka **obsahuje** objekt predka. Najprv sa preto musí vytvoriť predok.
- **Konštruktory** sa volajú od predka k potomkovi.
- **Destruktory** sa volajú opačne: od potomka k predkovi.

![Poradie volania konštruktorov a destruktorov pri dedičnosti](https://cdn.jsdelivr.net/gh/SPSITKNM/oop_opakovanie@main/assets/dedicnost-03-poradie-konstruktorov.svg)

- Presne to vidno vo výstupe vyššie: `Ucet(1000)` → `SporiaciUcet(...)` a na konci `~SporiaciUcet()` → `~Ucet()`.

### Ako potomok povie predkovi, s čím má vzniknúť
- Predok `Ucet` má konštruktor `Ucet(int z)`, teda potrebuje parameter.
- Potomok ho musí odovzdať v zápise za dvojbodkou:

```cpp
SporiaciUcet(int z, double u) : Ucet(z) {   // za dvojbodkou voláme konštruktor predka
    urok = u;                               // v tele nastavíme vlastné atribúty
}
```

- Za dvojbodkou sa zavolá konštruktor predka s hodnotou `z`. Až potom sa vykoná telo.
- Ak predok **má konštruktor bez parametrov**, nemusíme ho volať, C++ ho zavolá samo.
- Ak predok **nemá konštruktor bez parametrov** a potomok ho nezavolá vôbec, prekladač skončí chybou:

```cpp
SporiaciUcet(int z, double u) {             // CHYBA PRI PREKLADE: chýba : Ucet(z)
    urok = u;
}
```

## Prístup k členom predka: `private` vs. `protected`
- Potomok **nemá** prístup k `private` členom predka, hoci ich objekt fyzicky obsahuje.
- Je to enkapsulácia: predok si svoje dáta stráži aj pred vlastnými potomkami.

```cpp
void pripisUrok() {
    // zostatok = zostatok + zostatok * urok;   // CHYBA PRI PREKLADE: zostatok je private v Ucet
    int u = getZostatok() * urok;               // OK: cez getter
    vloz(u);                                    // OK: cez metódu predka
}
```

- **Riešenie A (preferované):** potomok pracuje cez `public` metódy predka, ako v príklade vyššie.
- **Riešenie B:** predok označí atribút `protected`. Vidí ho predok aj potomkovia, zvonka je stále zamknutý.

```cpp
#include <iostream>
using namespace std;

class Ucet {
protected:                                  // vidí predok a potomkovia, zvonka nie
    int zostatok;

public:
    Ucet(int z) {
        zostatok = z;
    }

    int getZostatok() const {
        return zostatok;
    }
};

class SporiaciUcet : public Ucet {
private:
    double urok;

public:
    SporiaciUcet(int z, double u) : Ucet(z) {
        urok = u;
    }

    void pripisUrok() {
        zostatok = zostatok + zostatok * urok;  // OK: zostatok je protected, potomok ho vidí
    }
};

int main() {
    SporiaciUcet s(1000, 0.05);
    s.pripisUrok();
    cout << s.getZostatok() << endl;            // 1050
    // s.zostatok = 5;                          // CHYBA PRI PREKLADE: zvonka je protected zamknuté
}
```

![private vs. protected pri dedičnosti](https://cdn.jsdelivr.net/gh/SPSITKNM/oop_opakovanie@main/assets/dedicnost-04-protected.svg)

| Modifikátor v predkovi | Trieda samotná | Potomok | Zvonka |
|---|---|---|---|
| `private` | ✔ | ✘ | ✘ |
| `protected` | ✔ | ✔ | ✘ |
| `public` | ✔ | ✔ | ✔ |

- Pozor: `protected` **poruší časť enkapsulácie**, lebo potomok siaha na dáta predka priamo. Ak predok zmení vnútro, môže rozbiť aj potomkov. Preto sa pri `protected` treba pýtať, či nestačí getter.
- V diagrame sa `protected` značí `#`.

## Redefinícia metódy
- Potomok môže napísať metódu s **rovnakým názvom aj parametrami** ako predok. Tým ju **redefinuje**: pre objekt potomka platí jeho verzia.
- Verziu predka stále vieme zavolať zápisom `Predok::metoda()`.

```cpp
#include <iostream>
using namespace std;

class Ucet {
protected:
    int zostatok;

public:
    Ucet(int z) {
        zostatok = z;
    }

    bool vyber(int suma) {                      // verzia predka
        if (suma > 0 && suma <= zostatok) {
            zostatok = zostatok - suma;
            return true;
        }
        return false;
    }

    int getZostatok() const {
        return zostatok;
    }
};

class StandartnyUcet : public Ucet {
private:
    int poplatok;

public:
    StandartnyUcet(int z, int p) : Ucet(z) {
        poplatok = p;
    }

    bool vyber(int suma) {                      // REDEFINÍCIA: rovnaká hlavička ako v Ucet
        cout << "Standartny vyber s poplatkom " << poplatok << endl;
        return Ucet::vyber(suma + poplatok);    // zavoláme verziu predka
    }
};

int main() {
    StandartnyUcet s(100, 2);
    bool ok = s.vyber(50);                      // vyberie 50 + poplatok 2
    cout << ok << " " << s.getZostatok() << endl;   // 1 48
}
```

- `Ucet::vyber(...)` je zápis s **názvom triedy a dvoma dvojbodkami**: „zavolaj verziu z Ucet“.
- Redefinícia (bez `virtual`) sa rozhoduje podľa **typu premennej**. Ako sa správa objekt, keď na neho ukazuje ukazovateľ na predka, rieši až **polymorfizmus** (`virtual`, `override`).

## Štyri typy dedičnosti

![Štyri typy dedičnosti — prehľad](https://cdn.jsdelivr.net/gh/SPSITKNM/oop_opakovanie@main/assets/dedicnost-05-prehlad-typov.svg)

| Typ | Anglicky | Predkov | Potomkov | Príklad |
|---|---|---|---|---|
| Jednoduchá | Single | 1 | 1 | `Ucet` ← `SporiaciUcet` |
| Viacúrovňová | Multilevel | reťaz | reťaz | `Osoba` ← `Zamestnanec` ← `Manazer` |
| Hierarchická | Hierarchical | 1 | viac | `Ucet` ← `StandartnyUcet`, `UverUcet` |
| Viacnásobná | Multiple | viac | 1 | `Auto`, `Lod` ← `Amfibia` |

### 1. Single (jednoduchá)
- **Jeden predok, jeden potomok.**
- Je to náš príklad `Ucet` ← `SporiaciUcet` z kroku 2 (pozri diagram vyššie).

```cpp
class SporiaciUcet : public Ucet { /* ... */ };     // jeden predok
```

### 2. Multilevel (viacúrovňová)
- **Reťaz dedičnosti:** potomok sa sám stane predkom ďalšej triedy.
- Trieda na spodku má všetko zo všetkých úrovní nad sebou.
- Každý konštruktor volá len konštruktor svojho **priameho** predka.

```cpp
#include <iostream>
#include <string>
using namespace std;

class Osoba {                                   // úroveň 1
protected:
    string meno;

public:
    Osoba(string m) {
        meno = m;
    }

    void predstavSa() {
        cout << "Som " << meno << endl;
    }
};

class Zamestnanec : public Osoba {              // úroveň 2: dedí od Osoba
protected:
    int plat;

public:
    Zamestnanec(string m, int p) : Osoba(m) {   // odovzdá meno predkovi
        plat = p;
    }

    void vypisPlat() {
        cout << meno << " zarobi " << plat << " eur" << endl;
    }
};

class Manazer : public Zamestnanec {            // úroveň 3: dedí od Zamestnanec
private:
    int pocetPodriadenych;

public:
    Manazer(string m, int p, int n) : Zamestnanec(m, p) {   // Osoba sa nevolá priamo
        pocetPodriadenych = n;
    }

    void vypisTim() {
        cout << meno << " vedie " << pocetPodriadenych << " ludi" << endl;
    }
};

int main() {
    Manazer m("Eva", 3000, 5);
    m.predstavSa();                             // z Osoba (o dve úrovne vyššie)
    m.vypisPlat();                              // zo Zamestnanec
    m.vypisTim();                               // vlastná metóda
}
```

Výstup programu:

```
Som Eva
Eva zarobi 3000 eur
Eva vedie 5 ludi
```

![Viacúrovňová dedičnosť — Osoba, Zamestnanec, Manazer](https://cdn.jsdelivr.net/gh/SPSITKNM/oop_opakovanie@main/assets/dedicnost-06-multilevel.svg)

- `Manazer` je `Zamestnanec`, `Zamestnanec` je `Osoba`, teda `Manazer` je aj `Osoba`.
- Konštruktory sa volajú v poradí `Osoba` → `Zamestnanec` → `Manazer`, destruktory opačne.

### 3. Hierarchical (hierarchická)
- **Jeden predok, viac potomkov.** Každý potomok pridáva vlastné správanie.
- Spoločné veci sú len v predkovi, potomkovia sú od seba nezávislí.
- Presne takto vyzerá bankový systém z komisionálnej skúšky (`Ucet`, `StandartnyUcet`, `UverUcet`).

```cpp
#include <iostream>
using namespace std;

class Ucet {                                    // spoločný predok
protected:
    int zostatok;

public:
    Ucet(int z) {
        zostatok = z;
    }

    void vloz(int suma) {
        if (suma > 0) {
            zostatok = zostatok + suma;
        }
    }

    bool vyber(int suma) {                      // základné pravidlo: nesmie ísť do mínusu
        if (suma > 0 && suma <= zostatok) {
            zostatok = zostatok - suma;
            return true;
        }
        return false;
    }

    int getZostatok() const {
        return zostatok;
    }
};

class StandartnyUcet : public Ucet {            // potomok 1: každý výber stojí poplatok
private:
    int poplatok;

public:
    StandartnyUcet(int z, int p) : Ucet(z) {
        poplatok = p;
    }

    bool vyber(int suma) {                      // redefinícia
        return Ucet::vyber(suma + poplatok);    // pravidlo predka, ale s poplatkom
    }
};

class UverUcet : public Ucet {                  // potomok 2: povolený mínus do limitu
private:
    int limit;

public:
    UverUcet(int z, int l) : Ucet(z) {
        limit = l;
    }

    bool vyber(int suma) {                      // redefinícia s iným pravidlom
        if (suma > 0 && suma <= zostatok + limit) {
            zostatok = zostatok - suma;
            return true;
        }
        return false;
    }
};

int main() {
    StandartnyUcet s(100, 2);
    UverUcet u(100, 200);

    cout << s.vyber(50) << " " << s.getZostatok() << endl;      // 1 48   (50 + poplatok 2)
    cout << s.vyber(50) << " " << s.getZostatok() << endl;      // 0 48   (52 > 48)

    cout << u.vyber(250) << " " << u.getZostatok() << endl;     // 1 -150 (do limitu 200)
    cout << u.vyber(100) << " " << u.getZostatok() << endl;     // 0 -150 (presiahlo by limit)

    s.vloz(10);                                 // vloz() sme nepísali, zdedili sme ho
    u.vloz(10);
}
```

![Hierarchická dedičnosť — Ucet, StandartnyUcet, UverUcet](https://cdn.jsdelivr.net/gh/SPSITKNM/oop_opakovanie@main/assets/dedicnost-07-hierarchical.svg)

- Obaja potomkovia dostali `vloz`, `vyber` aj `getZostatok` od predka.
- Každý si **redefinoval** `vyber` po svojom. V diagrame je to označené tagom `redefinícia`.
- Zmena vo `vloz` v triede `Ucet` sa prejaví v oboch potomkoch naraz.

### 4. Multiple (viacnásobná)
- **Jeden potomok, viac predkov.** Zápis: predkovia oddelení čiarkou.
- Potomok dostane členy **od všetkých** predkov.
- C++ dedenie od viacerých tried podporuje (napr. Java a C# nie, tam sa to rieši rozhraniami).

```cpp
#include <iostream>
using namespace std;

class Auto {
public:
    Auto() {
        cout << "Auto()" << endl;
    }

    void jazdi() {
        cout << "Jazdim po ceste" << endl;
    }

    void zapniMotor() {
        cout << "Motor auta" << endl;
    }
};

class Lod {
public:
    Lod() {
        cout << "Lod()" << endl;
    }

    void pluje() {
        cout << "Plavim po vode" << endl;
    }

    void zapniMotor() {                         // rovnaký názov ako v Auto
        cout << "Motor lode" << endl;
    }
};

class Amfibia : public Auto, public Lod {       // dedí od OBOCH, oddelené čiarkou
public:
    Amfibia() {
        cout << "Amfibia()" << endl;
    }
};

int main() {
    Amfibia a;                                  // Auto(), Lod(), Amfibia() v poradí zápisu
    a.jazdi();                                  // z Auto
    a.pluje();                                  // z Lod
    // a.zapniMotor();                          // CHYBA PRI PREKLADE: nejednoznačné, Auto aj Lod ho majú
    a.Auto::zapniMotor();                       // riešenie: povieme, ktorú verziu chceme
    a.Lod::zapniMotor();
}
```

Výstup programu:

```
Auto()
Lod()
Amfibia()
Jazdim po ceste
Plavim po vode
Motor auta
Motor lode
```

![Viacnásobná dedičnosť — Amfibia dedí od Auto a Lod](https://cdn.jsdelivr.net/gh/SPSITKNM/oop_opakovanie@main/assets/dedicnost-08-multiple.svg)

- Konštruktory predkov sa volajú v **poradí, v akom sú zapísaní** (`Auto`, potom `Lod`), až potom konštruktor potomka.
- Ak majú dvaja predkovia metódu s rovnakým názvom, volanie je **nejednoznačné** a prekladač ho odmietne. Vyriešime to zápisom `objekt.Predok::metoda()`.
- Viacnásobná dedičnosť je silná, ale zložitá. Používa sa opatrne.

#### Diamantový problém (dobré vedieť)
- Ak majú dvaja predkovia **spoločného predka**, vznikne diamant.
- `Brigadnik` dedí od `Student` aj `Zamestnanec`, ktorí obaja dedia od `Osoba`. Bez opatrenia by `Brigadnik` obsahoval **dve kópie** `Osoba`.
- Riešenie: **virtuálna dedičnosť** (`virtual public`). Spoločný predok potom existuje len raz.

```cpp
#include <iostream>
#include <string>
using namespace std;

class Osoba {
private:
    string meno;

public:
    void setMeno(string m) {
        meno = m;
    }

    string getMeno() const {
        return meno;
    }
};

class Student : virtual public Osoba {          // virtual: spoločný predok bude len jeden
};

class Zamestnanec : virtual public Osoba {
};

class Brigadnik : public Student, public Zamestnanec {
};

int main() {
    Brigadnik b;
    b.setMeno("Jan");                           // bez virtual: CHYBA PRI PREKLADE (nejednoznačné)
    cout << b.getMeno() << endl;                // Jan
}
```

![Diamantový problém a virtuálna dedičnosť](https://cdn.jsdelivr.net/gh/SPSITKNM/oop_opakovanie@main/assets/dedicnost-09-diamant.svg)

- Kombinácia viacerých typov (napr. hierarchická + multiple) sa volá **hybridná dedičnosť**. Diamant je jej typický príklad.

## Dedičnosť vs. skladanie (JE vs. MÁ)
- Dedičnosť použijeme len keď platí vzťah **JE** (potomok je špeciálny prípad predka).
- Ak platí vzťah **MÁ**, použijeme **skladanie** (objekt drží iný objekt ako atribút).

| Veta | Vzťah | Riešenie |
|---|---|---|
| `SporiaciUcet` **je** `Ucet` | JE | dedičnosť |
| `Manazer` **je** `Zamestnanec` | JE | dedičnosť |
| `Ucet` **má** majiteľa (`Klient`) | MÁ | atribút `Klient majitel;` |
| `Banka` **má** účty | MÁ | atribút s účtami |

```cpp
#include <iostream>
#include <string>
using namespace std;

class Klient {
private:
    string meno;

public:
    Klient(string m) {
        meno = m;
    }

    string getMeno() const {
        return meno;
    }
};

class Ucet {                                    // Ucet NIE JE Klient, Ucet MÁ Klienta
private:
    Klient majitel;                             // skladanie: atribút typu Klient
    int zostatok;

public:
    Ucet(string m, int z) : majitel(m) {        // Klient nemá prázdny konštruktor, inicializujeme ho takto
        zostatok = z;
    }

    string getMajitel() const {
        return majitel.getMeno();
    }
};

int main() {
    Ucet u("Jan", 100);
    cout << u.getMajitel() << endl;             // Jan
}
```

- Chyba začiatočníkov: dediť len preto, že chceme prevziať nejaký kód. Ak veta „X je Y“ nedáva zmysel, nededíme.
- Skladanie, agregácia a kompozícia sú rozobrané v kapitole *Vzťahy medzi objektmi*.

## Najčastejšie chyby
- **Zabudnuté `public` pri dedení.** V `class` je predvolené dedenie `private`, takže verejné metódy predka zvonka nefungujú.

```cpp
class SporiaciUcet : Ucet { /* ... */ };            // dedenie je private (predvolene v class)
class SporiaciUcet : public Ucet { /* ... */ };     // správne
```

- **Chýbajúce `: Predok(...)`**, keď predok nemá konštruktor bez parametrov.
- **Prístup k `private` členu predka** z potomka. Použi getter alebo `protected`.
- **Nejednoznačné volanie** pri viacnásobnej dedičnosti (rovnaký názov metódy u dvoch predkov).
- **Dedičnosť namiesto skladania:** `Ucet` nededí od `Klient`, pretože `Ucet` nie je klient.
- **Redefinícia bez `virtual` nie je polymorfizmus.** K tomu sa dostaneme pri štvrtom pilieri (abstraktné triedy a `virtual` pozri kapitolu *Abstrakcia v C++* hneď nižšie).

## Úlohy na cvičenie
- Vytvorte triedu `Zviera` (atribút `meno`, metóda `predstavSa()`) a potomkov `Pes` a `Macka`, každý s vlastnou metódou (`stekaj()`, `pradie()`). Nakreslite triedny diagram.
- Vytvorte reťaz `Vozidlo` ← `Auto` ← `SportoveAuto` (viacúrovňová dedičnosť). Každá úroveň pridá aspoň jeden atribút a metódu.
- Doplňte hierarchiu účtov o tretieho potomka `SporiaciUcet`, ktorý nepovolí výber viac ako 500 eur naraz.
- Vytvorte triedy `Lietadlo` a `Lod` a potomka `Hydroplan`. Vyriešte nejednoznačnú metódu `zapniMotor()`.
- Rozhodnite, kde platí JE a kde MÁ: `Kruh` – `Tvar`, `Auto` – `Motor`, `Student` – `Osoba`, `Trieda` – `Student`.

## Kontrolné otázky
- Vysvetlite princíp dedičnosti. Uveďte príklad v C++.
- Čo je predok a čo potomok? Ktorý smer má šípka v triednom diagrame?
- Aký je rozdiel medzi vzťahom JE a MÁ? Kedy použijeme dedičnosť?
- V akom poradí sa volajú konštruktory a destruktory pri dedičnosti?
- Ako odovzdá potomok parametre konštruktoru predka?
- Aký je rozdiel medzi `private` a `protected` z pohľadu potomka?
- Čo je redefinícia metódy a ako zavoláme verziu predka?
- Vymenujte a nakreslite štyri typy dedičnosti (single, multilevel, hierarchical, multiple).
- Čo je diamantový problém a ako sa rieši?

### Vzorová odpoveď: princíp dedičnosti
> Dedičnosť umožňuje vytvoriť novú triedu (potomka) z existujúcej triedy (predka). Potomok automaticky získa atribúty a metódy predka a môže pridať vlastné alebo redefinovať zdedené. Vzťah medzi nimi je „JE“ (`SporiaciUcet` je `Ucet`). Dedičnosť podporuje opätovné použitie kódu: spoločné veci píšeme raz v predkovi. V C++ ju zapisujeme `class Potomok : public Predok`.

---

# Abstrakcia v C++ — tretí pilier OOP

## Osnova hodiny
- Čo je abstrakcia: ukázať **čo**, schovať **ako**.
- Abstrakcia ako výber podstatných vlastností (model).
- Abstraktná trieda a čistá virtuálna metóda (`= 0`).
- Virtuálna vs. čistá virtuálna metóda.
- Abstraktná trieda so spoločným kódom (`Ucet`).
- Rozhranie (interface).
- Abstrakcia vs. enkapsulácia, najčastejšie chyby.

## Základná myšlienka
- **Abstrakcia = ukážeme len to podstatné, zložité veci schováme.**
- Príklad zo života: **diaľkový ovládač**.
  - Stlačíme „hlasnejšie“ a hlasitosť sa zvýši.
  - Vieme, **čo** tlačidlo robí. Nevieme, **ako** to televízor vnútri robí, a nemusíme.
- V programe to znamená dve veci:
  1. Do triedy dáme **len podstatné vlastnosti** reálnej veci (model).
  2. Niektoré pojmy sú príliš všeobecné na konkrétnu podobu. Vieme, **čo** musia vedieť, ale **ako** to robia, určia až konkrétni potomkovia (**abstraktná trieda**).

## Krok 1: model obsahuje len podstatné
- Skutočný klient banky má veľa vlastností: meno, číslo účtu, zostatok, farbu očí, obľúbené jedlo, výšku.
- Banku zaujíma len časť z nich. Do triedy dáme **len tie**.

![Abstrakcia — model obsahuje len podstatné vlastnosti](https://cdn.jsdelivr.net/gh/SPSITKNM/oop_opakovanie@main/assets/abstrakcia-01-podstatne-nepodstatne.svg)

```cpp
#include <iostream>
#include <string>
using namespace std;

class Ucet {
private:
    string majitel;                 // podstatné: kto účet vlastní
    string cislo;                   // podstatné: identifikácia účtu
    int zostatok;                   // podstatné: koľko peňazí je na účte
    // farba očí, obľúbené jedlo, výška: banku nezaujímajú, do modelu nepatria

public:
    Ucet(string m, string c, int z) {
        majitel = m;
        cislo = c;
        zostatok = z;
    }

    void vloz(int suma) {           // ČO vieme s účtom robiť
        if (suma > 0) {
            zostatok = zostatok + suma;
        }
    }

    bool vyber(int suma) {
        if (suma > 0 && suma <= zostatok) {
            zostatok = zostatok - suma;
            return true;
        }
        return false;
    }

    int getZostatok() const {
        return zostatok;
    }
};

int main() {
    Ucet a("Jan", "SK01", 100);
    a.vloz(50);
    a.vyber(30);
    cout << a.getZostatok() << endl;        // 120
}
```

- Čo je „podstatné“, závisí od **účelu**. Zdravotná poisťovňa by do modelu klienta dala výšku a váhu, banka nie.
- Používateľ triedy volá `vyber(30)`. Nezaujíma ho, ako presne sa kontroluje zostatok.

## Krok 2: všeobecný pojem bez konkrétnej podoby
- Predstav si, že niekto povie: „Nakresli **tvar**.“ Nevieme. Musíme sa opýtať: aký? Kruh? Štvorec? Trojuholník?
- Slovo „tvar“ je **pojem**, nie konkrétna vec. Vieme o ňom len jedno: **každý tvar má obsah**. Ako sa obsah počíta, závisí od konkrétneho tvaru.
- V programovaní takýto pojem zapíšeme ako **abstraktnú triedu**.

## Krok 3: abstraktná trieda a čistá virtuálna metóda
- Napíšeme triedu `Tvar`, ktorá povie len: „každý tvar vie vypočítať obsah“.

```cpp
class Tvar {
public:
    virtual double obsah() = 0;     // "každý tvar má obsah", ale AKO sa počíta, neviem
};
```

- Rozbor riadka `virtual double obsah() = 0;`:
  - `double obsah()` je obyčajná metóda, ktorá vráti číslo,
  - `= 0` znamená: **tu žiadny kód nebude**, doplní ho niekto iný,
  - `virtual` musí stáť pred tým (jeho význam podrobne vysvetlí pilier Polymorfizmus).
- Takejto metóde sa hovorí **čistá virtuálna metóda** (pure virtual).
- Trieda, ktorá má **aspoň jednu** čistú virtuálnu metódu, je **abstraktná**.

## Krok 4: konkrétne triedy doplnia „ako“

```cpp
#include <iostream>
using namespace std;

class Tvar {                                    // ABSTRAKTNÁ trieda
public:
    virtual double obsah() = 0;                 // čistá virtuálna metóda: bez tela
};

class Kruh : public Tvar {
private:
    double polomer;

public:
    Kruh(double r) {
        polomer = r;
    }

    double obsah() {                            // doplníme AKO pre kruh
        return 3.14 * polomer * polomer;
    }
};

class Obdlznik : public Tvar {
private:
    double a;
    double b;

public:
    Obdlznik(double x, double y) {
        a = x;
        b = y;
    }

    double obsah() {                            // iné AKO pre obdĺžnik
        return a * b;
    }
};

class Trojuholnik : public Tvar {
private:
    double zakladna;
    double vyska;

public:
    Trojuholnik(double z, double v) {
        zakladna = z;
        vyska = v;
    }

    double obsah() {                            // ešte iné AKO
        return zakladna * vyska / 2;
    }
};

int main() {
    Kruh k(2);
    Obdlznik o(3, 4);
    Trojuholnik t(4, 5);

    cout << k.obsah() << endl;                  // 12.56
    cout << o.obsah() << endl;                  // 12
    cout << t.obsah() << endl;                  // 10

    // Tvar x;                                  // CHYBA PRI PREKLADE: Tvar je abstraktný
}
```

![Abstraktná trieda Tvar a jej potomkovia](https://cdn.jsdelivr.net/gh/SPSITKNM/oop_opakovanie@main/assets/abstrakcia-02-tvar.svg)

- V diagrame je abstraktná trieda a jej abstraktná metóda písaná **kurzívou**, nad názvom je `«abstract»`.
- Každý tvar počíta obsah **inak**, ale všetky majú metódu `obsah()`. To je zaručené.

### Pravidlá abstraktnej triedy
1. **Objekt abstraktnej triedy sa nedá vytvoriť.** Nie je dokončená.

```cpp
Tvar x;         // CHYBA PRI PREKLADE: variable type 'Tvar' is an abstract class
```

2. **Potomok musí čistú virtuálnu metódu implementovať**, ak chce byť konkrétny (aby sa z neho dali vytvárať objekty). Inak zostane abstraktný aj on.

```cpp
class Trojuholnik : public Tvar {
    // obsah() nie je doplnený
};

Trojuholnik t;  // CHYBA PRI PREKLADE: Trojuholnik je stále abstraktný
```

3. **Hlavička musí sedieť**: rovnaký názov a rovnaké parametre. Iné parametre znamenajú **inú metódu**, pôvodná `= 0` ostáva nedoplnená.

```cpp
double obsah() { ... }          // sedí: doplní abstraktnú metódu
double obsah(int x) { ... }     // NESEDÍ: iná metóda, Tvar zostáva abstraktný
```

4. **`= 0` je možné len pri `virtual`.** Zápis `double obsah() = 0;` bez `virtual` je chyba.
5. Riadok `virtual double obsah() = 0;` je **zmluva**: kto chce byť tvar, musí vedieť povedať svoj obsah.

## Virtuálna vs. čistá virtuálna metóda
- Nie každá `virtual` metóda nútí potomka niečo doplniť. Núti len tá s `= 0`.

| Zápis | Názov | Potomok |
|---|---|---|
| `virtual void f() { ... }` | virtuálna metóda (má telo) | **môže** ju prekryť, nemusí |
| `virtual void f() = 0;` | čistá virtuálna metóda (bez tela) | **musí** ju implementovať |

```cpp
#include <iostream>
using namespace std;

class Zviera {
public:
    virtual void zvuk() {                       // má telo, potomok ju môže zmeniť
        cout << "..." << endl;
    }
};

class Pes : public Zviera {
public:
    void zvuk() {                               // prekryje verziu predka
        cout << "Haf" << endl;
    }
};

class Ryba : public Zviera {                    // zvuk() neprekrýva, použije sa verzia predka
};

int main() {
    Zviera z;                                   // OK: Zviera NIE JE abstraktné
    Pes p;
    Ryba r;
    z.zvuk();                                   // ...
    p.zvuk();                                   // Haf
    r.zvuk();                                   // ...
}
```

![Virtuálna vs. čistá virtuálna metóda](https://cdn.jsdelivr.net/gh/SPSITKNM/oop_opakovanie@main/assets/abstrakcia-03-virtual-vs-cista.svg)

- `Zviera` je **konkrétna** trieda, lebo nemá žiadnu metódu `= 0`. Objekt sa z nej dá vytvoriť.
- `Tvar` je **abstraktná** trieda, lebo má metódu `= 0`.
- Význam samotného `virtual` (ktorá verzia sa zavolá, keď na objekt potomka ukazuje ukazovateľ na predka) je **polymorfizmus**, ďalší pilier.

## Abstraktná trieda so spoločným kódom
- Abstraktná trieda nemusí byť len „prázdna zmluva“. Môže mať aj **hotové** atribúty a metódy, ktoré potomkovia zdedia.
- Rozdelenie práce:
  - **spoločné** veci píšeme raz v predkovi,
  - **rôzne** veci necháme ako `= 0` a doplnia ich potomkovia.
- Takto vyzerá bankový systém zo skúšky.

```cpp
#include <iostream>
using namespace std;

class Ucet {                                    // ABSTRAKTNÁ trieda
protected:
    int zostatok;

public:
    Ucet(int z) {
        zostatok = z;
    }

    virtual bool moznoVybrat(int suma) = 0;     // povie ČO (dá sa vybrať?), nie AKO

    bool vyber(int suma) {                      // hotová metóda, ktorá "prázdnu" použije
        if (moznoVybrat(suma)) {
            zostatok = zostatok - suma;
            return true;
        }
        return false;
    }

    int getZostatok() const {
        return zostatok;
    }
};

class StandartnyUcet : public Ucet {
public:
    StandartnyUcet(int z) : Ucet(z) {}

    bool moznoVybrat(int suma) {                // AKO: nesmie ísť do mínusu
        return suma > 0 && suma <= zostatok;
    }
};

class UverUcet : public Ucet {
private:
    int limit;

public:
    UverUcet(int z, int l) : Ucet(z) {
        limit = l;
    }

    bool moznoVybrat(int suma) {                // AKO: smie ísť do mínusu do limitu
        return suma > 0 && suma <= zostatok + limit;
    }
};

int main() {
    StandartnyUcet s(100);
    UverUcet u(100, 200);

    cout << s.vyber(150) << " " << s.getZostatok() << endl;     // 0 100
    cout << u.vyber(150) << " " << u.getZostatok() << endl;     // 1 -50

    // Ucet x(100);                             // CHYBA PRI PREKLADE: Ucet je abstraktný
}
```

![Abstraktný Ucet a jeho potomkovia](https://cdn.jsdelivr.net/gh/SPSITKNM/oop_opakovanie@main/assets/abstrakcia-04-ucet.svg)

- `vyber()` je napísaná **raz** v predkovi. Pri kontrole zavolá `moznoVybrat()`, ktorú doplní konkrétny potomok.
- Zmena pravidla výberu sa robí len v potomkovi, `vyber()` ostáva nedotknutá.
- To, že `vyber()` z predka zavolá verziu `moznoVybrat()` z **potomka**, je polymorfizmus. Podrobne ho rozoberá ďalší pilier.

## Rozhranie (interface)
- **Rozhranie** je abstraktná trieda, ktorá má **len čisté virtuálne metódy** a žiadne dáta.
- Popisuje len „čo vie“, bez akejkoľvek implementácie. Je to čistá zmluva.
- C++ nemá pre rozhranie samostatné kľúčové slovo (ako Java alebo C# `interface`), používa sa abstraktná trieda.

```cpp
#include <iostream>
#include <string>
using namespace std;

class Tlacitelne {                              // ROZHRANIE: len čisté virtuálne metódy
public:
    virtual void tlac() = 0;
};

class Faktura : public Tlacitelne {
private:
    int cislo;

public:
    Faktura(int c) {
        cislo = c;
    }

    void tlac() {                               // implementuje zmluvu
        cout << "Tlacim fakturu c. " << cislo << endl;
    }
};

class Fotka : public Tlacitelne {
private:
    string nazov;

public:
    Fotka(string n) {
        nazov = n;
    }

    void tlac() {                               // iná implementácia tej istej zmluvy
        cout << "Tlacim fotku " << nazov << endl;
    }
};

int main() {
    Faktura f(101);
    Fotka o("more.jpg");
    f.tlac();                                   // Tlacim fakturu c. 101
    o.tlac();                                   // Tlacim fotku more.jpg
}
```

![Rozhranie Tlacitelne a jeho implementácie](https://cdn.jsdelivr.net/gh/SPSITKNM/oop_opakovanie@main/assets/abstrakcia-05-rozhranie.svg)

- Rozhranie hovorí: „kto chce byť tlačiteľný, musí vedieť `tlac()`.“
- Nesúvisiace triedy (`Faktura`, `Fotka`) môžu implementovať to isté rozhranie.
- V diagrame sa rozhranie značí `«interface»` a implementácia **prerušovanou šípkou** s prázdnym trojuholníkom.

## Abstrakcia vs. enkapsulácia
- Pletú sa, lebo obe niečo skrývajú. Líšia sa cieľom.

![Enkapsulácia vs. abstrakcia](https://cdn.jsdelivr.net/gh/SPSITKNM/oop_opakovanie@main/assets/abstrakcia-06-vs-enkapsulacia.svg)

| | Enkapsulácia | Abstrakcia |
|---|---|---|
| Otázka | **Ako** ochránim dáta? | **Čo** ukážem používateľovi? |
| Nástroj | `private`, gettery, settery | zjednodušené rozhranie, abstraktná trieda |
| Skrýva | dáta (atribúty) | zložitosť (ako to funguje) |
| Príklad | `zostatok` je `private` | používateľ vidí `vyber()`, nie pravidlá |

- Skratka: **enkapsulácia = zámok na dátach, abstrakcia = zjednodušený ovládací panel.**

## Najčastejšie chyby
- **Pokus vytvoriť objekt abstraktnej triedy** (`Tvar x;`). Vytvárame len konkrétnych potomkov.
- **Potomok nedoplnil čistú virtuálnu metódu**, a tak zostal abstraktný.
- **Iná hlavička v potomkovi** (`obsah(int)` namiesto `obsah()`). Je to iná metóda a `= 0` ostáva nedoplnená.
- **`= 0` bez `virtual`.** Prekladač zápis odmietne.
- **Zámena `virtual` a `virtual ... = 0`.** Len druhá vyžaduje implementáciu od potomka.
- **Abstrakcia ako „všetko schovať“.** Do modelu dávame len podstatné, nie všetko a nie nič.

## Úlohy na cvičenie
- Vytvorte abstraktnú triedu `Zviera` s čistou virtuálnou metódou `zvuk()` a potomkov `Pes` a `Macka`. Skúste vytvoriť objekt `Zviera`. Čo sa stane?
- Do hierarchie tvarov pridajte `Stvorec` s vlastným výpočtom obsahu a pridajte do `Tvar` druhú čistú metódu `obvod()`. Doplňte ju všetkým potomkom.
- Doplňte hierarchiu účtov o `SporiaciUcet`, ktorý povolí výber najviac 500 eur naraz (upravte len `moznoVybrat`).
- Navrhnite rozhranie `Prehratelne` s metódou `prehraj()` a implementujte ho v triedach `Pesnicka` a `Video`. Nakreslite triedny diagram.
- Vysvetlite vlastnými slovami, prečo je `Zviera` z ukážky s obyčajnou `virtual` metódou konkrétna a `Tvar` abstraktný.

## Kontrolné otázky
- Čo je abstrakcia? Uveďte príklad.
- Čo je abstraktná trieda a čo čistá virtuálna metóda? Ako sa zapisuje?
- Dá sa vytvoriť objekt abstraktnej triedy? Prečo?
- Čo musí urobiť potomok, aby sa z neho dali vytvárať objekty?
- Aký je rozdiel medzi `virtual` a `virtual ... = 0`?
- Čo je rozhranie (interface) a ako sa v C++ zapisuje?
- Ako sa v triednom diagrame značí abstraktná trieda, abstraktná metóda a rozhranie?
- Aký je rozdiel medzi abstrakciou a enkapsuláciou?

### Vzorová odpoveď: princíp abstrakcie
> Abstrakcia znamená ukázať len podstatné a skryť zložitosť. V triede modelujeme len tie vlastnosti reálnej veci, ktoré sú pre problém dôležité. V C++ ju vyjadrujeme aj abstraktnými triedami: trieda s aspoň jednou čistou virtuálnou metódou (`virtual void f() = 0;`) určuje, **čo** musia potomkovia vedieť, ale nehovorí **ako**. Objekt abstraktnej triedy sa nedá vytvoriť, konkrétny potomok musí čisté virtuálne metódy implementovať.

---

# Triedy a objekty (objektová orientácia) 2024/25

## Osnova hodiny
- Objektový prístup (prečo potrebujeme objekty).
- Triedy, objekty,...
- Príklad.

## Prečo potrebujeme objekty?

### Udržateľnosť softvéru (maintenance)
- Štúdia Lientz a Swanson (1980).
- 487 rôznych systémov.
- Koľko úsilia to vyžaduje?

### Kedy to začalo?
- Jazyk Simula 67 (Ole-Johan Dahl a Kristen Nygaard, Norwegian Computing Center, 1960+)
  - triedy a inštancie (objekty)
  - automatické zanikanie objektov (garbage collection)
- Jazyk Smalltalk (Xerox PARC, Alan Kay a ďalší, 1970+)
  - pojem „objektovo-orientované programovanie“
  - použitie objektov a správ, ktoré si objekty posielajú a spracovávajú

## Objektová orientácia…
- Objektové techniky pomáhajú písať lepšie udržateľný softvér.
- Metóda a jazyk.
- Implementácia a prostredie.
- Knižnice.

## Metóda a jazyk
- Nejde len o programovací jazyk a spôsob jeho použitia.
- Ide aj o spôsob uvažovania a vyjadrovania...
- …a taktiež o záznamy v textovej alebo grafickej forme.

## Model domény
- Podpora vývoja.
- Vlastnosti a efektivita nástrojov pre vývoj.
- Nástroje pre podporu nasadzovania nových verzií.
- Nástroje pre podporu dokumentovania.

## Knižnice
- Objektové technológie veľmi spoliehajú na opakovanú použiteľnosť.
- Podpora vývoja formou využitia už implementovaných riešení (knižníc).
- Podpora vytvárania a správy nových vlastných knižníc.

## Máme byť dogmatickí?
- Objektovo orientovaný prístup sa dnes chápe ako základný nástroj pre vývoj softvéru. Avšak…
  - Existujú rôzne programovacie jazyky s rôznou mierou podpory techník objektového programovania (OOP).
  - Nie každý potrebuje všetky vlastnosti, ktoré OOP ponúka.
  - Objektová orientácia môže byť len jedným z faktorov úspešného vývoja, preto je potrebné uvažovať komplexnejšie.

## Metóda a jazyk – Triedy
- Triedy ako moduly.
- Triedy ako typy.
- Zasielanie správ (message passing, feature-based computation).
- Skrývanie informácií.
- Statická kontrola typov.
- Dedičnosť, redefinícia, polymorfizmus a dynamická väzba.
- Generickosť.
- Správa pamäte a garbage collection.

## Trieda
### Triedy
- Objektovo orientovaný prístup je postavený na pojme trieda.
- Triedu môžeme chápať ako časť softvéru, ktorá popisuje abstraktný dátový typ a jeho implementáciu.
- Abstraktným dátovým typom rozumieme objekty so spoločným správaním reprezentovaným zoznamom operácií, ktoré objekty vykonávajú.

## Triedy ako moduly
- OOP je najmä o štruktúre (architektúre) softvéru, kde je dôležitá modularita.
- Triedy nepopisujú len typy objektov, ale musia byť zároveň modulárne jednotky.
- V čisto objektovo orientovaných programoch by nemali byť iné samostatné jednotky ako triedy (napr. funkcie).

## Triedy ako typy
- V čisto objektovo orientovaných jazykoch a programoch by nemali byť iné typy ako triedy.
- Platí to aj pre systémové typy ako INT alebo DOUBLE.

## Zasielanie správ
- Message passing (feature call), feature-based computation je výpočtový mechanizmus.
- Objektu ako inštancii triedy je zaslaná správa daného mena a s potrebnými parametrami.
- Napr. `aPerson->ChangeLastName(“Smith”)`.
- Ten, kto zasiela správu (požaduje vykonanie operácie s určitými argumentmi), je KLIENT triedy.

## Skrývanie informácií
- Pre klienta sú dôležité iba tie operácie (metódy), ktoré popisujú vonkajšie správanie objektov triedy.
- Detaily implementácie by mali zostať skryté (dáta + pomocné operácie).
- Ak klient potrebuje získať informácie o stave (dátach) objektu, dostane sa k nim len prostredníctvom zaslania správy (volaním metódy, nie premennej).

## Statická väzba a kontrola typov
- Každá entita v programe (napr. premenná daného mena) musí mať definovaný typ.
- Požiadavka na objekt (zaslanie správy) musí zodpovedať operácii (metóde), ktorú trieda poskytuje.

## Generickosť
- Potreba existencie tried, ktoré vedia pracovať s typom, ktorý nie je vopred známy.
- Napr. zoznamy, do ktorých možno ukladať objekty rôznych tried (typov).

## Dedičnosť a redefinícia
- Dedičnosť znamená založenie novej triedy na základe už existujúcej triedy.
- Základom je rozšírenie pôvodnej triedy o nové vlastnosti.
- Dedičnosť taktiež umožňuje zmeniť niektoré vlastnosti pôvodnej triedy.

## Polymorfizmus a dynamická väzba
- Potreba, aby ten istý objekt vystupoval v rôznych kontextoch v rôznych rolách.
- Rolou rozumieme rôzne správanie, ktoré sa môže meniť v čase.

## Správa pamäte a garbage collection
- V rozsiahlych programoch vzniká a zaniká mnoho objektov, a to v rôznych a nie vždy jednoduchých situáciách.
- Je problém manuálne sledovať životný cyklus objektov.
- V moderných jazykoch je zanikanie objektov potrebné automatizovať.

## Príklad
### Deklarácia

## KeyValue Class Example implementácia v jazyku C++
- Konštruktor inicializuje objekt (plní pamäť dátami, ktoré objekt používa)

```cpp
#include <iostream>
using namespace std;

class KeyValue {
private:
    int key;
    double value;

public:
    KeyValue(int k, double v);
    int GetKey();
    double GetValue();
};
```

## KeyValues Class implementácia v jazyku C++
- Destruktor odstraňuje dáta objektu (uvoľňuje pamäť, ktorú objekt zaberá)
  
```cpp
class KeyValues {
private:
    KeyValue** keyValues;
    int count;

public:
    KeyValues(int n);
    ~KeyValues();
    KeyValue* CreateObject(int k, double v);
    KeyValue* SearchObject(int key);
    int Count();
};
```


## KeyValues Class implementácia v jazyku C#

```csharp
class KeyValue {
    private int key;
    private double value;

    public KeyValue(int k, double v) {
        key = k;
        value = v;
    }

    public int GetKey() {
        return key;
    }

    public double GetValue() {
        return value;
    }
}

class KeyValues {
    private KeyValue[] keyValues;
    private int count;

    public KeyValues(int n) {
        keyValues = new KeyValue[n];
        count = 0;
    }

    ~KeyValues() {
        // Destructor implementation (in C#, cleanup typically handled by GC)
    }

    public KeyValue CreateObject(int k, double v) {
        if (count < keyValues.Length) {
            keyValues[count] = new KeyValue(k, v);
            return keyValues[count++];
        }
        return null;
    }

    public KeyValue SearchObject(int key) {
        foreach (KeyValue kv in keyValues) {
            if (kv != null && kv.GetKey() == key) {
                return kv;
            }
        }
        return null;
    }

    public int Count() {
        return count;
    }
}
```

### Použitie
- Použitie kľúčového slova `new` zabezpečí vznik objektu (alokuje pamäť pre dáta („plochú“ časť) objektu).

## Main Function implementácia v C++

```cpp
int main() {
    int N = 5;
    KeyValues* myKeyValues = new KeyValues(N);

    KeyValue* myKeyValue = myKeyValues->CreateObject(0, 0.5);
    cout << myKeyValue->GetValue() << endl;

    for (int i = 1; i < N; i++) {
        myKeyValues->CreateObject(i, i + 0.5);
    }
    cout << myKeyValues->SearchObject(4)->GetValue() << endl;

    delete myKeyValues;

    // cout << myKeyValue->GetKey() << endl;

    getchar();
    return 0;
}
```

## Main Function implementácia v C#

```csharp
using System;

class Program {
    static void Main() {
        int N = 5;
        KeyValues myKeyValues = new KeyValues(N);

        KeyValue myKeyValue = myKeyValues.CreateObject(0, 0.5);
        Console.WriteLine(myKeyValue.GetValue());

        for (int i = 1; i < N; i++) {
            myKeyValues.CreateObject(i, i + 0.5);
        }
        Console.WriteLine(myKeyValues.SearchObject(4).GetValue());

        // In C#, explicit deletion is not required (handled by garbage collector).
        // No need for: delete myKeyValues;

        // Console.WriteLine(myKeyValue.GetKey());

        Console.ReadKey();
    }
}
```

### Výsledok
- Definícia (implementácia).

```csharp
0.5
4.5
```

### Definícia ( implementácia )


### KeyValues Class Method definicia v jazyku C++

```cpp
KeyValues::KeyValues(int n) {
    this->keyValues = new KeyValue*[n];
    this->count = 0;
}

KeyValues::~KeyValues() {
    for (int i = 0; i < this->count; i++) {
        delete this->keyValues[i];
    }
    delete[] this->keyValues;
}

int KeyValues::Count() {
    return this->count;
}

KeyValue* KeyValues::CreateObject(int k, double v) {
    KeyValue* newObject = new KeyValue(k, v);
    this->keyValues[this->count] = newObject;
    this->count += 1;
    return newObject;
}

KeyValue* KeyValues::SearchObject(int k) {
    for (int i = 0; i < this->count; i++) {
        if (this->keyValues[i]->GetKey() == k) {
            return this->keyValues[i];
        }
    }
    return nullptr;
}
```


## KeyValues Class Method definícia v jazyku C#

```csharp
class KeyValues {
    private KeyValue[] keyValues;
    private int count;

    public KeyValues(int n) {
        this.keyValues = new KeyValue[n];
        this.count = 0;
    }

    ~KeyValues() {
        // Destructor in C# is rarely needed (handled by garbage collector)
        // However, if manual cleanup is needed, implement IDisposable and use Dispose pattern.
    }

    public int Count() {
        return this.count;
    }

    public KeyValue CreateObject(int k, double v) {
        KeyValue newObject = new KeyValue(k, v);
        this.keyValues[this.count] = newObject;
        this.count += 1;
        return newObject;
    }

    public KeyValue SearchObject(int k) {
        for (int i = 0; i < this.count; i++) {
            if (this.keyValues[i].GetKey() == k) {
                return this.keyValues[i];
            }
        }
        return null;
    }
}
```


## Úlohy na cvičenie
- Implementujte príklad z prednášky a do triedy `KeyValues` pridajte metódu `KeyValue* RemoveObject(int k)`, ktorá odstráni objekt s daným kľúčom a vráti ukazovateľ na neho.
- Implementujte triedu `Faktura`, ktorá bude obsahovať číslo, objekt triedy `Osoba` (s menom a adresou) a pole objektov `PolozkaFaktury` (s názvom a cenou). Navrhnite konštruktor a destruktor a ďalšie potrebné metódy. Faktura bude mať metódu (funkciu), ktorá vypočíta a vráti celkovú cenu.

## Kontrolné otázky
- Aké sú hlavné príčiny potreby zmien softvéru?
- Aké sú hlavné faktory ovplyvňujúce objektovú orientáciu?
- Vysvetlite, čo rozumieme pojmom objektovo orientovaná metóda (prístup) a jazyk.
- Vysvetlite, čo rozumieme podporou objektovo orientovanej implementácie.
- Vysvetlite, čo rozumieme podporou opakovanej použiteľnosti.
- Vysvetlite pojmy trieda a objekt a použite správnu terminológiu.
- Zdôraznite vlastnosti triedy z pohľadu modularity.
- Vysvetlite princíp zapuzdrenia v OOP.
- Vysvetlite princíp zasielania správ.
- Vysvetlite princípy deklarácie a definície jednoduchej triedy v C++ / C#.
- 
---

# Návrh programu I 2024/25

## Osnova hodiny
- Čo vieme?
- Objektový návrh programu
- Príklad

## Čo vieme?

### Trieda
- Trieda je popisom objektov so spoločnými vlastnosťami.

## Class Template v jazyku C++

```cpp
class <meno> {
    private:
        <súkromné členské položky>
    public:
        <verejné členské položky>
};
```
## Class Template v jazyku C#

```csharp
class <Name> {
    // Private member variables
    private <private members>;

    // Public member methods and properties
    public <public members>;
}
```
- Členskými položkami môžu byť premenné (dáta) a metódy (funkcie).

### Objekt
- Objekt je inštanciou – pamäťovou reprezentáciou – triedy.
- Objekt je reprezentáciou nejakej entity, ktorá má stav reprezentovaný dátami a správanie reprezentované metódami.

### Konštruktor
- Konštruktor inicializuje objekty.
- Nemá návratovú hodnotu.
- Ak nie je deklarovaný, automaticky sa vytvorí implicitný konštruktor.
- Volá sa automaticky pri statickej deklarácii alebo použitím `new`.
- Konštruktorov môže byť viac, musia sa líšiť počtom alebo typom parametrov.

### Destruktor
- Slúži na dealokáciu pamäte vytvorenej dynamicky.
- Nemá návratovú hodnotu.
- Ak nie je deklarovaný, automaticky sa vytvorí implicitný destruktor.
- Volá sa automaticky pri statickej deklarácii alebo použitím `delete`.

## Objektový návrh

### Zadanie
- Majme malú banku s obmedzeným počtom klientov a účtov. V banke môžu klienti a účty pribúdať.
- Každý účet má jedného vlastníka a môže mať jedného partnera, obaja sú klienti banky a majú meno a kód. Na účty je možné vkladať a vyberať z nich, je možné zistiť stav na účte. Ak na účte nie je dostatok peňazí, nie je možné vybrať.
- Vklady na účtoch sú úročené, a to buď základnou alebo špeciálnou úrokovou sadzbou. Raz za čas banka všetkým účtom pripíše úrok zodpovedajúci úrokovej sadzbe.
- Účet resp. klienta je možné v banke vyhľadať podľa čísla resp. kódu.
- Je možné zistiť, ale nie meniť:
  - číslo účtu a jeho úrokovú sadzbu,
  - kód a meno klienta,
  - vlastníka a partnera účtu.

## Triedy
- Majme malú banku s obmedzeným počtom klientov a účtov. V banke môžu klienti a účty pribúdať.
- Každý účet má jedného vlastníka a môže mať jedného partnera, obaja sú klienti banky a majú meno a kód. Na účty je možné vkladať a vyberať z nich, je možné zistiť stav na účte. Ak na účte nie je dostatok peňazí, nie je možné vybrať.
- Vklady na účtoch sú úročené, a to buď základnou alebo špeciálnou úrokovou sadzbou. Raz za čas banka všetkým účtom pripíše úrok zodpovedajúci úrokovej sadzbe.
- Účet resp. klienta je možné v banke vyhľadať podľa čísla resp. kódu.

## Správanie
- Majme malú banku s obmedzeným počtom klientov a účtov. V banke môžu klienti a účty pribúdať.
- Každý účet má jedného vlastníka a môže mať jedného partnera, obaja sú klienti banky a majú meno a kód. Na účty je možné vkladať a vyberať z nich, je možné zistiť stav na účte. Ak na účte nie je dostatok peňazí, nie je možné vybrať.
- Vklady na účtoch sú úročené, a to buď základnou alebo špeciálnou úrokovou sadzbou. Raz za čas banka všetkým účtom pripíše úrok zodpovedajúci úrokovej sadzbe.
- Účet resp. klienta je možné v banke vyhľadať podľa čísla resp. kódu.

## Stav
- Majme malú banku s obmedzeným počtom klientov a účtov. V banke môžu klienti a účty pribúdať.
- Každý účet má jedného vlastníka a môže mať jedného partnera, obaja sú klienti banky a majú meno a kód. Na účty je možné vkladať a vyberať z nich, je možné zistiť stav na účte. Ak na účte nie je dostatok peňazí, nie je možné vybrať.
- Vklady na účtoch sú úročené, a to buď základnou alebo špeciálnou úrokovou sadzbou. Raz za čas banka všetkým účtom pripíše úrok zodpovedajúci úrokovej sadzbe.
- Účet resp. klienta je možné v banke vyhľadať podľa čísla resp. kódu.

## Trieda `Client`
- Kód a meno.
- Dá sa na ne spýtať.
- Nedajú sa meniť.

## Trieda `Account`
- Číslo a suma, vlastník a partner, úroková sadzba.
- Dá sa na ne spýtať.
- Číslo, úrokovú sadzbu, vlastníka a partnera nie je možné meniť.
- Vložiť, vybrať, zistiť stav, pripísať úrok.
- Niekedy nie je možné vybrať.

## Trieda `Bank`
- Obmedzený zoznam klientov a účtov.
- Možno pridať nového klienta a účet.
- Možno hromadne pripísať úrok podľa úrokovej sadzby.
- Možno vyhľadať klienta podľa kódu a účet podľa čísla.

## Príklad
## Deklarácia

## Client Class príklad implementácie v C++

```cpp
class Client {
private:
    int code;
    string name;

public:
    Client(int c, string n);
    int GetCode();
    string GetName();
};
```

## Client Class príklad implementácie v C#

```csharp
class Client {
    private int code;
    private string name;

    public Client(int c, string n) {
        this.code = c;
        this.name = n;
    }

    public int GetCode() {
        return code;
    }

    public string GetName() {
        return name;
    }
}
```


## Account and Bank Classes v jazyku C++

```cpp
class Account {
private:
    int number;
    double balance;
    double interestRate;
    Client* owner;
    Client* partner;

public:
    Account(int n, Client* c);
    Account(int n, Client* c, double ir);
    Account(int n, Client* c, Client* p);
    Account(int n, Client* c, Client* p, double ir);

    int GetNumber();
    double GetBalance();
    double GetInterestRate();
    Client* GetOwner();
    Client* GetPartner();
    bool CanWithdraw(double a);

    void Deposit(double a);
    bool Withdraw(double a);
    void AddInterest();
};

class Bank {
private:
    Client** clients;
    int clientsCount;
    Account** accounts;
    int accountsCount;

public:
    Bank(int c, int a);
    ~Bank();

    Client* GetClient(int c);
    Account* GetAccount(int n);

    Client* CreateClient(int c, string n);
    Account* CreateAccount(int n, Client* c);
    Account* CreateAccount(int n, Client* c, double ir);
    Account* CreateAccount(int n, Client* c, Client* p);
    Account* CreateAccount(int n, Client* c, Client* p, double ir);

    void AddInterest();
};
```


## Account and Bank Classes v jazyku C#

```csharp
class Account {
    private int number;
    private double balance;
    private double interestRate;
    private Client owner;
    private Client partner;

    public Account(int n, Client c) {
        this.number = n;
        this.owner = c;
    }

    public Account(int n, Client c, double ir) {
        this.number = n;
        this.owner = c;
        this.interestRate = ir;
    }

    public Account(int n, Client c, Client p) {
        this.number = n;
        this.owner = c;
        this.partner = p;
    }

    public Account(int n, Client c, Client p, double ir) {
        this.number = n;
        this.owner = c;
        this.partner = p;
        this.interestRate = ir;
    }

    public int GetNumber() { return number; }
    public double GetBalance() { return balance; }
    public double GetInterestRate() { return interestRate; }
    public Client GetOwner() { return owner; }
    public Client GetPartner() { return partner; }
    public bool CanWithdraw(double a) { return balance >= a; }

    public void Deposit(double a) { balance += a; }
    public bool Withdraw(double a) {
        if (CanWithdraw(a)) {
            balance -= a;
            return true;
        }
        return false;
    }
    public void AddInterest() { balance += balance * interestRate; }
}

class Bank {
    private Client[] clients;
    private int clientsCount;
    private Account[] accounts;
    private int accountsCount;

    public Bank(int c, int a) {
        clients = new Client[c];
        accounts = new Account[a];
        clientsCount = 0;
        accountsCount = 0;
    }

    ~Bank() {
        // Destructor logic not needed in C#
    }

    public Client GetClient(int c) { return clients[c]; }
    public Account GetAccount(int n) { return accounts[n]; }

    public Client CreateClient(int c, string n) {
        Client newClient = new Client(c, n);
        clients[clientsCount++] = newClient;
        return newClient;
    }

    public Account CreateAccount(int n, Client c) {
        Account newAccount = new Account(n, c);
        accounts[accountsCount++] = newAccount;
        return newAccount;
    }

    public Account CreateAccount(int n, Client c, double ir) {
        Account newAccount = new Account(n, c, ir);
        accounts[accountsCount++] = newAccount;
        return newAccount;
    }

    public Account CreateAccount(int n, Client c, Client p) {
        Account newAccount = new Account(n, c, p);
        accounts[accountsCount++] = newAccount;
        return newAccount;
    }

    public Account CreateAccount(int n, Client c, Client p, double ir) {
        Account newAccount = new Account(n, c, p, ir);
        accounts[accountsCount++] = newAccount;
        return newAccount;
    }

    public void AddInterest() {
        foreach (var account in accounts) {
            if (account != null) {
                account.AddInterest();
            }
        }
    }
}
```

### Tri typy metód
- **Konštruktory a destruktor:** Konštruktory inicializujú stav objektu po jeho vzniku, destruktor uvoľňuje dynamicky pridelenú pamäť pred zánikom objektu. Ak nie sú uvedené, vytvoria sa tieto metódy automaticky (bez algoritmu).
- **Metódy poskytujúce informácie o stave objektu:** Metódy buď priamo podávajú informáciu o hodnote dátovej položky objektu alebo poskytujú informáciu na základe algoritmu.
- **Metódy meniace stav objektu:** Metódy buď priamo zmenia hodnotu dátovej položky objektu alebo vykonajú zmenu na základe algoritmu.
- **Metódy poskytujúce informácie o stave objektu by nemali meniť jeho stav!!!**

## Objektové kompozície
- Objekt sa môže stať súčasťou iného objektu a stáva sa tak jeho dátovou položkou.
- Vznikajú tak komponované objekty s presne definovanými kompetenciami. Tie môžu realizovať prostredníctvom interakcie objektov, z ktorých sú komponované.
- Napríklad účet má klientov v rolách vlastníka a partnera resp. banka má klientov a účty.
- Jeden a ten istý objekt môže byť súčasťou viacerých kompozícií. Napríklad jeden klient môže byť súčasťou ako účtu, tak banky.

## Vzťahy medzi objektmi — asociácia, agregácia, kompozícia

Skladanie má tri podoby. Všetky sú vzťah „MÁ / POZNÁ“; líšia sa v tom,
**kto vlastní životný cyklus časti** a **či sa časť dá zdieľať**.

| Vzťah | UML značka (pri celku) | Časť existuje sama? | Zdieľateľná? | Zaniká s celkom? |
|---|---|---|---|---|
| Asociácia | plná čiara | áno | áno | nie |
| Agregácia | prázdny kosoštvorec `◇` | áno | áno | nie |
| Kompozícia | plný kosoštvorec `◆` | nie | nie (patrí 1 celku) | áno |

### Asociácia — „poznám iný objekt“

Objekt si drží odkaz na iný, aby ho vedel požiadať o službu. Ani jeden druhého nevlastní.

```cpp
class SeaUrchin {
public:
    void beEaten() { std::cout << "Jezko: som zjedeny!\n"; }
};

class Otter {
    SeaUrchin* food = nullptr;        // asociacia — iba odkaz
public:
    void setFood(SeaUrchin* u) { food = u; }
    void eat() { if (food) food->beEaten(); }
};

int main() {
    SeaUrchin urchin;                 // objekty vznikaju nezavisle
    Otter otter;
    otter.setFood(&urchin);
    otter.eat();                      // "Jezko: som zjedeny!"
}                                     // obaja zanikaju samostatne
```

`otter.beEaten()` neexistuje — vydra iba drží odkaz, metódu vykoná ježko
(`otter.food->beEaten()`). Asociácia neprenáša metódy druhej triedy; to robí len dedičnosť.

### Agregácia — „celok–časť, časť je samostatná“

Časť vznikne zvonku a celok si ju len pridá. Tá istá časť môže byť vo viacerých
celkoch. Keď celok zanikne, časti žijú ďalej.

```cpp
class Tortoise {
public:
    std::string name;
    Tortoise(std::string n) { name = n; }   // konstruktor — nastavi meno
};

class Creep {                         // skupina korytnaciek
    std::vector<Tortoise*> members;   // agregacia — odkazy, nevlastni ich
public:
    void add(Tortoise* t) { members.push_back(t); }
};

int main() {
    Tortoise franklin("Franklin");    // korytnacka vznika SAMA, mimo skupiny
    Creep beach, zoo;
    beach.add(&franklin);
    zoo.add(&franklin);               // ta ista korytnacka v dvoch skupinach
}                                     // skupiny zaniknu, franklin stale existuje
```

### Kompozícia — „časť nemôže existovať bez celku“

Časť vzniká vnútri celku a zaniká s ním. Patrí práve jednému celku, nedá sa zdieľať.

```cpp
class Lobby    { /* ... */ };
class Bathroom { /* ... */ };

class VisitorCenter {
    Lobby lobby;                      // kompozicia — hodnotovy clen
    std::vector<Bathroom> bathrooms;  // kompozicia — celok ich vytvara a vlastni
public:
    VisitorCenter() {
        bathrooms.emplace_back();     // casti vznikaju TU, vnutri celku
    }
};

int main() {
    VisitorCenter vc;                 // spolu s nim vznikli lobby aj bathroom
}                                     // vc zanika -> lobby a bathrooms zanikaju s nim
```

Nikde nie je `new Lobby()` zvonku. „Lobby bez budovy“ nedáva zmysel.

### Násobnosť (multiplicity)

Číslo na konci čiary = koľko objektov tej triedy pripadá na **jeden** objekt druhej strany.

| Zápis | Význam |
|---|---|
| `1` | práve jeden (povinný) |
| `0..1` | nula alebo jeden (nepovinný) |
| `*` / `0..*` | ľubovoľne veľa |
| `1..*` | aspoň jeden |

Príklad: `VisitorCenter  1 ◆────── 1..*  Bathroom` — každé centrum má aspoň
jednu toaletu, každá toaleta patrí práve jednému centru.

## Úlohy na cvičenie
- Implementujte príklad z prednášky a navrhnite kód, ktorý bude používať všetky triedy. Vytvorte desiatky klientov a účtov v banke a nasimulujte niektoré bežné úkony vykonávané v banke.
- Navrhnite a implementujte podobnú úlohu, ako napríklad lekársku ordináciu, malú školu a pod.

## Kontrolné otázky
- Vysvetlite, ako vznikajú objekty triedy, pojem konštruktor a princípy práce s ním v C++ / C#.
- Vysvetlite, ako zanikajú objekty triedy, pojem destruktor a princípy práce s ním v C++ / C#.
- Vysvetlite rozdiel medzi statickou a dynamickou deklaráciou objektov v C++ / C#.
- Ako sa dá postupovať, ak chceme v zadaní programu nájsť triedy, ich metódy a dátové členy?
- Kedy a prečo potrebujeme použiť viac konštruktorov jednej triedy?

--- 

# Objektová dekompozícia a trieda ako objekt 2024/25

## Osnova hodiny
- Čo je lepšie? Funkcie alebo objekty?
- Môže byť trieda zároveň objektom?
- Príklad.

## Funkcie alebo objekty?

### Funkcie vs objekty
- Je lepšie založiť štruktúru programu na funkciách alebo dátach?
- Na návrh systému môžeme nahliadať dvoma spôsobmi:
  - Ako na sadu funkcií (odpovedá na otázku, **ČO** systém bude robiť).
  - Ako na sadu objektov, ktoré spolupracujú (odpovedá na otázku, **KTO** bude zabezpečovať funkčnosť).

### Problémy
- Rozšíriteľnosť
- Opakovaná použiteľnosť
- Kombinovateľnosť

## Príklad zadania
- Majme malú banku s obmedzeným počtom klientov a účtov. V banke môžu klienti a účty pribúdať.
- Každý účet má jedného vlastníka a môže mať jedného partnera, obaja sú klienti banky a majú meno a kód. Na účty je možné vkladať a vyberať z nich, je možné zistiť stav na účte. Ak na účte nie je dostatok peňazí, nie je možné vybrať.
- Vklady na účtoch sú úročené buď základnou alebo špeciálnou úrokovou sadzbou. Raz za čas banka všetkým účtom pripíše úrok zodpovedajúci úrokovej sadzbe.
- Účet resp. klienta je možné v banke vyhľadať podľa čísla resp. kódu.

## Funkcie alebo objekty?
- Zhora nadol alebo naopak?
- Prečo objekty?

## Triedy ako objekty? Prečo?

### Trieda ako objekt
- Objektovo orientovaný prístup všeobecne vychádza z predpokladu, že „všetko je objekt“ (teda aj typy sú objekty).
- Môže byť trieda objektom? A za akých podmienok?
- Objekty majú svoj stav a správanie...

### Stav a správanie triedy
- Stav je reprezentovaný dátami.
- Správanie je reprezentované metódami.
- Musí byť splnené zapuzdrenie a skrytie informácií.
- Triede sa musí dať zaslať správa (zavolať jej metódu).

## Príklad

### Deklarácia a definícia

## StaticValue Class príklad v C++

```cpp
class StaticValue {
private:
    static int value;

public:
    static void IncValue();
    static int GetValue();
};

int StaticValue::value = 0;

void StaticValue::IncValue() {
    StaticValue::value += 1;
}

int StaticValue::GetValue() {
    return StaticValue::value;
}
```

## StaticValue Class príklad v C#

```csharp
class StaticValue {
    private static int value = 0;

    public static void IncValue() {
        value += 1;
    }

    public static int GetValue() {
        return value;
    }
}
```

### Použitie

## StaticValue použitie príklad v C++

```cpp
int main() {
    cout << StaticValue::GetValue() << endl;
    StaticValue::IncValue();
    cout << StaticValue::GetValue() << endl;

    StaticValue* sv = new StaticValue();
    cout << sv->GetValue() << endl;

    getchar();
    return 0;
}
```
## StaticValue použitie príklad v C#

```csharp
using System;

class Program {
    static void Main() {
        Console.WriteLine(StaticValue.GetValue());
        StaticValue.IncValue();
        Console.WriteLine(StaticValue.GetValue());

        StaticValue sv = new StaticValue();
        Console.WriteLine(sv.GetValue());

        Console.ReadKey();
    }
}
```

## Ako to funguje...
- Dáta a metódy deklarované ako „static“ patria triede.
- Prístup k nim však majú aj objekty (inštancie) triedy.
- Je potrebné rozlišovať medzi triednymi a inštančnými premennými a metódami.

## Vhodné konvencie
- V kontexte triedy sa pri prístupe k dátam alebo metódam nemusí uvádzať adresát správy.
- Pre zabránenie nedorozumeniam je vhodné:
  - pre prístup k inštančným dátam/metódam používať formu `OBJECT_NAME->METHOD_NAME`
  - pre prístup k triednym dátam/metódam používať formu `CLASS_NAME::METHOD_NAME`

## Adresát správy
- Adresátom správy je buď:
  - objekt (inštancia) tejto triedy v prípade inštančnej premennej alebo metódy,
  - alebo sama trieda v prípade triednej (static) premennej alebo metódy.

## Kde je rozdiel?

## StaticValue Class definícia v C++

```cpp
class StaticValue {
private:
    static int value;
    StaticValue();

public:
    static void IncValue();
    static int GetValue();
};
```


## StaticValue Class definícia v C#

```csharp
class StaticValue {
    private static int value;

    // Constructor
    private StaticValue() { }

    public static void IncValue() {
        value += 1;
    }

    public static int GetValue() {
        return value;
    }
}
```

### Trieda bez objektov

## Implementácia v jazyku C++

```cpp
#include <iostream>
using namespace std;

class StaticValue {
public:
    static int value;
    
    static int GetValue() {
        return value;
    }
    
    static void IncValue() {
        value++;
    }
};

int StaticValue::value = 0;

int main() {
    cout << StaticValue::GetValue() << endl;
    StaticValue::IncValue();
    cout << StaticValue::GetValue() << endl;

    StaticValue *sv = new StaticValue();
    cout << sv->GetValue() << endl;

    getchar();
    return 0;
}
```

## Implementácia v jazyku C#

```csharp
using System;

class StaticValue
{
    public static int value = 0;

    public static int GetValue()
    {
        return value;
    }

    public static void IncValue()
    {
        value++;
    }
}

class Program
{
    static void Main(string[] args)
    {
        Console.WriteLine(StaticValue.GetValue());
        StaticValue.IncValue();
        Console.WriteLine(StaticValue.GetValue());

        StaticValue sv = new StaticValue();
        Console.WriteLine(sv.GetValue());

        Console.ReadLine();
    }
}
```

## Konštruktor? Destruktor?
- Trieda existuje po celý čas behu programu.
- Ak má trieda triedne (static) premenné, musíme ich inicializovať zvlášť.
- Konštruktor ani destruktor pre triedu ako objekt neexistuje.

## Kto o kom vie?
- Prostredníctvom konštruktora triedy vytvárame objekty (inštancie), ale trieda o nich nič nevie.
- Z triednej metódy nie je možné pristupovať k členským položkám objektu.
- Objekty (inštancie) triedy majú prístup k členským (static) položkám triedy (pri použití nemusí byť jasné, s akou položkou pracujeme).

## Čo je správne volanie?

## Implementácia v jazyku C++

```cpp
#include <iostream>
using namespace std;

class StaticValue {
public:
    static int value;

    static int GetValue() {
        return value;
    }

    static void IncValue() {
        value++;
    }
};

int StaticValue::value = 0;

int main() {
    cout << StaticValue::GetValue() << endl;
    StaticValue::IncValue();
    cout << StaticValue::GetValue() << endl;

    StaticValue *sv = new StaticValue();
    cout << sv->GetValue() << endl;

    getchar();
    return 0;
}
```

## Implementácia v jazyku C#

```csharp
using System;

class StaticValue
{
    public static int value = 0;

    public static int GetValue()
    {
        return value;
    }

    public static void IncValue()
    {
        value++;
    }
}

class Program
{
    static void Main(string[] args)
    {
        Console.WriteLine(StaticValue.GetValue());
        StaticValue.IncValue();
        Console.WriteLine(StaticValue.GetValue());

        StaticValue sv = new StaticValue();
        Console.WriteLine(sv.GetValue());

        Console.ReadLine();
    }
}
```


## Kedy použiť triedu ako objekt?
- Vytvorenie knižnice funkcií (napr. matematika).
- Potrebujeme, aby objekty (inštancie) zdieľali spoločné dáta.
  - Napr. evidencia počtu objektov (inštancií) triedy.

## Upravte triedu pre počítanie objektov


## Implementácia v jazyku C++

```cpp
#include <iostream>
#include <string>
using namespace std;

class Client {
private:
    int code;
    string name;

public:
    Client(int c, string n) : code(c), name(n) {}

    int GetCode() {
        return code;
    }

    string GetName() {
        return name;
    }
};
```

## Implementácia v jazyku C#

```csharp
using System;

class Client {
    private int code;
    private string name;

    public Client(int c, string n) {
        code = c;
        name = n;
    }

    public int GetCode() {
        return code;
    }

    public string GetName() {
        return name;
    }
}
```


### Deklarácia a definícia


## Implementácia v jazyku C++

```cpp
#include <iostream>
#include <string>
using namespace std;

class Client {
private:
    static int objectsCount;
    int code;
    string name;

public:
    static int GetObjectsCount() {
        return objectsCount;
    }

    Client(int c, string n) : code(c), name(n) {
        objectsCount++;
    }

    ~Client() {
        objectsCount--;
    }

    int GetCode() {
        return code;
    }

    string GetName() {
        return name;
    }
};

int Client::objectsCount = 0;
```

## Implementácia v jazyku C#

```csharp
using System;

class Client {
    private static int objectsCount = 0;
    private int code;
    private string name;

    public static int GetObjectsCount() {
        return objectsCount;
    }

    public Client(int c, string n) {
        code = c;
        name = n;
        objectsCount++;
    }

    ~Client() {
        objectsCount--;
    }

    public int GetCode() {
        return code;
    }

    public string GetName() {
        return name;
    }
}
```

## Úlohy na cvičenie
- Implementujte príklady z prednášky a doplňte do tried `Client` a `Account` počítanie existujúcich objektov.
- Navrhnite a implementujte ďalšie príklady členských položiek tried. Napríklad rovnaká úroková sadzba pre všetky účty, ktorým nebola sadzba zadaná v konštruktore a ktorú je možné prostredníctvom metódy triedy zmeniť.

## Otázky
- Aký je rozdiel medzi funkčnou a objektovou dekompozíciou programu?
- Prečo preferujeme objektovú dekompozíciu a aké sú hlavné problémy funkčnej dekompozície?
- Za akých podmienok môžeme považovať triedu za objekt a ako to implementovať v C++ / C#?
- Vysvetlite rozdiel medzi členskými položkami triedy a inštancie a popíšte ich dostupnosť.
- Ako môžeme v C++ / C# dôsledne odlišovať prácu s členskými položkami tried a inštancií?
- Potrebuje trieda v roli objektu konštruktor resp. destruktor a prečo?

---


# Úvod do dedičnosti 2024/25

## Osnova hodiny
- Čo rieši dedičnosť?
- Príklad.
- Dedičnosť – základný princíp.

## Čo rieši dedičnosť?

### Čo sa rieši?
- Znovu-použiteľnosť
  - Nechceme znova opisovať (kopírovať) kód, ktorý sme už raz napísali a odladili.
- Rozšíriteľnosť
  - Chceme rozšíriť (pozmeniť) kód, ktorý sme už...

## Úloha triedy?
- Znovu-použiteľnosť a rozšíriteľnosť v kontexte používania tried môžeme chápať ako:
  - Kombinovanie s inými triedami, skladanie
  - Rozšírenie o nové správanie
  - Pozmenenie existujúceho správania

## Skladanie vs dedičnosť
- Skladaním dosiahneme, že objekt jednej triedy je zložený z objektov inej triedy.
  - Ide o vzťah „MÁ“.
- Dedičnosťou dosiahneme, že nová trieda je rozšírením alebo špeciálnym prípadom existujúcej triedy (alebo viacerých tried).
  - Ide o vzťah „JE“.

## Príklad


### Account Class in C++ and C#

## Implementácia v jazyku C++

```cpp
class Account
{
private:
    int number;
    double balance;
    double interestRate;

    Client *owner;
    Client *partner;

public:
    Account(int n, Client *o);
    Account(int n, Client *o, double ir);
    Account(int n, Client *o, Client *p);
    Account(int n, Client *o, Client *p, double ir);

    int GetNumber();
    double GetBalance();
    double GetInterestRate();
    Client *GetOwner();
    Client *GetPartner();
    bool CanWithdraw(double a);

    void Deposit(double a);
    bool Withdraw(double a);
    void AddInterest();
};
```

## Implementácia v jazyku C#

```csharp
public class Account
{
    private int number;
    private double balance;
    private double interestRate;

    private Client owner;
    private Client partner;

    // Constructors
    public Account(int n, Client o)
    {
        number = n;
        owner = o;
        balance = 0;
        interestRate = 0;
    }

    public Account(int n, Client o, double ir)
    {
        number = n;
        owner = o;
        interestRate = ir;
        balance = 0;
    }

    public Account(int n, Client o, Client p)
    {
        number = n;
        owner = o;
        partner = p;
        balance = 0;
        interestRate = 0;
    }

    public Account(int n, Client o, Client p, double ir)
    {
        number = n;
        owner = o;
        partner = p;
        interestRate = ir;
        balance = 0;
    }

    // Methods
    public int GetNumber()
    {
        return number;
    }

    public double GetBalance()
    {
        return balance;
    }

    public double GetInterestRate()
    {
        return interestRate;
    }

    public Client GetOwner()
    {
        return owner;
    }

    public Client GetPartner()
    {
        return partner;
    }

    public bool CanWithdraw(double amount)
    {
        return balance >= amount;
    }

    public void Deposit(double amount)
    {
        balance += amount;
    }

    public bool Withdraw(double amount)
    {
        if (CanWithdraw(amount))
        {
            balance -= amount;
            return true;
        }
        return false;
    }

    public void AddInterest()
    {
        balance += balance * interestRate;
    }
}
```
### Čo je na triede `Account` nesprávne?
- Účet s partnerom je rozšírením účtu bez partnera.
- Účet s partnerom **JE** účet.
- Môžeme využiť dedičnosť. Ako?

## Deklarácia predka

## Implementácia v jazyku c++

```cpp
class Account
{
private:
    int number;
    double balance;
    double interestRate;

    Client *owner;

public:
    Account(int n, Client *o);
    Account(int n, Client *o, double ir);

    int GetNumber();
    double GetBalance();
    double GetInterestRate();
    Client *GetOwner();
    bool CanWithdraw(double a);

    void Deposit(double a);
    bool Withdraw(double a);
    void AddInterest();
};
```

## Implementácia v jazyku C#

```csharp
public class Account
{
    private int number;
    private double balance;
    private double interestRate;

    private Client owner;

    // Constructors
    public Account(int n, Client o)
    {
        number = n;
        owner = o;
        balance = 0;
        interestRate = 0;
    }

    public Account(int n, Client o, double ir)
    {
        number = n;
        owner = o;
        interestRate = ir;
        balance = 0;
    }

    // Methods
    public int GetNumber()
    {
        return number;
    }

    public double GetBalance()
    {
        return balance;
    }

    public double GetInterestRate()
    {
        return interestRate;
    }

    public Client GetOwner()
    {
        return owner;
    }

    public bool CanWithdraw(double amount)
    {
        return balance >= amount;
    }

    public void Deposit(double amount)
    {
        balance += amount;
    }

    public bool Withdraw(double amount)
    {
        if (CanWithdraw(amount))
        {
            balance -= amount;
            return true;
        }
        return false;
    }

    public void AddInterest()
    {
        balance += balance * interestRate;
    }
}
```

## Deklarácia potomka

## PartnerAccount Class in C++ and C#

## Implementácia v jazyku C#

```cpp
class PartnerAccount : public Account
{
private:
    Client *partner;

public:
    PartnerAccount(int n, Client *o, Client *p);
    PartnerAccount(int n, Client *o, Client *p, double ir);

    Client *GetPartner();
};
```

## Implementácia v jazyku C#

```csharp
public class PartnerAccount : Account
{
    private Client partner;

    // Constructors
    public PartnerAccount(int n, Client o, Client p)
        : base(n, o)
    {
        partner = p;
    }

    public PartnerAccount(int n, Client o, Client p, double ir)
        : base(n, o, ir)
    {
        partner = p;
    }

    // Method
    public Client GetPartner()
    {
        return partner;
    }
}
```

### Implementácia konštruktorov
- Potomok `PartnerAccount` použije na inicializáciu členských položiek konštruktor rodiča `Account`, ktorému odovzdá potrebné inicializačné hodnoty.


## Account a PartnerAccount Constructors Implementácia v jazyku C# a C++

## C++ konštruktory

```cpp
// Account constructor with just number and owner
Account::Account(int n, Client *o)
{
    this->number = n;
    this->owner = o;
    this->balance = 0;
    this->interestRate = 0;
}

// Account constructor with number, owner, and interest rate
Account::Account(int n, Client *o, double ir)
{
    this->number = n;
    this->owner = o;
    this->balance = 0;
    this->interestRate = ir;
}

// PartnerAccount constructor with number, owner, and partner
PartnerAccount::PartnerAccount(int n, Client *o, Client *p) : Account(n, o)
{
    this->partner = p;
}

// PartnerAccount constructor with number, owner, partner, and interest rate
PartnerAccount::PartnerAccount(int n, Client *o, Client *p, double ir) : Account(n, o, ir)
{
    this->partner = p;
}
```

## C# konštruktory

```csharp
// Account constructor with just number and owner
public Account(int n, Client o)
{
    this.number = n;
    this.owner = o;
    this.balance = 0;
    this.interestRate = 0;
}

// Account constructor with number, owner, and interest rate
public Account(int n, Client o, double ir)
{
    this.number = n;
    this.owner = o;
    this.balance = 0;
    this.interestRate = ir;
}

// PartnerAccount constructor with number, owner, and partner
public PartnerAccount(int n, Client o, Client p) : base(n, o)
{
    this.partner = p;
}

// PartnerAccount constructor with number, owner, partner, and interest rate
public PartnerAccount(int n, Client o, Client p, double ir) : base(n, o, ir)
{
    this.partner = p;
}
```

## Použitie (zastupiteľnosť)

## Main Function v C++ and C#

## C++ Main Function

```cpp
int main()
{
    Account *a;
    PartnerAccount *pa;
    pa = new PartnerAccount(0, new Client(0, "Smith"), new Client(1, "Jones"));
    a = pa;

    cout << a->GetOwner()->GetName() << endl;
    // cout << a->GetPartner()->GetName() << endl;

    cout << pa->GetPartner()->GetName();

    getchar();
    return 0;
}
```

## C# Main Function

```csharp
using System;

class Program
{
    static void Main(string[] args)
    {
        Account a;
        PartnerAccount pa;
        pa = new PartnerAccount(0, new Client(0, "Smith"), new Client(1, "Jones"));
        a = pa;

        Console.WriteLine(a.GetOwner().GetName());
        // Console.WriteLine(a.GetPartner().GetName()); // This won't work because the Account class does not have GetPartner()

        Console.WriteLine(pa.GetPartner().GetName());

        Console.ReadKey();
    }
}
```
```csharp
Smith
Jones 
```

### Banka s účtami dvoch typov

## C++ Bank Class implementácia v jazyku C++

```cpp
class Bank
{
private:
    Client **clients;
    int clientsCount;

    Account **accounts;
    int accountsCount;

public:
    Bank(int c, int a);
    ~Bank();

    Client* GetClient(int c);
    Account* GetAccount(int n);

    Client* CreateClient(int c, std::string n);
    Account* CreateAccount(int n, Client *o);
    Account* CreateAccount(int n, Client *o, double ir);
    PartnerAccount* CreateAccount(int n, Client *o, Client *p);
    PartnerAccount* CreateAccount(int n, Client *o, Client *p, double ir);

    void AddInterest();
};
```

## Bank Class implementácia v jazyku C#

```csharp
public class Bank
{
    private Client[] clients;
    private int clientsCount;

    private Account[] accounts;
    private int accountsCount;

    public Bank(int c, int a)
    {
        clients = new Client[c];
        accounts = new Account[a];
        clientsCount = 0;
        accountsCount = 0;
    }

    public Client GetClient(int c)
    {
        return clients[c];
    }

    public Account GetAccount(int n)
    {
        return accounts[n];
    }

    public Client CreateClient(int c, string n)
    {
        Client newClient = new Client(c, n);
        clients[clientsCount++] = newClient;
        return newClient;
    }

    public Account CreateAccount(int n, Client o)
    {
        Account newAccount = new Account(n, o);
        accounts[accountsCount++] = newAccount;
        return newAccount;
    }

    public Account CreateAccount(int n, Client o, double ir)
    {
        Account newAccount = new Account(n, o, ir);
        accounts[accountsCount++] = newAccount;
        return newAccount;
    }

    public PartnerAccount CreateAccount(int n, Client o, Client p)
    {
        PartnerAccount newAccount = new PartnerAccount(n, o, p);
        accounts[accountsCount++] = newAccount;
        return newAccount;
    }

    public PartnerAccount CreateAccount(int n, Client o, Client p, double ir)
    {
        PartnerAccount newAccount = new PartnerAccount(n, o, p, ir);
        accounts[accountsCount++] = newAccount;
        return newAccount;
    }

    public void AddInterest()
    {
        foreach (var account in accounts)
        {
            if (account != null)
            {
                account.AddInterest();
            }
        }
    }
}
```
- Malo by to fungovať? A prečo?

## Dedičnosť – základný princíp

## Terminológia
- Predok – potomek, priamy predok – potomek
- Rodič – dcéra (syn)
- Nadriadená (super, báza) trieda – podradená (sub) trieda

## Vzťahy v dedičnosti
```
A
|__ B
    |__ C
```
- `A` je báza triedy `B`, A je rodič `B`, A je predok `C`
- `B` je báza triedy `C`, trieda B dedí z triedy A, B je rodič C
- `C` dedí z B aj A, C je dcérska trieda triedy B, C je potomek A a priamy potomek B.

## Príklady
- Vozidlo – bicykel, motorka, osobné auto
- Osoba – užívateľ, správca
- Kolekcia – zoznam, množina

### Nesprávne?
- Auto – Škoda
  - Škoda je **ZNAČKA** osobného auta.
- Strom – smrek
  - Smrek je **DRUH** ihličnatého stromu.

## Generalizácia - špecializácia
- Nezamieňať vzťah „je inštanciou“ a „dediť z“.
  - „je inštanciou“ je vzťah medzi triedou a objektom
  - „dediť z“ je vzťah medzi triedami.
- Vzťah dedičnosti definuje vzťah **VŠEOBECNÝ** – **ŠPECIALIZOVANÝ**
  - Potomek by teda mal reprezentovať špeciálny prípad predka...
  - ... a predok by mal reprezentovať zobecnenie svojich potomkov.

## Inak povedané...
- Predok definuje spoločné správanie všetkých svojich potomkov.
- Potomkovia môžu toto správanie rozšíriť alebo pozmeniť.
- Potomkovia sa nemôžu tohto správania zbaviť.
- A teda:
  - Dedí sa všetko bez výnimky!!!
  - Dedí sa aj miera skrytia informácií...

## Vzťah skladania a dedičnosti
- Skladanie – „MÁ“ vs dedičnosť „JE“.
- Dedičnosť môžeme chápať ako dôsledok skladania.
  - Inštancia triedy potomka obsahuje všetko, čo má inštancia triedy predka.

## Hierarchia
- Pri použití dedičnosti vznikajú hierarchie tried.
- V našom prípade pracujeme s jednoduchou dedičnosťou.
  - Každý potomek má práve jedného priameho predka.
  - Predok môže mať viac priamych potomkov.
- V prípade jednoduchej dedičnosti je touto hierarchiou strom.
- Nezamieňať hierarchiu objektov (kompozícia) a hierarchiu tried (dedičnosť).

## Liskov princíp substitúcie
- Barbara Liskov 1987. Data abstraction and hierarchy.
- Bertrand Meyer. Invarianty správania.
- Potomek môže vždy nahradiť predka...
  - ... a to preto, že majú spoločné správanie.
  - Naopak to neplatí...

## Vznik potomka
1. Volanie konštruktora objektu.
2. Volanie konštruktora priameho predka.
3. Vykonanie konštruktora priameho predka.
4. Vykonanie konštruktora objektu.

## Úlohy na cvičenie
- Implementujte príklad z prednášky a vytvorte banku s mnohými klientmi a účtami. Zamerajte sa na pochopenie princípu zastupiteľnosti a na to, ako fungujú konštruktory v dedičnosti.
- Navrhnite a implementujte ďalšie jednoduché príklady dedičnosti s rozšírením spoločného stavu a správania, ako napríklad Auto, Osobné auto, Nákladné auto.

## Kontrolné otázky
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

# Dedičnosť – zmena správania 2024/25

## Osnova hodiny
- Rozšírenie správania.
- Zmena správania.
- Príklad.

## Rozšírenie správania

### Keď rozširujeme správanie...
- Môžeme bezpečne použiť to, čo už máme.
- Nehrozí žiadny problém s pochopením, ako sa objekt správa.
- Objekt vystupuje sám za seba...
  - ...alebo za niektorého zo svojich predkov.

## Paradox špecializácie a rozšírenia
- Vzťah dedičnosti je vzťahom **všeobecný - špeciálny**.
- Potomok je teda špeciálnym prípadom predka.
- Paradoxne však, pri rozšírení dochádza k tomu, že potomok vie viac, ako ktorýkoľvek z jeho predkov.

## ...a teda
- Čím bohatšie správanie uvažujeme, tým menej tried ho poskytuje.
- V dedičnej hierarchii je najmenšie spoločné správanie definované v spoločnom predkovi.
- Koncové triedy tejto hierarchie majú najbohatšie správanie (každá trochu iné).

## Nesprávny príklad
- Potreba rozšírenia sama o sebe nie je dostatočná pre použitie dedičnosti.
- Napr. vzťah bodu a kružnice, mohli by sme potrebovať rozšíriť bod o prácu s polomerom (nové správanie).
- Je to dostatočné, aby sme sa rozhodli použiť dedičnosť?

### Nie!!!
- Nie je splnená podmienka špecializácie (kružnica nie je špeciálnym prípadom bodu).

## Zmena správania

### Zmena správania
- Ak je správanie deklarované v predkovi, môžeme ho v potomkovi deklarovať znova.
- Existuje potom viac metód rovnakého mena.
- Deklarované správanie potom musíme v potomkovi implementovať (aby bolo vykonateľné).
- Deklarované správanie nemusí byť implementované v predkovi.

## Pretíženie ako rozšírenie správania

### Pretíženie
- Pretížením rozumieme situáciu, keď daná metóda má rovnaké meno, ale má:
  - iné parametre,
  - iné typy parametrov,
  - iný typ návratovej hodnoty.
- Pretíženie však nie je zmena správania, aj keď má metóda rovnaké meno.

### Typy pretíženia
- Názov metódy zostáva rovnaký.
- Iný počet parametrov.
- Iné dátové typy parametrov.
- Iná návratová hodnota (nie v C++).
- Možno kombinovať.

## Prekrytie
- Prekrytím rozumieme situáciu, keď metóda potomka má rovnakú deklaráciu ako metóda predka (rovnakú signatúru).
- Potomok dedí aj metódu predka. Má teda dve metódy s rovnakou deklaráciou.

### Kedy použiť prekrytie?
- Typickým príkladom použitia pretíženia sú konštruktory.
- Typickým príkladom použitia prekrytia je skutočná zmena správania potomka.
  - Príkladom môže byť metóda na výber peňazí z rôznych typov účtov v banke.

## Príklad

### Deklarácia predka


## Account Class s Withdraw a Deposit Methods v C++ a C#

## C++ Account Class

```cpp
class Account
{
private:
    int number;
    double balance;
    double interestRate;

    Client *owner;

public:
    Account(int n, Client *o);
    Account(int n, Client *o, double ir);

    int GetNumber();
    double GetBalance();
    double GetInterestRate();
    Client *GetOwner();
    bool CanWithdraw(double a);

    void Deposit(double a);
    bool Withdraw(double a);
    void AddInterest();
};
```

## C# Account Class

```csharp
public class Account
{
    private int number;
    private double balance;
    private double interestRate;

    private Client owner;

    // Constructors
    public Account(int n, Client o)
    {
        number = n;
        owner = o;
        balance = 0;
        interestRate = 0;
    }

    public Account(int n, Client o, double ir)
    {
        number = n;
        owner = o;
        interestRate = ir;
        balance = 0;
    }

    // Methods
    public int GetNumber()
    {
        return number;
    }

    public double GetBalance()
    {
        return balance;
    }

    public double GetInterestRate()
    {
        return interestRate;
    }

    public Client GetOwner()
    {
        return owner;
    }

    public bool CanWithdraw(double amount)
    {
        return balance >= amount;
    }

    public void Deposit(double amount)
    {
        balance += amount;
    }

    public bool Withdraw(double amount)
    {
        if (CanWithdraw(amount))
        {
            balance -= amount;
            return true;
        }
        return false;
    }

    public void AddInterest()
    {
        balance += balance * interestRate;
    }
}
```


## Prekrytie
- Deklarujeme triedu `CreditAccount`.
- Prekryjeme metódu `CanWithdraw`.
  - Má rovnakú signatúru, ale inú definíciu.
  - Dôsledok: V triede `CreditAccount` bude inštančná metóda `CanWithdraw` dvakrát!!!

### Deklarácia potomka

## CreditAccount Class in C++ and C#

## C++ CreditAccount Class

```cpp
class CreditAccount : public Account
{
private:
    double credit;

public:
    CreditAccount(int n, Client *o, double c);
    CreditAccount(int n, Client *o, double ir, double c);

    bool CanWithdraw(double a);
};
```

## C# CreditAccount Class

```csharp
public class CreditAccount : Account
{
    private double credit;

    // Constructors
    public CreditAccount(int n, Client o, double c) : base(n, o)
    {
        this.credit = c;
    }

    public CreditAccount(int n, Client o, double ir, double c) : base(n, o, ir)
    {
        this.credit = c;
    }

    // Method
    public override bool CanWithdraw(double amount)
    {
        return balance + credit >= amount;
    }
}
```


### Definícia

## CanWithdraw Method v Account a CreditAccount Classes v C++ a C#

## C++ CanWithdraw Method

```cpp
// In Account class
bool Account::CanWithdraw(double a)
{
    return (this->balance >= a);
}

// In CreditAccount class
bool CreditAccount::CanWithdraw(double a)
{
    return (this->GetBalance() + this->credit >= a);
}
```

## C# CanWithdraw Method

```csharp
// In Account class
public virtual bool CanWithdraw(double amount)
{
    return balance >= amount;
}

// In CreditAccount class
public override bool CanWithdraw(double amount)
{
    return balance + credit >= amount;
}
```

### Definícia (pripomenutie)

## Withdraw Method v Account Class v C++ a C#

## C++ Withdraw Method

```cpp
bool Account::Withdraw(double a)
{
    bool success = false;
    if (this->CanWithdraw(a))
    {
        this->balance -= a;
        success = true;
    }
    return success;
}
```

## C# Withdraw Method

```csharp
public bool Withdraw(double amount)
{
    bool success = false;
    if (CanWithdraw(amount))
    {
        balance -= amount;
        success = true;
    }
    return success;
}
```

### Použitie


## Main Function s CreditAccount v C++ a C#

## C++ Main Function

```cpp
int main()
{
    Client *o = new Client(0, "Smith");

    CreditAccount *ca = new CreditAccount(1, o, 1000);
    cout << ca->CanWithdraw(1000) << endl;

    Account *a = ca;
    cout << a->CanWithdraw(1000) << endl;

    cout << ca->Withdraw(1000) << endl;

    a = nullptr;
    delete ca;

    getchar();
    return 0;
}
```

## C# Main Function

```csharp
using System;

class Program
{
    static void Main(string[] args)
    {
        Client o = new Client(0, "Smith");

        CreditAccount ca = new CreditAccount(1, o, 1000);
        Console.WriteLine(ca.CanWithdraw(1000));

        Account a = ca;
        Console.WriteLine(a.CanWithdraw(1000));

        Console.WriteLine(ca.Withdraw(1000));

        a = null;
        ca = null;

        Console.ReadKey();
    }
}
```

## Výsledok?

```csharp
1
0
0
```

## Sme hotoví?
- Nie!!!
- Ako vyberieme z účtu (ak môžeme), keď nemáme prístup k členskej premennej `balance`?
- Aké máme možnosti?

### Vlastná metóda?


## CreditAccount Class s Withdraw Method v C++ a C#

## C++ CreditAccount Class

```cpp
class CreditAccount : public Account
{
private:
    double credit;

public:
    CreditAccount(int n, Client *o, double c);
    CreditAccount(int n, Client *o, double ir, double c);

    bool CanWithdraw(double a);
    bool Withdraw(double a);
};
```

## C# CreditAccount Class

```csharp
public class CreditAccount : Account
{
    private double credit;

    // Constructors
    public CreditAccount(int n, Client o, double c) : base(n, o)
    {
        this.credit = c;
    }

    public CreditAccount(int n, Client o, double ir, double c) : base(n, o, ir)
    {
        this.credit = c;
    }

    // Method
    public override bool CanWithdraw(double amount)
    {
        return balance + credit >= amount;
    }

    public override bool Withdraw(double amount)
    {
        if (CanWithdraw(amount))
        {
            balance -= amount;
            return true;
        }
        return false;
    }
}
```

## Máme problém...

### Aké teda máme možnosti?
- Public prístup k dátovej položke?
- Porušenie zapuzdrenia?
- Alebo inak?

## Nový predok

## Porovnanie Account Class v C++ a C#

## C++ Account Class (Private Balance)

```cpp
class Account
{
private:
    int number;
    double balance;
    double interestRate;

    Client *owner;

public:
    Account(int n, Client *o);
    Account(int n, Client *o, double ir);

    int GetNumber();
    double GetBalance();
    double GetInterestRate();
    Client *GetOwner();
    bool CanWithdraw(double a);

    void Deposit(double a);
    bool Withdraw(double a);
    void AddInterest();
};
```

### C++ Account Class (Protected Balance)

```cpp
class Account
{
private:
    int number;
    double interestRate;

protected:
    double balance;

public:
    Account(int n, Client *o);
    Account(int n, Client *o, double ir);

    int GetNumber();
    double GetBalance();
    double GetInterestRate();
    Client *GetOwner();
    bool CanWithdraw(double a);

    void Deposit(double a);
    bool Withdraw(double a);
    void AddInterest();
};
```

C# Porovnanie 

Zmena viditeľnosti premennej balance z private na protected umožňuje triedam, ktoré dedia z triedy Account, priamy prístup k premenným balance. To môže byť užitočné pre podtriedy ako CreditAccount, kde je úprava zostatku častejšia.

### Funguje, ale...


### Withdraw Method in CreditAccount Class in C++ and C#

### C++ Withdraw Method v CreditAccount

```cpp
bool CreditAccount::Withdraw(double a)
{
    bool success = false;
    if (this->CanWithdraw(a))
    {
        this->balance -= a;
        success = true;
    }
    return success;
}
```

### C# Withdraw Method v CreditAccount

```csharp
public override bool Withdraw(double amount)
{
    bool success = false;
    if (CanWithdraw(amount))
    {
        balance -= amount;
        success = true;
    }
    return success;
}
```

- Máme rovnaký kód dvakrát.
- Porušujeme zapuzdrenie.
- Pri zastúpení predka potomkom sa použijú rôzne metódy.

## Výsledok

```csharp
1
0
1
```

### Porušenie zapuzdrenia
- Pri zmene správania môže vzniknúť potreba pracovať so súkromnou časťou predka.
- Ide samozrejme o porušenie zapuzdrenia a toho si musíme byť vedomí...
  - ...ale každé rozumné pravidlo má nejaké výnimky.

### Dá sa zavolať metóda predka?
- Je to rovnaké ako volanie statickej metódy.
  - Z potomka voláme originálnu metódu.
  - `Account::CanWithdraw(a);`

## Úlohy na cvičenie
- Implementujte príklady z prednášky. Zamerajte sa na prekrytie, vyskúšajte použitie „protected“.
- Navrhnite a implementujte jednoduchú dedičnú hierarchiu geometrických objektov, ktoré budú mať spoločné metódy „Obsah“ a „Obvod“. Využite prekrytie a rozoberte správanie pri použití substitučného princípu.

## Kontrolné otázky
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

