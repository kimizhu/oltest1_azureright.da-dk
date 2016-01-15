---
description: na
keywords: na
title: Configuring Usage Rights for Azure Rights Management
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 97ddde38-b91b-42a5-8eb4-3ce6ce15393d
---
# Konfigurere rettigheder for Azure rettighedsstyring
Når du angiver beskyttelse på filer eller e-mails ved hjælp af Azure Rights Management (Azure RMS), og du ikke bruger en skabelon, skal du selv konfigurere brugerrettighederne. Når du konfigurerer brugerdefinerede skabeloner til Azure RMS, vælger du desuden brugerrettighederne, som derefter automatisk anvendes, når skabelonen, der er valgt af brugere, administratorer, eller services er konfigureret. For eksempel i Azure portal kan du vælge roller, konfigurere en logisk gruppering af rettighederne, eller du kan konfigurere individuelle rettigheder.

Du kan bruge dette emne til at hjælpe dig med at konfigurere de brugerrettigheder, du vil bruge til det program, du bruger, og forstå, hvordan disse rettigheder fortolkes af programmer.

## Rettigheder og beskrivelser
I følgende tabel vises og beskrives de rettigheder, der understøtter rettighedsstyring, og hvordan de bruges og fortolkes. I denne tabel, den **almindelige navn** er typisk, hvordan du kan se Brug højre vises, eller der refereres til som en mere brugervenlig version af værdien af ét ord, der bruges i koden (den **kodning i politik** værdi). Den **API konstant eller værdi** er navnet SDK for et MSIPC-API-kald, bruges, når du skriver et RMS-enlightened program, der undersøger, om en højre forbrug eller tilføjer et forbrug ret til en politik.

|Almindeligt navn|Kodning i politik|Beskrivelse|Gennemførelse i brugerdefinerede Office-rettigheder|Navn på portalen Azure|Navn på AD RMS-skabeloner|API konstant eller værdi|Yderligere oplysninger|
|--------------------|---------------------|---------------|-------------------------------------------------------|--------------------------|-----------------------------|----------------------------|--------------------------|
|Rediger indhold, Rediger|DOCEDIT|Tillader brugeren at ændre, flytte, formatere eller filtrere indhold fra programmet. Det giver ikke ret til at gemme en redigeret kopi.|Som en del af den **ændring af** og **fuld kontrol** indstillinger.|**Rediger indhold**|**Rediger**|Ikke tilgængelig|Denne rettighed kan også bruger til at gemme dokumentet i Office-programmer.|
|Gem|REDIGER|Tillader brugeren at gemme dokumentet i dets nuværende placering.|Som en del af den **ændring af** og **fuld kontrol** indstillinger.|**Gem filen**|**Gem**|IPC_GENERIC_WRITEL "REDIGER"|Denne rettighed kan også bruger til at redigere dokumentet i Office-programmer.|
|Kommentar|KOMMENTAR|Giver mulighed for at tilføje anmærkninger eller kommentarer til indholdet.|Ikke implementeret|Ikke implementeret|Ikke implementeret|IPC_GENERIC_COMMENTL "KOMMENTAR"|Denne rettighed findes i SDK, er tilgængelig som en ad hoc-politik i modulet RMS beskyttelse til Windows PowerShell og er blevet implementeret i nogle programmer til leverandøren. Dog ikke er udbredt og understøttes ikke i øjeblikket af Office-programmer.|
|Gem som, eksport|EKSPORTERE|Giver mulighed for at gemme indholdet på et andet filnavn (Gem som). Afhængigt af programmet, kan filen gemmes uden beskyttelse.|Som en del af den **ændring af** og **fuld kontrol** indstillinger.|**Eksportere indhold (Gem som)**|**Eksport (Gem som)**|IPC_GENERIC_EXPORTL "EKSPORT"|Denne rettighed kan brugeren udføre andre eksportindstillinger i programmer, som også **Send til OneNote**.|
|Fremad|FREMAD|Giver mulighed for at videresende en e-mail-meddelelse og føje modtagere til den **til** og **Cc** linjer.|Nægtet, når du bruger den **Videresend ikke** standard politik.|**Fremad**|**Fremad**|IPC_EMAIL_FORWARDL "FREMAD"|Tillader ikke videresendelse til at tildele rettigheder til andre brugere som en del af handlingen fremad.|
|Fuld kontrol|EJER|Giver alle rettigheder til dokumentet, og alle tilgængelige handlinger kan udføres.|Som den **fuld kontrol** brugerdefineret indstilling.|**Fuld kontrol**|**Fuld kontrol**|IPC_GENERIC_ALLL "EJER"|Omfatter muligheden for at fjerne beskyttelsen.|
|Udskriv|UDSKRIV|Aktiverer indstillinger til at udskrive indholdet.|Som den **Udskriv indhold** indstilling i brugerdefinerede tilladelser. Ikke en pr. modtager indstilling.|**Udskriv**|**Udskriv**|IPC_GENERIC_PRINTL "PRINT|Ingen yderligere oplysninger|
|Svar|SVAR|Aktiverer indstillingen svar i en e-mail-klient, uden at tillade ændringer i den **til** eller **Cc** linjer.|Ikke tilgængelig|**Svar**|**Svar**|IPC_EMAIL_REPLY|Ingen yderligere oplysninger|
|Svar til alle|REPLYALL|Gør det muligt for den **svar til alle** i en e-mail-klient, men du ikke tillader brugeren at tilføje modtagere til den **til** eller **Cc** linjer.|Ikke tilgængelig|**Svar til alle**|**Svar til alle**|IPC_EMAIL_REPLYALLL "REPLYALL"|Ingen yderligere oplysninger|
|Få vist åbne, læse|VIS|Tillader brugeren at åbne dokumentet og få vist indholdet.|Som den **læse** brugerdefineret politik **Se** indstilling.|**Vis indhold**|**Vis**|IPC_GENERIC_READL "VISNING"|Ingen yderligere oplysninger|
|Kopier|UDTRÆK|Aktiverer indstillinger til at kopiere data fra dokumentet til det samme eller et andet dokument.|Som den **give brugere med læseadgang til at kopiere indhold** indstilling brugerdefineret politik.|**Kopier og ekstrakt indhold**|**Udtræk**|IPC_GENERIC_EXTRACTL "EXTRACT"|I nogle programmer gør det også hele dokumentet skal gemmes i ubeskyttet.|
|Visningsrettigheder|VIEWRIGHTSDATA|Tillader brugeren at få vist den politik, der er anvendt i dokumentet.|Ikke implementeret|**Få vist tildelte rettigheder**|**Visningsrettigheder**|IPC_READ_RIGHTSL "VIEWRIGHTSDATA"|Ignoreret af nogle programmer.|
|Rediger rettigheder|EDITRIGHTSDATA|Tillader brugeren at ændre den politik, der er anvendt i dokumentet. Omfatter, herunder at fjerne beskyttelsen.|Ikke implementeret|**Rediger rettigheder**|**Rediger rettigheder**|IPC_WRITE_RIGHTSL "EDITRIGHTSDATA"|Ingen yderligere oplysninger|
|Tillad makroer|OBJMODEL|Giver mulighed for at køre makroer eller udføre andre programmerede eller ekstern adgang til indholdet i et dokument.|Som den **tillade programmeringsmæssig adgang** indstilling brugerdefineret politik. Ikke en pr. modtager indstilling.|**Tillad makroer**|**Tillad makroer**|Ikke tilgængelig|Ingen yderligere oplysninger|

## Rettigheder som tilladelsesniveauer
Nogle programmer kan samle rettighederne til tilladelsesniveauer, der gør det nemmere at vælge de rettigheder, der typisk bruges sammen. Disse niveauer i permisisons hjælper med at abstrakt et kompleksitetsniveau fra brugere, så de kan vælge indstillinger, der er baseret på rolle.  For eksempel **læser** og **medforfatter**. Selvom disse indstillinger ofte vise brugerne en oversigt over rettighederne, kan de ikke omfatter enhver rettighed, der er angivet i ovenstående tabel.

Brug følgende tabel til en liste over disse tilladelsesniveauer og en komplet liste over de rettigheder, de indeholder.

|Tilladelsesniveau|Programmer|Rettigheder (almindelige navn)|
|---------------------|--------------|----------------------------------|
|Fremviser|Azure portal<br /><br />Rettighedsstyring, deling af programmer til Windows|Få vist åbne, læse<br /><br />Svar<br /><br />Svar til alle|
|Korrekturlæser|Azure portal<br /><br />Rettighedsstyring, deling af programmer til Windows|Få vist åbne, læse<br /><br />Gem<br /><br />Rediger indhold, Rediger<br /><br />Reply<sup>*</sup><br /><br />Svar til alle<sup>*</sup><br /><br />Fremad<sup>*</sup>|
|Medforfatter|Azure portal<br /><br />Rettighedsstyring, deling af programmer til Windows|Få vist åbne, læse<br /><br />Gem<br /><br />Rediger indhold, Rediger<br /><br />Kopier<br /><br />Visningsrettigheder<br /><br />Rediger rettigheder<br /><br />Tillad makroer<br /><br />Gem som, eksport<br /><br />Udskriv<br /><br />Reply<sup>*</sup><br /><br />Svar til alle<sup>*</sup><br /><br />Fremad<sup>*</sup>|
|Medejer|Azure portal<br /><br />Rettighedsstyring, deling af programmer til Windows|Få vist åbne, læse<br /><br />Gem<br /><br />Rediger indhold, Rediger<br /><br />Kopier<br /><br />Visningsrettigheder<br /><br />Rediger rettigheder<br /><br />Tillad makroer<br /><br />Gem som, eksport<br /><br />Udskriv<br /><br />Reply<sup>*</sup><br /><br />Svar til alle<sup>*</sup><br /><br />Fremad<sup>*</sup><br /><br />Fuld kontrol|
<sup>*</sup> Ikke gælder for de Rights Management, deling af programmer til Windows

## Rettigheder, der er inkluderet i standardskabeloner
De rettigheder, der følger med standardskabelonerne er som følger:

|Vist navn|Rettigheder (almindelige navn)|
|-------------|----------------------------------|
|&lt; Organisationsnavn &gt; - kun fortrolige visning|Få vist åbne, læse|
|&lt; Organisationsnavn &gt; - fortrolige|Få vist åbne, læse<br /><br />Gem<br /><br />Rediger indhold, Rediger<br /><br />Visningsrettigheder<br /><br />Tillad makroer<br /><br />Fremad<br /><br />Svar<br /><br />Svar til alle|

## Se også
[Konfiguration af Azure rettighedsstyring](../Topic/Configuring_Azure_Rights_Management.md)

