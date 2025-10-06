# Draft

## Flow

Ansvarlig for udlån:
Identificere sig overfor systemet (Vi har RFID nøglebrikker, brugernavn/adgangskode) vi kan bruge som identifikation af kendte personer
Vælge om det er et udlån eller en returnering

Ved returnering - følg et flow hvor vi interaktiv tjekker af at udstyret virker og ikke har skader
Tjek via et tjek skema som skal være på udstyret (Skal laves ved oprettelse af udstyret i databasen)

Ved udlån
Valider personen der skal låne (Medlemmer har en nøgle RFID vi kan validere på en terminal vi kan lave)
Hvis ikke medlem skal vi validere adressen / post nummer via sygesikring eller ligende og registrere personen via email eller telefon nummer
Personen får et link de skal udfylde enten på mail eller sms hvor vi skal validere det passer så vi kan godkende udlån
Udlåner ansvarlig oplyser regler og tjekker af (manuelt via chekcliste at udlevering er overholdt)

Tjeklisten følger udstyret
H