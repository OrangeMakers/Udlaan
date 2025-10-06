# Orangemakers Udlånssystem

Et system til at håndtere udlån af udstyr i Orangemakers, hvor man kan registrere, administrere og tracke udlån af fysiske genstande med fokus på privacy og nem brugeroplevelse.

## 📋 Dokumentation

### Kravspecifikation
- **[KRAVSPECIFIKATION.md](KRAVSPECIFIKATION.md)** - Overordnet kravspecifikation med projektbeskrivelse, roller og prioritering
- **[USER-STORIES.md](USER-STORIES.md)** - Detaljerede user stories for alle funktioner
- **[FUNKTIONELLE-KRAV.md](FUNKTIONELLE-KRAV.md)** - Funktionelle og ikke-funktionelle krav
- **[DATAMODEL.md](DATAMODEL.md)** - Database design og datamodel
- **[FLOWS.md](FLOWS.md)** - Process flows med Mermaid diagrammer
- **[ADMIN-DASHBOARD.md](ADMIN-DASHBOARD.md)** - Admin dashboard funktionalitet og interface beskrivelse

### Arbejdsdokumenter
- **[DRAFT.md](DRAFT.md)** - Arbejdsdokument med ideer og noter (ikke endelig spec)

### AI Optimering
- **[CLAUDE.md](CLAUDE.md)** - Vejledning til AI coding agents om dokumentstrukturen

## 🎯 Projekt Status

**Version**: 0.1
**Dato**: 2025-10-06
**Status**: Draft - Kravspecifikation under udvikling

## 🔑 Nøglefunktioner

### Privacy-First Design
- Persondata opbevares kun under aktivt udlån
- Automatisk sletning ved returnering
- Anonymiseret statistik bevares

### RFID Integration
- RFID login for ansvarlige
- RFID validering af medlemmer
- Terminal-baseret workflow

### Tjeklister og Kvalitetssikring
- Udleveringstjeklister
- Returneringstjeklister
- Skaderapportering

### Validering
- Medlemsvalidering via RFID
- Adressevalidering for ikke-medlemmer
- Email/SMS bekræftelse

## 📊 Quick Links

- [Se alle user stories →](USER-STORIES.md)
- [Se process flows →](FLOWS.md)
- [Se datamodel →](DATAMODEL.md)
- [Se funktionelle krav →](FUNKTIONELLE-KRAV.md)
- [Se admin dashboard →](ADMIN-DASHBOARD.md)

## 👥 Roller

- **Ansvarlig for udlån**: Betroet medlem der håndterer udlån/returneringer
- **Låntager**: Medlem eller person bosiddende på godkendt placering
- **Administrator**: System administrator

## 🔧 Udstyr Typer

Systemet håndterer:
- Skruemaskiner
- Rundsave
- Almindeligt værktøj
- Diverse udstyr

---

**Se [CLAUDE.md](CLAUDE.md) for information til AI coding agents**
