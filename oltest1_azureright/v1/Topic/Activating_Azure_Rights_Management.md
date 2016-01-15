---
description: na
keywords: na
title: Activating Azure Rights Management
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f8707e01-b239-4d1a-a1ea-0d1cf9a8d214
---
# Aktivering af Azure rettighedsstyring
Når du aktiverer [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] (Azure RMS), organisationen kan begynde at beskytte vigtige data ved hjælp af programmer og tjenester, der understøtter denne løsning til beskyttelse af oplysninger. Administratorer kan også administrere og overvåge beskyttede filer og e-mails, der ejer virksomheden. Du skal aktivere [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] før du kan begynde at bruge oplysninger rights management (IRM)-funktioner i Office, SharePoint og Exchange og beskytte følsomme eller fortrolige filer.

Hvis du vil vide mere om Azure Rights Management, før du aktiverer tjenesten – for eksempel hvilke forretningsproblemer, det løser nogle typiske Brug tilfælde og hvordan det fungerer, se [Hvad er Azure Rights Management?](../Topic/What_is_Azure_Rights_Management_.md)

> [!IMPORTANT]
> Før du aktiverer [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)], skal du sørge for, at virksomheden har en serviceplan, der omfatter [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] services. Hvis ikke, skal du ikke aktivere Azure RMS.
> 
> Yderligere oplysninger finder du i [Sky-abonnementer, der understøtter Azure RMS](../Topic/Requirements_for_Azure_Rights_Management.md#BKMK_SupportedSubscriptions) afsnit i den [Krav til Azure rettighedsstyring](../Topic/Requirements_for_Azure_Rights_Management.md) emne.

Når du har aktiveret Azure RMS, alle brugere i organisationen kan anvende beskyttelse af oplysninger på deres filer og alle brugere kan åbne (forbruger) filer, der er beskyttet af Azure RMS. Men hvis du foretrækker det, kan du begrænse der kan anvende beskyttelse af oplysninger, ved hjælp af onboarding af indstillinger for en faseopdelt installation. Yderligere oplysninger finder du i [Konfiguration af onboarding af indstillinger for en faseopdelt installation](../Topic/Activating_Azure_Rights_Management.md#BKMK_OnboardingControls) afsnit i dette emne.

## Aktivering af rettighedsstyring
Brug en af følgende fremgangsmåder til at aktivere [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)].

> [!TIP]
> Du kan også bruge Windows PowerShell-cmdlet, [Aktiver Aadrm](http://msdn.microsoft.com/library/windowsazure/dn629412.aspx), for at aktivere [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)].

#### At aktivere Rights Management på Office 365 admin-Center

1.  Når du har tilmeldt dig til en Office 365-plan, der omfatter Rights Management, [logge på Office 365 med din konto til arbejdet eller skolen](https://portal.office.com/) der er administrator for din installation af Office 365.

2.  Hvis Office 365 admin center ikke automatisk vises, Vælg ikonet app Opgavestarter i øverst til venstre og vælge **Admin**. Den **Admin** side om side vises kun til Office 365-administratorer.

    > [!TIP]
    > Admin center Hjælp finder du under [om på Office 365 admin center - Admin Hjælp](https://support.office.com/article/About-the-Office-365-admin-center-Admin-Help-58537702-d421-4d02-8141-e128e3703547).

3.  I venstre rude kan du udvide **Indstillinger for**.

4.  Klik på **Rights Management**.

    > [!NOTE]
    > Hvis du ikke kan se denne indstilling, kan det skyldes service plan eller produkt-versionen kan ikke understøtter rettighedsstyring, eller den er endnu ikke opgraderet understøtter rettighedsstyring.
    > 
    > Brug oplysningerne i den [Sky-abonnementer, der understøtter Azure RMS](../Topic/Requirements_for_Azure_Rights_Management.md#BKMK_SupportedSubscriptions) afdeling i den [Krav til Azure rettighedsstyring](../Topic/Requirements_for_Azure_Rights_Management.md) emne for at bekræfte support. Hvis din service plan eller produkt version understøttes, men du ikke kan se indstillingen Rights Management, kan det skyldes tjenesten ikke er endnu opgraderet. Hjælp til dette problem, skal du sende en e-mail til [askipteam](mailto:askipteam@microsoft.com?subject=I%20cannot%20activate%20RMS).

5.  På den **RIGHTS MANAGEMENT** skal du klikke på **Manage**.

6.  På den **rettighedsstyring** skal du klikke på **aktivere**.

7.  Når du bliver bedt om **vil du aktivere Rights Management?**, skal du klikke på **aktivere**.

Du kan nu se **Rights management er aktiveret** og mulighed for at deaktivere.

#### At aktivere Rights Management fra Azure Management Portal

1.  Når du har tilmeldt dig til kontoen Azure [logge på portalen Azure Management](http://go.microsoft.com/fwlink/p/?LinkID=275081).

2.  Klik på i venstre rude, **ACTIVE DIRECTORY**.

3.  Fra den **active directory** skal du klikke på **RIGHTS MANAGEMENT**.

4.  Vælg mappe til at administrere for [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)], skal du klikke på **Aktiver**, og derefter bekræfte din handling.

    > [!NOTE]
    > Hvis du ser en fejl under aktivering, kan det skyldes din service plan eller produkt-version ikke understøtter [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)].
    > 
    > Brug oplysningerne i den [Sky-abonnementer, der understøtter Azure RMS](../Topic/Requirements_for_Azure_Rights_Management.md#BKMK_SupportedSubscriptions) afsnit i den [Krav til Azure rettighedsstyring](../Topic/Requirements_for_Azure_Rights_Management.md) emne for at bekræfte RMS-support. Hjælp til dette problem, skal du sende en e-mail til [askipteam](mailto:askipteam?subject=I%20cannot%20activate%20RMS).

Den **RIGHTS MANAGEMENT STATUS** skal nu vise **aktive** og **Aktiver** erstattes af **Deaktiver**.

### Rights Management statusværdier og beskrivelser i Azure Management Portal
Ud over den **aktive** status, der angiver, at Rights Management-tjenesten er aktiveret og klar til brug, du kan også se **inaktiv**, **utilgængelig**, eller **uautoriseret**.

|Statusværdi|Beskrivelse|
|---------------|---------------|
|**Aktive**|[!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] er aktiveret og klar til brug.|
|**Inaktive**|[!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] er deaktiveret, og skal være aktiveret, før organisationen kan beskytte filer.|
|**Ikke tilgængelig**|Den [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] service er nede. Prøv igen senere.|
|**Uautoriseret**|Du har ikke tilladelse til at få vist status for den [!INCLUDE[aad_rightsmanagement_2](../Token/aad_rightsmanagement_2_md.md)] service. For eksempel din konto er spærret, eller du er ikke den globale administrator for den valgte lejer.|

## <a name="BKMK_OnboardingControls"></a>Konfiguration af onboarding af indstillinger for en faseopdelt installation
Hvis du ikke ønsker, at alle brugere skal være i stand til at beskytte filer straks ved hjælp af Azure RMS, kan du konfigurere brugerdefinerede onboarding af kontrolelementer ved hjælp af den [sæt AadrmOnboardingControlPolicy](http://msdn.microsoft.com/library/azure/dn857521.aspx) Windows PowerShell-kommando. Du kan køre denne kommando, før eller efter du aktiverer Azure RMS.

> [!IMPORTANT]
> Hvis du vil bruge denne kommando, skal du mindst have version **2.1.0.0** af den [Azure RMS Windows PowerShell modul](http://go.microsoft.com/fwlink/?LinkId=257721).
> 
> Hvis du vil kontrollere den version, du har installeret, ved at køre: **(Get-Module aadrm –ListAvailable).Version**

Hvis du vil som udgangspunkt kun administratorer i gruppen "IT-afdelingen" (som har en objekt-ID for fbb99ded-32a0-45f1-b038-38b519009503) til at være i stand til at beskytte indholdet til testformål, bruge følgende kommando:

```
Set-AadrmOnboardingControlPolicy – SecurityGroupObjectId fbb99ded-32a0-45f1-b038-38b519009503
```
Bemærk, at denne indstilling i konfigurationen, skal du angive en gruppe Du kan ikke angive individuelle brugere.

Eller hvis du vil sikre, at kun brugere, der er korrekt licens til at bruge Azure RMS kan beskytte indhold:

```
Set-AadrmOnboardingControlPolicy -UseRmsUserLicense $true
```
Når du bruger disse onboarding af kontrolelementer, kan alle brugere i organisationen altid forbruge beskyttet indhold, der er beskyttet af en undergruppe af brugere, men de kan ikke selv anvender beskyttelse af oplysninger fra-klientprogrammer. For eksempel ser de i deres Office-kunder de standardskabeloner, der udgives automatisk, når Azure RMS aktiveres eller brugerdefinerede skabeloner, du kan konfigurere.  Serverbaserede programmer som Exchange, kan implementere deres egen brugerspecifikke indstillinger for RMS-integration at opnå det samme resultat.

## Næste trin
Nu hvor du har aktiveret [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] for organisationen, kan du bruge den [Køreplan for Azure Rights Management installation](../Topic/Azure_Rights_Management_Deployment_Roadmap.md) til at kontrollere, om der er andre konfigurationstrin, du skal gøre, før du kaster dig [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] til brugere og administratorer. For eksempel kan du bruge [brugerdefinerede skabeloner](http://technet.microsoft.com/library/dn642472.aspx) for at gøre det lettere for brugerne at anvende beskyttelse af oplysninger i filer, tilslutte dine lokale servere til at bruge [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] ved at installere den [RMS-stik](http://technet.microsoft.com/library/dn375964.aspx), og installere den [Rights Management deling program](http://technet.microsoft.com/library/jj585031.aspx) der understøtter at beskytte alle filtyper på alle enheder. Office-tjenester, som Exchange Online og SharePoint Online kræver yderligere konfiguration, før du kan bruge deres IRM Information Rights Management () funktioner. Dog er der ingen andre konfiguration trin, som du vil gøre, se [Ved hjælp af Azure rettighedsstyring](../Topic/Using_Azure_Rights_Management.md) for operationelle retningslinjer til at understøtte en succesfuld implementering for organisationen.

Du kan finde oplysninger om, hvordan programmerne arbejder med [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)], se [Hvordan programmer understøtter Azure rettighedsstyring](../Topic/How_Applications_Support_Azure_Rights_Management.md).

## Se også
[Konfiguration af Azure rettighedsstyring](../Topic/Configuring_Azure_Rights_Management.md)

