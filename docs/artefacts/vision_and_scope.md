<div style="page-break-after: always;"></div>

### 1.1 Úvodní studie (Vision & Scope)

#### 1.1.1 Deklarace záměru

- [X] 1 odstavec: účel, přínos, motivace, provozní prostředí.

Účelem tohoto projektu je vytvoření digitálního dvojčete reálné
paralelní robotické struktury (dále jen hexapod)
v softwarovém systému ROS2.
Téma je hlavním předmětem diplomové práce autora,
která bude obsahovat kompletní řešení včetně rešerše, matematického modelu atd.,
řešený hexapod je využíván jako kalibrační prvek v optickém systému.
Provozní prostředí může být uvažováno různé podle konkétní scénáře použití,
tj. např. laboratorní podmínky,
integrace s optickým systémem ve výrobě apod.

Tato práce se soustředí čistě na SW část: implementace do ROS2.

#### 1.1.2 Stakeholdeři

- [x] kdo systém používá, kdo ho spravuje, kdo je regulátor/bezpečnostní autorita

| Osoba | Role |
| ----- | ---- |
| Operátor optického systému | Systém používá |
| Autor | Systém spravuje |
| Vedoucí práce, autor | Regulátor/bezpečnostní autorita |
| Zákazník | Platí za projekt |

#### 1.1.3 Top-5 klíčových scénářů použití (operational scenarios)

1. Funkční prvek optického systému:
   Vytvořený produkt bude sloužit jako součást optického systému (např. kalibrace optické dráhy).
2. Prediktivní simulace pohybu.
3. Testování řídicího algoritmu.
4. Monitoring stavu reálného stroje v reálném čase.
5. Diagnostika poruchy.

#### 1.1.4 Odhad složitosti a rizik

- [x] 3–5 hlavních rizik

1. Nedotažení systému do dostatečně fukční podoby.
2. Latence komunikace mezi ROS2 a HW (znemožní real-time synchronizaci).
3. Nedostupnost fyzického hexapodu pro finální ověření.

#### 1.1.5 Plán ověřování

- [X] v jedné větě: „úspěch je, když ...“ (měřitelné).

Úspěšným zakončením práce bude funkční digitální dvojče konkétního hexapodu, tj. dvojice fyzické struktury a jejího kompletního digitálního modelu, kde bude probíhat obousměrná komunikace.

#### 1.1.6 Hranice systému

- [x] co je uvnitř a co už je okolí
    - [ ] Kontext systému (C4 Kontext / kontextový diagram)
- [ ] seznam událostí / podnětů z okolí.

- Uvnitř systému:
    - Model hexapodu s řízením
    - Simulace
    - HMI / GUI
- Vně systému:
    - Mechanická konstrukce
    - Hardware
    - Napájecí síť

#### 1.1.7 Seznam rolí a aktérů (včetně bezpečnostních rolí).

- [x] Seznam a stručná charakteristika aktérů – rolí pracujících – komunikujících se systémem
- Pozor na
    - [ ] Úplnost seznamu aktérů,
    - [ ] Aktéry, kteří ve skutečnosti se systémem nekomunikují
    - [ ] Sekundární aktéry (není pro ně systém určen, nicméně komunikují;např. motor výtahu)

| Role | Charakteristika |
| ---- | --------------- |
| Operátor | Zadává požadavky na operace, systém používá a modifikuje pouze v uživatelské rovině. V případě chyby má k dispozici jen definované omezené možnosti řešení. |
| Admin | Systém spravuje, preventivně kontroluje. Má výrazně širší možnosti omezené pouze autorem systému. Při bezproblémovém provozu do systému nezasahuje.  |
| Subscriber | Systému může dávat požadavky na poskytnutí informací o předchozím, aktuálním i budoucím chodu, ale nemůže do chodu přímo zasahovat (vyjma nouzového zastavení). |

#### 1.1.8 Základní omezení: HW, rozhraní, standardy, bezpečnostní limity, reálný čas.

- Konfigurece Ubuntu 24.04 + ROSDOS Jazzy Jalisco.
- Výstup komunikace přes průmyslové standardy (EtherCAT?).
- Výkonové omezení (velikost RAM?, grafika?).

#### 1.1.9 Plán práce týmu + rozdělení rolí a autorizace (kdo co vytvořil).

Za celou práci zodpovídá autor - student.
Rolí vedoucího práce je dohlížet a korigovat, ale nenese přímo zodpovědnost za kvalitu výstupu.
