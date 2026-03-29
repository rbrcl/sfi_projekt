<div style="page-break-after: always;"></div>

### 1.2 Specifikace požadavků (Requirements Specification)

- [ ] Cíl: vytvořit popis požadavků tak, aby byly jednoznačné, testovatelné a sledovatelné.

#### 1.2.1 Use-case model / user stories: hlavní scénáře + alternativní a chybové toky.

- [x] 2 hlavni scenare
- [x] 1 alternativni
- [x] 1 chybovy

| Označení | Typ scénáře | Název |
| -------- | ----------- | ----- |
| UC-01 | hlavní | Polohování v optickém systému |
| UC-02 | hlavní | Vzdálený monitoring, diagnostika, kalibrace |
| UC-03 | chybový | Výpadek pohonu |
| UC-04 | alternativní | Manuální polohování |

##### Hlavní scénáře

1. Polohování v optickém systému:

    - Operátor zadá požadovanou orientaci platformy.
    - Systém provede simulaci pohybu, ověří jeho bezpečnost a proveditelnost.
    - Systém provede pohyb na fyzickém manipulátoru a zároveň ho po celou dobu monitoruje a porovnává s napočítaným průběhem simulace.

2. Vzdálený monitoring, diagnostika, kalibrace:

    - Admin se připojí systému, vyžádá si telemetrická data (polohy, proudy, stav ROS2 uzlů).
    - Provede kontrolní algoritmy v případě potřeby provede kalibraci.

##### Alternativní a chybové scénáře

3. Výpadek pohonu:

    - Při provádění pohybu se fyzický hexapod začne vychylovat od simulované polohy nebo proudové odběry.
    - Systém zastaví pohyb a stabilizuje platformu v bezpečné poloze.
    - Spustí se identifikační algoritmus, který zjistí odpovídající chování při výpadku konkrétního pohonu.
    - Vypíše se chybová zpráva.

4. Manuální polohování:

    - Operátor ovládá polohu hexapodu ručně (např. joystickem). Systém v reálném čase aktualizuje digitální dvojče, ale neposílá příkazy do fyzického HW.
    - Může být použit např. při mechanickém servisním zásahu.

#### 1.2.2 Seznam funkčních a nefunkčních požadavků.

- [ ] U každého: popis, priorita, zdroj, ověření.

| ID | Typ | Zkrácený text | UC | AC / metrika | Ověření |
|----|-----|---------------|----|--------------|---------|
| FR-01	| FR | Vizualizace polohy | UC-01 | Model v RViz2 odpovídá HW ±1 mm | D |
| FR-02	| FR | Inverzní kinematika | UC-01 | Výpočet polohy kloubů < 5 ms | A |
| FR-03 | FR | Detekce kolizí v simulaci | UC-01 | Zastavení před kolizí v modelu | T/A |
| FR-04 | FR | Logování telemetrie | UC-02 | Záznam (CSV/rosbag) 100 Hz	| T |
| FR-05	| FR | Validace cílové polohy | UC-01 | Odmítnutí bodu mimo pracovní prostor | T |
| NFR-01 | NFR | Latence řízení | UC-01 | Round-trip (SW->HW->SW) < 20 ms | T |
| NFR-02 | NFR | Bezpečnost (Failsafe) | UC-03 | Aktivace stop-stavu při ztrátě ROS zpráv | T |
| NFR-03 | NFR | Intuitivnost GUI | UC-04 | Zaškolení operátora do 15 min | D |

- Přehled metod ověření V&V

    | Zkratka | Název | Význam |
    | ------- | ----- | ------ |
    | I | Inspection (inspekce) | Ověření vizuální kontrolou nebo kontrolou dokumentace bez měření. |
    | T | Test (zkouška) | Ověření experimentem nebo měřením na reálném systému nebo prototypu. |
    | A | Analysis (analýza) | Ověření výpočtem, simulací nebo analytickým posouzením. |
    | D | Demonstration (demonstrace) | Ověření předvedením funkce bez přesného měření. |



##### Akceptační kritéria pro klíčové požadavky (doporučeno Given–When–Then).

| Požadavek | FR-05 Validace polohy |
| --------- | --------------------- |
| Given | Systém je v režimu Ready |
| When | Operátor zadá souřadnici Z mimo mechanický limi |
| Then | Systém pohyb nepovolí a v GUI zobrazí hlášení "Out of Reach" |

##### Nefunkční požadavky: bezpečnost (failsafe), spolehlivost/dostupnost, výkon/odezva, použitelnost, udržovatelnost, kyberbezpečnost.



#### 1.2.3 Požadavky na rozhraní (Interface Requirements): signály, zprávy, API, datové formáty, časování.

V ROS2 je v podstatě veškerá komunikace řešená pomocí tzv. topics.
Formát zprávy je možné stanovit uživatelsky.
Vzhledem k tomu, že veškeré fyzické a mechanické prvky jsou mimo hranice systému,
tak není jiné rozhraní potřebné.

| Topic | Message type | Obsah / Význam | Frekvence |
| ----- | ------------ | ---------------| --------- |
| /joint_states | sensor_msgs/JointState | Aktuální pozice, rychlosti a proudy motorů | 100 Hz |
| /cmd_pose | geometry_msgs/Pose | Požadovaná kartézská poloha platformy |On-demand |
| /diagnostics | diagnostic_msgs/DiagnosticArray | Stavy uzlů, teploty driverů, chybové kódy | 1 Hz |
| /set_mode | std_srvs/SetBool | Služba (API) pro přepnutí Simulation / Real-HW | Service |

#### 1.2.4 Stop-stavy a chování při poruchách (fault handling) – vazba na bezpečnost.

| Název | Podmínka | Popis | Bezpečnost |
| ----- | -------- | ----- | ---------- |
| E-STOP | Stisk tlačítka / Proudový peak | Okamžité odpojení silového napájení motorů. | ano |
| SOFT-STOP | Odchylka model vs. realita > 5 mm | Plynulé zastavení po trajektorii a uzamčení brzd. | ano |
| SIM-ONLY MODE | Ztráta spojení s HW robotem | Digitální dvojče pokračuje v simulaci, ale odpojí výstupy. | ne |
| COMM_FAULT | Prodleva informace z daného ROS2 uzlu > 100ms (?) | Systém plynule zastaví. | ano |
