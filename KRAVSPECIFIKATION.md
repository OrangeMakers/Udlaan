# Kravspecifikation - Orangemakers Udlånssystem

Dette dokument giver en overordnet oversigt over kravspecifikationen. Detaljerede krav findes i separate dokumenter.

**📋 Dokumentation:**
- **[USER-STORIES.md](USER-STORIES.md)** - Detaljerede user stories (US-001 til US-012)
- **[FUNKTIONELLE-KRAV.md](FUNKTIONELLE-KRAV.md)** - Funktionelle og ikke-funktionelle krav (FR-001 til FR-041, NFR-001 til NFR-005)
- **[DATAMODEL.md](DATAMODEL.md)** - Database design og entiteter
- **[FLOWS.md](FLOWS.md)** - Process flows med Mermaid diagrammer
- **[CLAUDE.md](CLAUDE.md)** - Guide til AI coding agents

---

## Projektbeskrivelse

Et system til at håndtere udlån af udstyr i Orangemakers, hvor man kan registrere, administrere og tracke udlån af fysiske genstande med fokus på:

### 🔐 Privacy-First Design
- Persondata opbevares kun under aktivt udlån
- Automatisk sletning ved returnering
- Anonymiseret statistik bevares for analyse

### 🏷️ RFID Integration
- RFID login for ansvarlige
- RFID validering af medlemmer
- Terminal-baseret workflow

### ✅ Tjeklister og Kvalitetssikring
- Udleveringstjeklister sikrer korrekt udlevering
- Returneringstjeklister med skadekontrol
- Skaderapportering og reparationstracking

### 📧 Validering
- Medlemsvalidering via RFID
- Adressevalidering for ikke-medlemmer
- Email/SMS bekræftelse for ikke-medlemmer

---

## Roller og Aktører

### Primære roller
- **Ansvarlig for udlån**: Betroet medlem der har styr på formaliteter og godkender/administrerer udlån
- **Låntager**: Person der skal låne udstyr. Kan være:
  - Medlem af Orangemakers (valideres via RFID)
  - Person bosiddende på en placering (valideres via adresse + email/SMS)
- **Administrator**: System administrator der håndterer tjeklister og reparationer

---

## Krav Oversigt

### User Stories
**Total: 12 user stories** - [Se detaljer →](USER-STORIES.md)

| Kategori | Antal | User Stories |
|----------|-------|--------------|
| Identitet og Validering | 1 | US-001 |
| Privacy og Datasikkerhed | 2 | US-002, US-003 |
| Brugervenlighed | 1 | US-004 |
| Autentificering og Identifikation | 4 | US-005, US-006, US-007, US-008 |
| Tjeklister og Kvalitetssikring | 4 | US-009, US-010, US-011, US-012 |

### Funktionelle Krav
**Total: 41 funktionelle krav** - [Se detaljer →](FUNKTIONELLE-KRAV.md)

| Kategori | Krav |
|----------|------|
| Identitet og Autentificering | FR-001 til FR-005 |
| Udstyrshåndtering | FR-006 til FR-010 |
| Udlån og Returnering | FR-011 til FR-015 |
| Privacy og Datasletning | FR-016 til FR-019 |
| RFID og Hardware | FR-020 til FR-023 |
| Validering og Kommunikation | FR-024 til FR-029 |
| Tjeklister | FR-030 til FR-036 |
| Skadehåndtering | FR-037 til FR-041 |

### Ikke-funktionelle Krav
**Total: 5 ikke-funktionelle krav** - [Se detaljer →](FUNKTIONELLE-KRAV.md#ikke-funktionelle-krav)

| Kategori | Krav |
|----------|------|
| Sikkerhed | NFR-001, NFR-002, NFR-003 |
| Brugervenlighed | NFR-004, NFR-005 |

### Datamodel
**Total: 11 entiteter** - [Se detaljer →](DATAMODEL.md)

**Primære entiteter:**
- Udstyr
- Udlån (med privacy-by-design)
- Ansvarlig
- Medlem

**Tjekliste entiteter:**
- Tjekliste
- Tjekpunkt
- TjeklisteUdfyldelse
- TjekpunktResultat

**Support entiteter:**
- Skaderapport
- ValideringsLink
- DataSletningsLog

### Process Flows
**Total: 6 flows** - [Se diagrammer →](FLOWS.md)

1. **Ansvarlig Logger Ind** - RFID eller password login
2. **Udlån til Medlem** - RFID validering + udleveringstjekliste
3. **Udlån til Ikke-medlem** - Adressevalidering + email/SMS bekræftelse + udleveringstjekliste
4. **Returnering af Udstyr** - Returneringstjekliste + automatisk datasletning
5. **Reparation af Beskadiget Udstyr** - Skadehåndtering workflow
6. **Låntagers Bekræftelse** - Email/SMS link validering

---

## Udstyrstyper

Systemet skal kunne håndtere følgende typer udstyr:
- Skruemaskiner
- Rundsave
- Almindeligt værktøj
- Diverse udstyr

Hver udstyrstype skal kunne identificeres og trackes individuelt.

---

## Åbne Spørgsmål og Afklaringer

### Identitet og Privacy
1. Hvad er minimumsdata vi skal gemme om låntager? (navn, tlf, email?)
2. Hvordan implementeres automatisk sletning af persondata ved returnering?
3. Skal vi gemme anonymiseret historik for statistik?

### Udstyr
4. Hvordan skal udstyr "parres" med systemet? (QR-koder, NFC, manuelt ID?)
5. Skal hvert enkelt værktøj have unikt ID eller kan de grupperes?

### Teknisk
6. Hvilken RFID teknologi bruges? (125kHz, 13.56MHz NFC, etc.)
7. Skal der anskaffes nye RFID læsere eller er de eksisterende?
8. Hvilken service bruges til adresse/sygesikring validering?
9. Hvilken service bruges til email/SMS? (SendGrid, Twilio, etc.)
10. Hvordan skal identitetsvalidering foregå teknisk for henholdsvis medlemmer og placering?
11. Hvordan defineres og valideres en "placering"?
12. Skal systemet integrere med eksisterende medlemssystem?

### Features
13. Skal der være notifikationer ved overskredne låneperioder?
14. Skal der være booking/reservation af udstyr?
15. Hvad er maksimal låneperiode?
16. Er der forskellige regler/rettigheder for medlemmer vs. placering-lånere?
17. Skal tjeklister være ens for alle udstyr eller udstyrs-specifikke?
18. Hvem er ansvarlig for at reparere beskadiget udstyr?

---

## Prioritering (MoSCoW)

### Must Have (MVP)
- RFID login for ansvarlige
- RFID validering for medlemmer
- RFID tagging af udstyr (klistermærker)
- Registrering af udstyr
- Basis udleveringstjekliste
- Basis returneringstjekliste
- Udlåns transaktion
- Returnering med automatisk datasletning
- Skaderapportering

### Should Have
- Email/SMS validering for ikke-medlemmer
- Adressevalidering via sygesikring
- Historik over udlån
- Søgefunktion
- Avancerede tjekliste features

### Could Have
- Notifikationer ved overskredne låneperioder
- Booking/reservation system
- Reparations workflow med notifikationer
- Rapporter over hyppige skader

### Won't Have (denne version)
- Automatisk integration med reparatører
- Fysisk udskrivning af tjeklister
- Mobil app (PWA er tilstrækkeligt)

---

## Tekniske Overvejelser

### Platform
- **Anbefaling**: Progressive Web App (PWA)
- Tilgængelig på alle enheder
- Nem interaktion via browser
- Offline-capable hvis nødvendigt

### Hardware
- RFID læsere til terminal
- RFID klistermærker til udstyr
- Terminal (desktop/tablet)
- Printer til RFID labels (fremtidig - til udskrivning af klistermærker)

### Integration
- Sygesikringsregister eller lignende validering
- Email service (SendGrid, Mailgun, etc.)
- SMS service (Twilio, etc.)
- Evt. eksisterende medlemssystem

### Datalagring
- Database: PostgreSQL eller SQLite
- Backup strategi
- GDPR compliance

---

## Næste Skridt

1. ✅ Færdiggør kravspecifikation
2. ⏳ Afklar åbne spørgsmål med stakeholders
3. ⏳ Prioriter krav endeligt
4. ⏳ Design UI mockups for key flows
5. ⏳ Vælg teknologi stack
6. ⏳ Setup projekt og development environment
7. ⏳ Start implementation (MVP Phase 1)

---

## Dokumenthistorik

| Version | Dato | Ændringer | Forfatter |
|---------|------|-----------|-----------|
| 0.1 | 2025-10-06 | Initial kravspecifikation | Claude/CP |

---

**Version**: 0.1
**Dato**: 2025-10-06
**Status**: Draft - Til review

**Se også**: [README.md](README.md) | [CLAUDE.md](CLAUDE.md)
