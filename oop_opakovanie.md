
# Objektovo orientované programovanie

## Modularita 2024/25

### Modul?

### KeyValue Class implementácia v C++

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


### KeyValue Class implementácia v C++

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

### KeyValue Class implementáciav C++

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

### Main Function príklad implementácia v C++

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

### Main Function príklad s KeyValue Class implementácia v C++

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

### Main Function s Nullptr implementácia v C++

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

### Implementácia v jazyku C#

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

### KeyValue Class Example implementácia v jazyku C++
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

### KeyValues Class implementácia v jazyku C++
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


### KeyValues Class implementácia v jazyku C#

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

#### Použitie
- Použitie kľúčového slova `new` zabezpečí vznik objektu (alokuje pamäť pre dáta („plochú“ časť) objektu).

### Main Function implementácia v C++

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

### Main Function implementácia v C#

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

#### Výsledok
- Definícia (implementácia).

```csharp
0.5
4.5
```

#### Definícia ( implementácia ) 


# KeyValues Class Method definicia v jazyku C++

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


### KeyValues Class Method definícia v jazyku C#

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
- Vysvetlite princípy deklarácie a definície jednoduchej triedy v C++ / C#.
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

### Class Template v jazyku C++

```cpp
class <meno> {
    private:
        <súkromné členské položky>
    public:
        <verejné členské položky>
};
```
### Class Template v jazyku C#

```csharp
class <Name> {
    // Private member variables
    private <private members>;

    // Public member methods and properties
    public <public members>;
}
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

### Client Class príklad implementácie v C++

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

### Client Class príklad implementácie v C#

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


### Account and Bank Classes v jazyku C++

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


### Account and Bank Classes v jazyku C#

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

### StaticValue Class príklad v C++

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

### StaticValue Class príklad v C#

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

#### Použitie

### StaticValue použitie príklad v C++

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
### StaticValue použitie príklad v C#

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

### StaticValue Class definícia v C++

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


### StaticValue Class definícia v C#

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

#### Trieda bez objektov

### Implementácia v jazyku C++ 

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

### Implementácia v jazyku C# 

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

### Konštruktor? Destruktor?
- Trieda existuje po celý čas behu programu.
- Ak má trieda triedne (static) premenné, musíme ich inicializovať zvlášť.
- Konštruktor ani destruktor pre triedu ako objekt neexistuje.

### Kto o kom vie?
- Prostredníctvom konštruktora triedy vytvárame objekty (inštancie), ale trieda o nich nič nevie.
- Z triednej metódy nie je možné pristupovať k členským položkám objektu.
- Objekty (inštancie) triedy majú prístup k členským (static) položkám triedy (pri použití nemusí byť jasné, s akou položkou pracujeme).

### Čo je správne volanie?

### Implementácia v jazyku C++

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

### Implementácia v jazyku C# 

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


### Kedy použiť triedu ako objekt?
- Vytvorenie knižnice funkcií (napr. matematika).
- Potrebujeme, aby objekty (inštancie) zdieľali spoločné dáta.
  - Napr. evidencia počtu objektov (inštancií) triedy.

### Upravte triedu pre počítanie objektov


### Implementácia v jazyku C++

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

### Implementácia v jazyku C# 

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


#### Deklarácia a definícia


### Implementácia v jazyku C++

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

### Implementácia v jazyku C# 

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

### Úlohy na cvičenie
- Implementujte príklady z prednášky a doplňte do tried `Client` a `Account` počítanie existujúcich objektov.
- Navrhnite a implementujte ďalšie príklady členských položiek tried. Napríklad rovnaká úroková sadzba pre všetky účty, ktorým nebola sadzba zadaná v konštruktore a ktorú je možné prostredníctvom metódy triedy zmeniť.

### Otázky
- Aký je rozdiel medzi funkčnou a objektovou dekompozíciou programu?
- Prečo preferujeme objektovú dekompozíciu a aké sú hlavné problémy funkčnej dekompozície?
- Za akých podmienok môžeme považovať triedu za objekt a ako to implementovať v C++ / C#?
- Vysvetlite rozdiel medzi členskými položkami triedy a inštancie a popíšte ich dostupnosť.
- Ako môžeme v C++ / C# dôsledne odlišovať prácu s členskými položkami tried a inštancií?
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


# Account Class in C++ and C#

### Implementácia v jazyku C++

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

### Implementácia v jazyku C# 

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
#### Čo je na triede `Account` nesprávne?
- Účet s partnerom je rozšírením účtu bez partnera.
- Účet s partnerom **JE** účet.
- Môžeme využiť dedičnosť. Ako?

### Deklarácia predka

### Implementácia v jazyku c++

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

### Implementácia v jazyku C# 

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

### Deklarácia potomka

### PartnerAccount Class in C++ and C#

### Implementácia v jazyku C# 

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

### Implementácia v jazyku C# 

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

#### Implementácia konštruktorov
- Potomok `PartnerAccount` použije na inicializáciu členských položiek konštruktor rodiča `Account`, ktorému odovzdá potrebné inicializačné hodnoty.


### Account a PartnerAccount Constructors Implementácia v jazyku C# a C++

### C++ konštruktory

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

### C# konštruktory

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

### Použitie (zastupiteľnosť)

### Main Function v C++ and C#

### C++ Main Function

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

### C# Main Function

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

#### Banka s účtami dvoch typov

### C++ Bank Class implementácia v jazyku C++

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

### Bank Class implementácia v jazyku C#

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


### Account Class s Withdraw a Deposit Methods v C++ a C#

### C++ Account Class

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

### C# Account Class

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


### Prekrytie
- Deklarujeme triedu `CreditAccount`.
- Prekryjeme metódu `CanWithdraw`.
  - Má rovnakú signatúru, ale inú definíciu.
  - Dôsledok: V triede `CreditAccount` bude inštančná metóda `CanWithdraw` dvakrát!!!

#### Deklarácia potomka

### CreditAccount Class in C++ and C#

### C++ CreditAccount Class

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

### C# CreditAccount Class

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


#### Definícia

### CanWithdraw Method v Account a CreditAccount Classes v C++ a C#

### C++ CanWithdraw Method

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

### C# CanWithdraw Method

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

#### Definícia (pripomenutie)

### Withdraw Method v Account Class v C++ a C#

### C++ Withdraw Method

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

### C# Withdraw Method

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

#### Použitie


### Main Function s CreditAccount v C++ a C#

### C++ Main Function

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

### C# Main Function

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

### Výsledok?

```csharp
1
0
0
```

### Sme hotoví?
- Nie!!!
- Ako vyberieme z účtu (ak môžeme), keď nemáme prístup k členskej premennej `balance`?
- Aké máme možnosti?

#### Vlastná metóda?


### CreditAccount Class s Withdraw Method v C++ a C#

### C++ CreditAccount Class

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

### C# CreditAccount Class

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

### Máme problém...

#### Aké teda máme možnosti?
- Public prístup k dátovej položke?
- Porušenie zapuzdrenia?
- Alebo inak?

### Nový predok

### Porovnanie Account Class v C++ a C#

### C++ Account Class (Private Balance)

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

## C++ Account Class (Protected Balance)

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

#### Funguje, ale...


# Withdraw Method in CreditAccount Class in C++ and C#

## C++ Withdraw Method v CreditAccount

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

## C# Withdraw Method v CreditAccount

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

### Výsledok

```csharp
1
0
1
```

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

