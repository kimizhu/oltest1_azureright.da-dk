---
description: na
keywords: na
title: Administering Azure Rights Management by Using Windows PowerShell
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a890e04a-4b70-41b5-8d5f-3c210a669faa
---
# Administration af Azure rettighedsstyring ved hj&#230;lp af Windows PowerShell
Selvom du kan aktivere Microsoft [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] (Azure RMS) ved hjælp af den [!INCLUDE[o365_2](../Token/o365_2_md.md)] admin center eller Azure portal, kan du også bruge Windows PowerShell-modul til [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] (AADRM) for at gøre dette.

Når du har aktiveret [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)], yderligere administration for tjenesten er muligvis ikke nødvendig. Men nogle scenarier, Avanceret konfiguration kan skal du bruge Windows PowerShell-modul til [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)]. I følgende tabel vises nogle af de avancerede konfigurationsscenarier, der bruger Windows PowerShell. Se en komplet liste over de tilgængelige cmdlet'er med flere oplysninger om hver enkelt [-cmdletter Azure Rights Management](http://msdn.microsoft.com/library/azure/dn629398.aspx).

> [!NOTE]
> Hvis du vil installere Windows PowerShell-modul til [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)], se [Installation af Windows PowerShell til Azure rettighedsstyring](../Topic/Installing_Windows_PowerShell_for_Azure_Rights_Management.md).

Der er også et supplerende modul til Windows PowerShell, **RMSProtection**, som understøtter både Azure RMS og AD RMS. Dette modul understøtter beskyttelse og fjerne beskyttelsen fra flere filer, så der for eksempel kan du bulk-beskytte alle filer i en mappe. Yderligere oplysninger finder du i [Indstillinger for superbrugere](../Topic/Configuring_Super_Users_for_Azure_Rights_Management_and_Discovery_Services_or_Data_Recovery.md#BKMK_RMSProtectionModule) afsnit i den [Konfiguration af Superbrugere til Azure Rights Management og Discovery Services eller genoprettelse af Data](../Topic/Configuring_Super_Users_for_Azure_Rights_Management_and_Discovery_Services_or_Data_Recovery.md) emne.

|Hvis du skal...|.. .use følgende cmdlets|
|-------------------|----------------------------|
|Overførsel fra lokale Rights Management (AD RMS eller Windows RMS) til [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)].|[Import af AadrmTpd](http://msdn.microsoft.com/library/azure/dn857523.aspx)|
|Oprette forbindelse til eller afbryde forbindelsen til den [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] tjeneste i din organisation.|[Tilslut AadrmService](http://msdn.microsoft.com/library/azure/dn629415.aspx)<br /><br />[Afbryder AadrmService](http://msdn.microsoft.com/library/azure/dn629416.aspx)|
|Oprette og administrere din egen lejer nøgle – Medbring din egen nøgle (BYOK)-scenario.|[Tilføj AadrmKey](http://msdn.microsoft.com/library/azure/dn629418.aspx)<br /><br />[Get-AadrmKeys](http://msdn.microsoft.com/library/azure/dn629420.aspx)|
|Aktivere eller deaktivere den [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] tjeneste i din organisation.|[Aktiver Aadrm](http://msdn.microsoft.com/library/azure/dn629412.aspx)<br /><br />[Deaktiver Aadrm](http://msdn.microsoft.com/library/azure/dn629422.aspx)|
|Deaktivere eller aktivere dokumentsporing websted for Azure Rights Management.|[Deaktiver AadrmDocumentTrackingFeature](https://msdn.microsoft.com/library/azure/mt548471.aspx)<br /><br />[Aktiver AadrmDocumentTrackingFeature](https://msdn.microsoft.com/library/azure/mt548469.aspx)<br /><br />[Get-AadrmDocumentTrackingFeature](https://msdn.microsoft.com/library/azure/mt548470.aspx)|
|Konfigurere onboarding af indstillinger for en faseopdelt installation af Azure Rights Management.|[Get-AadrmOnboardingControlPolicy](http://msdn.microsoft.com/library/azure/dn857522.aspx)<br /><br />[Sæt AadrmOnboardingControlPolicy](http://msdn.microsoft.com/library/azure/dn857521.aspx)|
|Opret og Administrer rettigheder politikskabeloner til din organisation.|[Tilføj AadrmTemplate](http://msdn.microsoft.com/library/azure/dn727075.aspx)<br /><br />[Eksport af AadrmTemplate](http://msdn.microsoft.com/library/azure/dn727078.aspx)<br /><br />[Get-AadrmTemplate](http://msdn.microsoft.com/library/azure/dn727079.aspx)<br /><br />[Get-AadrmTemplateProperty](http://msdn.microsoft.com/library/azure/dn727081.aspx)<br /><br />[Import af AadrmTemplate](http://msdn.microsoft.com/library/azure/dn727077.aspx)<br /><br />[Ny AadrmRightsDefinition](http://msdn.microsoft.com/library/azure/dn727080.aspx)<br /><br />[Fjern AadrmTemplate](http://msdn.microsoft.com/library/azure/dn727082.aspx)<br /><br />[Sæt AadrmTemplateProperty](http://msdn.microsoft.com/library/azure/dn727076.aspx)|
|Du kan konfigurere det maksimale antal dage, der kan få adgang til indhold, der beskytter din organisation uden en Internetforbindelse (Brug licens gyldighedsperioden).|[Get-AadrmMaxUseLicenseValidityTime](https://msdn.microsoft.com/library/azure/dn932062.aspx)<br /><br />[Sæt AadrmMaxUseLicenseValidityTime](https://msdn.microsoft.com/library/azure/dn932063.aspx)|
|Administrere funktionen superbruger af [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] for din organisation.|[Aktiver AadrmSuperUserFeature](http://msdn.microsoft.com/library/azure/dn629400.aspx)<br /><br />[Deaktiver AadrmSuperUserFeature](http://msdn.microsoft.com/library/azure/dn629428.aspx)<br /><br />[Tilføj AadrmSuperUser](http://msdn.microsoft.com/library/azure/dn629411.aspx)<br /><br />[Get-AadrmSuperUser](http://msdn.microsoft.com/library/azure/dn629408.aspx)<br /><br />[Fjern AadrmSuperUser](http://msdn.microsoft.com/library/azure/dn629405.aspx)|
|Administrere brugere og grupper der har tilladelse til at administrere den [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] tjeneste i din organisation.|[Tilføj AadrmRoleBasedAdministrator](http://msdn.microsoft.com/library/azure/dn629417.aspx)<br /><br />[Get-AadrmRoleBasedAdministrator](http://msdn.microsoft.com/library/azure/dn629407.aspx)<br /><br />[Fjern AadrmRoleBasedAdministrator](http://msdn.microsoft.com/library/azure/dn629424.aspx)|
|Få en log over [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] administrative opgaver for din organisation.|[Get-AadrmAdminLog](http://msdn.microsoft.com/library/azure/dn629430.aspx)|
|Log og analysere forbrug logføring for [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)].|[Aktiver AadrmUsageLogFeature](http://msdn.microsoft.com/library/azure/dn629421.aspx)<br /><br />[Get-AadrmUsageLog](http://msdn.microsoft.com/library/azure/dn629401.aspx)<br /><br />[Get-AadrmUsageLogFeature](http://msdn.microsoft.com/library/azure/dn629425.aspx)<br /><br />[Get-AadrmUsageLogLastCounterValue](http://msdn.microsoft.com/library/azure/dn629423.aspx)<br /><br />[Get-AadrmUsageLogStorageAccount](http://msdn.microsoft.com/library/azure/dn629419.aspx)<br /><br />[Sæt AadrmUsageLogStorageAccount](http://msdn.microsoft.com/library/azure/dn629426.aspx)<br /><br />[Deaktiver AadrmUsageLogFeature](http://msdn.microsoft.com/library/azure/dn629404.aspx)|
|Få vist aktuelt [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] tjenestekonfiguration for din organisation.|[Get-AadrmConfiguration](http://msdn.microsoft.com/library/azure/dn629410.aspx)|
|Overføre organisationen fra [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] til en lokal implementering af AD RMS.|[Sæt AadrmMigrationUrl](http://msdn.microsoft.com/library/azure/dn629429.aspx)<br /><br />[Get-AadrmMigrationUrl](http://msdn.microsoft.com/library/azure/dn629403.aspx)|

## Se også
[Azure rettighedsstyring](../Topic/Azure_Rights_Management.md)

