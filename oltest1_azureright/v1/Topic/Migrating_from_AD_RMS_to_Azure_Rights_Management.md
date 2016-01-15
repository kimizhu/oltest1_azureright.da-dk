---
description: na
keywords: na
title: Migrating from AD RMS to Azure Rights Management
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 828cf1f7-d0e7-4edf-8525-91896dbe3172
---
# Overflytning fra AD RMS Azure Rights Management
Brug følgende sæt af instruktioner til at overflytte din installation af Active Directory Rights Management Services (AD RMS) til Azure Rights Management (Azure RMS). Efter overførslen, brugerne har stadig adgang til dokumenter og e-mails, at organisationen beskyttet ved hjælp af AD RMS og nyligt beskyttet indhold bruger Azure RMS.

Tvivl om denne overførsel af AD RMS er bedst til din virksomhed?

-   En introduktion til Azure RMS, virksomhedens problemer, som det kan løses, hvordan den ser ud til administratorer og brugere og hvordan det fungerer, se [Hvad er Azure Rights Management?](../Topic/What_is_Azure_Rights_Management_.md)

-   En sammenligning af Azure RMS med AD RMS, se [Sammenligning af Azure Rights Management og AD RMS](../Topic/Comparing_Azure_Rights_Management_and_AD_RMS.md).

## Forudsætninger for overførsel af AD RMS på Azure RMS
Før du starter overflytningen til Azure RMS, Sørg for, at følgende forudsætninger er på plads, og at du forstår begrænsningerne.

|Kravet om|Yderligere oplysninger|
|-------------|--------------------------|
|En understøttet RMS-installation|Alle versioner af AD RMS i Windows Server 2008 via Windows Server 2012 R2 understøtter en overflytning til Azure RMS:<br /><br />-   Windows Server 2008 (x 86 eller x 64)<br />-   Windows Server 2008 R2 (x 64)<br />-   Windows Server 2012 (x 64)<br />-   Windows Server 2012 R2 (x 64) **Note:** Hvis du kører Windows RMS på Windows Server 2003, vil denne version af operativsystemet ikke support inden 2015. Du kan overføre denne version af RMS til Azure RMS, men denne proces understøttes kun, hvis operativsystemet understøttes stadig. Som en løsning, kan du importere dine publicerer tillidsdomænet (TPD) til en version af AD RMS, der understøttes og genimportere TPD uden indstillingen RMS 1.0 kompatibilitet. Yderligere oplysninger om TPDs, se [Trusted Publishing Domain](http://technet.microsoft.com/library/dd996639%28v=ws.10%29.aspx)<br />Alle gyldige AD RMS-topologier understøttes:<br /><br />-   I en enkelt skov-, enkelt RMS-klyngen<br />-   Enkelt skov, flere kun-licensering-RMS-klynger<br />-   Flere skove, flere RMS-klynger **Note:** Som standard overfører flere RMS-klynger til en enkelt Azure RMS lejer. Hvis du ønsker en anden RMS-lejere, skal du behandle dem som forskellige overførsler. En nøgle fra en RMS-klyngen, kan ikke importeres til mere end én Azure RMS lejer.|
|Alle krav til at køre på Azure RMS, herunder en Azure RMS-lejer (ikke aktiveret)|Se [Krav til Azure rettighedsstyring](../Topic/Requirements_for_Azure_Rights_Management.md).<br /><br />Selvom du skal have en Azure RMS lejer, før du kan overføre fra AD RMS, anbefaler vi, at du ikke aktiverer Rights Management-tjenesten inden overførslen. Overførselsprocessen omfatter dette trin, når du har eksporteret nøgler og skabeloner fra AD RMS og importeret dem til Azure RMS. Men hvis Azure RMS allerede er aktiveret, kan du stadig overføre fra AD RMS.|
|Forberedelse til Azure RMS:<br /><br />-   Directory-synkronisering mellem din lokale mappe og Azure Active Directory<br />-   E-mail-aktiverede grupperne i Azure Active Directory|Se [Forberedelse til Azure rettighedsstyring](../Topic/Preparing_for_Azure_Rights_Management.md).|
|Hvis du har brugt funktionerne i Exchange Server (for eksempel regler for transport og Outlook Web Access) eller SharePoint Server Management IRM (Information Rights) med AD RMS:<br /><br />-   Planen for en kort periode når IRM ikke vil være tilgængelige på disse servere|Du kan fortsætte med at bruge IRM på disse servere med Azure RMS efter overførslen. Et af trinene i overflytning er dog midlertidigt deaktivere tjenesten IRM, installere og konfigurere en forbindelse, omkonfigurere serverne og derefter genaktivere IRM.<br /><br />Dette er kun afbrydelser tjeneste under overflytningen.|
Begrænsninger:

-   Selvom overflytningsprocessen understøtter overførsel af din licens certifikatnøgle (SLC) til en hardware security module (HSM) til Azure RMS-server, understøtter Exchange Online i øjeblikket ikke denne konfiguration. Hvis du vil alle IRM-funktioner i Exchange Online, når du overflytter til Azure RMS, Azure RMS lejer nøglen skal være [administreres af Microsoft](http://technet.microsoft.com/library/dn440580.aspx). Du kan også køre IRM med reducerede funktioner i Exchange Online, mens din Azure RMS lejer administreres af dig (BYOK). Finde flere oplysninger om brug af Exchange Online med Azure RMS [Step 6. Configure IRM integration for Exchange Online](#BKMK_Step6Migration) i denne vejledning.

-   Hvis du har software og klienter, der ikke understøttes med Azure RMS, vil de ikke kunne beskytte eller forbruge indhold, der er beskyttet af Azure RMS. Sørg for at tjekke de understøttede programmer og klienter afsnit i den [Krav til Azure rettighedsstyring](../Topic/Requirements_for_Azure_Rights_Management.md) emne.

-   Hvis du importerer dine lokale nøgle til Azure RMS som arkiveret (du ikke angiver TPD skal være aktiv under importprocessen) og du overflytte brugere i batches for en trinvis overførsel, indhold, der netop er beskyttet af de overførte brugere vil ikke være tilgængelige for brugere, der forbliver på AD RMS. I dette scenario skal så vidt muligt sørger for overflytning af kort og Overflyt brugere i logiske grupper, så hvis de samarbejder med hinanden, de er flyttet sammen.

    Denne begrænsning gælder ikke, når du angiver TPD til active under importprocessen, da alle brugere vil beskytte indhold ved hjælp af den samme nøgle. Vi anbefaler denne konfiguration, da det gør det muligt at overflytte alle brugerne, uafhængigt af hinanden og i dit eget tempo.

-   Hvis du samarbejder med eksterne partnere (for eksempel ved hjælp af pålidelig bruger domæner eller federation), skal de også overflytte til Azure RMS enten på samme tid som din migrering eller snarest muligt derefter. Fortsætte med at få adgang til indhold, at din organisation, der tidligere er beskyttet ved hjælp af AD RMS, de skal foretage klient konfigurationsændringer, der ligner dem, du foretager, og medtages i dette dokument.

    På grund af de mulige konfigurationer variationer, der kan have din partners, er præcise instruktioner til dette omkonfiguration ude af virkefeltet for dette dokument. Hjælp, skal du kontakte Microsoft Customer Support Services (CSS).

## Sådan overflytter AD RMS Azure RMS

|Trin i overflytning|Yderligere oplysninger|
|-----------------------|--------------------------|
|**1. Hent Azure RMS Management administrationsværktøjer**|Yderligere oplysninger finder du [Step 1: Download the Azure Rights Management Administration Tool](../Topic/Migrating_from_AD_RMS_to_Azure_Rights_Management.md#BKMK_Step1Migration).|
|**2. Eksportere konfigurationsdata fra AD RMS og importere den til Azure RMS**|Du eksporterer konfigurationsdata (nøgler, skabeloner, URL-adresser) fra AD RMS til en XML-fil, og overfør derefter filen til Azure RMS ved hjælp af Import-AadrmTpd Windows PowerShell-cmdlet. Yderligere trin kan være nødvendigt, afhængigt af din på vigtige AD RMS-konfiguration:<br /><br />-   Softwaren er beskyttet nøgle til software-beskyttede nøgler overflytning: Centralt administrerede adgangskodebaserede nøgler i AD RMS til Microsoft-styrede Azure RMS lejer nøgle. Dette er den enkleste overflytningssti, og der kræves ingen yderligere trin.<br />-   HSM-beskyttede nøgle til HSM-beskyttede nøgler overflytning: Nøgler, der lagres som en HSM AD RMS til kunde-styrede Azure RMS lejer nøgle (den "sætter din egen nøgle" eller BYOK scenarie). Dette kræver yderligere trin til at overføre nøglen fra din lokale Thales HSM til Azure RMS HSM.<br />-   Softwaren er beskyttet nøgle til HSM-beskyttede nøgler overflytning: Centralt styrede adgangskodebaserede nøgler i AD RMS til kunde-styrede Azure RMS lejer nøgle (den "sætter din egen nøgle" eller BYOK scenarie). Dette kræver de fleste konfigurationen, fordi du skal pakke dit softwarenøgle og importere den til en lokal HSM, og benyt derefter yderligere trin for at overføre nøglen fra din lokale Thales HSM til Azure RMS HSM.<br /><br />Yderligere oplysninger finder du [Step 2. Export configuration data from AD RMS and import it to Azure RMS](../Topic/Migrating_from_AD_RMS_to_Azure_Rights_Management.md#BKMK_Step2Migration).|
|**3. Aktivere din RMS-lejer**|Hvis det er muligt, udføre dette trin efter importen, og ikke før.<br /><br />Finde flere oplysninger og instruktioner, [Step 3. Activate your RMS tenant](../Topic/Migrating_from_AD_RMS_to_Azure_Rights_Management.md#BKMK_Step3Migration).|
|**4. Konfigurere importerede skabeloner**|Når du importerer dine rettigheder politikskabeloner, arkiveres deres status. Hvis du ønsker, at brugere skal kunne se og bruge dem, skal du ændre status skabelon der udgives på portalen Azure Management.<br /><br />Yderligere oplysninger finder du [Step 4. Configure imported templates](../Topic/Migrating_from_AD_RMS_to_Azure_Rights_Management.md#BKMK_Step4Migration).|
|**5. Omkonfigurere klienter til at bruge Azure RMS**|Eksisterende Windows-baserede computere skal konfigureres for at bruge tjenesten Azure RMS i stedet for AD RMS. Dette trin gælder for computere i organisationen og for computere i partnerorganisationer, hvis du har samarbejder med dem, mens du kørte AD RMS.<br /><br />Derudover, hvis du har installeret den [mobilenhed udvidelser](http://technet.microsoft.com/library/dn673574.aspx) til understøttelse af mobile enheder som iOS telefoner og iPads, Android telefoner og tablets, Windows phone og Mac-computere, skal du fjerne SRV-posterne i DNS, omdirigeres disse klienter til at bruge AD RMS.<br /><br />Yderligere oplysninger finder du [Step 5. Reconfigure clients to use Azure RMS](../Topic/Migrating_from_AD_RMS_to_Azure_Rights_Management.md#BKMK_Step5Migration).|
|**6. Konfigurere IRM-integration med Exchange Online**|Dette trin er obligatorisk, hvis du vil bruge Exchange Online med Azure RMS.<br /><br />Yderligere oplysninger finder du [Step 6. Configure IRM integration for Exchange Online](#BKMK_Step6Migration).|
|**7. Installere RMS-stik**|Dette trin er obligatorisk, hvis du vil bruge en af følgende tjenester på stedet med Azure RMS:<br /><br />-   Exchange Server (for eksempel regler for transport og Outlook Web Access)<br />-   SharePoint Server<br />-   Windows-Server, der kører fil klassificering infrastruktur<br /><br />Yderligere oplysninger finder du [Step 7. Deploy the RMS connector](#BKMK_Step7Migration).|
|**8. Fabriksindstillinger AD RMS**|Når du har bekræftet, alle klienter bruger Azure RMS og ikke længere adgang til AD RMS-servere, kan du fabriksindstillinger AD RMS-installation.<br /><br />Yderligere oplysninger finder du [Step 8. Decommission AD RMS](#BKMK_Step8Migration).|
|**9. Nøglen Azure RMS lejer nøglen igen**|Dette trin er obligatorisk, hvis du kørte ikke i kryptografiske tilstand 2, før overførslen, og valgfrit, men anbefales til alle overførsler for at beskytte sikkerheden for din Azure RMS lejer nøgle.<br /><br />Yderligere oplysninger finder du [Step 9. Re-key your Azure RMS tenant key](#BKMK_Step9Migration).|

### <a name="BKMK_Step1Migration"></a>Trin 1: Hent værktøjet til webstedsadministration Azure Rights Management
Gå til Microsoft Download Center, og Hent den [Azure Rights Management Administration Tool](http://go.microsoft.com/fwlink/?LinkId=257721), som indeholder modulet Azure RMS administration til Windows PowerShell.

### <a name="BKMK_Step2Migration"></a>Trin 2. Eksportere konfigurationsdata fra AD RMS og importere den til Azure RMS
Dette trin er en todelt proces:

1.  Eksportere konfigurationsdata fra AD RMS ved at eksportere de betroede udgivelse domæner (TPDs) til en .XML-fil. Denne proces er den samme for alle overførsler.

2.  Importere konfigurationsdata til Azure RMS. Der findes forskellige procedurer for dette trin, afhængigt af den aktuelle konfiguration af AD RMS-installation og dine foretrukne topologi for Azure RMS lejer nøglen.

#### Eksportere konfigurationsdata fra AD RMS
Benyt følgende fremgangsmåde på alle AD RMS-klynger for alle betroede udgivelse domæner, der har beskyttet indhold til din organisation. Du behøver ikke at køre dette på kun-licensering-klynger.

> [!NOTE]
> Hvis du bruger Windows Server 2003 Rights Management, i stedet for disse instruktioner, skal du følge proceduren [eksportere SLC, TUD, TPD og RMS privat nøgle](http://technet.microsoft.com/library/jj835767%28v=ws.10%29.aspx) fra den [overflytning fra Windows RMS til AD RMS i forskellige infrastrukturforvalteres](http://technet.microsoft.com/library/jj835767%28v=ws.10%29.aspx) emne.

###### Hvis du vil eksportere konfigurationsdataene trusted (publishing domæneoplysninger)

1.  Log på AD RMS-klyngen som en bruger med AD RMS brugeradministrative tilladelser.

2.  Fra administrationskonsollen AD RMS (**Active Directory Rights Management Services**), udvid AD RMS-klyngenavnet, udvid **politikker, der er tillid til**, og klik derefter på **Trusted Publishing domæner**.

3.  Vælg publicerer tillidsdomænet i resultatruden, og klik derefter på ruden Handlinger **eksportere publicerer tillidsdomænet**.

4.  I den **eksportere Trusted Publishing Domain** dialogboks:

    -   Klik på **Gem som** og gemme sti og et filnavn efter eget valg. Sørg for at angive **.xml** som filtypenavnet (dette ikke er automatisk tilføjet).

    -   Angiv og Bekræft en stærk adgangskode. Husk denne adgangskode, fordi du skal bruge det senere, når du importerer konfigurationsdata til Azure RMS.

    -   Marker ikke afkrydsningsfeltet for at gemme filen tillidsdomænet i RMS version 1.0.

Når du har eksporteret alle pålidelige udgivelse domæner, er du klar til at starte proceduren for at importere disse data til Azure RMS.

#### Importere konfigurationsdata til Azure RMS
De nærmere procedurer for dette trin afhænger af den aktuelle konfiguration af AD RMS-installation, og dine foretrukne topologi for Azure RMS lejer nøglen.

Din aktuelle AD RMS-installation skal bruge en af følgende konfigurationer for din server Licensgiver (SLC) certifikatnøgle:

-   Beskyttelse med adgangskode i databasen AD RMS. Dette er standardkonfigurationen.

-   HSM beskyttelse ved hjælp af en Thales hardware security module (HSM).

-   HSM beskyttelse ved hjælp af en hardware security module (HSM) fra en anden leverandør end Thales.

-   Beskyttet med en adgangskode ved hjælp af et eksternt program til kryptografiske tjenester.

> [!NOTE]
> Du kan finde flere oplysninger om brugen af hardware sikkerhed moduler med AD RMS i [ved hjælp af AD RMS med Hardware sikkerhed moduler](http://technet.microsoft.com/library/jj651024.aspx).

Der er to Azure RMS lejer nøgle topologi indstillinger: Microsoft administrerer din lejer nøgle (**administreres af Microsoft**) eller du kan administrere din lejer nøgle (**kunde-styrede**). Når du administrerer din egen Azure RMS lejer nøgle, der nogle gange henvises til "sætter din egen nøgle" (BYOK) og kræver en hardware security module (HSM) fra Thales. Yderligere oplysninger finder du i [Choose your tenant key topology: Managed by Microsoft (the default) or managed by you (BYOK)](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_ChooseTenantKey) afsnit i den [Planlægning og implementering af Azure Rights Management lejer nøglen](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md) emne.

> [!IMPORTANT]
> Exchange Online understøtter ikke aktuelt Azure RMS BYOK.  Hvis du vil bruge BYOK efter overflytningen og planlægger at bruge Exchange Online, skal du kontrollere, at du forstår, hvordan denne konfiguration reducerer IRM-funktionaliteten for Exchange Online. Gennemse oplysningerne i den [BYOK pricing and restrictions](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_Pricing) afdeling i den  [Planlægning og implementering af Azure Rights Management lejer nøglen](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md) emne til at hjælpe dig med at vælge den bedste Azure RMS lejers nøgle topologi for overførslen.

Brug følgende tabel til at identificere, hvilken procedure der skal bruges til overflytningen. Kombinationer, der ikke er angivet, understøttes ikke.

|Aktuelle AD RMS-installation|Valgte Azure RMS lejer nøgle topologi|Vejledning til overflytning|
|--------------------------------|-----------------------------------------|-------------------------------|
|Beskyttelse med adgangskode i databasen AD RMS|Microsoft-styrede|Se den **Software beskyttet for at beskyttet software nøgle migration** procedure efter denne tabel.<br /><br />Dette er den enkleste overflytningssti og kræver kun, at du overfører din konfigurationsdata til Azure RMS.|
|HSM beskyttelse ved hjælp af en Thales nShield hardware security module (HSM)|Kunde-styrede (BYOK)|Se den **HSM beskyttet nøgle til HSM-beskyttede nøgler migration** procedure efter denne tabel.<br /><br />Det kræver BYOK værktøjssæt og to sæt trin for at overføre nøglen fra din lokale HSM til Azure RMS-HSMs og derefter overføre konfigurationsdataene til Azure RMS.|
|Beskyttelse med adgangskode i databasen AD RMS|Kunde-styrede (BYOK)|Se den **Software beskyttet for at HSM-beskyttede nøgler migration** procedure efter denne tabel.<br /><br />Dette kræver værktøjssæt, der er BYOK, og tre sæt af trin i første pakke dine softwarenøgle og importere den til en lokal HSM, derefter overføre nøglen fra din lokale HSM til Azure RMS-HSMs, og endelig overførsel af konfigurationsdataene på Azure RMS.|
|HSM beskyttelse ved hjælp af en hardware security module (HSM) fra en anden leverandør end Thales|Kunde-styrede (BYOK)|Kontakt leverandøren for at du HSM instruktioner hvordan du overfører din nøgle fra denne HSM til et Thales nShield Hardware Security Module (HSM). Følg derefter instruktionerne for den **HSM beskyttet nøgle til HSM-beskyttede nøgler migration** procedure efter denne tabel.|
|Adgangskode, der er beskyttet ved hjælp af et eksternt program til kryptografiske tjenester|Kunde-styrede (BYOK)|Kontakt leverandøren for at du kryptografiske oplysninger, hvordan du overfører din nøgle til et Thales nShield hardware security module (HSM). Følg derefter instruktionerne for den **HSM beskyttet nøgle til HSM-beskyttede nøgler migration** procedure efter denne tabel.|
Før du starter procedurerne, Sørg for, at du kan få adgang til .XML-filer, som du oprettede tidligere, når du har eksporteret de udgivelse domæner, der er tillid til. Disse kan eksempelvis gemmes på et USB-tommelfingeren drev, som du flytter fra AD RMS-serveren til den Internet-opkoblet arbejdsstation.

> [!NOTE]
> Dog kan du gemme disse filer, Brug Sikkerhed bedste fremgangsmåder til at beskytte dem, fordi disse data omfatter din private nøgle.

##### Softwaren er beskyttet for at beskyttet software nøgle overflytning
Brug denne procedure til at importere konfigurationsfilen AD RMS på Azure RMS, vil medføre Azure RMS lejer nøglen, der administreres af Microsoft.

###### Importere konfigurationsdata til Azure RMS

1.  På en Internet-opkoblet arbejdsstation, hente og installere Windows PowerShell-modul til Azure RMS (minimum version 2.1.0.0), som indeholder de [Import-AadrmTpd](http://msdn.microsoft.com/library/azure/dn857523.aspx) cmdlet.

    > [!TIP]
    > Hvis du tidligere har hentet og installeret modulet, kan du kontrollere versionsnummeret ved at køre: `(Get-Module aadrm -ListAvailable).Version`

    Installationsvejledning, se [Installation af Windows PowerShell til Azure rettighedsstyring](../Topic/Installing_Windows_PowerShell_for_Azure_Rights_Management.md).

2.  Start Windows PowerShell med de **Kør som administrator** indstilling og bruge den [Connect-AadrmService](http://msdn.microsoft.com/library/azure/dn629415.aspx) -cmdlet til at oprette forbindelse til tjenesten Azure RMS:

    ```
    Connect-AadrmService
    ```
    Når du bliver bedt om det, kan du angive din [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] lejers administratorlegitimationsoplysninger (typisk, du vil bruge en konto, der er en global administrator for Azure Active Directory eller Office 365).

3.  Brug af [Import-AadrmTpd](http://msdn.microsoft.com/library/azure/dn857523.aspx) -cmdlet til at overføre først eksporteret pålidelige udgivelse domæne (.xml)-fil. Hvis du har mere end en .XML-fil, fordi du havde flere domæner med tillid til udgivelse, kan du vælge den fil, der indeholder eksporterede publicerer tillidsdomænet, du vil bruge i Azure RMS til at beskytte indhold efter overførslen. Du kan bruge følgende kommando:

    ```
    Import-AadrmTpd -TpdFile <PathToTpdPackageFile> -ProtectionPassword -Active $True -Verbose
    ```
    For eksempel: **Import-AadrmTpd -TpdFile E:\contosokey1.xml -ProtectionPassword -Active $true -Verbose**

    Når du bliver bedt om det, Angiv den adgangskode, du tidligere har angivet, og bekræfte, at du vil udføre denne handling.

4.  Når kommandoen er udført, Gentag trin 3 for hver resterende .XML-fil, du har oprettet ved at eksportere dine udgivelse domæner, der er tillid til. Men for disse filer, kan du indstille **-Active** til **false** Når du kører kommandoen Importer. For eksempel: **Import-AadrmTpd -TpdFile E:\contosokey2.xml -ProtectionPassword -Active $false -Verbose**

5.  Brug af [afbrydelse-AadrmService](http://msdn.microsoft.com/library/azure/dn629416.aspx) -cmdlet til at afbryde forbindelsen til tjenesten Azure RMS:

    ```
    Disconnect-AadrmService
    ```

Du er nu klar til at gå til [Step 3. Activate your RMS tenant](../Topic/Migrating_from_AD_RMS_to_Azure_Rights_Management.md#BKMK_Step3Migration).

##### HSM-beskyttede nøgle til HSM-beskyttede nøgler overflytning
Det er en todelt fremgangsmåde til at importere HSM nøgle og konfiguration af AD RMS på Azure RMS, vil medføre Azure RMS lejer nøglen, der administreres af dig (BYOK).

Du skal først pakke HSM-tasten, så det er klar til at overføre til Azure RMS, og derefter importere den med konfigurationsdata.

###### Del 1: Pakke HSM-tasten, så den er klar til at overføre til Azure RMS

1.  Følg trinnene i den [Implementing bring your own key (BYOK)](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_ImplementBYOK) del af den [Planlægning og implementering af Azure Rights Management lejer nøglen](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md), ved hjælp af proceduren, der **Generer og overføre din lejer nøgle – via internettet** med følgende undtagelser:

    -   Følg ikke trin til **generere lejer nøglen**, fordi du allerede har tilsvarende fra AD RMS-installation. Du skal identificere den nøgle, der bruges af AD RMS-serveren fra Thales-installationen og bruge denne nøgle under overflytningen. Krypterede nøgler filer navngives normalt Thales **key_(keyAppName)_(keyIdentifier)** lokalt på serveren.

    -   Følg ikke trin til **overføre din lejer nøgle til Azure RMS**, som bruger kommandoen Tilføj AadrmKey.  I stedet overfører din forberedt HSM nøgle, når du overfører dine eksporterede publicerer tillidsdomænet, ved hjælp af kommandoen Import-AadrmTpd.

2.  På den Internet-opkoblet arbejdsstation i Windows PowerShell-session, genoprette forbindelsen til tjenesten Azure RMS.

Nu hvor du har forberedt din HSM nøgle til Azure RMS, er du klar til at importere nøglefilen til HSM og AD RMS-konfigurationsdata.

###### Del 2: Importere HSM nøgle og konfiguration data til Azure RMS

1.  Stadig på Internet-forbindelse arbejdsstationen og Windows PowerShell-session, overføre første eksporterede pålidelige udgivelse domæne (.xml) filen. Hvis du har mere end en .XML-fil, fordi du havde flere domæner med tillid til udgivelse, kan du vælge den fil, der indeholder eksporterede publicerer tillidsdomænet, der svarer til HSM nøgle, du vil bruge i Azure RMS til at beskytte indhold efter overførslen. Du kan bruge følgende kommando:

    ```
    Import-AadrmTpd -TpdFile <PathToTpdPackageFile> -ProtectionPassword -HsmKeyFile <PathToBYOKPackage> -Active $True -Verbose
    ```
    For eksempel: **Import -TpdFile E:\no_key_tpd_contosokey1.xml  -HsmKeyFile E:\KeyTransferPackage-contosokey.byok -ProtectionPassword -Active $true -Verbose**

    Når du bliver bedt om det, Angiv den adgangskode, du tidligere har angivet, og bekræfte, at du vil udføre denne handling.

2.  Når kommandoen er fuldført, skal du gentage trin 1 for hver resterende .XML-fil, du har oprettet ved at eksportere dine udgivelse domæner, der er tillid til. Men for disse filer, kan du indstille **-Active** til **false** Når du kører kommandoen Importer.  For eksempel: **Import -TpdFile E:\contosokey2.xml -HsmKeyFile E:\KeyTransferPackage-contosokey.byok -ProtectionPassword -Active $false -Verbose**

3.  Brug af [afbrydelse-AadrmService](http://msdn.microsoft.com/library/windowsazure/dn629416.aspx) -cmdlet til at afbryde forbindelsen til tjenesten Azure RMS:

    ```
    Disconnect-AadrmService
    ```

Du er nu klar til at gå til [Step 3. Activate your RMS tenant](../Topic/Migrating_from_AD_RMS_to_Azure_Rights_Management.md#BKMK_Step3Migration).

##### Softwaren er beskyttet for at HSM-beskyttede nøgler overflytning
Det er en fremgangsmåde i tre dele at importere konfigurationsfilen AD RMS på Azure RMS, vil medføre Azure RMS lejer nøglen, der administreres af dig (BYOK).

Du skal pakke din server Licensgiver (SLC) certifikatnøgle fra konfigurationsdata og overføre nøglen til en lokal Thales HSM og derefter pakke og overføre din HSM nøgle til Azure RMS og derefter importere konfigurationsdata.

###### Del 1: Pak din SLC fra konfigurationsdata og importere nøglen til din lokale HSM

1.  Brug følgende trin i den [Implementing bring your own key (BYOK)](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_ImplementBYOK) del af den [Planlægning og implementering af Azure Rights Management lejer nøglen](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md) emne:

    -   **Opret og Overfør din lejer nøgle – via internettet**: **Forbered din Internet-opkoblet arbejdsstation.**

    -   **Opret og Overfør din lejer nøgle – via internettet**: **Forberede arbejdsstationen afbrudt**

    Ikke følge disse trin for at generere nøglen lejer, fordi du allerede har tilsvarende i den eksporterede konfiguration-datafil (.xml). I stedet skal du køre en kommando til at udtrække nøglen fra filen og importere den til din lokale HSM.

2.  På den afbrudte arbejdsstation, skal du køre følgende kommando:

    ```
    KeyTransferRemote.exe -ImportRmsCentrallyManagedKey -TpdFilePath <TPD> -ProtectionPassword -KeyIdentifier <KeyID> -ExchangeKeyPackage <BYOK-KEK-pka-Region> -NewSecurityWorldPackage <BYOK-SecurityWorld-pkg-Region>
    ```
    For eksempel til Nordamerika: **KeyTransferRemote.exe -ImportRmsCentrallyManagedKey -TpdFilePath E:\contosokey1.xml -ProtectionPassword -KeyIdentifier contosorms1key –- -ExchangeKeyPackage &lt;BYOK-KEK-pka-NA-1&gt; -NewSecurityWorldPackage &lt;BYOK-SecurityWorld-pkg-NA-1&gt;**

    Yderligere oplysninger:

    -   Parameteren ImportRmsCentrallyManagedKey angiver, at handlingen er at importere SLC-nøgle.

    -   Hvis du ikke angiver adgangskoden i kommandoen, bliver du bedt om at angive den.

    -   Parameteren KeyIdentifier er for fulde navn på en nøgle, der opretter nøgler filnavnet. Du skal bruge små ASCII-tegn.

    -   Parameteren ExchangeKeyPackage angiver en område-specifik nøgleudveksling nøgle (KEK)-pakke, der har et navn, der begynder med BYOK-KEK - pkg-.

    -   Parameteren NewSecurityWorldPackage angiver en område-specifik sikkerhedspakke-verden, der har et navn, der begynder med BYOK-SecurityWorld - pkg-.

    Denne kommando resulterer i følgende:

    -   En nøglefil til HSM: %NFAST_KMDATA%\local\key_mscapi_ &lt; KeyID &gt;

    -   RMS data konfigurationsfilen med SLC fjernet: %NFAST_KMDATA%\local\no_key_tpd_ &lt; KeyID &gt; .xml

3.  Hvis du har mere end én RMS data konfigurationsfiler, skal du gentage trin 2 for resten af disse filer.

Nu, hvor din SLC er fjernet, så det er en HSM-baserede nøgle, er du klar til at pakke og overføre det til Azure RMS.

###### Del 2: Pakke og overføre din HSM nøgle til Azure RMS

1.  Brug følgende trin fra den [Implementing bring your own key (BYOK)](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_ImplementBYOK) del af den [Planlægning og implementering af Azure Rights Management lejer nøglen](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md):

    -   **Opret og Overfør din lejer nøgle – via internettet**: **Forbered din lejer nøgle til overførsel**

    -   **Opret og Overfør din lejer nøgle – via internettet**: **Overfør din lejer nøgle til Azure RMS**

Nu hvor du har overført HSM nøglen til Azure RMS, er du klar til at importere dataene AD RMS-konfiguration, der indeholder kun en henvisning til den overførte lejer nøgle.

###### Del 3: Importere konfigurationsdata til Azure RMS

1.  Stadig på arbejdsstationen Internetforbindelse og Windows PowerShell-session, overskrive konfigurationsfiler RMS med SLC, der er fjernet (fra den afbrudte arbejdsstation %NFAST_KMDATA%\local\no_key_tpd_ &lt; KeyID &gt; .xml)

2.  Overfør den første fil. Hvis du har mere end en .XML-fil, fordi du havde flere domæner med tillid til udgivelse, kan du vælge den fil, der indeholder eksporterede publicerer tillidsdomænet, der svarer til HSM nøgle, du vil bruge i Azure RMS til at beskytte indhold efter overførslen. Du kan bruge følgende kommando:

    ```
    Import-AadrmTpd -TpdFile <PathToNoKeyTpdPackageFile> -ProtectionPassword -HsmKeyFile <PathToKeyTransferPackage> -Active $true -Verbose
    ```
    For eksempel: **Import -TpdFile E:\no_key_tpd_contosorms1key.xml -ProtectionPassword -HsmKeyFile E:\KeyTransferPackage-contosorms1key.byok -Active $true -Verbose**

    Når du bliver bedt om det, Angiv den adgangskode, du tidligere har angivet, og bekræfte, at du vil udføre denne handling.

3.  Når kommandoen er fuldført, skal du gentage trin 2 for hver resterende .XML-fil, du har oprettet ved at eksportere dine udgivelse domæner, der er tillid til. Men for disse filer, kan du indstille **-Active** til **false** Når du kører kommandoen Importer. For eksempel: **Import -TpdFile E:\no_key_tpd_contosorms2key.xml -ProtectionPassword -HsmKeyFile E:\KeyTransferPackage-contosorms1key.byok -Active $false -Verbose**

4.  Brug af [afbrydelse-AadrmService](http://msdn.microsoft.com/library/windowsazure/dn629416.aspx) -cmdlet til at afbryde forbindelsen til tjenesten Azure RMS:

    ```
    Disconnect-AadrmService
    ```

Du er nu klar til at gå til [Step 3. Activate your RMS tenant](../Topic/Migrating_from_AD_RMS_to_Azure_Rights_Management.md#BKMK_Step3Migration).

### <a name="BKMK_Step3Migration"></a>Trin 3. Aktivere din RMS-lejer
Instruktioner til dette trin dækkes fuldt ud i den [Aktivering af Azure rettighedsstyring](../Topic/Activating_Azure_Rights_Management.md) emne.

> [!TIP]
> Hvis du har et abonnement på Office 365, kan du aktivere Azure RMS på Office 365 admin Center eller Azure Management Portal. Vi anbefaler, at du bruger portalen Azure Management, fordi du vil bruge denne management portal til at udføre de næste trin.

**Hvad nu, hvis din lejer Azure RMS allerede er aktiveret?** Hvis tjenesten Azure RMS allerede er aktiveret for din organisation, kan brugerne har allerede brugt Azure RMS til at beskytte indholdet med en automatisk genereret lejer nøgle (og standardskabelonerne) i stedet for eksisterende nøgler (og skabeloner) fra AD RMS. Det er usandsynligt, at ske på computere, der er godt styret på intranettet, fordi de konfigureres automatisk til din AD RMS-infrastruktur. Men det kan ske på arbejdsgruppecomputere eller computere, som jævnligt opretter forbindelse til intranettet. Desværre, det er også svært at identificere disse computere, hvilket er grunden til, at vi anbefaler, at du ikke aktiverer tjenesten, før du importerer konfigurationsdata fra AD RMS.

Hvis din lejer Azure RMS allerede er aktiveret, og du kan identificere disse computere, Sørg for, at du kører scriptet CleanUpRMS_RUN_Elevated.cmd på disse computere, som beskrevet i trin 5. Kørsel af dette script tvinger dem at geninitialisere brugermiljø, så de kan hente den opdaterede lejer nøgle og importerede skabeloner.

### <a name="BKMK_Step4Migration"></a>Trin 4. Konfigurere importerede skabeloner
Fordi de skabeloner, du har importeret en standardtilstanden for **arkiveret**, skal du ændre denne tilstand for at være **udgivet** Hvis du ønsker, at brugere skal kunne bruge disse skabeloner til Azure RMS.

Hvis dine skabeloner på AD RMS bruges desuden i **ANYONE** gruppen, fjernes denne gruppe automatisk, når du importerer skabelonerne til Azure RMS, skal du manuelt føje den samme gruppe eller brugere og de samme rettigheder til de importerede skabeloner. Gruppen svarer til Azure RMS hedder **AllStaff-&lt;tenant_GUID&gt;@&lt;tenant_name&gt;.onmicrosoft.com&gt;**. For eksempel denne gruppe kan ligne følgende for Contoso, Ltd: **AllStaff-9c11c87a-ac8b-46a3-8d5c-f4d0b72ee29a@contoso.onmicrosoft.com**.

Du kan se din organisation er automatisk oprettet gruppe, hvis du kopierer en af standard rettigheder politikskabeloner på portalen Azure og derefter identificere det **brugernavn** på den **rettigheder** side. Dog Azure portalen kan ikke bruges til at tilføje denne gruppe og skal i stedet bruge en af følgende indstillinger for Azure RMS PowerShell:

-   Brug af [eksport-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727078.aspx) -cmdlet til Eksporter skabelon til en. Csv-fil, som du kan redigere for at tilføje "AllStaff"-gruppe og rettigheder til de eksisterende grupper og rettigheder, og derefter bruge den [Import-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727077.aspx) -cmdlet til import af denne ændring tilbage til Azure RMS.

-   Brug af [Ny-AadrmRightsDefinition](https://msdn.microsoft.com/library/azure/dn727080.aspx) PowerShell-cmdlet til at definere gruppen "AllStaff" og med rettigheder som et objekt til definition af rettigheder og køre denne kommando igen for at definere de eksisterende grupper og rettigheder til skabelonen. Derefter tilføje disse objekter til definition af rettigheder til skabelonerne ved hjælp af den [Tilføj AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727075.aspx) cmdlet.

> [!NOTE]
> Gruppen "AllStaff" svarer ikke på samme måde som ANYONE i AD RMS:  Gruppen "AllStaff" omfatter alle brugere i din Azure lejer gruppen Alle omfatter alle godkendte brugere, der kan være uden for organisationen.
> 
> På grund af denne forskel mellem de to grupper skal du også tilføje eksterne brugere ud over gruppen "AllStaff". Eksterne e-mail-adresser til grupper understøttes ikke i øjeblikket.

Skabeloner, du importerer fra en AD RMS ser ud og opfører sig på samme måde som brugerdefinerede skabeloner, du kan oprette i Azure Management Portal. Hvis du vil ændre importerede skabeloner, der skal offentliggøres, så brugerne kan se dem og vælge dem fra programmer eller foretage andre ændringer til skabelonerne, se [Konfiguration af brugerdefinerede skabeloner til Azure rettighedsstyring](../Topic/Configuring_Custom_Templates_for_Azure_Rights_Management.md).

> [!TIP]
> For en mere ensartet oplevelse for brugere under overflytningen, foretag ændringer til de importerede skabeloner end disse to ændringer. og ikke udgive de to standardskabeloner, der følger med Azure RMS, eller oprette nye skabeloner på dette tidspunkt. I stedet vente overførselsprocessen er fuldført, og du har ikke i funktion AD RMS-serverne.

### <a name="BKMK_Step5Migration"></a>Trin 5. Omkonfigurere klienter til at bruge Azure RMS
For Windows-klienter:

1.  [Hente overflytningsscriptene](http://go.microsoft.com/fwlink/?LinkId=524619):

    -   CleanUpRMS_RUN_Elevated.cmd

    -   Redirect_OnPrem.cmd

    Disse scripts nulstille konfigurationen på Windows-computere, så de bruger Azure RMS service i stedet for AD RMS.

2.  Følg vejledningen i omdirigering af script (Redirect_OnPrem.cmd) til at redigere scriptet til at pege på din nye Azure RMS lejer.

3.  På Windows-computere at køre disse scripts med administratorrettigheder i brugerens kontekst.

Mobil enhed klienter og Mac-computere:

-   Fjerne DNS SRV-poster, som du oprettede, da du installerede den [AD RMS mobilenhed udvidelse](http://technet.microsoft.com/library/dn673574.aspx).

#### Ændringer foretaget af overflytningsscriptene
Dette afsnit dokumenterer de ændringer, der foretager overførslen-scripts. Du kan bruge disse oplysninger kun til reference eller i forbindelse med fejlfinding, eller hvis du foretrækker at foretage disse ændringer af dig selv.

CleanUpRMS_RUN_Elevated.cmd:

-   Slet indholdet i mapperne %userprofile%\AppData\Local\Microsoft\DRM og %userprofile%\AppData\Local\Microsoft\MSIPC, herunder alle undermapper og filer med lange filnavne.

-   Slet indholdet af følgende nøgler i registreringsdatabasen:

    -   HKEY_LOCAL_MACHINE\Software\Microsoft\Office\ (11.0|12.0|14.0) \Common\DRM

    -   HKEY_CURRENT_USER\Software\Microsoft\Office\ (11.0|12.0|14.0) \Common\DRM

    -   HKEY_LOCAL_MACHINE\Software\WoW6432Node\Microsoft\Office\ (11.0|12.0|14.0) \Common\DRM

    -   HKEY_CURRENT_USER\Software\WoW6432Node\Microsoft\Office\ (11.0|12.0|14.0) \Common\DRM

    -   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation

    -   HKEY_LOCAL_MACHINE\SOFTWARE\WoW6432Node\Microsoft\MSIPC\ServiceLocation

    -   HKEY_LOCAL_MACHINE\Software\Microsoft\MSDRM\ServiceLocation

-   Slet følgende værdier i registreringsdatabasen:

    -   HKEY_CURRENT_USER\Software\Microsoft\Office\15.0\Common\DRM\DefaultServerURL

    -   HKEY_CURRENT_USER\Software\Microsoft\Office\15.0\Common\DRM\DefaultServer

Redirect_OnPrem.cmd:

-   Opret følgende værdier i registreringsdatabasen for hver URL-adresse, der er angivet som en parameter under hver af de følgende steder:

    -   HKEY_CURRENT_USER\Software\Microsoft\Office\ (11.0|12.0|14.0) \Common\DRM\LicenseServerRedirection

    -   HKEY_CURRENT_USER\Software\WoW6432Node\Microsoft\Office\ (11.0|12.0|14.0) \Common\DRM\LicenseServerRedirection

    -   HKEY_LOCAL_MACHINE\Software\Microsoft\Office\ (11.0|12.0|14.0) \Common\DRM\LicenseServerRedirection

    -   HKEY_LOCAL_MACHINE\Software\WoW6432Node\Microsoft\Office\ (11.0|12.0|14.0) \Common\DRM\LicenseServerRedirection

    -   HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC\LicensingRedirection

    Hver post er en REG_SZ-værdien **https://OldRMSserverURL/_wmcs/licensing** med dataene i følgende format: **https://&lt;YourTenantURL&gt;/_wmcs/licensing**.

    > [!NOTE]
    > *&lt; YourTenantURL &gt;* har følgende format: **-{GUID} .rms. [område].aadrm.com**.
    > 
    > For eksempel:  5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com
    > 
    > Du kan finde denne værdi ved at identificere den **RightsManagementServiceId** værdi, når du kører den [få AadrmConfiguration](http://msdn.microsoft.com/library/windowsazure/dn629410.aspx) cmdlet til Azure RMS.

### <a name="BKMK_Step6Migration"></a>Trin 6. Konfigurere IRM-integration til Exchange Online
Hvis du tidligere har importeret dine TDP fra AD RMS til Exchange Online, skal du fjerne denne TDP for at undgå konflikt mellem skabeloner og politikker, når du har overflyttet til Azure RMS. Du kan bruge den [Fjern RMSTrustedPublishingDomain](https://technet.microsoft.com/en-us/library/jj200720%28v=exchg.150%29.aspx) cmdlet fra Exchange Online.

Hvis du vælger en Azure RMS lejers nøgle topologien for **Microsoft administreret**:

-   Se den [Exchange Online: IRM-konfigurationen](../Topic/Configuring_Applications_for_Azure_Rights_Management.md#BKMK_ExchangeOnline) afsnit i den [Konfiguration af programmer for Azure rettighedsstyring](../Topic/Configuring_Applications_for_Azure_Rights_Management.md) emne. Dette afsnit indeholder typisk kommandoer til at køre, der opretter forbindelse til Exchange Online-tjenesten, importerer nøglen lejer fra RMS Azure og aktiverer IRM-funktionalitet til Exchange Online. Når du har fuldført disse trin, får du alle RMS-funktioner i Exchange Online.

Hvis du vælger en Azure RMS lejers nøgle topologien for **kunde-styrede (BYOK)**:

-   Har reduceret vil RMS-funktionalitet med Exchange Online, som beskrevet i den [BYOK pricing and restrictions](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_Pricing) afdeling i den [Planlægning og implementering af Azure Rights Management lejer nøglen](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md) emne.

### <a name="BKMK_Step7Migration"></a>Trin 7. Installere RMS-stik
Hvis du har brugt funktionerne i Exchange Server eller SharePoint Server Management IRM (Information Rights) med AD RMS, skal du først deaktivere IRM på disse servere og fjerne AD RMS-konfiguration. Derefter installere Rights Management (RMS)-stik, der fungerer som en kommunikation grænseflade (relay) mellem lokale servere og Azure RMS.

Endelig for dette trin, skal Hvis du har importeret flere TPDs til Azure RMS, der blev brugt til at beskytte e-mail-meddelelser, du manuelt redigere registreringsdatabasen på Exchange Server-computere til at omdirigere URL-adresser til alle TPDs til RMS-stik.

> [!NOTE]
> Før du begynder, skal du kontrollere understøttede versioner af de lokale servere, der understøtter RMS-stik i "lokale servere, der understøtter Azure RMS" den [Programmer, der understøtter Azure RMS](../Topic/Requirements_for_Azure_Rights_Management.md#BKMK_SupportedApplications) del af den [Krav til Azure rettighedsstyring](../Topic/Requirements_for_Azure_Rights_Management.md) emne.

##### Deaktivere IRM på Exchange-servere og fjerne AD RMS-konfiguration

1.  Find følgende mappe på alle Exchange-servere, og slette alle posterne i denne mappe: \ProgramData\Microsoft\DRM\Server\S-1-5-18

2.  Fra en af Exchange-servere, skal du bruge udveksling [Set_IRMConfiguration](http://technet.microsoft.com/library/dd979792.aspx) -cmdlet til deaktivering først IRM-funktioner til meddelelser, der sendes til interne modtagere:

    ```
    Set-IRMConfiguration -InternalLicensingEnabled $false
    ```

3.  Derefter skal du bruge samme cmdlet til at deaktivere IRM-funktioner for meddelelser, der sendes til eksterne modtagere:

    ```
    Set-IRMConfiguration -ExternalLicensingEnabled $false
    ```

4.  Brug derefter samme cmdlet til deaktivering af IRM i Microsoft Office Outlook Web App og Microsoft Exchange ActiveSync:

    ```
    Set-IRMConfiguration -ClientAccessServerEnabled $false
    ```

5.  Endelig skal bruge samme cmdlet til at rydde alle cachelagrede certifikater:

    ```
    Set-IRMConfiguration -RefreshServerCertificates
    ```

6.  På de enkelte Exchange Server-nu Nulstil IIS, for eksempel ved at køre en kommandoprompt som administrator og skrive **iisreset**.

##### Deaktivere IRM på SharePoint-servere og fjerne AD RMS-konfiguration

1.  Sørg for, at der er ingen dokumenter, der er tjekket ud fra RMS-beskyttede biblioteker. Hvis der er der de bliver tilgængelig i slutningen af denne procedure.

2.  I SharePoint Central Administration af websted, i det **Hurtig start** skal du klikke på **sikkerhed**.

3.  På den **sikkerhed** side i den **informationspolitik** skal du klikke på **konfigurere IRM**.

4.  På den **Information Rights Management** side i den **Information Rights Management** afsnit, Vælg **må ikke bruge IRM på denne server**, klik derefter på **OK**.

5.  I hvert af SharePoint Server-computerne, skal du slette indholdet af den mappe \ProgramData\Microsoft\MSIPC\Server\*&lt; SID for den konto, der kører SharePoint Server &gt;*.

##### Installer og Konfigurer RMS-stik

-   Brug instruktionerne i den [Installation af Azure Rights Management-stik](../Topic/Deploying_the_Azure_Rights_Management_Connector.md) emne.

##### Kun Exchange og flere TPDs: Rediger registreringsdatabasen

-   På de enkelte Exchange Server-manuelt føje følgende nøgler i registreringsdatabasen for hver ekstra TPD, du importerede, hvis du vil omdirigere TPD URL-adresser til RMS-stikket. Disse poster i registreringsdatabasen, der er specifikke for migration og tilføjes ikke som værktøjet til konfiguration af serveren til Microsoft RMS connector.

    Når du foretager disse ændringer i registreringsdatabasen, kan du bruge følgende instruktioner:

    -   Erstat *ConnectorFQDN* med det navn, du har defineret i DNS for forbindelsen. For eksempel **rmsconnector.contoso.com**.

    -   Du kan bruge præfikset HTTP eller HTTPS connector URL-adresse, afhængigt af om du har konfigureret forbindelsen for at bruge HTTP- eller HTTPS til at kommunikere med dine lokale servere.

    **For Exchange-2013:**

    |Sti til registreringsdatabasen|Type|Værdi|Data|
    |----------------------------------|--------|---------|--------|
    |HKLM\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\LicenseServerRedirection|Reg_SZ|RMS Intranet Licensing URL https://&lt;ad &gt;/_wmcs/licens|En af følgende fremgangsmåder, afhængigt af om du bruger HTTP eller HTTPS fra Exchange-serveren til RMS-forbindelse:<br /><br />-   http://&lt;connectorFQDN&gt;/_wmcs/Licensing<br />-   https://&lt;connectorName&gt;/_wmcs/Licensing|
    |HKLM\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\LicenseServerRedirection|Reg_SZ|RMS ekstranet Licensing URL https://&lt;ad &gt;/_wmcs/licens|En af følgende fremgangsmåder, afhængigt af om du bruger HTTP eller HTTPS fra Exchange-serveren til RMS-forbindelse:<br /><br />-   http://&lt;connectorFQDN&gt;/_wmcs/Licensing<br />-   https://&lt;connectorFQDN&gt;/_wmcs/Licensing|
    **For Exchange Server 2010:**

    |Sti til registreringsdatabasen|Type|Værdi|Data|
    |----------------------------------|--------|---------|--------|
    |HKLM\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\LicenseServerRedirection|Reg_SZ|RMS Intranet Licensing URL https://&lt;ad &gt;/_wmcs/licens|En af følgende fremgangsmåder, afhængigt af om du bruger HTTP eller HTTPS fra Exchange-serveren til RMS-forbindelse:<br /><br />-   http://&lt;connectorName&gt;/_wmcs/Licensing<br />-   https://&lt;connectorName&gt;/_wmcs/Licensing|
    |HKLM\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\LicenseServerRedirection|Reg_SZ|RMS ekstranet Licensing URL https://&lt;ad &gt;/_wmcs/licens|En af følgende fremgangsmåder, afhængigt af om du bruger HTTP eller HTTPS fra Exchange-serveren til RMS-forbindelse:<br /><br />-   http://&lt;connectorName&gt;/_wmcs/Licensing<br />-   https://&lt;connectorName&gt;/_wmcs/Licensing|

Når du har fuldført disse procedurer, skal du læse den **Næste trin** afsnit i den [Installation af Azure Rights Management-stik](../Topic/Deploying_the_Azure_Rights_Management_Connector.md) emne.

### <a name="BKMK_Step8Migration"></a>Trin 8. Fabriksindstillinger AD RMS
Valgfrit: Du kan fjerne Service Connection Point (SCP) fra Active Directory for at forhindre, at computere discovering infrastrukturen på stedet Rights Management. Det er valgfrit, fordi omdirigering, som du har konfigureret i registreringsdatabasen (for eksempel ved at køre scriptet overflytning). Hvis du vil fjerne Service Connection Point, skal du bruge værktøjet AD SCP Register fra den [Rights Management Services Administration Toolkit](http://www.microsoft.com/download/details.aspx?id=1479).

Overvåge serverne AD RMS for aktivitet, for eksempel ved at kontrollere de [anmodninger i rapporten systemtilstand](https://technet.microsoft.com/library/ee221012%28v=ws.10%29.aspx),  [ServiceRequest tabel](http://technet.microsoft.com/library/dd772686%28v=ws.10%29.aspx) eller [overvågning af brugeradgang til beskyttet indhold](http://social.technet.microsoft.com/wiki/contents/articles/3440.ad-rms-frequently-asked-questions-faq.aspx). Når du har bekræftet, at RMS-klienter ikke længere kommunikerer med disse servere og klienter, der bruger korrekt Azure RMS, kan du fjerne rollen AD RMS-server fra disse server. Hvis du bruger dedikerede servere, foretrækker du muligvis advarende trin af første lukke serverne i en periode for at sikre, at der er ingen rapporterede problemer, der muligvis kræver genstart af disse servere for at sikre kontinuitet i tjenesten, mens du undersøger hvorfor klienter ikke bruger Azure RMS.

Efter nedlukning AD RMS-servere, vil du få mulighed for at gennemse dine skabeloner i Azure Management Portal og konsolidere dem, så brugere har færre til at vælge mellem, konfigurere dem igen eller tilføje nye skabeloner. Dette ville også være en god ide at udgive standardskabelonerne. Yderligere oplysninger finder du under [Konfiguration af brugerdefinerede skabeloner til Azure rettighedsstyring](../Topic/Configuring_Custom_Templates_for_Azure_Rights_Management.md).

### <a name="BKMK_Step9Migration"></a>Trin 9. Nøglen Azure RMS lejer nøglen igen
Dette trin er obligatorisk, når overførslen er fuldført, hvis installationen af AD RMS brugte RMS kryptografiske tilstand 1, fordi at skrive opretter en ny nøgle til lejer, bruger RMS kryptografiske tilstand 2. Brug af Azure RMS med kryptografisk tilstand 1 understøttes kun under overflytningen.

Dette trin er valgfrit, men anbefales, når overførslen er fuldført, selvom du kørte i RMS kryptografiske tilstand 2, fordi det bidrager til at sikre Azure RMS lejer nøglen fra potentielle sikkerhedsbrister til AD RMS-tasten. Når du igen nøglen Azure RMS lejer nøglen (også kendt som "rullende din nøgle"), der oprettes en ny nøgle, og nøglen oprindelige arkiveres. Men da flytter fra én nøgle til en anden der ikke sker straks, men over et par uger, ikke vente til du har mistanke om brud på din oprindelige nøgle men nøgle RMS lejer nøglen igen, så snart overførslen er fuldført.

Til nøglen igen Azure RMS lejer nøglen:

-   Hvis din RMS lejer nøgle styres af Microsoft: Ringe til Microsoft Customer Support Services (CSS) og bevise, at du er lejer RMS-administratoren.

-   Hvis din RMS lejer nøgle styres af dig (BYOK): Gentag fremgangsmåden for at oprette og oprette en ny nøgle, via internettet eller personligt BYOK.

Finde flere oplysninger om administration af din RMS lejer nøgle [Operationer for Azure Rights Management lejer nøglen](../Topic/Operations_for_Your_Azure_Rights_Management_Tenant_Key.md).

## Se også
[Konfiguration af Azure rettighedsstyring](../Topic/Configuring_Azure_Rights_Management.md)

