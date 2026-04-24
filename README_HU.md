# human2ai-intent-codec — @NullCodeLabs

> **HSL-C Codec v0.4** | Emberi szándék → AI-végrehajtható kényszertér  
> Kategória: Intent Engineering | Szint: haladó | Nyelv: EN + HU

---

## Mi ez?

Az AI nem azt csinálja, amit gondolsz — hanem amit kap.

**human2ai-intent-codec** egy strukturált kódolási protokoll, amely a nyers emberi szándékot AI-végrehajtható kényszertérré alakítja. Nem prompt-sablon. Nem instrukciólista. **Kényszertér:** olyan bemeneti struktúra, amelyen belül az AI csak a szándékodnak megfelelő kimenetet tud produkálni.

A Microsoft Research (2026) ugyanezt "intent formalization"-nek nevezi.  
Mi HSL-C Codec-nek hívjuk — és már GitHub-on van.

---

## Az intent gap

**Intent gap** = a távolság aközött, amit gondolsz, és amit az AI csinál.

| Forrás | Amit küld | Amit az AI értelmez |
|--------|-----------|---------------------|
| Felhasználó | "Írj egy összefoglalót" | formátum? hossz? célcsoport? — ismeretlen |
| Felhasználó | "Elemezd ezt" | milyen tengely? mi a cél? — ismeretlen |
| Felhasználó | "Javítsd meg" | mi a standard? kinek szól? — ismeretlen |

Minden kérdőjel mérhetetlen intent gap. A HSL-C Codec minden kérdőjelet bezár.

---

## Funkciók — hatékonyság szerint

### 🔴 ALWAYS ON — mindig fut, nem kapcsolható ki

**1. OHYL / Oknyomozó — a legnagyobb hatású modul**

Azt hozza fel, amit nem kérdeztek — de kellett volna. Visszafelé kérdez, gyökérokig megy. Minden kutatási, elemzési, piaci vagy validációs feladatnál kötelezően élő netes adatokból dolgozik. Ha a modell offline: azonnal jelzi, megmondja melyik feladatnál jelent korlátot, és leáll — nem degradáltan fut, nem hallgat róla.

**2. Legrövidebb Út — proaktív hatékonyság**

Minden feladatnál automatikusan keresi a legkevesebb lépést, legkevesebb tudást, legkevesebb időt, legkevesebb eszközt igénylő megoldást. Ha rövidebb út létezik → azt adja elsőnek, nem alternatívaként. Nem jelzi — csinálja. Az user dönt ha mást akar.

**3. Shut-Up Filter — az alapzaj kizárása**

Kiirt minden AI-ízt. Úgy ír, mintha te írtad volna. Tiltott: "Természetesen!" / "Örömmel segítek!" / "In conclusion" / "Furthermore" / "Delve" — és minden bevezető vagy lezáró mondat, ami nem tartalom. Ha elrontotta: 2-3 szóban beismeri. Tovább.

---

### 🟡 CODEC MAG — mindig aktív háttérrendszer

**4. Intent Gap Detekció + 4D Mátrix**

Minden inputnál ellenőrzi: ugyanazt érti-e mindkét fél? Ha eltérés: [f] jelzés, reset. A 4D mátrix négy tengelyen kódolja a szándékot — gép / ember / óhaj / kényszer — és öt gap-típust kezel: terminális / kontextuális / strukturális / szándék↔kimenet / instruction gap.

---

### 🟠 AUTO — kontextus alapján indul, kikapcsolható

**5. DIE — Disruptive Intelligence Engine**  
`Kikapcsolás: @NullCodeLabs DIE OFF`

Automatikusan aktiválódik diszruptív piaci kérdés, innovációs irány vagy "mi a következő lépés" kontextusnál. Az *adjacent possible*-t elemzi — a következő törési pontot és a ki nem használt piaci rést. Output: [DIE] jelöléssel, elkülönítve.

**6. Competitor Motor**  
`Kikapcsolás: @NullCodeLabs COMPETITOR OFF`

Automatikusan aktiválódik versenytárs, piac, pozicionálás vagy árképzés kontextusnál. Valódi képet ad — nem PR-összefoglalót. Szétválasztja: tény / következtetés / feltételezés. Output: nyers összkép → erősségek → gyengeségek → gyanús jelek → kihasználható rés → ellenstratégia → brutál őszinte végszó.

**7. NotebookLM Validációs Réteg**  
`Kikapcsolás: @NullCodeLabs NOTEBOOK OFF`

Automatikusan aktiválódik validáció, kutatás összefoglalása vagy projekt review kontextusnál. Azonosítja a feltárt mintázatokat, validálja külső forrásokkal, generál fejlesztési irányokat, listázza a még meg nem írt, de szükséges modulokat.

---

## Parancssor

```
go / igen / ok / mehet    → végrehajtás
stop / állj               → azonnali leállás
why / debug               → belső logika látható
@NullCodeLabs DIE OFF
@NullCodeLabs COMPETITOR OFF
@NullCodeLabs NOTEBOOK OFF
@NullCodeLabs MATRIX      → teljes állapot export
reset                     → tiszta lap
```

---

## Repo struktúra

```
human2ai-intent-codec-4NullCodeLabs/
├── README.md
├── README_HU.md
├── human2ai-intent-codec-@NullCodeLabs.txt
├── human2ai-intent-codec-@NullCodeLabs_EN.txt
├── LICENSE
└── SIGNATURE.md
```

---

## Kapcsolódó repók

| Repó | Kapcsolat |
|------|-----------|
| [ncl-control-core](https://github.com/NullCodeLabs/ncl-control-core) | HSL-C Kernel v0.4 |
| [shut-up-ai-just-answer](https://github.com/NullCodeLabs/shut-up-ai-just-answer) | Zero-noise végrehajtó réteg |
| [Write-Like-A-Pro-No-BS-With-AI-4NCL](https://github.com/NullCodeLabs/Write-Like-A-Pro-No-BS-With-AI-4NCL) | CFAI Standard v2.5 |

---

## Párhuzamos kutatás

> *"Structured Intent as Protocol-Like Layer"* — Microsoft Research, 2026  
> Független megerősítés. HSL-C Codec megoldja — nyílt forráskóddal, freelancer-méretű eszközzel.

---

## Licenc

**CC BY-NC-SA 4.0** — Infinity Possibility Media Co. | NullCodeLabs  
Nem kereskedelmi: szabad. Kereskedelmi: tilos. Módosítás: azonos licenc alatt.

---

**István Taubert** | [@NullCodeLabs](https://github.com/NullCodeLabs) | [Facebook](https://www.facebook.com/infinitypossibilities.HUB)

*"Nem a kérés hibás — hanem a kényszertér, amibe csomagolod."*  
*Built with zero noise. Powered by First Principles. — @NullCodeLabs*
