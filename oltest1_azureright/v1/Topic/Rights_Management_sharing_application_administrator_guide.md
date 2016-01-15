---
description: na
keywords: na
title: Rights Management sharing application administrator guide
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d9992e30-f3d1-48d5-aedc-4e721f7d7c25
---
# Rights Management deling program administratorvejledningen
Brug følgende oplysninger, hvis du er ansvarlig for Microsoft Rights Management deling program på et virksomhedsnetværk, eller hvis du vil have flere tekniske oplysninger, end der er i den [Rights Management deling program bruger guide](../Topic/Rights_Management_sharing_application_user_guide.md) eller [ofte stillede spørgsmål om Microsoft Rights Management deling program til Windows](http://go.microsoft.com/fwlink/?LinkId=303971):

-   [Automatisk installation af Microsoft Rights Management deling program](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_ScriptedInstall)

    -   [Kontrollerer, at installationen lykkedes](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_verifyscripted)

    -   [Fjerne kommandoer](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_uninstallscripted)

    -   [Undertrykke automatiske opdateringer](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_SuppressAutomaticUpdates)

    -   [Kun Azure RMS: Konfiguration af dokument-sporing](#BKMK_DocumentTracking)

    -   [Kun AD RMS: Understøttelse af flere e-mail-domæner i organisationen](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_FederatedDomains)

-   [Teknisk oversigt over Microsoft Rights Management deling program](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_AdminOverview)

    -   [Niveauer af beskyttelse – oprindelig og generiske](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_LevelsofProtection)

    -   [Understøttede filtyper og filtypenavne](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_SupportFileTypes)

    -   [Hvis du ændrer standardniveauet for beskyttelse af filer](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_ChangeDefaultProtection)

> [!TIP]
> Hvis du er ny til deling RMS-app eller ønsker yderligere oplysninger, se [hvordan RMS beskytter alle filtyper – ved hjælp af Deling af app RMS](https://curah.microsoft.com/191031/how-rms-protects-all-file-types-by-using-the-rms-sharing-app).

RMS deling program er bedst egnet til at arbejde med Azure RMS, da denne installationskonfiguration understøtter afsendelse beskyttede vedhæftede filer til brugere i en anden virksomhed, og funktioner som e-mail-beskeder og dokumentsporing med tilbagekaldte certifikater.  Dog med nogle begrænsninger fungerer det også med den lokale version AD RMS. Du kan finde en omfattende sammenligning af funktioner, der understøttes af Azure RMS og AD RMS i [sammenligne Azure Rights Management og AD RMS](https://technet.microsoft.com/library/jj739831.aspx). Hvis du har AD RMS og vil overføre Azure RMS, se [overflytning fra AD RMS Azure Rights Management](https://technet.microsoft.com/library/dn858447.aspx).

## <a name="BKMK_ScriptedInstall"></a>Automatisk installation af Microsoft Rights Management deling program
Windows-versionen af programmet RMS deling understøtter en scriptbaseret installation, hvilket gør den egnet til implementering i virksomheden.

De eneste forudsætninger for installationer er, at computerne, der kører en minimal version af Windows 7 Service Pack 1, og at Microsoft Framework, minimum version 4.0 er installeret. Hvis du vil installere Microsoft,.NET Framework 4.0, kan du [hente det installeres fra Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=17718).

#### Til at hente RMS Deling af programmet for automatisk installation

1.  Gå til den [Microsoft Rights Management, deling af programmer til Windows](http://www.microsoft.com/download/details.aspx?id=40857) side i Microsoft Download Center, og klik på **hente**.

2.  Vælg og Hent de filer, du har brug for. Der er to installationspakker til klienten: én for Windows 64-bit (Microsoft Rights Management deling program x64.zip) og en anden til Windows 32-bit (Microsoft Rights Management deling program x86.zip).

3.  Udpak filerne fra de komprimerede pakker, for eksempel ved at dobbeltklikke på dem. Kopier de udpakkede filer til et netværk, der kan få adgang til klientcomputere.

Installationspakker til RMS deling program understøtter forskellige installationsscenarier og omfatter følgende:

|Beskrivelse|Installationsscenario|
|---------------|-------------------------|
|Microsoft Online Tilmeldingsassistent|Kræves for følgende:<br /><br />-   Office 2010 og Azure RMS<br />-   Office 2013 og Azure RMS, hvis du ikke har installeret den [9 juni 2015, opdatering til Office-2013](https://support.microsoft.com/kb/3054853) (KB3054853)|
|Hotfix til Office (KB 2596501)|Kræves for følgende:<br /><br />-   Office 2010 og Azure RMS<br />-   Office 2010 og Active Directory-RMS|
|Hotfix til at aktivere AD RMS-klienten 1.0 til at arbejde med Azure RMS (KB 2843630)|Kræves for følgende:<br /><br />-   Office 2010 og Azure RMS<br />-   Office 2010 og Active Directory-RMS|
|AD RMS-klienten og RMS deling program|Kræves for følgende:<br /><br />-   2016 Office eller Office 2013 og Azure RMS eller Active Directory-RMS<br />-   Office 2010 og Azure RMS<br />-   Office 2010 og Active Directory-RMS<br />-   Deling af programmer og Office-tilføjelsesprogram kun RMS|
|Office-tilføjelsesprogrammet til båndet|Kræves for følgende:<br /><br />-   2016 Office eller Office 2013 og Azure RMS eller Active Directory-RMS<br />-   Office 2010 og Azure RMS<br />-   Office 2010 og Active Directory-RMS<br />-   Deling af programmer og Office-tilføjelsesprogram kun RMS|
|Værktøjet til forberedelse af Azure Active Directory Rights Management|Kræves for følgende:<br /><br />-   Office 2010 og Azure RMS|
Brug følgende procedurer til at identificere de kommandoer, der kræves for at installere RMS deling ansøgning om disse installationsscenarier:

-   **2016 Office eller Office 2013 og Azure RMS eller Active Directory-RMS**

    Brugerne kører Office 2016 eller Office 2013, Azure RMS eller Active Directory-RMS i organisationen, og brugere kan samarbejde med andre organisationer, der bruger Azure RMS eller Active Directory-RMS.

-   **Office 2010 og Azure RMS**

    Brugerne kører Office 2010, organisationen bruger Azure RMS, og brugere kan samarbejde med andre organisationer, der bruger Azure RMS eller Active Directory-RMS.

-   **Office 2010 og Active Directory-RMS**

    Brugerne kører Office 2010, organisationen bruger AD RMS og brugere kan samarbejde med andre organisationer, der bruger Azure RMS.

-   **Deling af programmer og Office-tilføjelsesprogram kun RMS**

    Brugerne kører Office 2016, 2013 Office eller Office 2010, organisationen bruger AD RMS og brugerne behøver ikke at samarbejde med andre organisationer, der bruger Azure RMS. Denne installation kan du installere lige dele programmer og Office-tilføjelsesprogram.

> [!NOTE]
> I disse scenarier, hvis din organisation kører AD RMS, brugerne kan modtage beskyttet indhold fra andre organisationer, der bruger Azure RMS, men brugerne kan ikke sende beskyttet indhold til brugerne i en organisation, der bruger Azure RMS. Hvis din organisation kører Azure RMS, kan brugerne, sende og modtage beskyttet indhold fra andre organisationer.

Computeren skal genstartes for at fuldføre installationen for hver procedure. Du kan starte en automatisk genstart ved hjælp af en kommando f.eks lukning /i.

#### Installere RMS deling ansøgning om Office 2016 eller Office 2013 og Azure RMS eller Active Directory-RMS

-   På hver computer, hvor du vil installere RMS deling program og relaterede komponenter, skal du køre følgende kommando med øgede rettigheder:

    ```
    setup.exe /s
    ```

For at kontrollere succes, se den [Kontrollerer, at installationen lykkedes](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_verifyscripted) afsnit i dette emne.

#### At anvende de dele af programmet til Office 2010 og Azure RMS RMS

1.  Du skal være den globale administrator for din Office 365 eller Azure Active Directory lejer, så du kan få din organisations certificering URL-adresse ved at køre værktøjet til forberedelse af Azure Active Directory Rights Management. Du skal køre dette værktøj kun én gang på en enkelt computer. Du vil bruge certificering URL-adressen, når du installerer RMS deling program på hver enkelt computer:

    1.  Logge på en computer ved hjælp af en lokal administrator-konto.

    2.  På den pågældende computer, [hente og installere de Microsoft Online Logonassistent](http://www.microsoft.com/download/details.aspx?id=28177).

    3.  Kør følgende kommando for at se vises på skærmen certificering service URL-adressen, som du kan derefter kopiere og gemme til næste trin:

        -   Til Windows 8.1 og Windows 8, 64-bit:

            ```
            x64\aadrmprep.exe /findCertificationUrl /logfile "<log file path and name>"
            ```

        -   Til Windows 8.1 og Windows 8, 32-bit:

            ```
            X86\aadrmprep.exe /findCertificationUrl /logfile "<log file path and name>"
            ```

        -   Til Windows 7, 64-bit:

            ```
            x64\win7\aadrmprep.exe /findCertificationUrl /logfile "<log file path and name>"
            ```

        > [!NOTE]
        > Denne kommando bliver du bedt om at angive dine legitimationsoplysninger for Azure. Hvis computeren ikke er tilsluttet et domæne, vil du blive bedt om. Hvis computeren er tilsluttet et domæne, kan værktøjet muligvis bruger cachelagrede legitimationsoplysninger.

2.  På hver computer, hvor du vil installere RMS Deling af programmet, skal du køre følgende kommando med øgede rettigheder:

    ```
    setup.exe /s /configureO2010Admin /certificationUrl <certification_url>
    ```

3.  På hver computer, hvor du vil installere RMS deling ansøgning, skal brugere køre følgende kommando (behøver ikke administratorrettigheder). Forskellige måder at opnå dette, herunder beder brugerne til at køre kommandoen (for eksempel et hyperlink i en e-mail eller et link på portalen Hjælp desk), eller du kan føje til deres logonscript:

    ```
    bin\RMSSetup.exe /configureO2010Only
    ```

For at kontrollere succes, se den [Kontrollerer, at installationen lykkedes](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_verifyscripted) afsnit i dette emne.

#### At anvende de dele af programmet til Office 2010 og Active Directory-RMS RMS

1.  På hver computer, hvor du vil installere RMS Deling af programmet, skal du køre følgende kommando med øgede rettigheder:

    ```
    setup.exe /s /configureO2010Admin
    ```

2.  På hver computer, hvor du vil installere RMS deling ansøgning, skal brugere køre følgende kommando (behøver ikke administratorrettigheder). Forskellige måder at opnå dette, herunder beder brugerne til at køre kommandoen (for eksempel et hyperlink i en e-mail eller et link på portalen Hjælp desk), eller du kan føje til deres logonscript:

    -   Til Windows 10, Windows 8.1 og Windows 8, 64-bit:

        ```
        x64\aadrmprep.exe /configureO2010
        ```

    -   Til Windows 10, Windows 8.1 og Windows 8, 32-bit:

        ```
        X86\aadrmprep.exe /configureO2010
        ```

    -   Til Windows 7, 64-bit:

        ```
        x64\win7\aadrmpep.exe /configureO2010
        ```

For at kontrollere succes, se den [Kontrollerer, at installationen lykkedes](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_verifyscripted) afsnit i dette emne.

#### Sådan installeres Deling af programmer og Office-tilføjelsesprogram kun RMS

1.  Installere AD RMS-klienten og RMS deling program ved hjælp af følgende kommando:

    -   Til 64-bit Windows:

        ```
        x64\setup_ipviewer.exe /norestart /quiet /msicl "MSIRESTARTMANAGERCONTROL=Disable" /log "<log file path and name>"
        ```

    -   Til 32-bit Windows:

        ```
        X86\setup_ipviewer.exe /norestart /quiet /msicl "MSIRESTARTMANAGERCONTROL=Disable" /log "<log file path and name>"
        ```

    For eksempel: `\\server5\apps\rms\x64\setup_ipviewer.exe /norestart /quiet /msicl "MSIRESTARTMANAGERCONTROL=Disable" /log "C:\Log files\ipviewerinstall.log"`

2.  Installer tilføjelsesprogrammet Office ved hjælp af følgende kommandoer:

    -   Til 64-bit version af Office:

        ```
        msiexec.exe /norestart /quiet MSIRESTARTMANAGERCONTROL=Disable /i "x64\Setup64.msi" /L*v "<log file path and name>"
        ```

    -   Til 32-bit version af Office:

        ```
        msiexec.exe /norestart /quiet MSIRESTARTMANAGERCONTROL=Disable /i "x86\Setup.msi" /L*v "<log file path and name>"
        ```

    For eksempel: `\\server5\apps\rms\msiexec.exe /norestart /quiet MSIRESTARTMANAGERCONTROL=Disable /i "x64\Setup64.msi" /L*v "C:\Log files\rmsofficeinstall.log"`

For at kontrollere succes, se den [Kontrollerer, at installationen lykkedes](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_verifyscripted) afsnit i dette emne.

### <a name="BKMK_verifyscripted"></a>Kontrollerer, at installationen lykkedes
Du kan bruge installationslogfilerne til at bekræfte en vellykket installation.

##### Til at kontrollere installationen succes for RMS deling ansøgning om Office 2016 eller Office 2013 og Azure RMS eller Active Directory-RMS

-   For at kontrollere succes af kommandoen Setup.exe på hver computer, kan du søge efter installationslogfilen **RMInstaller.log** i den *%temp%\RMS_installer_ &lt; guid &gt;* mappe, og derefter identificere returkoden.

    En vellykket installation har en returkode på 0, og et andet tal angiver en mislykket installation.

    Eksempel logfilnavn: **C:\temp\RMS_Installer_9352fc91-1982-43bf-958a-2ef1fe9c2ed0\RMInstaller.log**

##### Til at kontrollere installationen succes for dele af programmet til Office 2010 og Azure RMS RMS

1.  For at kontrollere succes af kommandoen Setup.exe på hver computer, kan du søge efter installationslogfilen **RMInstaller.log** i den *%temp%\RMS_installer_ &lt; guid &gt;* mappe, og derefter identificere returkoden.

    En vellykket installation har en returkode på 0, og et andet tal angiver en mislykket installation.

    Eksempel logfilnavn: **C:\temp\RMS_Installer_9352fc91-1982-43bf-958a-2ef1fe9c2ed0**

2.  For at kontrollere succes for kommandoen RMSSetup.exe, brugeren skal have følgende filer oprettet i deres *%localappdata%\microsoft\drm* mappe:

    -   CERT-Machine-2048.drm

    -   CERT-Machine.drm

    -   CLC-&#42;.drm

    -   GIK &#42;.drm

    Eksempel på en CLC &#42;.drm fil:

    **CLC-alice@isvtenant999.onmicrosoft.com-{1b9cfccf; k5b11; k4a10; kac15; k29b2b6980f4c} .drm**

##### Til at kontrollere installationen succes for dele af programmet til Office 2010 og Active Directory-RMS RMS

1.  For at kontrollere succes af kommandoen Setup.exe på hver computer, kan du søge efter installationslogfilen i den *%temp%\RMS_installer_ &lt; guid &gt;* mappe, og identificere returkoden.

    En vellykket installation har en returkode på 0, og et andet tal angiver en mislykket installation.

    Eksempel logfilnavn: **C:\temp\RMS_Installer_9352fc91-1982-43bf-958a-2ef1fe9c2ed0**

2.  For at kontrollere succes af kommandoen aadrmprep.exe på hver computer, søge efter følgende tekst i logfilen for installationen: **aadrmprep.exe afsluttedes med status lykkedes**

    > [!NOTE]
    > Nogle gange kan denne installation køre to gange. den første forekomst mislykkes, og andet er vellykket.

    Hvis du vil kontrollere manuelt ændringer i registreringsdatabasen, som gør dette værktøj, er de som følger:

    -   [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\Federation]

        "FederationHomeRealm"="urn: HostedRmsOnlineService:Certification"

    -   [HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSDRM\Federation]

        "FederationHomeRealm"="urn: HostedRmsOnlineService:Certification"

    -   [HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSDRM\ServiceLocation\Activation]

        @-= "&lt; certificering url &gt;"

    -   [HKEY_CURRENT_USER\SOFTWARE\Microsoft\Office\14.0\Common\DRM]

        DefaultUser = "&lt; default_user &gt;"

##### Til at kontrollere installationen succes for Deling af programmer og Office-tilføjelsesprogram kun RMS

1.  For at kontrollere succes af kommandoen Setup_ipviewer.exe, kan du søge efter følgende tekst i installationslogfilen: **Vellykkede handlinger eller fejlmappen installationsstatus: 0**

    Eksempel linjer fra en vellykket installation:

    **MSI (s) (F0:B8) [14:19:57:854]: Produkt: Active Directory Rights Management Services Client 2.1 - installationen er fuldført.**

    **MSI (s) (F0:B8) [14:19:57:854]: Windows Installer har installeret produktet. Produktnavn: Active Directory Rights Management Services Client 2.1. Version af produktet: 1.0.1179.1. Produktsprog: 1033. Producent: Microsoft Corporation. Vellykkede handlinger eller fejlmappen installationsstatus: 0.**

2.  For at kontrollere succes af Office-tilføjelsesprogrammet, på hver computer, kan du søge efter følgende tekst i installationslogfilen: **Vellykkede handlinger eller fejlmappen installationsstatus: 0**

    Eksempel linjer fra en vellykket installation:

    **MSI (s) (9C: 88) [18:49:04:007]: Produkt: Tilføjelsesprogrammer til Microsoft RMS Office - Installationen er fuldført.**

    **MSI (s) (9C: 88) [18:49:04:007]: Windows Installer har installeret produktet. Produktnavn: Microsoft RMS Office-tilføjelsesprogrammer. Version af produktet: 1.0.7. Produktsprog: 1033. Producent: Microsoft. Vellykkede handlinger eller fejlmappen installationsstatus: 0.**

### <a name="BKMK_uninstallscripted"></a>Fjerne kommandoer
Ikke alle kommandoerne installation, der kræves til disse installationer understøtter kommandoen fjernelse. Du kan fjerne AD RMS-klienten og programmet deling, og du kan fjerne Office-tilføjelsesprogrammet. Brug følgende kommandoer til at fjerne disse elementer.

##### Fjerne AD RMS-klienten og RMS deling program

-   Du kan bruge følgende kommandoer:

    -   Til 64-bit Windows:

        ```
        x64\setup_ipviewer.exe /uninstall /quiet
        ```

    -   Til 32-bit Windows:

        ```
        x86\setup_ipviewer.exe /uninstall /quiet
        ```

##### Sådan fjernes tilføjelsesprogrammet Office

-   Du kan bruge følgende kommandoer:

    -   Til 64-bit version af Office:

        ```
        msiexec /x \x64\Setup[64].msi /quiet
        ```

    -   Til 32-bit version af Office:

        ```
        msiexec /x \x86\Setup.msi /quiet
        ```

### <a name="BKMK_SuppressAutomaticUpdates"></a>Undertrykke automatiske opdateringer
Som standard, er brugere besked, hvis der er en nyere version af programmet RMS deling, og du bliver bedt om at hente den. Du kan undertrykke denne meddelelse ved at gøre følgende i registreringsdatabasen redigeres:

1.  Gå til **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC** og hvis den ikke allerede findes, kan du oprette en ny nøgle med navnet **RmsSharingApp**.

2.  Vælg **RmsSharingApp**, oprette en ny DWORD-værdi af **AllowUpdatePrompt**, og angiv værdien til **0**.

Da programmet RMS deling ikke understøttes af WSUS, kan du bruge følgende teknik til at afprøve de nye versioner af RMS deling program, før du implementerer den til alle brugere:

1.  På alle brugernes computere, der kører et script for at undertrykke automatiske opdateringer. På de computere, som administratorer kan bruge til at teste nye versioner, kan du ikke køre dette script.

2.  Når en ny version er tilgængelig, administratorer hente det og test den.

3.  Når testen er fuldført, og eventuelle problemer er løst, skal installere den nyeste version for alle brugere ved hjælp af de automatiske installation instruktioner i denne vejledning.

### <a name="BKMK_DocumentTracking"></a>Kun Azure RMS: Konfiguration af dokument-sporing
Hvis du har en [abonnement, der understøtter dokument sporing](https://technet.microsoft.com/en-us/dn858608), den dokumentsporing websted er aktiveret som standard for alle brugere i organisationen.  Dokumentsporing viser oplysninger som e-mail-adresser på de personer, der har forsøgt at få adgang til beskyttede dokumenter, som brugerne har delt, når disse personer har forsøgt at få adgang til dem og deres placering. Hvis visning af disse oplysninger er forbudt i din organisation på grund af kravene til beskyttelse af personlige oplysninger, kan du deaktivere adgang til dokumentsporing websted ved hjælp af den  [Deaktiver AadrmDocumentTrackingFeature](http://go.microsoft.com/fwlink/?LinkId=623032) cmdlet. Du kan genaktivere adgang til webstedet på et hvilket som helst tidspunkt ved hjælp af den [Aktiver AadrmDocumentTrackingFeature](http://go.microsoft.com/fwlink/?LinkId=623037), og du kan kontrollere, om adgang er i øjeblikket aktiveret eller deaktiveret ved hjælp af [få AadrmDocumentTrackingFeature](http://go.microsoft.com/fwlink/?LinkId=623037).

 Hvis du vil køre disse cmdlets, skal du mindst have version **2.3.0.0** af Azure RMS-modul til Windows PowerShell.  Installationsvejledning, se [installation af Windows PowerShell til Azure Rights Management](https://technet.microsoft.com/library/jj585012.aspx).

> [!TIP]
> Hvis du tidligere har hentet og installeret modulet, kan du kontrollere versionsnummeret ved at køre: `(Get-Module aadrm –ListAvailable).Version`

Følgende URL-adresser, der bruges til dokumentsporing og må (for eksempel føjes til zonen Websteder, hvis du bruger Internet Explorer med udvidet sikkerhed):

-   https://&#42;.azurerms.com

-   https://ecn.dev.virtualearth.net

    > [!NOTE]
    > denne URL-adresse er for Bing maps.

-   https://&#42;.microsoftonline.com

-   https://&#42;.microsoftonline-p.com

### <a name="BKMK_FederatedDomains"></a>Kun AD RMS: Understøttelse af flere e-mail-domæner i organisationen
Hvis du bruger AD RMS og brugere i organisationen har flere e-mail-domæner, skal måske som følge af en fusion eller overtagelse, du foretage følgende redigere i registreringsdatabasen:

1.  Gå til **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC** og hvis den ikke allerede findes, kan du oprette en ny nøgle med navnet **RmsSharingApp**.

2.  Vælg **RmsSharingApp**, oprette en ny Multistrengsværdi med navnet **FederatedDomains**, og derefter tilføje domæner og alle underdomæner, der bruges i din organisation. Jokertegn understøttes ikke.

    For eksempel: Firma, Coho vindyrkningsarealer &amp; Winery er en standard e-mail-domæne på **cohovineyardandwinery.com**, men som følge af fusioner, de også bruger e-mail-domæner **cohowinery.com**, **eastcoast.cohowinery.com**, og **cohovineyard**. For de **FederatedDomains** Værdidata administratoren angiver: **cohowinery.com; eastcoast.cohowinery.com; cohovineyard**

Hvis du ikke foretager denne ændring af registreringsdatabasen, kan brugere muligvis ikke forbruge indhold, der er beskyttet af andre brugere i organisationen. Denne redigering af registreringsdatabasen er ikke nødvendig, hvis du bruger Azure RMS.

## <a name="BKMK_AdminOverview"></a>Teknisk oversigt over Microsoft Rights Management deling program
Microsoft Rights Management deling program er et valgfrit kan downloades program til Microsoft Windows og andre platforme, indeholder følgende:

-   Beskyttelse af en enkelt fil eller bulk-beskyttelse af flere filer samt alle filer i en markeret mappe.

-   Fuld understøttelse af beskyttelsen af en hvilken som helst type fil og en indbygget viewer for almindeligt anvendte filtyper, tekst og billede.

-   Generel beskyttelse for filer, der ikke understøtter RMS-beskyttelse.

-   Fuld kompatibilitet med filer, der er beskyttet ved hjælp af Office IRM Information Rights Management ().

-   Fuld kompatibilitet med PDF-filer, der er beskyttet ved hjælp af SharePoint, FCI og understøttede PDF redigeringsværktøjer.

Microsoft Rights Management deling program bruger den nye [AD RMS-klienten 2.1 runtime](http://www.microsoft.com/download/details.aspx?id=38396). Ved hjælp af giver funktionaliteten af AD RMS 2.1, Microsoft Rights Management deling program slutbrugerne en simpel beskyttelse og forbrug oplevelse.

Med udgivelsen af RMS oktober 2013, du oprindeligt beskytte dokumenter ved hjælp af Office 2010 og sende dem til personer i et andet firma, der derefter kan forbruge dem ved hjælp af Azure RMS. Desuden med denne version, kan Hvis du bruger AD RMS i kryptografiske tilstand 2, du bruge RMS for enkeltpersoner og forbruge indhold fra personer i en anden virksomhed, der bruger Azure RMS. Finde flere oplysninger om kryptografiske tilstand 2 [AD RMS kryptografiske tilstande](http://technet.microsoft.com/library/hh867439%28v=ws.10%29.aspx).

### <a name="BKMK_LevelsofProtection"></a>Niveauer af beskyttelse – oprindelig og generiske
Microsoft Rights Management deling program understøtter beskyttelse på to forskellige niveauer, som beskrevet i følgende tabel.

|Type af beskyttelse|Oprindelig|Generisk|
|-----------------------|--------------|------------|
|Beskrivelse|For tekst, billede, Microsoft Office (Word, Excel, PowerPoint) filer, .PDF-filer og andre filtyper, program, der understøtter AD RMS, giver indbygget beskyttelse en stærk grad af beskyttelse, der omfatter både kryptering og håndhævelse af rettigheder (tilladelser).|For alle andre programmer og filtyper giver generel beskyttelse et højt beskyttelsesniveau, der omfatter både fil-indkapsling ved hjælp af den .pfile filtype og -godkendelse til at kontrollere, hvis en bruger har tilladelse til at åbne filen.|
|Beskyttelse|Filer er fuldt krypteret og beskyttelse håndhæves på følgende måder:<br /><br />-   Før beskyttet indhold er gengivet, skal godkendelsen ske til personer, der modtager filen via e-mail eller får adgang til den via fil eller share-tilladelser.<br />-   Desuden gennemtvinges rettigheder og politik, der er angivet af ejeren af indholdet, når filerne er beskyttet fuldt, når indholdet gengives i IP-Fremviser (til beskyttede filer af tekst og billede) eller det tilknyttede program (for alle andre understøttede filtyper).|Filbeskyttelse gennemtvinges på følgende måder:<br /><br />-   Før beskyttet indhold er gengivet, skal godkendelsen ske for dem, der har tilladelse til at åbne filen og givet adgang til den. Hvis godkendelsen mislykkes, åbnes filen ikke.<br />-   Rettigheder og politik, der er angivet af ejeren af indholdet vises for at oplyse, at autoriserede brugere af politikken, der skal bruges.<br />-   Overvåg logføring af autoriserede brugere åbne og få adgang til filer opstår, men ingen rettigheder håndhæves af ikke understøtter programmer.|
|Standard for filtyper|Dette er standard beskyttelsesniveauet for følgende filtyper:<br /><br />-   Tekst-og billedfiler<br />-   Microsoft Office (Word, Excel, PowerPoint) filer<br />-   Bærbare dokumentformat (.pdf)<br /><br />Yderligere oplysninger finder du i afsnittet [Understøttede filtyper og filtypenavne](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_SupportFileTypes).|Dette er standardbeskyttelse for alle andre filtyper (f.eks. .vsdx, .rtf osv.) ikke understøttes via fuld beskyttelse.|
Du kan ændre beskyttelsesniveauet standard, der anvendes af programmet RMS deling. Du kan ændre standardniveauet for oprindelig til generiske, fra generiske til oprindelig og endda forhindre RMS deling program, der anvender beskyttelse. Yderligere oplysninger finder du i [Hvis du ændrer standardniveauet for beskyttelse af filer](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_ChangeDefaultProtection) afsnit i dette emne.

### <a name="BKMK_SupportFileTypes"></a>Understøttede filtyper og filtypenavne
I følgende tabel viser en liste over filtyper, der har indbygget understøttelse af Microsoft Rights Management deling program. For disse filtyper ændres det oprindelige filtypenavn, når beskyttet oprindelig er anvendt, og disse filer bliver skrivebeskyttet.

Desuden når RMS indbygget Deling af programmet beskytter en Word, Excel eller PowerPoint-fil, der beskytter brugere ved at dele, denne handling opretter automatisk en anden fil, der er en kopi af oprindeligt med det samme navn, men med en **.ppdf** filtypenavn ¹. Denne version af filen sikrer, at modtagerne skal installerer RMS deling program altid kan åbne filen, der har indbygget beskyttelse, der er anvendt.

For filer, der er generisk beskyttet, ændres den oprindelige filtypenavn altid til .pfile.

> [!WARNING]
> Hvis du har firewall, web proxy eller sikkerhedssoftware, kontrollere og handle i overensstemmelse med filtypenavne, skal du konfigurere disse indstillinger for at understøtte disse nye filtypenavne.

|Oprindelige filtypenavn|RMS-beskyttede filtypenavn|
|---------------------------|------------------------------|
|.txt|.ptxt|
|.XML|.pxml|
|.jpg|.pjpg|
|.JPEG|.ppng|
|.PDF|.ppdf|
|.png|.ppng|
|.TIFF|.ptiff|
|.bmp|.pbmp|
|.gif|.pgif|
|.giff|.pgiff|
|.jpe|.pjpe|
|.jfif|.pjfif|
|.jif|.pjif|
|.JT|.pjt|
¹ PDF-gengivelse, der drives af Foxit. Copyright © 2003 – 2014 af Foxit Corporation.

I følgende tabel vises de filtyper, som oprindeligt understøtter programmet Microsoft Rights Management deling i Microsoft Office-2016, 2013 Office og Office 2010. For disse filer uændret filtypenavnet efter at filen er beskyttet af RMS.

|Filtyper, der understøttes af Office|Filtyper, der understøttes af Office|
|----------------------------------------|----------------------------------------|
|.doc<br /><br />.docm<br /><br />.docx<br /><br />.dot<br /><br />.dotm<br /><br />.dotx<br /><br />.potm<br /><br />.potx<br /><br />.pps<br /><br />.ppsm<br /><br />.ppsx<br /><br />.ppt<br /><br />.pptm|.pptx<br /><br />.thmx<br /><br />.xla<br /><br />.xlam<br /><br />.xls<br /><br />.xlsb<br /><br />.xlt<br /><br />.xlsm<br /><br />.xlsx<br /><br />.xltm<br /><br />.xltx<br /><br />.XPS|

### <a name="BKMK_ChangeDefaultProtection"></a>Hvis du ændrer standardniveauet for beskyttelse af filer
Du kan ændre, hvordan RMS deling programmet beskytter filer ved at redigere registreringsdatabasen. For eksempel kan du tvinge filer, der understøtter indbygget beskyttelse skal beskyttes generisk deling RMS-programmet.

Årsager til, hvorfor du måske gerne gøre dette:

-   For at sikre, at alle brugere kan åbne filen fra deres mobilenheder.

-   For at sikre, at alle brugere kan åbne filen, hvis de ikke har et program understøtter, der indbygget beskyttelse.

-   At give plads til sikkerhedssystemer, udføre handlinger på filer af deres filtypenavn og kan omkonfigureres til filtypenavnet .pfile, men ikke kan omkonfigureres til at rumme flere filtypenavne for indbygget beskyttelse.

Desuden kan du gennemtvinge RMS Deling af programmet skal anvende indbygget beskyttelse til filer, som kan have generel beskyttelse, der anvendes som standard. Dette kan være relevant, hvis du har et program, der understøtter RMS-APIs – for eksempel, et line of business-applikation, skrevet af interne udviklerne eller et program, der er købt fra en uafhængig softwareproducent ().

Du kan også tvinge RMS Deling af programmet til at blokere for beskyttelse af filer (gælder ikke indbygget beskyttelse eller generiske beskyttelse). For eksempel kan dette være nødvendigt Hvis du har et automatiseret program eller en tjeneste, der skal være i stand til at åbne en bestemt fil for at behandle indholdet. Når du blokerer beskyttelse for en filtype, kan brugerne ikke bruge RMS deling program til at beskytte en fil med filtypen. Når de prøver, vises en meddelelse om, at administratoren har forhindret beskyttelse og de skal annullere deres indsats for at beskytte filen.

Hvis du vil konfigurere deling af programmet skal anvende generisk beskyttelse til alle filer, der som standard har indbygget beskyttelse anvendes RMS, skal de følgende ændringer i registreringsdatabasen:

1.  **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\RMSSharingApp\FileProtection**: Opret en ny nøgle med navnet **&#42;**.

    Denne indstilling angiver, at filer med et hvilket som helst filtypenavn.

2.  I den nyligt tilføjede nøgle i **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\RMSSharingApp\FileProtection\ &#42;**, oprette en ny strengværdi (REG_SZ) med navnet **kryptering** hvor dataværdien af **Pfile**.

    Denne indstilling medfører deling udlignende generiske programbeskyttelse RMS.

Disse to indstillinger, medføre RMS deling udlignende generiske programbeskyttelse til alle filer med filtypenavnet. Hvis det er dit mål, kræves ingen yderligere konfiguration. Du kan definere undtagelser for bestemte filtyper, så de stadig oprindeligt er beskyttet. Hvis du vil gøre dette, skal du foretage redigeringer i tre yderligere registreringsdatabasen for hver filtype:

1.  **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\RMSSharingApp\FileProtection**: Tilføje en ny nøgle med navnet på filtypenavnet (uden den foregående periode).

    For eksempel for filer, der har en .docx filtypenavn, oprette en nøgle med navnet **DOCX**.

2.  I den nyligt tilføjede fil type nøgle (for eksempel **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\RMSSharingApp\FileProtection\DOCX**), oprette en ny DWORD-værdi med navnet **AllowPFILEEncryption** som har en værdi af **0**.

3.  I den nyligt tilføjede fil type nøgle (for eksempel **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\RMSSharingApp\FileProtection\DOCX**), oprette en ny strengværdi med navnet **kryptering** som har en værdi af **oprindelig**.

Alle filer er generisk beskyttet undtagen filer, der har filtypenavnet .docx, der oprindeligt er beskyttet af programmet RMS deling som følge af disse indstillinger.

Du kan gentage disse tre trin for andre filtyper, som du vil definere som undtagelser, fordi de understøtter indbygget beskyttelse, og du ikke ønsker, de skal beskyttes generisk deling RMS-programmet.

Du kan foretage lignende ændringer i registreringsdatabasen for andre scenarier ved at ændre værdien af den **kryptering** streng, der understøtter følgende værdier:

-   **Pfile**: Generel beskyttelse

-   **Oprindelig**: Indbygget beskyttelse

-   **Off**: Bloker beskyttelse

## Se også
[Rights Management deling program bruger guide](../Topic/Rights_Management_sharing_application_user_guide.md)

