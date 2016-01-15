---
description: na
keywords: na
title: How Applications Support Azure Rights Management
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2cdc7bde-4044-4021-b887-11476f99afd9
---
# Hvordan programmer underst&#248;tter Azure rettighedsstyring
Brug følgende oplysninger til at hjælpe dig med at forstå, hvordan dine slutbrugere programmer (f.eks. de Office-programmer, Word, Excel, PowerPoint og Outlook) og tjenester (såsom Exchange og SharePoint), kan bruge Microsoft [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] til at beskytte virksomhedens data:

-   [RMS deling program til Windows og mobile platforme](../Topic/How_Applications_Support_Azure_Rights_Management.md#BKMK_SharingAppIntro)

-   [Office-programmer: Word, Excel, PowerPoint, Outlook](../Topic/How_Applications_Support_Azure_Rights_Management.md#BKMK_OfficeAppsIntro)

    -   [Exchange Online og Exchange Server](../Topic/How_Applications_Support_Azure_Rights_Management.md#BKMK_ExchangeIntro)

    -   [SharePoint Online og SharePoint Server](../Topic/How_Applications_Support_Azure_Rights_Management.md#BKMK_SharePointIntro)

-   [Filservere, der kører Windows Server og bruge fil klassificering infrastruktur (FCI)](../Topic/How_Applications_Support_Azure_Rights_Management.md#BKMK_FCIIntro)

-   [Andre programmer, der understøtter den RMS APIs](../Topic/How_Applications_Support_Azure_Rights_Management.md#BKMK_APIAppsIntro)

> [!NOTE]
> At kontrollere versioner og programmer, der [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] (Azure RMS) understøtter, finder du i [Krav til Azure rettighedsstyring](../Topic/Requirements_for_Azure_Rights_Management.md).

I nogle tilfælde anvendes beskyttelse af oplysninger automatisk, i overensstemmelse med politikker, som du konfigurerer. Dette er eksempelvis tilfældet med SharePoint-biblioteker, klassificerede filer og regler for transport af Exchange. I andre tilfælde kan skal brugerne anvende beskyttelse af oplysninger sig fra deres programmer ved at vælge en skabelon eller ved at vælge specifikke indstillinger. Dette er eksempelvis tilfældet, når brugere deler en fil via e-mail eller beskytte en fil lokalt ved at begrænse adgangen til eller brugen til valgte brugere eller brugere uden for organisationen.

Skabeloner gør det lettere for brugerne (og administratorer, der konfigureres politikker) til at anvende det korrekte niveau af beskyttelse og begrænse adgangen til personer inden for organisationen. Selvom [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] leveres med to standardskabeloner, vil du sandsynligvis til at oprette brugerdefinerede skabeloner for at reducere det antal gange, når de har til at angive individuelle indstillinger. Yderligere oplysninger finder du under [Konfiguration af brugerdefinerede skabeloner til Azure rettighedsstyring](../Topic/Configuring_Custom_Templates_for_Azure_Rights_Management.md).

For de tilfælde, hvor brugerne skal anvende beskyttelse af oplysninger, skal du sørge for at forsyne dem med instruktioner og vejledning hvordan og hvornår der skal gøres. Vejledningen skal være specifik for programmet og de versioner, som de bruger, og hvordan de bruger dem, og vejledning til hvornår og hvordan til at anvende oplysninger beskyttelse skal passe til din virksomhed. Yderligere oplysninger finder du under [At hjælpe brugere med at beskytte filerne ved hjælp af Azure rettighedsstyring](../Topic/Helping_Users_to_Protect_Files_by_Using_Azure_Rights_Management.md).

Oplysninger om, hvordan du kan konfigurere disse programmer til Azure RMS, se [Konfiguration af programmer for Azure rettighedsstyring](../Topic/Configuring_Applications_for_Azure_Rights_Management.md).

> [!TIP]
> Eksempler og skærmbilleder af programmer ved hjælp af Azure RMS finder du på [Azure RMS i aktion: Se, hvad administratorer og brugere](../Topic/What_is_Azure_Rights_Management_.md#BKMK_RMSpictures) afsnit fra den [Hvad er Azure Rights Management?](../Topic/What_is_Azure_Rights_Management_.md) emne.

## <a name="BKMK_SharingAppIntro"></a>RMS deling program til Windows og mobile platforme
Programmet RMS deling er et gratis program, der er nødvendige for understøttelse af Office 2010, men det anbefales også til computere med Windows, Mac-computere og mobile enheder. En af dens fordele er, at den kan anvende generisk beskyttelse af programmer og filer, der ikke oprindeligt understøtter [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)], hvilket betyder, at alle filer, der kan beskyttes. Finde flere oplysninger om de forskellige beskyttelse niveauer på [beskyttelse – oprindelig og generiske](http://technet.microsoft.com/library/dn339003.aspx) afsnit fra den [Rights Management deling program administratorvejledningen](http://technet.microsoft.com/library/dn339003.aspx).

Når brugere beskytter deres filer ved hjælp af RMS kan Deling program, de også holde styr på de dokumenter, de beskyttet og tilbagekalde adgang til dem, hvis det er nødvendigt. Dette gøres ved hjælp af den [dokumentsporing websted](http://go.microsoft.com/fwlink/?LinkId=529562).

Til Windows-computere, RMS deling program ubemærket kan integreres med og forbedrer de programmer, som brugerne allerede anvender:

-   En Office-tilføjelsesprogrammet til Word, Excel, PowerPoint og Outlook er installeret. Dette giver brugere med en **del beskyttet** knap på båndet, som aktiverer en nem at bruge dialogboksen Indstillinger, der bruges oftest til at beskytte filer, der skal sendes. Denne knap indeholder også en hurtig måde at få adgang til dokumentet websted.

-   En ny Højreklik mulighed for Filoversigt. Dette giver brugere med en **beskytte lokal** indstilling, som aktiverer en nem at bruge dialogboksen Indstillinger, der bruges oftest til at beskytte filer, der er gemt på en disk.

-   Læseren til at åbne filer, der er beskyttet af [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)]. Med denne Fremviser startes automatisk, når der er ingen andre programmer installeret, kunne åbne den beskyttede fil.

-   Back end-konfiguration til Office 2010, der gør det muligt for Word, Excel, PowerPoint og Outlook fra denne pakke fungerer problemfrit med [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)].

Selvom deling ansøgning om Windows RMS kan hentes og installeres på en enkelt computer ved hjælp af den [Microsoft Rights Management side](http://go.microsoft.com/fwlink/?LinkId=303970), der understøtter også en enterprise-installation til uovervåget installation og brugerdefineret konfiguration. Yderligere oplysninger finder du i følgende ressourcer:

-   [Rights Management deling program administratorvejledningen](http://technet.microsoft.com/library/dn339003.aspx)

-   [Rights Management deling program bruger guide](http://technet.microsoft.com/library/dn339006.aspx)

RMS Deling af programmer til mobile enheder, der understøtter de mest almindeligt anvendte mobile enheder, f.eks iPad og iPhone, Android, Windows Phone og Windows justerbare vinkelben Brugere kan hente denne app fra relevante butikken, og der er kæder til dem fra den [Microsoft Rights Management side](http://go.microsoft.com/fwlink/?LinkId=303970).

## <a name="BKMK_OfficeAppsIntro"></a>Office-programmer: Word, Excel, PowerPoint, Outlook
Disse programmer understøtter rettighedsstyring ved hjælp af oplysninger rights management (IRM) indbygget og lade brugerne anvende beskyttelse til et gemt dokument eller en e-mail skal sendes. Brugere kan anvende skabeloner eller vælge meget tilpassede indstillinger for begrænsninger, rettigheder, og forbrug. Brugerne kan konfigurere en fil, så det kan kun få adgang til personer i organisationen, eller kontrollere om filen kan redigeres, eller begrænset til skrivebeskyttet, eller forhindre den i at blive udskrevet. Udløbsdato for tidsafhængige filer kan konfigureres (direkte af brugerne eller ved at anvende en skabelon) for, hvornår filen kan ikke længere åbnes. Til Outlook, kan brugerne også vælge den **Videresend ikke** indstilling for at forhindre lækage af data.

### <a name="BKMK_ExchangeIntro"></a>Exchange Online og Exchange Server
Når du bruger Exchange Online eller Exchange Server, kan du bruge oplysninger rights management (IRM) integration, der indeholder løsninger til beskyttelse for yderligere oplysninger:

-   **Exchange ActiveSync IRM** så mobile enheder kan beskytte og forbruge beskyttet e-mail-meddelelser.

-   RMS-understøttelse af de **Outlook Web App**, gennemføres på samme måde til Outlook-klienten, beskyttet e-mail-meddelelser, der sendes til dem, så brugere kan beskytte e-mail-meddelelser i skabeloner eller ved at angive individuelle indstillinger, og brugerne kan læse og bruge.

-   **Beskyttelsesregler** til Outlook-klienter, at en administrator konfigurerer du anvender automatisk RMS-skabeloner til e-mail-meddelelserne til angivne modtagere. For eksempel når interne e-mails sendes til din juridiske afdeling, de kan kun læses af medlemmer af den juridiske afdeling og kan ikke sendes. Brugerne kan se den beskyttelse, der er anvendt til e-mail-meddelelse, før du sender den, og som standard, de kan fjerne det, hvis de beslutter det ikke er nødvendigt. -E-mails krypteres, før de sendes. Yderligere oplysninger finder du [Outlook-regler til beskyttelse af](http://technet.microsoft.com/library/dd638178%28v=exchg.150%29.aspx) og [oprette en regel til beskyttelse af Outlook](http://technet.microsoft.com/library/dd638196%28v=exchg.150%29.aspx) i Exchange-biblioteket.

-   **Transport regler** at en administrator konfigurerer du anvender automatisk RMS-skabeloner til e-mail meddelelser baseret på egenskaber som afsender, modtager, emne og indhold. Disse er svarer til reglerne for beskyttelse, men ikke lader brugerne fjerne beskyttelsen, kan anvendes på Outlook Web Access og e-mails, som sendes fra mobilenheder og krypterer ikke e-mail-meddelelser, før de sendes fra klienten. Yderligere oplysninger finder du i [oprette en regel til beskyttelse af Transport](http://technet.microsoft.com/library/dd302432.aspx) i Exchange-biblioteket.

-   **Datapolitikker for tab forebyggelse (DLP)** der indeholder sæt af betingelser til at filtrere e-mail-meddelelser og udføre handlinger for at forhindre tab af data for fortrolige eller følsomme indhold (eksempelvis personlige oplysninger eller kreditkortoplysninger). Tip politik kan bruges, når følsomme data, der registreres, til at advare brugerne, som de kan være nødvendigt at anvende oplysninger beskyttelse, baseret på oplysningerne i e-mailen. Yderligere oplysninger finder du i [Forhindring af datatab](http://technet.microsoft.com/library/jj150527%28v=exchg.150%29.aspx) i Exchange-biblioteket.

-   **Office 365 meddelelseskryptering** bruger transport regler til at sende krypterede e-mails til personer uden for virksomheden, og e-mailen skal skrives i en browser med en grænseflade, der svarer til Outlook Web App. Du kan tilpasse teksten til sidehovedet i krypterede e-mails i din virksomhed og ansvarsfraskrivelse tekst og endda tilføje dit firmalogo. Yderligere oplysninger finder du i [Office 365 meddelelseskryptering](http://office.microsoft.com/o365-message-encryption-FX104179182.aspx) fra Office-webstedet.

Hvis du bruger Exchange Server, kan du bruge funktionerne til databeskyttelse med [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] ved at installere RMS-stik, som fungerer som et relæ mellem dine lokale servere og RMS cloud-tjenesten. Yderligere oplysninger finder du under [Installation af Azure Rights Management-stik](../Topic/Deploying_the_Azure_Rights_Management_Connector.md).

### <a name="BKMK_SharePointIntro"></a>SharePoint Online og SharePoint Server
Når du bruger SharePoint Online eller SharePoint Server, kan du bruge oplysninger rights management (IRM) integration, som gør det muligt for administratorer med at beskytte lister eller biblioteker, så når en bruger kontrol af et dokument, filen er beskyttet, så kun autoriserede personer kan få vist og bruge filen efter beskyttelse informationspolitikker, som du angiver. For eksempel kan filen være skrivebeskyttet, deaktivere kopiering af tekst, forhindre, at gemme en lokal kopi og forhindre, at udskrive filen.

Beskyttelse af oplysninger anvendes til lister og biblioteker, altid af en administrator, aldrig en slutbruger. Og den anvendes på niveauet for listen eller biblioteket for alle dokumenter i objektbeholderen i stedet for individuelle filer.  Hvis du bruger SharePoint Online, kan brugerne også anvende IRM på deres OneDrive for Business-bibliotek.

IRM-tjeneste skal først aktiveres for SharePoint. Derefter skal angive du Information Rights Management for et bibliotek. Brugerne kan også angive Information Rights Management til deres OneDrive for Business bibliotek for SharePoint Online og OneDrive til virksomheder. SharePoint bruger ikke rettigheder politikskabeloner, selvom der er SharePoint konfigurationsindstillinger, du kan vælge, der nøje svarer til de indstillinger, du kan angive i skabeloner.

Hvis du bruger SharePoint Server, kan du bruge funktionerne til databeskyttelse med [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] ved at installere RMS-stik, som fungerer som et relæ mellem dine lokale servere og RMS cloud-tjenesten. Yderligere oplysninger finder du under [Installation af Azure Rights Management-stik](../Topic/Deploying_the_Azure_Rights_Management_Connector.md).

> [!NOTE]
> Der er i øjeblikket nogle begrænsninger, når du bruger IRM med SharePoint:
> 
> -   Du kan ikke bruge standardrapporter eller brugerdefinerede skabeloner, som du styrer på portalen Azure.
> -   Filer, der har en. PPDF filtypenavnet for beskyttet PDF-filer understøttes ikke. Filer, der har. PDF-filens filtypenavn, og som har oprindeligt beskyttet af RMS understøttes, når du bruger en PDF-læser, som oprindeligt understøtter RMS.
> -   Da Office på mobile enheder ikke understøtter endnu RMS, disse enheder skal bruge en webbrowser til at få vist filer, der er beskyttet med RMS, og filerne er skrivebeskyttede.

Azure RMS gælder brugsrestriktioner og datakryptering for dokumenter, når de er hentet fra SharePoint, og ikke, når dokumentet er første oprettes i SharePoint eller overført til biblioteket. Finde oplysninger om, hvordan dokumenter er beskyttet, før de bliver hentet, [datakryptering i OneDrive til erhvervs- og SharePoint Online](https://technet.microsoft.com/library/dn905447.aspx) fra SharePoint-dokumentationen.

Du kan finde flere oplysninger om brugen af Azure RMS med SharePoint følgende indlæg fra Office-blog: [Hvad er nyt i Information Rights Management i SharePoint og SharePoint Online](http://blogs.office.com/2012/11/09/whats-new-with-information-rights-management-in-sharepoint-and-sharepoint-online/)

## <a name="BKMK_FCIIntro"></a>Filservere, der kører Windows Server og bruge fil klassificering infrastruktur (FCI)
Når du konfigurerer Windows Server til at bruge fil klassificering infrastruktur, kan denne funktion File Server Resource Manager kan scanne lokale filer og afgøre, om de indeholder følsomme data. For filer, der opfylder dette kriterium, er de mærket med klassificeringen egenskaber, der definerer en administrator. Fil klassificering infrastruktur kan derefter tage automatiske aktioner i henhold til klassificeringen. En af disse handlinger omfatter anvendelse af beskyttelse af oplysninger ved hjælp af [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] og implementering af Rights Management-stik (også kaldet RMS-stik). Office-filer er derefter automatisk beskyttet af Azure RMS.

For at beskytte alle filtyper, du vil ikke bruge RMS-stik, men i stedet køre et Windows PowerShell-script ved hjælp af cmdlets fra den [RMS beskyttelse værktøj](https://www.microsoft.com/en-us/download/details.aspx?id=47256).

Politikker for klassificering er fuldt konfigurerbare og med fleksible udvidelsesmuligheder, så du kan forhindre potentielle data lækage fra uautoriserede og autoriserede brugere. Det kan også hjælpe med at reducere risikoen for data lækage netværksadministratorer, fordi du kan konfigurere politikker, der ikke kræver disse administratorer har adgang til filerne.

Vejledning til installation og konfiguration af RMS-stik til Office-filer finder du under [Installation af Azure Rights Management-stik](../Topic/Deploying_the_Azure_Rights_Management_Connector.md).

Vejledning til at bruge Windows PowerShell-scriptet til alle filtyper finder du under [RMS-beskyttelse med Windows Server fil klassificering infrastruktur &#40;FCI&#41;](../Topic/RMS_Protection_with_Windows_Server_File_Classification_Infrastructure__FCI_.md).

## <a name="BKMK_APIAppsIntro"></a>Andre programmer, der understøtter den RMS APIs
Ved hjælp af RMS-SDK, din interne udviklere kan skrive line of business-programmer har indbygget understøttelse af [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)]. Hvordan beskyttelse af oplysninger er integreret med programmerne afhænger af, hvordan de er skrevet. For eksempel integration automatisk kan anvendes med minimal brugerinteraktion er nødvendig, eller for en mere tilpasset oplevelse, brugerne kan blive bedt om at konfigurere indstillinger for beskyttelse af oplysninger til filer. Yderligere oplysninger om SDK finder du på [Microsoft Rights Management SDK](http://msdn.microsoft.com/library/hh552972%28v=vs.85%29.aspx).

På samme måde giver mange softwareleverandører programmer til at informere løsninger til beskyttelse, også kendt som rettigheder (ERM) produkter til virksomhedsadministration. Et populært eksempel er en PDF-læser, der understøtter [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] til bestemte platforme. Du kan bruge tabellen i den [Enheden Klientegenskaber](../Topic/Requirements_for_Azure_Rights_Management.md#BKMK_ClientCapabilities) del af den [Krav til Azure rettighedsstyring](../Topic/Requirements_for_Azure_Rights_Management.md) emne for at identificere programmer, der understøtter RMS (RMS-enlightened programmer) og derefter bruge en søgning på internettet til at købe eller hente programmet.

> [!TIP]
> Nyudgivet programmer, skal du kontrollere RMS Fællesskabet kanaler, der er angivet i [Oplysninger og Support til Azure rettighedsstyring](../Topic/Information_and_Support_for_Azure_Rights_Management.md).

## Se også
[Introduktion til Azure rettighedsstyring](../Topic/Getting_Started_with_Azure_Rights_Management.md)

