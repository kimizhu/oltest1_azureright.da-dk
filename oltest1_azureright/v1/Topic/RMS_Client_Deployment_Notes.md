---
description: na
keywords: na
title: RMS Client Deployment Notes
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 03cc8c6f-3b63-4794-8d92-a5df4cdf598f
---
# RMS-klienten installation noter
Rights Management Service-klienten (RMS-klienten) version 2 er også kendt som MSIPC-klient. Det er software til Windows-computere, der kommunikerer med Microsoft Rights Management services på stedet eller i skyen for at beskytte adgangen til og brugen af oplysninger, som den bevæger sig gennem programmer og enheder, inden for grænserne af din organisation eller uden for de administrerede grænser. Ud over levering med det [Rights Management, deling af programmer til Windows](https://technet.microsoft.com/library/dn919648.aspx), RMS-klienten findes [som en valgfri download](http://www.microsoft.com/download/details.aspx?id=38396) der, med bekræftelse og accept af licensaftalen, frit kan distribueres med tredjeparts software, så klienter kan beskytte og forbruge indhold, der er beskyttet med Rights Management services.

Dette emne indeholder følgende afsnit:

-   [Fordeling af RMS-klienten](#BKMK_RedistributeInstaller)

-   [Installere RMS-klienten](#BKMK_InstallClient)

-   [Spørgsmål og svar om RMS-klienten](#BKMK_QA)

-   [Indstillinger for RMS-klienten](#BKMK_Settings)

-   [Kun AD RMS: At begrænse RMS-klienten til at bruge tillid til AD RMS-serverne](#BKMK_UsingTrustedServers)

-   [RMS Service Discovery](#BKMK_ServiceDiscovery)

## <a name="BKMK_RedistributeInstaller"></a>Fordeling af RMS-klienten
RMS-klienten kan omfordeles frit og sammen med andre programmer og IT-løsninger. Hvis du er en programudvikleren eller løsningsudbyder og vil distribuere RMS-klienten, har du to muligheder:

-   Anbefalet: Integrere RMS-klienten installer i installationen af programmet og køre det i uovervåget tilstand (den **/quiet** switch, detaljeret i næste afsnit).

-   Kontroller RMS-klienten en forudsætning for dit program. Med denne indstilling skal du give brugerne yderligere instruktioner at hente, installere og opdatere deres computere med klienten, før de kan bruge programmet.

## <a name="BKMK_InstallClient"></a>Installere RMS-klienten
RMS-klienten er indeholdt i en eksekverbar installationsfil med navnet **setup_msipc_***&lt; arch &gt;***.exe**, hvor *&lt; arch &gt;* er enten **x86** (til klientcomputere til 32-bit) eller **x64** (til klientcomputere til 64-bit). 64-bit (x 64) installer-pakken installerer både en 32-bit-runtime eksekverbare for kompatibilitet med 32-bit-programmer, der kører på en 64-bit operativsystem installation, samt en kørsel af 64-bit eksekverbare fil til understøttelse af oprindelige 64-bit-programmer. 32-bit (x 86)-installationsprogrammet kan ikke køre på en 64-bit Windows-installation.

> [!NOTE]
> Du skal bruge administratorrettigheder for at installere RMS-klienten, som medlem af gruppen Administratorer på den lokale computer.

Du kan installere RMS-klienten ved hjælp af en af følgende installationsmetoder:

-   **Lydløs tilstand.** Ved hjælp af den **/quiet** skifte som en del af de kommandolinjeparametre, du automatisk installere RMS-klienten på computere. Følgende eksempel viser en installation i uovervåget tilstand for RMS-klienten på en 64-bit-klientcomputer:

    ```
    setup_msipc_x64.exe /quiet
    ```

-   **Interaktiv tilstand.** Alternativt kan du installere RMS-klienten ved hjælp af GUI-baseret installationsprogram, som leveres af guiden Installation af RMS-klienten. For at gøre dette, og dobbeltklik på installationspakken RMS-klienten (**setup_msipc_***&lt; arch &gt;***.exe**) i den mappe, som den er kopieret eller hentet på den lokale computer.

## <a name="BKMK_QA"></a>Spørgsmål og svar om RMS-klienten
Følgende afsnit indeholder ofte stillede spørgsmål om RMS-klienten og svarene på dem.

### Hvilke operativsystemer understøtter RMS-klienten?
RMS-klienten understøttes med følgende operativsystemer:

|Windows Server-operativsystemet|Windows-operativsystemet for klient|
|-----------------------------------|---------------------------------------|
|Windows Server 2012 R2|8.1 på Windows|
|Windows Server 2012|Windows 8|
|Windows Server 2008 R2|Windows 7 med minimum af SP1|
|Windows Server 2008 (AD RMS kun)|Windows Vista med SP2 mindst (kun AD RMS)|

### Hvilke processorer eller platforme understøtter RMS-klienten?
RMS-klienten er understøttet på x 86- og x 64 computing platforme.

### Hvor er RMS-klienten installeret?
RMS-klienten installeres som standard i %ProgramFiles%\Active Directory Rights Management Services Client 2. &lt; underordnede versionsnummer &gt;.

### Hvilke filer er knyttet til RMS-klientsoftwaren?
Følgende filer installeres som en del af RMS-klientsoftwaren:

-   Msipc.dll

-   Ipcsecproc.dll

-   Ipcsecproc_ssp.dll

-   MSIPCEvents.man

Ud over disse filer installerer RMS-klienten flersproget brugergrænseflade (MUI) supportfiler på 44 sprog. Kør installationen af RMS-klienten for at kontrollere de sprog, der understøttes, og når installationen er fuldført, kan du gennemse indholdet af mapperne under standardstien til understøttelse af flere sprog.

### Er som standard inkluderet RMS-klienten, når jeg installerer et understøttet operativsystem?
Nr. Denne version af RMS-klienten, der leveres som en valgfri overførsel, der kan installeres separat på computere, der kører understøttede versioner af Microsoft Windows-operativsystemet.

### RMS-klienten opdateres automatisk af Microsoft Update?
Hvis du har installeret denne RMS-klienten ved hjælp af indstillingen uovervåget installation, arver de aktuelle indstillinger for Microsoft Update RMS-klienten. Hvis du har installeret RMS-klienten ved hjælp af GUI-baseret installationsprogram, installationsguiden af RMS-klienten beder dig om at aktivere Microsoft Update.

## <a name="BKMK_Settings"></a>Indstillinger for RMS-klienten
Følgende afsnit indeholder oplysninger om indstillinger om RMS-klienten. Disse oplysninger kan være nyttige, hvis du har problemer med programmer eller tjenester, der bruger RMS-klienten.

> [!NOTE]
> Nogle indstillinger afhænger af, om enlightened RMS-programmet kører som et klientprogram til tilstand (herunder Microsoft Word og Outlook eller RMS deling program), eller serverprogram tilstand (såsom SharePoint og Exchange).  I de følgende tabeller identificeres disse indstillinger som **klienttilstand** og **Server-tilstand**, henholdsvis.

### Hvor RMS-klienten butikker licenser på klientcomputere
RMS-klienten indeholder licenser på den lokale disk og cachelagrer også nogle oplysninger i Windows-registreringsdatabasen.

|Beskrivelse|Klientens tilstand stier|Server tilstand stier|
|---------------|----------------------------|-------------------------|
|Licens placering|%localappdata%\Microsoft\MSIPC|%ALLUSERSPROFILE%\Microsoft\MSIPC\Server\*&lt; SID &gt;*\|
|Skabelonplacering|%localappdata%\Microsoft\MSIPC\Templates|%ALLUSERSPROFILE%\Microsoft\MSIPC\Server\Templates\*&lt; SID &gt;*\|
|Placering i registreringsdatabasen|HKEY_CURRENT_USER<br /> \Software<br /> \Classes<br /> \Local indstillinger<br /> \Software<br /> \Microsoft<br /> \MSIPC|HKEY_CURRENT_USER<br /> \Software<br /> \Microsoft<br /> \MSIPC<br /> \Server<br /> \*&lt; SID &gt;*|
> [!NOTE]
> *&lt; SID &gt;* er sikker-id (SID) for kontoen, hvor serverprogrammet kører. For eksempel, hvis programmet kører under de indbyggede netværkstjenestekontoen, erstatte *&lt; SID &gt;* med værdien af det kendte sikkerheds-id for den pågældende konto (S-1-5-20).

### Indstillinger i Windows-registreringsdatabasen for RMS-klienten
Du kan bruge Windows-baserede registreringsnøgler til at angive eller redigere konfigurationer nogle RMS-klienten. For eksempel som administrator for RMS-enlightened programmer, der kommunikerer med AD RMS-servere, kan du opdatere placeringen af enterprise (override AD RMS-server, der aktuelt er valgt til udgivelse) afhængigt af klientcomputerens aktuelle placering i Active Directory-topologien. Eller kan du aktivere sporing af RMS på klientcomputeren, for at løse et problem med et program til RMS-enlightened. Brug følgende tabel til at identificere de registreringsdatabaseindstillinger, som du kan ændre for RMS-klienten.

|Opgave|Indstillinger|
|----------|-----------------|
|Kun AD RMS: Opdatere enterprise service placering for en klientcomputer|Opdater følgende nøgler i registreringsdatabasen:<br /><br />-   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation\EnterpriseCertification<br />    REG_SZ: standard<br />    **Værdi:**&lt; http eller https &gt; :// *RMS_Cluster_Name*/_wmcs/certificering<br />-   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation\EnterprisePublishing<br />    REG_SZ: standard<br />    **Værdi:** &lt; http eller https &gt; :// *RMS_Cluster_Name*/_wmcs/Licensing|
|Sådan aktiveres og deaktiveres sporing|Opdater følgende nøgle i registreringsdatabasen:<br /><br />-   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC<br />    REG_DWORD: Spor<br />    **Værdi:** 1 for at aktivere sporing, 0 for at deaktivere sporing (standard)|
|At ændre hyppigheden i dage til at opdatere skabeloner|Følgende værdier i registreringsdatabasen angiver, hvor ofte skabeloner vil blive opdateret på brugerens computer, hvis værdien TemplateUpdateFrequencyInSeconds ikke er angivet.  Hvis ingen af disse værdier er angivet, er standard opdateringsintervallet for programmer, der bruger RMS-klienten (version 1.0.1784.0) til at hente skabeloner 1 dag. Version over, kan det have en standardværdi for hver syvende dag.<br /><br />**Klienttilstand:**<br /><br />-   HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC<br />    REG_DWORD: TemplateUpdateFrequency<br />    **Værdi:** En heltalsværdi, der angiver antallet dage (mindst 1) mellem overførsler.<br /><br />**Servertilstand:**<br /><br />-   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\Server\*&lt; SID &gt;*<br />    REG_DWORD: TemplateUpdateFrequency<br />    **Værdi:** En heltalsværdi, der angiver antallet dage (mindst 1) mellem overførsler.|
|At ændre hyppigheden i sekunder at opdatere skabeloner **Important:** Hvis dette er angivet, ignoreres værdien for at opdatere skabeloner i dage. Angiv en eller den anden, ikke begge dele.|Følgende værdier i registreringsdatabasen angiver, hvor ofte opdateres skabeloner på brugerens computer. Hvis denne værdi eller at ændre hyppigheden i dage (TemplateUpdateFrequency) ikke er angivet, er standard opdateringsintervallet for programmer, der bruger RMS-klienten (version 1.0.1784.0) til at hente skabeloner 1 dag. Version over, kan det have en standardværdi for hver syvende dag.<br /><br />**Klienttilstand:**<br /><br />-   HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC<br />    REG_DWORD: TemplateUpdateFrequencyInSeconds<br />    **Værdi:** En heltalsværdi, der angiver antallet sekunder (mindst 1) mellem overførsler.<br /><br />**Servertilstand:**<br /><br />-   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\Server\*&lt; SID &gt;*<br />    REG_DWORD: TemplateUpdateFrequencyInSeconds<br />    **Værdi:** En heltalsværdi, der angiver antallet sekunder (mindst 1) mellem overførsler.|
|Kun AD RMS: Hente skabeloner umiddelbart efter næste udgivelse anmodning|Du vil måske RMS-klienten kan hente skabeloner hurtigst muligt under test og evalueringer. Du kan fjerne følgende nøgle i registreringsdatabasen og RMS-klienten skal hente skabeloner umiddelbart efter næste udgivelse anmodning i stedet for at vente på den tid, der er angivet af indstillingen TemplateUpdateFrequency i registreringsdatabasen:<br /><br />-   HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC\ &lt; servernavn &gt; \Template **Note:** &lt; servernavn &gt; kunne have ekstern (til corprights.contoso.com) og URL-adresser til intern (corprights) og derfor to forskellige poster.|
|Kun AD RMS: Aktivere understøttelse af organisationsnetværket godkendelse|Hvis RMS klientcomputeren opretter forbindelse til en AD RMS-klynge ved hjælp af et medlem af organisationsnetværk tillid, skal du konfigurere organisationsnetværk startdomænet.<br /><br />-   HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\Federation<br />    REG_SZ: FederationHomeRealm<br />    **Værdi:** Værdien af denne registreringsdatabasepost er ensartet ressource-id'et (URI) for tjenesten federation (for eksempel "https://fs-01.contoso.com").|
|Kun AD RMS: Til at understøtte partner federation servere, som kræver formularbaseret godkendelse for bruger-input|RMS-klienten fungerer i baggrunden som standard og brugerinput er ikke påkrævet. Partner federation servere kan dog konfigureres til at kræve brugerinput, sådan som via formularbaseret godkendelse. I så fald skal du konfigurere RMS-klienten ignorerer lydløs tilstand, så formen organisationsnetværket godkendelse vises i et browservindue, og brugeren hæves til godkendelse.<br /><br />-   HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\Federation<br />    REG_DWORD: EnableBrowser **Note:** Hvis organisationsserveren er konfigureret til at bruge formularbaseret godkendelse, kræves denne nøgle. Hvis organisationsserveren er konfigureret til at bruge integreret Windows-godkendelse, er denne nøgle er ikke påkrævet.|
|Kun AD RMS: Blokere ILS serviceforbrug|RMS-klienten gør det muligt for lang indhold, der er beskyttet af ILS-service som standard, men du kan konfigurere klienten for at blokere denne tjeneste ved at indstille følgende nøgle i registreringsdatabasen. Hvis denne nøgle i registreringsdatabasen er indstillet til at blokere tjenesten ILS, forsøg på at åbne og forbruge indhold, der er beskyttet af tjenesten ILS returnerer følgende fejl:<br />HRESULT_FROM_WIN32(ERROR_ACCESS_DISABLED_BY_POLICY)<br /><br />-   HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC<br />    REG_DWORD: **DisablePassportCertification**<br />    **Værdi:** 1 at blokere ILS forbrug, 0 for at tillade ILS forbrug (standard)|

### Administration af skabelonen Distribution til RMS-klienten
Skabeloner gør det nemt for brugere og administratorer hurtigt anvende rettighedsstyring beskyttelse og RMS-klienten henter automatisk skabeloner fra dens RMS-serverne eller en tjeneste, hvis du placerer skabelonerne i følgende mappeplacering, RMS-klienten kan ikke hente alle skabeloner fra dens standardplacering og i stedet henter de skabeloner, som du har lagt i denne mappe. RMS-klienten kan fortsætte med at hente skabeloner fra andre tilgængelige RMS-servere.

**Klienttilstand:** %localappdata%\Microsoft\MSIPC\UnmanagedTemplates

**Server-tilstand:** %allusersprofile%\Microsoft\MSIPC\Server\UnmanagedTemplates\*&lt; SID &gt;*

Når du bruger denne mappe, er der ingen speciel navngivningskonvention, der kræves, bortset fra at skabelonerne, der skal udstedes af RMS-serveren eller tjenesten, og de skal have filtypenavnet .xml. Contoso-Confidential.xml eller Contoso-ReadOnly.xml er gyldige navne.

## <a name="BKMK_UsingTrustedServers"></a>Kun AD RMS: At begrænse RMS-klienten til at bruge tillid til AD RMS-serverne
RMS-klienten kan være begrænset til at bruge kun bestemte pålidelige AD RMS-servere ved at foretage følgende ændringer i Windows-registreringsdatabasen på lokale computere.

**Hvis du vil aktivere begrænse RMS klienten til at bruge kun tillid til AD RMS-servere**

-   HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\TrustedServers\
    REG_DWORD: AllowTrustedServersOnly

    **Værdi:** Hvis der er angivet en værdi forskellig fra nul, kan RMS-klienten skal have tillid til kun de angivne servere, der er konfigureret på listen TrustedServers og Azure Rights Management-tjenesten.

**Føje medlemmer til listen over pålidelige AD RMS-servere**

-   HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\TrustedServers\
    REG_SZ: *&lt; URL_or_HostName &gt;*

    **Værdi:** Strengværdier, der er tilføjet i denne Registreringsdatabasenøglens placering kan være enten navneformatet for DNS-domæne (f.eks **adrms.contoso.com**) eller fuld URL-adresser til servere, der er tillid til AD RMS (for eksempel **https://adrms.contoso.com**). Hvis en bestemt URL-adresse, der starter med **https://**,  RMS-klienten skal bruge SSL eller TLS til at kontakte den angivne AD RMS-server.

## <a name="BKMK_ServiceDiscovery"></a>RMS Service Discovery
RMS service discovery giver mulighed for at kontrollere, hvilke RMS-serveren eller tjenesten at kommunikere med, før du beskyttede indhold RMS-klienten. Discovery service kan også ske, når RMS-klienten bruger beskyttet indhold, men dette er mindre tilbøjelige til at ske, fordi den politik, der er knyttet til indholdet, der indeholder foretrukne RMS-serveren eller servicen, og kun hvis, der er mislykket klienten derefter kører service discovery.

Discovery service søger først efter en lokal version af Rights Management (AD RMS). Hvis det ikke lykkes, skal søger discovery service automatisk efter sky-version af Rights Management (Azure RMS).

For at udføre service discovery for en lokal installation, kontrollerer RMS-klienten følgende:

1.  Windows-registreringsdatabasen på den lokale computer: Hvis service discovery-indstillinger er konfigureret i registreringsdatabasen, afprøves først disse indstillinger.  Disse indstillinger er ikke konfigureret i registreringsdatabasen som standard.

2.  Active Directory-domæneservices: Et medlem af et domæne computeren retter forespørgsler til Active Directory for et service connection point (SCP). Hvis der registreres en SCP, returneres URL-adressen på RMS-serveren til RMS-klienten til at bruge.

### Kun AD RMS: Aktivering af serverbaserede Service Discovery ved hjælp af Active Directory
Hvis kontoen ikke har tilstrækkelige rettigheder (virksomhedsadministratorer og lokal administrator på AD RMS-server), kan du automatisk registrere en et service connection point (SCP), når du installerer AD RMS cluster rodserveren. Hvis der allerede findes en SCP i skoven, skal du først slette den eksisterende SCP, før du kan registrere en ny.

Du kan registrere og slette en SCP, når AD RMS er installeret ved at benytte følgende fremgangsmåde. Før du begynder, Kontroller, at kontoen har de nødvendige rettigheder (virksomhedsadministratorer og lokal administrator på AD RMS-serveren).

##### At aktivere AD RMS service discovery ved at registrere en SCP i Active Directory

1.  Åbn Active Directory Management Services-konsollen på AD RMS-serveren:

    -   Hvis du bruger Windows Server 2008 R2 eller Windows Server 2008, skal du klikke på **Start**, skal du klikke på **Administration**, og klik derefter på **Active Directory Rights Management Services**.

    -   Hvis du bruger Windows Server 2012 R2 eller Windows Server 2012 i Serverstyring, skal du klikke på **Tools**, og klik derefter på **Active Directory Rights Management Services**.

2.  Højreklik på AD RMS-klyngen AD RMS-konsollen, og klik derefter på **Egenskaber**.

3.  Klik på den **SCP** tab.

4.  Vælg den **ændre SCP** afkrydsningsfelt.

5.  Vælg den **angive SCP til aktuelle certificering klynge** og klik derefter på **OK**.

### Aktivering af klientsiden Service Discovery ved hjælp af Windows-registreringsdatabasen
Du kan konfigurere registreringsdatabasen på klientcomputeren som et alternativ til at bruge en SCP, eller hvor der ikke findes en SCP så RMS-klienten kan finde sin AD RMS-server.

##### At aktivere-klientsiden AD RMS service discovery ved hjælp af Windows-registreringsdatabasen

1.  Åbn Windows Registreringseditor, Regedit.exe:

    -   På klientcomputeren, i vinduet Kør, Skriv **regedit**, og tryk derefter på ENTER for at åbne Registreringseditor.

2.  I Registreringseditor, gå til **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC**.

    > [!IMPORTANT]
    > Hvis du kører en 32-bit program på en 64-bit computer, bliver stien på følgende måde: 
    > **HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSIPC**

3.  Højreklik for at oprette undernøglen ServiceLocation, **MSIPC**, peg på **ny**, skal du klikke på **nøgle**, og skriv derefter **ServiceLocation**.

4.  Højreklik for at oprette undernøglen EnterpriseCertification, **ServiceLocation**, peg på **ny**, skal du klikke på **nøgle**, og skriv derefter **EnterpriseCertification**.

5.  For at angive URL-adressen til enterprise-certificering, skal du dobbeltklikke på den **(standard)** værdi under den **EnterpriseCertification** undernøgle, og hvornår den **Rediger streng** dialogboks, for **Værdidata**, type &lt;http or https&gt;://*AD RMS_cluster_name*/_wmcs/Certification, og klik derefter på **OK**.

6.  Højreklik for at oprette undernøglen EnterprisePublishing, **ServiceLocation**, peg på **ny**, skal du klikke på **nøgle**, og skriv derefter EnterprisePublishing.

7.  Dobbeltklik for at indstille virksomheden udgiver URL-adresse, **(standard)** , under den **EnterprisePublishing** undernøgle, og hvornår den **Rediger streng** vises dialogboksen, Skriv til **værdi data** følgende &lt;http or https&gt;://*AD RMS_cluster_name*/_wmcs/Licensing, og klik derefter på **OK**.

8.  Luk Registreringseditor.

Hvis RMS-klienten blev ikke fundet en SCP ved at forespørge Active Directory, og det ikke er angivet i registreringsdatabasen, mislykkes discovery servicekald AD RMS.

### Omdirigering af trafik til Server-licenser
I nogle tilfælde skal du omdirigere trafik under service discovery, for eksempel, når to organisationer er flettet sammen i én organisation gamle licensserveren er udgået og klienter skal omdirigeres til en ny licensserver. Eller du overflytter fra AD RMS til Azure RMS. Brug følgende fremgangsmåde til at aktivere omdirigering af licenser.

##### Aktivere RMS licensing omdirigering ved hjælp af Windows-registreringsdatabasen

1.  Åbn Windows Registreringseditor, Regedit.exe:

    -   På klientcomputeren, i vinduet Kør, Skriv **regedit**, og tryk derefter på ENTER for at åbne Registreringseditor.

2.  I Registreringseditor, gå til en af følgende:

    -   Til 64-bit version af Office på x 64-platform: HKLM\SOFTWARE\Microsoft\MSIPC\Servicelocation

    -   Til 32-bit version af Office på x 64-platform: HKLM\SOFTWARE\Wow6432Node\Microsoft\MSIPC\Servicelocation

3.  Oprette en LicensingRedirection-undernøgle ved at højreklikke på **Servicelocation**, peg på **ny**, skal du klikke på **nøgle**, og skriv derefter **LicensingRedirection**.

4.  Hvis du vil angive omdirigering licenser, skal du højreklikke på den **LicensingRedirection** undernøgle, Vælg **ny**, og vælg derefter **strengværdi**.  For **navnet**, angive den foregående server licensing URL-adresse og **værdi** angiver den nye server licensing URL-adresse.

    Hvis du vil omdirigere licenser fra en server hos Contoso.com til én ad Fabrikam.com, kan du angive følgende værdier:

    **Navn:** `https://contoso.com/_wmcs/licensing`

    **Værdi:** `https://fabrikam.com/_wmcs/licensing`

    > [!NOTE]
    > Hvis gamle licensserveren har både intranet og ekstranet URL-adresser angives derefter et nyt navn og værditilknytning skal angives for begge disse URL-adresser under nøglen LicensingRedirection.

5.  Gentag forrige trin for alle servere, der skal omdirigeres.

6.  Luk Registreringseditor.

