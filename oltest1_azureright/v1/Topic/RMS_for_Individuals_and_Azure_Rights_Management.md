---
description: na
keywords: na
title: RMS for Individuals and Azure Rights Management
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2efcb440-fefd-45e9-872b-f471573aadf2
---
# RMS for enkeltpersoner og Azure rettighedsstyring
RMS til personer, der er et gratis abonnement selvbetjening for brugerne i en organisation, der er blevet sendt følsomme filer, der er beskyttet af Microsoft Azure Rights Management (Azure RMS), men de kan ikke godkendes, da deres IT-afdelingen ikke administreres af en konto for dem i Azure. For eksempel IT-afdelingen ikke har Office 365 eller bruge Azure tjenester.

Disse brugere kan tilmelde dig en gratis arbejde eller skole-konto til brug i Azure RMS og hente og installere rettighedsstyring, der deler programmet. Derfor er disse brugere kan nu godkende for at bevise, at de er den person, de beskyttede filer blev sendt til, og Læs derefter de beskyttede filer på computere eller mobilenheder.

Ved hjælp af rettighedsstyring, der deler programmet på Windows-computere, disse brugere også beskytte filer på stedet eller sende beskyttede filer via e-mail til personer inden for eller uden for virksomheden. Hvis modtagerne af e-mailen, som de sender i en organisation, der ikke også administrerer brugerkonti i Azure, kan de for tilmelde dig en RMS for enkeltpersoner konto til at læse den beskyttede e-mail vedhæftet fil.

> [!IMPORTANT]
> Denne gratis abonnement sikrer, at autoriserede personer kan altid få vist filer, der er beskyttet. I øjeblikket, du kan også bruge denne gratis abonnement til at beskytte dokumenter og oprette nye beskyttede e-mails, men mulighed for at oprette nye beskyttet indhold henvender sig kun til prøveversionen og den fjernes muligvis i fremtiden. Yderligere oplysninger og eventuelle ændringer af bruger RMS til enkeltpersoner til at beskytte indhold, se den [Microsoft Rights Management vilkår for brug af](https://portal.aadrm.com/Legal/Service).

Finde flere oplysninger om, hvordan du kan beskytte filerne ved hjælp af den gratis rettighedsstyring deling ansøgning, den [Rights Management deling Programguide for brugere](http://technet.microsoft.com/library/dn339006.aspx).

RMS til personer, der er et eksempel på en selvbetjening tilmelding, der understøttes af Azure Active Directory. Finde flere oplysninger om, hvordan dette fungerer, [Hvad er nyt tilmelding af Azure?](https://azure.microsoft.com/documentation/articles/active-directory-self-service-signup/) i dokumentationen til Microsoft Azure. Brug de følgende afsnit for yderligere oplysninger, der er specifikke for RMS for personer:

-   [Hvordan brugerne tilmelde dig RMS for personer](../Topic/RMS_for_Individuals_and_Azure_Rights_Management.md#BKMK_SignUp)

    -   [Teknisk oversigt](../Topic/RMS_for_Individuals_and_Azure_Rights_Management.md#BKMK_TechnicalOverview)

-   [Hvordan administratorer kan styre de konti, der er oprettet til RMS for personer](../Topic/RMS_for_Individuals_and_Azure_Rights_Management.md#BKMK_TakeControlofAccounts)

-   [Hvordan du finder ud af, om brugerne har tilmeldt sig RMS for personer](#BKMK_Detect)

## <a name="BKMK_SignUp"></a>Hvordan brugerne tilmelde dig RMS for personer
For at tilmelde dig denne gratis konto, du beder om det. ved at besøge det [Microsoft Rights Management side](https://portal.aadrm.com/), og give dit arbejde eller skole, e-mail-adresse. Er den mest almindelige måde, vil du blive sendt videre til tilmelding til siden, hvis du har modtaget en e-mail med en beskyttet vedhæftet fil, som indeholder instruktioner hvordan til tilmelding. Du modtager en e-mail svar fra Microsoft og kan derefter fuldføre tilmeldingsprocessen ved at angive detaljer til at oprette din konto. Når du modtager en e-mail-bekræftelse fra Microsoft, sender denne endelige e-mail dig til en side, hvor du kan hente programmet deling for de forskellige enheder og et link til brugervejledningen.

#### At tilmelde sig en RMS for personer

1.  Ved hjælp af en Windows eller Mac computer, gå til den [Microsoft Rights Management side](https://portal.aadrm.com).

2.  Skriv den e-mail-adresse, du bruger til din organisation, som **janetm@contoso.com** eller **p.dover@fabrikam.com**.

    > [!IMPORTANT]
    > Personlige e-mail-konti understøttes ikke, så skal du ikke angive en Microsoft-konto (tidligere kendt som Microsoft Live ID-konto) eller en anden personlig konto, som du kan bruge hjemme fra din Internet-udbyder.

3.  Klik på **Kom i gang**.

    Microsoft bruger din e-mail-adresse til at kontrollere, om organisationen allerede har en [Betalt abonnement, der omfatter Azure RMS](https://technet.microsoft.com/library/dn655136.aspx). Hvis det er tilfældet, behøver du RMS for personer, så du skal være logget på straks og på selvbetjening Tilmeld dig RMS for personer, der er annulleret. Hvis et betalt abonnement på Azure RMS ikke findes, skal du fortsætte til næste trin.

4.  Vent på en bekræftelse af e-mailen skal sendes til den adresse, du har angivet. Det vil være fra Microsoft (til DoNotReply@microsoft.com) og har omfattet **Microsoft RMS**.

5.  Når du modtager e-mailen, skal du klikke på hyperlinket i vejledningen for at fuldføre tilmeldingsprocessen.

6.  Linket fører dig en ny **Microsoft Rights Management** side til at angive oplysninger for din konto. Skriv dit fornavn, dit efternavn, Indtast og Bekræft en adgangskode efter eget valg, Vælg dit land eller det nærmeste land til dit Hvis dit land ikke er angivet på rullelisten og klik derefter på **Create**.

7.  Vent en anden e-mail-meddelelse fra Microsoft, der nu bekræfter, at din konto er klar til brug.

8.  Når du modtager e-mailen, skal du klikke på linket for at logge på og læse instruktionerne for at hente og installere programmet deling, eller klik på Hjælp for at læse brugervejledningen til deling program.

Nu din konto er oprettet, er du klar til at starte med at beskytte filer og læse filer, som andre har beskyttet. Angiv din e-mail-adresse og adgangskode, du brugte til at oprette kontoen til RMS for personerne, når du bliver bedt om at logge på at beskytte og læsning af beskyttede filer.

### <a name="BKMK_TechnicalOverview"></a>Teknisk oversigt
RMS til personer, der bruger en egenhændig tilmeldingen, der også bruges af andre tjenester, der bruger Microsoft cloud-baseret teknologi til at godkende brugere.

Dette er, hvad der sker i baggrunden, når en bruger tilmelder sig RMS for personer og deres organisation har ikke et abonnement på Office 365 eller Azure abonnement og derfor ingen directory i Azure til at godkende brugere:

1.  Når den første bruger fra en organisation anmoder om et abonnement til RMS for personer, kontrolleres det domænenavn, der er angivet i deres e-mail-adresse til at se, om det allerede er tilknyttet en Azure lejer. Hvis der ikke er nogen eksisterende lejer, oprettes en ny lejer og Azure mappe automatisk for den organisation, der indeholder en konto for denne første bruger. I modsætning til med et betalt abonnement på Azure, er denne første konto ikke en global administrator, men en standardbruger. Den nye konto bruger en e-mail-adresse og adgangskode, som brugeren har angivet.

    > [!NOTE]
    > Nogle domænenavne kan ikke bruges til at oprette mappen og derfor ikke kan bruges til RMS for personer. Listen over blokerede domænenavne kan ses i filen JavaScript Object Notation: [http://portal.aadrm.com/content/blocked_domains.json](http://portal.aadrm.com/content/blocked_domains.json)

    Hvis der findes en eksisterende lejer, kontrolleres den for at se, om det allerede har et abonnement til Azure RMS. Når der findes ingen abonnement, kan gratis RMS enkeltpersoner abonnement tilføjes.

2.  Organisationen ydes RMS enkeltpersoner abonnement. Nu, denne bruger kan godkendes af Azure og kan derefter beskytte filer og læse filer, som andre har beskyttet ved hjælp af Azure Rights Management. For at beskytte og læse beskyttede filer, skal brugeren have en RMS-enlightened ansøgning, som den frie [Rights Management, der deler programmet](https://technet.microsoft.com/library/dn919648.aspx).

3.  Når den anden bruger fra samme organisation anmoder om en RMS enkeltpersoner abonnement, føjes en ny brugerkonto til den tidligere oprettede Azure mappe ved hjælp af organisationens RMS enkeltpersoner abonnement. Denne anden bruger kan gøre alt det, der kunne gøre den første bruger beskytte filer og læse beskyttede filer, men også disse to brugere kan nu mere let arbejde sikkert fordi de hurtigt kan anvende standardskabeloner til filer, der begrænser adgangen til kontiene i deres organisation Azure directory.

4.  Efterfølgende brugere fra den samme organisation følger det samme mønster, tilføjelse af brugerkonti (når nye brugere kan tilmelde dig) til organisationens Azure mappe. Flere firmaer, der føjes til mappen, jo flere brugere kan sikkert samarbejde med kolleger og partnere, og mere let at forhindre uautoriserede brugere i at læse deres filer, når de ikke bør have adgang til dem..

I hele denne proces er der gratis for virksomheden og ikke noget arbejde, der kræves fra IT-afdelingen. IT-afdelingen kan dog vælge at benytte en af følgende:

-   **Administrere konti og tilmeldingsprocessen**: IT-administratorer kan overtage ejerskabet af den automatisk oprettede mappe og konti i Azure. De kan derefter administrere konti ved at implementere directory integration-løsninger såsom synkronisering af adgangskoder og single sign-on. Eller de kan forhindre brugere i at oprette konti eller tilmelde sig en RMS for personer.

    Yderligere oplysninger finder du i afsnittet [Hvordan administratorer kan styre de konti, der er oprettet til RMS for personer](../Topic/RMS_for_Individuals_and_Azure_Rights_Management.md#BKMK_TakeControlofAccounts).

-   **Håndtere Rights Management**: IT-administratorer kan konvertere RMS enkeltpersoner abonnement for organisationen til et betalt abonnement, der omfatter Azure Rights Management. Når de gør dette, bevares de eksisterende Azure mappe og regnskaber for en problemfri overgang til eksisterende brugere, der brugte RMS til enkeltpersoner. Alle filer, som brugerne beskyttet tidligere vil stadig være beskyttet med samme regler, og de personer, de har tilladelse til at bruge filerne vil stadig kunne bruge filerne på samme måde.

    Når du tager dette kursus for handling, din organisation fordele ved at integrere Rights Management i dens arbejdsgange, tjenester og datalagre. Desuden kan du nu administrere Rights Management, fordi du har kontrol over din organisations lejer nøglen til Azure Rights Management. Du kan nu gøre følgende:

    -   Konfigurer Exchange og SharePoint til at understøtte Azure Rights Management, selvom de kører på stedet. Exchange og SharePoint understøttes oprindeligt til online-tjenester, og de understøttes af en forbindelse til de lokale servere. Yderligere oplysninger finder du i følgende:

        -   Afsnittene Exchange Online og SharePoint Online fra [Office 365: Konfiguration af klienter og online-tjenester](../Topic/Configuring_Applications_for_Azure_Rights_Management.md#BKMK_O365) i den [Konfiguration af programmer for Azure rettighedsstyring](../Topic/Configuring_Applications_for_Azure_Rights_Management.md) emne

        -   [Installation af Azure Rights Management-stik](../Topic/Deploying_the_Azure_Rights_Management_Connector.md)

    -   Udføre e-discovery på firmaet ejer data, så du kan eventuelt dekryptere filer, der er beskyttet med Rights Management. Yderligere oplysninger finder du under [Konfiguration af Superbrugere til Azure Rights Management og Discovery Services eller genoprettelse af Data](../Topic/Configuring_Super_Users_for_Azure_Rights_Management_and_Discovery_Services_or_Data_Recovery.md).

    -   Logge alle aktiviteter for Rights Management, som bruges i organisationen. Dette er særlig kraftig, fordi ikke blot kan du overvåge hvilke filer beskyttes, og der blevet adgang til de beskyttede filer, men du kan også identificere potentielt mistænkelig adfærd fra uautoriserede personer, der forsøger at få adgang til beskyttede filer. Yderligere oplysninger finder du under [Logføring og analyse af brugen af Azure Rights Management](../Topic/Logging_and_Analyzing_Azure_Rights_Management_Usage.md).

    -   Giver brugerne mulighed for at spore og tilbagekalde deres beskyttede dokumenter, hvis disse funktioner understøttes af din [Azure RMS abonnement](https://technet.microsoft.com/dn858608). Yderligere oplysninger finder du  [registrere og fjerne dine filer](https://technet.microsoft.com/library/dn986611.aspx) fra den [RMS deling program brugervejledningen](https://technet.microsoft.com/library/dn339006.aspx).

    -   Implementere en Medbring din egen nøgle løsning (BYOK), så din lejer nøgle til Azure Rights Management er genereret på stedet i overensstemmelse med din IT-politikker og sikkert overført til Microsoft ved hjælp af en Hardware Security Module (HSM). Yderligere oplysninger finder du under [Planlægning og implementering af Azure Rights Management lejer nøglen](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md).

## <a name="BKMK_TakeControlofAccounts"></a>Hvordan administratorer kan styre de konti, der er oprettet til RMS for personer
Hvis du ikke vil konvertere organisationens RMS til enkeltpersoner abonnementet til et betalingsabonnement, kan du styre brugerkonti i mappen Azure, der blev oprettet for din organisation på følgende måder:

-   Implementere directory integration løsninger til Azure Active Directory og Active Directory-domæneservices-infrastruktur. Du kan synkronisere konti og adgangskoder, så brugerne ikke behøver at oprette nye konti for at bruge Rights Management og din lokale adgangskodepolitikker gælder for nye Azure brugerkonti. Du kan også synkronisere adgangskoder, så brugerne ikke behøver at huske en anden adgangskode for at bruge Rights Management.

-   Du kan forhindre brugere i at bruge Azure Rights Management med RMS til enkeltpersoner abonnement tilmelding. I de fleste tilfælde er der lidt fordel i at gøre dette, fordi brugerne enten deler filer uden beskyttelse (som virksomheden kunne bringes i fare), eller vil bruge en anden fil beskyttelsesmekanisme, som ikke har IT-afdelingen med mulighed for at få adgang til dataene. Men hvis du vil forhindre brugere i at tilmelde dig til at bruge RMS for personer, Benyt en af følgende efter at du har overtaget ejerskabet af organisationens katalogtjeneste i Azure:

    -   Forhindre alle brugere i at ansøge om abonnementer Self service, som indeholder RMS til enkeltpersoner.  I øjeblikket, kan du angive dette af tjeneste; Indstillingen gælder for alle Azure abonnementer, der bruger Self service-processen. For at gøre dette skal du angive den **AllowAdHocSubscriptions** parameter til false med den [sæt MsolCompanySettings](http://technet.microsoft.com/library/dn194127.aspx) cmdlet fra modulet Windows PowerShell til Azure Active Directory. For eksempel: **Set-MsolCompanySettings -AllowAdHocSubscriptions $false**

    -   Forhindre brugere i at oprette en ny konto i Azure, hvilket betyder, at kun brugere, der allerede har en konto i Azure kan tilmelde sig Self service abonnementer, som indeholder RMS til enkeltpersoner.  For at gøre dette skal du angive den **AllowEmailVerifiedUsers** parameter til false med den [sæt MsolCompanySettings](http://technet.microsoft.com/library/dn194127.aspx) cmdlet fra modulet Windows PowerShell til Azure Active Directory. For eksempel: **Set-MsolCompanySettings -AllowEmailVerifiedUsers $false -AllowAdHocSubscriptions $true**

    -   Synkroniser Active Directory-domæneservices-infrastruktur med Azure Active Directory. Denne handling forhindrer, at nye firmaer der oprettes, når brugere tilmeldes selvbetjening abonnementer som RMS til enkeltpersoner, og du kan slette eller deaktivere konti, der tidligere blev oprettet i mappen Azure.

Til at styre brugerkonti i mappen Azure eller forhindre brugere i at tilmelde sig en RMS for personer, skal du have et abonnement, Azure og ejer mappen. Hvis du ikke allerede har et Azure-abonnement, kan du få en uden beregning. Hvis en mappe er oprettet automatisk for dig under processen Self service, kan du overtage ejerskabet af det domæne, der blev brugt til at oprette den. Hvis du allerede ejer en mappe på Azure, men brugerne har angivet et nyt domæne, som du bruger i din organisation, kan du flette domænet til din eksisterende mappe. Yderligere oplysninger finder du i instruktionerne i [Hvad er nyt tilmelding af Azure?](https://azure.microsoft.com/documentation/articles/active-directory-self-service-signup/)

## <a name="BKMK_Detect"></a>Hvordan du finder ud af, om brugerne har tilmeldt sig RMS for personer
Som administrator, hvordan ved du, hvis brugerne har tilmeldt sig RMS personer? Du kan bruge en hvilken som helst eller en kombination af følgende metoder:

-   Spørg brugerne, hvordan de beskytter meget fortrolige filer, især ved at samarbejde med andre uden for organisationen.

-   Når du har et abonnement, Azure for organisationen, kan du bruge den [Get-MsolAccountSku](https://msdn.microsoft.com/library/azure/dn194118.aspx) -cmdlet til at se, om **RIGHTSMANAGEMENT_ADHOC** returneres som en af abonnementerne. Hvis det er, er RMS enkeltpersoner abonnement, som blev givet til organisationen, med en gruppe af aktive enheder, der er tilgængelige for brugerne at anvende selvbetjeningsportalen tilmeldingsprocessen.

-   Bruge en system management løsning, som System Center Konfigurationsstyring til lageret installeret software og software i brug. Rettighedsstyring, der deler programmet kører ved hjælp af den **ipviewer.exe** program, og du kan [hente og installere programmet](http://go.microsoft.com/fwlink/?LinkId=303970) til fri til at identificere andre karakteristika om dette program, som du derefter bruge for software lager.

-   Være opmærksom på, om filtypenavne, der er oprettet af programmet Rights Management deling. Filtypenavnene .pfile og .ppdf er de mest åbenlyse eksempler, men der er andre filer, der ændrer deres filtypenavn, når de oprindeligt er beskyttet med Rights Management. Yderligere oplysninger finder du på [understøttede filtyper og filtypenavne](http://technet.microsoft.com/library/dn339003.aspx) afdeling i den [Rights Management deling program administratorvejledningen](http://technet.microsoft.com/library/dn339003.aspx).

## Se også
[Introduktion til Azure rettighedsstyring](../Topic/Getting_Started_with_Azure_Rights_Management.md)

