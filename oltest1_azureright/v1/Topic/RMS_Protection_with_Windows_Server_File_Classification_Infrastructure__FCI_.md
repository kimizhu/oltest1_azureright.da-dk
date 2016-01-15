---
description: na
keywords: na
title: RMS Protection with Windows Server File Classification Infrastructure (FCI)
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9aa693db-9727-4284-9f64-867681e114c9
---
# RMS-beskyttelse med Windows Server fil klassificering infrastruktur (FCI)
Brug denne artikel for at få instruktioner og et script for at bruge klienten Rights Management (RMS) med værktøjet RMS beskyttelse til at konfigurere File Server Resource Manager og fil klassificering infrastruktur (FCI).

Denne løsning kan du beskytte automatisk alle filer i en mappe på en filserver, der kører Windows Server, eller automatisk beskytte filer, der opfylder bestemte kriterier. Eksempelvis filer, der er blevet klassificeret som med fortrolige eller følsomme oplysninger. Denne løsning bruger [Azure rettighedsstyring](../Topic/Azure_Rights_Management.md) (Azure RMS) til at beskytte filer, så du skal have denne teknologi, der er installeret i organisationen.

> [!NOTE]
> Selvom Azure RMS indeholder en [connector](https://technet.microsoft.com/library/dn375964.aspx) understøtter fil klassificering infrastruktur, at løsningen understøtter kun indbygget beskyttelse – eksempelvis Office-filer.
> 
> For at understøtte alle filtyper med filen klassificering infrastruktur, skal du bruge Windows PowerShell **RMS beskyttelse** modul, som beskrevet i denne artikel. RMS beskyttelse som Deling af programmet, RMS-cmdletter understøtter generiske beskyttelse samt indbygget beskyttelse, hvilket betyder, at alle filer, der kan beskyttes. Finde flere oplysninger om disse forskellige beskyttelse niveauer i [Niveauer af beskyttelse – oprindelig og generiske](../Topic/Rights_Management_sharing_application_administrator_guide.md#BKMK_LevelsofProtection) afsnit i den [Rights Management deling program administratorvejledningen](../Topic/Rights_Management_sharing_application_administrator_guide.md).

Følg vejledningen der for Windows Server 2012 R2 eller Windows Server 2012. Hvis du kører andre understøttede versioner af Windows, skal du tilpasse nogle af trinnene for forskelle i din version af operativsystemet og den, der er beskrevet i denne artikel.

## Forudsætninger for Azure RMS beskyttelse med Windows Server FCI
Forudsætninger for disse instruktioner:

-   På hver filserver, hvor du skal køre filen Resource Manager med filen klassificering infrastruktur:

    -   Du har installeret File Server Resource Manager som en af rolletjenester til rollen Filtjenester.

    -   Du har identificeret en lokal mappe, der indeholder filerne for at beskytte med Rights Management. C:\FileShare.

    -   Du har installeret værktøjet RMS beskyttelse, herunder forudsætninger for værktøjet (f.eks RMS-klienten) og Azure RMS (f.eks. den vigtigste tjenestekonto). Yderligere oplysninger finder du i [-cmdletter RMS-beskyttelse](https://msdn.microsoft.com/library/azure/mt433195.aspx).

    -   Hvis du vil ændre standardniveauet for RMS-beskyttelse (Oprindelig eller generisk) af bestemte filtypenavne, du har redigeret registreringsdatabasen, som beskrevet i den [konfiguration fil API](https://msdn.microsoft.com/library/dn197834%28v=vs.85%29.aspx) side.

    -   Du har en internetforbindelse med computer konfigureret indstillinger, hvis det er nødvendigt for en proxy-server. For eksempel: `netsh winhttp import proxy source=ie`

-   Du har konfigureret yderligere forudsætninger for installationen af Azure Rights Management, som beskrevet i [about_RMSProtection_AzureRMS](https://msdn.microsoft.com/library/mt433202.aspx). Specielt, har du følgende værdier for at oprette forbindelse til Azure RMS ved hjælp af en service principal:

    -   BposTenantId

    -   AppPrincipalId

    -   Symmetrisk nøgle

-   Du har synkroniseret dine lokale Active Directory-brugerkonti med Azure Active Directory eller Office 365, herunder deres e-mail-adresse. Dette er nødvendigt for alle brugere, der kan være nødvendigt at få adgang til filer, når de er beskyttet af FCI og Azure RMS. Hvis du ikke gør dette trin (for eksempel i et testmiljø), kan brugere blive blokeret fra at få adgang til disse filer. Hvis du ønsker flere oplysninger om denne konto-konfiguration, se [Forberedelse til Azure rettighedsstyring](../Topic/Preparing_for_Azure_Rights_Management.md).

-   Du har identificeret skabelonen Rights Management til at bruge, der beskytter filerne. Sørg for, at du kender ID'ET for denne skabelon ved hjælp af den [Get-RMSTemplate](https://msdn.microsoft.com/library/azure/mt433197.aspx) cmdlet.

## Instruktioner til at konfigurere File Server Resource Manager FCI Azure RMS-beskyttelse
Følg disse instruktioner for at beskytte automatisk alle filer i en mappe ved hjælp af et Windows PowerShell-script som en brugerdefineret opgaverude. Benyt disse fremgangsmåder i denne rækkefølge:

1.  Windows PowerShell-script gemmes

2.  Oprette en klassificering egenskab til Rights Management (RMS)

3.  Oprette en regel for klassificering (klassificeringen for RMS)

4.  Konfigurere tidsplanen klassificering

5.  Oprette en brugerdefineret fil management opgave (Beskyt filer med RMS)

6.  Teste konfigurationen ved manuelt at køre reglen og opgave

I slutningen af denne vejledning, alle filerne i den valgte mappe vil blive klassificeret med den brugerdefinerede egenskab for RMS, og disse filer vil derefter være beskyttet med Rights Management. For en mere kompleks konfiguration, der beskytter selektivt nogle filer og ikke andre, kan du oprette eller bruge en anden klassifikation egenskab og en regel med en fil management-opgave, der beskytter filerne.

#### Windows PowerShell-script gemmes

1.  Udvid den [Windows PowerShell Script til Azure RMS-beskyttelse ved hjælp af File Server Resource Manager FCI](#BKMK_RMSProtection_Script) i denne artikel, og kopier indholdet. Indsætte indholdet af scriptet, og Navngiv filen **RMS-Protect-FCI.ps1** på din egen computer.

2.  Gennemgå scriptet, og Foretag følgende ændringer:

    -   Søg efter følgende streng og erstatte det med dine egne AppPrincipalId, du bruger med den [sæt RMSServerAuthentication](https://msdn.microsoft.com/library/mt433199.aspx) -cmdlet til at oprette forbindelse til Azure RMS:

        ```
        <enter your AppPrincipalId here>
        ```
        Scriptet kan f.eks:

        `[Parameter(Mandatory = $false)]`

        `[Parameter(Mandatory = $false)] [string]$AppPrincipalId = "b5e3f76a-b5c2-4c96-a594-a0807f65bba4",`

    -   Søg efter følgende streng og erstatte det med dine egne symmetriske nøgle, du bruger med den [sæt RMSServerAuthentication](https://msdn.microsoft.com/library/mt433199.aspx) -cmdlet til at oprette forbindelse til Azure RMS:

        ```
        <enter your key here>
        ```
        Scriptet kan f.eks:

        `[Parameter(Mandatory = $false)]`

        `[string]$SymmetricKey = "zIeMu8zNJ6U377CLtppkhkbl4gjodmYSXUVwAO5ycgA="`

    -   Søg efter følgende streng og erstatte det med dine egne BposTenantId (lejer ID), du bruger med den [sæt RMSServerAuthentication](https://msdn.microsoft.com/library/mt433199.aspx) -cmdlet til at oprette forbindelse til Azure RMS:

        ```
        <enter your BposTenantId here>
        ```
        Scriptet kan f.eks:

        `[Parameter(Mandatory = $false)]`

        `[string]$BposTenantId = "23976bc6-dcd4-4173-9d96-dad1f48efd42",`

    -   Hvis serveren kører Windows Server 2012, kan du muligvis indlæse modulet RMSProtection i begyndelsen af scriptet manuelt. Tilføj følgende kommando (eller tilsvarende, hvis mappen "Program Files" er på et andet drev end c-drevet:

        ```
        Import-Module "C:\Program Files\WindowsPowerShell\Modules\RMSProtection\RMSProtection.dll"
        ```

3.  Tilmeld script. Hvis du ikke logger scriptet (mere sikker), skal du konfigurere Windows PowerShell på de servere, der kører den. For eksempel at køre en Windows PowerShell-session med den **Kør som Administrator** indstilling, og skriv: **Set-ExecutionPolicy Unrestricted**. Denne konfiguration kan dog alle usignerede scripts, der køres (mindre sikker).

    Finde flere oplysninger om signering af Windows PowerShell-scripter [about_Signing](https://technet.microsoft.com/library/hh847874.aspx) i PowerShell-dokumentbibliotek.

4.  Gem filen lokalt på hver filserver, der kører fil Resource Manager med filen klassificering infrastruktur. For eksempel, gemme filen i **C:\RMS-Protection**. Sikre denne fil ved hjælp af NTFS-tilladelser, så uautoriserede brugere ikke kan ændre den.

Du er nu klar til at konfigurere File Server Resource Manager.

#### Oprette en klassificering egenskab til Rights Management (RMS)

-   I File Server Resource Manager, klassificering, Management, oprette en ny lokal egenskab:

    -   **Name**: Type **RMS**

    -   **Beskrivelse**:   Type **Rights Management protection**

    -   **Egenskabstype**: Vælg **Ja/Nej**

    -   **Value**: Vælg **Ja**

Vi kan nu oprette en regel for klassificering, der bruger denne egenskab.

#### Oprette en regel for klassificering (klassificeringen for RMS)

-   Opret en ny regel for klassificering:

    -   På den **generelle** under fanen:

        -   **Name**: Type **Classify for RMS**

        -   **Aktiveret**: Holde den standard, der er, at dette afkrydsningsfelt er markeret.

        -   **Beskrivelse**: Type **Classify all files in the &lt;folder name&gt; folder for Rights Management**.

            Erstat *&lt; mappenavn &gt;* med dine valgte mappenavn. For eksempel **klassificere alle filerne i mappen C:\FileShare til Rights Management**

        -   **Scope**: Tilføj den valgte mappe. For eksempel **C:\FileShare**.

            Vælg ikke afkrydsningsfelterne.

    -   På den **klassificering** under fanen:

    -   **Metode til klassificering af**: Vælg **klassificering i mappen**

    -   **Egenskaber** navn: Vælg **RMS**

    -   Egenskaben **værdi**: Vælg **Ja**

Selvom du kan køre klassificering reglerne manuelt til løbende operationer, skal denne regel til at køre på en tidsplan, så nye filer vil blive klassificeret med egenskaben RMS.

#### Konfigurere tidsplanen klassificering

-   På den **automatisk klassificering** under fanen:

    -   **Aktivere fast skema**: Marker dette afkrydsningsfelt.

    -   Konfigurere tidsplanen for alle regler for klassificering til at køre, som omfatter vores ny regel til at klassificere filer med egenskaben RMS.

    -   **Tillader fortløbende klassificering for nye filer**: Marker dette afkrydsningsfelt, så nye filer vil blive klassificeret.

    -   Valgfrit: Foretag eventuelle andre ændringer, som du ønsker, f.eks konfiguration af indstillinger for rapporter og meddelelser.

Nu du har fuldført konfigurationen af klassificering, er du klar til at konfigurere en opgave med administration for at anvende RMS-beskyttelse på filerne.

#### Oprette en brugerdefineret fil management opgave (Beskyt filer med RMS)

-   I **filhåndteringsopgaver**, oprette en ny fil management opgave:

    -   På den **generelle** under fanen:

        -   **Opgavenavn**: Type **Protect files with RMS**

        -   Holde den **aktivere** markeret.

        -   **Beskrivelse**: Type **Protect files in &lt;folder name&gt; with Rights Management and a template by using a Windows PowerShell script.**

            Erstat *&lt; mappenavn &gt;* med dine valgte mappenavn. For eksempel **beskytte filer i C:\FileShare med Rights Management og en skabelon ved hjælp af et Windows PowerShell-script**

        -   **Scope**: Vælg den valgte mappe. For eksempel **C:\FileShare**.

            Vælg ikke afkrydsningsfelterne.

    -   På den **handling** under fanen:

        -   **Type**: Vælg **brugerdefinerede**

        -   **Eksekverbare fil**: Angiv følgende:

            ```
            C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe
            ```
            Hvis Windows ikke er installeret på C:-drevet, ændrer denne sti, eller gå til denne fil.

        -   **Argument**: Angiv følgende, udlevering af dine egne værdier for &lt; sti &gt; og &lt; skabelon-ID &gt;:

            ```
            -Noprofile -Command "<path>\RMS-Protect-FCI.ps1 -File '[Source File Path]' -TemplateID <template GUID> -OwnerMail [Source File Owner Email]"
            ```
            For eksempel, hvis du kopierede script til C:\RMS-Protection og den skabelon-ID, du har identificeret fra forudsætningerne er e6ee2481-26b9-45e5-b34a-f744eacd53b0, angive følgende:

            `-Noprofile -Command "C:\RMS-Protection\RMS-Protect-FCI.ps1 -File '[Source File Path]' -TemplateID e6ee2481-26b9-45e5-b34a-f744eacd53b0 -OwnerMail [Source File Owner Email]"`

            I denne kommando **[kilde filsti]** og **[kilde fil ejer Email]** er begge FCI-specifikke variabler, så skriv dem nøjagtigt som de vises i ovenstående kommando. Den første, der bruges til automatisk for at angive den identificerede fil i mappen af FCI, og andet er til FCI til automatisk at hente den navngivne ejer den identificerede fil e-mail-adresse. Denne kommando skal gentages for hver fil i mappen, som i eksemplet, er hver fil i mappen C:\FileShare, som desuden har RMS som en filegenskab klassificering.

            > [!NOTE]
            > Den **-OwnerMail [Source File Owner Email]** parameter og værdi sikrer, at den oprindelige ejer af filen gives rettighedsstyring ejeren af filen, når den er beskyttet. Dette sikrer, at den oprindelige fil ejer har alle Rights Management-rettigheder til deres egne filer. Når filerne oprettes som en domænebruger, hentes e-mail-adressen automatisk fra Active Directory ved hjælp af navnet på brugerkontoen i filens ejer egenskab. For at gøre dette, skal file server i samme domæne eller tillidsdomænet som bruger.
            > 
            > Når det er muligt, kan du tildele oprindelige ejere beskyttede dokumenter for at sikre, at disse brugere fortsat har fuld kontrol over de filer, de har oprettet. Men hvis du bruger variablen [kilde fil ejer Email] som ovenfor, og en fil har ikke en domænebruger, der er defineret som ejer (for eksempel en lokal konto blev brugt til at oprette filen, så ejeren viser systemet,) mislykkes scriptet.
            > 
            > For filer, der ikke er en domænebruger, som ejer, kan du kopiere og gemme disse filer dig selv som en domænebruger, så du bliver ejer af netop disse filer. Eller hvis du har rettigheder, kan du manuelt ændre ejeren.  Eller du kan også angive en bestemt e-mail-adresse (som din egen eller en gruppeadresse for IT-afdelingen) i stedet for variablen [kilde fil ejer Email], hvilket betyder, at alle filer, der beskyttes ved hjælp af dette script skal bruge denne e-mail-adresse til at definere den nye ejer.

    -   **Køre kommandoen som**: Vælg **lokalt System**

    -   På den **stand** under fanen:

        -   **Egenskaber**: Vælg **RMS**

        -   **Erhvervsdrivende**: Vælg **lige**

        -   **Value**: Vælg **Ja**

    -   På den **plan** under fanen:

        -   **Run at**: Konfigurer din foretrukne tidsplan.

            Giver mulighed for masser af tid til scriptet til at fuldføre. Selvom denne løsning beskytter alle filer i mappen, køres scriptet én gang for hver fil, hver gang. Selvom det tager længere tid end at beskytte alle filer på samme tid, som understøtter værktøjet RMS-beskyttelse, er denne fil for fil-konfiguration for FCI mere effektive. For eksempel de beskyttede filer kan have forskellige ejere (bevarer den oprindelige ejer) når du bruger variablen [kilde fil ejer Email], og handlingen filen skal, hvis du senere ændrer konfigurationen for at beskytte filer i stedet for alle filer i en mappe efter eget valg.

        -   **Køre hele tiden på nye filer**: Marker dette afkrydsningsfelt.

#### Teste konfigurationen ved manuelt at køre reglen og opgave

1.  Kør reglen klassificering:

    1.  Klik på **klassificering regler** &gt; **nu køre klassificering med alle regler for**

    2.  Klik **vente klassificering til at udføre**, og klik derefter på **OK**.

2.  Venter på den **kører klassificering** dialogboksen for at lukke og derefter få vist resultaterne i rapporten vises automatisk. Du bør se **1** for den **Egenskaber** og antallet af filer i mappen. Bekræft ved at bruge Filoversigt og kontrollere egenskaberne for filerne i den valgte mappe. På den **klassificering** under fanen, skal du se **RMS** som et egenskabsnavn og **Ja** for sine **værdi**.

3.  Kør filen management opgaven:

    1.  Klik på **filhåndteringsopgaver** &gt; **beskytte filer med RMS** &gt; **Kør filen Management opgaven nu**

    2.  Klik **vente på, at opgaven er afsluttet**, og klik derefter på **OK**.

4.  Venter på den **kører filen administrationsopgave** dialogboksen for at lukke og derefter få vist resultaterne i rapporten vises automatisk. Du bør se antallet af filer, der findes i den valgte mappe i den **filer** felt. Kontroller, at filerne i den valgte mappe er nu beskyttet af RMS. For eksempel hvis den valgte mappe er C:\FileShare, Skriv følgende i en Windows PowerShell-session og bekræfte, at ingen filer har en status for **UnProtected**:

    ```
    foreach ($file in (Get-ChildItem -Path C:\FileShare -Force | where {!$_.PSIsContainer})) {Get-RMSFileStatus -f $file.PSPath}
    ```
    > [!TIP]
    > Tips til fejlfinding:
    > 
    > -   Hvis du kan se **0** i rapporten, i stedet for antallet af filer i mappen, angiver det, at scriptet ikke blev kørt. Kontroller først, selve script ved at indlæse dem i Windows PowerShell ISE til at validere script indholdet og forsøge at køre den for at se, hvis eventuelle fejl vises. Scriptet forsøger at oprette forbindelse og godkende Azure RMS uden argumenter, der er angivet.
    > 
    >     -   Hvis scriptet rapporterer, at den ikke kunne oprette forbindelse til Azure RMS, kan du se de værdier, der vises for den vigtigste tjenestekonto, som du har angivet i script.  Yderligere oplysninger om, hvordan du opretter tjenestekontoen principal, se den anden betingelse i [about_RMSProtection_AzureRMS](https://msdn.microsoft.com/library/mt433202.aspx)
    >     -   Hvis scriptet rapporterer, at det kunne tilsluttes Azure RMS og dit Azure område er uden for Nordamerika, kan du kontrollere, at du har redigeret registreringsdatabasen korrekt for denne konfiguration. Der er en god test for at køre Get-RMSTemplate direkte fra Windows PowerShell på serveren. Yderligere oplysninger om redigering af registreringsdatabasen, kan du se den tredje forudsætning i [about_RMSProtection_AzureRMS](https://msdn.microsoft.com/library/mt433202.aspx).
    > -   Hvis scriptet alene kører i Windows PowerShell ISE uden fejl, kan du prøve at køre det således af en PowerShell-session, angive et filnavn til at beskytte og uden parameteren - OwnerEmail:
    > 
    >     ```
    >     powershell.exe -Noprofile -Command "<path>\RMS-Protect-FCI.ps1 -File <full path and name of a file>' -TemplateID <template GUID>"
    >     ```
    >     -   Hvis scriptet kører korrekt under denne Windows PowerShell-session, Kontroller indtastningerne til **direktør** og **Argument** i filhandlingen management opgaven.  Hvis du har angivet **- OwnerEmail [kilde fil ejer Email]**, kan du prøve at fjerne denne parameter.
    > 
    >         Hvis filen management opgaven fungerer korrekt uden  **- OwnerEmail [kilde fil ejer Email]**, kontrollere, at de ubeskyttede filer har en domænebruger, der er angivet som ejeren af filen i stedet **SYSTEM**.  Du kan bruge den **sikkerhed** under fanen for filens egenskaber, og klik derefter på **Avanceret**. Den **ejer** værdi vises umiddelbart efter filen **navn**. Du skal også kontrollere, at filserveren er i samme domæne eller domænekonti slå brugerens e-mail-adresse fra Active Directory-domæneservices.
    > -   Hvis du kan se det korrekte antal filer i rapporten, men filerne er ikke beskyttet, kan du prøve at beskytte filerne manuelt ved hjælp af den [Beskyt RMSFile](https://msdn.microsoft.com/library/azure/mt433201.aspx) -cmdlet til at se, hvis eventuelle fejl vises.

Når du har bekræftet, at disse opgaver kører korrekt, kan du lukke filen Resource Manager. Beskyttes nye filer automatisk, og alle filerne beskyttes igen, når planerne kører. Beskytte filer igen sikrer, at eventuelle ændringer af skabelonen anvendes på filerne.

### <a name="BKMK_RMSProtection_Script"></a>Windows PowerShell Script til Azure RMS-beskyttelse ved hjælp af File Server Resource Manager FCI
Dette afsnit indeholder eksempelscript for at kopiere og redigere, som beskrevet i det foregående afsnit.

*&#42;&#42;Ansvarsfraskrivelse&#42;&#42;: Dette eksempelscript understøttes ikke under en hvilken som helst Microsoft \\\Standard support-program eller en tjeneste. Dette eksempelscript leveres som BESET uden garanti af nogen art.*

```
<# .SYNOPSIS Helper script to protect all file types with Azure RMS and FCI. .DESCRIPTION Protect files with Azure RMS and Windows Server FCI, using an RMS template ID. #> param( [Parameter(Mandatory = $false)] [ValidateScript({ If($_ -eq "") {$true} else { if (Test-Path -Path $_ -PathType Leaf) {$true} else {throw "Can't find file specified"} } })] [string]$File, [Parameter(Mandatory = $false)] [string]$TemplateID, [Parameter(Mandatory = $false)] [string]$OwnerMail, [Parameter(Mandatory = $false)] [string]$AppPrincipalId = "<enter your AppPrincipalId here>", [Parameter(Mandatory = $false)] [string]$SymmetricKey = "<enter your key here>", [Parameter(Mandatory = $false)] [string]$BposTenantId = "<enter your BposTenantId here>" ) # script information [String] $Script:Version = 'version 1.0' [String] $Script:Name = "RMS-Protect-FCI.ps1" #global working variables [switch] $Script:isScriptProcess = $False # Controls the script process. If false, the script gracefully stops running. #**Functions (general helper)*************************************** function Get-ScriptName(){ return $MyInvocation.ScriptName.Substring($MyInvocation.ScriptName.LastIndexOf('\') + 1, $MyInvocation.ScriptName.LastIndexOf('.') - $MyInvocation.ScriptName.LastIndexOf('\') - 1) } #**Functions (script specific)************************************** function Check-Module{ param ([String]$Module = $(Throw "Module name not specified")) [bool]$isResult = $False #try to load the module if (get-module -list -name $Module) { import-module $Module if (get-module -name $Module ) { $isResult = $True } else { $isResult = $False } } else { $isResult = $False } return $isResult } function Protect-File ($ffile, $ftemplateId, $fownermail) { [bool] $returnValue = $false try { If ($OwnerMail -eq $null -or $OwnerMail -eq "") { $protectReturn = Protect-RMSFile -File $ffile -TemplateID $ftemplateId $returnValue = $true Write-Host ( "Information: " + "Protected File: $ffile with Template: $ftemplateId") } else { $protectReturn = Protect-RMSFile -File $ffile -TemplateID $ftemplateId -OwnerEmail $fownermail $returnValue = $true Write-Host ( "Information: " + "Protected File: $ffile with Template: $ftemplateId, set Owner: $fownermail") } } catch { Write-Host ( "ERROR" + "During protection of file: $ffile with Template: $ftemplateId") } return $returnValue } function Set-RMSConnection ($fappId, $fkey, $fbposId) { [bool] $returnValue = $false try { Set-RMSServerAuthentication -AppPrincipalId $fappId -Key $fkey -BposTenantId $fbposId Write-Host ("Information: " + "Connected to Azure RMS Service with BposTenantId: $fbposId using AppPrincipalId: $fappId") $returnValue = $true } catch { Write-Host ("ERROR" + "During connection to Azure RMS Service with BposTenantId: $fbposId using AppPrincipalId: $fappId") } return $returnValue } #**Main Script (Script)********************************************* Write-Host ("-== " + $Script:Name + " " + $Version + " ==-") $Script:isScriptProcess = $True # Validate Azure RMS connection by checking the module and then connection if ($Script:isScriptProcess) { if (Check-Module -Module RMSProtection){ $Script:isScriptProcess = $True } else { Write-Host ("The RMSProtection module is not loaded") -foregroundcolor "yellow" -backgroundcolor "black" $Script:isScriptProcess = $False } } if ($Script:isScriptProcess) { #Write-Host ("Try to connect to Azure RMS with AppId: $AppPrincipalId and BPOSID: $BposTenantId" ) if (Set-RMSConnection $AppPrincipalId $SymmetricKey $BposTenantId) { Write-Host ("Connected to Azure RMS") } else { Write-Host ("Couldn't connect to Azure RMS") -foregroundcolor "yellow" -backgroundcolor "black" $Script:isScriptProcess = $False } } #  Start working loop if ($Script:isScriptProcess) { if ( !(($File -eq $null) -or ($File -eq "")) ) { if (!(Protect-File -ffile $File -ftemplateId $TemplateID -fownermail $OwnerMail)) { $Script:isScriptProcess = $False } } } # Closing if (!$Script:isScriptProcess) { Write-Host "ERROR occurred during script process" -foregroundcolor "red" -backgroundcolor "black"} write-host ("-== " + $Script:Name + " " + $Version + "  ==-") if (!$Script:isScriptProcess) { exit(-1) } else {exit(0)}
```

## Ændring af vejledningen til selektivt at beskytte filer
Når du har de foregående instruktioner arbejde, er det meget nemt at ændre dem til en mere avanceret konfiguration. Eksempelvis beskytte filerne ved hjælp af det samme script, men kun for filer, der indeholder personligt identificerbare oplysninger, og måske vælge en skabelon, der er mere restriktive rettigheder.

For at gøre dette, kan du bruge en af de indbyggede klassificering egenskaber (for eksempel **personligt identificerbare oplysninger**) eller oprette dit eget nye egenskab. Derefter oprette en ny regel, der bruger denne egenskab. For eksempel kan du vælge den **indhold klassificering**, vælge den **personligt identificerbare oplysninger** ejendom til en værdi af **Høj**, og konfigurere mønsteret streng eller et udtryk, der identificerer den fil, der er konfigureret for denne egenskab (f.eks strengen "**fødselsdato**").

Nu alt du skal gøre er at oprette en ny fil management opgave, der bruger det samme script, men muligvis med en anden skabelon, og Konfigurer betingelsen for egenskaben klassificering, som du lige har konfigureret. For eksempel, i stedet for den betingelse, som vi tidligere har konfigureret (**RMS** ejendom, **lige**, **Ja**), skal du vælge den **personligt identificerbare oplysninger** egenskab med den **Operator** værdi angivet til **lige** og **værdi** af **Høj**.

