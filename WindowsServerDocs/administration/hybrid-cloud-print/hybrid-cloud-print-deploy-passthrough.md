---
title: Bereitstellen von Windows Server Hybrid Cloud-drucken - Pass-Through-Authentifizierung
description: 'Gewusst wie: Drucken von Microsoft Hybrid Cloud mit Pass-Through-Authentifizierung einrichten'
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: Windows Server 2016
ms.tgt_pltfrm: na
ms.topic: ''
ms.assetid: fc239aec-e719-47ea-92fc-d82a7247c5e9
author: msjimwu
ms.author: coreyp
manager: dongill
ms.date: 3/15/2018
ms.openlocfilehash: f372c81cad480ad7d5595892985ae7a9a52ac093
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59887111"
---
# <a name="deploy-windows-server-hybrid-cloud-print-with-passthrough-authentication"></a>Bereitstellen von Windows Server-Hybrid-Cloud-Druck mit Pass-Through-Authentifizierung

>Gilt für: Windows Server 2016

Dieses Thema beschreibt für IT-Administratoren, die End-to-End-Bereitstellung die Microsoft Hybrid Cloud-Print-Lösung. Diese Lösung Ebenen vorhandene Windows-Server als Druckserver und ermöglicht es Azure Active Directory eingebunden, und die MDM-verwaltete ausgeführt wird, verwaltete Geräte, um zu ermitteln und die Ausgabe in der Organisation Drucker.

## <a name="pre-requisites"></a>Voraussetzungen

Es gibt eine Anzahl von Abonnements und Diensten auf Computern, die Sie abrufen, bevor die Installation starten müssen. Sie lauten wie folgt:

-   Azure AD Premium-Abonnement
    
    Finden Sie unter [erste Schritte mit einem Azure-Abonnement](https://azure.microsoft.com/trial/get-started-active-directory/), für ein Testabonnement von Azure. 

-   MDM-Dienst wie Intune
    
    Finden Sie unter [Microsoft Intune](https://www.microsoft.com/en-us/cloud-platform/microsoft-intune), für ein Testabonnement von Intune.

-   Windows Server, die als Active Directory ausgeführt wird

    Finden Sie unter [Schritt für Schritt: Einrichten von Active Directory in Windows Server 2016](https://blogs.technet.microsoft.com/canitpro/2017/02/22/step-by-step-setting-up-active-directory-in-windows-server-2016/), um Hilfe beim Einrichten von Active Directory.

-   Domäne eingebundenen Windows Server 2016 als Print Server ausgeführt wird
    
    Finden Sie unter [Installieren von Rollen, Rollendienste und Features mithilfe des Hinzufügen von Rollen und Features Assistenten](https://docs.microsoft.com/windows-server/administration/server-manager/install-or-uninstall-roles-role-services-or-features#BKMK_installarfw), Informationen zum Installieren von Rollen und Rollendiensten auf Windows Server.

-   Azure AD Connect
    
    Finden Sie unter [benutzerdefinierte Installation von Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-get-started-custom), um Hilfe beim Einrichten von Azure AD Connect.

-   Azure-Anwendungsproxy-Connector in einer anderen Domäne beigetretenen Windows Server-Computer
    
    Finden Sie unter [erste Schritte mit dem Anwendungsproxy und Installieren des Connectors](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-enable), um Hilfe beim Einrichten der Azure-Anwendungsproxy-Connector.

-   Öffentlichen Domänennamen
    
    Sie können den Domänennamen, die von Azure für Sie erstellt oder Ihren eigenen Domänennamen erwerben.

## <a name="deployment-steps"></a>Bereitstellungsschritte

Dieses Handbuch skizziert die Schritte für die Installation fünf (5):

- Schritt 1: Installieren von Azure AD Connect für die Synchronisierung zwischen Azure AD und lokales AD
- Schritt 2: Installieren Sie Hybrid Cloud-Print-Paket auf den Druckserver
- Schritt 3: Installieren von Azure-Anwendungsproxy (AAP) mit Pass-Through-Authentifizierung
- Schritt 4: Konfigurieren Sie die erforderlichen Richtlinien für die Verwaltung mobiler Geräte
- Schritt 5: Veröffentlichen von freigegebenen Druckern

### <a name="step-1---install-azure-ad-connect-to-sync-between-azure-ad-and-on-premises-ad"></a>Schritt 1: Installieren von Azure AD Connect für die Synchronisierung zwischen Azure AD und lokales AD
1. Herunterladen Sie auf dem Windows Server Active Directory-Computer die Azure AD Connect-software
2. Starten Sie das Installationspaket für die Azure AD Connect, und wählen **expresseinstellungen verwenden**
3. Geben Sie die Informationen, die bei der Installation angefordert, und klicken Sie auf **installieren**

### <a name="step-2---install-hybrid-cloud-print-package-on-the-print-server"></a>Schritt 2: Installieren der Druck-Hybrid Cloud-Paket auf dem Druckserver

1. Installieren Sie die Hybrid Cloud-Print-PowerShell-Module
    -  Führen Sie die folgenden Befehle aus einer PowerShell-Eingabeaufforderung
        - `find-module -Name "PublishCloudPrinter"` um sicherzustellen, dass der Computer im PowerShell-Katalog (PSGallery) erreichen kann
        - `install-module -Name "PublishCloudPrinter"`

    > HINWEIS: Sie feststellen, dass ein messaging besagt, dass "PSGallery" mit einem nicht vertrauenswürdigen Repository ist.  Geben Sie "y", um die Installation fortzusetzen.

2. Installieren Sie die Lösung für die Hybrid Cloud-drucken
    - In der gleichen erweiterten PowerShell-Eingabeaufforderung wechseln Sie zu `C:\Program Files\WindowsPowerShell\Modules\PublishCloudPrinter\1.0.0.0`
    - Führen Sie Folgendes aus: <br>
        `CloudPrintDeploy.ps1 -AzureTenant <Domain name used by Azure AD Connect> -AzureTenantGuid <Azure AD Directory ID>`
3.  Konfigurieren Sie die 2 Endpunkte von IIS zur Unterstützung von SSL
    -   Das SSL-Zertifikat kann ein selbstsigniertes Zertifikat oder eines der über eine vertrauenswürdige Zertifizierungsstelle (CA) ausgestellt werden.
    -  Stellen Sie selbstsigniertes Zertifikat verwenden, sicher, dass das Zertifikat importiert wird, um die Client-Computer
4.  Installieren des SQLite-Pakets
    - Öffnen Sie eine PowerShell-Eingabeaufforderung
    - Führen Sie den folgenden Befehl zum System.Data.SQLite Nuget-Pakete herunterladen <br>
        `Register-PackageSource -Name nuget.org -ProviderName NuGet -Location https://www.nuget.org/api/v2/ -Trusted -Force`
    - Führen Sie den folgenden Befehl zum Installieren der Pakete<br>
    `Install-Package system.data.sqlite [-requiredversion x.x.x.x] -providername nuget`

    > HINWEIS: Es wird empfohlen, herunterladen und installieren die neueste Version durch das Weglassen der "-Requiredversion" Option.

5.  Kopieren Sie die SQLite-Dlls für die MopriaCloudService Webapp \<Bin\> Ordner (**C:\\Inetpub\\"Wwwroot"\\MopriaCloudService\\Bin**): <br>
    - Die SQLite-Binärdateien muss auf "\\Programmdateien\\PackageManagement\\NuGet\\Pakete"

            \\System.Data.SQLite.**Core**.x.x.x.x\\lib\\net46\\System.Data.SQLite.dll
            --\> \<bin\>\\System.Data.SQLite.dll  
            \\System.Data.SQLite.**Core**.x.x.x.x\\build\\net46\\x86\\SQLite.Interop.dll
            --\> \<bin\>\\**x86**\\SQLite.Interop.dll  
            \\System.Data.SQLite.**Core**.x.x.x.x\\build\\net46\\x64\\SQLite.Interop.dll
            --\> \<bin\>\\**x64**\\SQLite.Interop.dll
            \\System.Data.SQLite.**Linq**.x.x.x.x\\lib\\net46\\System.Data.SQLite.Linq.dll
            --\> \<bin\>\\System.Data.SQLite.Linq.dll  
            \\System.Data.SQLite.**EF6**.x.x.x.x\\lib\\net46\\System.Data.SQLite.EF6.dll
            --\> \<bin\>\\System.Data.SQLite.EF6.dll

    > Hinweis: x.x.x.x ist die SQLite-Version, die über installiert.

6.  Update der `c:\inetpub\wwwroot\MopriaCloudService\web.config` x.x.x.x die SQLite-Version in der folgenden eingeschlossen \<Runtime\>/\<AssemblyBinding\> Abschnitte:

        <dependentAssembly>
        assemblyIdentity name="System.Data.SQLite" culture="neutral" publicKeyToken="db937bc2d44ff139" /
        <bindingRedirect oldVersion="0.0.0.0-x.x.x.x" newVersion="x.x.x.x" />
        </dependentAssembly>
        <dependentAssembly>
        <assemblyIdentity name="System.Data.SQLite.Core" culture="neutral" publicKeyToken="db937bc2d44ff139" />
        <bindingRedirect oldVersion="0.0.0.0-x.x.x.x" newVersion="x.x.x.x" />
        </dependentAssembly>
        <dependentAssembly>
        <assemblyIdentity name="System.Data.SQLite.EF6" culture="neutral" publicKeyToken="db937bc2d44ff139" />
        <bindingRedirect oldVersion="0.0.0.0-x.x.x.x" newVersion="x.x.x.x" />
        </dependentAssembly>
        <dependentAssembly>
        <assemblyIdentity name="System.Data.SQLite.Linq" culture="neutral" publicKeyToken="db937bc2d44ff139" />
        <bindingRedirect oldVersion="0.0.0.0-x.x.x.x" newVersion="x.x.x.x" />
        </dependentAssembly>

7. Erstellen Sie die SQLite-Datenbank:
    -  Herunterladen Sie und installieren Sie die Tools der SQLite-Binärdateien aus <https://www.sqlite.org/>
    -  Wechseln Sie zu **c:\\Inetpub\\"Wwwroot"\\MopriaCloudService\\Datenbank** Verzeichnis
    -  Führen Sie den folgenden Befehl zum Erstellen der Datenbank in diesem Verzeichnis:  `sqlite3.exe MopriaDeviceDb.db ".read MopriaSQLiteDb.sql"`
    -  Eröffnen Sie im Datei-Explorer die MopriaDeviceDb.db Dateieigenschaften Benutzer/Gruppen hinzufügen, die zulässig sind, zum Veröffentlichen in Mopria-Datenbank in der Registerkarte "Sicherheit"
        - Sollten Sie nur hinzufügen der erforderlichen Admin-Benutzergruppe.
8. Registrieren Sie die 2-Web-app in Azure AD OAuth2-Authentifizierung unterstützen
    -   Melden Sie sich als der globale Administratorrechte, um die Azure AD-Mandanten-Verwaltungsportal
        1. Wechseln Sie "App-Registrierungen" Registerkarte Drucken-Endpunkt hinzufügen
            -   Fügen Sie Anwendung hinzu, wählen Sie "Registrierung einer neuen Anwendung"
            -   Geben Sie einen geeigneten Namen ein, und wählen Sie "-Web-app / API"
            -   Anmelde-URL = "http://MicrosoftEnterpriseCloudPrint/CloudPrint"
        2.  Wiederholen Sie die für den Discovery-Endpunkt
            -   Anmelde-URL = "http://MopriaDiscoveryService/CloudPrint"
        3.  Wiederholen Sie die für die systemeigene Clientanwendung
            -   Wenn Sie den Namen der app bereitstellen möchten, stellen Sie sicher, dass Sie "Systemeigene Clientanwendung" als "Anwendungstyp" auswählen
            -   Redirect URI = "https://\<services-machine-endpoint\>/RedirectUrl"
        4.  Wechseln Sie in der nativen Client-App "Einstellungen"
            -   Kopieren Sie den Wert "Anwendungs-ID", die für Setup später verwendet werden
            -   Wählen Sie "Erforderliche Berechtigungen"
                1.  Klicken Sie auf "Hinzufügen"
                2.  Klicken Sie auf "API auswählen"
                3.  Suchen Sie nach dem Drucken Endpunkt und den Discovery-Endpunkt mit dem Namen, die, den Sie beim Erstellen des app-Endpunkts definiert
                4.  Fügen Sie die 2 Endpunkte hinzu.
                5.  Stellen Sie sicher, dass die Option "Delegierte Berechtigungen" für jeden app-Endpunkt aktiviert ist
                6.  Stellen Sie sicher, dass Sie die Schaltfläche "Fertig", am unteren Rand klicken
                7.  Klicken Sie auf "Erteilen von Berechtigungen", nachdem beide Endpunkte hinzugefügt wurden.  Wählen Sie die Option "Ja", wenn Sie dazu aufgefordert werden, um die Anforderung genehmigen.
            -   Wechseln Sie zu "UMLEITUNGS-URIS", und fügen Sie folgenden umleitungs-URIs zur Liste hinzu: `ms-appx-web://Microsoft.AAD.BrokerPlugin/\<NativeClientAppID\>`
                `ms-appx-web://Microsoft.AAD.BrokerPlugin/S-1-15-2-3784861210-599250757-1266852909-3189164077-45880155-1246692841-283550366`

### <a name="step-3---install-azure-application-proxy-aap-with-passthrough-authentication"></a>Schritt 3: Installieren von Azure-Anwendungsproxy (AAP) mit der Pass-Through-Authentifizierung
1. Melden Sie sich Ihr Azure AD (AAD)-Mandanten-Verwaltungsportal
    - Wählen Sie in der Liste der AAD-Menü "Anwendungsproxy"
    - Klicken Sie auf "Aktivieren des Anwendungsproxys" am oberen Rand des Bildschirms
    - Herunterladen des "Anwendungsproxyconnectors" in eine Domäne eingebundenen Windows Server-Computer, der als Web Application Proxy (WAP) fungiert.
2. Melden Sie sich als Administrator aus, und installieren Sie den "Anwendungsproxy-Connector" auf dem WAP-Computer
    - Während der Installation Geben Sie dem Anwendungsproxy-Connector die Anmeldeinformationen auf Ihre Azure-Prinzip, die Sie AAP aktivieren möchten
    - Stellen Sie sicher, dass der WAP-Computer mit Ihrem lokalen Active Directory verknüpft ist
3. Wechseln Sie zurück zum AAD-Mandanten-Verwaltungsportal, und fügen Sie den Anwendungsproxys
    - Wechseln Sie zu der **unternehmensanwendungen** Registerkarte
    - Klicken Sie auf **neue Anwendung**
    - Wählen Sie **lokale Anwendung** und Füllen der Felder
        - Name: Alle gewünschten Namen
        - Interne URL: Dies ist die interne URL in die Mopria Ermittlung unter der Clouddienst, der den WAP-Computer zugreifen können
        - Externe URL: Konfigurieren Sie nach Bedarf für Ihre Organisation
        - Präauthentifizierungsmethode: Pass-Through-

    >   Hinweis: Wenn Sie die oben genannten Einstellungen nicht finden, fügen Sie den Proxy mit den verfügbaren Einstellungen klicken Sie dann wählen Sie den Anwendungsproxy, die Sie gerade erstellt haben und navigieren Sie zu der **Anwendungsproxy** Registerkarte, und fügen Sie alle oben genannten Informationen.

4. Wiederholen Sie die 3, oben für das Drucken Clouddienst für Unternehmen, und geben Sie die interne URL mit Ihrem Enterprise-Clouddienst drucken

    >   Hinweis: Das https://&lt;Dienste-Computer-Endpoint &gt; /Mcs in URL, die unten genannten muss die Externalurl, die Sie für Ihre Mopria-Cloud-Dienst und/oder Drucken Clouddienst für Unternehmen einrichten.


### <a name="step-4---configure-the-required-mdm-policies"></a>Schritt 4: Konfigurieren Sie die erforderlichen Richtlinien für die Verwaltung mobiler Geräte
- Melden Sie sich Ihre MDM-Anbieter
- Suchen Sie die Enterprise Cloud-Print-Gruppenrichtlinie, und konfigurieren Sie die Richtlinien, die die folgenden Richtlinien befolgen:
    - CloudPrintOAuthAuthority = https://login.microsoftonline.com/\<Azure AD Directory ID\>
    - CloudPrintOAuthClientId = "Application ID"-Wert, der die systemeigenen Web-App, die Sie in Azure AD-Verwaltungsportal registriert.
    - CloudPrinterDiscoveryEndPoint = Externalurl %% Mopria Discovery-Dienst Azure-Anwendungsproxy in Schritt 3.3 erstellt (muss genau der gleiche, jedoch ohne das nachfolgende /)
    - MopriaDiscoveryResourceId = "App-ID URI" der Web-app / API für den Discovery-Endpunkt, der in Schritt 2.8 registriert.  Sie finden diese unter "Einstellungen" die Eigenschaften der app ->
    - CloudPrintResourceId = "App-ID URI" der Web-app / API für den Druck-Endpunkt, der in Schritt 2.8 registriert. Sie finden diese unter "Einstellungen" die Eigenschaften der app ->
    - DiscoveryMaxPrinterLimit = \<eine positive ganze Zahl\>

>   Hinweis: Wenn Sie Microsoft Intune-Dienst verwenden, finden Sie diese Einstellungen in der Kategorie "Cloud-Printer".

|Intune-Anzeigename                     |Richtlinie                         |
|----------------------------------------|-------------------------------|
|URL für druckerermittlung                   |CloudPrinterDiscoveryEndpoint  |
|Autoritäts-URL für Drucker            |CloudPrintOAuthAuthority       |
|GUID für native Azure-Client-app            |CloudPrintOAuthClientId        |
|Druckdienstressourcen-URI              |CloudPrintResourceId           |
|Maximal abgefragte Drucker (nur Mobilgerät)  |DiscoveryMaxPrinterLimit       |
|Ressourcen-Drucker URI  |MopriaDiscoveryResourceId      |


>   Hinweis: Wenn die Cloud-Print-Richtliniengruppe nicht verfügbar ist, aber der MDM-Anbieter unterstützt die OMA-URI-Einstellungen, können Sie die gleichen Richtlinien festlegen.  Finden Sie unter diesem <a href="https://docs.microsoft.com/windows/client-management/mdm/policy-csp-enterprisecloudprint#enterprisecloudprint-cloudprintoauthauthority">Artikel</a> zusätzliche Informationen.

- OMA-URI
    - `CloudPrintOAuthAuthority = ./Vendor/MSFT/Policy/Config/EnterpriseCloudPrint/CloudPrintOAuthAuthority`
        - Wert = `https://login.microsoftonline.com/` \<Azure AD-Verzeichnis-ID\>
    - `CloudPrintOAuthClientId = ./Vendor/MSFT/Policy/Config/EnterpriseCloudPrint/CloudPrintOAuthClientId`
        - Wert = \<systemeigen von Azure AD Anwendungs-ID\>
    - `CloudPrinterDiscoveryEndPoint = ./Vendor/MSFT/Policy/Config/EnterpriseCloudPrint/CloudPrinterDiscoveryEndPoint`
        - Wert = Externalurl %% Mopria Discovery-Dienst Azure-Anwendungsproxy in Schritt 3.3 erstellt (muss genau der gleiche, jedoch ohne das nachfolgende /)
    - `MopriaDiscoveryResourceId = ./Vendor/MSFT/Policy/Config/EnterpriseCloudPrint/MopriaDiscoveryResourceId`
        - Wert = "App-ID URI" der Web-app / API für den Discovery-Endpunkt, der in Schritt 2.8 registriert.  Sie finden diese unter "Einstellungen" die Eigenschaften der app ->
    - `CloudPrintResourceId = ./Vendor/MSFT/Policy/Config/EnterpriseCloudPrint/CloudPrintResourceId`
        - Wert = "App-ID URI" der Web-app / API für den Druck-Endpunkt, der in Schritt 2.8 registriert. Sie finden diese unter "Einstellungen" die Eigenschaften der app ->
    - `DiscoveryMaxPrinterLimit = ./Vendor/MSFT/Policy/Config/EnterpriseCloudPrint/DiscoveryMaxPrinterLimit`
        - Wert = \<eine positive ganze Zahl\>
  
### <a name="step-5---publish-desired-shared-printers"></a>Schritt 5: Veröffentlichen Sie die gewünschte freigegebene Drucker
1. Installieren Sie die gewünschten Drucker auf den Druckserver
2. Freigabe des Druckers, über die Benutzeroberfläche der Drucker-Eigenschaften
3. Wählen Sie die gewünschte Gruppe von Benutzern Zugriff gewähren
4. Speichern Sie die Änderungen zu und schließen Sie das Druckereigenschaftenfenster
5. Öffnen Sie von einem Computer mit Windows 10 Fall creators Update eine Eingabeaufforderung mit erhöhten Windows PowerShell
    1. Führen Sie die folgenden Befehle
        - `find-module -Name "PublishCloudPrinter"` um sicherzustellen, dass der Computer im PowerShell-Katalog (PSGallery) erreichen kann
        - `install-module -Name "PublishCloudPrinter"`

        >   HINWEIS: Sie feststellen, dass ein messaging besagt, dass "PSGallery" mit einem nicht vertrauenswürdigen Repository ist.  Geben Sie "y", um die Installation fortzusetzen.

        - Publish-CloudPrinter
            - Drucker = Name des freigegebenen Drucker, die definiert wurde
            - Hersteller = Druckerhersteller
            - Modell Druckermodell =
            - OrgLocation = ein JSON-Zeichenfolge, die den druckerspeicherort, z. B. angeben:   `{"attrs": [{"category":"country", "vs":"USA", "depth":0}, {"category":"organization", "vs":"Microsoft", "depth":1}, {"category":"site", "vs":"Redmond, WA", "depth":2}, {"category":"building", "vs":"Building 1", "depth":3}, {"category":"floor\_number", "vn":1, "depth":4}, {"category":"room\_name", "vs":"1111", "depth":5}]}`
            - SDDL = SDDL-Zeichenfolge, die Berechtigungen für den Drucker darstellt. Dies kann abgerufen werden, indem der Sicherheitsregisterkarte von Drucker Eigenschaften entsprechend ändern, und klicken Sie dann den folgenden Befehl an einer Eingabeaufforderung ausführen: `(Get-Printer PrinterName -full).PermissionSDDL`
                Beispiel: "G:DUD:(A;OICI;FA;;;WD)"

            > HINWEIS: Sie müssen hinzufügen **`O:BA`** als Präfix für das Ergebnis aus den obigen Befehl Eingabeaufforderung vor dem Festlegen des Werts, wie die SDDL-Einstellung.  Beispiel: SDDL = `O:BAG:DUD:(A;OICI;FA;;;WD)`

            - DiscoveryEndpoint = https://&lt;services-machine-endpoint&gt;/mcs
            - PrintServerEndpoint = https://&lt;services-machine-endpoint&gt;/ecp
            - AzureClientId = Anwendungs-ID des registrierten Web-App mit nativen Werts von oben
            - AzureTenantGuid = Verzeichnis-ID des Azure AD-Mandanten
            - DiscoveryResourceId = [Optional] Anwendungs-ID, die über einen Proxy Mopria-Discovery-Cloud-Diensts

        > HINWEIS: Sie können alle erforderlichen Parameterwerte in der Befehlszeile als auch eingeben.<br>
**Veröffentlichen von CloudPrinter** PowerShell Befehlssyntax: <br>
Veröffentlichen von CloudPrinter-Drucker \<Zeichenfolge\> -Hersteller \<Zeichenfolge\> -Modell \<Zeichenfolge\> - OrgLocation \<Zeichenfolge\> - Sddl \<Zeichenfolge\> - DiscoveryEndpoint \<Zeichenfolge\> - PrintServerEndpoint \<Zeichenfolge\> - AzureClientId \<Zeichenfolge\> - AzureTenantGuid \<Zeichenfolge\> [-DiscoveryResourceId \<Zeichenfolge\>] <br>
Beispielbefehl: `publish-cloudprinter -Printer EcpPrintTest -Manufacturer Microsoft -Model FilePrinterEcp -OrgLocation '{"attrs": [{"category":"country", "vs":"USA", "depth":0}, {"category":"organization", "vs":"MyCompany", "depth":1}, {"category":"site", "vs":"MyCity, State", "depth":2}, {"category":"building", "vs":"Building 1", "depth":3}, {"category":"floor\_number", "vn":1, "depth":4}, {"category":"room\_name", "vs":"1111", "depth":5}]}' -Sddl "O:BAG:DUD:(A;OICI;FA;;;WD)" -DiscoveryEndpoint https://<services-machine-endpoint>/mcs -PrintServerEndpoint https://<services-machine-endpoint>/ecp -AzureClientId <Native Web App ID> -AzureTenantGuid <Azure AD Directory ID> -DiscoveryResourceId <Proxied Mopria Discovery Cloud Service App ID>`


## <a name="verifing-the-deployment"></a>Verifing der Bereitstellung
Klicken Sie auf einen verknüpften Azure AD-Geräten, die die MDM-Richtlinien konfiguriert wurde:
- Öffnen Sie einen Webbrowser, und wechseln Sie zu https://&lt;Dienste-Computer-Endpoint &gt; /Mcs/Services
- Den JSON-Text, der den Satz von Funktionen dieses Endpunkts beschreibt sollte angezeigt werden.
- Wechseln Sie zu "Einstellungen der OS -\> -Geräte:\> Drucker und Scanner"
    - Einen Link "Suche nach clouddruckern" sollte angezeigt werden.
    - Klicken Sie auf den link
    - Klicken Sie auf den Link "Wählen Sie einen Speicherort für die Suche"
        - Die Hierarchie der Gerät-Speicherort sollte angezeigt werden.
    - Wählen Sie einen Speicherort aus, und klicken Sie auf **OK** , und klicken Sie dann auf **Suche** Schaltfläche, um die Drucker suchen
    - Wählen Sie die Drucker aus, und klicken Sie auf **Add Device** Schaltfläche
    - Drucken Sie nach der Druckerinstallation erfolgreich an den Drucker in Ihrer bevorzugten app

>   Hinweis: Wenn den Drucker "EcpPrintTest" verwenden zu können, finden Sie die Ausgabedatei auf dem Druckserver-Computer unter "C:\\ECPTestOutput\\EcpTestPrint.xps" Speicherort.