---
description: na
keywords: na
title: Configuring Applications for Azure Rights Management
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ea09cbc5-b98b-444e-8b60-5bc3cb199c36
---
# Konfiguration af programmer for Azure rettighedsstyring
> [!NOTE]
> Disse oplysninger er for IT-administratorer og konsulenter, som har implementeret Azure Rights Management. Hvis du har brug for hjælp til brugere og oplysninger om, hvordan du bruger Rights Management for et bestemt program eller åbne en fil, der er beskyttet med rettigheder, kan du bruge Hjælp og vejledning, der følger med programmet.
> 
> Eksempelvis for Office-programmer, klikke på ikonet Hjælp og indtaste søgeord som **Rights Management** eller **IRM**. RMS deling program til Windows, finder du på [Rights Management deling program brugervejledningen](http://technet.microsoft.com/library/dn339006.aspx).

Når du har installeret Azure Rights Management (Azure RMS) for din organisation, kan du bruge følgende oplysninger til at konfigurere programmer og tjenester til at understøtte RMS Azure. Disse omfatter Office-programmer som Word 2013 og Word 2010 og Exchange Online (regler for transport, Forhindring af datatab, gør ikke fremad og kryptering) og SharePoint Online (beskyttede biblioteker), f.eks. Oplysninger om, hvordan disse programmer og tjenester understøtter rettighedsstyring, se [Hvordan programmer understøtter Azure rettighedsstyring](../Topic/How_Applications_Support_Azure_Rights_Management.md).

> [!IMPORTANT]
> Finde oplysninger om understøttede versioner og andre krav, [Krav til Azure rettighedsstyring](../Topic/Requirements_for_Azure_Rights_Management.md).

-   [Office 365: Konfiguration af klienter og online-tjenester](../Topic/Configuring_Applications_for_Azure_Rights_Management.md#BKMK_O365)

    -   [Exchange Online: IRM-konfigurationen](../Topic/Configuring_Applications_for_Azure_Rights_Management.md#BKMK_ExchangeOnline)

    -   [SharePoint Online- og OneDrive til virksomheder: IRM-konfigurationen](#BKMK_SharePointOnline)

-   [2016 Office og Office-2013: Konfiguration til klienter](#BKMK_Office2013Configuration)

-   [Office 2010: Konfiguration til klienter](../Topic/Configuring_Applications_for_Azure_Rights_Management.md#BKMK_Office2010Configuration)

-   [Rights Management deling program: Installation og konfiguration til klienter](../Topic/Configuring_Applications_for_Azure_Rights_Management.md#BKMK_SharingApp)

    -   [Deling af programmer til Windows RMS: Installation og konfiguration](../Topic/Configuring_Applications_for_Azure_Rights_Management.md#BKMK_SharingAppforWindows)

    -   [RMS deling ansøgning om mobile platforme: Installation](../Topic/Configuring_Applications_for_Azure_Rights_Management.md#BKMK_SharingAppMovileDevices)

-   [Andre programmer, der understøtter den RMS APIs: Installation og konfiguration](../Topic/Configuring_Applications_for_Azure_Rights_Management.md#BKMK_RMSAPIs)

Hvis du vil konfigurere lokale servere som Exchange Server og SharePoint Server, se [Installation af Azure Rights Management-stik](../Topic/Deploying_the_Azure_Rights_Management_Connector.md).

> [!TIP]
> Eksempler på højt niveau og skærmbilleder af programmer, der er konfigureret til at bruge Azure RMS finder du på [Azure RMS i aktion: Se, hvad administratorer og brugere](../Topic/What_is_Azure_Rights_Management_.md#BKMK_RMSpictures) afsnit fra den [Hvad er Azure Rights Management?](../Topic/What_is_Azure_Rights_Management_.md) emne.

## <a name="BKMK_O365"></a>Office 365: Konfiguration af klienter og online-tjenester
Da Office 365 understøtter indbygget Azure RMS, kræves ingen konfiguration af klientcomputer til at understøtte oplysninger rights management (IRM)-funktioner for programmer som Word, Excel, PowerPoint, Outlook og Outlook Web App. Alle brugere, der har at gøre er at logge på deres Office-programmer med deres [!INCLUDE[o365_1](../Token/o365_1_md.md)] legitimationsoplysninger, og de kan beskytte filer og e-mails og bruge filer og e-mails, der er beskyttet af andre.

Vi anbefaler dog, at du supplere disse programmer med Rights Management Deling af programmet, så brugere får fordelen af Office-tilføjelsesprogram. Yderligere oplysninger finder du i [Rights Management deling program: Installation og konfiguration til klienter](../Topic/Configuring_Applications_for_Azure_Rights_Management.md#BKMK_SharingApp) afsnit i dette emne.

### <a name="BKMK_ExchangeOnline"></a>Exchange Online: IRM-konfigurationen
Hvis du vil konfigurere Exchange Online for at understøtte RMS Azure, skal du konfigurere tjenesten information rights management (IRM) til Exchange Online. For at gøre dette skal du bruge Windows PowerShell (ingen grund til at installere et separat modul), og køre [PowerShell-kommandoer til Exchange Online](https://technet.microsoft.com/library/jj200677.aspx).

> [!NOTE]
> Du kan ikke i øjeblikket konfigurere Exchange Online for at understøtte RMS Azure, hvis du bruger en kunde-styrede lejer nøgle (BYOK) til Azure RMS i stedet for standardkonfigurationen af en Microsoft-styrede lejer nøgle. Yderligere oplysninger finder du i [BYOK pricing and restrictions](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_Pricing) afsnit i den [Planlægning og implementering af Azure Rights Management lejer nøglen](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md) emne.
> 
> Hvis du forsøger at konfigurere Exchange Online, når du bruger Azure RMS BYOK, mislykkes kommandoen til at importere nøgle (trin 5, i følgende procedure) med fejlmeddelelsen **[FailureCategory = Cmdlet-FailedToGetTrustedPublishingDomainFromRmsOnlineException]**.

Nedenstående anvisninger giver et typisk sæt kommandoer, du vil køre for at aktivere Exchange Online for at bruge Azure RMS:

1.  Hvis det er første gang, du har brugt Windows PowerShell til Exchange Online på din computer, skal du konfigurere Windows PowerShell for at køre scripts, der signerede. Start Windows PowerShell-session ved hjælp af den **Kør som administrator** indstilling, og skriv derefter:

    ```
    Set-ExecutionPolicy RemoteSigned
    ```

2.  I Windows PowerShell-sessionen, logge på Exchange Online ved hjælp af en konto, der er aktiveret for fjernadgang til Shell. Alle konti, der er oprettet i Exchange Online er som standard aktiveret for fjernadgang til Shell, men det kan være deaktiveret (og aktiveret) ved hjælp af den   [sæt bruger &lt; UserIdentity &gt; - RemotePowerShellEnabled](https://technet.microsoft.com/library/jj984292%28v=exchg.160%29.aspx) kommando.

    Hvis du vil logge på, skal du skrive:

    ```
    $Cred = Get-Credential
    ```
    I den **anmodning om legitimationsoplysninger til Windows PowerShell** dialogboksen boks, indtast Office 365-brugernavn og adgangskode.

3.  Opret forbindelse til Exchange Online-tjenesten ved at køre følgende to kommandoer:

    ```
    $Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri https://ps.outlook.com/powershell/ -Credential $Cred -Authentication Basic –AllowRedirection
    ```

    ```
    Import-PSSession $Session
    ```

4.  Angiv placeringen af nøglen Azure RMS lejer i henhold til dit område:

    For Nordamerika (og regeringen abonnementer):

    ```
    Set-IRMConfiguration -RMSOnlineKeySharingLocation "https://sp-rms.na.aadrm.com/TenantManagement/ServicePartner.svc"
    ```
    For Europa:

    ```
    Set-IRMConfiguration -RMSOnlineKeySharingLocation "https://sp-rms.eu.aadrm.com/TenantManagement/ServicePartner.svc"
    ```
    For Asien:

    ```
    Set-IRMConfiguration -RMSOnlineKeySharingLocation "https://sp-rms.ap.aadrm.com/TenantManagement/ServicePartner.svc"
    ```
    For Sydamerika:

    ```
    Set-IRMConfiguration -RMSOnlineKeySharingLocation "https://sp-rms.sa.aadrm.com/TenantManagement/ServicePartner.svc"
    ```

5.  Importere konfigurationsdata fra Azure RMS til Exchange Online, i form af publicerer tillidsdomænet (TPD). Dette omfatter Azure RMS lejer nøglen og Azure RMS-skabeloner:

    ```
    Import-RMSTrustedPublishingDomain -RMSOnline -name "RMS Online"
    ```
    I denne kommando, vi har brugt navnet på **RMS Online** til navnet på TPD for Azure RMS i Exchange Online. Når TPD er importeret, hedder **RMS Online - 1** i Exchange Online.

6.  Aktivere Azure RMS-funktioner, så IRM-funktioner er tilgængelige for Exchange Online:

    ```
    Set-IRMConfiguration -InternalLicensingEnabled $true
    ```
    Når du har kørt denne kommando, aktiveres automatisk Rights Management for Outlook-klient, Outlook Web app og Exchange ActiveSync.

7.  Du kan eventuelt test, denne konfiguration er udført ved hjælp af følgende kommando:

    ```
    Test-IRMConfiguration -Sender <user email address>
    ```
    For eksempel: **Test-IRMConfiguration -Sender  adams@contoso.com**

    Denne kommando udfører en række kontrolforanstaltninger, der omfatter kontrol af forbindelsen til tjenesten, henter konfigurationen, henter URI'er, licenser og nogen skabeloner. I Windows PowerShell-session, får du vist resultaterne af hver og enden, hvis alt overfører kontrollen: **SAMLEDE RESULTAT: GENNEMLØB**

8.  Afbryd din fjernsession PowerShell:

    ```
    Remove-PSSession $Session
    ```

Brugere kan nu beskytte deres e-mail-meddelelser ved hjælp af Azure RMS. I Outlook Web App, f.eks **angive tilladelser** fra den udvidede menu (**...**), og vælg derefter **Videresend ikke** eller en af de tilgængelige skabeloner til at anvende beskyttelse af oplysninger til e-mail-meddelelsen og vedhæftede filer. Fordi Outlook Web App cachelagrer Brugergrænsefladen for en dag, vent dog for denne periode skal forløbe, før du forsøger at anvende beskyttelse af oplysninger til e-mail-meddelelser og efter at have kørt disse konfigurationskommandoer. Før Brugergrænsefladen er opdateret til at afspejle den nye konfiguration, kan du ikke se nogen indstillinger fra den **angive tilladelser** i menuen.

> [!IMPORTANT]
> Hvis du opretter nye [brugerdefinerede skabeloner](https://technet.microsoft.com/library/dn642472.aspx) Azure RMS eller opdatere skabeloner, hver gang, skal du køre følgende kommando i Exchange Online PowerShell (hvis nødvendigt, Kør trin 2 og 3 først) til at synkronisere disse ændringer til Exchange Online: `Import-RMSTrustedPublishingDomain -Name "RMS Online - 1" -RefreshTemplates –RMSOnline`

Som en Exchange-administrator, kan du nu konfigurere funktioner, der anvendes automatisk, beskyttelse af oplysninger, som [transport regler](https://technet.microsoft.com/library/dd302432.aspx), [Datapolitikker for tab forebyggelse (DLP)](https://technet.microsoft.com/library/jj150527%28v=exchg.150%29.aspx), og [beskyttet talebesked](https://technet.microsoft.com/library/dn198211%28v=exchg.150%29.aspx) (Unified Messaging).

Du kan finde detaljerede instruktioner til at konfigurere Exchange Online for at aktivere IRM-funktionaliteten i Exchange-biblioteket. For eksempel:

-   [Oprette forbindelse til Exchange Online ved hjælp af remote PowerShell](https://technet.microsoft.com/library/jj984289%28v=exchg.160%29.aspx)

-   [Konfigurere IRM for at bruge Azure Rights Management](https://technet.microsoft.com/library/dn151475%28v=exchg.150%29.aspx)

#### Office 365 meddelelseskryptering
Du kan køre de samme trin som beskrevet i forrige afsnit, men hvis du ikke vil skabeloner der skal vises, før trin 6 Kør følgende kommando for at forhindre, at IRM-skabeloner er tilgængelige i Outlook Web App og Outlook-klienten: `Set-IRMConfiguration -ClientAccessServerEnabled $false`

Derefter er du klar til at konfigurere [transport regler](https://technet.microsoft.com/library/dd302432.aspx) til at ændre sikkerheden for meddelelsen automatisk, når modtagerne er placeret uden for organisationen, og vælg den **anvender Office 365-meddelelseskryptering** indstilling.

Finde flere oplysninger om meddelelseskryptering, [kryptering i Office 365](https://technet.microsoft.com/library/dn569286.aspx) i Exchange-biblioteket.

### <a name="BKMK_SharePointOnline"></a>SharePoint Online- og OneDrive til virksomheder: IRM-konfigurationen
Hvis du vil konfigurere SharePoint Online og OneDrive til virksomheder til at understøtte RMS Azure, skal du først aktivere tjenesten information rights management (IRM) til SharePoint Online ved hjælp af SharePoint admin center. Derefter webstedsejere kan IRM-beskytte deres SharePoint-lister og dokumentbiblioteker, og brugerne kan IRM-beskytte deres OneDrive for Business-bibliotek, så dokumenter, der gemmes, og deles med andre, som automatisk er beskyttet af Azure RMS.

For at aktivere tjenesten information rights management (IRM) til SharePoint Online, skal du se følgende instruktioner fra webstedet Office:

-   [Indstillet af IRM Information Rights Management () i SharePoint admin center](http://office.microsoft.com/office365-sharepoint-online-enterprise-help/set-up-information-rights-management-irm-insharepoint-online-HA102895193.aspx)

Denne konfiguration sker ved Office 365-administratoren.

#### Konfigurere IRM for biblioteker og lister
Når du har aktiveret IRM-tjeneste til SharePoint, kan webstedsejere IRM-beskytte deres SharePoint-dokumentbiblioteker og lister. Yderligere oplysninger finder du i følgende Office-websted:

-   [Anvende IRM på en liste eller et bibliotek](http://office.microsoft.com/sharepoint-help/apply-information-rights-management-to-a-list-or-library-HA102891460.aspx)

Denne konfiguration er udført af administratoren af SharePoint-webstedet.

#### <a name="BKMK_OneDrive"></a>Konfigurere IRM for OneDrive til virksomheder
Når du har aktiveret IRM-tjeneste til SharePoint Online, kan brugernes OneDrive for Business dokumentbibliotek konfigureres til Rights Management-beskyttelse.  Brugerne kan konfigurere det selv ved hjælp af den **Indstillinger for** -ikonet i deres OneDrive. Selvom administratorer kan konfigurere Rights Management til brugernes OneDrive til virksomheder ved hjælp af SharePoint Administration center, kan du gøre dette ved hjælp af Windows PowerShell.

> [!NOTE]
> Yderligere oplysninger om konfiguration af OneDrive for virksomheder, se dokumentationen til Office,[Opsætning af OneDrive til virksomheder i Office 365](https://support.office.com/article/Set-up-OneDrive-for-Business-in-Office-365-3e21f8f0-e0a1-43be-aa3e-8c0236bf11bb).

##### Konfiguration af brugere
Give brugere disse instruktioner, så de kan konfigurere deres OneDrive til virksomheder og IRM-beskytte deres business-filer.

1.  Klik på OneDrive, den **indstillinger** ikon for at åbne menuen Indstillinger, og klik derefter på **indhold af portalwebsted**.

2.  Peger på den **dokumenter** side om side, vælger ellipser (**...**), og klik derefter på **Indstillinger.**

3.  På den **indstillinger** side i den **tilladelser og administration** skal du klikke på **Information Rights Management**.

4.  På den **oplysninger rettigheder administrationsindstillinger** side, vælge **begrænse tilladelserne til dette bibliotek ved hentning** afkrydsningsfeltet, Angiv dit valg af navn og en beskrivelse for tilladelser og eventuelt klikke på **Vis indstillinger** til at konfigurere valgfri konfigurationer, og klik derefter på **OK**.

    Yderligere oplysninger om af konfigurationsindstillinger finder du i instruktionerne i [anvende Information Rights Management til en liste eller bibliotek](https://support.office.com/article/Apply-Information-Rights-Management-to-a-list-or-library-3bdb5c4e-94fc-4741-b02f-4e7cc3c54aa1) fra Office-dokumentationen.

Da denne konfiguration er afhængig af brugere i stedet for en administrator at beskytte deres OneDrive for Business bibliotek IRM, kan du instruere brugerne om fordelene ved at beskytte deres filer og hvordan du gør dette. For eksempel forklares, når de deler et dokument fra OneDrive til virksomheder, de tillader kun de personer har adgang til den med de begrænsninger, de konfigurerer, selvom filen er omdøbt og kopieres til et andet sted.

##### Konfigurationen for administratorer
Selvom du ikke kan konfigurere IRM for brugernes OneDrive til virksomheder ved hjælp af SharePoint Administration center, kan du gøre dette ved hjælp af Windows PowerShell. Hvis du vil aktivere IRM for disse biblioteker, skal du følge disse trin:

1.  Hent og installer den [SharePoint Online klient komponenter SDK](http://www.microsoft.com/en-us/download/details.aspx?id=42038).

2.  Hent og installer den [SharePoint Online Management Shell](http://www.microsoft.com/en-us/download/details.aspx?id=35588).

3.  Kopier indholdet af følgende script, og Navngiv filen sæt IRMOnOneDriveForBusiness.ps1 på din computer.

    *&#42;&#42;Ansvarsfraskrivelse&#42;&#42;*: Dette eksempelscript understøttes ikke under en hvilken som helst Microsoft \\\Standard support-program eller en tjeneste. Dette eksempelscript leveres som BESET uden garanti af nogen art.

    ```
    # Requires Windows PowerShell version 3 <# Description: Configures IRM policy settings for OneDrive for Business and can also be used for SharePoint Online libraries and lists Script Installation Requirements: SharePoint Online Client Components SDK http://www.microsoft.com/en-us/download/details.aspx?id=42038 SharePoint Online Management Shell http://www.microsoft.com/en-us/download/details.aspx?id=35588 ====== #> # URL will be in the format https://<tenant-name>-admin.sharepoint.com $sharepointAdminCenterUrl = "https://contoso-admin.sharepoint.com" $tenantAdmin = "admin@contoso.com" $webUrls = @("https://contoso-my.sharepoint.com/personal/user1_contoso_com", "https://contoso-my.sharepoint.com/personal/user2_contoso_com", "https://contoso-my.sharepoint.com/personal/user3_contoso_com") <# As an alternative to specifying the URLs as an array, you can import them from a CSV file (no header, single value per row). Then, use: $webUrls = Get-Content -Path "File_path_and_name.csv" #> $listTitle = "Documents" function Load-SharePointOnlineClientComponentAssemblies { [cmdletbinding()] param() process { # assembly location: C:\Program Files\Common Files\microsoft shared\Web Server Extensions\16\ISAPI try { Write-Verbose "Loading Assembly: Microsoft.Office.Client.Policy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.Office.Client.Policy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null Write-Verbose "Loading Assembly: Microsoft.Office.Client.TranslationServices, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.Office.Client.TranslationServices, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.DocumentManagement, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.DocumentManagement, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Publishing, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Publishing, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Runtime, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Runtime, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Search.Applications, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Search.Applications, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Search, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Search, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Taxonomy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Taxonomy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.UserProfiles, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.UserProfiles, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null return $true } catch { if($_.Exception.Message -match "Could not load file or assembly") { Write-Error -Message "Unable to load the SharePoint Server 2013 Client Components.`nDownload Location: http://www.microsoft.com/en-us/download/details.aspx?id=42038" } else { Write-Error -Exception $_.Exception } return $false } } } function Load-SharePointOnlineModule { [cmdletbinding()] param() process { do { # Installation location: C:\Program Files\SharePoint Online Management Shell\Microsoft.Online.SharePoint.PowerShell $spoModule = Get-Module -Name Microsoft.Online.SharePoint.PowerShell -ErrorAction SilentlyContinue if(-not $spoModule) { try { Import-Module Microsoft.Online.SharePoint.PowerShell -DisableNameChecking return $true } catch { if($_.Exception.Message -match "Could not load file or assembly") { Write-Error -Message "Unable to load the SharePoint Online Management Shell.`nDownload Location: http://www.microsoft.com/en-us/download/details.aspx?id=35588" } else { Write-Error -Exception $_.Exception } return $false } } else { return $true } } while(-not $spoModule) } } function Set-IrmConfiguration { [cmdletbinding()] param( [parameter(Mandatory=$true)][Microsoft.SharePoint.Client.List]$List, [parameter(Mandatory=$true)][string]$PolicyTitle, [parameter(Mandatory=$true)][string]$PolicyDescription, [parameter(Mandatory=$false)][switch]$IrmReject, [parameter(Mandatory=$false)][DateTime]$ProtectionExpirationDate, [parameter(Mandatory=$false)][switch]$DisableDocumentBrowserView, [parameter(Mandatory=$false)][switch]$AllowPrint, [parameter(Mandatory=$false)][switch]$AllowScript, [parameter(Mandatory=$false)][switch]$AllowWriteCopy, [parameter(Mandatory=$false)][int]$DocumentAccessExpireDays, [parameter(Mandatory=$false)][int]$LicenseCacheExpireDays, [parameter(Mandatory=$false)][string]$GroupName ) process { Write-Verbose "Applying IRM Configuration on '$($List.Title)'" # reset the value to the default settings $list.InformationRightsManagementSettings.Reset() $list.IrmEnabled = $true # IRM Policy title and description $list.InformationRightsManagementSettings.PolicyTitle       = $PolicyTitle $list.InformationRightsManagementSettings.PolicyDescription = $PolicyDescription # Set additional IRM library settings # Do not allow users to upload documents that do not support IRM $list.IrmReject = $IrmReject.IsPresent $parsedDate = Get-Date if([DateTime]::TryParse($ProtectionExpirationDate, [ref]$parsedDate)) { # Stop restricting access to the library at <date> $list.IrmExpire = $true $list.InformationRightsManagementSettings.DocumentLibraryProtectionExpireDate = $ProtectionExpirationDate } # Prevent opening documents in the browser for this Document Library $list.InformationRightsManagementSettings.DisableDocumentBrowserView = $DisableDocumentBrowserView.IsPresent # Configure document access rights # Allow viewers to print $list.InformationRightsManagementSettings.AllowPrint = $AllowPrint.IsPresent # Allow viewers to run script and screen reader to function on downloaded documents $list.InformationRightsManagementSettings.AllowScript = $AllowScript.IsPresent # Allow viewers to write on a copy of the downloaded document $list.InformationRightsManagementSettings.AllowWriteCopy = $AllowWriteCopy.IsPresent if($DocumentAccessExpireDays) { # After download, document access rights will expire after these number of days (1-365) $list.InformationRightsManagementSettings.EnableDocumentAccessExpire = $true $list.InformationRightsManagementSettings.DocumentAccessExpireDays   = $DocumentAccessExpireDays } # Set group protection and credentials interval if($LicenseCacheExpireDays) { # Users must verify their credentials using this interval (days) $list.InformationRightsManagementSettings.EnableLicenseCacheExpire = $true $list.InformationRightsManagementSettings.LicenseCacheExpireDays   = $LicenseCacheExpireDays } if($GroupName) { # Allow group protection. Default group: $list.InformationRightsManagementSettings.EnableGroupProtection = $true $list.InformationRightsManagementSettings.GroupName             = $GroupName } } end { if($list) { Write-Verbose "Committing IRM configuration settings on '$($list.Title)'" $list.InformationRightsManagementSettings.Update() $list.Update() $script:clientContext.Load($list) $script:clientContext.ExecuteQuery() } } } function Get-CredentialFromCredentialCache { [cmdletbinding()] param([string]$CredentialName) #if( Test-Path variable:\global:CredentialCache ) if( Get-Variable O365TenantAdminCredentialCache -Scope Global -ErrorAction SilentlyContinue ) { if($global:O365TenantAdminCredentialCache.ContainsKey($CredentialName)) { Write-Verbose "Credential Cache Hit: $CredentialName" return $global:O365TenantAdminCredentialCache[$CredentialName] } } Write-Verbose "Credential Cache Miss: $CredentialName" return $null } function Add-CredentialToCredentialCache { [cmdletbinding()] param([System.Management.Automation.PSCredential]$Credential) if(-not (Get-Variable CredentialCache -Scope Global -ErrorAction SilentlyContinue)) { Write-Verbose "Initializing the Credential Cache" $global:O365TenantAdminCredentialCache = @{} } Write-Verbose "Adding Credential to the Credential Cache" $global:O365TenantAdminCredentialCache[$Credential.UserName] = $Credential } # load the required assemblies and Windows PowerShell modules if(-not ((Load-SharePointOnlineClientComponentAssemblies) -and (Load-SharePointOnlineModule)) ) { return } # Add the credentials to the client context and SharePoint Online service connection # check for cached credentials to use $o365TenantAdminCredential = Get-CredentialFromCredentialCache -CredentialName $tenantAdmin if(-not $o365TenantAdminCredential) { # when credentials are not cached, prompt for the tenant admin credentials $o365TenantAdminCredential = Get-Credential -UserName $tenantAdmin -Message "Enter the password for the Office 365 admin" if(-not $o365TenantAdminCredential -or -not $o365TenantAdminCredential.UserName -or $o365TenantAdminCredential.Password.Length -eq 0 ) { Write-Error -Message "Could not validate the supplied tenant admin credentials" return } # add the credentials to the cache Add-CredentialToCredentialCache -Credential $o365TenantAdminCredential } # connect to Office365 first, required for SharePoint Online cmdlets to run Connect-SPOService -Url $sharepointAdminCenterUrl -Credential $o365TenantAdminCredential # enumerate each of the specified site URLs foreach($webUrl in $webUrls) { $grantedSiteCollectionAdmin = $false try { # establish the client context and set the credentials to connect to the site $script:clientContext = New-Object Microsoft.SharePoint.Client.ClientContext($webUrl) $script:clientContext.Credentials = New-Object Microsoft.SharePoint.Client.SharePointOnlineCredentials($o365TenantAdminCredential.UserName, $o365TenantAdminCredential.Password) # initialize the site and web context $script:clientContext.Load($script:clientContext.Site) $script:clientContext.Load($script:clientContext.Web) $script:clientContext.ExecuteQuery() # load and ensure the tenant admin user account if present on the target SharePoint site $tenantAdminUser = $script:clientContext.Web.EnsureUser($o365TenantAdminCredential.UserName) $script:clientContext.Load($tenantAdminUser) $script:clientContext.ExecuteQuery() # check if the tenant admin is a site admin if( -not $tenantAdminUser.IsSiteAdmin ) { try { # grant the tenant admin temporary admin rights to the site collection Set-SPOUser -Site $script:clientContext.Site.Url -LoginName $o365TenantAdminCredential.UserName -IsSiteCollectionAdmin $true | Out-Null $grantedSiteCollectionAdmin = $true } catch { Write-Error $_.Exception return } } try { # load the list orlibrary using CSOM $list = $null $list = $script:clientContext.Web.Lists.GetByTitle($listTitle) $script:clientContext.Load($list) $script:clientContext.ExecuteQuery() # **************  ADMIN INSTRUCTIONS  ************** # If necessary, modify the following Set-IrmConfiguration parameters to match your required values # The supplied options and values are for example only # Example that shows the Set-IrmConfiguration command with all parameters: Set-IrmConfiguration -List $list -PolicyTitle "Protected Files" -PolicyDescription "This policy restricts access to authorized users" -IrmReject -ProtectionExpirationDate $(Get-Date).AddDays(180) -DisableDocumentBrowserView -AllowPrint -AllowScript -AllowWriteCopy -LicenseCacheExpireDays 25 -DocumentAccessExpireDays 90 Set-IrmConfiguration -List $list -PolicyTitle "Protected Files" -PolicyDescription "This policy restricts access to authorized users" } catch { Write-Error -Message "Error setting IRM configuration on site: $webUrl.`nError Details: $($_.Exception.ToString())" } } finally { if($grantedSiteCollectionAdmin) { # remove the temporary admin rights to the site collection Set-SPOUser -Site $script:clientContext.Site.Url -LoginName $o365TenantAdminCredential.UserName -IsSiteCollectionAdmin $false | Out-Null } } } Disconnect-SPOService -ErrorAction SilentlyContinue
    ```

4.  Gennemgå scriptet, og Foretag følgende ændringer:

    1.  Søge efter `$sharepointAdminCenterUrl` og erstatte værdien i eksemplet med din egen URL-adresse på SharePoint admin center.

        Du kan finde denne værdi som den grundlæggende URL-adresse, når du går ind på administrationssiden for SharePoint, og den har følgende format: https://*&lt; tenant_name &gt;*-admin.sharepoint.com

        For eksempel hvis lejer er "contoso", vil du angive: **https://contoso-admin.sharepoint.com**

    2.  Søge efter `$tenantAdmin` og erstatte værdien i eksemplet med dine egne fulde globale administratorkonto til Office 365.

        Denne værdi er den samme som den, du bruger til at logge på Office 365 admin-portalen som global administrator og har følgende format: brugernavn @-*&lt; lejer domænenavn &gt;*.com

        For eksempel hvis Office 365 global administratorbrugernavn er "admin" til "den contoso.com" lejer domæne, skal du angive: **admin@contoso.com**

    3.  Søge efter `$webUrls` og erstatte værdierne eksempel med dine brugeres OneDrive til Business web URL-adresser, tilføjelse eller sletning af så mange poster, som du har brug for.

        Alternativt kan du se kommentarerne i scriptet om, hvordan du erstatter denne matrix ved at importere en. Csv-fil, der indeholder alle de webadresser, skal du konfigurere.  Vi har lavet et andet eksempel på et script for at søge automatisk efter og udtrække URL-adresserne for at udfylde dette. Csv-fil. Når du er klar til at gøre dette, skal du udvide den [Yderligere script til at sende alle OneDrive til Business URL-adresser til en. Csv-fil](#BKMK_Script_OD4B_URLS) afsnit umiddelbart efter følgende fremgangsmåde.

        Internettet er URL-adressen til brugerens OneDrive til virksomheder i følgende format: https://*&lt; lejer navn &gt;*-my.sharepoint.com/personal/*&lt; brugernavn &gt;*_*&lt; lejer navn &gt;*_com

        For eksempel, hvis brugeren i forpagteren contoso har et brugernavn af "rsimone", vil du angive: **https://contoso-my.sharepoint.com/personal/rsimone_contoso_com**

    4.  Da vi bruger scriptet til at konfigurere OneDrive til virksomheder, ikke ændre værdien af **Documents** for den `$listTitle` variabel.

    5.  Søge efter `ADMIN INSTRUCTIONS`. Hvis du foretager nogen ændringer i dette afsnit, konfigureres brugerens OneDrive til virksomheder til IRM med "Beskyttede filer" politik titel og beskrivelse af "denne politik begrænser adgangen til autoriserede brugere".  Ingen andre IRM-indstillinger indstilles som er sandsynligvis passer til de fleste miljøer. Du kan dog ændre den foreslåede politik titel og beskrivelse, og også tilføje andre IRM indstillinger, der passer til dit miljø. Se eksemplet kommenterede i scriptet til at hjælpe dig med at oprette dit eget sæt parametre til kommandoen Set-IrmConfiguration.

5.  Gem scriptet og underskrive den. Hvis du ikke logger scriptet (mere sikker), skal Windows PowerShell konfigureres på computeren til at køre scripts, der ikke er signerede. For at gøre dette skal du køre en Windows PowerShell-session med den **Kør som Administrator** indstilling, og skriv: **Set-ExecutionPolicy Unrestricted**. Denne konfiguration kan dog alle usignerede scripts, der køres (mindre sikker).

    Finde flere oplysninger om signering af Windows PowerShell-scripter [about_Signing](https://technet.microsoft.com/library/hh847874.aspx) i PowerShell-dokumentbibliotek.

6.  Kør scriptet, og hvis du bliver bedt om det, kan du angive adgangskoden til Office 365 admin-konto. Hvis du redigere scriptet og køre den i samme Windows PowerShell-session, bliver du ikke bedt om om legitimationsoplysninger.

> [!TIP]
> Du kan også bruge dette script til at konfigurere IRM til SharePoint Online-bibliotek. For denne konfiguration, vil du højst sandsynligt at aktivere indstillingen ekstra **tillader ikke, at brugerne overfører dokumenter, der ikke understøtter IRM**, for at sikre, at biblioteket indeholder kun beskyttede dokumenter.    For at gøre dette skal du tilføje den `-IrmReject` parameter til kommandoen sæt IrmConfiguration i scriptet.
> 
> Skal du også redigere det `$webUrls` variabel (for eksempel **https://contoso.sharepoint.com**) og  `$listTitle` variabel (for eksempel **$Reports**).

Hvis du vil deaktivere IRM for brugerens OneDrive for Business-biblioteker, kan du udvide den [Script til at deaktivere IRM for OneDrive til virksomheder](#BKMK_Script_OD4B_DisableIRM) sektion.

###### <a name="BKMK_Script_OD4B_URLS"></a>Yderligere script til at sende alle OneDrive til Business URL-adresser til en. Csv-fil
Du kan bruge følgende Windows PowerShell-script til at udtrække URL-adresserne for alle brugere OneDrive til Business-biblioteker, som du kan derefter kontrollere, Rediger om nødvendigt og derefter importere til de vigtigste script til trin 4c ovenfor.

Dette script kræver også den [SharePoint Online klient komponenter SDK](http://www.microsoft.com/en-us/download/details.aspx?id=42038) og [SharePoint Online Management Shell](http://www.microsoft.com/en-us/download/details.aspx?id=35588). Følg samme fremgangsmåde for at kopiere og indsætte det, Gem filen lokalt (for eksempel "rapport-OneDriveForBusinessSiteInfo.ps1"), ændre den   `$sharepointAdminCenterUrl` og `$tenantAdmin` værdier som før, og derefter køre scriptet.

*&#42;&#42;Ansvarsfraskrivelse&#42;&#42;*: Dette eksempelscript understøttes ikke under en hvilken som helst Microsoft \\\Standard support-program eller en tjeneste. Dette eksempelscript leveres som BESET uden garanti af nogen art.

```
# Requires Windows PowerShell version 3 <# Description: Queries the search service of an Office 365 tenant to retrieve all OneDrive for Business sites. Details of the discovered sites are written to a .CSV file (by default,"OneDriveForBusinessSiteInfo_<date>.csv"). Script Installation Requirements: SharePoint Online Client Components SDK http://www.microsoft.com/en-us/download/details.aspx?id=42038 SharePoint Online Management Shell http://www.microsoft.com/en-us/download/details.aspx?id=35588 ====== #> # URL will be in the format https://<tenant-name>-admin.sharepoint.com $sharepointAdminCenterUrl = "https://contoso-admin.sharepoint.com" $tenantAdmin = "admin@contoso.onmicrosoft.com" $reportName = "OneDriveForBusinessSiteInfo_$((Get-Date).ToString("yyyy-MM-dd_hh.mm.ss")).csv" $oneDriveForBusinessSiteUrls= @() $resultsProcessed = 0 function Load-SharePointOnlineClientComponentAssemblies { [cmdletbinding()] param() process { # assembly location: C:\Program Files\Common Files\microsoft shared\Web Server Extensions\16\ISAPI try { Write-Verbose "Loading Assembly: Microsoft.Office.Client.Policy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.Office.Client.Policy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null Write-Verbose "Loading Assembly: Microsoft.Office.Client.TranslationServices, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.Office.Client.TranslationServices, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.DocumentManagement, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.DocumentManagement, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Publishing, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Publishing, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Runtime, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Runtime, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Search.Applications, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Search.Applications, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Search, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Search, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Taxonomy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Taxonomy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.UserProfiles, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.UserProfiles, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null return $true } catch { if($_.Exception.Message -match "Could not load file or assembly") { Write-Error -Message "Unable to load the SharePoint Server 2013 Client Components.`nDownload Location: http://www.microsoft.com/en-us/download/details.aspx?id=42038" } else { Write-Error -Exception $_.Exception } return $false } } } function Load-SharePointOnlineModule { [cmdletbinding()] param() process { do { # Installation location: C:\Program Files\SharePoint Online Management Shell\Microsoft.Online.SharePoint.PowerShell $spoModule = Get-Module -Name Microsoft.Online.SharePoint.PowerShell -ErrorAction SilentlyContinue if(-not $spoModule) { try { Import-Module Microsoft.Online.SharePoint.PowerShell -DisableNameChecking return $true } catch { if($_.Exception.Message -match "Could not load file or assembly") { Write-Error -Message "Unable to load the SharePoint Online Management Shell.`nDownload Location: http://www.microsoft.com/en-us/download/details.aspx?id=35588" } else { Write-Error -Exception $_.Exception } return $false } } else { return $true } } while(-not $spoModule) } } function Get-CredentialFromCredentialCache { [cmdletbinding()] param([string]$CredentialName) #if( Test-Path variable:\global:CredentialCache ) if( Get-Variable O365TenantAdminCredentialCache -Scope Global -ErrorAction SilentlyContinue ) { if($global:O365TenantAdminCredentialCache.ContainsKey($CredentialName)) { Write-Verbose "Credential Cache Hit: $CredentialName" return $global:O365TenantAdminCredentialCache[$CredentialName] } } Write-Verbose "Credential Cache Miss: $CredentialName" return $null } function Add-CredentialToCredentialCache { [cmdletbinding()] param([System.Management.Automation.PSCredential]$Credential) if(-not (Get-Variable CredentialCache -Scope Global -ErrorAction SilentlyContinue)) { Write-Verbose "Initializing the Credential Cache" $global:O365TenantAdminCredentialCache = @{} } Write-Verbose "Adding Credential to the Credential Cache" $global:O365TenantAdminCredentialCache[$Credential.UserName] = $Credential } # load the required assemblies and Windows PowerShell modules if(-not ((Load-SharePointOnlineClientComponentAssemblies) -and (Load-SharePointOnlineModule)) ) { return } # Add the credentials to the client context and SharePoint Online service connection # check for cached credentials to use $o365TenantAdminCredential = Get-CredentialFromCredentialCache -CredentialName $tenantAdmin if(-not $o365TenantAdminCredential) { # when credentials are not cached, prompt for the tenant admin credentials $o365TenantAdminCredential = Get-Credential -UserName $tenantAdmin -Message "Enter the password for the Office 365 admin" if(-not $o365TenantAdminCredential -or -not $o365TenantAdminCredential.UserName -or $o365TenantAdminCredential.Password.Length -eq 0 ) { Write-Error -Message "Could not validate the supplied tenant admin credentials" return } # add the credentials to the cache Add-CredentialToCredentialCache -Credential $o365TenantAdminCredential } # establish the client context and set the credentials to connect to the site $clientContext = New-Object Microsoft.SharePoint.Client.ClientContext($sharepointAdminCenterUrl) $clientContext.Credentials = New-Object Microsoft.SharePoint.Client.SharePointOnlineCredentials($o365TenantAdminCredential.UserName, $o365TenantAdminCredential.Password) # run a query against the Office 365 tenant search service to retrieve all OneDrive for Business URLs do { # build the query object $query = New-Object Microsoft.SharePoint.Client.Search.Query.KeywordQuery($clientContext) $query.TrimDuplicates        = $false $query.RowLimit              = 500 $query.QueryText             = "SPSiteUrl:'/personal/' AND contentclass:STS_Site" $query.StartRow              = $resultsProcessed $query.TotalRowsExactMinimum = 500000 # run the query $searchExecutor = New-Object Microsoft.SharePoint.Client.Search.Query.SearchExecutor($clientContext) $queryResults = $searchExecutor.ExecuteQuery($query) $clientContext.ExecuteQuery() # enumerate the search results and store the site URLs $queryResults.Value[0].ResultRows | % { $oneDriveForBusinessSiteUrls += $_.Path $resultsProcessed++ } } while($resultsProcessed -lt $queryResults.Value.TotalRows) $oneDriveForBusinessSiteUrls | Out-File -FilePath $reportName
```

###### <a name="BKMK_Script_OD4B_DisableIRM"></a>Script til at deaktivere IRM for OneDrive til virksomheder
Hvis du vil deaktivere IRM for brugernes OneDrive til virksomheder, skal du bruge følgende eksempelscript.

Dette script kræver også den [SharePoint Online klient komponenter SDK](http://www.microsoft.com/en-us/download/details.aspx?id=42038) og [SharePoint Online Management Shell](http://www.microsoft.com/en-us/download/details.aspx?id=35588). Kopier og Indsæt indholdet, Gem filen lokalt (for eksempel "Disable-IRMOnOneDriveForBusiness.ps1") og ændre de   `$sharepointAdminCenterUrl` og `$tenantAdmin` værdier. Angiv OneDrive for Business URL-adresser eller bruge scriptet i forrige afsnit, så du kan importere disse, og derefter køre scriptet manuelt.

*&#42;&#42;Ansvarsfraskrivelse&#42;&#42;*: Dette eksempelscript understøttes ikke under en hvilken som helst Microsoft \\\Standard support-program eller en tjeneste. Dette eksempelscript leveres som BESET uden garanti af nogen art.

```
# Requires Windows PowerShell version 3 <# Description: Disables IRM for OneDrive for Business and can also be used for SharePoint Online libraries and lists Script Installation Requirements: SharePoint Online Client Components SDK http://www.microsoft.com/en-us/download/details.aspx?id=42038 SharePoint Online Management Shell http://www.microsoft.com/en-us/download/details.aspx?id=35588 ====== #> $sharepointAdminCenterUrl = "https://contoso-admin.sharepoint.com" $tenantAdmin = "admin@contoso.com" $webUrls = @("https://contoso-my.sharepoint.com/personal/user1_contoso_com", "https://contoso-my.sharepoint.com/personal/user2_contoso_com", "https://contoso-my.sharepoint.com/personal/person3_contoso_com") <# As an alternative to specifying the URLs as an array, you can import them from a CSV file (no header, single value per row). Then, use: $webUrls = Get-Content -Path "File_path_and_name.csv" #> $listTitle = "Documents" function Load-SharePointOnlineClientComponentAssemblies { [cmdletbinding()] param() process { # assembly location: C:\Program Files\Common Files\microsoft shared\Web Server Extensions\16\ISAPI try { Write-Verbose "Loading Assembly: Microsoft.Office.Client.Policy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.Office.Client.Policy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null Write-Verbose "Loading Assembly: Microsoft.Office.Client.TranslationServices, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.Office.Client.TranslationServices, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.DocumentManagement, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.DocumentManagement, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Publishing, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Publishing, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Runtime, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Runtime, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Search.Applications, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Search.Applications, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Search, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Search, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Taxonomy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Taxonomy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.UserProfiles, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.UserProfiles, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null return $true } catch { if($_.Exception.Message -match "Could not load file or assembly") { Write-Error -Message "Unable to load the SharePoint Server 2013 Client Components.`nDownload Location: http://www.microsoft.com/en-us/download/details.aspx?id=42038" } else { Write-Error -Exception $_.Exception } return $false } } } function Load-SharePointOnlineModule { [cmdletbinding()] param() process { do { # Installation location: C:\Program Files\SharePoint Online Management Shell\Microsoft.Online.SharePoint.PowerShell $spoModule = Get-Module -Name Microsoft.Online.SharePoint.PowerShell -ErrorAction SilentlyContinue if(-not $spoModule) { try { Import-Module Microsoft.Online.SharePoint.PowerShell -DisableNameChecking return $true } catch { if($_.Exception.Message -match "Could not load file or assembly") { Write-Error -Message "Unable to load the SharePoint Online Management Shell.`nDownload Location: http://www.microsoft.com/en-us/download/details.aspx?id=35588" } else { Write-Error -Exception $_.Exception } return $false } } else { return $true } } while(-not $spoModule) } } function Remove-IrmConfiguration { [cmdletbinding()] param( [parameter(Mandatory=$true)][Microsoft.SharePoint.Client.List]$List ) process { Write-Verbose "Disabling IRM Configuration on '$($List.Title)'" $List.IrmEnabled = $false $List.IrmExpire  = $false $List.IrmReject  = $false $List.InformationRightsManagementSettings.Reset() } end { if($List) { Write-Verbose "Committing IRM configuration settings on '$($list.Title)'" $list.InformationRightsManagementSettings.Update() $list.Update() $script:clientContext.Load($list) $script:clientContext.ExecuteQuery() } } } function Get-CredentialFromCredentialCache { [cmdletbinding()] param([string]$CredentialName) #if( Test-Path variable:\global:CredentialCache ) if( Get-Variable O365TenantAdminCredentialCache -Scope Global -ErrorAction SilentlyContinue ) { if($global:O365TenantAdminCredentialCache.ContainsKey($CredentialName)) { Write-Verbose "Credential Cache Hit: $CredentialName" return $global:O365TenantAdminCredentialCache[$CredentialName] } } Write-Verbose "Credential Cache Miss: $CredentialName" return $null } function Add-CredentialToCredentialCache { [cmdletbinding()] param([System.Management.Automation.PSCredential]$Credential) if(-not (Get-Variable CredentialCache -Scope Global -ErrorAction SilentlyContinue)) { Write-Verbose "Initializing the Credential Cache" $global:O365TenantAdminCredentialCache = @{} } Write-Verbose "Adding Credential to the Credential Cache" $global:O365TenantAdminCredentialCache[$Credential.UserName] = $Credential } # load the required assemblies and Windows PowerShell modules if(-not ((Load-SharePointOnlineClientComponentAssemblies) -and (Load-SharePointOnlineModule)) ) { return } # Add the credentials to the client context and SharePoint Online service connection # check for cached credentials to use $o365TenantAdminCredential = Get-CredentialFromCredentialCache -CredentialName $tenantAdmin if(-not $o365TenantAdminCredential) { # when credentials are not cached, prompt for the tenant admin credentials $o365TenantAdminCredential = Get-Credential -UserName $tenantAdmin -Message "Enter the password for the Office 365 admin" if(-not $o365TenantAdminCredential -or -not $o365TenantAdminCredential.UserName -or $o365TenantAdminCredential.Password.Length -eq 0 ) { Write-Error -Message "Could not validate the supplied tenant admin credentials" return } # add the credentials to the cache Add-CredentialToCredentialCache -Credential $o365TenantAdminCredential } # connect to Office365 first, required for SharePoint Online cmdlets to run Connect-SPOService -Url $sharepointAdminCenterUrl -Credential $o365TenantAdminCredential # enumerate each of the specified site URLs foreach($webUrl in $webUrls) { $grantedSiteCollectionAdmin = $false try { # establish the client context and set the credentials to connect to the site $script:clientContext = New-Object Microsoft.SharePoint.Client.ClientContext($webUrl) $script:clientContext.Credentials = New-Object Microsoft.SharePoint.Client.SharePointOnlineCredentials($o365TenantAdminCredential.UserName, $o365TenantAdminCredential.Password) # initialize the site and web context $script:clientContext.Load($script:clientContext.Site) $script:clientContext.Load($script:clientContext.Web) $script:clientContext.ExecuteQuery() # load and ensure the tenant admin user account if present on the target SharePoint site $tenantAdminUser = $script:clientContext.Web.EnsureUser($o365TenantAdminCredential.UserName) $script:clientContext.Load($tenantAdminUser) $script:clientContext.ExecuteQuery() # check if the tenant admin is a site admin if( -not $tenantAdminUser.IsSiteAdmin ) { try { # grant the tenant admin temporary admin rights to the site collection Set-SPOUser -Site $script:clientContext.Site.Url -LoginName $o365TenantAdminCredential.UserName -IsSiteCollectionAdmin $true | Out-Null $grantedSiteCollectionAdmin = $true } catch { Write-Error $_.Exception return } } try { # load the list orlibrary using CSOM $list = $null $list = $script:clientContext.Web.Lists.GetByTitle($listTitle) $script:clientContext.Load($list) $script:clientContext.ExecuteQuery() Remove-IrmConfiguration -List $list } catch { Write-Error -Message "Error setting IRM configuration on site: $webUrl.`nError Details: $($_.Exception.ToString())" } } finally { if($grantedSiteCollectionAdmin) { # remove the temporary admin rights to the site collection Set-SPOUser -Site $script:clientContext.Site.Url -LoginName $o365TenantAdminCredential.UserName -IsSiteCollectionAdmin $false | Out-Null } } } Disconnect-SPOService -ErrorAction SilentlyContinue
```

## <a name="BKMK_Office2013Configuration"></a>2016 Office og Office-2013: Konfiguration til klienter
Da disse nyere versioner af Office har indbygget understøttelse af Azure RMS, kræves ingen konfiguration af klientcomputer til at understøtte oplysninger rights management (IRM)-funktioner for programmer som Word, Excel, PowerPoint, Outlook og Outlook Web App. Alle brugere, der har at gøre er at logge på deres Office-programmer med deres [!INCLUDE[o365_1](../Token/o365_1_md.md)] legitimationsoplysninger, og de kan beskytte filer og e-mails og bruge filer og e-mails, der er beskyttet af andre.

Vi anbefaler dog, at du supplere disse programmer med Rights Management Deling af programmet, så brugere får fordelen af Office-tilføjelsesprogram. Yderligere oplysninger finder du i [Rights Management deling program: Installation og konfiguration til klienter](../Topic/Configuring_Applications_for_Azure_Rights_Management.md#BKMK_SharingApp) afsnit i dette emne.

## <a name="BKMK_Office2010Configuration"></a>Office 2010: Konfiguration til klienter
For klientcomputerne skal bruge Azure RMS med Office 2010, skal de have installeret Deling Rights Management-program til Windows. Der kræves ingen yderligere konfiguration, bortset fra brugere skal logge på med deres [!INCLUDE[o365_1](../Token/o365_1_md.md)] legitimationsoplysninger, og de kan derefter beskytte filer og bruge filer, der er beskyttet af andre.

Yderligere oplysninger om rettighedsstyring, der deler programmet, kan du se de [Rights Management deling program: Installation og konfiguration til klienter](../Topic/Configuring_Applications_for_Azure_Rights_Management.md#BKMK_SharingApp) afsnit i dette emne.

## <a name="BKMK_SharingApp"></a>Rights Management deling program: Installation og konfiguration til klienter
Rights Management (RMS) dele af programmet er påkrævet for klientcomputerne skal bruge Azure RMS med Office 2010, og anbefales til alle computere og mobile enheder, der understøtter Azure RMS. RMS, der deler programmet integreres med Office programmer ved at installere en Office-tilføjelsesprogrammet, så brugerne let kan beskytte filer og e-mails direkte fra båndet. Det tilbyder desuden generel beskyttelse af filtyper, der ikke understøttes oprindeligt af Azure RMS og et dokument, websted for brugere at registrere og fjerne filer, som de har beskyttet.

### <a name="BKMK_SharingAppforWindows"></a>Deling af programmer til Windows RMS: Installation og konfiguration
For at installere og konfigurere RMS deling ansøgning om Windows til en enterprise-installation, finder du på [Rights Management deling program administratorvejledningen](http://technet.microsoft.com/library/dn339003.aspx).

> [!TIP]
> Du kan hurtigt installere og teste RMS deling ansøgning om en enkelt computer, se [hente og installere rettighedsstyring, der deler programmet](http://technet.microsoft.com/library/dn574734.aspx) fra den [Rights Management deling program brugervejledningen](http://technet.microsoft.com/library/dn339006.aspx).

### <a name="BKMK_SharingAppMovileDevices"></a>RMS deling ansøgning om mobile platforme: Installation
Hvis du vil installere RMS Deling af programmer til mobile platforme, kan du hente den relevante app ved hjælp af hyperlinkene på den [Microsoft Rights Management side](http://go.microsoft.com/fwlink/?LinkId=303970). Ingen konfiguration for at bruge Azure RMS med denne app.

## <a name="BKMK_RMSAPIs"></a>Andre programmer, der understøtter den RMS APIs: Installation og konfiguration
Denne kategori omfatter line of business-programmer, der er udviklet internt ved hjælp af RMS-SDK og programmer fra softwareleverandører, der er skrevet ved hjælp af RMS-SDK. Følg vejledningen, der følger med programmet til disse programmer.

## Næste trin
Når du har konfigureret dine programmer til at understøtte Azure Rights Management, kan du bruge den [Køreplan for Azure Rights Management installation](../Topic/Azure_Rights_Management_Deployment_Roadmap.md) til at kontrollere, om der er andre konfigurationstrin, kan du gøre, før du kaster dig [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] til brugere og administratorer. Hvis ikke, skal du se [Ved hjælp af Azure rettighedsstyring](../Topic/Using_Azure_Rights_Management.md) for de næste trin.

## Se også
[Konfiguration af Azure rettighedsstyring](../Topic/Configuring_Azure_Rights_Management.md)

