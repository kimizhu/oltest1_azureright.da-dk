---
description: na
keywords: na
title: Requirements for Azure Rights Management
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: dc78321d-d759-4653-8818-80da74b6cdeb
---
# Krav til Azure rettighedsstyring
Du skal installere Microsoft Azure Rights Management (Azure RMS) i din organisation, skal du sørge for, at følgende forudsætninger. Du kan derefter bruge den [Køreplan for Azure Rights Management installation](../Topic/Azure_Rights_Management_Deployment_Roadmap.md) at installere Rights Management til din organisation.

|Kravet om|Yderligere oplysninger|
|-------------|--------------------------|
|En sky-abonnement på RMS|Organisationen skal have en sky-abonnement, der understøtter RMS.<br /><br />Licensering oplysninger finder du i [Sky-abonnementer, der understøtter Azure RMS](../Topic/Requirements_for_Azure_Rights_Management.md#BKMK_SupportedSubscriptions) afsnit i dette emne.|
|Azure AD directory|Organisationen skal have en Azure AD directory understøtter brugergodkendelse for RMS. Hvis du vil bruge dine brugerkonti fra din lokale mappe (AD DS), skal du desuden også konfigurere directory integration.<br /><br />Godkendelse i flere niveauer (MFA) understøttes med Azure RMS, når du har den nødvendige klientsoftware og korrekt konfigureret MFA understøttende infrastruktur.<br /><br />Yderligere oplysninger finder du i [Azure AD directory](../Topic/Requirements_for_Azure_Rights_Management.md#BKMK_AzureADTenant) afsnit i dette emne.|
|Klientenheder|Brugere skal have en klientenheder (computer eller mobil enhed), der kører et operativsystem, der understøtter RMS.<br /><br />Yderligere oplysninger finder du i [Klientenheder, der understøtter Azure RMS](../Topic/Requirements_for_Azure_Rights_Management.md#BKMK_SupportedDevices) afsnit i dette emne.|
|Programmer|Brugere skal køre programmer, der understøtter RMS.<br /><br />Yderligere oplysninger finder du i [Programmer, der understøtter Azure RMS](../Topic/Requirements_for_Azure_Rights_Management.md#BKMK_SupportedApplications) afsnit i dette emne.|
|Infrastruktur, der understøtter tilslutning til internettet og afhængige cloud-tjenester|Hvis du har en firewall eller lignende mellemliggende netværksenheder, der skal konfigureres til at tillade bestemte forbindelser finder du i [Office 356 URL- og IP-adresseområder](https://support.office.com/en-US/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2).<br /><br />Listen over URL-adresser og IP-adresser i den **Office 356 portal og identitet** afsnit gælder for Office 365-portalen og Azure Active Directory-ressourcer på Azure Rights Management. Du kan bruge vejledningen i denne artikel til at holde opdateret med ændringer til disse oplysninger ved at abonnere på en RSS-kilde.<br /><br />Ud over oplysningerne i Office artikel, der er specifikke for Azure RMS:<br /><br />-   Afslut ikke TLS-client-service-forbindelse (for eksempel gøre pakkeniveau inspektion). Herved brydes fastgørelse, at RMS-klienter bruger med Microsoft-styrede CAs til at sikre deres kommunikation med Azure RMS certifikatet.<br />-   Brug ikke en web proxy-konfiguration, der godkender på vegne af en bruger.|

Hvis du vil bruge Azure RMS med lokale servere, understøttes følgende produkter:

-   Exchange Server

-   SharePoint Server

-   Windows Server filservere, der understøtter fil klassificering infrastruktur

Finde oplysninger om krav til yderligere Azure RMS til dette scenario, den [Lokale servere, der understøtter Azure RMS](../Topic/Requirements_for_Azure_Rights_Management.md#BKMK_SupportedServers) afsnit i dette emne.

> [!IMPORTANT]
> I følgende installationsscenario understøttes ikke:
> 
> -   Kører AD RMS og Azure RMS side om side i den samme organisation, undtagen under overflytningen, som beskrevet i [Overflytning fra AD RMS Azure Rights Management](../Topic/Migrating_from_AD_RMS_to_Azure_Rights_Management.md).
> 
> Der er en understøttet overflytningssti [fra AD RMS på Azure RMS](http://technet.microsoft.com/library/Dn858447.aspx), og fra [Azure RMS til AD RMS](http://msdn.microsoft.com/library/azure/dn629429.aspx). Hvis du skal installere RMS Azure og derefter beslutter, at du ikke længere vil bruge denne cloud-tjeneste, finder du i [Nedlukning og deaktivere Azure rettighedsstyring](../Topic/Decommissioning_and_Deactivating_Azure_Rights_Management.md).

Brug de følgende afsnit for at lære mere om Azure RMS-krav.

## <a name="BKMK_SupportedSubscriptions"></a>Sky-abonnementer, der understøtter Azure RMS
Hvis du vil bruge Azure RMS, skal organisationen have mindst én af følgende abonnementer med et tilstrækkeligt antal licenser til brugere og tjenester, der beskytter filer og e-mail-meddelelser. Hvis du har en tjeneste, der anvendes til beskyttelse af brugerne (ejerne af de filer eller e-mails), kræver disse brugere en af disse licenser. Brugere, der kun vil forbruge (for eksempel, læse og redigere) dette beskyttede data behøver ikke en licens.

-   Office 365

-   Azure Rights Management Premium (tidligere Azure RMS enkeltstående)

-   Enterprise Mobility-pakke

-   RMS til enkeltpersoner

Brug de følgende afsnit for at få flere oplysninger og indstillinger for tilmelding.

Finde en licensudstedende sammenligning af Azure RMS-funktioner til betalte abonnementer, [tilbud på sammenligning af Rights Management Services (RMS)](http://technet.microsoft.com/dn858608).

### Office 365-abonnement
[Gratis 30-dages prøveversion: Enterprise-E3](http://go.microsoft.com/fwlink/p/?LinkID=403802)

Dette abonnement er beregnet til organisationer, der ønsker at bruge Office online-tjenester og deres funktion, Information Rights Management, som bruger Azure RMS. Dog inkluderer ikke alle Office 365-abonnementer Azure RMS.

|Licensering|Office 365 Business Essentials|Office 365 Business Premium|Office 365 Enterprise E1<br /><br />Office 365 uddannelse A1|Office 365 Enterprise E3<br /><br />Office 365 uddannelse A3<br /><br />Office 365 regering G3|Office 365 Enterprise E4<br /><br />Office 365 uddannelse A4<br /><br />Office 365 regering G4|Office 365 Enterprise K1|SharePoint-Plan 1<br />SharePoint Plan 2|Exchange Online Plan 1<br />Exchange Online Plan 2|
|---------------|----------------------------------|-------------------------------|--------------------------------------------------------|----------------------------------------------------------------------------------|----------------------------------------------------------------------------------|----------------------------|----------------------------------------|--------------------------------------------------|
|Beskyttelse af oplysninger rettigheder (IRM)|Nej|Nej|Nej|Ja|Ja|Nej|Nej|Nej|

### Azure Rights Management Premium-abonnementet
[Gratis 30-dages prøveversion](https://portal.microsoftonline.com/Signup/MainSignUp15.aspx?&amp;OfferId=A43415D3-404C-4df3-B31B-AAD28118A778&amp;dl=RIGHTSMANAGEMENT&amp;ali=1)

Dette abonnement var tidligere kendt som Azure RMS separat, og det er beregnet til organisationer, der ønsker at bruge Azure RMS, men ikke har abonnement, der omfatter Azure RMS. For eksempel, hvis du har et abonnement til Office 365 Business Essentials eller Office 365 Enterprise E1, disse abonnementer indeholder ikke Azure RMS (se tabellen i det foregående afsnit). Azure RMS kan, du købe et abonnement til Azure Rights Management Premium (eller købe et andet abonnement, som Office 365 Enterprise E4, der indeholder Azure RMS).

Yderligere oplysninger finder du i [Microsoft Azure Rights Management](http://products.office.com/business/microsoft-azure-rights-management).

Dette abonnement tilbyder også en prøveperiode for dig at prøve Azure RMS til 25 brugere uden merpris. Hvis abonnementet udløber, før du køber et abonnement til udskiftning, kan du se i afsnittet "Hvad sker der Når prøveabonnementet udløber?"

|Licensering|Office 365 Business Essentials|Office 365 Business Premium|Office 365 Enterprise E1<br /><br />Office 365 uddannelse A1|Office 365 Enterprise E3<br /><br />Office 365 uddannelse A3<br /><br />Office 365 regering G3|Office 365 Enterprise E4<br /><br />Office 365 uddannelse A4<br /><br />Office 365 regering G4|Office 365 Enterprise K1|SharePoint-Plan 1<br />SharePoint Plan 2|Exchange Online Plan 1<br />Exchange Online Plan 2|
|---------------|----------------------------------|-------------------------------|--------------------------------------------------------|----------------------------------------------------------------------------------|----------------------------------------------------------------------------------|----------------------------|----------------------------------------|--------------------------------------------------|
|Beskyttelse af oplysninger rettigheder (IRM)|Ja|Yes <sup>1</sup>|Ja|Ja|Ja|Ja|Ja|Ja|
<sup>1</sup> Business præmie, er der nogle klient begrænsninger: Du kan beskytte indhold og forbruger beskyttet indhold med RMS ved hjælp af Outlook Web App og RMS deling app. Du kan bruge beskyttet indhold ved hjælp af alle andre Office-programmer, som indeholder Office Online og klientprogrammerne til Office 365 Business Premium.

#### <a name="BKMK_TrialExpiryBehavior"></a>Hvad sker der, når prøveabonnementet udløber?
Hvis dit prøveabonnement udløber, vil du miste adgang til indhold, som er beskyttet ved hjælp af dit prøveabonnement til Azure RMS. Men hvis du derefter køber et abonnement, der understøtter Azure RMS, gendannes access automatisk.

En undtagelse til at miste adgang efter udløbet er Hvis organisationen har brugt Azure RMS med RMS enkeltpersoner abonnement før du fik prøveabonnementet. Derefter adgang til beskyttet indhold forbliver tidligere, selvom prøveabonnementet udløber.

### Enterprise Mobility Suite-abonnement
[Gratis 30-dages prøveversion](http://go.microsoft.com/fwlink/?LinkId=615385)

Dette abonnement er beregnet til organisationer, der ønsker at bruge en kombination af Azure Active Directory Premium, Windows Intune og Azure Rights Management. Yderligere oplysninger finder du på [Oversigt over Microsoft Enterprise Mobility](http://go.microsoft.com/fwlink/?LinkId=615386).

|Licensering|Office 365 Business Essentials|Office 365 Business Premium|Office 365 Enterprise E1<br /><br />Office 365 uddannelse A1|Office 365 Enterprise E3<br /><br />Office 365 uddannelse A3<br /><br />Office 365 regering G3|Office 365 Enterprise E4<br /><br />Office 365 uddannelse A4<br /><br />Office 365 regering G4|Office 365 Enterprise K1|SharePoint-Plan 1<br />SharePoint Plan 2|Exchange Online Plan 1<br />Exchange Online Plan 2|
|---------------|----------------------------------|-------------------------------|--------------------------------------------------------|----------------------------------------------------------------------------------|----------------------------------------------------------------------------------|----------------------------|----------------------------------------|--------------------------------------------------|
|Beskyttelse af oplysninger rettigheder (IRM)|Ja|Yes <sup>1</sup>|Ja|Ja|Ja|Ja|Ja|Ja|
<sup>1</sup> Business præmie, er der nogle klient begrænsninger: Du kan beskytte indhold og forbruger beskyttet indhold med RMS ved hjælp af Outlook Web App og RMS deling app. Du kan bruge beskyttet indhold ved hjælp af alle andre Office-programmer, som indeholder Office Online og klientprogrammerne til Office 365 Business Premium.

### RMS til enkeltpersoner abonnement
Dette abonnement er udviklet til personer i en organisation, der endnu ikke er implementeret, Azure RMS eller AD RMS. Det giver mulighed for, at disse personer kan læse indholdet, der er beskyttet af en organisation, der bruger Azure RMS, og de kan også beskytte deres eget indhold.

Yderligere oplysninger finder du under [RMS for enkeltpersoner og Azure rettighedsstyring](../Topic/RMS_for_Individuals_and_Azure_Rights_Management.md).

## <a name="BKMK_AzureADTenant"></a>Azure AD directory
Du skal have en Azure AD directory bruge Azure RMS. Du kan bruge din organisation konto for denne mappe til at logge på Azure Management Portal, for eksempel kan du konfigurere og Administrer skabeloner til Rights Management.

Hvis du ikke har en Azure abonnement for din organisation, kan du få en ved at tilmelde dig et gratis prøveabonnement.: Gå til den [Azure få startet](https://account.windowsazure.com/organization) side, og følg vejledningen.

Yderligere oplysninger finder du følgende ressourcer i dokumentationen til Azure Active Directory:

-   [Hvad er en Azure AD mappe?](http://msdn.microsoft.com/en-us/library/185da266-58a9-43e6-9c66-2c8f702545c6)

-   [Hvordan Azure abonnementer, der er knyttet til Azure AD](http://msdn.microsoft.com/en-us/library/edf05c2e-944a-4da5-a330-dc9dc479f127)

Hvis du vil integrere adresselisten Azure AD med din lokale AD skove, se [katalogintegration](http://msdn.microsoft.com/en-us/library/bf82bdff-2467-403b-8c1a-0e9eebcf31e8).

> [!NOTE]
> Hvis du har mobile enheder eller Mac-computere, der godkender på stedet ved hjælp af AD FS eller en udbyder af tilsvarende godkendelse:
> 
> -   Du skal bruge AD FS på minimum serverversionen af **Windows Server 2012 R2**, eller en alternativ godkendelsesprovider, der understøtter protokollen OAuth 2.0.

### <a name="BKMK_MFA"></a>Godkendelse i flere niveauer (MFA) og Azure RMS
Hvis du vil bruge flere faktorer kræver godkendelse (MFA) med Azure RMS mindst én af følgende:

-   Office 2013 (minimum version):

    -   Hvis du har Office 2013, skal du også installere de [9 juni 2015, opdatering til Office 2013 (KB3054853)](https://support.microsoft.com/kb/3054853). Opdater, og hvordan moderne godkendelse giver Active Directory-godkendelse bibliotek ADAL-baserede log 2013 i Office, finder du yderligere oplysninger om dette [Office 2013 moderne godkendelse offentlige prøveversion annoncerede](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/)  på Office-bloggen.

-   Rights Management deling ansøgning om Windows:

    -   Du skal have installeret den mindste version af 1.0.1908.0, som kan bekræftes ved hjælp af Kontrolpanel, programmer og funktioner. Finde flere oplysninger om deling programmet  [Rettighedsstyring, deling af programmer til Windows](../Topic/Rights_Management_Sharing_Application_for_Windows.md).

-   Rights Management Deling af app til mobile enheder og Mac-computere:

    -   Sørg for, at du har den nyeste version installeret. Understøttelse af MFA gik i September 2015 udgivelsen af RMS deling app.

Konfigurer derefter MFA-løsning:

-   For Microsoft-styrede lejere (du har Azure Active Directory eller Office 365):

    -   Konfigurere Azure MFA for at gennemtvinge MFA for brugere. Yderligere oplysninger finder du [Introduktion til Azure godkendelse i flere niveauer i skyen](https://azure.microsoft.com/documentation/articles/multi-factor-authentication-get-started-cloud/) fra Azure dokumentation.

        Yderligere oplysninger om Azure MFA, se [Hvad er godkendelse i flere niveauer Azure?](https://azure.microsoft.com/documentation/articles/multi-factor-authentication/)

-   For organisationsnetværket lejere (der opereres federation servere på stedet):

    -   Konfigurere serverne federation for Azure Active Directory eller Office 365. For eksempel, hvis du bruger AD FS, se [konfigurere yderligere godkendelsesmetoder for AD FS](https://technet.microsoft.com/library/dn758113.aspx) på TechNet.

        Yderligere oplysninger om dette scenario, du  [det fungerer med Office 365 – identitet programmet nu strømlinet](https://blogs.office.com/2014/01/30/the-works-with-office-365-identity-program-now-streamlined/) på Office-bloggen.

## <a name="BKMK_SupportedDevices"></a>Klientenheder, der understøtter Azure RMS
Brug de følgende afsnit til at identificere, hvilke enheder understøtter Azure Rights Management (RMS) og hvilke RMS-funktioner, de understøtter:

-   [Computere](../Topic/Requirements_for_Azure_Rights_Management.md#BKMK_RMSSupportedComputers)

-   [Mobile enheder](../Topic/Requirements_for_Azure_Rights_Management.md#BKMK_RMSSupportedMobileDevices)

-   [Enheden Klientegenskaber](../Topic/Requirements_for_Azure_Rights_Management.md#BKMK_ClientCapabilities)

### <a name="BKMK_RMSSupportedComputers"></a>Computere
Følgende operativsystemer til computer understøtter rettighedsstyring Azure:

-   **Windows 7** (x 86, x 64)

-   **Windows 8** (x 86, x 64)

-   **Windows 8.1** (x 86, x 64)

-   **Windows 10** (x 86, x 64)

-   **Mac OS X**: Minimum version af Mac OS X 10.8 (Mountain Lion)

### <a name="BKMK_RMSSupportedMobileDevices"></a>Mobile enheder
Følgende operativsystemer til mobile enhed understøtter rettighedsstyring Azure:

-   **Windows Phone**: Windows Phone 8.1

-   **Android telefoner og tablets**: Minimum version af Android 4.0.3

-   **iPhone og iPad**: Minimum version af iOS 7.0

-   **Windows RT tablets**: Windows 8 RT, Windows 8.1 RT

### <a name="BKMK_ClientCapabilities"></a>Enheden Klientegenskaber
Ikke alle understøttede klientenheder understøtter i øjeblikket alle RMS-funktioner. Brug følgende tabel til at identificere, hvilke programmer understøtter RMS-funktioner og undtagelser.

Medmindre andet er angivet, gælder de understøttede funktioner for både Azure RMS og AD RMS. Derudover kræver understøttelse af AD RMS på iOS, Android, OS X og Windows Phone 8.1 [Active Directory Rights Management Services Mobile enhedsudvidelse](http://technet.microsoft.com/library/a69ead9d-7dd3-4b38-9830-4728e9757341).

Oplysninger om tabel-kolonner:

-   **Beskyttet PDF**: Filer, der har filtypenavnet .ppdf og, der automatisk oprettes, når du bruger RMS deling program til at dele Office-filer og PDF-filer via e-mail. RMS deling ansøgningen omfatter en læser til beskyttede PDF-filer. Tidligere, hvis du har oprettet PDF-filer, du er beskyttet ved hjælp af Azure RMS eller AD RMS, du kan fortsætte med at læse disse filer på Windows, iOS og Android-enheder ved hjælp af Foxit Reader og Nitro Pro.

-   **E-mail:** E-mail-klienter, der er angivet, kan beskytte den e-mail, der automatisk beskytter alle vedhæftede filer. I dette scenario kan klientens Eksempelfunktionen vise beskyttet indhold (meddelelse og vedhæftede filer) til autoriserede modtagere. Hvis en selve e-mail-meddelelsen ikke er beskyttet, men den vedhæftede fil er beskyttet, kan klientens Eksempelfunktionen kan ikke vise den beskyttede vedhæftede fil til autoriserede modtagere.

-   **Andre filtyper,**: Tekst og billede filer indeholder filer, der har filtypenavnet .txt, .XML-, .jpg, JPEG-.og. Disse filer ændrer deres filtypenavn, når de oprindeligt er beskyttet af RMS og bliver skrivebeskyttet. Filer, der ikke kan beskyttes oprindeligt har filtypenavnet .pfile, når de er generisk beskyttet af RMS. Yderligere oplysninger finder du på [beskyttelse – oprindelig og generiske](https://technet.microsoft.com/library/dn339003.aspx) og [understøttede filtyper og filtypenavne](https://technet.microsoft.com/library/dn339003.aspx) sektioner fra den [Rights Management deling program administratorvejledningen](http://technet.microsoft.com/library/dn339003%28v=ws.10%29.aspx).

|**Enhed operativsystemet.**|Word, Excel, PowerPoint|Beskyttet PDF-fil|Email|Andre filtyper|
|-------------------------------|---------------------------|---------------------|---------|------------------|
|**Windows**|Office 2010<br /><br />Office-2013<br /><br />Office Mobile apps (kun Azure RMS)<sup>1</sup><br /><br />Office Online<sup>2</sup>|Gaaiho Doc<br /><br />GigaTrust Desktop PDF-klient til Adobe<br /><br />Foxit Reader<br /><br />Nitro PDF-læser<br /><br />RMS deling app|Outlook 2010<br /><br />Outlook 2013<br /><br />Outlook Web App (OWA)<br /><br />Windows Mail<sup>3</sup>|RMS deling ansøgning om Windows: Tekst, billeder, pfile<br /><br />Siemens JT2Go: JT-filer (kun Windows-10)|
|**iOS**|Kontoret for iPad og iPhone<sup>4</sup><br /><br />Office Online<sup>2</sup><br /><br />TITUS dokumenter|Foxit Reader<br /><br />RMS deling app<sup>1</sup><br /><br />TITUS dokumenter|NitroDesk<br /><br />Outlook til iPad og iPhone<sup>3</sup><br /><br />OWA til iOS<br /><br />Sikker øer IQProtector<sup>1</sup><br /><br />TITUS Mail|RMS deling app<sup>1</sup>: Tekst, billeder, pfile<br /><br />TITUS Docs: Pfile|
|**Android**|GigaTrust App til Android<br /><br />Office Online<sup>2</sup>|GigaTrust App til Android<br /><br />Foxit Reader<br /><br />RMS deling app<sup>1</sup>|9Folders<br /><br />GigaTrust App til Android<br /><br />NitroDesk<br /><br />OWA til Android<sup>5</sup><br /><br />Samsung E-mail (S3 og senere)<br /><br />Sikker øer IQProtector<sup>1</sup><br /><br />TITUS klassificering til mobil|RMS deling app<sup>1</sup>: Tekst, billeder, pfile|
|**OS X**|Office 2011 (kun AD RMS)<br /><br />2016 i Office til Mac<br /><br />Office Online<sup>2</sup>|Foxit Reader<br /><br />RMS deling app<sup>1</sup>|Outlook 2011 (kun AD RMS)<br /><br />Outlook 2016 til Mac<br /><br />Outlook til Mac|RMS deling app<sup>1</sup>: Tekst, billeder, pfile|
|**Windows RT**|Office 2013 RT<br /><br />Office Online<sup>2</sup>|Understøttes ikke|Outlook 2013 RT<br /><br />Mail app til Windows<br /><br />Windows Mail<sup>3</sup>|Siemens JT2Go: JT-filer|
|**Windows Phone 8.1**|Office Mobile (kun AD RMS)|RMS deling app<sup>1</sup>|Outlook Mobile|RMS deling app<sup>1</sup>: Tekst, billeder, pfile|
|**BlackBerry 10**|Understøttes ikke|Understøttes ikke|BlackBerry e-mail<sup>3</sup>|Understøttes ikke|
<sup>1</sup> understøtter visning af beskyttet indhold.

<sup>2</sup> understøtter visning af beskyttet indhold i SharePoint Online, OneDrive til virksomheder og Outlook Web Access.

<sup>3</sup> bruger Exchange ActiveSync IRM, som skal være aktiveret af Exchange-administratoren. Brugere kan få vist, svar og svar alle beskyttede e-mails, men brugere ikke kan beskytte nye e-mail-meddelelser, selv.

<sup>4</sup> understøtter visning og redigering af beskyttede dokumenter. Yderligere oplysninger finder du i følgende indlæg på Office-bloggen: [Azure Rights Management support leveres til Office til iPad og iPhone](https://blogs.office.com/2015/07/22/azure-rights-management-support-comes-to-office-for-ipad-and-iphone-2/)

<sup>5</sup> yderligere oplysninger finder du under følgende indlæg på Office-bloggen: [OWA til Android er nu tilgængelig på udvalgte enheder](http://blogs.office.com/2014/06/11/owa-for-android-now-available-on-select-devices/)

> [!TIP]
> Du kan finde flere oplysninger om kommende RMS-understøttelse i Office til forskellige platforme, følgende indlæg fra Office-blog: [Office overalt, hvor som helst kryptering](http://blogs.office.com/2015/02/18/office-everywhere-encryption-everywhere/)

## <a name="BKMK_SupportedApplications"></a>Programmer, der understøtter Azure RMS
Følgende programmer har indbygget understøttelse af Azure RMS, hvilket betyder, at RMS tæt integreret i disse programmer ved hjælp af RMS APIs for at understøtte brugsrestriktioner. Disse programmer er også kendt som RMS-enlightened:

-   **Microsoft Office-programmer** (Word, Excel, PowerPoint og Outlook) fra følgende pakker kan beskytte indhold ved hjælp af Azure RMS:

    -   Office 365 ProPlus

    -   Office 365 Enterprise E3

    -   Office 365 Enterprise E4

    -   Office Professional Plus 2016

    -   Office Professional Plus 2013

    -   Office Professional Plus 2010

    Andre udgaver af Office (med undtagelse af Office 2007) kan forbruge beskyttet indhold.

    > [!NOTE]
    > Azure RMS med Office Professional Plus 2010 eller Office Professional 2010:
    > 
    > -   Kræver den Rights Management, deling af programmer til Windows
    > -   Ikke understøttet på Windows-10

-   **Den Rights Management, deling af programmer til Windows**

    Yderligere oplysninger om rettighedsstyring deling program til Windows, finder du i følgende ressourcer:

    -   [Rights Management deling program administratorvejledningen](http://technet.microsoft.com/library/dn339003.aspx)

    -   [Rights Management deling program bruger guide](http://technet.microsoft.com/library/dn339006.aspx)

-   **Den Rights Management, deling af programmer til mobile platforme**

    Yderligere oplysninger om rettighedsstyring deling ansøgning om mobile platforme, finder du i følgende ressourcer:

    -   Hent den relevante app ved hjælp af hyperlinkene på [Microsoft Rights Management side](http://go.microsoft.com/fwlink/?LinkId=303970)

    -   Hvis du administrerer mobile enheder ved hjælp af Microsoft Intune, kan du installere og konfigurere programmet på [iOS og Android-enheder, som en politik administreres app](https://technet.microsoft.com/library/dn878026.aspx).

    -   [Ofte stillede spørgsmål om Microsoft rettighedsstyring, deling af programmer til Mobile platforme](http://technet.microsoft.com/dn451248)

-   **Andre programmer, der understøtter den RMS APIs**:

    -   Branche-programmer, der er udviklet internt ved hjælp af RMS-SDK

    -   Programmer fra softwareleverandører, der er skrevet ved hjælp af RMS-SDK

    Yderligere oplysninger om SDK finder du på [Microsoft Rights Management SDK](http://msdn.microsoft.com/library/hh552972%28v=vs.85%29.aspx).

> [!IMPORTANT]
> Følgende programmer understøttes ikke i øjeblikket af Azure RMS:
> 
> -   Microsoft Office til Mac 2011
> -   Microsoft-OneDrive til virksomheder til SharePoint Server 2013
> -   XPS-fremviseren
> 
> Derudover har RMS deling program følgende begrænsninger:
> 
> -   Til Windows-computere: Kræver en minimal version af Windows 7 Service Pack 1

Yderligere oplysninger om, hvordan disse programmer understøtter Azure RMS, se [Hvordan programmer understøtter Azure rettighedsstyring](../Topic/How_Applications_Support_Azure_Rights_Management.md).

Du kan finde oplysninger om, hvordan du konfigurerer dem, i [Konfiguration af programmer for Azure rettighedsstyring](../Topic/Configuring_Applications_for_Azure_Rights_Management.md).

## <a name="BKMK_SupportedServers"></a>Lokale servere, der understøtter Azure RMS
Følgende lokale serverprodukter understøttes med Azure RMS, når du bruger Azure RMS-stik, der fungerer som en kommunikation grænseflade (relay) mellem lokale servere og Azure RMS. Denne konfiguration kræver desuden, at du konfigurerer katalogsynkronisering mellem Active Directory-områder og Azure Active Directory.

-   **Exchange Server**:

    -   Exchange Server 2013

    -   Exchange Server 2010

-   **Office SharePoint Server**:

    -   Office SharePoint Server 2013

    -   Office SharePoint Server 2010

-   **Fil servere, der kører Windows Server og bruge fil klassificering infrastruktur (FCI)**:

    -   Windows Server 2012 R2

    -   Windows Server 2012

    > [!NOTE]
    > Filservere, der kører Windows Server 2008 R2 har ikke en indbygget fil management opgavehandling at anvende RMS-beskyttelse, kan du ikke bruge RMS-forbindelsen til dette scenario. Du kan dog bruge fil klassificering infrastruktur og Azure RMS på disse systemer, hvis du konfigurerer en brugerdefineret fil management opgave for at køre en eksekverbar fil eller et script, der kan beskytte filerne ved hjælp af Azure RMS. For eksempel en Windows PowerShell-script, der benytter den [beskyttelse af RMS-cmdletter](https://msdn.microsoft.com/library/azure/mt433195.aspx).
    > 
    > Du kan også bruge disse cmdlets med servere, der kører en nyere versioner af Windows Server, med fordelen, at disse cmdlets kan beskytte alle filtyper. RMS-connector beskytter Office-filer. Du kan finde trinvise vejledninger i [RMS-beskyttelse med Windows Server fil klassificering infrastruktur &#40;FCI&#41;](../Topic/RMS_Protection_with_Windows_Server_File_Classification_Infrastructure__FCI_.md).

RMS-connector understøttes på Windows Server 2012 R2, Windows Server 2012 og Windows Server 2008 R2.

Yderligere oplysninger om, hvordan du konfigurerer RMS-tilslutning til disse lokale servere, se [Installation af Azure Rights Management-stik](../Topic/Deploying_the_Azure_Rights_Management_Connector.md).

## Se også
[Introduktion til Azure rettighedsstyring](../Topic/Getting_Started_with_Azure_Rights_Management.md)

