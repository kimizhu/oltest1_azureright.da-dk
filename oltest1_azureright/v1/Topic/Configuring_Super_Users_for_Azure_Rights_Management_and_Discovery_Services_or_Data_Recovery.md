---
description: na
keywords: na
title: Configuring Super Users for Azure Rights Management and Discovery Services or Data Recovery
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: acb4c00b-d3a9-4d74-94fe-91eeb481f7e3
---
# Konfiguration af Superbrugere til Azure Rights Management og Discovery Services eller genoprettelse af Data
Funktionen superbruger af Microsoft [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] (Azure RMS) sikrer, at autoriserede personer og servicer kan altid læse og inspicere de data, der beskytter Azure RMS for organisationen. Og om nødvendigt fjerne beskyttelsen eller ændre den beskyttelse, som tidligere blev anvendt. En superbruger har altid fuld ejerrettigheder til alle brug licenser, der er ydet af organisationens RMS lejer. Denne mulighed kaldes undertiden "Kognitiv over data" og er et afgørende element i vedligeholdelsen styringen af organisationens data. For eksempel vil du bruge denne funktion til en af følgende situationer:

-   En medarbejder forlader virksomheden, og du skal læse de filer, de beskyttet.

-   IT-administratoren skal fjerne den aktuelle politik for beskyttelse, der er konfigureret til filer og anvende en ny politik for beskyttelse.

-   Exchange Server skal indekset postkasser til søgehandlinger.

-   Du har eksisterende IT-tjenester for data tab forebyggelse (DLP) løsninger, kryptering af indhold gateways (CEG) og anti-malware-produkter, der skal til at kontrollere filer, som allerede er beskyttet.

-   Du skal masse dekryptere filer til overvågning, juridiske eller andre årsager til overholdelse.

Superbruger-funktion er ikke aktiveret som standard, og ingen brugere er tildelt denne rolle. Det er aktiveret for dig automatisk, hvis du konfigurerer forbindelsen Rights Management til Exchange, og det er ikke påkrævet for almindelige tjenester, der kører Exchange Online, SharePoint Online eller SharePoint Server.

Hvis du skal manuelt aktivere funktionen superbruger, kan du bruge Windows PowerShell-cmdlet [Aktiver AadrmSuperUserFeature](https://msdn.microsoft.com/library/azure/dn629400.aspx), og derefter tildele brugere (eller -tjenestekonti) efter behov ved hjælp af den [Tilføj AadrmSuperUser](https://msdn.microsoft.com/library/azure/dn629411.aspx) cmdlet. Du kan have en eller flere Superbrugere for organisationen, men du skal føje individuelle brugere; grupper understøttes ikke.

> [!NOTE]
> Hvis du endnu ikke har installeret Windows PowerShell-modul til [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)], se [Installation af Windows PowerShell til Azure rettighedsstyring](../Topic/Installing_Windows_PowerShell_for_Azure_Rights_Management.md).

Sikkerhed bedste fremgangsmåder for superbruger-funktion:

-   Begrænse og overvåge de administratorer, der er tildelt en global administrator for din Office 365 eller Azure RMS lejer, eller som er tildelt rollen GlobalAdministrator ved hjælp af den [Tilføj AadrmRoleBasedAdministrator](https://msdn.microsoft.com/library/azure/dn629417.aspx) cmdlet. Disse brugere kan aktivere funktionen superbruger og tildele brugere (og sig selv) som Superbrugere og eventuelt dekryptere alle filer, der beskytter din organisation.

-   Du kan se, hvilke brugere og tjenestekonti er tildelt som superbrugere ved at bruge den [cmdlet Get-AadrmSuperUser](https://msdn.microsoft.com/library/azure/dn629408.aspx).  Ligesom alle handlinger for administration, aktivering eller deaktivering af funktionen super og tilføje eller fjerne super brugere er logget og kan overvåges ved hjælp af den [få AadrmAdminLog](https://msdn.microsoft.com/library/azure/dn629430.aspx) kommando. Når Superbrugere dekryptere filer, handlingen er logget og kan overvåges med [Besøgslogføringen](https://technet.microsoft.com/library/dn529121.aspx).

-   Hvis du ikke behøver superbruger-funktion for almindelige tjenester, aktivere funktionen, når du har brug for det, og deaktivere den igen ved hjælp af den [Deaktiver AadrmSuperUserFeature](https://msdn.microsoft.com/library/azure/dn629428.aspx) cmdlet.

Følgende logfil ekstrakten viser nogle eksempel fra ved hjælp af Get-AadrmAdminLog-cmdlet. I dette eksempel bekræfter administratoren af Contoso, Ltd, superbruger-funktion er deaktiveret, tilføjer Richard Simone som superbruger, kontrollerer, at Richard er konfigureret til Azure RMS kun super brugeren og derefter aktiverer funktionen superbruger, så Richard nu kan dekryptere nogle filer, der er beskyttet af en medarbejder, der nu har forladt virksomheden.

`2015-08-01T18:58:20	admin@contoso.com	GetSuperUserFeatureState	Passed	Disabled`
`2015-08-01T18:59:44	admin@contoso.com	AddSuperUser -id rsimone@contoso.com	Passed	True`
`2015-08-01T19:00:51	admin@contoso.com	GetSuperUser	Passed	rsimone@contoso.com`
`2015-08-01T19:01:45	admin@contoso.com	SetSuperUserFeatureState -state Enabled	Passed	True`

## <a name="BKMK_RMSProtectionModule"></a>Indstillinger for superbrugere
Ofte nogen, der er tildelt en superbruger for [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] skal fjerne beskyttelsen fra flere filer på flere forskellige steder. Det er muligt at gøre det manuelt, men det er mere effektiv (og ofte mere pålidelig) til dette script. Hertil, [hente værktøjet RMS beskyttelse](http://www.microsoft.com/en-us/download/details.aspx?id=47256). Brug derefter de  [Fjern RMSFile](https://msdn.microsoft.com/library/azure/mt433200.aspx) cmdlet, og [Beskyt RMSFile](https://msdn.microsoft.com/library/azure/mt433201.aspx)   cmdlet efter behov.

> [!IMPORTANT]
> Fjern filer for genoprettelseshandlinger, den aktuelle version af værktøjet understøtter ikke brugergodkendelse for Azure RMS, men beskyttelse af RMS-værktøj er designet til Superbrugere til masse. Indtil problemet er løst, skal du bruge en principal tjenestekonto godkendes af Azure RMS, før du kan fjerne beskyttelsen fra filer.  Finde flere oplysninger og instruktioner, [about_RMSProtection_AzureRMS](https://msdn.microsoft.com/library/azure/mt433202.aspx).

Du kan finde flere oplysninger om disse cmdlets, i [-cmdletter RMS-beskyttelse](https://msdn.microsoft.com/library/azure/mt433195.aspx).

> [!NOTE]
> RMSProtection Windows PowerShell-modul, der følger med værktøjet RMS-beskyttelse er forskellig fra og supplerer vigtigste [Windows PowerShell-modul til Azure Rights Management](https://technet.microsoft.com/library/jj585027.aspx). Det understøtter både Azure RMS og AD RMS.

## Se også
[Konfiguration af Azure rettighedsstyring](../Topic/Configuring_Azure_Rights_Management.md)

