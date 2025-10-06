# User Stories - Orangemakers Udlånssystem

Detaljerede user stories for alle funktioner i systemet.

**Se også:**
- [Process Flows](FLOWS.md) for visuelle workflows
- [Funktionelle Krav](FUNKTIONELLE-KRAV.md) for tekniske detaljer
- [Datamodel](DATAMODEL.md) for datastruktur

---

## Identitet og Validering

### US-001: Validering af låntagers identitet
- **Som** ansvarlig
- **Vil jeg** kunne validere at den der låner udstyret er den de udgiver sig for at være
- **Så** jeg kan sikre ansvarlig udlån og spore hvem der har udstyret

**Acceptkriterier:**
- Låntager skal kunne identificere sig (fx ID, medarbejdernummer, etc.)
- System skal kunne verificere identitet mod et register
- Ansvarlig skal kunne se og godkende låntagers identitet før udlån

**Relaterede krav:** FR-001, FR-002, FR-005
**Relaterede flows:** [Flow 2: Udlån til Medlem](FLOWS.md#flow-2-udlån-til-medlem), [Flow 3: Udlån til Ikke-medlem](FLOWS.md#flow-3-udlån-til-ikke-medlem-placering)

---

## Privacy og Datasikkerhed

### US-002: Automatisk sletning af persondata
- **Som** system administrator
- **Vil jeg** at persondata automatisk slettes når udstyr returneres
- **Så** vi kun opbevarer persondata så længe det er absolut nødvendigt (GDPR compliance)

**Acceptkriterier:**
- Ved returnering af udstyr skal persondata fjernes fra systemet
- Anonymiseret data (uden personhenførbare oplysninger) må gerne bevares til statistik
- Systemet skal logge hvornår data er slettet

**Relaterede krav:** NFR-002, FR-017, FR-018
**Relaterede flows:** [Flow 4: Returnering af Udstyr](FLOWS.md#flow-4-returnering-af-udstyr)

---

### US-003: Minimal dataindsamling
- **Som** låntager
- **Vil jeg** kun afgive de absolut nødvendige personoplysninger
- **Så** jeg føler mig tryg ved at låne udstyr

**Acceptkriterier:**
- Systemet skal kun bede om minimumsdata nødvendigt for udlån
- Låntager skal informeres om hvad data bruges til
- Låntager skal informeres om hvornår data slettes

**Relaterede krav:** NFR-002, FR-016
**Relaterede flows:** [Flow 3: Udlån til Ikke-medlem](FLOWS.md#flow-3-udlån-til-ikke-medlem-placering)

---

## Brugervenlighed

### US-004: Hurtig og nem udlånsproces
- **Som** ansvarlig
- **Vil jeg** kunne registrere et udlån med få klik/trin
- **Så** processen ikke tager lang tid og bliver en barriere

**Acceptkriterier:**
- Udlån skal kunne registreres på max 1-2 minutter
- Interface skal være intuitivt og selvforklarende
- Systemet skal være tilgængeligt på mobile enheder

**Relaterede krav:** NFR-004, NFR-005
**Relaterede flows:** [Flow 2: Udlån til Medlem](FLOWS.md#flow-2-udlån-til-medlem)

---

## Autentificering og Identifikation

### US-005: RFID login for ansvarlig
- **Som** ansvarlig for udlån
- **Vil jeg** kunne identificere mig selv med RFID nøglebrik eller brugernavn/adgangskode
- **Så** jeg hurtigt kan logge ind og starte et udlån eller returnering

**Acceptkriterier:**
- System skal understøtte login med RFID nøglebrik
- System skal også understøtte login med brugernavn/adgangskode som alternativ
- Login skal være hurtigt (under 2 sekunder)

**Relaterede krav:** FR-020, FR-021
**Relaterede flows:** [Flow 1: Ansvarlig Logger Ind](FLOWS.md#flow-1-ansvarlig-logger-ind)

---

### US-006: RFID validering af medlemmer
- **Som** ansvarlig
- **Vil jeg** kunne validere medlemmer via deres RFID nøgle på en terminal
- **Så** jeg nemt kan bekræfte de er gyldige medlemmer

**Acceptkriterier:**
- Medlemmer skal kunne identificeres ved at scanne deres RFID
- System skal vise medlemsstatus (aktiv/inaktiv)
- System skal vise medlemsoplysninger til ansvarlig

**Relaterede krav:** FR-022, FR-023
**Relaterede flows:** [Flow 2: Udlån til Medlem](FLOWS.md#flow-2-udlån-til-medlem)

---

### US-007: Adressevalidering for ikke-medlemmer
- **Som** ansvarlig
- **Vil jeg** kunne validere ikke-medlemmers adresse via sygesikring eller lignende
- **Så** jeg kan bekræfte de bor på en godkendt placering

**Acceptkriterier:**
- System skal kunne modtage adresse/postnummer
- System skal validere via sygesikringsregister eller lignende
- Valideringsstatus skal vises tydeligt

**Relaterede krav:** FR-024, FR-025
**Relaterede flows:** [Flow 3: Udlån til Ikke-medlem](FLOWS.md#flow-3-udlån-til-ikke-medlem-placering)

---

### US-008: Email/SMS bekræftelse til låntager
- **Som** låntager (ikke-medlem)
- **Vil jeg** modtage et link på email eller SMS
- **Så** jeg kan bekræfte mine oplysninger før udlånet godkendes

**Acceptkriterier:**
- System skal sende valideringslink til email eller SMS
- Låntager skal kunne åbne link og bekræfte/udfylde data
- Ansvarlig skal kunne se når låntager har bekræftet
- Udlån kan først gennemføres når låntager har bekræftet

**Relaterede krav:** FR-026, FR-027, FR-028, FR-029
**Relaterede flows:** [Flow 3: Udlån til Ikke-medlem](FLOWS.md#flow-3-udlån-til-ikke-medlem-placering), [Flow 6: Låntagers Bekræftelse](FLOWS.md#flow-6-låntagers-bekræftelse-emailsms-link)

---

## Tjeklister og Kvalitetssikring

### US-009: Udleveringstjekliste
- **Som** ansvarlig
- **Vil jeg** følge en tjekliste ved udlevering af udstyr
- **Så** jeg sikrer alle regler er gennemgået og udstyret udleveres korrekt

**Acceptkriterier:**
- System skal vise udleveringstjekliste for det specifikke udstyr
- Ansvarlig skal kunne afkrydse hvert punkt
- Tjekliste skal inkludere gennemgang af regler
- Udlån kan først registreres når tjekliste er gennemført

**Relaterede krav:** FR-030, FR-033
**Relaterede flows:** [Flow 2: Udlån til Medlem](FLOWS.md#flow-2-udlån-til-medlem), [Flow 3: Udlån til Ikke-medlem](FLOWS.md#flow-3-udlån-til-ikke-medlem-placering)

---

### US-010: Returneringstjekliste med skadekontrol
- **Som** ansvarlig
- **Vil jeg** følge en interaktiv tjekliste når udstyr returneres
- **Så** jeg kan verificere udstyret virker og ikke er beskadiget

**Acceptkriterier:**
- System skal vise returneringstjekliste for det specifikke udstyr
- Hvert punkt skal kunne markeres (OK/Ikke OK)
- Ved skader skal der kunne tilføjes noter
- Returnering kan først godkendes når tjekliste er gennemført

**Relaterede krav:** FR-031, FR-034, FR-035
**Relaterede flows:** [Flow 4: Returnering af Udstyr](FLOWS.md#flow-4-returnering-af-udstyr)

---

### US-011: Skaderapportering
- **Som** ansvarlig
- **Vil jeg** kunne rapportere skader på returneret udstyr
- **Så** vi kan holde styr på udstyrets tilstand og reparationsbehov

**Acceptkriterier:**
- System skal tillade detaljerede noter om skader
- Beskadiget udstyr skal markeres og ikke kunne udlånes før reparation
- Der skal gemmes historik over skader på udstyret

**Relaterede krav:** FR-037, FR-038, FR-039, FR-040
**Relaterede flows:** [Flow 4: Returnering af Udstyr](FLOWS.md#flow-4-returnering-af-udstyr), [Flow 5: Reparation af Beskadiget Udstyr](FLOWS.md#flow-5-reparation-af-beskadiget-udstyr)

---

### US-012: Opret tjekliste ved nyt udstyr
- **Som** administrator
- **Vil jeg** definere tjeklister når jeg tilføjer nyt udstyr
- **Så** der altid er relevante tjeklister til det specifikke udstyr

**Acceptkriterier:**
- Ved tilføjelse af udstyr skal der kunne oprettes/vælges tjeklister
- Både udleverings- og returneringstjekliste skal kunne defineres
- Tjeklister skal kunne tilpasses udstyrstype

**Relaterede krav:** FR-032, FR-036
**Relaterede flows:** N/A (admin funktion)

---

### US-013: Ansvarsfraskrivelse gennem instruktionsbekræftelse
- **Som** forening (Orangemakers)
- **Vil jeg** dokumentere at instruktion er givet og modtaget
- **Så** vi fraskriver ansvar ved skader forårsaget af forkert brug af udstyret

**Acceptkriterier:**
- Låntager skal eksplicit bekræfte at have modtaget instruktion
- Låntager skal bekræfte at have kompetence til at bruge udstyret
- Ansvarlig skal bekræfte at have givet fyldestgørende instruktion
- Alle bekræftelser skal timestampes
- Udlån kan ikke gennemføres før alle bekræftelser er givet
- System skal gemme bekræftelser som dokumentation

**Juridisk rationale:**
- Dokumenterer foreningens opfyldelse af undervisningspligt
- Dokumenterer låntagers accept af ansvar
- Fraskriver foreningen ansvar ved personskade eller materielskade

**Relaterede krav:** FR-044, FR-045, FR-046, FR-047, FR-048
**Relaterede flows:** [Flow 2: Udlån til Medlem](FLOWS.md#flow-2-udlån-til-medlem), [Flow 3: Udlån til Ikke-medlem](FLOWS.md#flow-3-udlån-til-ikke-medlem-placering)

---

## User Story Mapping

### Core Journey: Udlån og Returnering
```
Login (US-005)
  → Udlån (US-004, US-006/US-007/US-008, US-009, US-013)
  → Returnering (US-010, US-011)
  → Privacy (US-002)
```

### Setup Journey: Administrator
```
Opret udstyr
  → Definer tjeklister (US-012)
```

### Legal Protection Journey
```
Instruktion gives (Ansvarlig)
  → Bekræftelse modtaget (Låntager)
  → Bekræftelse kompetence (Låntager)
  → Bekræftelse givet instruktion (Ansvarlig)
  → Dokumentation gemmes (US-013)
```

---

**Version**: 0.1
**Dato**: 2025-10-06
**Se også**: [KRAVSPECIFIKATION.md](KRAVSPECIFIKATION.md) | [FLOWS.md](FLOWS.md) | [FUNKTIONELLE-KRAV.md](FUNKTIONELLE-KRAV.md)
