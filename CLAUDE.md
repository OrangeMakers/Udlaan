# AI Coding Agent Guide - Orangemakers Udlånssystem

Dette dokument beskriver dokumentstrukturen for AI coding agents der skal arbejde med projektet.

## 📁 Dokumentstruktur

### Primære Specifikationsfiler

#### README.md
**Formål**: Projektets hovedindgang og index
**Indhold**:
- Projektbeskrivelse
- Links til alle dokumenter
- Quick overview af nøglefunktioner
- Status og version

**Hvornår at bruge**: Start her for at forstå projektet overordnet

---

#### KRAVSPECIFIKATION.md
**Formål**: Overordnet kravspecifikation og sammenhæng
**Indhold**:
- Projektbeskrivelse
- Roller og aktører
- Prioritering (MoSCoW)
- Åbne spørgsmål
- Udstyrstyper
- Tekniske overvejelser
- Links til detaljerede dokumenter

**Hvornår at bruge**: For at forstå projektets scope, prioriteter og sammenhæng

---

#### USER-STORIES.md
**Formål**: Detaljerede user stories grupperet efter kategori
**Indhold**:
- US-001 til US-012 med acceptkriterier
- Kategorier:
  - Identitet og Validering
  - Privacy og Datasikkerhed
  - Brugervenlighed
  - Autentificering og Identifikation
  - Tjeklister og Kvalitetssikring

**Hvornår at bruge**: Når du skal implementere features - hver user story beskriver "hvad" og "hvorfor"

---

#### FUNKTIONELLE-KRAV.md
**Formål**: Tekniske krav og specifikationer
**Indhold**:
- FR-001 til FR-041 (funktionelle krav)
- NFR-001 til NFR-005 (ikke-funktionelle krav)
- Kategorier:
  - Identitet og Autentificering
  - Udstyrshåndtering
  - Udlån og Returnering
  - Privacy og Datasletning
  - RFID og Hardware
  - Validering og Kommunikation
  - Tjeklister
  - Skadehåndtering

**Hvornår at bruge**: Når du skal implementere tekniske løsninger - beskriver "hvordan" på detaljeret niveau

---

#### DATAMODEL.md
**Formål**: Database design og datastruktur
**Indhold**:
- Entiteter og deres felter
- Relationer mellem entiteter
- Privacy-by-Design principper
- Datahåndtering ved sletning

**Entiteter**:
- Udstyr
- Udlån (med midlertidige persondata)
- Ansvarlig
- Medlem
- Tjekliste, Tjekpunkt, TjeklisteUdfyldelse, TjekpunktResultat
- Skaderapport
- ValideringsLink
- DataSletningsLog

**Hvornår at bruge**: Når du skal implementere database schema, queries eller data access layer

---

#### FLOWS.md
**Formål**: Visuelle process flows med Mermaid diagrammer
**Indhold**:
- Flow 1: Ansvarlig Logger Ind
- Flow 2: Udlån til Medlem
- Flow 3: Udlån til Ikke-medlem
- Flow 4: Returnering af Udstyr
- Flow 5: Reparation af Beskadiget Udstyr

**Format**: Mermaid flowcharts (GitHub-kompatible)

**Hvornår at bruge**: Når du skal forstå eller implementere workflows og brugerrejser

---

#### ADMIN-DASHBOARD.md
**Formål**: Admin dashboard funktionalitet og interface beskrivelse
**Indhold**:
- Dashboard sektioner (Overblik, Udstyrshåndtering, Tjeklister, Brugere, Udlånsoversigt, Skaderapporter, Rapporter, Systemindstillinger)
- Funktioner per sektion
- Navigation og layout
- Sikkerhed og roller
- Mockup beskrivelser

**Hvornår at bruge**: Når du skal implementere admin interface eller forstå administratorens workflow

---

#### DRAFT.md
**Formål**: Arbejdsdokument med løse ideer og noter
**Status**: IKKE endelig specifikation
**Indhold**: Rå noter og ideer under udvikling

**Hvornår at bruge**: IKKE til implementation - kun som reference til diskussion. Alt væsentligt er flyttet til de andre dokumenter.

---

## 🔄 Arbejdsflow for AI Agent

### 1. Start et nyt feature
```
1. Læs README.md for at forstå projektet
2. Find relevant user story i USER-STORIES.md
3. Tjek funktionelle krav i FUNKTIONELLE-KRAV.md
4. Tjek datamodel i DATAMODEL.md
5. Se flow diagram i FLOWS.md
6. Implementer feature
```

### 2. Forstå en eksisterende feature
```
1. Find user story i USER-STORIES.md
2. Se tilhørende flow i FLOWS.md
3. Tjek funktionelle krav i FUNKTIONELLE-KRAV.md
4. Se datamodel i DATAMODEL.md
```

### 3. Opdater specifikation
```
1. Diskuter ændringer i DRAFT.md først
2. Når enighed, opdater relevante spec-filer:
   - USER-STORIES.md
   - FUNKTIONELLE-KRAV.md
   - DATAMODEL.md
   - FLOWS.md
3. Opdater KRAVSPECIFIKATION.md hvis scope/prioritet ændres
4. Opdater README.md hvis nødvendigt
```

---

## 🎯 Nøgleprincipper

### Privacy-First
- Persondata opbevares KUN på Udlån entity
- Automatisk NULL'es ved returnering
- Anonymiseret data bevares for statistik
- Se DATAMODEL.md for detaljer

### RFID Integration
- Ansvarlig: RFID eller password login
- Medlemmer: RFID validering
- Se FLOWS.md for login flows

### Tjeklister
- Hvert udstyr har udleverings- og returneringstjekliste
- Tjeklister skal gennemføres før udlån/returnering godkendes
- Se DATAMODEL.md for tjekliste struktur

---

## 📋 Dokument Cross-Reference

| Spørgsmål | Dokument |
|-----------|----------|
| Hvad skal systemet kunne? | USER-STORIES.md |
| Hvordan skal det implementeres? | FUNKTIONELLE-KRAV.md |
| Hvilke data skal gemmes? | DATAMODEL.md |
| Hvordan fungerer processen? | FLOWS.md |
| Hvad skal admin dashboard have? | ADMIN-DASHBOARD.md |
| Hvad er prioriteten? | KRAVSPECIFIKATION.md |
| Hvad er project status? | README.md |

---

## 🔗 Referencer mellem Dokumenter

### USER-STORIES.md referencer
- Links til FLOWS.md for at se visuelt flow
- Links til FUNKTIONELLE-KRAV.md for tekniske detaljer
- Links til DATAMODEL.md for data struktur

### FUNKTIONELLE-KRAV.md referencer
- Links til USER-STORIES.md for at forstå "hvorfor"
- Links til DATAMODEL.md for entiteter

### FLOWS.md referencer
- Links til USER-STORIES.md for baggrund
- Links til FUNKTIONELLE-KRAV.md for krav

---

## ⚠️ Vigtige Noter for AI Agents

1. **DRAFT.md er IKKE source of truth** - Brug kun som reference
2. **Privacy er kritisk** - Følg altid privacy-by-design princippet
3. **Alle flows skal have tjeklister** - Glem dem ikke i implementation
4. **RFID er hardware-afhængig** - Husk abstraktion/interface layer
5. **Validering kan fejle** - Implementer graceful fallbacks

---

## 📝 Vedligeholdelse

Når du opdaterer specifikationen:

1. ✅ Opdater den relevante fil (USER-STORIES, FUNKTIONELLE-KRAV, etc.)
2. ✅ Opdater cross-references hvis nødvendigt
3. ✅ Opdater KRAVSPECIFIKATION.md hvis scope/prioritet ændres
4. ✅ Opdater README.md hvis det påvirker overordnet beskrivelse
5. ✅ Opdater version og dato i relevante filer

---

**Version**: 0.1
**Dato**: 2025-10-06