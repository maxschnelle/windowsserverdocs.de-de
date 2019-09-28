---
title: Bereitstellen der Druck Passthrough-Authentifizierung für Windows Server Hybrid Cloud
description: Einrichten von Microsoft Hybrid Cloud Print mit Passthrough-Authentifizierung
ms.prod: windows-server
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
ms.openlocfilehash: e9d461e2e9442e9473a6d2c9b13d9ede17361348
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71370397"
---
# <a name="deploy-windows-server-hybrid-cloud-print-with-passthrough-authentication"></a>Bereitstellen von Windows Server Hybrid Cloud Print mit Passthrough-Authentifizierung

>Gilt für: Windows Server 2016

In diesem Thema für IT-Administratoren wird die End-to-End-Bereitstellung der Microsoft Hybrid Cloud Print-Lösung beschrieben. Diese Lösung wird auf vorhandenen Windows-Servern ausgeführt, die als Druck Server ausgeführt werden, und ermöglicht Azure Active Directory verbundenen und MDM-verwalteten Geräten das Auffinden und Drucken in von der Organisation verwalteten Druckern.

## <a name="pre-requisites"></a>Voraussetzungen

Es gibt eine Reihe von Abonnements, Diensten und Computern, die Sie vor dem Starten dieser Installation erwerben müssen. Sie lauten wie folgt:

-   Premium-Abonnement Azure AD
    
    Ein Testabonnement für Azure finden [Sie unter Einstieg in ein Azure-Abonnement](https://azure.microsoft.com/trial/get-started-active-directory/). 

-   MDM-Dienst, z. b. InTune
    
    Ein Testabonnement für InTune finden Sie unter [Microsoft InTune](https://www.microsoft.com/en-us/cloud-platform/microsoft-intune).

-   Windows Server wird als Active Directory ausgeführt

    Weitere [Informationen finden Sie unterschritt für Schritt: Einrichten von Active Directory in Windows Server 2016](https://blogs.technet.microsoft.com/canitpro/2017/02/22/step-by-step-setting-up-active-directory-in-windows-server-2016/)für Hilfe beim Einrichten von Active Directory.

-   In die Domäne eingebundener Windows Server 2016, ausgeführt als Druck Server
    
    Informationen zum Installieren von Rollen und Rollen Diensten unter Windows Server finden [Sie unter Installieren von Rollen, Rollen Diensten und Features mithilfe des Assistenten zum Hinzufügen von Rollen und Features](https://docs.microsoft.com/windows-server/administration/server-manager/install-or-uninstall-roles-role-services-or-features#BKMK_installarfw).

-   Azure AD Connect
    
    Hilfe zum Einrichten Azure AD Connect finden Sie unter [benutzerdefinierte Installation von Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-get-started-custom).

-   Azure-Anwendung proxyconnector auf einem separaten Windows Server-Computer mit Domänen Verknüpfung
    
    Hilfe zum Einrichten Azure-Anwendung proxyconnectors finden Sie unter [Get Started with Application Proxy und install the Connector](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-enable).

-   Öffentlicher Domänen Name
    
    Sie können den Domänen Namen verwenden, der von Azure für Sie erstellt wurde, oder einen eigenen Domänen Namen erwerben.

## <a name="deployment-steps"></a>Bereitstellungsschritte

In diesem Leitfaden werden fünf (5) Installationsschritte erläutert:

- Schritt 1: Installieren von Azure AD Connect für die Synchronisierung zwischen Azure AD und lokalem AD
- Schritt 2: Installieren von Hybrid Cloud Print Package auf dem Druck Server
- Schritt 3: Installieren von Azure-Anwendung Proxy (AAP) mit Passthrough-Authentifizierung
- Schritt 4: Konfigurieren der erforderlichen MDM-Richtlinien
- Schritt 5: Freigegebene Drucker veröffentlichen

### <a name="step-1---install-azure-ad-connect-to-sync-between-azure-ad-and-on-premises-ad"></a>Schritt 1: Installieren von Azure AD Connect für die Synchronisierung zwischen Azure AD und lokalem AD
1. Laden Sie auf dem Computer mit Windows Server Active Directory die Azure AD Connect Software herunter.
2. Starten Sie das Installationspaket Azure AD Connect, und wählen Sie **Express Einstellungen verwenden** .
3. Geben Sie die im Installationsprozess angeforderten Informationen ein, und klicken Sie auf **Installieren** .

### <a name="step-2---install-hybrid-cloud-print-package-on-the-print-server"></a>Schritt 2: Installieren von Hybrid Cloud Print Package auf dem Druck Server

1. Installieren der Hybrid Cloud-Druck-PowerShell-Module
   - Führen Sie die folgenden Befehle an einer PowerShell-Eingabeaufforderung mit erhöhten Rechten aus
      - `find-module -Name "PublishCloudPrinter"`So überprüfen Sie, ob der Computer die PowerShell-Katalog (psgallery) erreichen kann
      - `install-module -Name "PublishCloudPrinter"`

     > HINWEIS: Möglicherweise wird ein Messaging angezeigt, das besagt, dass "psgallery" ein nicht vertrauenswürdiges Repository ist.  Geben Sie "y" ein, um die Installation fortzusetzen.

2. Installieren der Hybrid Cloud-Drucklösung
    - Wechseln Sie in der gleichen PowerShell-Eingabeaufforderung mit erhöhten Rechten in das Verzeichnis.`C:\Program Files\WindowsPowerShell\Modules\PublishCloudPrinter\1.0.0.0`
    - Führen Sie Folgendes aus: <br>
        `CloudPrintDeploy.ps1 -AzureTenant <Domain name used by Azure AD Connect> -AzureTenantGuid <Azure AD Directory ID>`
3. Konfigurieren der 2 IIS-Endpunkte zur Unterstützung von SSL
   -   Das SSL-Zertifikat kann ein selbst signiertes Zertifikat oder ein von einer vertrauenswürdigen Zertifizierungsstelle (ca) ausgestelltes Zertifikat sein.
   -  Wenn Sie ein selbst signiertes Zertifikat verwenden, stellen Sie sicher, dass das Zertifikat auf die Client Computer importiert wurde.
4. SQLite-Paket installieren
   - Öffnen Sie eine PowerShell-Eingabeaufforderung mit erhöhten Rechten.
   - Führen Sie den folgenden Befehl zum Herunterladen von System. Data. sqlite nuget-Paketen aus. <br>
       `Register-PackageSource -Name nuget.org -ProviderName NuGet -Location https://www.nuget.org/api/v2/ -Trusted -Force`
   - Führen Sie den folgenden Befehl aus, um die Pakete zu installieren<br>
   `Install-Package system.data.sqlite [-requiredversion x.x.x.x] -providername nuget`

   > HINWEIS: Es wird empfohlen, die neueste Version herunterzuladen und zu installieren, indem Sie die Option "-Requirements dversion" auslagern.

5. Kopieren Sie die SQLite-DLLs in den Ordner "mopriacloudservice \<webapp bin\> " (**C:\\Inetpub\\\\wwwroot\\mopriacloudservice bin**): <br>
   - Die SQLite-Binärdateien sollten sich im\\Ordner "\\Program Files packagemanagement\\\\nuget Packages" befinden.

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

   > Hinweis: x. x. x. x ist die oben installierte SQLite-Version.

6. Aktualisieren Sie `c:\inetpub\wwwroot\MopriaCloudService\web.config` die Datei so, dass Sie die SQLite-Version x. x. x. \<x\>in die/\<folgenden assemblyBinding\> -Abschnitte einschließt:

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
    -  Herunterladen und Installieren der SQLite Tools Binärdateien von<https://www.sqlite.org/>
    -  Wechseln Sie **zu "\\c: Inetpub\\\\wwwroot mopriacloudservice\\Database** Directory".
    -  Führen Sie den folgenden Befehl aus, um die Datenbank in diesem Verzeichnis zu erstellen:`sqlite3.exe MopriaDeviceDb.db ".read MopriaSQLiteDb.sql"`
    -  Öffnen Sie im Datei-Explorer die Eigenschaften der Datei "mopriadevicedb. DB", um Benutzer/Gruppen hinzuzufügen, die auf der Registerkarte "Sicherheit" in der Datenbank "mopria" veröffentlichen dürfen.
        - Es wird empfohlen, nur die erforderliche Administrator Benutzergruppe hinzuzufügen.
8. Registrieren der 2 Web-App mit Azure AD zur Unterstützung der OAuth2-Authentifizierung
   - Melden Sie sich als globaler Administrator beim Azure AD Mandanten Verwaltungs Portal an.
     1. Registerkarte "App-Registrierungen" zum Hinzufügen eines Druck Endpunkts
        - Anwendung hinzufügen, wählen Sie "neue Anwendungs Registrierung" aus.
        - Geben Sie einen geeigneten Namen an, und wählen Sie "Web-App/API".
        - Anmelde-URL = "<http://MicrosoftEnterpriseCloudPrint/CloudPrint>"
     2. Wiederholen für den Ermittlungs Endpunkt
        - Anmelde-URL = "<http://MopriaDiscoveryService/CloudPrint>"
     3. Wiederholen für die Native Client-Anwendung
        -   Wenn Sie den APP-Namen angeben, stellen Sie sicher, dass Sie "Native Client Application" als "Anwendungstyp" auswählen.
        -   Umleitungs-URI =\<"https://Services-Machine\>-Endpoint/RedirectUrl"
     4. Wechseln Sie in die Native Client-App "Einstellungen".
        -   Kopieren Sie den Wert für "Anwendungs-ID", der für spätere Setup Schritte verwendet werden soll.
        -   Wählen Sie "erforderliche Berechtigungen" aus.
            1.  Klicken Sie auf "hinzufügen"
            2.  Klicken Sie auf API auswählen.
            3.  Suchen Sie nach dem Druck Endpunkt und dem Ermittlungs Endpunkt mit dem Namen, den Sie beim Erstellen des App-Endpunkts definiert haben.
            4.  2 Endpunkte hinzufügen
            5.  Stellen Sie sicher, dass die Option "Delegierte Berechtigungen" für jeden App-Endpunkt aktiviert ist.
            6.  Stellen Sie sicher, dass Sie im unteren Bereich auf die Schaltfläche "Done" klicken.
            7.  Klicken Sie auf "Berechtigungen erteilen", nachdem beide Endpunkte hinzugefügt wurden.  Wählen Sie "Ja", wenn Sie zum Genehmigen der Anforderung aufgefordert werden.
        -   Wechseln Sie zu "Umleitungs-URIs", und fügen Sie die folgenden Umleitungs-URIs zur Liste hinzu:`ms-appx-web://Microsoft.AAD.BrokerPlugin/\<NativeClientAppID\>`
            `ms-appx-web://Microsoft.AAD.BrokerPlugin/S-1-15-2-3784861210-599250757-1266852909-3189164077-45880155-1246692841-283550366`

### <a name="step-3---install-azure-application-proxy-aap-with-passthrough-authentication"></a>Schritt 3: Installieren des Azure-Anwendung Proxys (AAP) mit Passthrough-Authentifizierung
1. Melden Sie sich bei Ihrem Azure AD (AAD)-Mandanten Verwaltungs Portal an.
    - Wählen Sie in der Aad-Menü Liste "Anwendungs Proxy" aus.
    - Klicken Sie oben auf dem Bildschirm auf "Anwendungs Proxy aktivieren".
    - Laden Sie den anwendungsproxyconnector auf einen in die Domäne eingebundener Windows Server-Computer herunter, der als webanwendungsproxy (WAP) fungiert.
2. Melden Sie sich auf dem WAP-Computer als Administrator an, und installieren Sie den anwendungsproxyconnector.
    - Geben Sie während der Installation dem anwendungsproxyconnector die Anmelde Informationen für Ihr Azure-Grundsatz, für das Sie AAP aktivieren möchten, an.
    - Stellen Sie sicher, dass der WAP-Computer mit Ihrem lokalen Active Directory verknüpft ist.
3. Zurück zum Aad-Mandanten Verwaltungs Portal und Hinzufügen der Anwendungs Proxys
   - Wechseln Sie zur Registerkarte **Unternehmensanwendungen** .
   - Klicken Sie auf **neue Anwendung**
   - Wählen Sie **lokale Anwendung aus** , und füllen Sie die Felder aus.
       - Name: Beliebiger Name
       - Interne URL: Dies ist die interne URL des clouddiensts "mopria Discovery", auf den der WAP-Computer zugreifen kann.
       - Externe URL: Entsprechend Ihrer Organisation konfigurieren
       - Methode für die Vorauthentifizierung: Passthrough

     >   Hinweis: Wenn Sie nicht alle oben aufgeführten Einstellungen finden, fügen Sie den Proxy mit den verfügbaren Einstellungen hinzu, und wählen Sie dann den Anwendungs Proxy aus, den Sie soeben erstellt haben, und klicken Sie auf die Registerkarte **Anwendungs Proxy** .

4. Wiederholen Sie den Vorgang 3 (oben) für den unternehmensclouddruckdienst, und geben Sie die interne URL zum Druckdienst der Unternehmens Cloud an

    >   Hinweis: Die unten&lt;erwähnte https://Services-Machine&gt;-Endpoint/MCS-URL sollte die externe URL sein, die Sie für den mopria-clouddienst und/oder den Unternehmens-Cloud-Druckdienst eingerichtet haben.


### <a name="step-4---configure-the-required-mdm-policies"></a>Schritt 4: Konfigurieren der erforderlichen MDM-Richtlinien
- Anmelden bei Ihrem MDM-Anbieter
- Suchen Sie nach der Unternehmens Cloud-druckrichtlinien Gruppe, und konfigurieren Sie die Richtlinien gemäß den folgenden Richtlinien:
  - Cloudprintoauthauthority = https://login.microsoftonline.com/\<Azure AD-Verzeichnis-ID\>
  - Cloudprintoauthclientid = "Anwendungs-ID" Wert der systemeigenen Web-App, die Sie im Azure AD Verwaltungs Portal registriert haben
  - Cloudprinterdiscoveryendpoint = externe URL des Azure-Anwendung Proxy, der in Schritt 3,3 erstellt wurde (muss genau gleich sein, aber ohne nachfolgende/)
  - Mopriadiscoveryresourceid = der APP-ID-URI der Web-App/API für den in Schritt 2,8 registrierten Ermittlungs Endpunkt.  Sie finden diesen unter den Einstellungen > Eigenschaften der app.
  - Cloudprintresourceid = der APP-ID-URI der Web-App/API für den in Schritt 2,8 registrierten Druck Endpunkt. Sie finden diesen unter den Einstellungen > Eigenschaften der app.
  - Discoverymaxprinterlimit = \<eine positive ganze Zahl\>

>   Hinweis: Wenn Sie Microsoft InTune-Dienst verwenden, können Sie diese Einstellungen unter der Kategorie "Cloud Printer" (Cloud Printer) finden.

|InTune-Anzeige Name                     |Richtlinie                         |
|----------------------------------------|-------------------------------|
|URL für Drucker Ermittlung                   |Cloudprinterdiscoveryendpoint  |
|URL der Drucker Zugriffs Autorität            |Cloudprintoauthauthority       |
|Azure Native Client-App-GUID            |Cloudprin"authclientid"        |
|Ressourcen-URI des Druck Diensts              |Cloudprintresourceid           |
|Maximal abzufragende Drucker (nur Mobilgeräte)  |Discoverymaxprinterlimit       |
|Ressourcen-URI für Drucker Ermittlungsdienst  |Mopriadiscoveryresourceid      |


>   Hinweis: Wenn die clouddruckrichtliniengruppe nicht verfügbar ist, der MDM-Anbieter jedoch Oma-URI-Einstellungen unterstützt, können Sie dieselben Richtlinien festlegen.  Weitere Informationen finden Sie in diesem <a href="https://docs.microsoft.com/windows/client-management/mdm/policy-csp-enterprisecloudprint#enterprisecloudprint-cloudprintoauthauthority">Artikel</a> .

- OMA-URI
    - `CloudPrintOAuthAuthority = ./Vendor/MSFT/Policy/Config/EnterpriseCloudPrint/CloudPrintOAuthAuthority`
        - Wert = `https://login.microsoftonline.com/` \<Azure AD Verzeichnis-ID\>
    - `CloudPrintOAuthClientId = ./Vendor/MSFT/Policy/Config/EnterpriseCloudPrint/CloudPrintOAuthClientId`
        - Wert = \<Azure AD Anwendungs-ID der nativen App\>
    - `CloudPrinterDiscoveryEndPoint = ./Vendor/MSFT/Policy/Config/EnterpriseCloudPrint/CloudPrinterDiscoveryEndPoint`
        - Value = externe URL des Azure-Anwendung in Schritt 3,3 erstellten Proxys für den mopria-Ermittlungsdienst (muss genau identisch sein, aber ohne das nachfolgende/)
    - `MopriaDiscoveryResourceId = ./Vendor/MSFT/Policy/Config/EnterpriseCloudPrint/MopriaDiscoveryResourceId`
        - Value = der APP-ID-URI der Web-App/API für den in Schritt 2,8 registrierten Ermittlungs Endpunkt.  Sie finden diesen unter den Einstellungen > Eigenschaften der app.
    - `CloudPrintResourceId = ./Vendor/MSFT/Policy/Config/EnterpriseCloudPrint/CloudPrintResourceId`
        - Value = der APP-ID-URI der Web-App/API für den in Schritt 2,8 registrierten Druck Endpunkt. Sie finden diesen unter den Einstellungen > Eigenschaften der app.
    - `DiscoveryMaxPrinterLimit = ./Vendor/MSFT/Policy/Config/EnterpriseCloudPrint/DiscoveryMaxPrinterLimit`
        - Value = \<eine positive ganze Zahl\>
  
### <a name="step-5---publish-desired-shared-printers"></a>Schritt 5: Veröffentlichen der gewünschten freigegebenen Drucker
1. Installieren des gewünschten Druckers auf dem Druck Server
2. Freigeben des Druckers über die Benutzeroberfläche der Druckereigenschaften
3. Wählen Sie den gewünschten Benutzer Satz aus, der Zugriff gewährt.
4. Speichern Sie die Änderungen, und schließen Sie das Fenster Druckereigenschaften.
5. Öffnen Sie auf einem Windows 10 Fall Creator-Update Computer eine Windows PowerShell-Eingabeaufforderung mit erhöhten Rechten.
   1. Führen Sie die folgenden Befehle aus:
      - `find-module -Name "PublishCloudPrinter"`So überprüfen Sie, ob der Computer die PowerShell-Katalog (psgallery) erreichen kann
      - `install-module -Name "PublishCloudPrinter"`

        >   HINWEIS: Möglicherweise wird ein Messaging angezeigt, das besagt, dass "psgallery" ein nicht vertrauenswürdiges Repository ist.  Geben Sie "y" ein, um die Installation fortzusetzen.

      - Publish-cloudprinter
        - Printer = der Name des freigegebenen Druckers, der definiert wurde
        - Hersteller = Druckerhersteller
        - Model = Drucker Modell
        - Orgloation = eine JSON-Zeichenfolge, die den Drucker Speicherort angibt, z. b.:`{"attrs": [{"category":"country", "vs":"USA", "depth":0}, {"category":"organization", "vs":"Microsoft", "depth":1}, {"category":"site", "vs":"Redmond, WA", "depth":2}, {"category":"building", "vs":"Building 1", "depth":3}, {"category":"floor\_number", "vn":1, "depth":4}, {"category":"room\_name", "vs":"1111", "depth":5}]}`
        - SDDL = SDDL-Zeichenfolge, die die Berechtigungen für den Drucker darstellt. Dies kann erreicht werden, indem Sie die Registerkarte "Sicherheit" der Druckereigenschaften entsprechend ändern und dann den folgenden Befehl an einer Eingabeaufforderung ausführen:`(Get-Printer PrinterName -full).PermissionSDDL`
            e.g. "G:DUD: (A; OICI; FA;;; WD) "

          > HINWEIS: Sie müssen dem Ergebnis im **`O:BA`** obigen Eingabe Aufforderungs Befehl als Präfix hinzufügen, bevor Sie den Wert als SDDL-Einstellung festlegen.  Beispiel: SDDL =`O:BAG:DUD:(A;OICI;FA;;;WD)`

        - DiscoveryEndpoint = https://&lt;Services-Machine-Endpoint&gt;/MCS
        - Printserverendpoint = https://&lt;Services-Machine-Endpoint&gt;/ECP
        - Azureclientid = Anwendungs-ID des registrierten systemeigenen Web-App-Werts von oben
        - Azuretenantguid = Verzeichnis-ID Ihres Azure AD Mandanten
        - Discoveryresourceid = [optional] Anwendungs-ID des clouddiensts für die topria-Ermittlung

        > HINWEIS: Sie können auch alle erforderlichen Parameterwerte in der Befehlszeile eingeben.<br>
        **Publish-cloudprinter** PowerShell-Befehlssyntax: <br>
        Publish-cloudprinter-Printer \<string @ no__t-1-Manufacturer \<string @ no__t-3-Model \<string @ no__t-5-orglokation \<string @ no__t-7-SDDL \<string @ no__t-9-DiscoveryEndpoint \>0string @ no__t-11- Printserverendpoint 2string @ no__t-13-azureclientid 4string @ no__t-15-azuretenantguid 6string @ no__t-17 [-discoveryresourceid 8string @ no__t-19] <br>
        Beispiel Befehl:`publish-cloudprinter -Printer EcpPrintTest -Manufacturer Microsoft -Model FilePrinterEcp -OrgLocation '{"attrs": [{"category":"country", "vs":"USA", "depth":0}, {"category":"organization", "vs":"MyCompany", "depth":1}, {"category":"site", "vs":"MyCity, State", "depth":2}, {"category":"building", "vs":"Building 1", "depth":3}, {"category":"floor\_number", "vn":1, "depth":4}, {"category":"room\_name", "vs":"1111", "depth":5}]}' -Sddl "O:BAG:DUD:(A;OICI;FA;;;WD)" -DiscoveryEndpoint https://<services-machine-endpoint>/mcs -PrintServerEndpoint https://<services-machine-endpoint>/ecp -AzureClientId <Native Web App ID> -AzureTenantGuid <Azure AD Directory ID> -DiscoveryResourceId <Proxied Mopria Discovery Cloud Service App ID>`


## <a name="verifing-the-deployment"></a>Überprüfen der Bereitstellung
Auf einem Azure AD eingebundener Gerät, auf dem die MDM-Richtlinien konfiguriert sind:
- Öffnen Sie einen Webbrowser, und wechseln Sie zu&lt;https://Services-Machine-&gt;Endpoint/MCS/Services
- Der JSON-Text, der den Funktions Satz dieses Endpunkts beschreibt, sollte angezeigt werden.
- Wechseln Sie zu "Betriebs Systemeinstellungen\> -\> Geräte-Drucker & Scanner".
    - Der Link "Suchen nach clouddruckern" sollte angezeigt werden.
    - Klicken Sie auf den Link.
    - Klicken Sie auf den Link "Such Speicherort auswählen".
        - Die Hierarchie der Geräte Orte sollte angezeigt werden.
    - Wählen Sie einen Standort aus, und klicken Sie auf **OK** und dann auf die Schaltfläche **Suchen** , um die Drucker
    - Drucker auswählen und auf Schaltfläche " **Gerät hinzufügen** " klicken
    - Drucken Sie nach erfolgreicher Drucker Installation von Ihrer bevorzugten APP an den Drucker.

>   Hinweis: Wenn Sie den "ecpprinttest"-Drucker verwenden, finden Sie die Ausgabedatei auf dem Druck Server Computer unter dem Speicherort "C\\:\\ecptestoutput ecptestprint. XPS".