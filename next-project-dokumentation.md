# Next Project – Systemdokumentation

## Översikt

**Next Project** är ett webbaserat projektlednings- och ekonomisystem för byggentreprenadföretag. Systemet hanterar hela projektlivscykeln från kalkyl och budget till fakturering, dagbok och ekonomisk uppföljning. Det är ett SPA (Single Page Application) med URL `next.nordsys.se`.

Systemet är kopplat till ett externt system kallat **Accurator** (leverantörsmarknadsplats), och kan integreras med externt bokföringssystem via verifikationsnummer.

---

## Systemstruktur – Huvudnivåer

```
Next Project
├── Toppmeny (global navigation)
│   ├── Accurator (dropdown)
│   ├── Meddelanden
│   ├── Kunder
│   ├── Leverantörer
│   ├── Prislista
│   ├── Timpriser
│   ├── Administration
│   ├── Support
│   └── Logga ut
│
├── Vänsterpanel – Projektträd
│   └── Hierarkisk lista av kunder/projekt
│
└── Projektmodulerna (flikar per projekt)
    ├── Projekt
    ├── Projektöversikt
    ├── Budget
    ├── Inköp
    ├── Arbetsorder
    ├── Anbud/avtal
    ├── Avvikelse
    ├── ÄTA
    ├── Planering
    ├── Bokf kostn/Int
    ├── Bokf timmar
    ├── Prognos
    ├── Faktura
    ├── Dagbok
    ├── Dagbok 2.0
    ├── Dokument
    └── Karta
```

---

## 1. Vänsterpanel – Projektträd

Hierarkisk trädstruktur för navigering. Färgkodade statusindikatorer på varje projekt.

**Projektstatusfilter:** Mallar, Admin, Offert, Nytt, Beställt, Pågående, Utfört, Klart för fakturering, Fakturerat, Avslutat

---

## 2. Projektmoduler

### 2.1 Projekt (4 underflikar)

#### 2.1.1 Projektinformation

| Sektion | Fält |
|---|---|
| **PROJEKT** | Projektnr, Projektnamn, Projekttyp, Ersättningsform, Projektledare, Arbetsledare, Projektkategori, Note/Spec, Intern notering |
| **KUND** | Kund, Kundkontakt, Referenser (Referensnr, Värde, Arbetsorder, ÄTA) |
| **PROJEKTSTATUS** | Projektstart, Projektslut, Status, Orderdatum, Slutbesiktning, Garantitid, Garantibesiktning |
| **FAKTURERING** | Påslagsmall, Ramavtal, Deb./timma |
| **NYCKELTAL** | Timmar/Kostnad/Intäkter/TB/TG% per rad: Budget, Bokfört ÄTA, Bokfört ej ÄTA, S:a bokfört, Prognos |
| **ARBETSPLATSADRESS** | Adress, Postnr, Ort, Sträcka (km), Arbetsplatsid |

#### 2.1.2 Kontaktlista
Roll, Typ, Företag, Kontakt, Mobil, Telefon, E-post.
Roller: Projektledare (Intern), Arbetsledare (Intern), Kundkontakt (Kund), UE inköp.

#### 2.1.3 Betalplan
Faktureringsplan med lyft/dellyft. Kontraktssumma, Innehåll %, Momstyp, Fakturerat belopp.
Tabell: Aktiviteter fördelade på lyft med %-satser och belopp per datum.
**Koppling:** → **Faktura**

#### 2.1.4 Projektinställningar
ACCURATOR: Visa i Accurator (checkbox)

---

### 2.2 Projektöversikt

Tabell med ekonomisk sammanfattning per projekt.

**Kolumner:** Projektnr, Projektnamn, Projektledare, Projektstart, Kundnamn, Status, Budg kostnad, Budg intäkt, Budg TB, Budg TG%, Betalplan, Bokf kostnad, Bokf intäkt, TB, TG%, SLP prognos, Fakturerbart m.fl.

---

### 2.3 Budget

Revisionsbaserad produktionsbudget. Underflikar: **Kostnader**, **Intäkter**.

**Kolumner:**
- *Dimensioner:* Kontonr, Kontobeskrivning, Aktivitet, Läge
- *Budget:* Kalkylerad kostnad, Justering, Produktionsbudget
- *Resurser:* Kod, Beskrivning, Kontotyp, Mängd, Enhet, Kostn/enh

**Funktioner:** Skapa budget från mall, Slå samman rader, Ändringslogg, Saknas i budget, Sammanställning, **Skapa inköp**, Exportera Excel

**Kopplingar:** → **Prognos** (grund), → **Inköp** (via "Skapa inköp")

---

### 2.4 Inköp

Upphandlingsmodul. Underflikar: Inköp, Tidsplan, Dokument.

**Inköpslista:** Inköp nr, Benämning, Kontonr, Status, Ansvarig, Inköpsbudget, Inköpsmål (%), Köpt summa, Vinst, Leverantör

**Tidskritiska datum:** Önskat leveransdatum, Beställning senast, Anbud senast, Förfrågan senast, Leverans start/slut

**Inköpsdetalj (6 underflikar):** Övergripande, Inköpsrader, Leverantörer, Dokument, Betalplan, Checklistor

**Kopplingar:** ← **Budget**, → **Prognos**, ↔ **Leverantörsregistret**

---

### 2.5 Arbetsorder

AO-hantering. Underflikar: Huvud, Resursuppföljning.

**AO-lista:** AO nr, Beskrivning, Kund, Status, Ekonomistatus, Ersättningsform, Produktionsstart, Bokf kostnad, Bokf intäkt, TB, TG%

**AO-detalj (8 underflikar):** Övergripande, Orderrader, Checklistor, Foton/dokument, Bokf kostnad, Bokf intäkt, Bokf timmar, Leverantörer

**Orderrader:** Kod, Benämning, Kontonr, Enhet, Kalkyl mgd, Kalk kostnad, Utf mängd, Kostn/enh, Pris/enh, Prislista pris/enh, Utförd datum, Debiterbar, Visa i mobilen, Faktura nr, Utf kostnad, Verifikationsnr

**Kopplingar:** → **Faktura**, → **Bokf kostn/Int**, → **Planering**

---

### 2.6 Anbud/avtal

Offertkonstruktion. Sektioner: Offertdatum, Priser vid löpande arbete, Betalning/fakturering, Resursplanering, Övriga villkor.
**Koppling:** Anbudsbelopp används i **ÄTA**

---

### 2.7 Avvikelse

**Kolumner:** Avvikelsenr, Referensnr, Benämning, Rapporterat av, Noterad datum, Status, Avvikelsetyp, Kund, Kundkontakt

**Detalj-sektioner:** Specifikation (Klassificering, Beskrivning, Orsak, Läge, Föreslagen åtgärd), Beslut från beställare, Tid (Tidsförlängning, Antal dagar), Ekonomi (Uppsk självkostnad, Uppskattat pris, Offererat pris, Avtalat pris)

**Underflikar:** Detaljer, Kommunikation, Dokument

**Koppling:** "Skapa ÄTA från avvikelse" → **ÄTA**

---

### 2.8 ÄTA (Ändrings- och Tilläggsarbeten)

**Kolumner:** ÄTA nr, Benämning, Avvikelse-referens, Kund, Entreprenadtyp, ÄTA belopp, Påslagsmall, Ersättningsform, Anbudsbelopp, Bokf kostnad, Bokf intäkt, TB, TG%, ÄTA status, Godkänd av kund

**ÄTA-statusar:** Ny, Pågående, Utförd, Beställd, Godkänd

**Detalj-underflikar:** ÄTA Generellt, Orderrader, Checklistor, Foton/dokument, Bokf kostnad, Bokf intäkt, Bokf timmar

**Kopplingar:** ← **Avvikelse**, → **Faktura**, ↔ **Projektöversikt** (summering)

---

### 2.9 Planering

**Underflikar:** Resursplanering (kalendervy per person), Arbetsorder, Tidsplan arbetsorder (Gantt), Tidsplan

**Koppling:** ← **Arbetsorder** + **Administration (Användare)**

---

### 2.10 Bokf kostn/Int

Verifikationsbaserad transaktionsvy. Underflikar: **Kostnader**, **Intäkter**.

**Kolumner:** Verifikation nr, Verifikationstext, Projektnr, AO/ÄTA, Konto, Nettobelopp, AO/ÄTA-benämning, Debiterbar, Fakturerat, Faktura nr, Leverantörens fakturanr, Leverantör, Bokf datum, Påslag (%), Upparb intäkt

**Koppling:** ← Externt bokföringssystem (verifikationsnummer)

---

### 2.11 Bokf timmar

Tidrapportering. Underflikar: Timmar projekt, Timmar person, Attestera timmar och resor.

**Kolumner:** Godkänd, Datum, Timmar, Roll, Namn, Projektnr, AO/ÄTA, Dagboksnotering, Resa (km)

**Knappar:** Godkänn timmar, Attestera, Justera timkostnader, Hämta lönefil

**Koppling:** → **Projektöversikt**, **Arbetsorder**, **Prognos**

---

### 2.12 Prognos

Ekonomisk prognos per period med versionshantering.

**Kolumner:** Låst, Period, Version, Budget revision, Aktiv, Period start/slut, Inkludera ÄTA, Bokf kostnad/intäkt, TB, TG%, Återst. kost./intäkt, SLP kostnad/intäkt/TB/TG%

**Prognosdetalj per konto:**

| Grupp | Kolumner |
|---|---|
| Aktuell budget | Produktionsbudget, ÄTA totalt, Aktuell produktionsbudget |
| Inköp | Avtalat belopp, Inköpsvinst |
| Bokfört | ÄTA totalt, Bokat totalt |
| Återstående | Produktionsbudget, ÄTA, Aktuell produktionsbudget |
| Prognos | Prognos, Slutlägesprognos (SLP) |

**Koppling:** ← Budget, Inköp, Bokf kostn/Int, ÄTA

---

### 2.13 Faktura

**Kolumner:** Faktura nr, Externt fakturanr, Låst, Fakturarubrik, Kund, Kundkontakt, Distributionsstatus, Fakturadatum, Bokföringsdatum, Förfallodag, Betalad datum, Nettobelopp, Momsbelopp, Fakturabelopp

**Detalj (4 underflikar):** Fakturarader (Kod, Beskrivning, Kontonr, Enhet, Mängd, Pris/enh, Moms, Påslag, Totalt), Faktura-övergripande, Skattereduktion, Fakturabilagor

**Koppling:** ← **Betalplan**, **AO**, **ÄTA** → **Bokf kostn/Int**

---

### 2.14 Dagbok

Kalenderbaserad dagbok. Underflikar: Dagbok, Personalliggare.

**Formulär per dag:** Påbörjat/pågående arbete, Färdigställt arbete, Avvikelser och störningar, ÄTA, Kundgodkännande, Arbetsförhållanden

**Detalj-underflikar:** Orderrader, Dokument, Checklista

**Koppling:** → **Faktura**, kopplas till AO/ÄTA

---

### 2.15 Dagbok 2.0

Strukturerad dagbok med 4 noteringsektioner per dag: Påbörjat/pågående/avslutat, Avvikelser/störningar/hinder, Ändringar och tilläggsarbeten, Övrigt.

**Underflikar:** Noteringar, Väder, Arbetsstyrka, Orderrader, Dokument, Checklistor, Nya och ändrade handlingar

---

### 2.16 Dokument

Trädbaserad dokumenthantering. Auto-genererade mappar per AO, ÄTA, Inköp.

**Kolumner:** Beskrivning, Dokumenttyp, NextDocs sync status, Filstorlek, URL-adress, Visa i portalen, Inkludera i rapporter

**Koppling:** ← AO/ÄTA (auto-mappar), ↔ **NextDocs** (extern sync)

---

### 2.17 Karta

Google Maps-integration med karta/satellit-vy för projektplatser.

---

## 3. Global navigation

### 3.1 Accurator
- Skapa leverantörskonto
- Marknadsplatsen

### 3.2 Kunder
Kundregister. Kolumner: Kundnr, Kund, Kundtyp, Valuta, Orgnr, Adress, E-post, Telefon, Fakturatyp, VAT-nummer, IBAN, Betalningsvillkor, Byggmoms.
Underflikar: Grundinformation, Kontaktpersoner, Avancerat, Dokument.

### 3.3 Leverantörer
Leverantörsregister. Kolumner: Leverantör nr, Orgnr, VAT, EAN, Plusgiro/Bankgiro, Betalningsvillkor, Leverantörstyp, Företagskategorier, Regioner.
Underflikar: Grundinformation, Kontakter, Avancerat, Dokument, Leverantörsstatistik, Företagsbedömning.

### 3.4 Prislista
Artikelbaserade prislistor. Flikar: Prislista, Kundpriser, Projektpriser, Ramavtal, Favoritlistor.
Artiklar: Artikelnr, Beskrivning, Kategori, Konto, Enhet, Kostn/enh, Lagersaldo, Pris/enh, Debiterbar.

### 3.5 Timpriser
| Kod | Beskrivning | Enhet | Kostn/enh | Pris/enh | Kontonr |
|---|---|---|---|---|---|
| AK | Arbetstidsförkortning | tim | 0 | 0 | 7 |
| BL | Arbetsledning | tim | 950 | 950 | 7 |
| EL | Elektriker | tim | 600 | 600 | 4430 |
| LED | Ledig utan ersättning | tim | 0 | 0 | 7 |
| PC | Platschef | tim | 1 150 | 1 150 | 7 |
| PJ | Projektledare | tim | 1 150 | 1 150 | 7 |
| SEM | Semester | tim | 0 | 0 | 7 |
| YA | Yrkesarbetare | tim | 595 | 595 | 4300 |

### 3.6 Administration
Flikar: Användare/Behörigheter, Ekonomi, Kommunikation, Integrationer, Inställningar.
Underflikar (Användare): Användare, Grupper/Rättigheter, Next Docs-delning, Projektportal, Hantera licenser.

---

## 4. Datakopplingar

```
Budget ──────────────────────────────► Prognos
  │                                       ▲
  ├── Skapa inköp ──► Inköp ─────────────┤
  │                    │                  │
  │                    └── Leverantörer   │
Projekt ──► Betalplan ──► Faktura ◄──── ÄTA ◄── Avvikelse
  │                          ▲             ▲
  │                          │             │
Arbetsorder ────────────────┘             │
  │                                        │
  ├── Orderrader (Prislista/Timpriser)     │
  ├── Bokf timmar                          │
  └── Dagbok ─────────────────────────────┘

Bokf kostn/Int ◄── Externt bokföringssystem (verifikationsnr)
Dokument ◄──── AO, ÄTA, Inköp (auto-mappar) + NextDocs sync
Planering ◄──── Arbetsorder + Admin (Användare)
Kunder ──► Projekt, Faktura
Leverantörer ──► Inköp, Bokf kostn/Int
Prislista ──► Orderrader
Timpriser ──► Bokf timmar
Accurator (extern) ──► Inköp
```

---

## 5. Nyckelbegrepp

| Term | Förklaring |
|---|---|
| **AO** | Arbetsorder – uppdragsenhet inom projekt |
| **ÄTA** | Ändring och Tilläggsarbete – extra arbete utöver grundkontraktet |
| **TB** | Täckningsbidrag (Intäkt – Kostnad) |
| **TG%** | Täckningsgrad i procent |
| **SLP** | Slutlägesprognos – prognos för projektets slutvärde |
| **UE** | Underentreprenör |
| **Lyft** | Faktureringstillfälle enligt betalplan |
| **Innehållet** | Kvarhållen del av fakturabelopp (garanti/retention) |
| **Verifikat** | Bokföringspost från externt system |
| **ID06** | Svensk legitimationsstandard för byggindustrin |
| **Accurator** | Extern leverantörsmarknadsplats |
| **NextDocs** | Externt dokumenthanteringssystem med synkronisering |
| **P2512** | Periodbeteckning (P + år + månad, ex. december 2025) |

---

## 6. Teknisk struktur

- **Typ:** Single Page Application (SPA)
- **URL-struktur:** `next.nordsys.se/{kundid}/client/`
- **UI-mönster:** Split-panel layout (lista ovan, detalj nedan)
- **Exportformat:** Excel på de flesta listvyer
- **Mobilapp:** Next Mobile (fält märkta "Visa i mobilen")
- **Integrationer:** Externt bokföringssystem, NextDocs, Accurator, Next Vehicle, API-användare (next_qlik, lundatech)
- **Karttjänst:** Google Maps
- **Språk:** Svenska
