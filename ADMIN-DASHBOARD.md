# Admin Dashboard - Orangemakers Udlånssystem

Dette dokument beskriver admin dashboard funktionalitet og interface elementer.

**Se også:**
- [User Stories](USER-STORIES.md) for baggrund
- [Funktionelle Krav](FUNKTIONELLE-KRAV.md) for tekniske krav
- [Datamodel](DATAMODEL.md) for entiteter

---

## Oversigt

Admin dashboard giver administratorer et centralt overblik over udlånssystemet og mulighed for at administrere udstyr, tjeklister, brugere og se rapporter.

**Målgruppe**: Administratorer (rolle: administrator)

---

## Dashboard Sektioner

### 1. Overblik (Dashboard Forside)

**Formål**: Hurtig status på systemet

**Widgets:**
- **Aktive udlån**: Antal aktuelle udlån
- **Forsinket returnering**: Antal udlån der er overskredet forventet returdato
- **Beskadiget udstyr**: Antal enheder til reparation
- **Ledigt udstyr**: Antal enheder klar til udlån
- **Seneste aktivitet**: Liste over de seneste 10 udlån/returneringer

**Relaterede krav**: FR-014

---

### 2. Udstyrshåndtering

**Formål**: Administrer alt udstyr i systemet

**Funktioner:**
- **Liste over alt udstyr** med søgning og filtrering
  - Filtre: Status (ledig, udlånt, beskadiget), Type, Placering
  - Søgning: Navn, ID
- **Opret nyt udstyr**
  - Felter: Navn, Type, Beskrivelse, Placering, Generel note
  - Standard låneperiode (dage)
  - Maksimal låneperiode (dage)
  - Tilknyt udleveringstjekliste
  - Tilknyt returneringstjekliste
- **Rediger eksisterende udstyr**
  - Alle felter kan redigeres
  - Historik over ændringer
- **Slet udstyr** (kun hvis aldrig udlånt)
- **Vis udstyr detaljer**
  - Generel info
  - Udlånshistorik (anonymiseret)
  - Skadehistorik
  - Nuværende status

**Relaterede krav**: FR-006, FR-007, FR-008, FR-009, FR-010, FR-049, FR-052, FR-053
**Relaterede entiteter**: [Udstyr](DATAMODEL.md#udstyr)

---

### 3. Tjeklistehåndtering

**Formål**: Opret og administrer tjeklister til udlevering og returnering

**Funktioner:**
- **Liste over alle tjeklister**
  - Filtre: Type (udlevering/returnering), Udstyrstype
- **Opret ny tjekliste**
  - Navn
  - Type (udlevering eller returnering)
  - Udstyrstype/kategori
  - Beskrivelse
  - Tilføj tjekpunkter:
    - Beskrivelse
    - Rækkefølge
    - Obligatorisk (ja/nej)
    - Type (afkrydsning/note)
- **Rediger tjekliste**
  - Tilføj/fjern/ændre tjekpunkter
  - Ændre rækkefølge (drag-and-drop)
- **Slet tjekliste** (kun hvis ikke i brug)
- **Forhåndsvisning af tjekliste**

**Relaterede krav**: FR-032, FR-033, FR-034, FR-037, FR-038
**Relaterede entiteter**: [Tjekliste](DATAMODEL.md#tjekliste), [Tjekpunkt](DATAMODEL.md#tjekpunkt)
**Relaterede user stories**: US-012

---

### 4. Brugerhåndtering

**Formål**: Administrer ansvarlige og medlemmer

#### 4.1 Ansvarlige

**Funktioner:**
- **Liste over ansvarlige**
  - Filtre: Aktiv/inaktiv, Rolle
- **Opret ny ansvarlig**
  - Navn, Email
  - Rolle (ansvarlig/administrator)
  - RFID kode (valgfrit)
  - Password (valgfrit hvis RFID)
- **Rediger ansvarlig**
  - Nulstil password
  - Skift RFID kode
  - Deaktiver/aktiver
- **Slet ansvarlig** (kun hvis ingen udlån registreret)

**Relaterede krav**: FR-022, FR-023
**Relaterede entiteter**: [Ansvarlig](DATAMODEL.md#ansvarlig)

#### 4.2 Medlemmer

**Funktioner:**
- **Liste over medlemmer**
  - Filtre: Status (aktiv/inaktiv)
  - Søgning: Navn, medlemsnummer, RFID
- **Opret nyt medlem**
  - Navn
  - RFID kode
  - Medlemsnummer
  - Gyldigt fra/til dato
- **Rediger medlem**
  - Opdater gyldigheds periode
  - Skift RFID kode
  - Skift status
- **Slet medlem** (kun hvis ingen udlån historik)

**Relaterede krav**: FR-024, FR-025
**Relaterede entiteter**: [Medlem](DATAMODEL.md#medlem)

---

### 5. Udlånsoversigt

**Formål**: Se og administrer aktive og historiske udlån

**Funktioner:**
- **Liste over alle udlån**
  - Filtre:
    - Status (aktiv/returneret)
    - Låntagertype (medlem/placering)
    - Datointerval
    - Udstyr
    - Forsinket (ja/nej)
  - Søgning: Udstyr navn, låntager (kun aktive)
- **Vis udlån detaljer**
  - Udstyr info
  - Låntager info (kun hvis aktiv eller indenfor 3-måneders retention)
  - Udlånsdato, forventet retur, faktisk retur
  - Ansvarlig der godkendte
  - Bekræftelser (instruktion/kompetence)
  - Udleveringstjekliste udfyldelse
  - Returneringstjekliste udfyldelse (hvis returneret)
- **Manuelt luk udlån** (force returnering ved nødsituation)
  - Kræver administrator rolle
  - Skal angive årsag

**Relaterede krav**: FR-011, FR-012, FR-013, FR-014
**Relaterede entiteter**: [Udlån](DATAMODEL.md#udlån)

---

### 6. Skaderapporter

**Formål**: Administrer skader og reparationer

**Funktioner:**
- **Liste over skaderapporter**
  - Filtre: Status (afventer/under reparation/repareret)
  - Sortering: Nyeste først
- **Vis skaderapport detaljer**
  - Udstyr info
  - Beskrivelse af skade
  - Rapporteret af og dato
  - Relateret udlån (hvis relevant)
  - Reparationsnoter
  - Reparationsdato
- **Opdater skaderapport**
  - Marker som "under reparation"
  - Tilføj reparationsnoter
  - Marker som repareret
  - Angiv reparationsdato
- **Statistik**
  - Hyppigst beskadigede udstyr
  - Gennemsnitlig reparationstid
  - Antal skader per måned

**Relaterede krav**: FR-039, FR-040, FR-041, FR-042, FR-043
**Relaterede entiteter**: [Skaderapport](DATAMODEL.md#skaderapport)
**Relaterede user stories**: US-011
**Relaterede flows**: [Flow 5](FLOWS.md#flow-5-reparation-af-beskadiget-udstyr)

---

### 7. Rapporter og Statistik

**Formål**: Indsigt i udlånsmønstre og systemets brug

**Rapporter:**

#### 7.1 Udlånsstatistik
- Antal udlån per måned/år
- Antal udlån per udstyrstype
- Gennemsnitlig låneperiode
- Mest populære udstyr
- Peak udlånstider

#### 7.2 Brugerstatistik
- Antal unikke låntagere per måned (anonymiseret)
- Fordeling: Medlemmer vs. placering
- Gennemsnitlig lånevarighed per type

#### 7.3 Skadestatistik
- Antal skader per måned
- Skader per udstyrstype
- Gennemsnitlig reparationstid
- Kostbareste udstyr (mest skadesramt)

#### 7.4 Effektivitetsstatistik
- Udstyr udnyttelsesgrad (% tid udlånt)
- Gennemsnitlig tid fra anmodning til udlån (ikke-medlemmer)
- Forsinkede returneringer

**Privacy Note**: Alle rapporter skal bruge anonymiseret data uden personhenførbare oplysninger.

**Relaterede krav**: FR-015, FR-019
**Relaterede user stories**: US-002

---

### 8. Systemindstillinger

**Formål**: Konfigurer systemparametre

**Indstillinger:**
- **Generelle indstillinger**
  - Systemets navn
  - Kontaktinformation
  - Åbningstider
- **Email/SMS templates**
  - Valideringslink template
  - Returkvittering template
  - Påmindelse om returnering template (fremtidig)
- **Datasletning**
  - Vis datasletningslog
  - Kør manuel datasletning (kun administrator)
  - Konfigurer retention periode (standard: 3 måneder)
- **Integration**
  - Sygesikringsregister API konfiguration
  - Email service konfiguration
  - SMS service konfiguration

**Relaterede krav**: FR-016, FR-017, FR-018, FR-019, FR-020, FR-021, FR-026, FR-027, FR-028, FR-029

---

## Navigation og Layout

### Hovedmenu (Sidebar)

```
📊 Dashboard (overblik)
📦 Udstyr
   - Oversigt
   - Opret nyt
   - Tjeklister
👥 Brugere
   - Ansvarlige
   - Medlemmer
📋 Udlån
   - Aktive udlån
   - Historik
🔧 Skaderapporter
📈 Rapporter
⚙️ Indstillinger
```

### Top Bar
- Søgefelt (global søgning)
- Notifikationer (skader, forsinkede returneringer)
- Bruger menu (profil, log ud)

---

## Sikkerhed og Roller

### Administrator
- **Adgang til alt**
- Kan oprette/redigere/slette alt
- Kan se datasletningslog
- Kan køre manuel datasletning
- Kan manuelt lukke udlån

### Ansvarlig (uden admin rettigheder)
- **Begrænset adgang**
- Kan se udlånsoversigt (kun aktive)
- Kan se udstyrsoversigt
- Kan ikke slette eller ændre systemkritiske indstillinger
- Kan ikke administrere brugere

**Relaterede krav**: NFR-001, NFR-002, NFR-003

---

## Tekniske Krav til Dashboard

### Brugervenlighed
- Responsivt design (fungerer på tablet/desktop)
- Intuitivt interface
- Hurtig loading tid (< 2 sekunder)
- Keyboard shortcuts for hyppige handlinger

### Tilgængelighed
- WCAG 2.1 niveau AA
- Keyboard navigation
- Screen reader support

### Performance
- Lazy loading af lister
- Pagination (max 50 items per side)
- Caching af statistik

**Relaterede krav**: NFR-004, NFR-005

---

## Mockup Beskrivelser

### Dashboard Forside Mockup

```
┌─────────────────────────────────────────────────────────────┐
│ 📊 Dashboard                                    [Bruger] [⚙️] │
├─────────────────────────────────────────────────────────────┤
│                                                               │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌──────────┐   │
│  │ Aktive   │  │Forsinket │  │Beskadiget│  │  Ledigt  │   │
│  │  udlån   │  │  retur   │  │  udstyr  │  │  udstyr  │   │
│  │    12    │  │     3    │  │     2    │  │    45    │   │
│  └──────────┘  └──────────┘  └──────────┘  └──────────┘   │
│                                                               │
│  ┌────────────────────────────────────────────────────────┐ │
│  │ 📋 Seneste aktivitet                                   │ │
│  ├────────────────────────────────────────────────────────┤ │
│  │ 10:30 - Boremaskine BD-123 returneret                │ │
│  │ 09:15 - Rundsav RS-456 udlånt til medlem              │ │
│  │ 08:45 - Skruetrækker ST-789 udlånt (placering)       │ │
│  │ ...                                                    │ │
│  └────────────────────────────────────────────────────────┘ │
│                                                               │
│  ┌────────────────────────┐  ┌──────────────────────────┐  │
│  │ ⚠️ Påkrævet handling   │  │ 📊 Denne uge             │  │
│  ├────────────────────────┤  ├──────────────────────────┤  │
│  │ • 3 forsinkede retur   │  │ • 24 udlån               │  │
│  │ • 2 enheder til rep.   │  │ • 18 returneringer       │  │
│  └────────────────────────┘  │ • 2 skader rapporteret   │  │
│                               └──────────────────────────┘  │
└─────────────────────────────────────────────────────────────┘
```

---

## Fremtidige Udvidelser

**Could Have** (ikke i MVP):
- Push notifikationer ved forsinkede returneringer
- Automatisk email påmindelse før forventet returdato
- Booking/reservation system
- QR-kode print funktion for udstyr labels
- Export af rapporter til PDF/Excel
- Grafisk visualisering af statistik (charts)
- Dashboard widgets customization
- Bulk operationer (import/export af udstyr)

---

**Version**: 0.1
**Dato**: 2025-10-06
**Se også**: [KRAVSPECIFIKATION.md](KRAVSPECIFIKATION.md) | [README.md](README.md) | [FUNKTIONELLE-KRAV.md](FUNKTIONELLE-KRAV.md)
