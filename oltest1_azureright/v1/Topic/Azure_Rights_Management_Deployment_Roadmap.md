---
description: na
keywords: na
title: Azure Rights Management Deployment Roadmap
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 086600c2-c5d8-47ec-a4c0-c782e1797486
---
# K&#248;replan for Azure Rights Management installation
Brug følgende trin til at forberede, implementere og administrere Azure Rights Management (Azure RMS) for din organisation.

Men hvis du bare vil prøve Azure RMS hurtigt for dig selv, snarere end rulle ud i et produktionsmiljø, se [Hurtig Start selvstudiet til Azure rettighedsstyring](../Topic/Quick_Start_Tutorial_for_Azure_Rights_Management.md).

> [!IMPORTANT]
> Før du udføre følgende trin, skal du kontrollere, at du har gennemgået [Krav til Azure rettighedsstyring](../Topic/Requirements_for_Azure_Rights_Management.md).

## Trin 1: Bekræft, at du har et abonnement, der omfatter Azure Rights Management
Der er mere end én type abonnement, der omfatter [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)]. Se den [Sky-abonnementer, der understøtter Azure RMS](../Topic/Requirements_for_Azure_Rights_Management.md#BKMK_SupportedSubscriptions) afsnit i den [Krav til Azure rettighedsstyring](../Topic/Requirements_for_Azure_Rights_Management.md) emne, og Kontroller, at dit abonnement omfatter den funktionalitet, du vil bruge i organisationen ved at referere til tabellen i [tilbud på sammenligning af Rights Management Services (RMS)](https://technet.microsoft.com/dn858608).

## Trin 2: Forbered din lejer konto for at bruge Rights Management
Før du begynder at bruge [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)], skal følgende fremstilling:

1.  Kontroller, at din Azure eller Office 365 lejer indeholder brugerkonti og grupper, der skal bruges ved Azure RMS til at godkende brugere fra din organisation. Hvis det er nødvendigt, oprette disse konti og grupper, eller synkronisere dem fra din lokale mappe. Yderligere oplysninger finder du under [Forberedelse til Azure rettighedsstyring](../Topic/Preparing_for_Azure_Rights_Management.md).

2.  Beslut, om du vil Microsoft til at administrere din lejer nøgle (standard), eller oprette og administrere din nøgle lejer selv (kendt som sætter din egen nøgle eller BYOK). Bemærk, at der i øjeblikket kan du ikke bruge BYOK Hvis du bruger Exchange Online. Yderligere oplysninger finder du under [Planlægning og implementering af Azure Rights Management lejer nøglen](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md).

3.  Installere Windows PowerShell-modul til [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] på mindst en computer med internetadgang. Du kan udføre dette trin nu eller senere. Yderligere oplysninger finder du under [Installation af Windows PowerShell til Azure rettighedsstyring](../Topic/Installing_Windows_PowerShell_for_Azure_Rights_Management.md).

4.  Hvis du bruger i øjeblikket på stedet Rights Management services: Udføre en overførsel for at flytte de nøgler, skabeloner og URL-adresser til skyen. Yderligere oplysninger finder du under [Overflytning fra AD RMS Azure Rights Management](../Topic/Migrating_from_AD_RMS_to_Azure_Rights_Management.md).

5.  Aktiver Rights Management, så du kan begynde at bruge tjenesten. Hvis en faseopdelt installation er påkrævet, kan du konfigurere brugerdefinerede onboarding af kontrolelementer for at begrænse brugen til bestemte brugere. Yderligere oplysninger finder du under [Aktivering af Azure rettighedsstyring](../Topic/Activating_Azure_Rights_Management.md).

Overvej eventuelt konfigurere følgende:

-   Brugerdefinerede skabeloner, hvis standard rettigheder politikskabeloner, ikke er tilstrækkelige til din organisation. Du kan udføre dette trin nu eller senere. Yderligere oplysninger finder du under [Konfiguration af brugerdefinerede skabeloner til Azure rettighedsstyring](../Topic/Configuring_Custom_Templates_for_Azure_Rights_Management.md).

-   Brug logføring, så du kan overvåge, hvordan din organisation bruger Rights Management. Du kan udføre dette trin nu eller senere. Yderligere oplysninger finder du under [Logføring og analyse af brugen af Azure Rights Management](../Topic/Logging_and_Analyzing_Azure_Rights_Management_Usage.md).

## Trin 3: Konfigurere dine programmer og tjenester til Rights Management
Konfiguration af programmerne kan omfatte installere rettighedsstyring Deling af programmet og aktivere understøttelse af oplysninger rights management (IRM)-funktioner i SharePoint Online- eller Exchange Online. Yderligere oplysninger finder du under [Konfiguration af programmer for Azure rettighedsstyring](../Topic/Configuring_Applications_for_Azure_Rights_Management.md).

Hvis du har eksisterende IT-tjenester, der skal kontrollere de filer, der kan beskytte Azure RMS – som hukommelsesfejl forebyggelse (DLP) dataløsninger indhold kryptering gateways (CEG) og anti-malware-produkter – konfigureres tjenestekonti skal Superbrugere for Azure RMS. Yderligere oplysninger finder du under [Konfiguration af Superbrugere til Azure Rights Management og Discovery Services eller genoprettelse af Data](../Topic/Configuring_Super_Users_for_Azure_Rights_Management_and_Discovery_Services_or_Data_Recovery.md).

Hvis du har lokale tjenester, som du vil bruge med Azure Rights Management, installere og konfigurere forbindelsen Rights Management. Yderligere oplysninger finder du under [Installation af Azure Rights Management-stik](../Topic/Deploying_the_Azure_Rights_Management_Connector.md).

## Trin 4: Udgive og forbruge rettighedsbeskyttede indhold
Du er nu klar til at udgive og forbruge beskyttet indhold og logge, hvor dit firma bruger Rights Management. Yderligere oplysninger finder du under [Ved hjælp af Azure rettighedsstyring](../Topic/Using_Azure_Rights_Management.md).

## Trin 5: Administrere Rights Management til din lejer konto efter behov
Når du begynder at bruge [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)], du kan finde den [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] modul til Windows PowerShell bruges til at hjælpe script eller automatisere administrative ændringer. Yderligere oplysninger finder du under [Administration af Azure rettighedsstyring ved hjælp af Windows PowerShell](../Topic/Administering_Azure_Rights_Management_by_Using_Windows_PowerShell.md).

## Se også
[Konfiguration af Azure rettighedsstyring](../Topic/Configuring_Azure_Rights_Management.md)

