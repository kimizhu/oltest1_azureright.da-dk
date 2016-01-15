---
description: na
keywords: na
title: Frequently Asked Questions for Azure Rights Management
search: na
ms.date: na
ms.service: rights-management
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 71ce491f-41c1-4d15-9646-455a6eaa157d
---
# Ofte stillede sp&#248;rgsm&#229;l til Azure rettighedsstyring
Nogle ofte stillede spørgsmål til Microsoft [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)], også kendt som Azure RMS:

## Hvad skal jeg installere RMS Azure, og hvordan jeg komme i gang?
Kontroller først, [Krav til Azure rettighedsstyring](../Topic/Requirements_for_Azure_Rights_Management.md), som indeholder oplysninger om sky abonnementsindstillinger, hvordan du kan bruge dine lokale servere med Azure RMS, hvilke installationsscenarier, der er i øjeblikket ikke understøttes, hvilke enheder og programmer understøtter Azure RMS og et link Hvis du har brug for en liste over IP-adresser og domænenavne til firewalls eller proxy-servere. Du kan også kontrollere de andre emner den [Introduktion til Azure rettighedsstyring](../Topic/Getting_Started_with_Azure_Rights_Management.md) afsnit for at få en grundlæggende forståelse af, hvordan [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)] hjælper med at beskytte virksomhedens data, hvordan det fungerer sammen med programmer, hvordan det sammenligner med den lokale version af Active Directory Rights Management og forstå termer og forkortelser, som er specifikke for [!INCLUDE[aad_rightsmanagement_1](../Token/aad_rightsmanagement_1_md.md)].

Når du er klar til at prøve Azure RMS for dig selv, eller installere det til din organisation, bruges den [Køreplan for Azure Rights Management installation](../Topic/Azure_Rights_Management_Deployment_Roadmap.md) en liste over trin med hyperlinks til yderligere oplysninger og trinvise vejledninger instruktioner.

Hvis du har brug for yderligere oplysninger, ressourcer og supportmuligheder, se [Oplysninger og Support til Azure rettighedsstyring](../Topic/Information_and_Support_for_Azure_Rights_Management.md).

## Er det muligt at integrere Azure RMS med min lokale servere?
Ja. Azure RMS kan integreres med dine lokale servere, som Exchange Server, SharePoint og Windows filservere. For at gøre dette skal du bruge den [forbindelse til Rights Management](https://technet.microsoft.com/library/dn375964.aspx). Eller hvis du bare interesseret i at bruge fil klassificering infrastruktur (FC) med Windows Server, kan du bruge den [beskyttelse af RMS-cmdletter](https://technet.microsoft.com/library/mt601315%28v=ws.10%29.aspx). Du kan også synkronisere og samle din Active Directory-domænecontrollere med Azure AD for en mere problemfri oplevelse godkendelse for brugere, for eksempel ved hjælp af [Azure AD Connect](http://azure.microsoft.com/documentation/articles/active-directory-aadconnect/).

Azure RMS automatisk opretter og administrerer XrML certifikater efter behov, så det ikke bruger en lokal PKI. Finde flere oplysninger om, hvordan Azure RMS bruger certifikater til [Gennemgang af, hvordan Azure RMS fungerer: Første brug, beskyttelse af indhold forbrug af indhold](../Topic/What_is_Azure_Rights_Management_.md#BKMK_Walthrough) afsnit i den [Hvad er Azure Rights Management?](../Topic/What_is_Azure_Rights_Management_.md) emne.

## Jeg har en hybrid installation af Exchange med nogle brugere på Exchange Online og andre på Exchange Server, er dette understøttes af Azure RMS?
Absolut, og det dejligt er, at brugere skal kunne beskytte og forbruge beskyttede e-mails og vedhæftede filer på tværs af de to Exchange-installationer uden problemer. For denne konfiguration, [aktivere Azure RMS](https://technet.microsoft.com/library/jj658941.aspx) og [aktivere IRM for Exchange Online](https://technet.microsoft.com/library/dn151475%28v=exchg.150%29.aspx), derefter [installation og konfiguration af RMS-connector](https://technet.microsoft.com/library/dn375964.aspx) til Exchange Server.

## Hvis jeg installerer Azure RMS i produktionen, er min virksomhed derefter låst til løsning eller risiko for at miste adgang til indhold, som vi har beskyttet med Azure RMS?
Nej, du altid forblive i kontrol af dine data og kan fortsætte med at få adgang til det, selv hvis du beslutter at bruge længere Azure RMS. Yderligere oplysninger finder du under [Nedlukning og deaktivere Azure rettighedsstyring](../Topic/Decommissioning_and_Deactivating_Azure_Rights_Management.md).

Men før du fabriksindstillinger Azure RMS installationen, vi vil gerne høre fra dig og forstå, hvorfor du har taget denne beslutning. Hvis Azure RMS ikke opfylder virksomhedens behov, Kontakt os i tilfælde af nye funktioner, der er planlagt i nær fremtid, eller hvis der er alternativer. Sende en e-mail til [AskIPTeam@Microsoft.com](mailto:askipteam@microsoft.com?subject=Planning%20to%20decommission%20Azure%20RMS) og vi vil meget gerne diskutere dine tekniske og forretningsmæssige behov.

## Kan jeg kontrollere, hvilke af mine brugere kan bruge Azure RMS til at beskytte indhold?
Ja, har Azure RMS-onboarding af kontrolelementer i dette scenarie. Yderligere oplysninger finder du i [Konfiguration af onboarding af indstillinger for en faseopdelt installation](../Topic/Activating_Azure_Rights_Management.md#BKMK_OnboardingControls) afsnit i den [Aktivering af Azure rettighedsstyring](../Topic/Activating_Azure_Rights_Management.md) emne.

## Er det muligt at forhindre brugere i at dele beskyttede dokumenter med bestemte organisationer?
En af de største fordele ved Azure RMS er, at den understøtter business-to-business samarbejde uden at du behøver at konfigurere Eksplicitte tillidsforhold til hver partnerorganisation, fordi Azure AD tager sig af godkendelsen for dig.

Der er ingen indstilling for administration for at forhindre brugere i at dele dokumenter sikkert med bestemte organisationer. For eksempel, du vil blokere en organisation, som du ikke har tillid til, eller som har en konkurrerende virksomhed. Forhindrer, at Azure RMS sende beskyttede dokumenter til brugere i disse ville ikke organisationer mening da brugerne kan derefter dele deres dokumenter, der er beskyttet, er sandsynligvis den sidste ting, der skal ske i denne situation! For eksempel ville du kunne identificere, der deler virksomhedens fortrolige dokumenter med hvilke brugere i disse organisationer, som du kan gøre, når dokumentet (eller e-mail) er beskyttet af Azure RMS.

## Når jeg deler et beskyttet dokument med nogen uden for min virksomhed, hvordan brugeren få godkendt?
Azure RMS bruger altid en Azure Active Directory-konto og en tilhørende e-mail-adresse til brugergodkendelse, hvilket gør business-to-business samarbejde problemfri for administratorer. Hvis andre organisationen bruger Azure tjenester, har brugere allerede konti i Azure Active Directory, selvom disse konti oprettes og administreres på stedet og derefter synkroniseres til Azure.  Hvis organisationen har Office 365, under overfladen, Brug denne tjeneste Azure Active Directory også for brugerkonti.  Hvis brugerens organisation ikke har administrerede konti i Azure, brugere kan tilmelde sig [RMS for personer,](https://technet.microsoft.com/library/dn592127.aspx), hvor der oprettes en ikke-administreret Azure lejer og en mappe til organisationen med en konto for brugeren, så brugeren kan derefter godkendes til Azure RMS.

Godkendelsesmetoden for disse konti kan variere, afhængigt af, hvordan administratoren i andre organisationen har konfigureret Azure Active Directory-konti. For eksempel kan de bruge adgangskoder, der er oprettet for disse konti, godkendelse af flere faktorer (MFA), Føderation eller adgangskoder, der er oprettet i Active Directory-domæneservices og derefter synkroniseres til Azure Active Directory.

## Kan jeg føje brugere fra uden for mit firma til brugerdefinerede skabeloner?
Ja.  Oprettelse af brugerdefinerede skabeloner, som slutbrugere (og administratorer) kan vælge fra programmer gør det hurtigt og nemt for dem at anvende beskyttelse af oplysninger, ved hjælp af foruddefinerede politikker, som du angiver. En af indstillingerne i skabelonen, er der er i stand til at få adgang til indholdet, og du kan angive brugere og grupper i organisationen, og brugere uden for organisationen.

Hvis du vil angive brugere uden for din organisation, kan du bruge den [Windows PowerShell-modul til Azure Rights Management](https://technet.microsoft.com/library/jj585012.aspx). Du kan bruge en af følgende indstillinger:

-   **Eksport, redigering og import den opdaterede skabelon**:  Dette er den nemmeste metode, hvis du vil føje disse eksterne brugere til en eksisterende skabelon, der indeholder andre grupper. Brug af [eksport-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727078.aspx) -cmdlet til Eksporter skabelon til en. Csv-fil, du kan redigere for at tilføje eksterne e-mail-adresserne for disse brugere og deres rettigheder til de eksisterende grupper og rettigheder. Brug derefter de [Import-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727077.aspx) -cmdlet til import af denne ændring tilbage til Azure RMS.

-   **Bruger et objekt til definition af rettigheder til at oprette eller opdatere en skabelon**:    Angiv de eksterne e-mail-adresser og deres rettigheder i et rettigheder definition objekt, som du derefter kan bruge til at oprette eller opdatere en skabelon. Du angive rettigheder definition-objekt ved hjælp af den [Ny AadrmRightsDefinition](https://msdn.microsoft.com/library/azure/dn727080.aspx) -cmdlet til at oprette en variabel og derefter oplyse denne variabel til parameteren - RightsDefinition med den [Tilføj AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727075.aspx) cmdlet (til en ny skabelon) eller [sæt AadrmTemplateProperty](https://msdn.microsoft.com/library/azure/dn727076.aspx) cmdlet (Hvis du vil redigere en eksisterende skabelon). Men hvis du tilføjer disse brugere til en eksisterende skabelon, skal du definere rettigheder definition objekter til de eksisterende grupper i skabelonerne og ikke blot eksterne brugere.

Du kan finde flere oplysninger om brugerdefinerede skabeloner, i [Konfiguration af brugerdefinerede skabeloner til Azure rettighedsstyring](../Topic/Configuring_Custom_Templates_for_Azure_Rights_Management.md).

## Hvilke enheder og hvilke filtyper understøttes af Azure RMS?
Se en liste over understøttede enheder i [Klientenheder, der understøtter Azure RMS](../Topic/Requirements_for_Azure_Rights_Management.md#BKMK_SupportedDevices) afsnit i den [Krav til Azure rettighedsstyring](../Topic/Requirements_for_Azure_Rights_Management.md) emne. Da ikke alle de understøttede enheder kan i øjeblikket understøtter alle RMS-funktioner, skal du også kontrollere den [Enheden Klientegenskaber](../Topic/Requirements_for_Azure_Rights_Management.md#BKMK_ClientCapabilities) tabel i det samme emne.

Azure RMS kan understøtte alle filtyper. Til tekst, billede, Microsoft Office (Word, Excel, PowerPoint) filer, .PDF-filer og nogle andre program-filtyper giver Azure RMS indbygget beskyttelse, der omfatter både kryptering og håndhævelse af rettigheder (tilladelser). For alle andre programmer og filtyper indeholder generel beskyttelse filen indkapsling og godkendelse til at bekræfte, hvis en bruger har tilladelse til at åbne filen.

Se en liste over filtypenavne, der har indbygget understøttelse af Azure RMS, den [understøttede filtyper og filtypenavne](http://technet.microsoft.com/library/dn339003.aspx) del af den [Rights Management deling program administratorvejledningen](http://technet.microsoft.com/library/dn339003.aspx). Filtypenavne vises ikke understøttes ved hjælp af Deling af program, der anvender generiske beskyttelse til disse filer automatisk RMS.

## Når understøtter migrering fra AD RMS?
I første omgang understøtter ikke Azure RMS overførsel fra en lokal installation af Rights Management, f.eks AD RMS. Men det understøttes nu.

Yderligere oplysninger finder du under [Overflytning fra AD RMS Azure Rights Management](../Topic/Migrating_from_AD_RMS_to_Azure_Rights_Management.md).

## Vi virkelig vil bruge BYOK sammen med Azure RMS, men vi har lært, at det er ikke kompatibel med Exchange Online – Hvad er dit råd?
Lad ikke denne aktuelle begrænsning forsinke implementeringen Azure RMS. Hvis du har Exchange Online og vil bruge sætter din egen nøgle (BYOK), anbefaler vi, at du implementerer Azure RMS i nøgleadministration standardtilstanden nu, hvor Microsoft opretter og administrerer din nøgle. På den måde får du alle fordelene ved beskyttelse af dine vigtige filer og e-mails nu, med mulighed for at flytte til BYOK senere (for eksempel når Exchange Online understøtter BYOK).

Men hvis virksomhedens politikker, skal du bruge en hardware security module (HSM), og dette ellers ville blokere Azure RMS-installation, en anden mulighed er at anvende Azure RMS med BYOK nu, med reducerede RMS-funktioner til Exchange. Yderligere oplysninger finder du i [BYOK pricing and restrictions](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md#BKMK_Pricing) afsnit i den [Planlægning og implementering af Azure Rights Management lejer nøglen](../Topic/Planning_and_Implementing_Your_Azure_Rights_Management_Tenant_Key.md) emne.

## En funktion, jeg søger efter tilsyneladende ikke beskyttet biblioteker til at arbejde med SharePoint-er understøttelse af denne funktion, der er planlagt?
SharePoint understøtter RMS beskyttede dokumenter ved hjælp af IRM beskyttet i øjeblikket, biblioteker, som ikke understøtter brugerdefinerede skabeloner, dokumentsporing og visse andre funktioner.  Yderligere oplysninger, kan du udvide den   [SharePoint Online- og OneDrive til virksomheder: IRM-konfigurationen](../Topic/Configuring_Applications_for_Azure_Rights_Management.md#BKMK_SharePointOnline) afsnit i den [Hvordan programmer understøtter Azure rettighedsstyring](../Topic/How_Applications_Support_Azure_Rights_Management.md) emne.

Hvis du er interesseret i en bestemt funktion, der endnu ikke understøttes, skal du holde øje med meddelelser på den [RMS-teamets blog](http://blogs.technet.com/b/rms/).

## Hvordan kan jeg konfigurere et drev for virksomheder i SharePoint Online, så brugere kan dele deres filer sikkert med personer i og uden for virksomheden?
Som standard konfigurere som en Office 365-administrator kan du ikke brugere kan gøre.

Ligesom en SharePoint-webstedsadministrator aktiverer og konfigurerer IRM til et SharePoint-bibliotek, som de ejer, vil OneDrive til virksomheder er udviklet til brugere til at aktivere og konfigurere IRM for deres egne OneDrive for Business-bibliotek.  Men ved hjælp af PowerShell, du kan gøre dette for dem. Instruktioner, udvide de [SharePoint Online- og OneDrive til virksomheder: IRM-konfigurationen](../Topic/Configuring_Applications_for_Azure_Rights_Management.md#BKMK_SharePointOnline)  afsnit i den [Konfiguration af programmer for Azure rettighedsstyring](../Topic/Configuring_Applications_for_Azure_Rights_Management.md) artikel.

## Har du et tip eller trick for en vellykket installation af RMS?
Når tilsyn med mange installationer og lytte til vores kunder, partnere oplever konsulenter og supportmedarbejdere – en af de største tip, vi kan videregive fra: **Design og implementering af politikker for enkle rettigheder**.

Da Azure RMS understøtter sikker deling med andre, kan du råd til at være ambitiøs med din rækkevidde til beskyttelse af oplysninger. Men være konservativ med politikker for rettigheder. For mange organisationer kommer den største indflydelse på forretningen fra forebyggelse af lækage af data ved at anvende standard rettigheder-politikskabelon, der begrænser adgangen til personer i organisationen. Du kan selvfølgelig få meget mere detaljeret end, hvis du vil – forhindre personer i udskrivning, redigering etc. Men holde mere detaljeret begrænsninger som undtagelse for dokumenter, der virkelig har brug for sikkerhed på højt niveau, og ikke implementerer disse mere restriktive politikker på én dag, men planen for en mere trinvis tilgang.

## Hvilke funktioner kan eller kan ikke bruges sammen med de forskellige abonnementer til Azure RMS
For betalte abonnementer, der understøtter Azure RMS (Office 365, Azure RMS præmie og Enterprise Mobility pakke), er der visse forskelle i de RMS-funktioner, der understøttes. Se en liste over disse, [tilbud på sammenligning af Rights Management Services (RMS)](http://technet.microsoft.com/dn858608).

Gratis abonnement, der understøtter Azure RMS (RMS for personer) understøtter lang indhold, der er beskyttet af Azure RMS. Yderligere oplysninger finder du under [RMS for enkeltpersoner og Azure rettighedsstyring](../Topic/RMS_for_Individuals_and_Azure_Rights_Management.md).

## Hvor kan jeg få tekniske oplysninger om RMS Azure gratis abonnement (RMS for personer) – for eksempel hvordan det virkelig fungerer, hvordan at overtage styringen af kontiene og hvilke domæner kan ikke bruges?
Du kan finde svar på disse spørgsmål i den [RMS for enkeltpersoner og Azure rettighedsstyring](../Topic/RMS_for_Individuals_and_Azure_Rights_Management.md) emne.

## Hvordan vi få adgang til filer, der er beskyttet af en medarbejder, der nu har forladt organisationen?
Brug funktionen superbruger af Azure RMS, hvor godkendte brugere har fuld ejerrettigheder til alle brug licenser, der blev ydet af organisationens RMS lejer. Denne samme funktion kan autoriserede services indeks og kontrollerer filer, efter behov.

Yderligere oplysninger finder du under [Konfiguration af Superbrugere til Azure Rights Management og Discovery Services eller genoprettelse af Data](../Topic/Configuring_Super_Users_for_Azure_Rights_Management_and_Discovery_Services_or_Data_Recovery.md).

## (Rights Management) kan forhindre skærmbilleder?
Rettighedsstyring blokerer skærmbilleder fra de fleste af de almindeligt anvendte skærmen capture værktøjer, som kan hjælpe med at undgå utilsigtet eller uagtsomt afsløring af fortrolige eller følsomme oplysninger. Der er mange måder, en bruger kan dele data, der vises på skærmen, og tage et skærmbillede er kun én metode. En outputmåde deling viste oplysninger af brugeren kan for eksempel tage et billede af den ved hjælp af deres telefon kamera, genindtaste data eller blot mundtlig vejledning til at overføre det til nogen.

Som disse eksempler viser, forhindre ikke teknologi alene altid brugere i at dele data, der ikke burde. Mens Rights Management kan hjælpe med at beskytte dine vigtige data ved hjælp af godkendelse og brugen af politikker, skal denne rettigheder firmaadministrationsløsning bruges sammen med andre kontrolelementer. For eksempel implementere fysisk sikkerhed, omhyggeligt skærm og overvåge personer, der har godkendt adgang til virksomhedens data og investerer i uddannelse af bruger, så brugerne forstår, hvilke data bør ikke deles.

## Hvor kan jeg finde understøttende oplysning til Azure RMS – som legal, overholdelse og SLA?
Azure RMS understøtter andre tjenester og er også afhængig af andre tjenester. Hvis du leder efter oplysninger, der er relateret til Azure RMS, men ikke om, hvordan Azure RMS-tjenesten, kan du kontrollere følgende ressourcer:

**Juridiske og beskyttelse af personlige oplysninger:**

-   Microsoft Azure aftale oplysninger: [Microsoft Azure aftale](http://azure.microsoft.com/support/legal/subscription-agreement/)

-   Til beskyttelse af personlige oplysninger for Microsoft Azure: [Microsoft Azure erklæring](http://azure.microsoft.com/support/legal/privacy-statement/)

**Sikkerhed, overholdelse og overvågning:**

Se den [Sikkerhed, overholdelse og lovgivningsmæssige krav](../Topic/What_is_Azure_Rights_Management_.md#BKMK_RMScompliance) afsnit i den [Hvad er Azure Rights Management?](../Topic/What_is_Azure_Rights_Management_.md) emne. Derudover gælder følgende:

-   For eksterne certificeringer for Azure RMS: [Microsoft Azure Sikkerhedscenter](http://azure.microsoft.com/support/trust-center/)

-   FIPS 140-oplysninger: [FIPS 140 validering](https://technet.microsoft.com/library/security/cc750357.aspx)

**Aftaler om serviceniveau:**

-   Serviceniveauaftalen for Azure RMS, af det valgte land: [Serviceniveauaftalen](http://microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&amp;DocumentTypeId=37)

-   Serviceniveauaftalen for Azure Active Directory: [Aftaler om serviceniveau](http://azure.microsoft.com/support/legal/sla/)

**Dokumentation:**

-   Azure dokumentationen til Active Directory-websted: [Azure Active Directory](http://azure.microsoft.com/documentation/services/active-directory/)

-   Azure Active Directory-bibliotek: [Azure Active Directory](http://msdn.microsoft.com/library/azure/jj673460.aspx)

-   Office 365-bibliotek: [Office 365](http://technet.microsoft.com/library/dn127064%28v=office.14%29.aspx)

## Hvad skal jeg gøre, hvis mit spørgsmål ikke her?
Brug links og ressourcer, der er angivet i [Oplysninger og Support til Azure rettighedsstyring](../Topic/Information_and_Support_for_Azure_Rights_Management.md).

Der er desuden ofte stillede spørgsmål udviklet til slutbrugere:

-   [Ofte stillede spørgsmål om rettighedsstyring, deling af programmer til Windows](https://technet.microsoft.com/dn467883)

-   [Ofte stillede spørgsmål om rettighedsstyring deling ansøgning om Mobile og Mac-platforme](https://technet.microsoft.com/dn451248)

-   [Ofte stillede spørgsmål om sporing af dokument](http://go.microsoft.com/fwlink/?LinkId=523977)

Denne side med ofte stillede spørgsmål om opdateres jævnligt med nye tilføjelser, der er angivet i de månedlige opdatering meddelelser til dokumentationen på de [Team Microsoft Rights Management (RMS)](http://blogs.technet.com/b/rms/) blog.

> [!TIP]
> Du kan bruge den [docs mærke](http://blogs.technet.com/b/rms/archive/tags/docs/) på bloggen, så du nemt finde disse meddelelser i dokumentationen.

## Se også
[Introduktion til Azure rettighedsstyring](../Topic/Getting_Started_with_Azure_Rights_Management.md)

