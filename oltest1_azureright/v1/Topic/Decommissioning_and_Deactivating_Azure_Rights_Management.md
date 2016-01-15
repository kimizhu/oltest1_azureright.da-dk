---
description: na
keywords: na
title: Decommissioning and Deactivating Azure Rights Management
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0b1c2064-0d01-45ae-a541-cebd7fd762ad
---
# Nedlukning og deaktivere Azure rettighedsstyring
Du har altid kontrol af, om din organisation beskytter indhold ved hjælp af [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] (Azure RMS), og hvis du beslutter du ikke længere ønsker at bruge denne løsning til beskyttelse af oplysninger, du har garanti for, at du ikke vil være låst ude af indhold, der tidligere var beskyttet. Hvis du ikke har brug for fortsat adgang til tidligere beskyttet indhold, blot at deaktivere tjenesten, og du kan lade dit abonnement på Azure Rights Management, udløber. For eksempel det er rimeligt, at når du har fuldført testen [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] før du implementerer den i et produktionsmiljø.

Men hvis du har installeret [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] i produktionen, skal du sikre, at du har en kopi af din nøgle til lejeradministration af Azure Rights Management, før du kan deaktivere tjenesten og gøre dette, før abonnementet udløber, da dette sikrer, at du kan bevare adgang til indhold, som er beskyttet af Azure Rights Management, når tjenesten er deaktiveret. Hvis du har brugt Medbring din egen nøgle løsning (BYOK) hvor du kan oprette og administrere din egen nøgle i en HSM, har du allerede Azure Rights Management lejer nøglen. Men hvis det blev styret af Microsoft (standard), se vejledningen for at eksportere din lejer nøgle i [Operationer for Azure Rights Management lejer nøglen](../Topic/Operations_for_Your_Azure_Rights_Management_Tenant_Key.md) emne.

> [!TIP]
> Selv når dit abonnement udløber, forbliver din lejer Azure Rights Management til forbruger indhold i en længere periode. Du vil dog ikke længere kunne eksportere din nøgle til lejeradministration.

Når du har din Azure Rights Management lejer nøgle, kan du installere Rights Management på lokaler (AD RMS) og importere din lejer nøgle som en publicerer tillidsdomænet (TPD). Du har følgende muligheder for nedlukning Azure Rights Management-installation:

|Hvis dette gælder for dig...|… Benyt følgende fremgangsmåde:|
|--------------------------------|-----------------------------------|
|Alle brugere skal fortsætte med at bruge Rights Management og bruge en lokal løsning i stedet for at bruge Azure RMS →|Brug af [sæt AadrmMigrationUrl](https://msdn.microsoft.com/library/azure/dn629429.aspx) -cmdlet til direkte eksisterende brugere til din lokale installation, når de indtager indhold, der er beskyttet efter ændringen. Brugere bruger automatisk AD RMS-installation til at forbruge det beskyttede indhold.<br /><br />For brugerne at forbruge indhold, som er beskyttet, før ændringen, omdirigere dine klienter til den lokale installation ved hjælp af den **LicensingRedirection** nøglen i registreringsdatabasen for 2016 Office eller Office 2013, som beskrevet i den [service discovery afsnit](https://technet.microsoft.com/library/jj159267%28v=ws.10%29.aspx) i RMS-klienten installation noter og **LicenseServerRedirection** registreringsdatabasenøglen til Office 2010, som beskrevet i [registreringsdatabaseindstillinger til Office](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx).|
|Du vil stoppe ved hjælp af teknologier til styring af helt →|Give en angiven administrator [super brugerrettigheder](https://technet.microsoft.com/library/mt147272.aspx) og give denne person den [værktøj til beskyttelse af RMS](http://www.microsoft.com/en-us/download/details.aspx?id=47256).<br /><br />Denne administrator kan derefter bruge værktøjet til bulk-dekryptere filer i mapper, der er beskyttet af Azure Rights Management, så filerne, der er tilbage til at blive beskyttet og derfor kan læses uden en Rights Management-teknologi som Azure RMS og AD RMS. Dette værktøj kan bruges med både Azure RMS og AD RMS, så du har mulighed for at dekryptere filer før, eller når du deaktiverer Azure RMS eller en kombination.|
|Er det ikke muligt at identificere alle de filer, der er beskyttet af Azure RMS eller alle brugere skal kunne læse automatisk alle beskyttede filer, der er gået glip af →|Installere en indstilling i registreringsdatabasen på alle klientcomputere ved hjælp af den **LicensingRedirection** nøglen i registreringsdatabasen for 2016 Office og Office-2013, som beskrevet i den [service discovery afsnit](https://technet.microsoft.com/library/jj159267%28v=ws.10%29.aspx) i RMS-klienten installation noter og **LicenseServerRedirection** registreringsdatabasenøglen til Office 2010, som beskrevet i [registreringsdatabaseindstillinger til Office](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx).<br /><br />Også installere en anden indstilling i registreringsdatabasen til at forhindre brugere i at beskytte nye filer ved at indstille **DisableCreation** til **1**, som beskrevet i [Office registreringsdatabaseindstillinger](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx).|
|Der skal kontrolleres, manuel genoprettelsestjenesten for alle filer, der blev mistet →|Bonussen udpeget brugere i en gruppe til genoprettelse af data [super brugerrettigheder](https://technet.microsoft.com/library/mt147272.aspx) og give dem den [værktøj til beskyttelse af RMS](http://www.microsoft.com/en-us/download/details.aspx?id=47256) så de kan fjerne beskyttelsen filer, når der anmodes om af standardbrugere.<br /><br />På alle computere, du installerer registreringsdatabaseindstillingen for at forhindre brugere i at beskytte nye filer ved at indstille **DisableCreation** til **1**, som beskrevet i [Office registreringsdatabaseindstillinger](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx).|
Yderligere oplysninger om procedurerne i denne tabel, kan du se i følgende ressourcer:

-   Finde oplysninger om AD RMS og deployment referencer, [Active Directory Rights Management Services-Overview](https://technet.microsoft.com/library/hh831364.aspx).

-   Vejledning til at importere din Azure RMS lejer nøgle som en TPD-fil finder du under [tilføje et Trusted Publishing domæne](https://technet.microsoft.com/library/cc771460.aspx).

-   For at installere Windows PowerShell-modul til Azure RMS, til at angive URL-migrering, se [Installation af Windows PowerShell til Azure rettighedsstyring](../Topic/Installing_Windows_PowerShell_for_Azure_Rights_Management.md).

Når du er klar til at deaktivere tjenesten Azure RMS for organisationen, kan du bruge følgende instruktioner.

## Deaktivere rettighedsstyring
Brug en af følgende fremgangsmåder til at deaktivere [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)].

> [!TIP]
> Du kan også bruge Windows PowerShell-cmdlet, [Deaktiver Aadrm](http://msdn.microsoft.com/library/windowsazure/dn629422.aspx), for at deaktivere [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)].

#### Deaktivere rettighedsstyring på Office 365 admin-Center

1.  [Logge på Office 365 med din konto til arbejdet eller skolen](https://portal.office.com/) der er administrator for din installation af Office 365.

2.  Hvis Office 365 admin center ikke automatisk vises, Vælg ikonet app Opgavestarter i øverst til venstre og vælge **Admin**. Den **Admin** side om side vises kun til Office 365-administratorer.

    > [!TIP]
    > Admin center Hjælp finder du under [om på Office 365 admin center - Admin Hjælp](https://support.office.com/article/About-the-Office-365-admin-center-Admin-Help-58537702-d421-4d02-8141-e128e3703547).

3.  I venstre rude kan du udvide **Indstillinger for**.

4.  Klik på **Rights Management**.

5.  På den **RIGHTS MANAGEMENT** skal du klikke på **Manage**.

6.  På den **rettighedsstyring** skal du klikke på **Deaktiver**.

7.  Når du bliver bedt om **vil du deaktivere rettighedsstyring?**, skal du klikke på **Deaktiver**.

Du kan nu se **Rights Management er ikke aktiveret** og mulighed for at aktivere.

#### Deaktivere rettighedsstyring fra Azure Portal

1.  Log på den [Azure Portal](http://go.microsoft.com/fwlink/p/?LinkID=275081).

2.  Klik på i venstre rude, **ACTIVE DIRECTORY**.

3.  Fra den **active directory** skal du klikke på **RIGHTS MANAGEMENT**.

4.  Vælg mappe til at administrere for [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)], skal du klikke på **Deaktiver**, og derefter bekræfte din handling.

Den **RIGHTS MANAGEMENT STATUS** skal nu vise **inaktiv** og **Deaktiver** erstattes af **Aktiver**.

## Se også
[Konfiguration af Azure rettighedsstyring](../Topic/Configuring_Azure_Rights_Management.md)

