---
description: na
keywords: na
title: Deploying the Azure Rights Management Connector
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 90e7e33f-9ecc-497b-89c5-09205ffc5066
---
# Installation af Azure Rights Management-stik
Du kan bruge disse oplysninger til at få mere for at vide om Microsoft Rights Management (RMS)-stik, og hvordan du kan bruge det til at beskytte oplysninger med eksisterende lokale installationer, der bruger Microsoft Exchange Server, Microsoft SharePoint Server eller filservere, der kører Windows Server og bruge fil klassificering infrastruktur (FCI) funktion af File Server Resource Manager.

> [!TIP]
> Et detaljeret eksempel scenario med skærmbilleder, se den [Automatisk beskytte filer på filservere, der kører Windows Server og fil klassificering infrastruktur](../Topic/What_is_Azure_Rights_Management_.md#BKMK_Example_FCI) afsnit i den [Hvad er Azure Rights Management?](../Topic/What_is_Azure_Rights_Management_.md) emne.

## <a name="OverviewConnector"></a>Oversigt over Microsoft Rights Management-stik
Microsoft Rights Management (RMS)-stik, kan du hurtigt aktivere eksisterende lokale servere bruge IRM Information Rights Management () funktionalitet med skybaseret Microsoft Rights Management-tjenesten (Azure RMS). Med denne funktion kan IT og brugerne kan nemt beskytte dokumenter og billeder både inden for organisationen og udvendig, uden at skulle installere ekstra infrastruktur eller etablere tillidsforhold med andre organisationer. Du kan bruge denne forbindelse, selvom nogle af brugerne opretter forbindelse til online-tjenester i et scenarie med hybrid. For eksempel nogle brugernes postkasser bruge Exchange Online og nogle brugernes postkasser bruge Exchange Server. Når du installere RMS-tilslutning, alle brugere kan beskytte og forbruge e-mails og vedhæftede filer ved hjælp af Azure RMS og beskyttelse af oplysninger fungerer problemfrit mellem to installationskonfigurationer.

RMS-connector er en lille flademål-tjeneste, du installerer på stedet, på servere, der kører Windows Server 2012 R2, Windows Server 2012 eller Windows Server 2008 R2. Ud over kører forbindelsen på fysiske computere, kan du også køre den på virtuelle maskiner, herunder Azure IaaS FOS. Når du installerer og konfigurerer forbindelsen, fungerer den som kommunikation interface (relay) mellem de lokale servere og cloud-tjeneste.

Hvis du administrerer din egen nøgle lejer for Azure RMS (den Medbring, du ejer nøglen eller BYOK scenario), RMS-stik og de lokale servere, der bruger den ikke adgang hardware Sikkerhedsmodulet (HSM), der indeholder din nøgle til lejeradministration. Dette er fordi alle kryptografiske handlinger, der bruger nøglen lejer udføres i Azure RMS og ikke på stedet.

![](../Image/RMS_connector.png)

RMS-stik understøtter følgende lokale servere: Exchange Server, SharePoint Server og filservere, der kører Windows Server og bruge fil klassificering infrastruktur til at klassificere og Anvend politikker for Office-dokumenter i en mappe. Hvis du vil beskytte alle filtyper ved hjælp af filen klassificering, Brug ikke RMS-stik, men i stedet bruge de [beskyttelse af RMS-cmdletter](https://msdn.microsoft.com/library/azure/mt433195.aspx).

> [!NOTE]
> Understøttede versioner af disse lokale servere, finder du under "lokale servere, der understøtter Azure RMS" i den [Programmer, der understøtter Azure RMS](../Topic/Requirements_for_Azure_Rights_Management.md#BKMK_SupportedApplications) del af den [Krav til Azure rettighedsstyring](../Topic/Requirements_for_Azure_Rights_Management.md) emne.

Brug de følgende afsnit til at hjælpe dig med at planlægge, installere og konfigurere RMS-stik. Derefter skal du gøre nogle installationskonfiguration af indlæg, så dine servere kan bruge forbindelsen.

-   [Prerequisites for the RMS connector](../Topic/Deploying_the_Azure_Rights_Management_Connector.md#BKMK_Prereqs)

-   **Trin 1:**  [Installing the RMS connector](../Topic/Deploying_the_Azure_Rights_Management_Connector.md#BKMK_InstallingConnector)

-   **Trin 2:**  [Entering credentials](../Topic/Deploying_the_Azure_Rights_Management_Connector.md#EnteringCredentials)

-   **Trin 3:**  [Authorizing servers to use the RMS connector](../Topic/Deploying_the_Azure_Rights_Management_Connector.md#AuthorizingServers)

-   **Trin 4:**  [Configuring load balancing and high availability](../Topic/Deploying_the_Azure_Rights_Management_Connector.md#ConfiguringConnector)

-   Valgfrit: [Configuring the RMS connector to use HTTPS](../Topic/Deploying_the_Azure_Rights_Management_Connector.md#BKMK_ConfiguringHTTPS)

-   Valgfrit: [Configuring the RMS connector for a web proxy server](../Topic/Deploying_the_Azure_Rights_Management_Connector.md#BKMK_ConfiguringWebProxy)

-   Valgfrit: [Installing the RMS connector administration tool on administrative computers](../Topic/Deploying_the_Azure_Rights_Management_Connector.md#BKMK_InstallingStandaloneTool)

-   **Trin 5:**  [Configuring servers to use the RMS connector](../Topic/Deploying_the_Azure_Rights_Management_Connector.md#ConfiguringServers)

    -   [Configuring an Exchange server to use the connector](../Topic/Deploying_the_Azure_Rights_Management_Connector.md#BKMK_ExchangeServer)

    -   [Configuring a SharePoint server to use the connector](../Topic/Deploying_the_Azure_Rights_Management_Connector.md#BKMK_ConfiguringSharePoint)

    -   [Configuring a file server for File Classification Infrastructure to use the connector](../Topic/Deploying_the_Azure_Rights_Management_Connector.md#BKMK_FileServer)

-   [Next steps](../Topic/Deploying_the_Azure_Rights_Management_Connector.md#BKMK_NextSteps)

## <a name="BKMK_Prereqs"></a>Forudsætninger for RMS-stik
Før du installerer connector RMS, Sørg for, at følgende krav er på plads.

|Kravet om|Yderligere oplysninger|
|-------------|--------------------------|
|Tjenesten Rights Management (RMS) er aktiveret|[Aktivering af Azure rettighedsstyring](../Topic/Activating_Azure_Rights_Management.md)|
|Katalogsynkronisering mellem Active Directory-områder og Azure Active Directory|Når RMS er aktiveret, skal der være konfigureret Azure Active Directory for at arbejde med brugere og grupper i Active Directory-databasen. **Important:** Du skal gøre dette bibliotek synkronisering trin RMS Connector til at arbejde, selv for en test-netværk. Selvom du kan bruge Office 365 og Azure Active Directory ved hjælp af konti, som du opretter manuelt i Azure Active Directory, kræver denne forbindelse, at kontiene i Azure Active Directory er synkroniseret med Active Directory-domæneservices; synkronisering af manuel adgangskoder er ikke tilstrækkeligt.<br />Yderligere oplysninger finder du i følgende ressourcer:<br /><br />-   [Instruktioner til konfiguration af dit AD Azure lejer](http://technet.microsoft.com/library/hh967611.aspx)<br />-   [Instruktioner for at aktivere katalogsynkronisering med AAD ved hjælp af DirSync](http://technet.microsoft.com/library/hh967642.aspx)|
|Valgfrit, men anbefales:<br /><br />-   Aktiver organisationsnetværk mellem din lokale Active Directory og Azure Active Directory|Du kan aktivere samling af identiteter mellem den lokale mappe og Azure Active Directory. Denne konfiguration giver en mere problemfri brugeroplevelse ved hjælp af single sign-on til RMS-tjenesten. Uden single sign-on bedt brugerne om deres legitimationsoplysninger, før de kan bruge rettighedsbeskyttede indhold.<br /><br />Instruktioner til at konfigurere organisationsnetværk ved hjælp af Active Directory Federation Services (AD FS) mellem Active Directory-domæneservices og Azure Active Directory finder du på [Tjekliste: Brug AD FS til at implementere og administrere single sign-on-](http://technet.microsoft.com/library/jj205462.aspx) i Windows Server-biblioteket.|
|Mindst to medlemscomputere, du vil installere RMS-tilslutning:<br /><br /><ul><li>En 64-bit fysisk eller virtuel computer, der kører et af følgende operativsystemer:<br /><br /><ul><li>Windows Server 2012 R2</li><li>Windows Server 2012</li><li>Windows Server 2008 R2</li></ul></li><li>Mindst 1 GB RAM</li><li>Mindst 64 GB plads på harddisken</li><li>Mindst ét netværkskort</li><li>Adgang til internettet via en firewall (eller en webproxy), der ikke kræver godkendelse</li><li>Skal være i en skov eller et domæne, der har tillid til andre områder i organisationen, som indeholder installationer af Exchange eller SharePoint-servere, du vil bruge med RMS-stik</li></ul>|For fejltolerance og høj tilgængelighed, skal du installere RMS-connector på mindst to computere. **Tip:** Hvis du bruger Outlook Web Access eller mobile enheder, der bruger Exchange ActiveSync IRM, og det er vigtigt, at du har adgang til e-mails og vedhæftede filer, der er beskyttet af Azure RMS, anbefaler vi, at du implementerer en NLB-gruppe connector servere, der sikrer høj tilgængelighed.<br />Du behøver ikke dedikerede servere til at køre på forbindelsen, men du skal installere det på en separat computer fra de servere, der bruger forbindelsen. **Important:** Ikke Installer connector på en computer, der kører Exchange Server, SharePoint Server eller en filserver, der er konfigureret for infrastruktur for klassificering af filen, hvis du vil bruge funktionaliteten fra disse tjenester med Azure RMS. Desuden Installer ikke denne forbindelse på en domænecontroller.|

## <a name="BKMK_InstallingConnector"></a>Installere RMS-stik
Efter du har bekræftet, at forudsætningerne i det foregående afsnit, kan du bruge følgende instruktioner til at installere RMS-tilslutning:

1.  Identificere computere (mindst to), der kører på RMS-forbindelsen. De skal opfylde minimum specifikation er anført i det foregående afsnit.

    > [!NOTE]
    > Du installerer et enkelt RMS-stik (bestående af flere servere med høj tilgængelighed) pr. lejer (Office 365 lejer eller Azure AD lejer). I modsætning til Active Directory-RMS har du ikke at installere RMS-stik i hvert område.

2.  Hente kildefilerne til RMS-stikket fra den [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=314106).

    For at installere RMS-tilslutning, skal du hente RMSConnectorSetup.exe.

    Derudover gælder følgende:

    -   Hvis du senere vil konfigurere stikket fra en 32-bit computer, skal du også hente RMSConnectorAdminToolSetup_x86.exe.

    -   Hvis du vil bruge værktøjet til konfiguration af serveren til RMS-forbindelsen, hvis du vil automatisere konfigurationen af indstillingerne i registreringsdatabasen på du lokale servere, også hente GenConnectorConfig.ps1.

3.  Kør på den computer, hvor du vil installere RMS-tilslutning, **RMSConnectorSetup.exe** med administratorrettigheder.

4.  Vælg på siden Velkommen på siden Microsoft Rights Management Connector Installation **installere Microsoft Rights Management-stik på computeren**, og klik derefter på **Næste**.

5.  Læse og acceptere licensbetingelserne RMS-stik, og klik derefter på **Næste**.

Angiv en konto og adgangskode for at konfigurere RMS connector for at fortsætte.

## <a name="EnteringCredentials"></a>At angive legitimationsoplysninger
Før du kan konfigurere RMS-stik, skal du angive legitimationsoplysninger for en konto med tilstrækkelige rettigheder til at konfigurere RMS-stik.

Hvis du har implementeret desuden [onboarding af kontrolelementer](https://technet.microsoft.com/library/jj658941.aspx), skal du sørge for, at den konto, du angiver er i stand til at beskytte indholdet. Begrænset mulighed for at beskytte indhold til gruppen "IT-afdelingen" kan være den konto, du angiver her, medlem af gruppen. Hvis ikke, vises fejlmeddelelsen: **Der blev ikke finde placeringen af administrationstjenesten og organisation. Kontroller, at Microsoft Rights Management-tjenesten er aktiveret for din organisation.**

Du kan bruge en konto med en af følgende rettigheder:

-   **Office 365-lejeadministratoren**: En konto, der er en global administrator for din Office 365-lejer.

-   **Microsoft RMS lejer Global Administrator**: En konto med administratorrettigheder på Microsoft RMS forpagteren.

-   **Microsoft RMS connector Administrator**: En konto i Azure Active Directory, der har fået tildelt rettigheder til at installere og administrere RMS-tilslutning til organisationen.

    > [!NOTE]
    > Hvis du vil bruge Microsoft RMS connector administratorkonto, skal du først gøre følgende for at tildele administratorrollen RMS-stik:
    > 
    > 1.  På den samme computer, skal du hente og installere Windows PowerShell til Rights Management. Yderligere oplysninger finder du under [Installation af Windows PowerShell til Azure rettighedsstyring](../Topic/Installing_Windows_PowerShell_for_Azure_Rights_Management.md).
    > 
    >     Start Windows PowerShell med de **Kør som administrator** kommandoen og oprette forbindelse til tjenesten Azure RMS ved hjælp af den [Connect-AadrmService](http://msdn.microsoft.com/library/windowsazure/dn629415.aspx) kommando:
    > 
    >     ```
    >     Connect-AadrmService                   //provide Office365 Tenant Administrator or Microsoft RMS Tenant Global Administrator credential
    >     ```
    > 2.  Kør derefter den [Tilføj AadrmRoleBasedAdministrator](http://msdn.microsoft.com/library/windowsazure/dn629417.aspx) kommandoen ved hjælp af kun én af følgende parametre:
    > 
    >     ```
    >     Add-AadrmRoleBasedAdministrator -EmailAddress <email address> -Role "ConnectorAdministrator"
    >     ```
    > 
    >     ```
    >     Add-AadrmRoleBasedAdministrator -ObjectId <object id> -Role "ConnectorAdministrator"
    >     ```
    > 
    >     ```
    >     Add-AadrmRoleBasedAdministrator -SecurityGroupDisplayName <group Name> -Role "ConnectorAdministrator"
    >     ```
    >     For eksempel, skal du skrive: **Add-AadrmRoleBasedAdministrator -EmailAddress melisa@contoso.com -Role " ConnectorAdministrator "**
    > 
    >     Men disse kommandoer bruges rollen som ConnectorAdministrator, kan du også bruge GlobalAdministrator rolle her, også.

Under installationsprocessen RMS forbindelsen er godkendt og installeret alle de nødvendige software, Internet Information Services (IIS) installeres, hvis det ikke allerede er til stede og connector softwaren er installeret og konfigureret. RMS er desuden rede for konfiguration ved at oprette følgende:

-   En tom tabel servere, der har tilladelse til at bruge forbindelsen til at kommunikere med Azure RMS. Du kan tilføje servere til denne tabel senere.

-   Et sæt af sikkerhedstokens for forbindelsen, som tillader transaktioner med Azure RMS. Disse symboler er hentet fra RMS Azure og installeret på den lokale computer i registreringsdatabasen. De er beskyttet ved hjælp af det data protection application programming interface (DPAPI) og lokale System konto legitimationsoplysninger.

Benyt følgende fremgangsmåde på den sidste side i guiden, og klik derefter på **er færdig med**:

-   Hvis dette er den første forbindelse, du har installeret, skal du ikke markere **Launch connector-administratorkonsollen at autorisere servere** på nuværende tidspunkt. Du vælger denne indstilling, når du har installeret den anden (eller sidste) RMS-forbindelse. I stedet køre guiden igen på mindst én anden computer. Du skal installere mindst to stik.

-   Hvis du har installeret den anden (eller sidste) forbindelse, vælge **Launch connector-administratorkonsollen at autorisere servere**.

> [!TIP]
> På dette tidspunkt er der en kontrolprøve, som du kan udføre for at teste, om webtjenester til RMS-forbindelsen er funktionsdygtige:
> 
> -   En webbrowser til at oprette forbindelse til **http://&lt;connectoraddress&gt;/_wmcs/certification/servercertification.asmx**, erstatte *&lt; connectoraddress &gt;* med serveradresse eller navn, der har den RMS-stik, der er installeret. En vellykket forbindelse viser et **ServerCertificationWebService** side.

Hvis du vil fjerne forbindelsen RMS, Kør guiden igen, og vælg indstillingen Fjern.

## <a name="AuthorizingServers"></a>Godkendelse af serverne til at bruge RMS-stik
Når du har installeret RMS-connector på mindst to computere, er du klar til at godkende servere og tjenester, som du vil bruge RMS-forbindelse. For eksempel servere, som kører Exchange Server 2013 eller SharePoint Server 2013.

For at definere disse servere skal køre værktøjet til webstedsadministration RMS-stik og føje poster til listen over tilladte servere. Du kan køre dette værktøj, når du vælger **Launch connector Administrationskonsol til at godkende servere** i slutningen af Microsoft Rights Management connector installation guide, eller du kan køre det separat fra guiden.

Når du godkender disse servere, kan du være opmærksom på følgende overvejelser:

-   Servere, som du tilføjer tildeles særlige rettigheder. Alle konti, du angiver for Exchange Server-rolle i connector-konfiguration, der skal tildeles de [super brugerrolle](https://technet.microsoft.com/library/mt147272.aspx) i Azure RMS, som giver dem adgang til alt indhold til denne RMS lejer. Superbruger-funktionen aktiveres automatisk på dette tidspunkt, hvis det er nødvendigt. For at undgå sikkerhedsrisikoen i udvidelse af rettigheder skal være omhyggelig med at angive kun de konti, der bruges af Exchange-servere i din organisation. Almindelige brugerrettigheder tildeles alle de servere, der er konfigureret som SharePoint-servere eller filservere, der bruger FCI.

-   Du kan tilføje flere servere som en enkelt post, ved at angive en Active Directory-sikkerhed eller distributionsgruppe eller en tjenestekonto, der bruges af mere end én server. Når du bruger denne konfiguration, gruppen af servere deler de samme RMS-certifikater og alle betragtes som ejere for indhold, som nogle af dem har beskyttet. For at minimere administrative udgifter, anbefaler vi, at du bruger denne konfiguration af en enkelt gruppe i stedet for individuelle servere til at godkende virksomhedens Exchange-servere eller en SharePoint-serverfarm.

På den **servere mulighed for at udnytte forbindelsen** skal du klikke på **Tilføj**.

### <a name="BKMK_AddServer"></a>Føje en server til listen over tilladte servere
På den **tillader en server for at udnytte forbindelsen** side, Indtast navnet på objektet eller Gennemse for at identificere objektet til at autorisere.

Det er vigtigt, at du godkender det rette objekt. For en server til at bruge forbindelsen, skal den konto, der kører tjenesten på stedet (for eksempel Exchange eller SharePoint) vælges til godkendelse. Hvis tjenesten kører som en tjenestekonto, der er konfigureret, f.eks navnet på service-kontoen på listen. Hvis tjenesten kører som lokalt System, kan du tilføje navnet på computerobjektet (servernavn kr). Oprette en gruppe, der indeholder disse konti som best practice, og angive gruppen i stedet for individuelle servernavne.

Yderligere oplysninger om de forskellige serverroller:

-   For servere, der kører Exchange: Du skal angive en sikkerhedsgruppe, og du kan bruge standardgruppe (**Exchange-servere**), som Exchange automatisk opretter og vedligeholder alle Exchange-servere i skoven.

-   For servere, der kører SharePoint:

    -   Hvis et SharePoint 2010-serveren er konfigureret til at køre som lokalt System (det ikke bruger en tjenestekonto), oprette en sikkerhedsgruppe i Active Directory-domæneservices manuelt og tilføje navn computerobjektet for serveren i denne konfiguration til denne gruppe.

    -   Hvis en SharePoint-server er konfigureret til at bruge en tjenestekonto (den anbefalede praksis til SharePoint 2010) og den eneste mulighed for SharePoint 2013, kan du gøre følgende:

        1.  Føje den tjenestekonto, der kører tjenesten SharePoint Central Administration for at aktivere SharePoint konfigureres fra dens administratorkonsollen.

        2.  Føje den konto, der er konfigureret til SharePoint App Pool.

        > [!TIP]
        > Hvis disse to konti er forskellige, kan du overveje at oprette en enkelt gruppe, der indeholder begge konti for at minimere de administrative udgifter.

-   De tilknyttede tjenester kører filservere, der bruger filen klassificering infrastrukturen, som kontoen Lokalt System, så du skal tillade computerkontoen til filservere (servernavn kr) eller en gruppe, der indeholder disse computerkonti.

Når du er færdig med at tilføje servere på listen, skal du klikke på **Luk**.

Hvis du ikke allerede har gjort det, skal du nu konfigurere belastningsjustering for de servere, der har RMS-connector installeret og overvejer at bruge HTTPS til forbindelser mellem disse servere og servere, som du lige har tilladelse.

## <a name="ConfiguringConnector"></a>Konfiguration af belastning modkontoen og høj tilgængelighed
Når du har installeret den anden eller endelige forekomst af RMS-stik, definere et stik URL-servernavn og konfigurere et system til belastningsjustering.

Servernavnet connector URL-adresse kan være et vilkårligt navn under et navneområde, du styrer. For eksempel kunne du oprette en post i DNS-systemet for **rmsconnector.contoso.com** og konfigurere denne post for at bruge en IP-adresse i systemet til belastningsjustering. Der er ingen særlige krav til dette navn, og det skal ikke konfigureres på connector-serverne. Medmindre dine Exchange- og SharePoint-servere vil være kommunikerer med forbindelsen via internettet, har dette navn ikke løses på internettet.

> [!IMPORTANT]
> Vi anbefaler, at du ikke ændre dette navn, når du har konfigureret Exchange eller SharePoint-servere for at kunne bruge forbindelsen, fordi du skal derefter fjerne markeringen i disse alle konfigurationer af IRM-servere og konfigurere dem igen.

Når navnet er oprettet i DNS og er konfigureret til en IP-adresse, kan du konfigurere belastningsjustering for adressen, der dirigerer trafik til connector-servere. Du kan bruge et hvilket som helst IP-baserede belastning til dette formål, som indeholder funktionen netværk indlæses afstemning (NLB) i Windows Server. Yderligere oplysninger finder du i [Load Balancing Deployment Guide](http://technet.microsoft.com/library/cc754833%28v=WS.10%29.aspx).

Brug følgende indstillinger til at konfigurere NLB-klyngen:

-   Porte: 80 (for HTTP) eller 443 (til HTTPS)

    Du kan finde flere oplysninger om, om du vil bruge HTTP eller HTTPS i næste afsnit.

-   Tilhørsforhold: Ingen

-   Metode til softwaredistribution: Er lig med

Dette navn, du definerer for NLB-systemet (til servere, som kører tjenesten RMS connector) er navnet på organisationen RMS-stik, du vil bruge senere, når du konfigurerer de lokale servere bruge Azure RMS.

## <a name="BKMK_ConfiguringHTTPS"></a>Konfiguration af RMS-forbindelsen for at bruge HTTPS
> [!NOTE]
> Denne konfigurationstrin er valgfrit, men anbefales for ekstra sikkerhed.

Men brug af TLS eller SSL er valgfrit for RMS-forbindelse, anbefaler vi det til alle HTTP-baseret sikkerhedsfølsomme service. Denne konfiguration godkender de servere, der kører forbindelse til din Exchange- og SharePoint-servere, der bruger forbindelsen. Derudover kan alle data, der sendes fra disse servere til forbindelsen er krypteret.

For at aktivere RMS connector til at bruge TLS, på hver server, der kører på RMS-forbindelsen, skal du installere et servercertifikat til godkendelse, der indeholder det navn, du vil bruge til forbindelsen. For eksempel, hvis din RMS-connector navn, du har defineret i DNS er **rmsconnector.contoso.com**, installere et servercertifikat til godkendelse, der indeholder **rmsconnector.contoso.com** i certifikatets emne som det almindelige navn. Angive **rmsconnector.contoso.com** i alternative navnet på certifikatet som DNS-værdi. Certifikatet har ikke at medtage navnet på serveren. Derefter i IIS, binde dette certifikat på standardwebstedet.

Hvis du bruger HTTPS-indstilling, kan du sikre, at alle servere, der kører forbindelsen har et gyldigt server-godkendelse, certifikat, som er knyttet til et rodnøglecenter, der er tillid til dine Exchange- og SharePoint-servere. Desuden Hvis nøglecenter (CA), der har udstedt certifikater til connector-servere udgiver en liste over tilbagekaldte certifikater (CRL), skal Exchange og SharePoint-servere kunne hente denne liste over tilbagekaldte certifikater.

> [!TIP]
> Du kan bruge følgende oplysninger og ressourcer til at hjælpe dig med at anmode om og installere et servercertifikat til godkendelse, og at binde dette certifikat til standard-webstedet i IIS:
> 
> -   Hvis du bruger Active Directory-certifikattjenester (AD CS) og et virksomhedsnøglecenter (CA) til at installere disse certifikater til servergodkendelse, kan du kopiere og derefter bruge certifikatskabelon webserver. Denne certifikatskabelon bruger **angivet i anmodningen** til navnet på certifikatholderen, hvilket betyder, at du kan angive FQDN RMS forbindelse navn til certifikatets emnenavn eller alternative emnenavn, når du anmoder om certifikatet.
> -   Hvis du bruger et separat Nøglecenter eller købe dette certifikat fra et andet firma, se [certifikater for konfiguration af Internet Server (IIS 7)](http://technet.microsoft.com/library/cc731977%28v=ws.10%29.aspx) i den [Web Server (IIS)](http://technet.microsoft.com/library/cc753433%28v=ws.10%29.aspx) dokumentbibliotek på TechNet.
> -   For at konfigurere IIS til at bruge certifikatet, se [tilføje en Binding til et websted (IIS 7)](http://technet.microsoft.com/library/cc731692.aspx) i den i den [Web Server (IIS)](http://technet.microsoft.com/library/cc753433%28v=ws.10%29.aspx) dokumentbibliotek på TechNet.

## <a name="BKMK_ConfiguringWebProxy"></a>Konfiguration af RMS-tilslutning til en Web-proxy-server
Hvis serverne connector er installeret i et netværk, der ikke har direkte forbindelse til internettet og kræver manuel konfiguration af en Web-proxy-server til udgående adgang til internettet, skal du konfigurere registreringsdatabasen på serverne til RMS-connector.

#### Sådan konfigureres RMS-forbindelsen for at bruge en web-proxyserver

1.  På hver server, der kører på RMS-forbindelsen, ved at åbne Registreringseditor, såsom Regedit.

2.  Gå til **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\AADRM\Connector**

3.  Tilføje strengværdien af **ProxyAddress** og derefter angive Data for denne værdi skal være **-http://&lt;MyProxyDomainOrIPaddress&gt;:&lt;MyProxyPort&gt;**

    For eksempel: **http://proxyserver.contoso.com:8080**

4.  Luk Registreringseditor, og genstart serveren eller udføre kommandoen IISReset for at genstarte IIS.

## <a name="BKMK_InstallingStandaloneTool"></a>Installation af værktøjet til webstedsadministration RMS-stik på administrative computere
Du kan køre værktøjet til webstedsadministration RMS-stik fra en computer, der ikke har RMS connector er installeret, hvis computeren opfylder følgende krav:

-   En fysisk eller virtuel computer, der kører Windows Server 2012 eller Windows Server 2012 R2 (alle udgaver), Windows Server 2008 R2 eller Windows Server 2008 R2 Service Pack 1 (alle udgaver), Windows 8.1, Windows 8 eller Windows 7.

-   Mindst 1 GB RAM.

-   Mindst 64 GB plads på harddisken.

-   Mindst en netværksgrænseflade.

-   Adgang til internettet via en firewall (eller en webproxy).

For at installere værktøjet til webstedsadministration RMS-stik, skal du køre følgende filer:

-   En 32-bit-computer: RMSConnectorAdminToolSetup_x86.exe

-   En 64-bit-computer: RMSConnectorSetup.exe

Hvis du ikke har allerede hentet disse filer, kan du gøre det fra den [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=314106).

## <a name="ConfiguringServers"></a>Konfiguration af serverne til at bruge RMS-stik
Når du har installeret og konfigureret RMS-stik, er du klar til at konfigurere dine lokale servere, der bruger Rights Management og oprette forbindelse til Azure RMS ved hjælp af forbindelsen. Det betyder, at du konfigurerer følgende servere:

-   For Exchange-2013: Client access-servere og postkasse-servere

-   Til Exchange 2010: Client access-servere og servere, hub transport

-   For SharePoint: Front-end-SharePoint-webservers, herunder dem, der er vært for Central Administration af serveren

-   Filen klassificering infrastruktur: Windows Server-computere, der har installeret filen Resource Manager

Denne konfiguration kræver indstillinger i registreringsdatabasen. Hvis du vil gøre dette, har du to muligheder:

|Konfigurationsindstillingen|Fordele|Ulemper|
|-------------------------------|-----------|-----------|
|Automatisk ved hjælp af værktøjet til konfiguration af serveren til Microsoft RMS-stik|Ingen direkte redigering af registreringsdatabasen. Dette er automatiseret ved hjælp af et script.<br /><br />Du behøver ikke at køre en Windows PowerShell-cmdlet for at få din Microsoft RMS URL-adresse.<br /><br />Forudsætningerne kontrolleres automatisk, (men ikke automatisk remediated) Hvis du Kør det lokalt.|Når du kører værktøjet, skal du oprette en forbindelse til en server, der allerede kører på RMS-forbindelsen.|
|Manuelt ved at redigere registreringsdatabasen|Der kræves ingen forbindelse til en server, der kører på RMS-forbindelsen.|Yderligere administrative udgifter, der er følsom over for fejl.<br /><br />Du skal have Microsoft RMS URL-adressen, som kræver, at du kører en Windows PowerShell-kommando.<br /><br />Du skal foretage alle forudsætninger check altid selv.|
> [!IMPORTANT]
> I begge tilfælde skal du manuelt installere eventuelle krav og konfigurere Exchange, SharePoint og fil klassificering infrastruktur for at bruge Rights Management.

I de fleste organisationer bliver automatisk konfiguration ved hjælp af værktøjet til konfiguration af serveren til Microsoft RMS connector bedre mulighed, fordi det giver større effektivitet og pålidelighed end manuel konfiguration.

Når du har foretaget ændringerne i konfigurationen på disse servere, du skal genstarte dem, hvis de kører Exchange eller SharePoint og tidligere konfigureret til at bruge AD RMS. Det er ikke nødvendigt at genstarte disse servere, hvis du konfigurerer dem til Rights Management for første gang. Du skal altid genstarte filserver, der er konfigureret til at bruge fil klassificering infrastruktur, når du har foretaget disse konfigurationsændringer.

#### Sådan bruges værktøjet til konfiguration af serveren til Microsoft RMS-stik

1.  Hvis du ikke har allerede hentet script til værktøjet til konfiguration af serveren til Microsoft RMS connector (GenConnectorConfig.ps1), kan du hente den fra den [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=314106).

2.  Gem filen GenConnectorConfig.ps1 på computeren, hvor du vil køre værktøjet. Hvis du vil køre værktøjet lokalt, skal dette være den server, du vil konfigurere til at kommunikere med RMS-stik. Ellers kan du gemme den på enhver computer.

3.  Beslutte, hvordan du kører værktøjet:

    -   **Lokalt**: Du kan køre værktøjet interaktivt, fra serveren skal være konfigureret til at kommunikere med RMS-stik. Dette er nyttigt for en engangs-konfiguration, som et testmiljø.

    -   **Softwareinstallation**: Du kan køre værktøjet til at producere registreringsdatabasefiler, du derefter anvender en eller flere af de relevante servere ved hjælp af et systems management-program, der understøtter softwareinstallation, som System Center Konfigurationsstyring.

    -   **Gruppepolitik**: Du kan køre værktøjet til at oprette et script, som du giver en administrator, der kan oprette Gruppepolitik objekter-servere skal være konfigureret. Dette script opretter en Gruppepolitik objekt for hver enkelt server konfigureres, som administratoren kan derefter tildele til de relevante servere.

    > [!NOTE]
    > Dette værktøj konfigurerer servere, der skal kommunikere med RMS-stik, og som står i begyndelsen af dette afsnit. Undlad at køre dette værktøj på de servere, der kører på RMS-forbindelsen.

4.  Start Windows PowerShell med de **køre som administrator** indstilling, og kommandoen Get-help for at få instruktioner Sådan bruges værktøjet til din valgte konfigurationsmetode:

    ```
    Get-help .\GenConnectorConfig.ps1 -detailed
    ```

Når værktøjet er kørt, bedt om at indtaste Webadressen til RMS-forbindelsen for din organisation. Angiv protokolpræfikset (HTTP:// eller HTTPS://) og navnet på den forbindelse, du har defineret i DNS for \\\load balanceres adressen på din forbindelse. For example, https://connector.contoso.com. Værktøjet derefter bruger denne URL-adresse til at kontakte de servere, der kører på RMS-forbindelsen og få andre parametre, der bruges til at oprette de nødvendige konfigurationer.

> [!IMPORTANT]
> Når du kører dette værktøj, Sørg for, at du angiver navnet på RMS NLB-forbindelsen for din virksomhed og ikke navnet på en enkelt server, der kører tjenesten RMS connector.

Brug de følgende afsnit til bestemte oplysninger for hver tjenestetype:

-   [Configuring an Exchange server to use the connector](../Topic/Deploying_the_Azure_Rights_Management_Connector.md#BKMK_ExchangeServer)

-   [Configuring a SharePoint server to use the connector](../Topic/Deploying_the_Azure_Rights_Management_Connector.md#BKMK_ConfiguringSharePoint)

-   [Configuring a file server for File Classification Infrastructure to use the connector](../Topic/Deploying_the_Azure_Rights_Management_Connector.md#BKMK_FileServer)

> [!NOTE]
> Når disse servere er konfigureret til at bruge stikket, fungerer muligvis ikke klientprogrammer, der er installeret lokalt på disse servere med RMS. Når dette sker, skyldes det, at programmerne, der forsøger at bruge forbindelsen i stedet for at bruge RMS direkte, som ikke understøttes.
> 
> Desuden Hvis Office 2010 er installeret lokalt på en Exchange-server, den klient app IRM-funktioner fungerer muligvis fra den pågældende computer når serveren er konfigureret til at bruge forbindelsen, men dette understøttes ikke.
> 
> I begge scenarier, skal du installere klientprogrammer på separate computere, der ikke er konfigureret til at bruge forbindelsen. De korrekt bruger derefter RMS direkte.

### <a name="BKMK_ExchangeServer"></a>Konfiguration af en Exchange-server for at bruge connector
Følgende Exchange roller kommunikere med RMS-stik:

-   For Exchange-2013: Client access server og postkasseserveren

-   Til Exchange 2010: Client access server og hub transport-server

Hvis du vil bruge RMS-stik, skal disse Exchange-servere køre en af følgende softwareversioner:

-   Exchange Server med Exchange 2013 kumulative opdatering 3 2013

-   Exchange Server 2010 med opdatering af Exchange 2010 Service Pack 3 opdateringspakke 6

Du skal også installere på disse servere, en version af RMS-klienten, der indeholder understøttelse af RMS kryptografiske tilstand 2. Den mindste version, der understøttes i Windows Server 2008 er inkluderet i et hotfix, som du kan hente fra [RSA nøglelængde øges til 2048 bit AD RMS i Windows Server 2008 R2 og Windows Server 2008](http://support.microsoft.com/kb/2627272). Den mindste version til Windows Server 2008 R2 kan downloades fra [RSA nøglelængde øges til 2048 bit AD RMS i Windows 7 eller Windows Server 2008 R2](http://support.microsoft.com/kb/2627273). 2012 til Windows Server og Windows Server 2012 R2 har indbygget understøttelse af kryptografiske tilstand 2.

> [!IMPORTANT]
> Hvis disse versioner eller nyere versioner af Exchange og RMS-klienten ikke er installeret, kan du ikke konfigurere Exchange for at bruge connector. Kontroller, at disse versioner er installeret, før du fortsætter.

##### Konfiguration af Exchange-servere for at bruge connector

1.  Benyt en af følgende på de Exchange-serverroller, der kommunikerer med RMS-stik:

    -   Køre serveren configuration tool for Microsoft RMS-stik. Yderligere oplysninger finder du [How to use the server configuration tool for Microsoft RMS connector](../Topic/Deploying_the_Azure_Rights_Management_Connector.md#BKMK_HowToRunTheTool) i dette emne.

    -   Foretage manuelle ændringer ved hjælp af tabellerne i de følgende afsnit til manuelt for at føje indstillinger i registreringsdatabasen på serverne.

2.  Aktivere IRM-funktionaliteten i Exchange. Yderligere oplysninger finder du i [procedurer for administration af oplysninger rettigheder](https://technet.microsoft.com/library/dd351212%28v=exchg.150%29.aspx) i Exchange-biblioteket.

Kun, hvis du vil tilføje eller kontrollere indstillingerne i registreringsdatabasen på disse servere, som konfigurerer serverne til at bruge RMS forbindelsen manuelt, skal du bruge tabellerne i de følgende afsnit. Instruktioner i, når du bruger disse tabeller:

-   *MicrosoftRMSURL* er URL-adressen til din organisation Microsoft RMS-service. At finde denne værdi:

    1.  Kør den [få AadrmConfiguration](http://msdn.microsoft.com/library/windowsazure/dn629410.aspx) cmdlet til Azure RMS. Hvis du ikke allerede er installeret Windows PowerShell-modul til Azure RMS, se [Installation af Windows PowerShell til Azure rettighedsstyring](../Topic/Installing_Windows_PowerShell_for_Azure_Rights_Management.md).

    2.  Fra outputtet, identificere de **LicensingIntranetDistributionPointUrl** værdi.

        For eksempel: **LicensingIntranetDistributionPointUrl: https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com/_wmcs/licensing**

    3.  Fjerne fra værdien, **/_wmcs/licens** fra denne streng. Den resterende streng er din URL-adresse til Microsoft-RMS. I vores eksempel er den URL-adresse til Microsoft-RMS følgende værdi:

        **https://5c6bb73b-1038-4eec-863d-49bded473437.RMS.NA.aadrm.com**

-   *ConnectorFQDN* er navnet belastningsfordeling, du har defineret i DNS for forbindelsen. For eksempel **rmsconnector.contoso.com**.

-   Bruge præfikset HTTPS connector URL-adresse, hvis du har konfigureret forbindelsen for at bruge HTTPS til at kommunikere med dine lokale servere. Yderligere oplysninger finder du i [Configuring the RMS connector to use HTTPS](../Topic/Deploying_the_Azure_Rights_Management_Connector.md#BKMK_ConfiguringHTTPS) afsnit i dette emne. De URL-adresser til Microsoft-RMS Brug altid HTTPS.

#### Tabel for Exchange 2013 indstillinger i registreringsdatabasen

|Sti til registreringsdatabasen|Type|Værdi|Data|
|----------------------------------|--------|---------|--------|
|HKEY_LOCAL_MACHINE\Software\Microsoft\MSDRM\ServiceLocation\Activation|Reg_SZ|Standard|https://*_wmcs/MicrosoftRMSURL/certificering*|
|HKEY_LOCAL_MACHINE\Software\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing|Reg_SZ|Standard|https://MicrosoftRMSURL/_wmcs/Licensing|
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\CertificationServerRedirection|Reg_SZ|https://*MicrosoftRMSURL*|En af følgende fremgangsmåder, afhængigt af om du bruger HTTP eller HTTPS fra Exchange-serveren til RMS-forbindelse:<br /><br />-   http://*ConnectorFQDN*<br />-   https://*ConnectorFQDN*|
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\LicenseServerRedirection|Reg_SZ|https://*MicrosoftRMSURL*|En af følgende fremgangsmåder, afhængigt af om du bruger HTTP eller HTTPS fra Exchange-serveren til RMS-forbindelse:<br /><br />-   http://*ConnectorFQDN*<br />-   https://*ConnectorFQDN*|

#### Tabel til Exchange 2010 registreringsdatabaseindstillinger

|Sti til registreringsdatabasen|Type|Værdi|Data|
|----------------------------------|--------|---------|--------|
|HKEY_LOCAL_MACHINE\Software\Microsoft\MSDRM\ServiceLocation\Activation|Reg_SZ|Standard|https://*MicrosoftRMSURL*/_wmcs/certificering|
|HKEY_LOCAL_MACHINE\Software\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing|Reg_SZ|Standard|https://*MicrosoftRMSURL*/_wmcs/licens|
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\CertificationServerRedirection|Reg_SZ|https://*MicrosoftRMSURL*|En af følgende fremgangsmåder, afhængigt af om du bruger HTTP eller HTTPS fra Exchange-serveren til RMS-forbindelse:<br /><br />-   http://*ConnectorFQDN*<br />-   https://*ConnectorFQDN*|
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\LicenseServerRedirection|Reg_SZ|https://*MicrosoftRMSURL*|En af følgende fremgangsmåder, afhængigt af om du bruger HTTP eller HTTPS fra Exchange-serveren til RMS-forbindelse:<br /><br />-   http://*ConnectorFQDN*<br />-   https://*ConnectorFQDN*|

### <a name="BKMK_ConfiguringSharePoint"></a>Konfiguration af en SharePoint-server for at bruge connector
Følgende SharePoint roller kommunikere med RMS-stik:

-   Front-end-SharePoint-webservers, herunder dem, der er vært for Central Administration af serveren

Hvis du vil bruge RMS-stik, skal disse servere, der kører SharePoint køre en af følgende softwareversioner:

-   SharePoint Server 2013

-   SharePoint Server 2010

En server med SharePoint 2013 skal også kører en version af MSIPC client 2.1, der from1.0.622.34 gennem 1.0.10907.0.

> [!WARNING]
> Der er flere versioner af klienten MSIPC 2.1, så sørg for at installere en version, der er nævnt i denne artikel.
> 
> Du kan kontrollere klientversionen ved at kontrollere versionsnummeret for MSIPC.dll, som er placeret i **\Program Files\Active Directory Rights Management Services Client 2.1**. Egenskabsdialogboksen viser versionsnummeret for MSIPC 2.1-klienten.

Disse servere, der kører SharePoint 2010 skal have installeret en version af den MSDRM-klient, der understøtter kryptografiske RMS tilstand 2. Den mindste version, der understøttes i Windows Server 2008 er inkluderet i et hotfix, som du kan hente fra [RSA nøglelængde øges til 2048 bit AD RMS i Windows Server 2008 R2 og Windows Server 2008](http://support.microsoft.com/kb/2627272), og den mindste version til Windows Server 2008 R2 kan downloades fra [RSA nøglelængde øges til 2048 bit AD RMS i Windows 7 eller Windows Server 2008 R2](http://support.microsoft.com/kb/2627273). 2012 til Windows Server og Windows Server 2012 R2 har indbygget understøttelse af kryptografiske tilstand 2.

##### Til at konfigurere SharePoint-servere for at bruge connector

1.  Benyt en af følgende på de SharePoint-servere, der kommunikerer med RMS-stik:

    -   Køre serveren configuration tool for Microsoft RMS-stik. Yderligere oplysninger finder du [How to use the server configuration tool for Microsoft RMS connector](../Topic/Deploying_the_Azure_Rights_Management_Connector.md#BKMK_HowToRunTheTool) i dette emne.

    -   Hvis du bruger SharePoint 2013, foretage manuelle ændringer ved hjælp af tabellen i det følgende afsnit til manuelt for at føje indstillinger i registreringsdatabasen på serverne.

2.  Aktivere IRM i SharePoint. Yderligere oplysninger finder du i [konfigurere Information Rights Management (SharePoint Server 2010)](https://technet.microsoft.com/library/hh545607%28v=office.14%29.aspx) i SharePoint-biblioteket.

    Når du følger disse instruktioner, skal du konfigurere SharePoint for at bruge forbindelsen ved at angive **Brug denne RMS-server**, og angiv derefter den belastningsfordeling connector URL-adresse, du har konfigureret. Angiv protokolpræfikset (HTTP:// eller HTTPS://) og navnet på den forbindelse, du har defineret i DNS for \\\load balanceres adressen på din forbindelse. Hvis navnet på din forbindelse er https://connector.contoso.com, ser din konfiguration, som følgende billede:

    ![](../Image/AzRMS_SharePointConnector.png)

    Når IRM er aktiveret på en SharePoint-farm, kan du aktivere IRM på enkelte biblioteker ved hjælp af den **Information Rights Management** indstilling på den **Indstillinger for dokumentbibliotek** side for hver af bibliotekerne.

    > [!IMPORTANT]
    > SharePoint til at få adgang til RMS ved hjælp af forbindelsen, skal du tillade, at de tilsvarende konti i administrationsværktøjet RMS-stik. Hvis du ikke allerede har gjort dette, vises [Authorizing servers to use the RMS connector](../Topic/Deploying_the_Azure_Rights_Management_Connector.md#AuthorizingServers) i dette emne.

Du kan bruge tabellen i afsnittet nedenfor, hvis du vil tilføje eller kontrollere indstillingerne i registreringsdatabasen på en server, der kører SharePoint 2013 manuelt.

#### Tabel til SharePoint 2013 registreringsdatabaseindstillinger
Instruktioner i, når du bruger denne tabel:

-   *MicrosoftRMSURL* er URL-adressen til din organisation Microsoft RMS-service. At finde denne værdi:

    1.  Kør den [få AadrmConfiguration](http://msdn.microsoft.com/library/windowsazure/dn629410.aspx) cmdlet til Azure RMS. Hvis du ikke allerede er installeret Windows PowerShell-modul til Azure RMS, se [Installation af Windows PowerShell til Azure rettighedsstyring](../Topic/Installing_Windows_PowerShell_for_Azure_Rights_Management.md).

    2.  Fra outputtet, identificere de **LicensingIntranetDistributionPointUrl** værdi.

        For eksempel: **LicensingIntranetDistributionPointUrl: https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com/_wmcs/licensing**

    3.  Fjerne fra værdien, **/_wmcs/licens** fra denne streng. Den resterende streng er din URL-adresse til Microsoft-RMS. I vores eksempel er den URL-adresse til Microsoft-RMS følgende værdi:

        **https://5c6bb73b-1038-4eec-863d-49bded473437.RMS.NA.aadrm.com**

-   *ConnectorFQDN* er navnet belastningsfordeling, du har defineret i DNS for forbindelsen. For eksempel **rmsconnector.contoso.com**.

-   Bruge præfikset HTTPS connector URL-adresse, hvis du har konfigureret forbindelsen for at bruge HTTPS til at kommunikere med dine lokale servere. Yderligere oplysninger finder du i [Configuring the RMS connector to use HTTPS](../Topic/Deploying_the_Azure_Rights_Management_Connector.md#BKMK_ConfiguringHTTPS) afsnit i dette emne. De URL-adresser til Microsoft-RMS Brug altid HTTPS.

|Sti til registreringsdatabasen|Type|Værdi|Data|
|----------------------------------|--------|---------|--------|
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation\LicensingRedirection|Reg_SZ|https://*MicrosoftRMSURL*/_wmcs/licens|En af følgende fremgangsmåder, afhængigt af om du bruger HTTP eller HTTPS fra SharePoint-server til RMS-forbindelse:<br /><br />-   http://*ConnectorFQDN*/_wmcs/licens<br />-   https://*ConnectorFQDN*/_wmcs/licens|
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation\EnterpriseCertification|Reg_SZ|Standard|En af følgende fremgangsmåder, afhængigt af om du bruger HTTP eller HTTPS fra SharePoint-server til RMS-forbindelse:<br /><br />-   http://*ConnectorFQDN*/_wmcs/certificering<br />-   https://*ConnectorFQDN*/_wmcs/certificering|
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation\EnterprisePublishing|Reg_SZ|Standard|En af følgende fremgangsmåder, afhængigt af om du bruger HTTP eller HTTPS fra SharePoint-server til RMS-forbindelse:<br /><br />-   http://*ConnectorFQDN*/_wmcs/licens<br />-   https://*ConnectorFQDN*/_wmcs/licens|

### <a name="BKMK_FileServer"></a>Konfiguration af en filserver til fil klassificering infrastruktur til at bruge connector
Hvis du vil bruge RMS-stik og fil klassificering infrastruktur til at beskytte Office-dokumenter, skal file server køre et af følgende operativsystemer:

-   Windows Server 2012 R2

-   Windows Server 2012

##### For at konfigurere filservere for at bruge forbindelsen

1.  Benyt en af følgende på den fil, der er servere, der er konfigureret til fil klassificering infrastruktur, og som skal kommunikere med RMS-stik:

    -   Køre serveren configuration tool for Microsoft RMS-stik. Yderligere oplysninger finder du [How to use the server configuration tool for Microsoft RMS connector](../Topic/Deploying_the_Azure_Rights_Management_Connector.md#BKMK_HowToRunTheTool) i dette emne.

    -   Foretage manuelle ændringer ved hjælp af tabellen i det følgende afsnit til manuelt for at føje indstillinger i registreringsdatabasen på serverne.

2.  Opret regler for klassificering og filhåndteringsopgaver til beskyttelse af dokumenter med RMS-kryptering, og derefter angive en RMS-skabelon for at anvende automatisk RMS-politikker. Yderligere oplysninger finder du [Oversigt over File Server Resource Manager](http://technet.microsoft.com/library/hh831701.aspx) i Windows Server-dokumentbibliotek.

Du kan bruge tabellen i afsnittet nedenfor, hvis du vil tilføje eller kontrollere indstillingerne i registreringsdatabasen på en filserver, der bruger filen klassificering infrastruktur til at beskytte dokumenter manuelt.

#### Tabel til filserver og registreringsdatabaseindstillinger fil klassificering infrastruktur
Instruktioner i, når du bruger denne tabel:

-   *ConnectorFQDN* er navnet belastningsfordeling, du har defineret i DNS for forbindelsen. For eksempel **rmsconnector.contoso.com**.

-   Bruge præfikset HTTPS connector URL-adresse, hvis du har konfigureret forbindelsen for at bruge HTTPS til at kommunikere med dine lokale servere. Yderligere oplysninger finder du i [Configuring the RMS connector to use HTTPS](../Topic/Deploying_the_Azure_Rights_Management_Connector.md#BKMK_ConfiguringHTTPS) afsnit i dette emne. De URL-adresser til Microsoft-RMS Brug altid HTTPS.

|Sti til registreringsdatabasen|Type|Værdi|Data|
|----------------------------------|--------|---------|--------|
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing|Reg_SZ|Standard|http://*ConnectorFQDN*/_wmcs/licens|
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\ServiceLocation\Activation|Reg_SZ|Standard|http://*ConnectorFQDN*/_wmcs/certificering|

## <a name="BKMK_NextSteps"></a>Næste trin
Nu, hvor RMS-connector er installeret og konfigureret, og dine servere er konfigureret til at bruge den, kan IT-administratorer og brugere, beskytte og forbruge e-mail og dokumenter ved hjælp af Azure RMS. Hvis det nemt for brugere, ved at installere RMS deling program, der installerer et tilføjelsesprogram til Office og tilføjer nye Højreklik indstillinger til fil Explorer. Yderligere oplysninger finder du på [Rights Management deling program administratorvejledningen](http://technet.microsoft.com/library/%20dn339003%28v=ws.10%29.aspx).

Desuden bør du overveje følgende for at hjælpe dig med at overvåge RMS-stik og virksomhedens brug af RMS:

-   Indbygget **connector for Microsoft Rights Management** ydelsestællere

-   [Logføring og analyse af brugen af Azure Rights Management](../Topic/Logging_and_Analyzing_Azure_Rights_Management_Usage.md)

Du kan bruge den [Køreplan for Azure Rights Management installation](../Topic/Azure_Rights_Management_Deployment_Roadmap.md) til at kontrollere, om der er andre konfigurationstrin, kan du gøre, før du kaster dig ud af [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] for brugere og administratorer. Hvis der ikke er nogen andre konfigurationstrin, du skal gøre, se [Ved hjælp af Azure rettighedsstyring](../Topic/Using_Azure_Rights_Management.md) for operationelle retningslinjer til at understøtte en succesfuld implementering for organisationen.

## Se også
[Konfiguration af Azure rettighedsstyring](../Topic/Configuring_Azure_Rights_Management.md)

