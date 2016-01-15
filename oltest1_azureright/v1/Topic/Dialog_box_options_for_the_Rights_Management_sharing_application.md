---
description: na
keywords: na
title: Dialog box options for the Rights Management sharing application
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7b91ab30-6363-4929-bcbd-4dfbd05f644a
---
# Dialogboksens indstillinger for rettighedsstyring, der deler programmet
Med disse oplysninger kan du angive indstillingerne i RMS deling program **føje beskyttelse** dialogboksen eller **del, der er beskyttet med** dialogboksen. Denne dialogboks vises når du [beskytte en fil til at dele](http://technet.microsoft.com/library/dn574735.aspx) eller [beskytte en fil i stedet](http://technet.microsoft.com/library/dn574733.aspx) og vælge brugerdefinerede tilladelser.

> [!IMPORTANT]
> Hvis de viste indstillinger er forskellige fra dem, der er beskrevet her, har du sandsynligvis ikke den nyeste version af programmet deling er installeret. Du kan hente den nyeste version fra den [Microsoft Rights Management](http://go.microsoft.com/fwlink/?LinkId=303970) side.
> 
> Hvordan ved du, hvis du har den nyeste version? Søg efter **Microsoft Rights Management deling program** vises i programmer og funktioner, og Kontroller det tilsvarende versionsnummer. Hvis du vil se og bruge indstillingerne i tabellen, versionen skal være mindst **1.0.1770.0**. Du kan se nummeret på den nyeste version fra download-siden.

Ud over de indstillinger, du kan vælge, du også tænker muligvis:

-   [Hvad er den .ppdf-fil, der oprettes automatisk?](../Topic/Dialog_box_options_for_the_Rights_Management_sharing_application.md#BKMK_PPDF)

-   [Hvad er forskellen mellem generiske beskyttelse og indbygget (standard) beskyttelse?](../Topic/Dialog_box_options_for_the_Rights_Management_sharing_application.md#BKMK_GenericNative)

|Indstilling|Beskrivelse|
|---------------|---------------|
|**BRUGERE**|Hvis du ikke allerede har angivet en e-mail-adresse fra Outlook, kan du skrive e-mail-adresserne på de personer, du vil være i stand til at åbne filen.<br /><br />Hvis din organisation bruger den lokale version af Rights Management (AD RMS), er kan du angive e-mail-adresser begrænset til personer i din organisation. Når det gælder, og du prøver at angive eksterne e-mail-adresser, vises en meddelelse om, at firmakonfigurationen giver mulighed for Deling af beskyttet indhold internt i virksomheden. Hvis din organisation bruger Azure RMS, kan disse e-mail-adresser dog for personer i din organisation, eller for personer i en anden organisation.<br /><br />For eksempel: janetm@contoso.com; p.dover@Fabrikam.com|
|**Generel beskyttelse**|Hvis denne indstilling er markeret, betyder det, at den valgte fil oprindeligt ikke kan beskyttes. Du kan finde flere oplysninger. [Hvad er forskellen mellem generiske beskyttelse og indbygget (standard) beskyttelse?](../Topic/Dialog_box_options_for_the_Rights_Management_sharing_application.md#BKMK_GenericNative) i dette emne.|
|**Fremviser – få kun vist.**<br /><br />**Korrekturlæser – få vist og redigere**<br /><br />**Medforfatter – få vist, redigere, kopiere og udskrive**<br /><br />**Medejer – alle tilladelser** **Note:** Disse indstillinger har et ikon med en runde før navnet, som repræsenterer en globus i verden. Dette ikon bruges, fordi du normalt vælge en af disse indstillinger, når du sender en vedhæftet fil til en i en anden organisation.|Vælg en af følgende indstillinger, hvis du vil definere rettigheder for et beskyttet dokument. Klik på hver enkelt indstilling for at få vist en beskrivelse.<br /><br />Når du vælger en af disse indstillinger, kun personerne, du angiver i **brugere** har rettighederne du angiver for at åbne og bruge dokumentet. For eksempel, hvis de sender videre til en anden, åbnes dokumentet ikke.|
|Politikskabeloner, der konfigurerer administratoren.<br /><br />For eksempel, hvis dit firmanavn er Contoso, Ltd: **Contoso, Ltd - kun fortrolige visning** **Note:** Disse indstillinger har et firkantet ikon før navnet, som repræsenterer en kontorbygning. Dette ikon bruges, fordi du normalt vælge en af disse indstillinger, når du sender en vedhæftet fil til nogen i din organisation.|Når du deler et dokument med personer, der arbejder for virksomheden, kan du se de tilgængelige politikskabeloner, der konfigureres af administratoren. Vælg en af disse, når dokumentet ikke blive delt uden for organisationen.<br /><br />Når du vælger en af disse indstillinger, definerer administratoren rettigheder til dokumentet, og hvem der kan åbne den.|
|**Disse dokumenter udløbe**|Vælg denne indstilling for tid-følsomme filer, som de brugere, du har valgt ikke skal kunne åbne efter en dato, du angiver. Du vil stadig kunne åbne den oprindelige fil, men efter midnat (den aktuelle tidszone), på den dag, du angiver andre vil ikke kunne åbne filen.<br /><br />Denne indstilling er ikke tilgængelig, hvis du vælger en politikskabelon, som systemadministratoren konfigurerer.|
|**Email mig, når nogen forsøger at åbne disse dokumenter**|**Note:** Denne indstilling er i Vis udskrift.<br />Vælg denne indstilling, hvis du vil modtage e-mail-beskeder, når nogen forsøger at åbne det dokument, du beskytte. E-mailen vil sige, hvem der har forsøgt at åbne den, hvornår og om de blev gennemført.<br /><br />Denne indstilling er kun tilgængelig, hvis din organisation bruger Azure RMS. Hvis din organisation bruger den lokale version af Rights Management (AD RMS), vises denne indstilling ikke.|
|**Lad mig straks at tilbagekalde adgang til disse dokumenter**|Vælg denne indstilling, hvis du kan være nødvendigt at tilbagekalde adgang til dokumenterne, der senere ved hjælp af webstedet til dokumentsporing og tilbagekaldelse skal træde i kraft straks. Angivelse af denne indstilling betyder, mens dokumentet ikke er tilbagekaldt, skal brugerne altid dog en internetforbindelse til at læse dokumentet, hver gang de åbner den. Der kan være nogle situationer, hvor brugere kan tilslutte deres enhed til internettet, og brugere kan ikke læse dokumentet efter hensigten.<br /><br />Hvis du ikke vælger denne indstilling, kan du stadig tilbagekalde dokumenterne, der senere ved hjælp af dokument-registreringswebstedet. Men da brugerne ikke behøver altid en internetforbindelse til at læse dokumentet, de ikke vide straks, at dokumentet er blevet tilbagekaldt, og kan fortsætte med at læse den, indtil de næste godkender med Azure RMS. Det maksimale antal dage, som nogen kunne fortsætte med at læse et beskyttet dokument, du har tilbagekaldt er 30 dage som standard, men en administrator kan ændre denne værdi for at være større end 30 dage eller færre.<br /><br />Denne indstilling er kun tilgængelig, hvis din organisation bruger Azure RMS. Hvis din organisation bruger den lokale version af Rights Management (AD RMS), vises denne indstilling ikke.|

## <a name="BKMK_GenericNative"></a>Hvad er forskellen mellem generiske beskyttelse og indbygget (standard) beskyttelse?

-   Når du **generisk beskytte en fil**, uautoriserede brugere kan ikke åbne filen. Men når autoriserede personer åbne filen, kan de derefter videresende den til andre ubeskyttede eller gemme den et sted, som andre kan få adgang til. De gør, dog, vises en meddelelse, der fortæller dem, hvilke tilladelser de har til filen, og de bliver bedt om at imødekomme disse, men denne beskyttelse kan ikke gennemtvinges. Når du beskytter generisk en fil, kan du desuden begrænse rettighederne yderligere godkendelse. For eksempel, du kan ikke begrænse indholdet til kun at få vist eller Udskriv ikke.:

    > [!NOTE]
    > En generisk beskyttet fil altid har et filtypenavn på **.pfile**.

-   I sammenligning, når du bruger den **indbygget (standard) beskyttelse** af Rights Management med programmer, der understøtter det (f.eks Office-filer), gælder beskyttelsen til fil, selvom filen sendes til nogen anden eller gemt på en anden placering. Og når du beskytter disse filer, kan du bruge restriktive tilladelser som skrivebeskyttet, eller tilladelse til at redigere, men ikke udskrive eller kopiere. For eksempel kan du vælge **Fremviser – Vis kun**, således at indholdet ikke kan redigeres, udskrives eller kopieres.

Yderligere tekniske oplysninger finder du under de [Niveauer af beskyttelse – oprindelig og generiske](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_LevelsofProtection) afsnit i den [Rights Management deling program administratorvejledningen](../Topic/Rights_Management_sharing_application_administrator_guide.md).

## <a name="BKMK_PPDF"></a>Hvad er den .ppdf-fil, der oprettes automatisk?

-   Når du deler en beskyttet fil via e-mail (dele beskyttet), RMS deling programmet automatisk opretter en **.ppdf** version af filen til Word, Excel, PowerPoint eller PDF-fil. Dette er et skrivebeskyttet beskyttet version af den fil, der kun godkendte brugere kan åbne, og det sikrer, at modtagerne kan altid få vist den vedhæftede fil, selvom de bruger en mobilenhed, der ikke har et program, som oprindeligt understøtter rettighedsstyring. Forudsat at disse personer har RMS deling app installeret, vil de kunne læse den vedhæftede fil.

    I dette scenario, i modsætning til en generisk beskyttet fil gennemtvinges format begrænsning. Modtageren kan ikke gemme denne version af filen, og hvis de sender den vedhæftede fil til en anden, forbliver de oprindelige begrænsninger med dokumentet. Kun personer, der var givet tilladelse til det beskyttede dokument vil kunne åbne den.

    > [!NOTE]
    > En .ppdf-fil oprettes automatisk, når du deler beskyttet (dele pr. e-mail), men oprettes ikke, når du beskytter på stedet.

## Eksempler og andre instruktioner
I de følgende afsnit i brugervejledningen til deling program til Rights Management eksempler til hvordan du kan bruge den Rights Management, deling af programmer og vejledninger:

-   [Eksempler på brug af RMS deling program](../Topic/Rights_Management_sharing_application_user_guide.md#BKMK_SharingExamples)

-   [Hvad vil du gøre?](../Topic/Rights_Management_sharing_application_user_guide.md#BKMK_SharingInstructions)

## Se også
[Rights Management deling program bruger guide](../Topic/Rights_Management_sharing_application_user_guide.md)

