<div style="page-break-after: always;"></div>

### 1.2 Specifikace požadavků (Requirements Specification)

- [ ] Cíl: vytvořit popis požadavků tak, aby byly jednoznačné, testovatelné a sledovatelné.

#### 1.2.1 Use-case model / user stories: hlavní scénáře + alternativní a chybové toky.

- [ ] 2 hlavni scenare
- [x] 2 alternativni/chybove toky

- Polohování v optickém systému:
    - Operátor zadá požadovanou orientaci platformy.
    - Systém provede simulaci pohybu, ověří jeho bezpečnost a proveditelnost.
    - Systém provede pohyb na fyzickém manipulátoru a zároveň ho po celou dobu monitoruje.
- Chybový tok - výpadek pohonu:
    - Při provádění pohybu se fyzický hexapod začne vychylovat od simulované polohy.
    - Systém zastaví pohyb a stabilizuje platformu v bezpečné poloze.
    - Spustí se identifikační algoritmus, který zjistí odpovídající chování při výpadku konkrétního pohonu.
    - Vypíše se chybová zpráva.
- Chybový tok - proudové přetížení:
    - Při provádění pohybu začnou pohony platformy odebírat výrazně větší proudy oproti simulaci.
    - Systém zastaví pohyb a stabilizuje platformu v bezpečné poloze.
    - Identifikační algoritmus ověří proudové odchylky jednotlivých pohonů a na výstupu odhadne polohu a směr omezení.

#### 1.2.2 Seznam funkčních a nefunkčních požadavků s identifikátory (např. FR-01, NFR-03). U každého: popis, priorita, zdroj, verifikace.

| ID | Typ | Zkrácený text | UC | AC / metrika | Ověření |
|----|-----|---------------|----|--------------|---------|
| FR-01 | FR | bla | UC-00 | bla | ITAD |
| FR-02 | FR | bla | UC-00 | bla | ITAD |
| FR-03 | FR | bla | UC-00 | bla | ITAD |
| NFR-01 | NFR | bla | UC-00 | bla | ITAD |
| NFR-02 | NFR | bla | UC-00 | bla | ITAD |

##### Akceptační kritéria pro klíčové požadavky (doporučeno Given–When–Then).



##### Nefunkční požadavky: bezpečnost (failsafe), spolehlivost/dostupnost, výkon/odezva, použitelnost, udržovatelnost, kyberbezpečnost.



#### 1.2.3 Požadavky na rozhraní (Interface Requirements): signály, zprávy, API, datové formáty, časování.

V ROS2 je v podstatě veškerá komunikace řešená pomocí tzv. topics. Formát zprávy je možné stanovit uživatelsky. Vzhledem k tomu, že veškeré fyzické a mechanické prvky jsou mimo hranice systému, tak není jiné rozhraní potřebné

- signály
- zprávy
- API
- datové formáty
- časování

| Topic | Message type | Obsah |
| ----- | ------------ | ----- |
|  |  | aktuální poloha všech 6 pohonů |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |

#### 1.2.4 Stop-stavy a chování při poruchách (fault handling) – vazba na bezpečnost.

- [ ] popsat 2 az 3 stop stavy

| Název | Podmínka | Popis | Bezpečnost? |
| ----- | -------- | ----- | ----------- |
|  |  |  |  |
|  |  |  |  |
