---
description: na
keywords: na
title: Logging and Analyzing Azure Rights Management Usage
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a735f3f7-6eb2-4901-9084-8c3cd3a9087e
---
# Logf&#248;ring og analyse af brugen af Azure Rights Management
Du kan bruge oplysningerne i dette emne til at hjælpe dig med at forstå, hvordan du kan bruge logføring med Azure Rights Management (Azure RMS) forbrug. Azure Rights Management-tjenesten kan logge alle anmodninger, at det er for din organisation, som omfatter anmodninger fra brugere, handlinger, der udføres af administratorer til Rights Management i organisationen og handlinger, der udføres af Microsoft operatorer til at understøtte implementeringen Azure Rights Management.

Du kan derefter bruge disse Azure Rights Management-logfiler til at understøtte følgende virksomhedsscenarier:

-   Analyse til brancheindsigt.

    Azure rettighedsstyring skriver logfiler i udvidede W3C-logfilformat til en Azure storage-konto, du angiver. Du kan derefter give disse logfiler til et lager af dit valg (en database, OLAP (online analytical processing)-systemet, eller en kort reducere system) til at analysere oplysninger og lave rapporter. Som et eksempel kan du identificere, hvem der får adgang til RMS-beskyttede data. Du kan bestemme, hvad RMS-beskyttede data personer har adgang til, og fra hvilke enheder og hvorfra. Du kan finde ud af, om brugerne kan læse beskyttet indhold. Du kan også angive, hvilke personer der har læst et vigtigt dokument, som er beskyttet.

-   Skærm for misbrug.

    Oplysninger om rettighedsstyring logføring af Azure er tilgængelige i nær-realtid, så du løbende kan overvåge virksomhedens brug af Rights Management. 99,9% af logfiler er tilgængelige inden for 15 minutter af en RMS-har iværksat denne handling.

    For eksempel kan du få en advarsel, hvis der er en pludselig forøgelse af personer, der læser RMS-beskyttede data uden for almindelige arbejdstid, hvilket kunne tyde på, at en ondsindet bruger indsamler oplysninger til at sælge til konkurrenterne. Eller, hvis den samme bruger tilsyneladende har adgang til data fra to forskellige IP-adresser inden for et kort tidsrum, som kunne tyde på, som en brugerkonto er blevet afsløret.

-   Udføre sikkerhedsværktøj analyse.

    Hvis du har en hukommelsesfejl i oplysninger, er du sandsynligvis skal stilles der for nylig adgang til bestemte dokumenter, og hvilke oplysninger en mistænkt person adgang til for nylig. Du kan besvare disse type spørgsmål, når du bruger Azure Rights Management og logføring, fordi personer, der bruger beskyttet indhold skal altid have en Rights Management-licens til at åbne dokumenter og billeder, der er beskyttet af Azure Rights Management, selvom disse filer flyttes via e-mail eller kopieret til USB-drev eller andre lagringsenheder. Det betyder, at du kan bruge Azure Rights Management logfiler som endelige kilde til oplysninger for sikkerhedsværktøj analyse når du beskytter dine data ved hjælp af Azure Rights Management.

> [!NOTE]
> Hvis du er interesseret i logføring af administrative opgaver for Azure Rights Management, og Benyt ikke ønsker at spore, hvordan brugerne anvender Rights Management, kan du bruge den [få AadrmAdminLog](https://msdn.microsoft.com/library/azure/dn629430.aspx) Windows PowerShell-cmdlet til Azure Rights Management.
> 
> Du kan også bruge portalen Azure til overordnede anvendelsesrapporter, der omfatter **Brug af RMS**, **mest aktive brugere af RMS**, **Brug af RMS-enheden**, og **RMS aktiveret programbrug**. For at få adgang til disse rapporter fra Azure portal, skal du klikke på **Active Directory**, Vælg og Åbn en mappe og derefter klikke på **rapporter**,

Brug de følgende afsnit kan finde flere oplysninger om rettighedsstyring Azure Besøgslogføringen.

-   [Sådan aktiveres logføring af Azure Rights Management-forbrug](../Topic/Logging_and_Analyzing_Azure_Rights_Management_Usage.md#BKMK_EnableRMSLogging)

-   [Adgang til og bruge din Azure Rights Management besøgslogfiler](../Topic/Logging_and_Analyzing_Azure_Rights_Management_Usage.md#BKMK_AccesAndUseLogs)

-   [Sådan administreres lagerpladsen Azure Rights Management log](../Topic/Logging_and_Analyzing_Azure_Rights_Management_Usage.md#BKMK_ManageStorage)

-   [Sådan stedfortræderadgang til din Azure Rights Management besøgslogfiler](../Topic/Logging_and_Analyzing_Azure_Rights_Management_Usage.md#BKMK_Delegate)

-   [Sådan fortolkes besøgslogfiler din Azure Rights Management](../Topic/Logging_and_Analyzing_Azure_Rights_Management_Usage.md#BKMK_Interpret)

-   [Windows PowerShell-reference](../Topic/Logging_and_Analyzing_Azure_Rights_Management_Usage.md#BKMK_PowerShell)

## <a name="BKMK_EnableRMSLogging"></a>Sådan aktiveres logføring af Azure Rights Management-forbrug
Azure rettighedsstyring Besøgslogføring er valgfri, så hvis du vil bruge den, skal du udføre bestemte trin. Når du bruger Besøgslogføringen Azure Rights Management, der er ingen ændring i hvordan fungerer Rights Management og logføringsprocessen selve er gratis. Men du skal angive en konto på Azure storage for logfilerne, og du skal betale for dette lager.

Før du begynder, skal du kontrollere, at du opfylder følgende forudsætninger for at bruge Azure Rights Management Besøgslogføringen:

|Kravet om|Yderligere oplysninger|
|-------------|--------------------------|
|Et IT-styret abonnement, der omfatter Azure Rights Management|Du skal have et abonnement på Microsoft Azure Rights Management, der administreres af din organisation. Organisationer, der bruger RMS for personer kan ikke bruge Besøgslogføringen Azure Rights Management.<br /><br />Hvis din organisation har brugere, der bruger RMS for personer, indeholder Azure Rights Management Besøgslogføringen business meget gode grunde til at konvertere RMS personer til et abonnement på Microsoft Azure Rights Management.<br /><br />Finde flere oplysninger om, hvilke abonnementer, der omfatter Azure RMS i [Sky-abonnementer, der understøtter Azure RMS](../Topic/Requirements_for_Azure_Rights_Management.md#BKMK_SupportedSubscriptions) afsnit i den [Krav til Azure rettighedsstyring](../Topic/Requirements_for_Azure_Rights_Management.md) emne.<br /><br />Finde flere oplysninger om RMS for personer [RMS for enkeltpersoner og Azure rettighedsstyring](../Topic/RMS_for_Individuals_and_Azure_Rights_Management.md)|
|Azure-abonnement|Du skal have et abonnement på Azure og tilstrækkelig lagerplads på Azure for Azure Rights Management-logfiler.|
|Windows PowerShell til Azure rettighedsstyring|Hvis du ikke allerede har gjort det, kan du hente og installere Windows PowerShell-modul til Azure Rights Management. Du skal bruge Windows PowerShell-cmdletter til at konfigurere og administrere din Azure Rights Management besøgslogfiler.<br /><br />Yderligere oplysninger finder du under [Installation af Windows PowerShell til Azure rettighedsstyring](../Topic/Installing_Windows_PowerShell_for_Azure_Rights_Management.md).|
Brug følgende fremgangsmåde til at aktivere Besøgslogføringen Azure Rights Management, som omfatter trin for at oprette en konto på Azure storage og derefter konfigurere Azure for at bruge denne konto i lagerplads til Rights Management-logfiler.

> [!NOTE]
> Denne procedure forudsætter, at du har en Azure konto. Azure rettighedsstyring Besøgslogføringen understøtter individuelle konti, men en vane at bruge arbejdet eller skolen konti. Vi anbefaler desuden, at du opretter en dedikeret storage konto for Rights Management-logfiler. Du skal dele hurtigtasterne storage med Azure Rights Management og eventuelt med andre personer, hvis de bruger også logfilerne.
> 
> Finde flere oplysninger om Azure storage, den [Azure dokumentation til lagring af](http://azure.microsoft.com/documentation/services/storage/).

#### Hvordan du opretter din konto i lagerplads og aktiverer logføringen af statistikoplysninger Azure Rights Management

1.  Log på den [Azure portal](https://manage.windowsazure.com/).

2.  Vælg **Storage**.

    > [!TIP]
    > Hvis du ikke kan se denne indstilling, kan du kontrollere, at du har et abonnement, Azure ud over dit abonnement på Rights Management.

3.  Klik på **Opret en STORAGE konto** og den **URL-adresse**, Angiv et entydigt navn for storage-konto og eventuelt ændre den **placering/TILHØRSFORHOLD gruppe** så den passer til dit område.

4.  Klik på **OK**, og Vent, indtil du kan se navnet på din storage vise status **Online**.

5.  Klik på **styre Access-taster**.

6.  Fra den **styre Access-taster** dialogboks, der viser dine primære og sekundære adgangstaster, kopiere den primære hurtigtast til Udklipsholder, og luk derefter dialogboksen.

7.  Start Windows PowerShell med de **Kør som administrator** indstilling. Kør den [Connect-AadrmService](https://msdn.microsoft.com/library/azure/dn629415.aspx) kommando til at oprette forbindelse til Azure Rights Management-tjenesten:

    ```
    Connect-AadrmService
    ```

8.  Brug af [sæt AadrmUsageLogStorageAccount](https://msdn.microsoft.com/library/azure/dn629426.aspx) kommando for at angive, hvor du vil beholde din Azure Rights Management besøgslogfiler erstatter *&lt; Access_Key &gt;* primære hurtigtast, du kopierede i trin 6 og *&lt; StorageAccount &gt;* med navnet på den konto i lagerplads, du oprettede i trin 3:

    ```
    $accesskey = convertto-securestring -asplaintext -force –string <Access_Key> Set-AadrmUsageLogStorageAccount -AccessKey $accesskey -StorageAccount <StorageAccount>
    ```

9. Brug af [Aktiver AadrmUsageLogFeature](https://msdn.microsoft.com/library/azure/dn629421.aspx) kommando for at aktivere Azure Rights Management Besøgslogføringen:

    ```
    Enable-AadrmUsageLogFeature
    ```
    Du bør se meddelelsen: **Brug af log-funktionen er aktiveret for Rights management-tjenesten.**

Nu, at Besøgslogføring er aktiveret, begynder at logge alle aktioner for organisationen Azure Rights Management, og gemmer oplysningerne til din konto i lagerplads. Oplysninger om logføring er ikke tilgængelig indtil dette tidspunkt.

## <a name="BKMK_AccesAndUseLogs"></a>Adgang til og bruge din Azure Rights Management besøgslogfiler
Azure rettighedsstyring skriver logs til din konto på Azure storage som en serie af BLOB. Alle blob indeholder en eller flere logføringsposter i udvidede W3C-logfilformat. Blob-navne er tal, i den rækkefølge, de blev oprettet. Den [Sådan fortolkes besøgslogfiler din Azure Rights Management](../Topic/Logging_and_Analyzing_Azure_Rights_Management_Usage.md#BKMK_Interpret) afsnit senere i dette dokument indeholder flere oplysninger om indholdet i logfilen og deres oprettelse.

Det kan tage et stykke tid for logfiler, der skal vises i din konto i lagerplads efter en Azure Rights Management-handling. De fleste logfiler vises inden for 15 minutter.

Storage-konto, du har oprettet din Azure Rights Management besøgslogfiler er som en postkasse og understøtter læser direkte fra lager-konto, men den er ikke optimeret til at blive brugt på denne måde. I stedet opnår den bedste ydeevne og reducere omkostningerne, anbefales det, at du henter logfilerne til det lokale lager, som en lokal mappe, en database eller en kort reducere lageret.

Du kan hente din besøgslogfiler på to måder:

-   Du kan bruge Windows PowerShell-cmdlet [få AadrmUsageLog](https://msdn.microsoft.com/library/azure/dn629401.aspx).

    Dette er den nemmeste måde at få adgang til din besøgslogfiler. Denne cmdlet henter logger på computeren, henter hver blob som en fil til en placering, du angiver.

-   Brug af [Azure Storage SDK](http://www.windowsazure.com/en-us/develop/net/) til at skrive dine egne brugerdefinerede program til at hente logfilerne.

    Et brugerdefineret program, der kan give større fleksibilitet end Get-AadrmUsageLogs-cmdlet. For eksempel kan du uddelegere overførslen af logfiler til nogen eller en proces, der ikke skal bruge dine administrative legitimationsoplysninger på Azure Rights Management. Eller kan du forespørge logfilerne i realtid, da du vil overvåge for misbrug.

#### At hente din besøgslogfiler ved hjælp af PowerShell

-   Start Windows PowerShell med de **Kør som administrator** indstilling og køre **Get-AadrmUsageLog –Path &lt;location&gt;**. For eksempel, når du har oprettet en mappe med navnet **logs** på E-drevet:

    -   Hente alle tilgængelige logfiler i mappen E:\logs: `Get-AadrmUsageLog -Path "e:\logs"`

    -   At hente et bestemt interval af BLOB: `Get-AadrmUsageLog –Path "e:\logs" –FromCounter 1024 –ToCounter 2047`

Når du kører disse cmdlets, viser navnet på den sidste-blob, der blev hentet i Windows PowerShell. Du kan tildele dette navn til en variabel, kan du køre Get-AadrmUsageLog i en løkke eller en plan, hentes de trinvise logfiler hver gang.

For eksempel:

**PS C:\ &gt; $LastBlobName = Get-AadrmUsageLog – stien "e:\logs"**

**1527**

**PS C:\ &gt; $LastBlobName**

**1527**

> [!TIP]
> Du kan sammenlægge alle hentede logfiler til en CSV-format ved hjælp af [Microsoft Log Parser](http://www.microsoft.com/download/details.aspx?id=24659), som er et værktøj til at konvertere mellem forskellige kendte logfilformater. Du kan også bruge dette værktøj til at konvertere data til SYSLOG-format, eller du kan importere den til en database. Når du har installeret værktøjet, køre **LogParser.exe /?** for hjælp og oplysninger, der skal bruge dette værktøj. For eksempel kan du køre følgende kommando for at importere alle oplysninger i et filformat for .log: **logparser –i:w3c –o:csv “SELECT &#42; INTO AllLogs.csv FROM &#42;.log”**.

Du kan afbryde og genoptage Besøgslogføringen. Når du afbryder logføring, bevarer Azure Rights Management kontooplysningerne storage, så du nemt kan genoptage logge igen.

#### At suspendere og genoptage logføringen af statistikoplysninger

-   Hvis du vil afbryde logføring, skal du bruge følgende cmdlet: [Deaktiver AadrmUsageLogFeature](https://msdn.microsoft.com/library/azure/dn629404.aspx)

-   Hvis du vil genoptage logføring, ved at bruge følgende cmdlet: [Aktiver AadrmUsageLogFeature](https://msdn.microsoft.com/library/azure/dn629421.aspx)

-   Hvis du vil kontrollere, om logging er aktiveret eller deaktiveret, kan du bruge følgende cmdlet: [Get-AadrmUsageLogFeature](https://msdn.microsoft.com/library/azure/dn629425.aspx)

    En værdi på **True** betyder, at Besøgslogføring er aktiveret for Azure Rights Management og en værdi på **False** betyder, at Besøgslogføring er deaktiveret.

## <a name="BKMK_ManageStorage"></a>Sådan administreres lagerpladsen Azure Rights Management log
Du er debiteret for den lagerplads, der bruges til at holde din Azure Rights Management-logfiler.

Azure Rights Management understøtter ikke automatisk administration af din brug af logfiler. Hvis du tager ingen handling, forbliver de på din konto i lagerplads. Men for at spare plads og reducere udgifterne til oplagring, kan du slette dem, når du har hentet dem. Eller du kan vælge, hvilke filer der skal slettes. Med en enkelt undtagelse bruger Azure Rights Management ikke disse logfiler, så der er ingen begrænsninger om, hvor du kan slette dem.

Den fil, du ikke skal slette (eller ændre) hedder **metadata** der findes i den **rms-metadata** beholder. Azure rettighedsstyring bruger denne blob til at holde styr på det sidste blob-nummer, der bruges. Hvis denne fil slettes, Azure Rights Management starter en ny beholder til logfiler, med et blob-nummer, der starter med 1, og alle fremtidige overførsler, der bruger Get-AadrmUsageLog-cmdlet bruger denne nye beholder til at hente logfiler. Alle logfiler i den originale emballage er derfor bevares, men tabt. Den eneste måde at hente disse tabte logfiler er at bruge Azure storage SDK.

> [!TIP]
> Du kan uddelegere funktionen styring til en anden virksomhed i stedet for at administrere din Azure Rights Management log storage selv, ved at dele storage konto navn og adgang til nøglen. Yderligere oplysninger finder du i [Sådan stedfortræderadgang til din Azure Rights Management besøgslogfiler](../Topic/Logging_and_Analyzing_Azure_Rights_Management_Usage.md#BKMK_Delegate) afsnit senere i dette emne.

I nogle tilfælde vil du genoprette din storage access-taster. For eksempel:

-   Du kan ændre det firma, der administrerer din Azure Rights Management besøgslogfiler.

-   Du har mistanke om, at din storage-hurtigtast er skadet.

Hvis dette sker for dig, er når du bruger den sekundære hurtigtast (på den antagelse, at du tidligere har brugt den primære hurtigtast) til at sikre kontinuitet i tjenesten. Når du genoprette den adgangsnøgle, som du ikke tidligere har brugt, kan du derefter konfigurere Azure Rights Management til at bruge den nye nøgle. Benyt følgende fremgangsmåde til at genoprette sekundære hurtigtasten og konfigurere Azure Rights Management til at bruge den:

#### At genoprette den sekundære hurtigtast

1.  Log på den [Azure portal](https://manage.windowsazure.com/).

2.  Vælg **Storage**.

3.  Klik på **styre Access-taster**.

4.  I den **styre Access-taster** dialogboksen, skal du klikke på **genoprette** ved siden af sekundære hurtigtast og kopiere den nye nøgle sekundære adgang til Udklipsholder.

5.  Start Windows PowerShell med de **Kør som administrator** indstilling og bruge den [sæt AadrmUsageLogStorageAccount](https://msdn.microsoft.com/library/azure/dn629426.aspx) -cmdlet til at konfigurere Azure Rights Management til at bruge denne nye hurtigtast, erstatter *&lt; StorageAccount &gt;* med navnet på din konto i lagerplads og *&lt; Access_Key &gt;* den regenererede sekundære hurtigtast, du lige har kopieret:

    ```
    Set-AadrmUsageLogStorageAccount -StorageAccount <StorageAccount>-AccessKey <Access_Key>
    ```
    > [!WARNING]
    > Men når du kører denne kommando, kan du skifte til en anden konto i lagerplads, handlingen orphans tidligere logfilerne, og de vil ikke længere være tilgængelig til Set-AadrmUsageLogStorageAccount-cmdlet eller lignende kommandoer til styring og funktioner.

6.  Tilbage i de **styre Access-taster** dialogboks skal du genoprette din adgang til primær nøgle.

## <a name="BKMK_Delegate"></a>Sådan stedfortræderadgang til din Azure Rights Management besøgslogfiler
Du kan uddelegere adgang til RMS-logfilerne ved at dele storage konto navn og adgang til nøglen. Du vil uddelegere adgang til en anden administrator, en udvikler i din egen organisation eller en uafhængig softwareleverandør (ISV). Fordi de ikke har administratorlegitimationsoplysninger din RMS, kan de ikke bruge Get-AardrmUsageLog-cmdlet til at hente RMS-logfiler. I stedet skal de bruge Windows Storage SDK til at hente logfilerne. Alternativt kan de skrive et program til at læse logger direkte fra Azure Storage.

Det er sikkert at dele storage konto navn og adgang til nøglen på denne måde, når kontoen storage er dedikeret til RMS-logfiler. Selvom andre brugere har adgang til nøglen, kan de ikke bruge dette til at få adgang til en anden konto i lagerplads eller bruge kontoen RMS lejer.

## <a name="BKMK_Interpret"></a>Sådan fortolkes besøgslogfiler din Azure Rights Management
Brug følgende oplysninger til at hjælpe dig med at fortolke besøgslogfiler Azure Rights Management.

### Storage konto layout
Første gang skriver Azure Rights Management logger på din konto i lagerplads, oprettes følgende to beholdere:

-   **Rms-metadata**: Denne beholder er forbeholdt Azure Rights Management. Ikke ændre eller slette denne objektbeholder.

-   **Rms - logs - &lt; guid &gt;**: Denne beholder er hvor Azure Rights Management opretter og gemmer logfilerne. Du kan sikkert slette alle filer i denne objektbeholder, hvis du ikke længere vil logføringsoplysninger, de indeholder.

Over tid, Azure Rights Management kan oprette flere **Rms - logs - &lt; guid &gt;** beholdere. For eksempel hvis de **Rms-metadata** beholder bliver beskadiget eller slettes ved et uheld, Azure Rights Management nulstiller indholdet og opretter en ny **Rms - logs - &lt; guid &gt;** beholder for alle fremtidige logfiler. De gamle logfiler i objektbeholderen gamle slettes ikke, men er tabt.

### Log-sekvens
Azure rettighedsstyring skriver logfilerne som en serie af BLOB. Alle blob indeholder en eller flere logføringsposter i udvidede W3C-logfilformat.

Navnet på hver enkelt blob er et tal. Inden for hver logbeholder hedder første blob 000000001. Hver blob er navngivet sekventielt i den rækkefølge, hvori den blev oprettet. Alle blob indeholder en eller flere logfilposter. Hver enkelt logpost har et UTC tidsstempel, der angiver, hvornår den tilsvarende anmodning er blevet forkyndt på Azure Rights Management.

> [!IMPORTANT]
> Logføring af Azure Rights Management-system er optimeret til at give dig logfiler hurtigt i stedet for i nøje rækkefølge. Rækkefølgen af blob, samt rækkefølgen af poster i en blob muligvis forkert kronologisk rækkefølge. Den eneste grund til BLOB er navngivet sekventielt er at du kan hente dem effektivt trinvist.
> 
> To eksempler på mulige log sekvens resultater:
> 
> -   Logposter i blob-000000004 kan overlappe kronologisk med logposter i blob-000000003. I ekstreme tilfælde, alle poster i logfilen i blob 000000004 måske er oprettet før alle poster i logfilen i blob-000000003.
> -   Den anden post i loggen i en blob måske er oprettet før den første post i loggen, men blev skrevet til opbevaring i omvendt rækkefølge.

Før du analysere dine Azure Rights Management besøgslogfiler, anbefales det, at du henter og importerer logfilen til et lager, hvor du kan sortere de logfiler, der er baseret på deres tidsstempel. Finde flere oplysninger ved at hente logfilerne, den [Adgang til og bruge din Azure Rights Management besøgslogfiler](../Topic/Logging_and_Analyzing_Azure_Rights_Management_Usage.md#BKMK_AccesAndUseLogs) afsnit i dette emne.

Da logfilerne er ikke nødvendigvis kronologisk, men fleste af dem er skrevet senest 15 minutter efter anmodning, når du identificerer de logfiler, som du vil ved hjælp af deres tidsstempel, 15 minutter tilsættes til den tid, du er interesseret i. Derefter hente disse logfiler. Denne strategi bør sikre, at du får næsten alle logfiler.

En anden ting at huske er, at tidsstemplet på hver enkelt logpost det lokale signeringstidspunkt på Azure Rights Management-tjenesten, der har behandlet anmodningen. Da Azure Rights Management kører på flere servere på tværs af flere datacenter, kan undertiden logfilerne forekomme at være usammenhængende, selv når de er sorteret efter deres tidsstempel. Men den anden er lille og normalt inden for et minut. I de fleste tilfælde er det ikke et problem, der ville være et problem for analyse af logfilen.

### Blob-format
Alle blob er i udvidede W3C-logfilformat. Det starter med de to følgende linjer:

**#Software: RMS**

**#Version: 1.1**

Den første linje angiver, at disse er Azure Rights Management-logfiler. Den anden linje angiver, at resten af blob følger version 1.1-specifikationen. Vi anbefaler, at programmer, der kan analysere disse logfiler kontrollerer disse to linjer, før du fortsætter med at analysere resten af blob.

Den tredje linje optæller en liste over feltnavne, der er adskilt af tabulatorer:

**#Fields: dato tid række-id anmodningstype bruger-id resultatet Korrelations-id indhold-id ejer e-mail-udstederen skabelon-id-filnavn Udgivelsesdato c-info c ip-**

Hver af de efterfølgende linjer er en logpost. Værdierne i felterne, der er i samme rækkefølge som den foregående linje, og er adskilt af tabulatorer. Brug følgende tabel til at fortolke felterne.

|Feltnavn|W3C datatype|Beskrivelse|Eksempel værdi|
|------------|----------------|---------------|------------------|
|dato|Dato|UTC-dato, hvor anmodningen er blevet forkyndt.<br /><br />Kilden er det lokale klokkeslæt på den server, der betjenes af anmodningen.|2013-06-25|
|tid|Tid|UTC-klokkeslæt i 24-timers format, når anmodningen er blevet forkyndt.<br /><br />Kilden er det lokale klokkeslæt på den server, der betjenes af anmodningen.|21:59:28|
|række-id|Tekst|GLOBALLY Unique for denne post i loggen.<br /><br />Denne værdi er nyttig, når du samle logfiler eller kopi logfiler til et andet format.|1c3fe7a9-d9e0-4654-97b7-14fafa72ea63|
|anmodningstypen|Navn|Navnet på den RMS-API, der blev anmodet om.|AcquireLicense|
|bruger-id|Streng|Den bruger, der har fremsat anmodningen.<br /><br />Værdien er omgivet af enkelte anførselstegn. Nogle anmodningstyper er anonym, så værdien er ".|«den joe@contoso.com»|
|resultatet|Streng|'Fuldført' Hvis anmodningen er blevet forkyndt lykkes.<br /><br />Fejltypen i enkelte anførselstegn, hvis anmodningen mislykkedes.|'Succes'|
|Korrelations-id|Tekst|GUID, der er fælles mellem RMS-klienten log og serverloggen for en given anmodning.<br /><br />Denne værdi kan være nyttige i forbindelse med fejlfinding af problemer med klienten.|cab52088-8925-4371-be34-4b71a3112356|
|indhold-id|Tekst|GUID, omsluttet af klammeparenteser, der identificerer det beskyttede indhold (eksempelvis et dokument).<br /><br />Dette felt indeholder en værdi, hvis anmodningen type er AcquireLicense og er tom for alle andre anmodningstyper af.|{bb4af47b-cfed-4719-831d-71b98191a4f2}|
|e-mail-ejer|Streng|E-mail-adresse for ejeren af dokumentet.|Alice@Contoso.com|
|udstederen|Streng|E-mail-adresse til udstederen af dokumentet.|Alice@Contoso.com (eller) FederatedEmail.4c1f4d-93bf-00a95fa1e042@contoso.onmicrosoft.com'|
|Skabelon-id|Streng|ID for den skabelon, der bruges til at beskytte dokumentet.|{6d9371a6-4e2d-4e97-9a38-202233fed26e}|
|Filnavn|Streng|Filnavnet på det dokument, der er beskyttet.|TopSecretDocument.docx|
|Udgivelsesdato|Dato|Den dato, hvor dokumentet er beskyttet.|2015-10-15T21:37:00|
|c-info|Streng|Oplysninger om klient-platform, der fremsat anmodningen.<br /><br />En bestemt streng, varierer, afhængigt af programmet (f.eks. operativsystemet eller browseren).|' MSIPC, version = 1.0.623.47; Programnavn = WINWORD. EXE; AppVersion = 15.0.4753.1000; AppArch = x 86 OSName = Windows; OSVersion = 6.1.7601; OSArch = amd64'|
|c-ip|Adresse|IP-adressen på den klient, der sender anmodningen.|64.51.202.144|

#### Undtagelser for feltet bruger-id
Selvom feltet bruger-id Angiver som regel den bruger, der har fremsat anmodningen, er der to undtagelser hvor værdien ikke knyttes til en ægte bruger:

-   Værdien **' microsoftrmsonline @-&lt; YourTenantID &gt;. &lt; region &gt; rms.. aadrm.com'**.

    Dette angiver en Office 365-tjeneste, som Exchange Online og Sharepoint Online, opretter anmodningen. I strengen, *&lt; YourTenantID &gt;* er GUID'ET til din lejer og *&lt; region &gt;* er det område, hvor din lejer er registreret. For eksempel **na** repræsenterer Nordamerika, **eu** repræsenterer Europa, og **ap** repræsenterer Asien.

-   Hvis du bruger RMS-stik.

    Anmodninger fra denne forbindelse er logget med tjenestens hovednavn, RMS genereres automatisk, når du installerer en RMS-stik.

#### Typiske anmodningstyper
Der er mange anmodningstyper af til Azure Rights Management, men i følgende tabel beskrives nogle af de mest typisk anvendte anmodningstyper.

|Anmodningstypen|Beskrivelse|
|-------------------|---------------|
|AcquireLicense|en klient fra en Windows-baseret computer, der anmoder om en licens til RMS-beskyttet indhold.|
|AcquirePreLicense|en klient på vegne af brugeren anmoder om en licens til RMS-beskyttet indhold.|
|AcquireTemplates|blev foretaget et kald til erhverver skabeloner, der er baseret på skabelonen id'er|
|AcquireTemplateInformation|blev foretaget et kald til at få id på skabelonen fra tjenesten.|
|AddTemplate|er foretaget et kald fra Azure portal til at tilføje en skabelon.|
|BECreateEndUserLicenseV1|er foretaget et kald fra en mobil enhed til at oprette en slutbrugerlicensaftale.|
|BEGetAllTemplatesV1|er foretaget et kald fra en mobil enhed (backend) til at få alle skabeloner.|
|Certificer|klienten bekræfter indholdet af beskyttelsen.|
|Dekryptere|klienten forsøger at dekryptere RMS-beskyttet indhold.|
|DeleteTemplateById|er foretaget et kald fra Azure portal til at slette en skabelon som skabelon-ID.|
|ExportTemplateById|er foretaget et kald fra Azure portal til at eksportere en skabelon, der er baseret på en skabelon-id|
|FECreateEndUserLicenseV1|magen til AcquireLicense anmodningen, men fra mobilenheder.|
|FECreatePublishingLicenseV1|det samme som Certificer og GetClientLicensorCert kombineres, fra mobile klienter.|
|FEGetAllTemplates|der foretages et kald, fra en mobil enhed (front) til at hente skabelonerne.|
|GetAllTemplates|er foretaget et kald fra Azure portal til at få alle skabeloner.|
|GetClientLicensorCert|klienten anmoder om en udgivelse certifikat (der bruges senere til at beskytte indhold) fra en Windows-baseret computer.|
|GetConfiguration|en Azure PowerShell cmdlet kaldes for at få konfigurationen af Azure RMS forpagteren.|
|GetConnectorAuthorizations|er foretaget et kald fra RMS-forbindelser til at få deres konfiguration fra skyen.|
|GetTenantFunctionalState|af Azure portal kontrollerer, om Azure RMS aktiveres.|
|GetTemplateById|er foretaget et kald fra Azure portal til at hente en skabelon ved at angive en skabelon-id|
|ExportTemplateById|en opkaldet foretages fra Azure portal til at eksportere en skabelon ved at angive en skabelon-id|
|FindServiceLocationsForUser|er foretaget et kald til at forespørge om URL-adresser, som bruges til at kalde Certificer eller AcquireLicense.|
|ImportTemplate|er foretaget et kald fra Azure portal til at importere en skabelon.|
|ServerCertify|er foretaget et kald fra en RMS-aktiverede klient (f.eks SharePoint) at certificere serveren.|
|SetUsageLogFeatureState|er foretaget et kald til Aktiver logføringen af statistikoplysninger.|
|SetUsageLogStorageAccount|er foretaget et kald til at angive placeringen af logfilerne Azure RMS.|
|SignDigest|er foretaget et kald, når en nøgle, der bruges til signering formål. Dette kaldes normalt en gang pr. AcquireLicence (eller FECreateEndUserLicenseV1), Certificer, og GetClientLicensorCert (eller FECreatePublishingLicenseV1).|
|UpdateTemplate|er foretaget et kald fra Azure portal til at opdatere en eksisterende skabelon.|

## <a name="BKMK_PowerShell"></a>Windows PowerShell-reference
Brug følgende Windows PowerShell-cmdletter til at hjælpe dig med at konfigurere og bruge Azure Rights Management Besøgslogføringen:

-   [Deaktiver AadrmUsageLogFeature](https://msdn.microsoft.com/library/azure/dn629404.aspx)

-   [Aktiver AadrmUsageLogFeature](https://msdn.microsoft.com/library/azure/dn629421.aspx)

-   [Get-AadrmUsageLog](https://msdn.microsoft.com/library/azure/dn629401.aspx)

-   [Get-AadrmUsageLogFeature](https://msdn.microsoft.com/library/azure/dn629425.aspx)

-   [Get-AadrmUsageLogLastCounterValue](https://msdn.microsoft.com/library/azure/dn629423.aspx)

-   [Get-AadrmUsageLogStorageAccount](https://msdn.microsoft.com/library/azure/dn629419.aspx)

-   [Sæt AadrmUsageLogStorageAccount](https://msdn.microsoft.com/library/azure/dn629426.aspx)

Yderligere oplysninger om at bruge Windows PowerShell til Azure Rights Management, se [Administration af Azure rettighedsstyring ved hjælp af Windows PowerShell](../Topic/Administering_Azure_Rights_Management_by_Using_Windows_PowerShell.md).

## Se også
[Ved hjælp af Azure rettighedsstyring](../Topic/Using_Azure_Rights_Management.md)

