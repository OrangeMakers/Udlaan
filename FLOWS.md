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
    Start([Ansvarlig vælger Udlån]) --> ScanMember[Medlem scanner RFID]
    ScanMember --> ValidateMember[System validerer medlem]
    ValidateMember --> MemberValid{Gyldigt medlem?}
    MemberValid -->|Nej| MemberError[Vis fejl: Ugyldigt medlem]
    MemberValid -->|Ja| ShowMember[Vis medlemsinfo]
    ShowMember --> ScanEquip[Scanner RFID tag på udstyr]
    ScanEquip --> CheckStatus{Status?}
    CheckStatus -->|Ledig| ShowEquip[Vis udstyr]
    CheckStatus -->|Udlånt| ShowLoanInfo[Vis: Udlånt til X, forventet retur Y]
    CheckStatus -->|Beskadiget| ShowDamage[Vis skaderapport]
    ShowLoanInfo --> HasEquip{Har udstyr i hånden?}
    HasEquip -->|Ja| OfferReturn[Tilbyd: Registrer returnering nu]
    OfferReturn --> AcceptReturn{Registrer retur?}
    AcceptReturn -->|Ja| ReturnFlow([Gå til Returneringsflow])
    AcceptReturn -->|Nej| End1([Afslut - kan ikke udlånes])
    HasEquip -->|Nej| End1
    ShowDamage --> CheckRepair{Skade udbedret?}
    CheckRepair -->|Nej| End1
    CheckRepair -->|Ja| MarkRepaired[Marker skade som udbedret]
    MarkRepaired --> ShowEquip
    ShowEquip --> ShowPeriod[Vis standard/maks låneperiode]
    ShowPeriod --> SelectPeriod[Vælg låneperiode op til maks]
    SelectPeriod --> GiveInstr[Ansvarlig giver instruktion i brug]
    GiveInstr --> Checklist[Vis udleveringstjekliste]
    Checklist --> CheckItems[Ansvarlig gennemgår punkter]
    CheckItems --> AllDone{Alle punkter OK?}
    AllDone -->|Nej| CheckItems
    AllDone -->|Ja| Confirm1[Låntager: Bekræft modtaget instruktion]
    Confirm1 --> Confirm2[Låntager: Bekræft kompetence til brug]
    Confirm2 --> Confirm3[Ansvarlig: Bekræft givet instruktion]
    Confirm3 --> RegisterLoan[Registrer udlån med bekræftelser]
    RegisterLoan --> UpdateStatus[Opdater udstyr status til udlånt]
    UpdateStatus --> MoreItems{Låne flere ting?}
    MoreItems -->|Ja| ScanEquip[Scanner RFID tag på næste udstyr]
    MoreItems -->|Nej| Confirm[Vis bekræftelse]
    Confirm --> End([Udlån gennemført])
```

**Relaterede krav:** FR-010, FR-011, FR-022, FR-023, FR-032, FR-035, FR-044, FR-045, FR-046, FR-047, FR-048, FR-052, FR-053, FR-054, US-006, US-009, US-013

**Ansvarsfraskrivelse:** Dette flow inkluderer juridisk vigtige bekræftelser der dokumenterer instruktion er givet og modtaget, hvilket fraskriver foreningen ansvar.

---

## Flow 3: Udlån til Ikke-medlem (Placering)

```mermaid
flowchart TD
    Start([Ansvarlig vælger Udlån]) --> AskContact[Spørg låntager om telefon eller email]
    AskContact --> EnterContact[Indtast telefon/email]
    EnterContact --> CheckKnown{Kendt i systemet?}
    CheckKnown -->|Ja| SendNewLink[Send nyt oprettelseslink]
    CheckKnown -->|Nej| SendLink[Send oprettelseslink email/SMS]
    SendNewLink --> WaitInfo[Afventer låntager udfylder]
    SendLink --> WaitInfo
    WaitInfo --> BorrowerFills([Låntager: Udfylder info via link])
    BorrowerFills --> ValidateAddress[System: Valider adresse via sygesikring]
    ValidateAddress --> AddressValid{Adresse gyldig?}
    AddressValid -->|Nej| ShowError[Vis fejl til låntager]
    AddressValid -->|Ja| BorrowerSubmit[Låntager: Indsend oplysninger]
    BorrowerSubmit --> NotifyScreen[Vis på skærm til ansvarlig]
    NotifyScreen --> ReviewInfo[Ansvarlig: Gennemse oplysninger]
    ReviewInfo --> ApproveInfo{Godkend info?}
    ApproveInfo -->|Nej| RejectInfo[Afvis - bed om korrektioner]
    RejectInfo --> WaitInfo
    ApproveInfo -->|Ja| ShowBorrower[Vis godkendte låntager info]
    ShowBorrower --> ScanEquip[Scanner RFID tag på udstyr]
    ScanEquip --> CheckStatus{Status?}
    CheckStatus -->|Ledig| ShowEquip[Vis udstyr]
    CheckStatus -->|Udlånt| ShowLoanInfo[Vis: Udlånt til X, forventet retur Y]
    CheckStatus -->|Beskadiget| ShowDamage[Vis skaderapport]
    ShowLoanInfo --> HasEquip{Har udstyr i hånden?}
    HasEquip -->|Ja| OfferReturn[Tilbyd: Registrer returnering nu]
    OfferReturn --> AcceptReturn{Registrer retur?}
    AcceptReturn -->|Ja| ReturnFlow([Gå til Returneringsflow])
    AcceptReturn -->|Nej| End1([Afslut - kan ikke udlånes])
    HasEquip -->|Nej| End1
    ShowDamage --> CheckRepair{Skade udbedret?}
    CheckRepair -->|Nej| End1
    CheckRepair -->|Ja| MarkRepaired[Marker skade som udbedret]
    MarkRepaired --> ShowEquip
    ShowEquip --> ShowPeriod[Vis standard/maks låneperiode]
    ShowPeriod --> SelectPeriod[Vælg låneperiode op til maks]
    SelectPeriod --> GiveInstr[Ansvarlig giver instruktion i brug]
    GiveInstr --> Checklist[Vis udleveringstjekliste]
    Checklist --> CheckItems[Ansvarlig gennemgår punkter]
    CheckItems --> AllDone{Alle punkter OK?}
    AllDone -->|Nej| CheckItems
    AllDone -->|Ja| Confirm1[Låntager: Bekræft modtaget instruktion]
    Confirm1 --> Confirm2[Låntager: Bekræft kompetence til brug]
    Confirm2 --> Confirm3[Ansvarlig: Bekræft givet instruktion]
    Confirm3 --> RegisterLoan[Registrer udlån med bekræftelser]
    RegisterLoan --> UpdateStatus[Opdater udstyr status til udlånt]
    UpdateStatus --> MoreItems{Låne flere ting?}
    MoreItems -->|Ja| ScanEquip[Scanner RFID tag på næste udstyr]
    MoreItems -->|Nej| Confirm[Vis bekræftelse]
    Confirm --> End([Udlån gennemført])
```

**Relaterede krav:** FR-010, FR-011, FR-026, FR-027, FR-028, FR-029, FR-030, FR-031, FR-032, FR-035, FR-044, FR-045, FR-046, FR-047, FR-048, FR-052, FR-053, FR-054, FR-055, FR-056, US-007, US-008, US-009, US-013

**Ansvarsfraskrivelse:** Dette flow inkluderer juridisk vigtige bekræftelser der dokumenterer instruktion er givet og modtaget, hvilket fraskriver foreningen ansvar.

**Låntager workflow:** Låntager modtager link, udfylder selv alle oplysninger inkl. adresse. System validerer adresse automatisk. Ansvarlig gennemser og godkender oplysninger på skærm før udlån gennemføres.

---

## Flow 4: Returnering af Udstyr

```mermaid
flowchart TD
    Start([Ansvarlig vælger Returnering]) --> ScanEquip[Scanner RFID tag på udstyr]
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
    SetReturned --> SetScheduledDeletion[Sæt planlagt sletningsdato = nu + 3 måneder]
    SetScheduledDeletion --> SendReceipt[Send returkvittering til låntager]
    SendReceipt --> UpdateEquip[Opdater udstyrsstatus]
    UpdateEquip --> ShowConfirm[Vis bekræftelse]
    ShowConfirm --> End([Returnering gennemført])
```

**Relaterede krav:** FR-010, FR-012, FR-013, FR-017, FR-020, FR-033, FR-036, FR-039, FR-040, FR-050, FR-054, US-010, US-011

**Privacy Note:** Ved returnering sættes planlagt sletningsdato til 3 måneder frem. Persondata bevares midlertidigt for håndtering af tvister. Automatisk job sletter persondata når sletningsdato nås (FR-017, FR-020, FR-021)

**Receipt Note:** Returkvittering sendes til låntager som dokumentation for returnering

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

## Flow 6: Låntagers Udfyldelse (Email/SMS Link)

```mermaid
flowchart TD
    Start([Låntager modtager oprettelseslink]) --> OpenLink[Åbner link på enhed]
    OpenLink --> ValidToken{Token gyldigt?}
    ValidToken -->|Nej| Expired[Vis: Link udløbet]
    ValidToken -->|Ja| ShowForm[Vis formular]
    ShowForm --> FillInfo[Udfyld: Navn, adresse, kontaktinfo]
    FillInfo --> ValidateAddr[System validerer adresse]
    ValidateAddr --> AddrValid{Adresse gyldig?}
    AddrValid -->|Nej| ShowAddrError[Vis fejl: Ugyldig adresse]
    ShowAddrError --> FillInfo
    AddrValid -->|Ja| ShowTerms[Vis lånevilkår]
    ShowTerms --> ReviewAll[Gennemgå alt]
    ReviewAll --> Correct{Alt korrekt?}
    Correct -->|Nej| FillInfo
    Correct -->|Ja| AcceptTerms[Acceptér vilkår]
    AcceptTerms --> Submit[Indsend oplysninger]
    Submit --> NotifyScreen[Vis på ansvarlig's skærm]
    NotifyScreen --> WaitApproval[Afventer ansvarlig's godkendelse]
    WaitApproval --> End([Info klar til gennemsyn])
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
