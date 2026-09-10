# Úvod do softvérového inžinierstva — modelovanie správania

Skôr než sa začne programovať, treba vedieť **čo** sa má postaviť a **prečo**.
Diagramy a wireframy (nižšie) sú len nástroje, ktorými sa výsledok zachytí — táto
prvá časť je o metóde, ktorá im predchádza.

## SW analytik

Analytik nie je „kreslič diagramov". Jeho úloha je **položiť správne otázky skôr,
než sa začne programovať**, a nedať sa odbiť tým, čo si zákazník *myslí*, že chce.
Rozpráva sa s ľuďmi z firmy, zisťuje, ako proces reálne funguje — kde sa
rozhoduje, čo môže zlyhať — a až z toho vzniknú požiadavky, use casy a návrh
systému. Diagram je potom spoločný jazyk medzi biznisom a vývojom.

Takto sa na váš softvér bude pýtať aj potenciálny zákazník — a tieto otázky si
viete položiť sami, kým ešte len rozmýšľate, čo postaviť.

### Požiadavka

**Požiadavka** = jedna konkrétna vec, ktorú má systém robiť alebo spĺňať. Musí byť
**overiteľná** — ak sa nedá jednoznačne povedať „splnené / nesplnené", je to len
želanie, nie požiadavka.

| | Funkčná požiadavka | Nefunkčná požiadavka (NFR) |
|---|---|---|
| Odpovedá na | *čo* systém robí | *ako dobre* to robí |
| Príklad | „Systém zobrazí stav žiadosti" | „Žiadosť vidí len jej autor", „Odozva do 2 s" |

**FURPS** — model na roztriedenie požiadaviek: **F**unctionality (funkčnosť),
**U**sability (použiteľnosť), **R**eliability (spoľahlivosť), **P**erformance
(výkon), **S**upportability (udržiavateľnosť). Prvé `F` sú funkčné požiadavky,
zvyšok sú NFR.

**MoSCoW** — priorita pre *rozsah*, nie „dôležitosť":

| Trieda | Význam |
|---|---|
| **M**ust have | bez toho nemá zmysel dodať |
| **S**hould have | dôležité, ale dá sa dočasne obísť |
| **C**ould have | pridá sa, ak zvýši čas |
| **W**on't have (teraz) | vedome odložené na neskôr |

Požiadavky sa vedú v tabuľke, aby bolo vidno ich stav a väzbu na riešenie:

| Kód | Popis | Priorita | Stav | Rieši sa cez |
|---|---|---|---|---|
| R1 | Zamestnanec chce poznať stav svojej žiadosti | Must | Analyzované | centrálny stav + notifikácie |
| R2 | Vedúci chce históriu žiadostí oddelenia | Must | Analyzované | audit log (história zmien stavu) |

### AS-IS a TO-BE

Analytik zachytí **dva stavy procesu**:

- **AS-IS** — ako to funguje *dnes*, aj s chybami
- **TO-BE** — ako to má fungovať *po* zavedení systému

Medzi nimi je najdôležitejšia otázka: **prečo dnešný stav nefunguje?** Nestačí
prvá odpoveď — pýtaj sa „prečo" dovtedy, kým sa nenarazí na **koreňovú príčinu**:

> Zamestnanec nevie stav žiadosti.
> — *Prečo?* Lebo stav žije len v e-mailoch.
> — *Prečo?* Lebo neexistuje spoločný systém záznamu.
> — *Prečo?* Lebo proces vznikol ad-hoc, bez vlastníka, ktorý by ho navrhol.

Často zistíš, že viacero rôznych sťažností sú v skutočnosti **symptómy jednej
príčiny** — a vyrieši ich jeden zásah, nie štyri.

### Od požiadavky po test

Všetky artefakty — proces, dáta, obrazovka, test — sú **prepojené**. Každý
vychádza z požiadavky a dá sa po tej niti prejsť tam aj späť. Toto je odpoveď na
otázku „načo toľko diagramov":

![Traceability — od požiadavky R1 po test](https://cdn.jsdelivr.net/gh/SPSITKNM/oop_opakovanie@main/assets/traceability-poziadavka-test.svg)

Posledný článok, **test**, sa píše v tvare **Given – When – Then**, aby bola
požiadavka jednoznačne overiteľná:

> **Given** zamietnutá žiadosť
> **When** zamestnanec otvorí prehľad „Moje žiadosti"
> **Then** vidí stav *Zamietnutá* aj dôvod, bez čakania na e-mail

Ak sa niektorý článok reťaze nedá vyplniť (požiadavka bez testu, obrazovka bez
požiadavky), je to signál, že v analýze niečo chýba — alebo je tam niečo navyše.

## Diagram aktivít

Behaviorálny UML diagram. Zobrazuje **tok riadenia** medzi činnosťami — ich
poradie, vetvenie podľa podmienok a paralelné vetvy. Vyzerá ako vývojový diagram
(flowchart), ale má presnú UML sémantiku.

**Kedy ho použiť:**

- rozpísať scenár use casu krok po kroku (nadväzuje na *Use Case → Scenáre*)
- zachytiť biznis proces alebo pracovný postup
- opísať algoritmus na vyššej úrovni, bez kódu

## Notácia

| Prvok | Značka | Význam |
|---|---|---|
| počiatočný uzol | vyplnený kruh `●` | začiatok toku |
| akcia / aktivita | zaoblený obdĺžnik | jeden krok (činnosť) |
| tok riadenia | šípka | poradie krokov |
| rozhodovací uzol | kosoštvorec, 1 vstup → viac vetiev | vetvenie; každá vetva má stráženú podmienku `[…]` |
| zlučovací uzol | kosoštvorec, viac vstupov → 1 výstup | vetvy sa opäť spájajú |
| fork / join | hrubá čiara | rozdelenie do paralelných vetiev a ich synchronizácia |
| koncový uzol | kruh v kruhu `◉` | koniec toku |
| plavecké dráhy (swimlanes) | zvislé alebo vodorovné pruhy | kto akciu vykonáva (aktér, systém, modul) |

**Stráženie (guard)** `[podmienka]` — text v hranatých zátvorkách pri vetve
rozhodovacieho uzla. Vetvy musia pokryť všetky možnosti a nesmú sa prekrývať.

## Príklad — prihlásenie používateľa

![Diagram aktivít — prihlásenie používateľa](https://cdn.jsdelivr.net/gh/SPSITKNM/oop_opakovanie@main/assets/activity-prihlasenie.svg)

Čítanie:

1. Používateľ **zadá meno a heslo**.
2. Rozhodovací uzol **Údaje platné?**
   - `[nie]` → **Zobraz chybu**, tok sa vráti na zadanie údajov (slučka).
   - `[áno]` → **Vytvor reláciu (session)**.
3. **Fork** — súčasne prebehne *Načítaj profil* a *Zapíš do logu (audit)*.
4. **Join** — počká sa na dokončenie oboch paralelných vetiev.
5. **Zobraz nástenku** → koncový uzol.

Rozšírenie „zobraz chybu pri zlom hesle" je presne to, čo by v use case diagrame
bol vzťah `«extend»` — tu je rozpísané do konkrétneho toku.

## BPMN — procesný pohľad

**BPMN** = *Business Process Model and Notation* (štandard OMG). Nie je súčasťou
UML. Opisuje **biznis proces** — kto, čo a v akom poradí robí, aby vznikol
výsledok. Často zachytáva spoluprácu viacerých oddelení alebo firiem. Jeho
najväčšia sila: rozumie mu aj netechnický človek, takže je to spoločný jazyk
medzi analytikom a zadávateľom.

![BPMN — proces žiadosti o dovolenku](https://cdn.jsdelivr.net/gh/SPSITKNM/oop_opakovanie@main/assets/bpmn-ziadost-o-dovolenku.svg)

Čítanie: zamestnanec **vyplní žiadosť** → HR ju **posúdi** → brána **Schválené?**
rozhodne. `[áno]` sa termín **automaticky zapíše do kalendára** a proces končí
úspechom; `[nie]` sa zamestnancovi **pošle oznámenie o zamietnutí** a proces
končí neúspechom. Dva pruhy (*lanes*) ukazujú, že vypĺňanie robí zamestnanec a
posudzovanie HR — presne ten druh informácie, ktorý analytik potrebuje.

## Udalosti (events)

Kruh. Hrúbka obrysu hovorí, kde v procese udalosť je:

| Udalosť | Značka | Význam |
|---|---|---|
| štartová | tenký kruh | čo proces **spúšťa** (prišla žiadosť, nastal termín) |
| medzičasová | dvojitý kruh | niečo **počas** behu (uplynul čas, prišla správa) |
| koncová | hrubý kruh | proces **skončil** (úspešne alebo neúspešne) |

## Úlohy (tasks) a ich typy

Tu BPMN prekonáva obyčajný vývojový diagram — rozlišuje **kto alebo čo** prácu
vykoná. Malá ikona v ľavom hornom rohu úlohy určuje typ:

| Typ úlohy | Kto/čo ju robí | Príklad |
|---|---|---|
| **User task** | človek, ale **cez systém** (formulár v aplikácii) | „Vyplniť žiadosť", „Posúdiť žiadosť" |
| **Manual task** | človek **bez systému** (fyzická činnosť) | „Odniesť zložku do archívu" |
| **Service task** | **automaticky systém** alebo externá služba (API) | „Zapísať do kalendára", „Odoslať e-mail" |
| **Script task** | procesný engine spustí **skript / kód** priamo v procese | „Vypočítať zostatok dovolenky" |
| **Send / Receive task** | odošle správu / čaká na správu | „Poslať notifikáciu" / „Počkať na potvrdenie z banky" |
| **Business rule task** | vyhodnotí **rozhodovaciu tabuľku** (DMN) | „Určiť zľavu podľa vernostného stupňa" |

Pre analytika je tento výber dôležitý:

- **User task** → treba navrhnúť obrazovku a počítať s človekom
- **Service task** → treba integráciu, niečo naprogramovať ako automat
- **Manual task** → systém sa toho vôbec netýka (len to zdokumentujeme)

## Brány (gateways)

Kosoštvorec. Symbol vnútri určuje správanie:

| Brána | Symbol | Správanie |
|---|---|---|
| **exkluzívna (XOR)** | `×` | pokračuje **práve jedna** vetva (if / else) |
| **paralelná (AND)** | `+` | pokračujú **všetky** vetvy naraz |
| **inkluzívna (OR)** | `○` | pokračuje **jedna alebo viac** vetiev podľa podmienok |
| **udalosťová** | pentagón | čaká sa, ktorá **udalosť** nastane skôr |

Rozvetvenie aj opätovné zlúčenie sa kreslí rovnakou bránou.

## Toky a účastníci

| Prvok | Značka | Význam |
|---|---|---|
| sekvenčný tok | plná šípka | poradie krokov **v jednom** procese |
| tok správ (message flow) | prerušovaná šípka s krúžkom | komunikácia **medzi** dvoma účastníkmi (poolmi) |
| bazén (pool) | veľký rámec | jeden **účastník** procesu (firma, systém, zákazník) |
| dráha (lane) | pruh v bazéne | **rola** alebo oddelenie vnútri účastníka |

## Diagram aktivít vs BPMN

| | Diagram aktivít (UML) | BPMN |
|---|---|---|
| Účel | správanie softvéru, scenár use casu, algoritmus | biznis proces, workflow v organizácii |
| Publikum | vývojári, analytici | analytici, biznis, procesní vlastníci |
| Zaradenie | jeden zo 14 UML diagramov | samostatný štandard (OMG) |
| Vykonateľnosť | nie | áno — BPMN engine dokáže proces spustiť |
| Rozdelenie zodpovednosti | swimlanes | pools + lanes, navyše message flow medzi nimi |

Pre školský projekt spravidla stačí **diagram aktivít** na rozpis scenárov.
BPMN spomíname preto, že v praxi (najmä v procesnom a bankovom prostredí) je
veľmi rozšírený.

## Wireframe a mockup

Keď je jasné *čo* systém robí (use casy) a *ako* proces beží (BPMN / diagram
aktivít), analytik načrtne aj *ako to bude vyzerať na obrazovke*. Nie preto, aby
navrhol finálny dizajn — ale aby **overil tok a obsah obrazovky** skôr, než sa
začne programovať.

| Úroveň | Čo to je | Kedy |
|---|---|---|
| **wireframe** | nízkofidelitný náčrt — rozloženie prvkov, žiadne farby ani písma | najskôr, na overenie štruktúry a toku |
| **mockup** | vernejší návrh — už s farbami, typografiou, reálnym obsahom | keď je štruktúra odsúhlasená |
| **prototyp** | klikateľný model, dá sa ním „preklikať" scenár | pred vývojom, na používateľské testovanie |

Wireframe kreslíme len pre **kľúčové obrazovky** (2–3), nie pre celú aplikáciu, a
každú viažeme na konkrétny use case.

![Wireframe — nová žiadosť o dovolenku a zoznam žiadostí](https://cdn.jsdelivr.net/gh/SPSITKNM/oop_opakovanie@main/assets/wireframe-ziadost-o-dovolenku.svg)

Ľavá obrazovka pokrýva use case „podať žiadosť", pravá „sledovať stav". Farby
odznakov stavu zámerne kopírujú stavy z procesu (zelená = schválené, žltá =
čaká, červená = zamietnuté) — rovnaký vizuálny jazyk naprieč diagramom aj
obrazovkou uľahčuje orientáciu.

> **Pre študentov:** toto je bod, kde si navrhnete **vlastnú aplikáciu** — čo
> chcete postaviť. Ako budete na programovaní preberať ďalšie koncepty, tento
> návrh budete postupne implementovať. Oplatí sa navrhnúť niečo, čo naozaj
> chcete mať hotové.

## Súvisiace

- **Use Case diagram** a scenáre — [šablóna Systémovej analýzy](/citacka.html?s=pro&doc=systemova-analyza)
- **Triedny diagram**, vzťahy medzi triedami (asociácia / agregácia / kompozícia) — [Opakovanie OOP](/citacka.html?s=oop&doc=oop-opakovanie#vztahy-medzi-objektmi-asociacia-agregacia-kompozicia)
