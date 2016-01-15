---
description: na
keywords: na
title: Preparing for Azure Rights Management
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: afbca2d6-32a7-4bda-8aaf-9f93f5da5abc
---
# Forberedelse til Azure rettighedsstyring
Når du har tilmeldt sig et abonnement til sky og etableret din virksomhed med en konto til [!INCLUDE[o365_1](../Token/o365_1_md.md)] eller Azure Active Directory, er du klar til at aktivere den [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] service.

Før du gør dette, kontrollere, at følgende er på plads:

-   Brugerkonti og grupper i skyen, som du opretter manuelt, eller, der automatisk oprettes og synkroniseres fra Active Directory-domæneservices (AD DS).

    Når du synkroniserer dine lokale brugerkonti og -grupper, skal ikke alle attributter, der synkroniseres. Du kan finde en liste over de attributter, der skal synkroniseres til Azure RMS i denne [Azure RMS afsnit](https://azure.microsoft.com/documentation/articles/active-directory-aadconnectsync-attributes-synchronized/) fra Azure Active Directory-dokumentationen. For at lette installation, anbefaler vi, at du bruger [Azure AD Connect](http://azure.microsoft.com/documentation/articles/active-directory-aadconnect/) til at oprette forbindelse til din lokale mapper med Azure Active Directory, men du kan bruge en hvilken som helst mappe synkroniseringsmetode, der opnår samme resultat.

-   E-mail-aktiverede grupperne i skyen, som du vil bruge sammen med Rights Management. Disse kan være indbyggede grupper eller manuelt oprettet grupper, der indeholder brugere, der bruger Rights Management.

    Hvis du har Exchange Online, kan du oprette og bruge e-mail-aktiverede grupperne ved hjælp af Exchange admin center. Hvis du har AD DS og synkroniserer til Azure AD, kan du oprette og bruge e-mail-aktiverede grupper, der enten sikkerhedsgrupper eller distributionsgrupper.

## Aktivere rettighedsstyring
Som standard [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] er deaktiveret, når du tilmelder dig din [!INCLUDE[o365_2](../Token/o365_2_md.md)] eller Azure AD konto. At aktivere [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] for organisationen, skal du aktivere tjenesten. Yderligere oplysninger finder du under [Aktivering af Azure rettighedsstyring](../Topic/Activating_Azure_Rights_Management.md).

## Se også
[Konfiguration af Azure rettighedsstyring](../Topic/Configuring_Azure_Rights_Management.md)

