---
description: na
keywords: na
title: Installing Windows PowerShell for Azure Rights Management
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0d665ed6-b1de-4d63-854a-bc57c1c49844
---
# Installation af Windows PowerShell til Azure rettighedsstyring
Brug følgende oplysninger til at hjælpe dig med at installere Windows PowerShell til Microsoft [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] (Azure RMS).

Du kan bruge dette modul til Windows PowerShell til at administrere [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] fra kommandolinjen ved hjælp af en computer, der har forbindelse til internettet og, der opfylder forudsætningerne, der er nævnt i næste afsnit. Windows PowerShell til [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] understøtter scripting til automatisering eller kan være nødvendig for avancerede konfigurationsscenarier. Yderligere oplysninger om administrationsopgaver og konfigurationer, der understøtter modulet, du [Administration af Azure rettighedsstyring ved hjælp af Windows PowerShell](../Topic/Administering_Azure_Rights_Management_by_Using_Windows_PowerShell.md).

## Forudsætninger
Denne tabel viser en liste over forudsætningerne for at installere og bruge Windows PowerShell til [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)].

|Kravet om|Yderligere oplysninger|
|-------------|--------------------------|
|En version af Windows, der understøtter den [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] Administrationsmodulet|Se listen over understøttede operativsystemer i den **systemkrav** del af den [overførselssiden for Azure Rights Management Administration Tool](http://go.microsoft.com/fwlink/?LinkId=257721).|
|Minimum version af Windows PowerShell: 2.0|Understøttelse af [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] Administrationsmodulet introduceres i Windows PowerShell 2.0.<br /><br />Som standard de fleste Windows-operativsystemer med mindst installere version 2.0 af Windows PowerShell. Hvis du vil installere Windows PowerShell 2.0, skal du se [installere Windows PowerShell 2.0](http://msdn.microsoft.com/library/ff637750.aspx). **Tip:** Du kan bekræfte versionen af Windows PowerShell, som du kører, ved at skrive **$PSVersionTable** i en Windows PowerShell-session.|
|Minimum version af Microsoft.NET Framework: 4.5 **Tip:** Denne version af Microsoft,.NET Framework-er inkluderet i de nyere operativsystemer, så du bør kun skal installere den manuelt, hvis klientoperativsystemet er mindre end Windows 8.0 eller server-operativsystemet er mindre end Windows Server 2012.|Hvis dette ikke allerede er installeret, kan du hente den [Microsoft,.NET Framework 4.5](http://www.microsoft.com/download/details.aspx?id=30653).<br /><br />Denne version af Microsoft.NET Framework, der kræves til nogle af klasserne, som de [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] Administrationsmodulet bruges.|
|Microsoft Online Services-In Assistant 7.0|Microsoft Online Services Log på-assistenten er påkrævet for [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] godkendelse.<br /><br />Yderligere oplysninger finder du i [Download Center: Microsoft Online Services assistenten for IT-fagfolk RTW](http://www.microsoft.com/en-us/download/details.aspx?id=41950).|

## Sådan installeres Administrationsmodulet Rights Management

1.  Gå til Microsoft Download Center og [hente Azure Rights Management Administration Tool](https://go.microsoft.com/fwlink/?LinkId=257721), som indeholder de [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] Administrationsmodulet til Windows PowerShell.

2.  Fra den lokale mappe, hvor du har hentet og gemt den [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] installer filen, skal du dobbeltklikke på den eksekverbare fil, du hentede til din platform (WindowsAzureADRightsManagementAdministration_x64 eller WindowsAzureADRightsManagementAdministration_x86.exe) for at starte Azure AD Rights Management Administration installationsguiden.

3.  Fuldfør guiden.

Windows PowerShell for [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] er nu installeret.

## Næste trin
Hvis du vil se, hvilke cmdlets, der er tilgængelige, skal du starte Windows PowerShell med de **Kør som administrator** indstilling, og Skriv følgende:

```
Get-Command -Module aadrm
```
Brug `the Get-Help <cmdlet_name>` kommando for at få hjælp til en bestemt cmdlet.

Yderligere oplysninger:

-   Komplet liste over tilgængelige cmdlets: [Azure Rights Management-cmdlet'er](https://msdn.microsoft.com/library/windowsazure/dn629398.aspx)

-   Liste over de vigtigste konfigurationsscenarier, der understøtter Windows PowerShell: [Administration af Azure rettighedsstyring ved hjælp af Windows PowerShell](../Topic/Administering_Azure_Rights_Management_by_Using_Windows_PowerShell.md)

Før du kan køre de kommandoer, der konfigurerer den [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] service, skal du oprette forbindelse til tjenesten ved hjælp af den [Connect-AadrmService](https://msdn.microsoft.com/library/windowsazure/dn629415.aspx) cmdlet. Når du er færdig med at køre konfigurationskommandoer, du vil afbryde forbindelsen til tjenesten ved hjælp af den [afbrydelse-AadrmService](https://msdn.microsoft.com/library/windowsazure/dn629416.aspx) cmdlet.

> [!NOTE]
> Hvis du endnu ikke har aktiveret [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)], du kan gøre dette, når du har oprettet forbindelse til tjenesten, ved hjælp af den [Aktiver Aadrm](https://msdn.microsoft.com/library/windowsazure/dn629412.aspx) cmdlet.

## Se også
[Administration af Azure rettighedsstyring ved hjælp af Windows PowerShell](../Topic/Administering_Azure_Rights_Management_by_Using_Windows_PowerShell.md)

