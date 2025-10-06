# Process Flows - Orangemakers Udlånssystem

Dette dokument beskriver de primære process flows i systemet med Mermaid diagrammer.

**Se også:**
- [User Stories](USER-STORIES.md) for baggrund
- [Funktionelle Krav](FUNKTIONELLE-KRAV.md) for tekniske krav

---

## Flow 1: Ansvarlig Logger Ind

```mermaid
flowchart TD
    Start([Ansvarlig ankommer til terminal]) --> LoginScreen[System viser login muligheder]
    LoginScreen --> Choice{Vælg login metode}
    Choice -->|RFID| ScanRFID[Scanner RFID nøglebrik]
    Choice -->|Password| EnterCreds[Indtaster brugernavn/password]
    ScanRFID --> Validate[System validerer]
    EnterCreds --> Validate
    Validate --> Valid{Gyldig?}
    Valid -->|Nej| LoginScreen
    Valid -->|Ja| MainMenu[Vis hovedmenu]
    MainMenu --> MenuChoice{Vælg handling}
    MenuChoice -->|Udlån| LoanFlow([Gå til Udlånsflow])
    MenuChoice -->|Returnering| ReturnFlow([Gå til Returneringsflow])
    MenuChoice -->|Admin| AdminFlow([Gå til Admin])
```

**Relaterede krav:** FR-020, FR-021, FR-022, US-005

---

## Flow 2: Udlån til Medlem

```mermaid
flowchart TD
    Start([Ansvarlig vælger Udlån]) --> ScanEquip[Scanner/søg udstyr]
    ScanEquip --> CheckStatus{Status = ledig?}
    CheckStatus -->|Nej| Error[Vis fejl: Ikke tilgængeligt]
    CheckStatus -->|Ja| ShowEquip[Vis udstyr]
    ShowEquip --> ScanMember[Medlem scanner RFID]
    ScanMember --> ValidateMember[System validerer medlem]
    ValidateMember --> MemberValid{Gyldigt medlem?}
    MemberValid -->|Nej| MemberError[Vis fejl: Ugyldigt medlem]
    MemberValid -->|Ja| ShowMember[Vis medlemsinfo]
    ShowMember --> GiveInstr[Ansvarlig giver instruktion i brug]
    GiveInstr --> Checklist[Vis udleveringstjekliste]
    Checklist --> CheckItems[Ansvarlig gennemgår punkter]
    CheckItems --> AllDone{Alle punkter OK?}
    AllDone -->|Nej| CheckItems
    AllDone -->|Ja| Confirm1[Låntager: Bekræft modtaget instruktion]
    Confirm1 --> Confirm2[Låntager: Bekræft kompetence til brug]
    Confirm2 --> Confirm3[Ansvarlig: Bekræft givet instruktion]
    Confirm3 --> RegisterLoan[Registrer udlån med bekræftelser]
    RegisterLoan --> UpdateStatus[Opdater udstyr status til udlånt]
    UpdateStatus --> Confirm[Vis bekræftelse]
    Confirm --> End([Udlån gennemført])
```

**Relaterede krav:** FR-011, FR-022, FR-023, FR-030, FR-033, FR-044, FR-045, FR-046, FR-047, FR-048, US-006, US-009, US-013

**Ansvarsfraskrivelse:** Dette flow inkluderer juridisk vigtige bekræftelser der dokumenterer instruktion er givet og modtaget, hvilket fraskriver foreningen ansvar.

---

## Flow 3: Udlån til Ikke-medlem (Placering)

```mermaid
flowchart TD
    Start([Ansvarlig vælger Udlån]) --> ScanEquip[Scanner/søg udstyr]
    ScanEquip --> CheckStatus{Status = ledig?}
    CheckStatus -->|Nej| Error[Vis fejl: Ikke tilgængeligt]
    CheckStatus -->|Ja| ShowEquip[Vis udstyr]
    ShowEquip --> EnterInfo[Ansvarlig indtaster låntager info]
    EnterInfo --> ValidateAddress[Valider adresse via sygesikring]
    ValidateAddress --> AddressValid{Adresse gyldig?}
    AddressValid -->|Nej| AddressError[Vis fejl: Ugyldig adresse]
    AddressValid -->|Ja| SendLink[Send valideringslink email/SMS]
    SendLink --> WaitConfirm[Afventer låntagers bekræftelse]
    WaitConfirm --> Confirmed{Bekræftet?}
    Confirmed -->|Timeout| Cancelled[Annuller udlån]
    Confirmed -->|Ja| NotifyResponsible[Notificer ansvarlig]
    NotifyResponsible --> GiveInstr[Ansvarlig giver instruktion i brug]
    GiveInstr --> Checklist[Vis udleveringstjekliste]
    Checklist --> CheckItems[Ansvarlig gennemgår punkter]
    CheckItems --> AllDone{Alle punkter OK?}
    AllDone -->|Nej| CheckItems
    AllDone -->|Ja| Confirm1[Låntager: Bekræft modtaget instruktion]
    Confirm1 --> Confirm2[Låntager: Bekræft kompetence til brug]
    Confirm2 --> Confirm3[Ansvarlig: Bekræft givet instruktion]
    Confirm3 --> RegisterLoan[Registrer udlån med bekræftelser]
    RegisterLoan --> UpdateStatus[Opdater udstyr status til udlånt]
    UpdateStatus --> Confirm[Vis bekræftelse]
    Confirm --> End([Udlån gennemført])
```

**Relaterede krav:** FR-011, FR-024, FR-025, FR-026, FR-027, FR-028, FR-030, FR-033, FR-044, FR-045, FR-046, FR-047, FR-048, US-007, US-008, US-009, US-013

**Ansvarsfraskrivelse:** Dette flow inkluderer juridisk vigtige bekræftelser der dokumenterer instruktion er givet og modtaget, hvilket fraskriver foreningen ansvar.

---

## Flow 4: Returnering af Udstyr

```mermaid
flowchart TD
    Start([Ansvarlig vælger Returnering]) --> ScanEquip[Scanner/søg udstyr]
    ScanEquip --> FindLoan[Find aktivt udlån]
    FindLoan --> LoanFound{Udlån fundet?}
    LoanFound -->|Nej| Error[Vis fejl: Ikke udlånt]
    LoanFound -->|Ja| ShowInfo[Vis låneinfo]
    ShowInfo --> Checklist[Vis returneringstjekliste]
    Checklist --> CheckPoint[Gennemgå tjekpunkt]
    CheckPoint --> PointOK{OK?}
    PointOK -->|Ikke OK| AddNote[Tilføj note om problem]
    AddNote --> Damage[Marker skade]
    Damage --> MorePoints{Flere punkter?}
    PointOK -->|OK| MorePoints
    MorePoints -->|Ja| CheckPoint
    MorePoints -->|Nej| DamageCheck{Skader rapporteret?}
    DamageCheck -->|Ja| CreateReport[Opret skaderapport]
    CreateReport --> MarkDamaged[Marker udstyr som beskadiget]
    MarkDamaged --> ConfirmReturn[Bekræft returnering]
    DamageCheck -->|Nej| ConfirmReturn
    ConfirmReturn --> AutoProcess[System automatisk proces]
    AutoProcess --> SetReturned[Marker udlån som returneret]
    SetReturned --> DeleteData[SLET persondata]
    DeleteData --> KeepAnon[BEVAR anonymiseret data]
    KeepAnon --> LogDeletion[Log datasletning]
    LogDeletion --> UpdateEquip[Opdater udstyrsstatus]
    UpdateEquip --> ShowConfirm[Vis bekræftelse]
    ShowConfirm --> End([Returnering gennemført])
```

**Relaterede krav:** FR-012, FR-013, FR-017, FR-018, FR-031, FR-034, FR-037, FR-038, US-010, US-011

**Privacy Note:** Dette flow demonstrerer automatisk datasletning (NFR-002, FR-017)

---

## Flow 5: Reparation af Beskadiget Udstyr

```mermaid
flowchart TD
    Start([Administrator finder beskadiget udstyr]) --> ShowReports[Vis skaderapporter]
    ShowReports --> UpdateStatus[Markér under reparation]
    UpdateStatus --> AddNotes[Tilføj reparationsnote]
    AddNotes --> Repair[Reparation udføres]
    Repair --> Done{Repareret?}
    Done -->|Nej| Repair
    Done -->|Ja| MarkRepaired[Markér som repareret]
    MarkRepaired --> SetDate[Angiv reparationsdato]
    SetDate --> FinalNotes[Tilføj afsluttende noter]
    FinalNotes --> UpdateEquip[Opdater udstyr status til ledig]
    UpdateEquip --> End([Udstyr klar til udlån])
```

**Relaterede krav:** FR-040, FR-041, US-011

---

## Flow 6: Låntagers Bekræftelse (Email/SMS Link)

```mermaid
flowchart TD
    Start([Låntager modtager link]) --> OpenLink[Åbner link på enhed]
    OpenLink --> ValidToken{Token gyldigt?}
    ValidToken -->|Nej| Expired[Vis: Link udløbet]
    ValidToken -->|Ja| ShowInfo[Vis indsamlede oplysninger]
    ShowInfo --> Review[Gennemgå oplysninger]
    Review --> Correct{Korrekt?}
    Correct -->|Nej| Edit[Redigér oplysninger]
    Edit --> Review
    Correct -->|Ja| ShowTerms[Vis lånevilkår]
    ShowTerms --> Accept{Acceptér?}
    Accept -->|Nej| Decline[Afvis udlån]
    Accept -->|Ja| Confirm[Bekræft oplysninger]
    Confirm --> UpdateSystem[System opdaterer status]
    UpdateSystem --> Notify[Notificér ansvarlig]
    Notify --> End([Bekræftelse gennemført])
```

**Relaterede krav:** FR-028, FR-029, US-008

---

## Dataflow: Privacy-by-Design ved Returnering

```mermaid
flowchart LR
    subgraph "Under Udlån"
        A[Udlån Entity]
        A --> B[Persondata: Navn, kontakt, adresse]
        A --> C[Anonyme data: Type, måned/år]
    end

    subgraph "Ved Returnering"
        D[Returnering Process]
        D --> E[NULL persondata felter]
        D --> F[BEVAR anonyme data]
        D --> G[Log i DataSletningsLog]
    end

    subgraph "Efter Returnering"
        H[Udlån Entity]
        H --> I[Persondata: NULL]
        H --> J[Anonyme data: Bevaret]
        K[DataSletningsLog]
    end

    A --> D
    D --> H
    D --> K
```

**Relaterede krav:** NFR-002, FR-017, FR-018, US-002

---

**Version**: 0.1
**Dato**: 2025-10-06
**Se også**: [KRAVSPECIFIKATION.md](KRAVSPECIFIKATION.md) | [USER-STORIES.md](USER-STORIES.md) | [DATAMODEL.md](DATAMODEL.md)
