# Funktionelle og Ikke-funktionelle Krav - Orangemakers Udlånssystem

Tekniske krav og specifikationer for systemet.

**Se også:**
- [User Stories](USER-STORIES.md) for at forstå "hvorfor"
- [Datamodel](DATAMODEL.md) for entiteter
- [Process Flows](FLOWS.md) for workflows

---

## Funktionelle Krav

### Identitet og Autentificering
- **FR-001**: System skal kunne registrere låntagers identitet
- **FR-002**: System skal kunne validere låntagers identitet
- **FR-003**: System skal kunne skelne mellem medlemmer og ikke-medlemmer
- **FR-004**: System skal kunne validere placering for ikke-medlemmer
- **FR-005**: Ansvarlig skal kunne se låntagers verifikationsstatus og type (medlem/placering)

**Relaterede user stories:** US-001, US-006, US-007
**Relaterede flows:** [Flow 2](FLOWS.md#flow-2-udlån-til-medlem), [Flow 3](FLOWS.md#flow-3-udlån-til-ikke-medlem-placering)

---

### Udstyrshåndtering
- **FR-006**: Hvert stykke udstyr skal have en unik identifikator
- **FR-007**: System skal kunne registrere forskellige typer udstyr (skruemaskine, rundsav, værktøj, etc.)
- **FR-008**: System skal kunne vise om udstyr er ledigt eller udlånt
- **FR-009**: Ansvarlig skal kunne tilføje nyt udstyr til systemet
- **FR-010**: Ansvarlig skal kunne scanne/identificere udstyr hurtigt

**Relaterede entiteter:** [Udstyr](DATAMODEL.md#udstyr)
**Relaterede flows:** [Flow 2](FLOWS.md#flow-2-udlån-til-medlem), [Flow 3](FLOWS.md#flow-3-udlån-til-ikke-medlem-placering)

---

### Udlån og Returnering
- **FR-011**: System skal kunne registrere et nyt udlån (koble udstyr + låntager)
- **FR-012**: System skal kunne registrere returnering af udstyr
- **FR-013**: Ved returnering skal persondata automatisk slettes
- **FR-014**: System skal vise oversigt over alle aktive udlån
- **FR-015**: System skal vise historik over tidligere udlån (anonymiseret)

**Relaterede user stories:** US-002, US-004
**Relaterede entiteter:** [Udlån](DATAMODEL.md#udlån)
**Relaterede flows:** [Flow 2](FLOWS.md#flow-2-udlån-til-medlem), [Flow 3](FLOWS.md#flow-3-udlån-til-ikke-medlem-placering), [Flow 4](FLOWS.md#flow-4-returnering-af-udstyr)

---

### Privacy og Datasletning
- **FR-016**: System skal kun gemme nødvendige personoplysninger
- **FR-017**: System skal automatisk fjerne persondata ved returnering
- **FR-018**: System skal logge hvornår persondata er slettet
- **FR-019**: System skal kunne generere anonymiseret statistik uden persondata

**Relaterede user stories:** US-002, US-003
**Relaterede entiteter:** [Udlån](DATAMODEL.md#udlån), [DataSletningsLog](DATAMODEL.md#datasletningslog)
**Relaterede flows:** [Flow 4](FLOWS.md#flow-4-returnering-af-udstyr)
**Se også:** [Privacy-by-Design Dataflow](FLOWS.md#dataflow-privacy-by-design-ved-returnering)

---

### RFID og Hardware
- **FR-020**: System skal kunne læse RFID nøglebrikker
- **FR-021**: Ansvarlige skal kunne logge ind med RFID eller brugernavn/adgangskode
- **FR-022**: Medlemmer skal kunne identificeres via RFID nøgle på terminal
- **FR-023**: System skal vise medlemsstatus ved RFID scanning

**Relaterede user stories:** US-005, US-006
**Relaterede entiteter:** [Ansvarlig](DATAMODEL.md#ansvarlig), [Medlem](DATAMODEL.md#medlem)
**Relaterede flows:** [Flow 1](FLOWS.md#flow-1-ansvarlig-logger-ind), [Flow 2](FLOWS.md#flow-2-udlån-til-medlem)

---

### Validering og Kommunikation
- **FR-024**: System skal kunne validere adresse/postnummer for ikke-medlemmer
- **FR-025**: System skal kunne integrere med sygesikringsregister eller lignende validering
- **FR-026**: System skal kunne sende valideringslink via email
- **FR-027**: System skal kunne sende valideringslink via SMS
- **FR-028**: Låntager skal kunne bekræfte oplysninger via link før udlån godkendes
- **FR-029**: Ansvarlig skal kunne se bekræftelsesstatus

**Relaterede user stories:** US-007, US-008
**Relaterede entiteter:** [ValideringsLink](DATAMODEL.md#valideringslink)
**Relaterede flows:** [Flow 3](FLOWS.md#flow-3-udlån-til-ikke-medlem-placering), [Flow 6](FLOWS.md#flow-6-låntagers-bekræftelse-emailsms-link)

---

### Tjeklister
- **FR-030**: Hvert udstyr skal have tilknyttet udleveringstjekliste
- **FR-031**: Hvert udstyr skal have tilknyttet returneringstjekliste
- **FR-032**: Tjeklister skal kunne oprettes/redigeres ved tilføjelse af udstyr
- **FR-033**: Udleveringstjekliste skal gennemføres før udlån kan registreres
- **FR-034**: Returneringstjekliste skal gennemføres før returnering kan godkendes
- **FR-035**: Hvert tjekpunkt skal kunne markeres (OK/Ikke OK/Noter)
- **FR-036**: Tjeklister skal kunne tilpasses udstyrstype

**Relaterede user stories:** US-009, US-010, US-012
**Relaterede entiteter:** [Tjekliste](DATAMODEL.md#tjekliste), [Tjekpunkt](DATAMODEL.md#tjekpunkt), [TjeklisteUdfyldelse](DATAMODEL.md#tjeklisteudfyldelse), [TjekpunktResultat](DATAMODEL.md#tjekpunktresultat)
**Relaterede flows:** [Flow 2](FLOWS.md#flow-2-udlån-til-medlem), [Flow 3](FLOWS.md#flow-3-udlån-til-ikke-medlem-placering), [Flow 4](FLOWS.md#flow-4-returnering-af-udstyr)

---

### Skadehåndtering
- **FR-037**: System skal kunne registrere skader fundet ved returnering
- **FR-038**: Beskadiget udstyr skal automatisk markeres som "ikke ledig"
- **FR-039**: Der skal kunne tilføjes detaljerede noter om skader
- **FR-040**: System skal gemme skadehistorik per udstyr
- **FR-041**: Beskadiget udstyr skal kunne markeres som repareret og gøres ledigt igen

**Relaterede user stories:** US-011
**Relaterede entiteter:** [Skaderapport](DATAMODEL.md#skaderapport), [Udstyr](DATAMODEL.md#udstyr)
**Relaterede flows:** [Flow 4](FLOWS.md#flow-4-returnering-af-udstyr), [Flow 5](FLOWS.md#flow-5-reparation-af-beskadiget-udstyr)

---

## Ikke-funktionelle Krav

### Sikkerhed
- **NFR-001**: Persondata skal håndteres i henhold til GDPR
- **NFR-002**: Persondata skal kun opbevares så længe låntager har udstyret (automatisk sletning ved returnering)
- **NFR-003**: System skal logge alle udlåns-transaktioner (uden persondata efter returnering)

**Relaterede user stories:** US-002, US-003
**Se også:** [Privacy-by-Design Princip](DATAMODEL.md#privacy-by-design-princip)

---

### Brugervenlighed
- **NFR-004**: System skal være tilgængeligt med nemmest mulig interaktion
- **NFR-005**: System skal være intuitivt og nemt at bruge

**Relaterede user stories:** US-004

---

## Krav Matrix

| Kategori | Antal Krav | Prioritet | Status |
|----------|-----------|-----------|--------|
| Identitet og Autentificering | 5 | Must Have | Draft |
| Udstyrshåndtering | 5 | Must Have | Draft |
| Udlån og Returnering | 5 | Must Have | Draft |
| Privacy og Datasletning | 4 | Must Have | Draft |
| RFID og Hardware | 4 | Must Have | Draft |
| Validering og Kommunikation | 6 | Should Have | Draft |
| Tjeklister | 7 | Must Have | Draft |
| Skadehåndtering | 5 | Should Have | Draft |
| Ikke-funktionelle | 5 | Must Have | Draft |

**Total**: 46 krav (41 funktionelle, 5 ikke-funktionelle)

---

## Krav Afhængigheder

### Privacy Chain (Kritisk)
```
FR-016 (Minimal data)
  → FR-011 (Registrer udlån)
  → FR-013 (Automatisk sletning)
  → FR-017 (Fjern persondata)
  → FR-018 (Log sletning)
```

### Udlån til Medlem Chain
```
FR-020 (Læs RFID)
  → FR-021 (Login)
  → FR-006 (Udstyr ID)
  → FR-022 (Medlem RFID)
  → FR-030 (Udleveringstjekliste)
  → FR-033 (Gennemfør tjekliste)
  → FR-011 (Registrer udlån)
```

### Udlån til Ikke-medlem Chain
```
FR-021 (Login)
  → FR-006 (Udstyr ID)
  → FR-024 (Valider adresse)
  → FR-026/FR-027 (Send link)
  → FR-028 (Bekræft)
  → FR-030 (Udleveringstjekliste)
  → FR-033 (Gennemfør tjekliste)
  → FR-011 (Registrer udlån)
```

### Returnerings Chain
```
FR-012 (Registrer returnering)
  → FR-031 (Returneringstjekliste)
  → FR-034 (Gennemfør tjekliste)
  → FR-037 (Registrer skader hvis relevante)
  → FR-013 (Automatisk sletning)
  → FR-017 (Fjern persondata)
  → FR-018 (Log sletning)
```

---

**Version**: 0.1
**Dato**: 2025-10-06
**Se også**: [KRAVSPECIFIKATION.md](KRAVSPECIFIKATION.md) | [USER-STORIES.md](USER-STORIES.md) | [DATAMODEL.md](DATAMODEL.md)
