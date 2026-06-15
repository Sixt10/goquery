# Rapport

## 1) Metod och exempel

### Metod
1. Inventera datakällor och åtkomst (lokalt, Drive, Slack).
2. Extrahera relevanta datapunkter med spårbar identifierare per rad.
3. Validera mot primär källa där möjligt (tidsstämpel, avsändare, originaldokument).
4. Klassificera verifieringsgrad per datapunkt.
5. Dokumentera avvikelser och osäkerhet explicit.

### EXEMPEL (syntetisk data): Tabell för arbetssätt

| Rad-ID | Källa | Beskrivning | Underlag | Verifieringsstatus |
|---|---|---|---|---|
| EX-001 | Lokalt | Transaktion summerad | CSV-export + checksumma | Verifierad |
| EX-002 | Drive | Delad fil med KPI | Delvis komplett revisionshistorik | Delvis verifierad |
| EX-003 | Slack | Kommentar om beslut | Skärmdump utan tråd-kontekst | Ej verifierad |

### EXEMPEL (syntetisk data): Tillämpning per post

| Post | Observation | Kontrollsteg | Resultat | Verifieringsstatus |
|---|---|---|---|---|
| EX-A | Siffra i månadsrapport | Matchad mot primär export | Match | Verifierad |
| EX-B | Ändringsdatum i Drive-dokument | Matchad mot metadata, ej full historik | Delvis match | Delvis verifierad |
| EX-C | Påstående i Slack-meddelande | Saknar länk till ursprungsdata | Ej styrkt | Ej verifierad |

## 2) Faktiskt verifierat utfall

> Endast faktiskt kontrollerade resultat redovisas här. Inga syntetiska exempel blandas in.

| Rad-ID | Källa | Vad som verifierats | Evidens | Verifieringsstatus |
|---|---|---|---|---|
| V-001 | Lokalt | Filintegritet för `dataset_2026-05-11.csv` | SHA256 matchar referens | Verifierad |
| V-002 | Drive | Version och ägare för `KPI_Q2` | Metadata bekräftad, innehåll stickprovskontrollerat | Delvis verifierad |
| V-003 | Slack | Beslutstidpunkt i kanaltråd | Tidsstämpel funnen, saknar koppling till beslutsprotokoll | Delvis verifierad |
| V-004 | Extern bilaga | Refererad tabell i bilaga B | Bilaga saknas i leverans | Ej verifierad |

### Dataproveniens

#### Källa: Lokalt
- **Tidpunkt:** 2026-05-12 09:15 UTC
- **Konto:** `analyst@company.local`
- **Scope-nivå:** Projektmapp `/data/project-x` (read-only)
- **Kommentar:** Hash-verifiering utförd mot referensmanifest.

#### Källa: Drive
- **Tidpunkt:** 2026-05-12 09:32 UTC
- **Konto:** `analyst@company.com`
- **Scope-nivå:** Delad mapp `Q2-Reporting` (viewer)
- **Kommentar:** Metadata tillgänglig; full revisionshistorik ej exporterad.

#### Källa: Slack
- **Tidpunkt:** 2026-05-12 09:47 UTC
- **Konto:** `analyst@company.com`
- **Scope-nivå:** Workspace `company`, kanal `#project-x` (member)
- **Kommentar:** Trådreferenser verifierade, men ej fullständig dokumentkedja.
