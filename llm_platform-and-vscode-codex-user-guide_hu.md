# LLM Platform and VS Code Codex User Guide

> Human2AI | @NullCodeLabs | 2026  
> Magyar kiadás

## 1. A rendszer egy percben

A Human2AI rendszerben két külön master prompt létezik.

- `llm-platform-master-prompt.txt` — általános, platformszintű Human2AI működési réteg.
- `codex-vscode-master-prompt.txt` — VS Code/Codex számára optimalizált fejlesztői működési réteg.

A két fájl nem egymás másolata, és nem ugyanott töltődik be.

Az LLM-platform prompt az adott AI-szolgáltatás globális instrukciós helyére kerül.  
A Codex prompt a Codex saját lokális instrukciós rétegébe kerül.

Kanonikus források:

- https://github.com/NullCodeLabs/Human2ai-intent-codec/blob/main/llm-platform-master-prompt.txt
- https://github.com/NullCodeLabs/Human2ai-intent-codec/blob/main/codex-vscode-master-prompt.txt

A kézikönyv nem másolja be a promptok teljes tartalmát. Mindig a kanonikus `.txt` fájl a forrás.

---

## 2. Mit jelent a két réteg?

### LLM Platform Master Prompt

Az általános LLM-platform prompt a modell teljes beszélgetési működését szabályozza:

- Contract
- Supervisor Body
- AllGAP
- Precedence / Precedent
- TCO
- OHYL / Investigator
- DIE
- kanonikus állapot
- kontextusfegyelem
- zero-noise kimenet

Nem egyetlen chatre vagy projektre készült. A cél a platformszintű alapműködés.

### Codex VS Code Master Prompt

A Codex-változat ugyanazt a Human2AI működési logikát fordítja le szoftverfejlesztési környezetre.

Kiemelt területek:

- repository
- working tree
- függőségek
- tesztek
- Git
- build
- migráció
- biztonság
- minimális patch
- kanonikus kód
- hibakeresés
- kontextuskezelés

### Fontos

A ChatGPT Custom Instructions nem folyik át automatikusan a VS Code alatti Codexbe.

A Codex saját instruction stackből indul.

---

## 3. Hol kell használni az LLM-platform promptot?

A cél nem az, hogy minden új chat első üzeneteként bemásold.

Ahol a szolgáltató ad account-level vagy globális instrukciós mezőt, oda kell betölteni.

Ahol nincs ilyen, ott projektutasítás vagy API system/developer message a megfelelő hely.

| Platform | Ajánlott hely |
|---|---|
| ChatGPT | Settings → Personalization → Custom Instructions |
| Claude | Settings → Instructions for Claude |
| Gemini | Settings & help → Personal Intelligence → Instructions for Gemini |
| Perplexity | Profile / Personalization + Project Instructions |
| Kimi | Project Instructions; Kimi Code esetén külön globális instruction file |
| DeepSeek | Weben chat/projekt; API-ban system message |
| Qwen | Consumer felületen platformfüggő; API / Model Studio esetén system message |

### Irányelv

Globális helyre az általános OS kerül.

Projektutasításba csak projekt-specifikus delta kerüljön, kivéve ha az adott platform a globális instrukciót nem viszi át a projektbe.

---

## 4. ChatGPT

### Globális beállítás

1. Nyisd meg: `Settings`.
2. Válaszd: `Personalization`.
3. Nyisd meg: `Custom Instructions`.
4. Másold be a kanonikus `llm-platform-master-prompt.txt` tartalmát.
5. Mentsd el.
6. Új chatben ellenőrizd a működést.

### Projekt esetén

A projekt saját utasítási réteget adhat.

A projektbe csak azt írd, ami az adott projektre specifikus:

- cél
- stack
- fájlszabály
- domain-korlát
- elfogadási feltétel

Ne készíts kézi másolatot az általános OS-ről, ha a platform működése ezt nem igényli.

---

## 5. Claude

Claude-ban az account-wide `Instructions for Claude` a megfelelő hely az általános platform OS-hez.

Lépések:

1. Profil / initials.
2. `Settings`.
3. `Instructions for Claude`.
4. Illeszd be a `llm-platform-master-prompt.txt` tartalmát.
5. Projekt esetén a `Set project instructions` mezőbe csak a projekt saját deltája kerüljön.

A projekt knowledge base tartalom.  
A globális instruction működési szabály.

Ne keverd a kettőt.

---

## 6. Gemini

### Globális normál Gemini

1. Nyisd meg a Gemini webes felületét.
2. `Settings and help`.
3. `Personal Intelligence`.
4. `Instructions for Gemini`.
5. `Add`.
6. Illeszd be a platform promptot.
7. Mentsd el.

### Gem esetén

A Gem saját `Instructions` mezőt kap.

A Gem instrukció nem ugyanaz, mint a globális `Instructions for Gemini`.

---

## 7. Perplexity

Perplexityben a személyes profil és a Project Instructions két külön réteg.

Ajánlott elrendezés:

- általános Human2AI preferenciák → Profile / Personalization
- konkrét kutatási vagy fejlesztési projekt → Project Instructions
- projektfájl → referenciaanyag

A prompt ne legyen egyszerre tudásfájl és instrukciós réteg, ha a platform külön kezeli a kettőt.

---

## 8. Kimi, DeepSeek, Qwen

### Kimi

Normál Kimi Project esetén a Project Instructions minden projektchatre érvényes.

Kimi Code külön fejlesztői instruction-rendszert használ.

### DeepSeek

Ha a webes consumer felület nem kínál megbízható account-wide instrukciós mezőt:

- használd chat- vagy projektszinten
- API esetén használd system message-ként

### Qwen

A consumer felület funkciói változhatnak.

API / Model Studio használatnál a system message a stabil, modellfüggetlen elv.

### Szabály

Ha egy platform nem ad valódi globális instrukciós réteget, ne erőltesd.

A kanonikus prompt maradjon változatlan. Csak a betöltési adapter változik.

---

## 9. VS Code + Codex: a helyes architektúra

A Codex nem a ChatGPT Custom Instructionsből dolgozik.

Saját instruction stacket épít.

Ezért a `codex-vscode-master-prompt.txt` külön Codex-forrás.

Gyakorlati sorrend:

```text
Natív Codex rendszer / sandbox / engedélyek
        ↓
config.toml developer_instructions [ha használod]
        ↓
$CODEX_HOME/AGENTS.override.md vagy AGENTS.md
        ↓
projektgyökértől cwd-ig: AGENTS.* vagy fallback fájlnevek
        ↓
aktuális user kérés + lokális környezet
```

---

## 10. Windows telepítés: Codex master prompt

Célállapot:

```text
C:\Users\<WINDOWS_USER>\.codex\codex-vscode-master-prompt.txt
C:\Users\<WINDOWS_USER>\.codex\AGENTS.md
C:\Users\<WINDOWS_USER>\.codex\sync-codex-prompt.ps1
C:\Users\<WINDOWS_USER>\.codex\config.toml
```

A kanonikus forrás kizárólag a `.txt`.

Az `AGENTS.md` Codex-kompatibilis tükör.

Kézzel nem szerkeszted.

Lépések:

1. Hozd létre a `C:\Users\<WINDOWS_USER>\.codex\` mappát, ha még nincs.
2. Tedd bele a `codex-vscode-master-prompt.txt` kanonikus fájlt.
3. Hozd létre a `sync-codex-prompt.ps1` szinkronscriptet.
4. Futtasd a szinkront.
5. Indíts új Codex sessiont.

---

## 11. Egyirányú TXT → AGENTS.md szinkron

```powershell
$src = "$env:USERPROFILE\.codex\codex-vscode-master-prompt.txt"
$dst = "$env:USERPROFILE\.codex\AGENTS.md"

Copy-Item $src $dst -Force
Write-Host "Synced: $src -> $dst"
```

Mentési hely:

```text
C:\Users\<WINDOWS_USER>\.codex\sync-codex-prompt.ps1
```

Kézi futtatás:

```powershell
powershell -ExecutionPolicy Bypass -File "$env:USERPROFILE\.codex\sync-codex-prompt.ps1"
```

### Kanonikus szabály

Az `AGENTS.md` generált kompatibilitási fájl.

Soha ne javítsd kézzel.

Minden módosítás a `codex-vscode-master-prompt.txt` fájlban történik, majd újraszinkronizálod.

---

## 12. config.toml: mire való és mire nem

A `project_doc_fallback_filenames` nem a `$CODEX_HOME` globális `.txt` fájlját teszi automatikusan globális utasítássá.

A dokumentált globális réteg a `$CODEX_HOME` alatti:

- `AGENTS.md`
- `AGENTS.override.md`

Ajánlott minimum:

```toml
# C:\Users\<WINDOWS_USER>\.codex\config.toml

# A globális Human2AI prompt betöltését az AGENTS.md tükör adja.
# A config.toml csak más Codex-beállításokat tartalmazzon, ha tényleg szükséges.
```

Projekt-fallback fájlnevekhez:

```toml
project_doc_fallback_filenames = ["codex-vscode-master-prompt.txt"]
```

Ezt csak akkor használd, ha repositoryn belüli `.txt` instrukciófájlt is Codex-projektutasításként akarsz felismerni.

---

## 13. Globális prompt vs. projekt delta

### Globális Codex prompt

Tartalmazza:

- Human2AI Contract
- Supervisor Body
- AllGAP
- Precedence
- Precedent
- TCO
- OHYL
- DIE
- repository-first
- canonical code
- minimal patch
- testing
- Git discipline
- dependency discipline
- security baseline

### Projekt AGENTS.md

Tartalmazza:

- repository célja
- tech stack
- build parancsok
- tesztparancsok
- könyvtárszerkezet
- konvenciók
- projekt-specifikus invariánsok
- deploy és migráció sajátosságok

### Ne duplikálj

A projekt AGENTS.md ne másolja újra a globális Human2AI OS-t.

Csak a projekt saját deltáját tartalmazza.

---

## 14. Napi használat: ideális munkafolyamat

1. Indítsd a VS Code-ot a megfelelő repositoryban.
2. Győződj meg róla, hogy a globális TXT legutóbbi állapota át lett szinkronizálva AGENTS.md-be.
3. Indíts új Codex sessiont, ha a globális promptot közben módosítottad.
4. A feladatot outcome-ként add meg.
5. Mondd meg, mi nem sérülhet.
6. Mondd meg, mi számít elfogadottnak.
7. Ne írd elő a technikai módszert, ha az nem hard constraint.
8. Kódmódosítás után kérj vagy engedj releváns tesztet.
9. Commit / push / deploy csak a kívánt scope szerint.

Példa:

```text
CÉL: a login 2 másodpercen belül adjon visszajelzést.
NEM SÉRÜLHET: jelenlegi Google login, Firestore schema, mobil UI.
ELFOGADÁS: meglévő tesztek + új regressziós teszt pass.
MÓDSZER: rád bízom; keresd a legrövidebb megbízható utat.
```

---

## 15. A prompt frissítésének helyes rendje

A kanonikus fájl ugyanaz marad.

Nem készül:

- final2
- revised
- v7-copy
- new-final
- revised-final

A verziót Git commit, tag vagy belső fejléc követheti.

Lépések:

1. Módosítsd helyben a `codex-vscode-master-prompt.txt` fájlt.
2. Nézd át a deltát.
3. Futtasd a `sync-codex-prompt.ps1` fájlt.
4. Ellenőrizd, hogy az `AGENTS.md` azonos-e a TXT tartalmával.
5. Commitold a kanonikus TXT módosítását.
6. Indíts új Codex sessiont.

Gyors ellenőrzés:

```powershell
$a = Get-FileHash "$env:USERPROFILE\.codex\codex-vscode-master-prompt.txt"
$b = Get-FileHash "$env:USERPROFILE\.codex\AGENTS.md"
$a.Hash -eq $b.Hash
```

Elvárt eredmény:

```text
True
```

---

## 16. Hogyan teszteld, hogy tényleg fut?

Ne azt kérdezd:

```text
Betöltötted-e a promptot?
```

Viselkedést tesztelj.

### Shortest Path teszt

```text
Adj két technikai út helyett egyetlen ajánlott utat.
A döntést teljes TCO, karbantartás és visszaállíthatóság alapján hozd meg.
```

### Precedent teszt

```text
Mielőtt új modult írsz, keresd meg, van-e már ugyanez a funkció
a repositoryban, a standard libraryban vagy a frameworkben.
```

### Canonical Code teszt

```text
Ne hozz létre új helper fájlt, ha a funkció jelenlegi
kanonikus implementációja javítható.
```

### AllGAP teszt

```text
A hiba frontendként látszik.
Vizsgáld meg, nem backend, auth, schema, config vagy deploy boundary okozza-e.
```

---

## 17. Hibaelhárítás

### A Codex úgy viselkedik, mintha nem látná a globális promptot

Ellenőrizd:

- `$env:USERPROFILE\.codex\AGENTS.md` létezik-e
- tartalma megegyezik-e a kanonikus TXT-vel
- a sync script lefutott-e
- új Codex session indult-e
- nincs-e `AGENTS.override.md`
- nincs-e projektben specifikusabb `AGENTS.md`

### A platform prompt működik normál chatben, de projektben nem

Ellenőrizd a platform projektutasításainak precedence szabályait.

Ha a projekt saját instruction rétege erősebb, a projekt deltájában őrizd meg a szükséges globális invariánsokat.

### A válasz túl hosszú vagy túl AI-s

Ne told hozzá újra ugyanazt a stílusszabályt minden chathez.

A globális promptot javítsd.

---

## 18. Bizalom, biztonság, terjesztés

A kanonikus prompt `.txt` formátuma szándékosan egyszerű.

A felhasználónak nem kell futtatható binárist, installert, makrót vagy idegen scriptet megbíznia ahhoz, hogy a promptot elolvassa és LLM-be illessze.

A `.txt` önmagában nem biztonsági pajzs.

A valódi biztonsági határt az adja, hogy:

- milyen fájlokat futtatsz
- milyen repositoryt nyitsz meg
- milyen shell parancsot engedélyezel
- milyen projektinstrukciókat örökölsz
- milyen dependency-ket telepítesz

A promptfájl ettől még jó terjesztési forma, mert:

- passzív
- könnyen auditálható
- diffelhető
- verziózható
- platformfüggetlen

### Codex-specifikus figyelmeztetés

Egy idegen repository `AGENTS.md` vagy hasonló projektinstrukciós fájlja ugyanúgy befolyásolhatja az agent viselkedését.

Ismeretlen repositoryban előbb nézd át az instrukciós fájlokat.

---

## 19. Rövid FAQ

### Felülírja a Codex prompt a ChatGPT platform promptot?

Nem.

Külön rendszerben töltődnek be.

A közös Human2AI logikát a két prompt tartalmi összehangolása adja.

### Kell a Codex TXT-t VS Code Settingsbe másolni?

Nem.

A javasolt Windows megoldás:

```text
kanonikus TXT a .codex mappában
↓
automatikus AGENTS.md tükör
↓
Codex
```

### Miért kell AGENTS.md, ha a kanonikus fájl TXT?

Mert a Codex globális user instruction forrása az `AGENTS.md`.

Az `AGENTS.md` itt csak kompatibilitási tükör, nem második Source of Truth.

### A project_doc_fallback_filenames kiváltja ezt?

Nem globálisan.

A fallback fájlnevek a projektinstrukciók körét bővítik.

### Mikor kell új Codex session?

Globális instrukció módosítása után ez a biztos út, hogy az új állapot frissen épüljön be.

---

## 20. Kanonikus linkek

### Human2AI promptok

- https://github.com/NullCodeLabs/Human2ai-intent-codec/blob/main/llm-platform-master-prompt.txt
- https://github.com/NullCodeLabs/Human2ai-intent-codec/blob/main/codex-vscode-master-prompt.txt

### Platformdokumentáció

- OpenAI Custom Instructions: https://help.openai.com/en/articles/8096356
- OpenAI Codex agent instruction stack: https://openai.com/index/unrolling-the-codex-agent-loop/
- Claude Personalization: https://support.claude.com/en/articles/10185728-understanding-claude-s-personalization-features
- Claude Projects: https://support.claude.com/en/articles/9519177-how-can-i-create-and-manage-projects
- Google Instructions for Gemini: https://support.google.com/gemini/answer/16598625?hl=en
- Google Custom Gems: https://support.google.com/gemini/answer/15235603?hl=en
- Perplexity Projects: https://www.perplexity.ai/help-center/en/articles/10352961-what-are-spaces
- Kimi Projects: https://www.kimi.com/en/help/features/project
- Kimi Code Customization: https://www.kimi.com/en/help/kimi-code/cli-customization

---

@NullCodeLabs | Human2AI Intent Codec | 2026
