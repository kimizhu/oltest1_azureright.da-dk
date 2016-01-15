---
description: na
keywords: na
title: Configuring Custom Templates for Azure Rights Management
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1775d8d0-9a59-42c8-914f-ce285b71ac1c
---
# Konfiguration af brugerdefinerede skabeloner til Azure rettighedsstyring
Når du har aktiveret Azure Rights Management (Azure RMS), kan brugerne automatisk at bruge to standardskabeloner, der gør det nemt for dem at anvende politikker til følsomme filer, der begrænser adgangen til autoriserede brugere i organisationen. Disse to skabeloner har følgende rettigheder politikbegrænsninger:

-   Skrivebeskyttet visning til beskyttet indhold

    -   Navn: **&lt; Organisationsnavn &gt; - fortrolige Vis kun**

    -   Særlig tilladelse: Vis indhold

-   Læse eller ændre tilladelser for det beskyttede indhold

    -   Navn: **&lt; Organisationsnavn &gt; - fortrolige**

    -   Specifikke tilladelser: Få vist indhold, gemme filen, redigere indhold, få vist tildelte rettigheder, tillade makroer, fremad, svar, svar til alle

Desuden den [RMS deling program](http://technet.microsoft.com/library/dn339006.aspx) gør det muligt for brugere at definere deres egne sæt tilladelser. Og for Outlook-klienten og Outlook Web Access, brugerne kan vælge de **Videresend ikke** indstilling for e-mail-meddelelser.

For mange organisationer være standardskabelonerne tilstrækkeligt. Men hvis du vil oprette dine egne brugerdefinerede rettigheder politikskabeloner, kan du gøre det på. Hvorfor oprette en brugerdefineret skabelon, omfatter følgende:

-   Ønsker du en skabelon til at tildele rettigheder til et undersæt af brugere i organisationen i stedet for alle brugere.

-   Du vil kun et undersæt af brugere skal kunne se og vælge en skabelon (skabelon afdelings) fra programmer i stedet for alle brugere i organisationen se, og du kan vælge skabelonen.

-   Du vil definere en brugerdefineret lige efter en skabelon, få vist og Rediger, men ikke kopiere og udskrive.

-   Du vil konfigurere yderligere indstillinger i en skabelon, der omfatter en udløbsdato, og om indholdet kan opnås uden en internetforbindelse.

For brugerne at kunne vælge en brugerdefineret skabelon, der indeholder indstillinger, som disse, skal du først oprette en brugerdefineret skabelon, konfigurerer den og derefter udgive den.

Brug følgende afsnit til at hjælpe dig med at konfigurere og bruge brugerdefinerede skabeloner:

-   [Hvordan du kan oprette, konfigurere og udgive en brugerdefineret skabelon](../Topic/Configuring_Custom_Templates_for_Azure_Rights_Management.md#BKMK_HowToConfigureCustomTemplates)

-   [Sådan kopieres en skabelon](../Topic/Configuring_Custom_Templates_for_Azure_Rights_Management.md#BKMK_HowToCopyTemplates)

-   [Sådan fjernes skabeloner (arkiv)](../Topic/Configuring_Custom_Templates_for_Azure_Rights_Management.md#BKMK_HowToArchiveTemplates)

-   [Opdatering af skabeloner til brugere](../Topic/Configuring_Custom_Templates_for_Azure_Rights_Management.md#BKMK_RefreshingTemplates)

-   [Windows PowerShell-reference](../Topic/Configuring_Custom_Templates_for_Azure_Rights_Management.md#BKMK_PowerShellTemplates)

## <a name="BKMK_HowToConfigureCustomTemplates"></a>Hvordan du kan oprette, konfigurere og udgive en brugerdefineret skabelon
Du Opret og administrer brugerdefinerede skabeloner i Azure Management Portal. Du kan gøre dette direkte fra Azure Management portalen, eller du kan logge på Office 365 admin center, og vælg den **Avancerede funktioner** til Rights Management, som derefter bliver omdirigeret til portalen Azure Management.

Brug følgende procedurer til at oprette, konfigurere og udgive brugerdefinerede skabeloner til Rights Management.

#### Oprette en brugerdefineret skabelon

1.  Afhængigt af om du logger på Office 365 admin center eller Azure portalen, du gør et af følgende:

    -   Fra den [Office 365 admin center](https://portal.office.com/):

        1.  Klik på i venstre rude, **tjenesteindstillingerne**.

        2.  Fra den **tjenesteindstillingerne** skal du klikke på **rights management**.

        3.  I den **beskytter dine oplysninger** skal du klikke på **Manage**.

        4.  I den **rettighedsstyring** skal du klikke på **Avancerede funktioner til**.

            > [!NOTE]
            > Hvis du ikke har aktiveret Rights Management, skal du først klikke på **aktivere** og bekræfte handlingen. Yderligere oplysninger finder du under [Aktivering af Azure rettighedsstyring](../Topic/Activating_Azure_Rights_Management.md).
            > 
            > Hvis du ikke har klikket på **Avancerede funktioner** før, når Rights Management er aktiveret, skal du følge den på skærmen instruktioner til at få et gratis abonnement til Azure, der kræves for at få adgang til portalen Azure.

            Hvis du klikker på **Avancerede funktioner** indlæses i Azure portal, hvor du kan administrere **RIGHTS MANAGEMENT** for organisationens Azure Active Directory.

    -   Fra den [Azure Portal](http://go.microsoft.com/fwlink/p/?LinkID=275081):

        1.  Klik på i venstre rude, **ACTIVE DIRECTORY**.

        2.  Fra den **active directory** skal du klikke på **RIGHTS MANAGEMENT**.

        3.  Vælg mappen til at administrere for Rights Management.

        4.  Hvis du ikke allerede har aktiveret Rights Management, skal du klikke på **Aktiver** og bekræfte handlingen.

            > [!NOTE]
            > Yderligere oplysninger finder du under [Aktivering af Azure rettighedsstyring](../Topic/Activating_Azure_Rights_Management.md).

2.  Opret en ny skabelon:

    -   På portalen Azure fra den **komme i gang med Rights Management** Hurtig start side, klik på **opretter en ny skabelon til rettigheder politik**.

        Hvis du ikke se denne side efter at følge vejledningen for Office 365 straks, kan du bruge navigation i vejledningen ovenfor, til portalen Azure.

3.  På den **tilføjer en ny skabelon til rettigheder politik** skal du vælge et sprog, hvor du vil skrive skabelonens navn og beskrivelse, som brugere får vist (du kan føje flere sprog til senere). Derefter skrive et entydigt navn og en beskrivelse, og klik på knappen færdig.

Fra den **komme i gang med Rights Management** Hurtig start side, klik på **administrere dine rettigheder politikskabeloner**. Kan du se den nyoprettede skabelon føjes til listen over skabeloner med statussen **arkiveret**. På dette stadium skabelonen er oprettet, men ikke er konfigureret, og er ikke synlige for brugerne.

#### Til at konfigurere og udgive en brugerdefineret skabelon

1.  Vælg den netop oprettede skabelon fra den **skabeloner** side i portalen Azure Management.

2.  Fra den **skabelonen er blevet tilføjet** Hurtig start side, klik på **Introduktion** fra trin 1, **konfigurere rettigheder for brugere og grupper,** klik derefter på **Kom i gang nu** eller **tilføje**, og vælg derefter de brugere og grupper der har rettigheder til at bruge det indhold, der er beskyttet af den nye skabelon.

    > [!NOTE]
    > De brugere eller grupper, som du vælger, skal have en e-mail-adresse. Dette vil næsten altid være tilfældet, men i en simpel testmiljø, du muligvis tilføje e-mail-adresser til brugerkonti eller grupper i et produktionsmiljø.

    En vane at bruge grupper i stedet for brugerne, hvilket forenkler administrationen af skabelonerne. Hvis du har Active Directory på stedet og synkroniserer til Azure AD, kan du bruge e-mail-aktiverede grupper, der enten sikkerhedsgrupper eller distributionsgrupper. Men hvis du vil tildele rettigheder til alle brugere i organisationen, det bliver mere effektivt at kopiere en af standardskabelonerne i stedet for at angive flere grupper. Yderligere oplysninger finder du i [Sådan kopieres en skabelon](../Topic/Configuring_Custom_Templates_for_Azure_Rights_Management.md#BKMK_HowToCopyTemplates) afsnit i dette emne.

    > [!TIP]
    > Du kan senere tilføje brugere uden for din organisation til skabelonen ved hjælp af den [Windows PowerShell-modul til Azure Rights Management](https://technet.microsoft.com/library/jj585012.aspx) og bruge en af følgende metoder:
    > 
    > -   **Eksport, redigering og import den opdaterede skabelon**:  Dette er den nemmeste metode til at føje eksterne brugere til en eksisterende skabelon, der indeholder andre grupper. Brug af [eksport-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727078.aspx) -cmdlet til Eksporter skabelon til en. Csv-fil, du kan redigere for at tilføje eksterne e-mail-adresserne for disse brugere og deres rettigheder til de eksisterende grupper og rettigheder. Brug derefter de [Import-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727077.aspx) -cmdlet til import af denne ændring tilbage til Azure RMS.
    > -   **Bruge et objekt til definition af rettigheder til at opdatere en skabelon**:    Angiv de eksterne e-mail-adresser og deres rettigheder i et rettigheder definition objekt, som du derefter kan bruge til at opdatere din skabelon. Du angive rettigheder definition-objekt ved hjælp af den [Ny AadrmRightsDefinition](https://msdn.microsoft.com/library/azure/dn727080.aspx) -cmdlet til at oprette en variabel og derefter oplyse denne variabel til parameteren - RightsDefinition med den [sæt AadrmTemplateProperty](https://msdn.microsoft.com/library/azure/dn727076.aspx) -cmdlet til at ændre en eksisterende skabelon. Men hvis du tilføjer disse brugere til en eksisterende skabelon, skal du også definere rettigheder definition objekter til de eksisterende grupper i skabelonerne og ikke kun de nye, eksterne brugere.

3.  Klik på knappen Næste, og Tildel derefter en af de anførte rettigheder til valgte brugere og grupper.

    Bruge det viste beskrivelse yderligere oplysninger om hver rettighed (og brugerdefinerede rettigheder). Yderligere oplysninger findes også i [Konfigurere rettigheder for Azure rettighedsstyring](../Topic/Configuring_Usage_Rights_for_Azure_Rights_Management.md). Programmer, der understøtter RMS kan dog variere i hvordan de kan implementere disse rettigheder. Deres dokumentationen og gøre dine egne test med de programmer, som brugerne kan bruge til at kontrollere funktionsmåden, før du anvender skabelonen til brugere. For at gøre denne skabelon, der er synlig for kun administratorer til denne test, gør denne skabelon en afdelings skabelon (trin 6).

4.  Hvis du har valgt **brugerdefinerede**, skal du klikke på knappen Næste, og vælg derefter de brugerdefinerede rettigheder.

    Selvom du kan bruge enhver kombination af de individuelle rettigheder, der er tilgængelig i nogle programmer, kan visse rettigheder have afhængigheder til andre individuelle rettigheder. Når dette er tilfældet, vælges automatisk de afhængige rettigheder for dig.

    > [!TIP]
    > Overvej at tilføje den **kopiere og udtrække indhold** til højre, og giv det valgte administratorer og personale i andre roller, der har ansvaret for gendannelse af data. Tildele denne rettighed kan dem fjerne beskyttelse, hvis det er nødvendigt, fra filer og e-mails, der beskyttes ved hjælp af denne skabelon. Denne mulighed for at fjerne beskyttelsen på niveauet skabelon indeholder flere detaljerede kontrolelement end ved hjælp af funktionen superbruger.

5.  Klik på knappen færdig.

6.  Hvis du vil skabelon skal være synlige for kun et undersæt af brugere, når de ser en liste over skabeloner i programmer: Klik på **område** konfigurere dette som en afdelings skabelon, og klik på **Kom i gang nu**. Ellers skal du gå til trin 9.

    Yderligere oplysninger om afdelings skabeloner: Alle brugere i mappen Azure se alle de skabeloner, der er udgivet som standard, og de kan derefter vælge dem fra programmer, når de ønsker at beskytte indhold. Hvis du ønsker specifikke brugere kun kan se nogle af de skabeloner, der er udgivet, skal du område skabeloner for disse brugere. Derefter kunne kun disse brugere vælge disse skabeloner. Andre brugere, der ikke angiver se ikke skabelonerne og derfor ikke kan vælge dem. Denne teknik kan gøre for at vælge den rigtige skabelon lettere for brugerne, især når du opretter skabeloner, der er designet til at blive brugt af bestemte grupper eller afdelinger. Brugere kan derefter se kun de skabeloner, der er designet til dem.

    For eksempel, har du oprettet en skabelon til personaleafdelingen, der gælder den skrivebeskyttet tilladelse til medlemmer af regnskabsafdelingen. Så kun medlemmer af personaleafdelingen kan anvende denne skabelon, når de bruger rettighedsstyring, der deler programmet, omfanget af skabelonen til den e-mail-aktiveret gruppe kaldet efterslæb. Derefter anvende kun medlemmer af denne gruppe se og kan denne skabelon.

7.  På den **synlighed skabelon** skal du markere de brugere og grupper, der vil kunne se og vælge skabelonen fra RMS-enlightened-programmer. Som skal før, en vane, Brug grupper i stedet for brugere, og de grupper eller brugere, der vælger du have en e-mail-adresse.

8.  Klik på knappen Næste, og beslutte, om du vil konfigurere programkompatibilitet for din afdelings skabelon. Hvis du gør det, skal du klikke på **PROGRAMKOMPATIBILITET**, markere afkrydsningsfeltet og klikke på **komplet**.

    Hvorfor du skal muligvis konfigurere programkompatibilitet? Ikke alle programmer kan understøtte afdelings skabeloner. For at gøre dette, skal programmet først godkende med tjenesten RMS før hentning af skabelonerne. Hvis godkendelsesprocessen ikke opstår som standard hentes ingen af afdelings skabeloner. Du kan tilsidesætte denne funktionsmåde ved at angive, at alle afdelinger skabeloner skal hente, ved konfiguration af programkompatibilitet og vælge den **Vis denne skabelon til alle brugere, når programmerne, der ikke understøtter brugeridentitet** afkrydsningsfelt.

    For eksempel hvis du ikke konfigurerer programkompatibilitet for skabelonen afdelinger i eksemplet personale, se kun brugere i personaleafdelingen skabelonen afdelings når de bruger programmet RMS deling, men ingen brugere se skabelonen afdelinger, når de bruger Outlook Web Access (OWA) fra Exchange Server 2013 Exchange OWA og Exchange ActiveSync i øjeblikket understøtter ikke afdelings skabeloner. Hvis du tilsidesætter standardindstillingen ved at konfigurere programkompatibilitet, se kun brugere i personaleafdelingen afdelings skabelonen, når de bruger RMS Deling af programmet, men alle brugere se skabelonen afdelinger, når de bruger Outlook Web Access (OWA). Hvis brugerne bruge OWA- eller Exchange ActiveSync i Exchange Online, enten alle brugere ser afdelings skabeloner eller ingen brugere vil se afdeling-skabeloner, der er baseret på skabelon-status (arkivering eller udgivne) i Exchange Online.

    > [!NOTE]
    > Hvis du har programmer, der ikke endnu har indbygget understøttelse af afdelings skabeloner, kan du bruge en [brugerdefineret RMS-skabelon download script](http://go.microsoft.com/fwlink/?LinkId=524506) eller andre værktøjer til at installere disse skabeloner i mappen lokale RMS-klienten. Disse programmer vises derefter korrekt afdelings skabeloner til brugere og grupper, du har valgt for området skabelon:
    > 
    > -   Office 2010 klientmappen er **%localappdata%\Microsoft\DRM\Templates**.
    > -   Fra en klientcomputer, som har hentet alle skabelonerne, kan du kopiere og derefter indsætte skabelonfiler til andre computere.
    > 
    > 2016 Office understøtter indbygget afdelings skabeloner, og det gør Office 2013 med de seneste opdateringer ([KB 3054853](https://support.microsoft.com/kb/3054853)).

9. Klik på **KONFIGURER** og tilføje flere sprog, som brugere anvender, samt navn og beskrivelse af denne skabelon på det pågældende sprog. Når du har flere sprog brugere, er det vigtigt at tilføje de enkelte sprog, som de bruger og angive et navn og beskrivelse på det pågældende sprog. Brugere får derefter vist navn og beskrivelse af skabelonen på samme sprog som deres klient-operativsystem, der sikrer, at de forstår, at den politik, der anvendes til et dokument eller en e-mail-meddelelse. Hvis der er nogen, som passer til deres klientoperativsystem, går navn og beskrivelse, der kan de se tilbage til det sprog og den beskrivelse, du har angivet, når du først har oprettet skabelonen.

    Kontroller derefter, om du vil foretage ændringer af følgende indstillinger:

    |Indstilling|Yderligere oplysninger|
    |---------------|--------------------------|
    |**udløb af indhold**|Definere en dato eller et antal dage til denne skabelon, når du ikke skal åbne filer, der er beskyttet af skabelonen. Du kan angive en dato, eller du kan angive et antal dage fra det tidspunkt, beskyttelsen, der anvendes til filen.<br /><br />Når du angiver en dato, er effektiv midnat i den aktuelle tidszone.|
    |**offlineadgang**|Brug denne indstilling til at afstemme de sikkerhedskrav, der er, at du har mod de krav, som brugerne skal kunne åbne beskyttede filer når de ikke har en internetforbindelse.<br /><br />Hvis du angiver, at indholdet er ikke tilgængelig uden en internetforbindelse eller indhold er kun tilgængelig for et angivet antal dage, når denne grænse er nået, brugere skal være godkendt igen og deres adgang logføres. Når dette sker, hvis deres legitimationsoplysninger ikke er gemt i cachen, bliver brugerne bedt om at logge på, før de kan åbne filen.<br /><br />Ud over godkendelse igen er politikken og brugergruppemedlemskab evalueres igen. Det betyder, at brugere kan forvente andet resultater for den samme fil, hvis der er ændringer i medlemskabet politik eller en gruppe fra hvornår de sidst har åbnet filen.|

10. Når du er sikker på, at skabelonen er konfigureret korrekt til brugerne, skal du klikke på **Udgiv** gøre skabelonen synlige for brugere, og klik derefter på **Gem**.

11. Klik på knappen tilbage på portalen Management for at vende tilbage til den **skabeloner** side, hvor skabelonen nu har en opdateret status for **udgivet**.

Hvis du vil foretage ændringer i din skabelon, markere den og derefter bruge start hurtigt trin igen. Eller Vælg en af følgende indstillinger:

-   At tilføje flere brugere og grupper og definere rettigheder for disse brugere og grupper: Klik på **rettigheder**, og klik derefter på **tilføje**.

-   Fjerne brugere eller grupper, som du tidligere har valgt: Klik på **rettigheder**, Vælg den bruger eller gruppe på listen, og klik derefter på **slette**.

-   Ændre, hvilke brugere der kan se skabeloner at vælge dem fra programmer: Klik på **område**, og klik derefter på **tilføje** eller **slette**, eller **PROGRAMKOMPATIBILITET**.

-   At gøre skabelonen ikke længere synlige for alle brugere: Klik på **KONFIGURER**, skal du klikke på **arkiv**, og klik derefter på **Gem**.

-   Til at foretage andre konfigurationsændringer: Klik på **KONFIGURER**, foretag ændringerne, og klik derefter på **Gem**.

> [!WARNING]
> Når du foretager ændringer i en skabelon, der tidligere blev gemt, kan klienter ikke se disse ændringer til skabelonen indtil skabeloner er opdateret på deres computere. Yderligere oplysninger finder du i [Opdatering af skabeloner til brugere](../Topic/Configuring_Custom_Templates_for_Azure_Rights_Management.md#BKMK_RefreshingTemplates) afsnit i dette emne.

## <a name="BKMK_HowToCopyTemplates"></a>Sådan kopieres en skabelon
Hvis du vil oprette en ny skabelon, der er meget lignende indstillinger til en eksisterende skabelon, skal du vælge den oprindelige skabelon på den **skabeloner** skal du klikke på **kopi**, kan du angive et entydigt navn og foretage de ændringer, du har brug for.

> [!IMPORTANT]
> Når du kopierer en skabelon til **udgivet** eller **arkiveret** status kopieres også. Så hvis du kopierer et udgivet skabelon, øjeblikkelig status bliver offentliggjort, medmindre du ændrer den.

Du kan kopiere brugerdefinerede skabeloner og standardskabelonerne. En vane at kopiere en af standardskabelonerne i stedet for at oprette en ny brugerdefineret skabelon, hvis du vil skabelon til at tildele rettigheder til alle brugere i organisationen. Denne metode betyder, at du ikke behøver at oprette eller vælge flere grupper til at angive alle brugere. I dette scenario, Sørg for at angive et nyt navn og en beskrivelse af kopierede skabelonen til flere sprog.

## <a name="BKMK_HowToArchiveTemplates"></a>Sådan fjernes skabeloner (arkiv)
Standardskabeloner kan ikke slettes, men de kan arkiveres, så brugere ikke får dem.

På samme måde, hvis du har udgivet en brugerdefineret skabelon, og du ikke længere ønsker, at brugerne skal kunne se det, kan du redigere skabelonen og vælge **arkiv** og **Gem** fra den **KONFIGURER** side. Eller du kan vælge det fra den **skabeloner** side, og vælg **arkiv**.

Da du ikke kan redigere standardskabelonerne, hvis du vil arkivere disse skabeloner, skal du bruge den **arkiv** indstilling fra den **skabeloner** side. Du kan arkivere Outlook **Videresend ikke** indstilling.

#### Fjerne en standardskabelon

-   Fra den **skabeloner** side, Vælg standardskabelonen, og på **arkiv**.

Status ændres fra **udgivet** til **arkiveret**. Hvis du ændrer mening, Vælg skabelonen, og klik på **Udgiv**.

## <a name="BKMK_RefreshingTemplates"></a>Opdatering af skabeloner til brugere
Når du bruger Azure RMS, hentes skabeloner automatisk til klientcomputere, så brugerne kan vælge dem fra deres programmer. Du skal dog tage yderligere trin, hvis du ændrer skabelonerne:

|Programmet eller tjenesten|Hvordan skabeloner opdateres efter ændringer|
|------------------------------|------------------------------------------------|
|Exchange Online|Manuel konfiguration, der kræves for at opdatere skabeloner.<br /><br />Udvid afsnittet nedenfor for konfigurationstrin, [Exchange Online kun: Sådan konfigureres Exchange for at hente ændres brugerdefinerede skabeloner](../Topic/Configuring_Custom_Templates_for_Azure_Rights_Management.md#BKMK_ExchangeOnlineTemplatesUpdate).|
|Office 365|Automatisk opdateret – ingen yderligere trin påkrævet.|
|2016 Office og Office-2013<br /><br />Deling af programmer til Windows RMS|Automatisk opdateret – på en plan:<br /><br />-   For disse nyere versioner af Office: Opdateringsintervallet standard er hver syvende dag.<br />-   Til deling af programmer til Windows RMS: Fra og med version 1.0.1784.0, er standard opdateringsintervallet hver 1 dag. Tidligere versioner er standard opdateringsinterval for hver syvende dag.<br /><br />At tvinge en opdatering, før denne tidsplan, Udvid afsnittet nedenfor [2016 Office, Office 2013 og deling ansøgning om Windows RMS: Sådan tvinges en opdatering for en brugerdefineret skabelon, der ændrede](#BKMK_Office2013ForceUpdate).|
|Office 2010|Opdateres, når brugere logger på.<br /><br />Hvis du vil gennemtvinge en opdatering, spørge eller tvinge brugere til at logge af og logge på igen igen. Eller se det efterfølgende afsnit [Kun Office 2010: Sådan tvinges en opdatering for en brugerdefineret skabelon, der ændrede](#BKMK_Office2010ForceUpdate).|
Til mobile enheder, der bruger Deling af programmet RMS skabeloner automatisk hentes (og opdateres, hvis det er nødvendigt) uden yderligere konfiguration, der kræves.

### <a name="BKMK_ExchangeOnlineTemplatesUpdate"></a>Exchange Online kun: Sådan konfigureres Exchange for at hente ændres brugerdefinerede skabeloner
Hvis du allerede har konfigureret Management IRM (Information Rights) til Exchange Online, Hent brugerdefinerede skabeloner ikke for brugere, før du kan foretage følgende ændringer ved hjælp af Windows PowerShell i Exchange Online.

> [!NOTE]
> Finde flere oplysninger om, hvordan du bruger Windows PowerShell i Exchange Online, [ved hjælp af PowerShell med Exchange Online](https://technet.microsoft.com/library/jj200677%28v=exchg.160%29.aspx).

Du skal følge denne fremgangsmåde, hver gang du ændrer en skabelon.

##### For at opdatere skabeloner for Exchange Online

1.  Hvis du bruger Windows PowerShell i Exchange Online, oprette forbindelse til tjenesten:

    1.  Angiv din Office 365-brugernavn og adgangskode:

        ```
        $Cred = Get-Credential
        ```

    2.  Opret forbindelse til Exchange Online-tjenesten ved at køre følgende to kommandoer:

        ```
        $Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri https://ps.outlook.com/powershell/ -Credential $Cred -Authentication Basic –AllowRedirection
        ```

        ```
        Import-PSSession $Session
        ```

2.  Brug af [Import-RMSTrustedPublishingDomain](http://technet.microsoft.com/library/jj200724%28v=exchg.160%29.aspx) -cmdlet til at importere dine publicerer tillidsdomænet (TPD) fra Azure RMS igen:

    ```
    Import-RMSTrustedPublishingDomain -Name "<TPD name>" -RefreshTemplates -RMSOnline
    ```
    For eksempel, hvis dit navn TPD **Online RMS - 1** (en typisk navn for mange organisationer), Angiv: **Import-RMSTrustedPublishingDomain -Name "RMS Online - 1" -RefreshTemplates -RMSOnline**

    > [!NOTE]
    > Du kan kontrollere din TPD navn, du kan bruge den [få RMSTrustedPublishingDomain](http://technet.microsoft.com/library/jj200707%28v=exchg.160%29.aspx) cmdlet.

3.  Vent et par minutter for at bekræfte, at skabelonerne er importeret, og derefter køre den [Get-RMSTemplate](http://technet.microsoft.com/library/dd297960%28v=exchg.160%29.aspx) cmdlet og angive typen til alle. For eksempel:

    ```
    Get-RMSTemplate -TrustedPublishingDomain "RMS Online - 1" -Type All
    ```
    > [!TIP]
    > Det er praktisk at opbevare en kopi af output, så du kan let kopiere navne eller GUID'er Hvis du arkiverer en skabelon senere.

4.  For hver importerede skabelon, der skal være tilgængelige i Outlook Web App, skal du bruge den [Set-RMSTemplate](http://technet.microsoft.com/library/hh529923%28v=exchg.160%29.aspx) cmdlet og angive typen til fordelt:

    ```
    Set-RMSTemplate -Identity "<name  or GUID of the template>" -Type Distributed
    ```
    Fordi Outlook Web Access gemmer Brugergrænsefladen i 24 timer, kan brugerne ikke se den nye skabelon til op til en dag.

Derudover, hvis du arkiverer en skabelon (brugerdefineret eller standard) og bruge Exchange Online med Office 365, brugerne fortsætter med at se de arkiverede skabeloner, hvis de bruger Outlook Web App eller mobile enheder, der bruger Exchange ActiveSync-protokollen.

Så brugere ikke længere se disse skabeloner, oprette forbindelse til tjenesten ved hjælp af Windows PowerShell i Exchange Online og derefter bruge den [Set-RMSTemplate](http://technet.microsoft.com/library/hh529923%28v=exchg.160%29.aspx) cmdlet ved at køre følgende kommando:

```
Set-RMSTemplate -Identity "<name or GUID of the template>" -Type Archived
```

### <a name="BKMK_Office2013ForceUpdate"></a>2016 Office, Office 2013 og deling ansøgning om Windows RMS: Sådan tvinges en opdatering for en brugerdefineret skabelon, der ændrede
Du kan ændre den tidsplan for automatisk ved at redigere registreringsdatabasen på de computere, der kører Office 2016, Office 2013 eller Rights Management (RMS) deling program til Windows, så de ændrede skabeloner opdateres hyppigere end standardværdien på computere. Du kan også tvinge en øjeblikkelig opdatering ved at slette de eksisterende data i en værdi i registreringsdatabasen.

> [!WARNING]
> Hvis du bruger Registreringseditor forkert, kan det forårsage alvorlige problemer, der kræver, at du skal geninstallere operativsystemet. Microsoft kan ikke garantere, at problemer, der skyldes forkert brug af Registreringseditor, kan løses. Du kan bruge Registreringseditor på egen risiko.

##### Sådan ændres automatiske tidsplanen

1.  En Registreringseditor til at oprette og angive en af følgende værdier i registreringsdatabasen:

    -   Angive en opdateringshyppighed dage (mindst 1 dag):  Oprette en ny værdi i registreringsdatabasen med navnet **TemplateUpdateFrequency** og definere heltalsværdien for de data, som angiver hyppigheden i dage til at hente eventuelle ændringer til en skabelon, der er hentet. Brug følgende tabel til at finde den sti til registreringsdatabasen for at oprette den nye registreringsdatabaseværdi.

        |Sti til registreringsdatabasen|Type|Værdi|
        |----------------------------------|--------|---------|
        |HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC|REG_DWORD|TemplateUpdateFrequency|

    -   Angive en opdateringshyppighed i sekunder (mindst 1 sekund):  Oprette en ny værdi i registreringsdatabasen med navnet **TemplateUpdateFrequencyInSeconds** og definere heltalsværdien for de data, der angiver hyppigheden i sekunder at overføre ændringer for hentede skabelon. Brug følgende tabel til at finde den sti til registreringsdatabasen for at oprette den nye registreringsdatabaseværdi.

        |Sti til registreringsdatabasen|Type|Værdi|
        |----------------------------------|--------|---------|
        |HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC|REG_DWORD|TemplateUpdateFrequencyInSeconds|

    Sørg for, at du opretter og angiver en af disse registreringsdatabaseværdier, ikke begge dele. Hvis begge er til stede, **TemplateUpdateFrequency** ignoreres.

2.  Hvis du vil gennemtvinge en øjeblikkelig opdatering af skabelonerne, kan du gå til den næste procedure. Ellers skal du genstarte din Office-programmer og forekomster af File Explorer nu.

##### At tvinge en øjeblikkelig opdatering

1.  Ved hjælp af Registreringseditor, slette data til den **LastUpdatedTime** værdi. For eksempel vises dataene måske **2015-04-20T15:52**; slette 2015-04-20T15:52, vises der ingen data. Brug følgende tabel til at finde den sti til registreringsdatabasen for at slette data på denne værdi i registreringsdatabasen.

    |Sti til registreringsdatabasen|Type|Værdi|
    |----------------------------------|--------|---------|
    |HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC\ &lt; MicrosoftRMS_FQDN &gt; \Template|REG_SZ|LastUpdatedTime|
    > [!TIP]
    > I i Registreringsdatabasestien *&lt; MicrosoftRMS_FQDN &gt;* henviser til tjenesten Microsoft RMS FQDN. Hvis du vil kontrollere denne værdi:
    > 
    > 1.  Kør den [få AadrmConfiguration](https://msdn.microsoft.com/library/windowsazure/dn629410.aspx) cmdlet til Azure RMS. Hvis du ikke allerede er installeret Windows PowerShell-modul til Azure RMS, se [Installation af Windows PowerShell til Azure rettighedsstyring](../Topic/Installing_Windows_PowerShell_for_Azure_Rights_Management.md).
    > 2.  Fra outputtet, identificere de **LicensingIntranetDistributionPointUrl** værdi.
    > 
    >     For eksempel: **LicensingIntranetDistributionPointUrl: https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com/_wmcs/licensing**
    > 3.  Fjerne fra værdien, **https://** og **/_wmcs/licens** fra denne streng. Værdien af det resterende er tjenesten Microsoft RMS FQDN. I eksemplet er tjenesten Microsoft RMS FQDN følgende værdi:
    > 
    >     **5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com**

2.  Vil du slette følgende mappe og alle filer, der indeholder: **%localappdata%\Microsoft\MSIPC\Templates**

3.  Genstart Office-programmer og forekomster af Filoversigt.

### <a name="BKMK_Office2010ForceUpdate"></a>Kun Office 2010: Sådan tvinges en opdatering for en brugerdefineret skabelon, der ændrede
Ved redigering af registreringsdatabasen på de computere, der kører Office 2010, kan du angive en værdi, så de ændrede skabeloner opdateres på computere uden at vente brugere logger af og på igen. Du kan også tvinge en øjeblikkelig opdatering ved at slette de eksisterende data i en værdi i registreringsdatabasen.

> [!WARNING]
> Hvis du bruger Registreringseditor forkert, kan det forårsage alvorlige problemer, der kræver, at du skal geninstallere operativsystemet. Microsoft kan ikke garantere, at problemer, der skyldes forkert brug af Registreringseditor, kan løses. Du kan bruge Registreringseditor på egen risiko.

##### Sådan ændres opdateringshyppigheden

1.  Ved hjælp af Registreringseditor, oprette en ny værdi i registreringsdatabasen med navnet **UpdateFrequency** og definere heltalsværdien for de data, som angiver hyppigheden i dage til at hente eventuelle ændringer til en skabelon, der er hentet. Brug følgende tabel til at finde den sti til registreringsdatabasen for at oprette den nye registreringsdatabaseværdi.

    |Sti til registreringsdatabasen|Type|Værdi|
    |----------------------------------|--------|---------|
    |HKEY_CURRENT_USER\Software\Microsoft\MSDRM\TemplateManagement|REG_DWORD|UpdateFrequency|

2.  Hvis du vil gennemtvinge en øjeblikkelig opdatering af skabelonerne, kan du gå til den næste procedure. Ellers skal du genstarte Office-programmerne nu.

##### At tvinge en øjeblikkelig opdatering

1.  Ved hjælp af Registreringseditor, slette data til den **LastUpdatedTime** værdi. For eksempel vises dataene måske **2015-04-20T15:52**; slette 2015-04-20T15:52, vises der ingen data. Brug følgende tabel til at finde den sti til registreringsdatabasen for at slette data på denne værdi i registreringsdatabasen.

    |Sti til registreringsdatabasen|Type|Værdi|
    |----------------------------------|--------|---------|
    |HKEY_CURRENT_USER\Software\Microsoft\MSDRM\TemplateManagement|REG_SZ|lastUpdatedTime|

2.  Vil du slette følgende mappe og alle filer, der indeholder: **%localappdata%\Microsoft\MSIPC\Templates**

3.  Genstart Office-programmerne.

## <a name="BKMK_PowerShellTemplates"></a>Windows PowerShell-reference
Alt, hvad du kan gøre i Azure Management Portal til at oprette og administrere skabeloner, du kan gøre fra kommandolinjen, ved hjælp af Windows PowerShell. Desuden kan du eksportere og importere skabeloner, så du kan kopiere skabeloner mellem lejere eller udføre bulk redigeringer af komplekse egenskaber i skabeloner, såsom flersprogede navne og beskrivelser.

Du kan også bruge eksport og import for at sikkerhedskopiere og gendanne dine brugerdefinerede skabeloner, som best practice, regelmæssigt sikkerhedskopiere dine brugerdefinerede skabeloner, så hvis du foretager en ændring, der ikke er beregnet, kan du nemt vende tilbage til en tidligere version.

> [!IMPORTANT]
> Hvis du vil bruge Windows PowerShell til at oprette og administrere Azure RMS rettigheder politikskabeloner, skal du mindst have version 2.0.0.0 af den [Windows PowerShell-modul til Azure RMS](http://go.microsoft.com/fwlink/?LinkId=257721).
> 
> Hvis du tidligere har installeret dette modul til Windows PowerShell, skal du køre følgende kommando i et vindue i PowerShell til at kontrollere versionsnummeret: `(Get-Module aadrm -ListAvailable).Version`

Installationsvejledning, se [Installation af Windows PowerShell til Azure rettighedsstyring](../Topic/Installing_Windows_PowerShell_for_Azure_Rights_Management.md).

Cmdlets, der understøtter oprettelse og administration af skabeloner:

-   [Tilføj AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727075.aspx)

-   [Eksport af AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727078.aspx)

-   [Get-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727079.aspx)

-   [Get-AadrmTemplateProperty](https://msdn.microsoft.com/library/azure/dn727081.aspx)

-   [Import af AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727077.aspx)

-   [Ny AadrmRightsDefinition](https://msdn.microsoft.com/library/azure/dn727080.aspx)

-   [Fjern AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727082.aspx)

-   [Sæt AadrmTemplateProperty](https://msdn.microsoft.com/library/azure/dn727076.aspx)

## Næste trin
Når du har konfigureret brugerdefinerede skabeloner til Azure Rights Management, bruge den [Køreplan for Azure Rights Management installation](../Topic/Azure_Rights_Management_Deployment_Roadmap.md) til at kontrollere, om der er andre konfigurationstrin, kan du gøre, før du kaster dig [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] til brugere og administratorer. Hvis der ikke er nogen andre konfigurationstrin, du skal gøre, se [Ved hjælp af Azure rettighedsstyring](../Topic/Using_Azure_Rights_Management.md) for operationelle retningslinjer til at understøtte en succesfuld implementering for organisationen.

## Se også
[Konfiguration af Azure rettighedsstyring](../Topic/Configuring_Azure_Rights_Management.md)

