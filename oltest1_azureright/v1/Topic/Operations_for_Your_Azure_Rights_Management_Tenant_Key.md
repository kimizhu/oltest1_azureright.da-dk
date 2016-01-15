---
description: na
keywords: na
title: Operations for Your Azure Rights Management Tenant Key
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1284d0ee-0a72-45ba-a64c-3dcb25846c3d
---
# Operationer for Azure Rights Management lejer n&#248;glen
Afhængigt af din lejer nøgle topologi (Microsoft-styrede eller debitor-administreret) har du forskellige niveauer af kontrol og ansvar for Microsoft Azure Rights Management (Azure RMS) lejer nøglen, efter at den gennemføres.

Når du administrerer din egen nøgle lejer, kaldes dette ofte som du sætter din egen nøgle (BYOK). Yderligere oplysninger om denne situation, og hvordan du vælger mellem de to lejer nøgle topologier, se [Planlægning og implementering af Azure Rights Management lejer nøglen](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md).

Følgende tabel identificerer, hvilke handlinger du kan gøre, afhængigt af den topologi, som du har valgt til din Azure RMS lejer nøgle.

|Livscyklus operation|Microsoft-styrede (standard)|Kunde-styrede (BYOK)|
|------------------------|--------------------------------|------------------------|
|Tilbagekalde din nøgle til lejeradministration|Ingen (automatisk)|Ingen (automatisk)|
|Nøglen igen din nøgle til lejeradministration|Ja|Ja|
|Sikkerhedskopiere og gendanne din nøgle til lejeradministration|Nej|Ja|
|Eksport dine lejer nøgle|Ja|Nej|
|Besvare et brud|Ja|Ja|
Når du har identificeret som topologi, der er implementeret, kan du bruge en af de følgende afsnit for flere oplysninger om disse handlinger for Azure RMS lejer nøglen.

## <a name="BKMK_MSManagedOperations"></a>Microsoft-administreret: Lejer nøgle livscyklus operationer
Hvis Microsoft administrerer din lejer nøgle for Azure Rights Management (standard), kan du bruge de følgende afsnit kan finde flere oplysninger om livscyklus-operationer, der er relevante for denne topologi:

-   [Tilbagekalde din nøgle til lejeradministration](../Topic/Operations_for_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_MSRevoke)

-   [Nøglen igen din nøgle til lejeradministration](../Topic/Operations_for_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_MSRekey)

-   [Sikkerhedskopiere og gendanne din nøgle til lejeradministration](../Topic/Operations_for_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_MSBackup)

-   [Eksport dine lejer nøgle](../Topic/Operations_for_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_MSExport)

-   [Besvare et brud](../Topic/Operations_for_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_MSBreach)

### <a name="BKMK_MSRevoke"></a>Tilbagekalde din nøgle til lejeradministration
Når du afmelde Azure RMS, Azure RMS stopper med lejer nøglen og kræves ingen handling fra dig.

### <a name="BKMK_MSRekey"></a>Nøglen igen din nøgle til lejeradministration
At skrive er også kendt som rullende din nøgle. Ikke igen nøgle lejer nøglen, medmindre det er strengt nødvendigt. Ældre klienter, som Office 2010 er ikke udviklet til at håndtere vigtige ændringer problemfrit. I dette scenario, skal du rydde RMS-tilstand på computere ved hjælp af Gruppepolitik eller en tilsvarende mekanisme. Der er dog nogle legitime hændelser, der kan tvinge dig til nøglen lejer nøglen igen. For eksempel:

-   Virksomheden er opdelt i to eller flere firmaer. Når du igen nøglen lejer nøglen, vil den nye virksomhed ikke har adgang til nyt indhold, der udgiver dine medarbejdere. De kan få adgang til det gamle indhold, hvis de har en kopi af den gamle lejer nøglen.

-   Du mener masterkopi af lejer nøglen (kopi i din besiddelse) blev beskadiget.

Du kan igen nøgle lejer nøglen ved at kalde Microsoft Customer Support Services (CSS) og bevise, at du er administrator af lejer.

Når du igen nøglen nøglen lejer, er nyt indhold beskyttet ved hjælp af den nye lejer-nøgle. Dette sker i en trinvis måde, så i en periode, nogle nye indhold fortsætter med at være beskyttet med den gamle lejer nøgle. Beskyttet indhold forbliver tidligere beskyttede gamle lejer nøglen. Til dette scenario, bevarer Azure RMS gamle lejer nøglen, så det kan udstede licenser til gamle indhold.

### <a name="BKMK_MSBackup"></a>Sikkerhedskopiere og gendanne din nøgle til lejeradministration
Microsoft er ansvarlig for sikkerhedskopiering af din lejer nøgle, og der kræves ingen handling fra dig.

### <a name="BKMK_MSExport"></a>Eksport dine lejer nøgle
Du kan eksportere dine Azure RMS-konfiguration og lejer nøglen ved at følge instruktionerne i disse tre trin:

##### Trin 1: Indlede eksport

-   For at gøre dette skal du kontakte Microsoft kundesupport Service (CSS). Du skal bevise, at du er administrator for din Azure RMS lejer.

##### Trin 2: Vent på godkendelse

-   Microsoft bekræfter, at din anmodning om at frigive RMS lejer nøglen er lovlig. Denne proces kan tage op til 3 uger.

##### Trin 3: Modtage vigtige instruktioner fra CSS

-   Microsoft Customer Support Services (CSS) sender dig dit Azure RMS-konfiguration og lejer nøgle som krypteret i en adgangskodebeskyttet fil med filtypenavnet .tpd. Hvis du vil gøre dette, sender CSS først dig (som den person, der startede eksport) et værktøj via e-mail. Du skal køre værktøjet fra en kommandoprompt som følger:

    ```
    AadrmTpd.exe -createkey
    ```
    Dette genererer en RSA-nøglepar og gemmer de offentlige og private halvdele som filer i den aktuelle mappe. For eksempel: **PublicKey-FA29D0FE-5049-4C8E-931B-96C6152B0441.txt** og **PrivateKey-FA29D0FE-5049-4C8E-931B-96C6152B0441.txt**.

    Svare på e-mailen fra CSS, vedhæfte en fil, der har et navn, der begynder med **PublicKey**. CSS næste sender dig en TPD-fil som en .XML-fil, der er krypteret med RSA-nøgle. Kopier denne fil til den samme mappe, som du oprindeligt kørte værktøjet AadrmTpd og køre værktøjet igen, ved hjælp af din fil, der starter med **PrivateKey** og fra CSS-filen. For eksempel:

    ```
    AadrmTpd.exe -key PrivateKey-FA29D0FE-5049-4C8E-931B-96C6152B0441.txt -target TPD-77172C7B-8E21-48B7-9854-7A4CEAC474D0.xml
    ```
    Kommandoens output skal være to filer: En indeholder almindelig tekst-adgangskode for det TPD, der er beskyttet med adgangskode, og den anden er den adgangskodebeskyttede TPD sig selv. Begge bør have samme GUID som offentlige og private nøgle filer fra, når du har kørt kommandoen AadrmTpd.exe - createkey vil krydshenvise til formål:

    -   Password-FA29D0FE-5049-4C8E-931B-96C6152B0441.txt

    -   ExportedTPD-FA29D0FE-5049-4C8E-931B-96C6152B0441.xml

    Tag sikkerhedskopi af disse filer og gemme dem sikkert for at sikre, at du kan fortsætte med at dekryptere indhold, der er beskyttet med lejer nøglen. Desuden, hvis du vil overføre til AD RMS, kan du importere filen TPD (den fil, der starter med **ExportedTDP**) til AD RMS-serveren.

##### Trin 4: Løbende: Beskytte din nøgle til lejeradministration

-   Når du modtager din lejer nøgle, være godt beskyttet, fordi Hvis nogen får adgang til det, de kan dekryptere alle dokumenter, der er beskyttet ved hjælp af nøglen.

    Hvis årsagen til eksport af din lejer nøgle, fordi du ikke længere vil bruge Azure RMS som best practice, nu deaktivere din RMS lejer. Ikke vente med at gøre dette, når du har modtaget din lejer nøgle, fordi denne foranstaltning vil bidrage til at begrænse følgerne, hvis din lejer nøgle åbnes med nogen, som ikke skal have. Yderligere oplysninger finder du [Nedlukning og deaktivere Azure rettighedsstyring](../Topic/Decommissioning_and_Deactivating_Azure_Rights_Management.md).

### <a name="BKMK_MSBreach"></a>Besvare et brud
Ingen sikkerhedssystem, uanset hvor stærk er udført uden en overtrædelse svar proces. Lejer nøglen kan være beskadiget eller stjålet. Selv når den er godt beskyttet og, måske sårbarheder fundet i nuværende generation HSM teknologi eller aktuelle nøglelængder og algoritmer.

Microsoft har et dedikeret team til at reagere på sikkerhedshændelser i sine produkter og tjenester. Så snart der er en troværdig rapport på en hændelse, igangsætter dette team til at undersøge omfanget, årsagen og afhjælpninger. Hvis denne hændelse påvirker dine aktiver, vil derefter Microsoft informere dine Azure RMS lejer administratorer via e-mail ved hjælp af den adresse, du angav, da du abonnerer.

Hvis du har en overtrædelse, afhænger den bedste handling, som du eller Microsoft kan træffe af omfanget af en overtrædelse; Microsoft samarbejder med dig gennem denne proces. Følgende tabel viser nogle typiske situationer og de sandsynlige svar, selvom det præcise svar vil afhænge af de oplysninger, der er konstateret under undersøgelsen.

|Beskrivelse af hændelsen|Sandsynlige svar|
|----------------------------|--------------------|
|Din nøgle til lejeradministration er lækket.|Nøgle igen lejer nøglen. Se den [Nøglen igen din nøgle til lejeradministration](../Topic/Operations_for_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_MSRekey) afsnit i dette emne.|
|En uautoriseret person eller malware har fået ret til at bruge din lejer nøgle, men selve nøglen lækker ikke.|At skrive din lejer nøgle hjælper ikke her og kræver Rodårsagsanalyse. Hvis en proces eller software fejl var ansvarlig for uautoriseret person at få adgang, vil denne situation skal løses.|
|Bliver ikke beregningsmæssigt muligt sårbarhed opdaget i RSA-algoritme, eller nøglelængden eller brute-force-angreb.|Microsoft skal opdatere Azure RMS understøttelse af nye algoritmer og længere nøglelængder der er robust og bed alle kunder til at forny deres lejer nøgler.|

## <a name="BKMK_BYOKManagedOperations"></a>Kunde administreret: Lejer nøgle livscyklus operationer
Hvis du administrerer din lejer nøgle til Azure Rights Management (Medbring din egen nøgle eller BYOK, scenario), bruge de følgende afsnit kan finde flere oplysninger om livscyklus-operationer, der er relevante for denne topologi:

-   [Tilbagekalde din nøgle til lejeradministration](../Topic/Operations_for_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_BYOKRevoke)

-   [Nøglen igen din nøgle til lejeradministration](../Topic/Operations_for_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_BYOKRekey)

-   [Sikkerhedskopiere og gendanne din nøgle til lejeradministration](../Topic/Operations_for_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_BYOKBackup)

-   [Eksport dine lejer nøgle](../Topic/Operations_for_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_BYOKExport)

-   [Besvare et brud](../Topic/Operations_for_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_BYOKBreach)

### <a name="BKMK_BYOKRevoke"></a>Tilbagekalde din nøgle til lejeradministration
Når du afmelde Azure RMS, Azure RMS stopper med lejer nøglen og kræves ingen handling fra dig.

### <a name="BKMK_BYOKRekey"></a>Nøglen igen din nøgle til lejeradministration
At skrive er også kendt som rullende din nøgle. Ikke igen nøgle lejer nøglen, medmindre det er strengt nødvendigt. Ældre klienter, som Office 2010 er ikke udviklet til at håndtere vigtige ændringer problemfrit. I dette scenario, skal du rydde RMS-tilstand på computere ved hjælp af Gruppepolitik eller en tilsvarende mekanisme. Der er dog nogle legitime hændelser, der kan tvinge dig til nøglen lejer nøglen igen. For eksempel:

-   Virksomheden er opdelt i to eller flere firmaer. Når du igen nøglen lejer nøglen, vil den nye virksomhed ikke har adgang til nyt indhold, der udgiver dine medarbejdere. De kan få adgang til det gamle indhold, hvis de har en kopi af den gamle lejer nøglen.

-   Du mener masterkopi af lejer nøglen (kopi i din besiddelse) blev beskadiget.

Når du igen nøglen nøglen lejer, er nyt indhold beskyttet ved hjælp af den nye lejer-nøgle. Dette sker i en trinvis måde, så i en periode, nogle nye indhold fortsætter med at være beskyttet med den gamle lejer nøgle. Beskyttet indhold forbliver tidligere beskyttede gamle lejer nøglen. Til dette scenario, bevarer Azure RMS gamle lejer nøglen, så det kan udstede licenser til gamle indhold.

Generere til nøglen igen lejer nøglen, og Opret en ny nøgle via internettet eller personligt, ved hjælp af procedurerne i det [Implementing bring your own key (BYOK)](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_ImplementBYOK) punkt fra den [Planlægning og implementering af Azure Rights Management lejer nøglen](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md) emne.

### <a name="BKMK_BYOKBackup"></a>Sikkerhedskopiere og gendanne din nøgle til lejeradministration
Du er ansvarlig for at sikkerhedskopiere din nøgle til lejeradministration. Hvis du har oprettet din lejer nøgle i en Thales HSM, for at tage en sikkerhedskopi af nøglen, lige sikkerhedskopiere filen Tokenized nøgle filen verden og administratoren kort.

Hvis du har overført din nøgle ved at følge fremgangsmåderne i det [Implementing bring your own key (BYOK)](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_ImplementBYOK) afsnit fra den [Planlægning og implementering af Azure Rights Management lejer nøglen](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md) emne, Azure RMS bevares Tokenized nøgle filen, til at beskytte mod svigt i alle Azure RMS-noder. Dog anser ikke dette er en fuld sikkerhedskopi. Eksempelvis hvis du får brug for en almindelig tekst-kopi af din nøgle til brug uden for en Thales HSM, vil Azure RMS ikke kunne hente den for dig, fordi den indeholder kun en kopi, der ikke kan nyttiggøres.

### <a name="BKMK_BYOKExport"></a>Eksport dine lejer nøgle
Hvis du bruger BYOK, kan du eksportere din lejer nøgle fra Azure RMS. Kopien i Azure RMS er ikke kan nyttiggøres. Hvis du vil slette denne nøgle, så den kan ikke længere bruges, skal du kontakte Microsoft kundesupport Service (CSS).

### <a name="BKMK_BYOKBreach"></a>Besvare et brud
Ingen sikkerhedssystem, uanset hvor stærk er udført uden en overtrædelse svar proces. Lejer nøglen kan være beskadiget eller stjålet. Selv når den er godt beskyttet og, måske sårbarheder fundet i nuværende generation HSM teknologi eller aktuelle nøglelængder og algoritmer.

Microsoft har et dedikeret team til at reagere på sikkerhedshændelser i sine produkter og tjenester. Så snart der er en troværdig rapport på en hændelse, igangsætter dette team til at undersøge omfanget, årsagen og afhjælpninger. Hvis denne hændelse påvirker dine aktiver, vil derefter Microsoft informere dine Azure RMS lejer administratorer via e-mail ved hjælp af den adresse, du angav, da du abonnerer.

Hvis du har en overtrædelse, afhænger den bedste handling, som du eller Microsoft kan træffe af omfanget af en overtrædelse; Microsoft samarbejder med dig gennem denne proces. Følgende tabel viser nogle typiske situationer og de sandsynlige svar, selvom det præcise svar vil afhænge af de oplysninger, der er konstateret under undersøgelsen.

|Beskrivelse af hændelsen|Sandsynlige svar|
|----------------------------|--------------------|
|Din nøgle til lejeradministration er lækket.|Nøgle igen lejer nøglen. Se den [Nøglen igen din nøgle til lejeradministration](../Topic/Operations_for_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_BYOKRekey) afsnit i dette emne.|
|En uautoriseret person eller malware har fået ret til at bruge din lejer nøgle, men selve nøglen lækker ikke.|At skrive din lejer nøgle hjælper ikke her og kræver Rodårsagsanalyse. Hvis en proces eller software fejl var ansvarlig for uautoriseret person at få adgang, vil denne situation skal løses.|
|Svaghed afsløres i den nuværende generations HSM teknologi.|Microsoft skal opdatere HSMs. Hvis der er grund til at tro, at sikkerhedsproblemet udsættes nøgler, bede Microsoft alle kunder til at forny deres lejer nøgler.|
|Bliver ikke beregningsmæssigt muligt sårbarhed opdaget i RSA-algoritme, eller nøglelængden eller brute-force-angreb.|Microsoft skal opdatere Azure RMS understøttelse af nye algoritmer og længere nøglelængder der er robust og bed alle kunder til at forny deres lejer nøgler.|

## Se også
[Ved hjælp af Azure rettighedsstyring](../Topic/Using_Azure_Rights_Management.md)

