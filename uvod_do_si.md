# Úvod do softvérového inžinierstva — modelovanie správania

Triedny diagram alebo ER diagram opisujú **štruktúru** (čo systém obsahuje).
Diagram aktivít a BPMN opisujú **správanie** — *ako* niečo prebieha krok za krokom.
Sú to najbežnejšie nástroje na zachytenie procesu alebo scenára tak, aby mu
rozumel aj neprogramátor.

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

ASCII náčrt (keby si potreboval kresliť rýchlo na tabuľu):

```
        (●)
         │
         ▼
 ┌────────────────────┐  ◄────────────┐
 │ Zadaj meno a heslo │               │
 └────────────────────┘               │
         │                            │
         ▼                            │
     ╱Údaje platné?╲──[nie]──►[Zobraz chybu]──┘
         │ [áno]
         ▼
   [Vytvor reláciu]
         │
     ════╪════  fork
      ▼      ▼
 [Načítaj  [Zapíš do
  profil]   logu]
      ▼      ▼
     ════╪════  join
         ▼
  [Zobraz nástenku]
         │
         ▼
        (◉)
```

## BPMN (v skratke)

**BPMN** = *Business Process Model and Notation* (štandard OMG). Slúži na
modelovanie **biznis procesov**, často naprieč viacerými oddeleniami alebo
firmami. Je podrobnejší a „biznisovejší" než diagram aktivít.

| Prvok | Značka | Význam |
|---|---|---|
| udalosť (event) | kruh — tenký = štart, dvojitý = medzičas, hrubý = koniec | čo sa stalo alebo má stať |
| úloha (task) | zaoblený obdĺžnik | jednotka práce |
| brána (gateway) | kosoštvorec — `×` exkluzívna, `+` paralelná, `○` inkluzívna | vetvenie a zlučovanie toku |
| sekvenčný tok | plná šípka | poradie v rámci jedného procesu |
| tok správ (message flow) | prerušovaná šípka | komunikácia medzi účastníkmi |
| bazén a dráhy (pool / lane) | veľký rámec s pruhmi | účastník procesu (firma, rola) |

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

## Súvisiace

- **Use Case diagram** a scenáre — [šablóna Systémovej analýzy](/citacka.html?s=pro&doc=systemova-analyza)
- **Triedny diagram**, vzťahy medzi triedami (asociácia / agregácia / kompozícia) — [Opakovanie OOP](/citacka.html?s=oop&doc=oop-opakovanie#vztahy-medzi-objektmi-asociacia-agregacia-kompozicia)
