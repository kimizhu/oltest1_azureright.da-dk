---
description: na
keywords: na
title: Helping Users to Protect Files by Using Azure Rights Management
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 58f9a6ff-4121-4c8c-9865-1bb290604ad2
---
# At hj&#230;lpe brugere med at beskytte filerne ved hj&#230;lp af Azure rettighedsstyring
Når du har installeret og konfigureret Azure Rights Management (Azure RMS) for din organisation, kan du få hjælp og vejledning for brugere, administratorer og supportteknikerne:

-   **Slutbrugeroplysninger:**

    Lade dem vide, hvordan og hvornår til at beskytte dokumenter og e-mails, der indeholder følsomme oplysninger. Når det er muligt, give disse oplysninger til deres eksisterende arbejdsgange, så de kan integrere de ekstra trin i en allerede velkendt proces i stedet for at indføre helt nye processer. Sørg for at fortælle dem, fordelene (og risici), der er specifikke for din virksomhed, og som giver retningslinjer for, hvornår de skal beskytte filer og e-mails. Hvis du har konfigureret [brugerdefinerede skabeloner](http://technet.microsoft.com/library/dn642472.aspx), giver oplysninger om, hvilken fremgangsmåde til at vælge, hvis skabelonens navn og beskrivelse, ikke er tilstrækkeligt at vælge den korrekte.

    > [!TIP]
    > Eksempel videoer for slutbrugere:
    > 
    > -   [Azure RMS-brugeroplevelse](http://channel9.msdn.com/Series/Information-Protection/Azure-RMS-user-experience)
    > -   [Sporing af Azure RMS-dokument og tilbagekaldelse](http://channel9.msdn.com/Series/Information-Protection/Azure-RMS-Document-Tracking-and-Revocation)

-   **Administratoroplysninger:**

    Nogle programmer anvender automatisk beskyttelse af oplysninger, ved hjælp af politikker og indstillinger, der konfigureres af administratorer. Du skal muligvis give instruktioner til administratorer, der administrerer disse programmer og tjenester til disse programmer. Yderligere oplysninger finder du under [Hvordan programmer understøtter Azure rettighedsstyring](../Topic/How_Applications_Support_Azure_Rights_Management.md) og [Konfiguration af programmer for Azure rettighedsstyring](../Topic/Configuring_Applications_for_Azure_Rights_Management.md).

-   **Hjælp-oplysninger på skrivebordet:**

    En af de mest nyttige værktøjer til helpdesk er den [RMS Analyzer](https://www.microsoft.com/en-us/download/details.aspx?id=46437).   Hjælp desk operatorer kan køre den med indstillingen Azure RMS-administratoren, og de kan bede brugerne at køre programmet med indstillingen Azure RMS-bruger. Dette værktøj kan ikke kun hjælpe med at identificere problemer, men også løse problemer, der findes, og hvis du stadig ikke rettet, registrere sporingslogger.

    Hvis der er legitime anmodninger skal have adgang til alle de rettigheder til beskyttede dokumenter, for eksempel en anmodning fra den juridiske afdeling eller en leder efter en medarbejder, der har forladt virksomheden, Kontroller helpdesk har processer til at anmode om dette ved hjælp af Azure RMS [superbruger funktion](https://technet.microsoft.com/en-us/library/mt147272.aspx).

    Desuden er nogle af de typiske problemer, brugerne rapporterer muligvis:

    -   **Logge på Hjælp:**

        Brugere kan blive bedt om legitimationsoplysninger, når Azure RMS skal godkendes af en bruger, og kan ikke bruge cachelagrede legitimationsoplysninger. Dette er brugerens arbejde eller skole konto og adgangskode, der er knyttet til din Office 365-lejer eller lejer Azure Active Directory. Det vil ikke være en Microsoft-konto (tidligere Microsoft Live ID) eller deres personlige e-mail-konto, da disse ikke understøttes i øjeblikket af Azure RMS. Give oplysninger om, hvilken konto der skal bruges, når brugere bliver bedt om legitimationsoplysninger, når de bruger disse programmer med Azure RMS brugere og supportteknikerne.

    -   **Problemer med at beskytte eller bruger indholdstyper:**

        Sørg for, at brugerne har den relevante vejledning til de programmer, de bruger, og bruger programmer og enheder, der understøttes af Azure RMS. Du kan finde flere oplysninger om understøttede programmer og enheder, i [Krav til Azure rettighedsstyring](../Topic/Requirements_for_Azure_Rights_Management.md).

        Hvis brugere se en fejl under forsøget på at beskytte eller forbruge indhold, kan du bede dem til at køre de [RMS Analyzer](https://www.microsoft.com/en-us/download/details.aspx?id=46437) som bruger Azure RMS.

        Hvis brugere rapporterer, at de kan åbne beskyttet indhold, men har ikke de rettigheder, som de har brug for, kan du bede dem til at køre de [RMS Analyzer](https://www.microsoft.com/en-us/download/details.aspx?id=46437) som bruger Azure RMS og hente og få vist skabelonerne. Dette bekræfter, at de har hentet skabelonerne, og hvilke rettigheder skabelonerne, der indeholder. Problemet kan være, at brugeren ikke er den rigtige gruppe, der er konfigureret for skabelonen, eller, skabelonen skal omkonfigurere for brugeren.

Brug følgende afsnit programspecifikke oplysninger til at hjælpe brugerne med at beskytte følsomme dokumenter og e-mails.

## Brug af databeskyttelse med programmet Rights Management Deling
Rights Management (RMS) dele af programmet er nødvendige for at beskytte og forbruge beskyttet indhold, hvis de bruger Office 2010, men også anbefales til alle computere og mobile enheder, der understøtter Azure RMS.

Ud over at gøre det lettere for brugerne at beskytte vigtige dokumenter, kan RMS deling program brugerne til at holde styr på de dokumenter, som de har beskyttet og tilbagekalde adgang til dem, hvis det er nødvendigt.

Vejledning til at bruge dette program til Windows-computere finder du under de [Rights Management deling program brugervejledningen](http://technet.microsoft.com/library/dn339006.aspx).

Mobile enheder, finder du på [ofte stillede spørgsmål om Microsoft Rights Management deling ansøgning om Mobile platforme](http://technet.microsoft.com/dn451248).

> [!TIP]
> Et detaljeret eksempel scenario med skærmbilleder, se den [Brugere dele vedhæftede filer sikkert med mobile brugere](../Topic/What_is_Azure_Rights_Management_.md#BKMK_Example_SharingApp) afsnit i den [Hvad er Azure Rights Management?](../Topic/What_is_Azure_Rights_Management_.md) emne.

## Med beskyttelse af oplysninger med Office 365, 2016 Office eller Office 2013
Hvis du bruger Azure RMS og ikke har installeret rettighedsstyring, der deler programmet, brugere kan ikke se den **del beskyttet** knap på båndet eller **beskytte lokal** fra Stifinder, der gør det lettere for dem at beskytte filer. De skal følge instruktioner, der svarer til disse for disse brugere.

> [!TIP]
> Du kan finde programspecifik hjælp og vejledning i brugen af beskyttelse af oplysninger med disse programmer, kan du søge efter **IRM** og programmet navn og version.

#### Til at beskytte et dokument i Word 2013

1.  Opret et nyt dokument i Microsoft Word.

2.  Fra den **fil** menuen skal du klikke på **Info**, skal du klikke på **Beskyt dokument**, skal du klikke på **begrænse adgang**, og derefter vælge en skabelon til hurtigt at anvende de relevante rettigheder, eller Vælg **begrænse adgang** og vælger rettighederne til dig selv.

    > [!NOTE]
    > Hvis det er første gang, du har brugt Rights Management, skal du kontakte den [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] service og vil blive bedt om legitimationsoplysninger til at konfigurere IRM i Office-klienten.

3.  Gem dokumentet.

Når andre åbner dokumentet, godkendes først. Hvis de ikke har tilladelse til at åbne dokumentet, åbnes dokumentet ikke. Hvis de har tilladelse til at åbne dokumentet, åbnes med begrænsede brugerrettigheder, der er angivet for den pågældende bruger. Et forbrug ret til kun at få vist tillader eksempelvis ikke bruger til at redigere eller gemme dokumentet, selvom det først kopieres til en anden placering. Brugerrettighederne vises øverst i dokumentet ved hjælp af en begrænsning banner. Banneret kan du få vist de tilladelser, der anvendes på dokumentet, eller det kan indeholde et hyperlink for at få dem vist.

#### Til at beskytte en e-mail ved hjælp af Outlook 2013 og Exchange Online

1.  I Outlook kan du oprette en ny e-mail-meddelelse, der er adresseret til en modtager i organisationen.

2.  Fra den **Indstillinger for** og klik på **tilladelse**, og vælg derefter en indstilling. For eksempel: **Meddeler ikke**, **&lt; firmanavn - &gt; fortrolige** eller **&lt; firmanavn - &gt; fortrolige visning kun**.

3.  Send meddelelsen.

På samme måde til at få vist et beskyttet dokument, godkendes Når modtagerne modtager e-mailen, de først. Hvis de har tilladelse til at se e-mail-meddelelsen, åbnes med begrænsede brugerrettigheder, der er angivet for den pågældende bruger. For eksempel, hvis du har valgt **Videresend ikke**, knappen fremad på båndet er ikke tilgængelig.

#### Til at beskytte en e-mail ved hjælp af Outlook Web App

1.  I Outlook Web App, kan du oprette en ny e-mail-meddelelse, der er adresseret til en modtager i organisationen.

2.  Klik på  **...**,  skal du klikke på **indstille tilladelse**, og vælg derefter en indstilling. For eksempel: **Meddeler ikke**, **ikke besvare alle**, **&lt; firmanavn - &gt; fortrolige** eller **&lt; firmanavn - &gt; fortrolige visning kun**.

3.  Send meddelelsen.

På samme måde til at få vist et beskyttet dokument, godkendes Når modtagerne modtager e-mailen, de først. Hvis de har tilladelse til at se e-mail-meddelelsen, åbnes med begrænsede brugerrettigheder, der er angivet for den pågældende bruger. For eksempel, hvis du har valgt **gør ikke svar til alle**,  **svar til alle** indstilling i meddelelsesvinduet er ikke tilgængelig.

## Se også
[Ved hjælp af Azure rettighedsstyring](../Topic/Using_Azure_Rights_Management.md)

