---
title: Bereitstellen von Windows Server Hybrid Cloud Print
description: Einrichten von Microsoft Hybrid Cloud Print
ms.assetid: fc239aec-e719-47ea-92fc-d82a7247c5e9
ms.topic: how-to
author: msjimwu
ms.author: coreyp
manager: dongill
ms.date: 3/15/2018
ms.openlocfilehash: 3e5b732beb502bb0bf365136947ff380caf71545
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87879913"
---
# <a name="deploy-windows-server-hybrid-cloud-print"></a>Bereitstellen von Windows Server Hybrid Cloud Print

>Gilt für: Windows Server 2016

In diesem Thema für IT-Administratoren wird die End-to-End-Bereitstellung der Microsoft Hybrid Cloud Print (HCP)-Lösung beschrieben. Diese Lösung wird auf vorhandenen Windows-Servern ausgeführt, die als Druck Server ausgeführt werden, und ermöglicht Azure Active Directory (Azure AD) verbundenen und MDM-verwalteten Geräten das Auffinden und Drucken in von der Organisation verwalteten Druckern.

## <a name="pre-requisites"></a>Voraussetzungen

Es gibt eine Reihe von Abonnements, Diensten und Computern, die Sie vor dem Starten dieser Installation erwerben müssen. Dies sind:

- Azure AD Premium-Abonnement.

  Weitere Informationen finden [Sie unter Starten eines Azure-Abonnements](https://azure.microsoft.com/trial/get-started-active-directory/) für ein Testabonnement für Azure.

- MDM-Dienst, z. b. InTune.

  Weitere Informationen finden Sie unter [Microsoft InTune](https://www.microsoft.com/cloud-platform/microsoft-intune) für ein Testabonnement für InTune.

- Computer mit Windows Server 2016 oder höher, auf dem Active Directory ausgeführt wird.

  [Unterschritt Weise Anleitung: Einrichten von Active Directory in Windows Server 2016](https://blogs.technet.microsoft.com/canitpro/2017/02/22/step-by-step-setting-up-active-directory-in-windows-server-2016/) finden Sie Hilfe zum Einrichten Active Directory.

- Ein dedizierter, in eine Domäne eingebundener Windows Server 2016-Computer, der als Druck Server ausgeführt wird.

- Ein dedizierter, in eine Domäne eingebundener Windows Server 2016-Computer, der als Connector-Server ausgeführt wird.

  Weitere Informationen finden Sie Untergrund Legendes [Azure AD anwendungsproxyconnectors](https://docs.microsoft.com/azure/active-directory/manage-apps/application-proxy-connectors) .

- Ein Windows 10 Fall Creator-Update oder ein späterer Computer zum Veröffentlichen von Druckern.

- Öffentlicher Domänen Name.

  Sie können den für Sie von Azure erstellten Domänen Namen (Domain*Name*. onmicrosoft.com) verwenden oder einen eigenen Domänen Namen erwerben. Siehe [Hinzufügen des benutzerdefinierten Domänen Namens mithilfe des Azure Active Directory Portals](https://docs.microsoft.com/azure/active-directory/fundamentals/add-custom-domain)

## <a name="deployment-steps"></a>Bereitstellungsschritte

Die folgenden Schritte gelten für eine typische Hybrid Cloud-Druck Bereitstellung.

### <a name="step-1---install-azure-ad-connect"></a>Schritt 1: Installieren von Azure AD Connect

1. Azure AD Connect synchronisiert Azure AD mit lokalem AD. Laden Sie auf dem Windows Server-Computer mit Active Directory die Azure AD Connect Software mit Express-Einstellungen herunter, und installieren Sie Sie. Weitere Informationen finden [Sie unter Getting Started with Azure AD Connect using Express Settings](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-install-express).

### <a name="step-2---install-application-proxy"></a>Schritt 2: Installieren des Anwendungs Proxys

1. Mithilfe des Anwendungs Proxys können Benutzer in Ihrer Organisation über die Cloud auf lokale Anwendungen zugreifen. Installieren Sie den Anwendungs Proxy auf dem Connector-Server.
    - Installationsanweisungen finden Sie unter [Tutorial: Hinzufügen einer lokalen Anwendung für den Remote Zugriff über den Anwendungs Proxy in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/manage-apps/application-proxy-add-on-premises-application).
    - Eine dedizierte Connectorgruppe wird empfohlen, wenn die Organisation über eine komplexe Netzwerktopologie verfügt. Weitere Informationen finden [Sie unter Veröffentlichen von Anwendungen in getrennten Netzwerken und Orten mithilfe von](https://docs.microsoft.com/azure/active-directory/manage-apps/application-proxy-connector-groups)Stecker

### <a name="step-3---register-and-configure-applications"></a>Schritt 3: registrieren und Konfigurieren von Anwendungen

Um die authentifizierte Kommunikation mit den HCP-Diensten zu ermöglichen, müssen drei Anwendungen erstellt werden: 2 Webanwendungen, die die beiden HCP-Dienste darstellen, und 1 native Anwendung für die Kommunikation mit diesen Diensten.

1. Melden Sie sich an Azure-Portal, um Web-Apps zu registrieren
    - Klicken Sie unter Azure Active Directory auf **App-Registrierungen**  >  **neue Registrierung**.

    ![Aad-App-Registrierung 1](../media/hybrid-cloud-print/AAD-AppRegistration.png)

    - Geben Sie einen APP-Namen für den mopria-Ermittlungsdienst ein. Klicken Sie zum Fertigstellen auf **registrieren** .

    ![Aad-App-Registrierung 2](../media/hybrid-cloud-print/AAD-AppRegistration-Mopria.png)

    - Wiederholen Sie den Vorgang für den Enterprise Cloud Print Service
    - Wiederholen Sie diesen Schritt für Native App
    - Die drei Anwendungen sollten unter **App-Registrierungen**angezeigt werden.

    ![Aad-App-Registrierung 3](../media/hybrid-cloud-print/AAD-AppRegistration-AllApps.png)

2. Machen Sie die API für die 2 Webanwendungen verfügbar.
    - Klicken Sie auf dem Blatt " **App-Registrierungen** " auf die app "mopria Discovery Service", wählen Sie **eine API**verfügbar machen aus, und klicken Sie dann neben Anwendungs-ID-URI auf **festlegen** .

    ![Aad verfügbar machen von API 1](../media/hybrid-cloud-print/AAD-AppRegistration-Mopria-ExposeAPI.png)

    - Klicken Sie auf **Speichern** , ohne den Standardwert für Anwendungs-ID-URI zu ändern. Dieser Wert muss jetzt nur noch festgelegt werden und wird später geändert.

    ![Aad verfügbar machen API 2](../media/hybrid-cloud-print/AAD-AppRegistration-Mopria-ExposeAPI-Save.png)

    - Klicken Sie auf **Bereich hinzufügen**.

    ![Aad verfügbar machen API 3](../media/hybrid-cloud-print/AAD-AppRegistration-Mopria-ExposeAPI-AddScope.png)

    - Geben Sie einen Bereichs Namen an, gestatten Sie Administratoren und Benutzern die Zustimmung, geben Sie die Zustimmungs Beschreibung ein, und klicken Sie dann auf **Bereich hinzufügen** .

    ![Aad verfügbar machen API 4](../media/hybrid-cloud-print/AAD-AppRegistration-Mopria-ExposeAPI-ScopeName.png)

    - Wiederholen Sie den Vorgang für den Enterprise Cloud Print Service Verwenden Sie einen anderen Bereichs Namen und eine Beschreibung der Zustimmung.

    ![Aad verfügbar machen API 5](../media/hybrid-cloud-print/AAD-AppRegistration-ECP-ExposeAPI-ScopeName.png)

3. Hinzufügen von API-Berechtigungen
    - Wechseln Sie zurück zum Blatt App-Registrierungen. Klicken Sie auf die native APP, und wählen Sie API-Berechtigungen aus. Klicken Sie auf **Berechtigung hinzufügen**.

    ![Aad-API-Berechtigung 1](../media/hybrid-cloud-print/AAD-AppRegistration-APIPermission.png)

    - Wechseln Sie zu den von **meiner Organisation verwendeten APIs**, und verwenden Sie das Suchfeld, um den zuvor hinzugefügten mopria Discovery-Dienst zu finden Klicken Sie im Suchergebnis auf den Dienst.

    ![Aad-API-Berechtigung 2](../media/hybrid-cloud-print/AAD-AppRegistration-APIPermission-Mopria.png)

    - Wählen Sie **Delegierte Berechtigungen**aus. Aktivieren Sie das Kontrollkästchen neben dem API-Bereich. Klicken Sie auf **Berechtigungen hinzufügen**.

    ![Aad-API-Berechtigung 3](../media/hybrid-cloud-print/AAD-AppRegistration-APIPermission-Mopria-Add.png)

    - Wiederholen Sie den Vorgang, um dem Enterprise Cloud-Druckdienst Berechtigungen

    ![Aad-API-Berechtigung 4](../media/hybrid-cloud-print/AAD-AppRegistration-APIPermission-ECP-Add.png)

    - Nachdem Sie auf das Blatt "API-Berechtigungen" zurückgekehrt sind, warten Sie 10 Sekunden, bevor Sie auf die Zustimmung des Haupt **Administrators klicken.**

    ![Aad-API-Berechtigung 5](../media/hybrid-cloud-print/AAD-AppRegistration-APIPermission-GrantConsent.png)

    - Wenn Sie aufgefordert werden, klicken Sie auf **Ja** .

    ![Aad-API-Berechtigung 6](../media/hybrid-cloud-print/AAD-AppRegistration-APIPermission-GrantConsent-Yes.png)

    - Vergewissern Sie sich, dass die Spalte Status der API-Berechtigung mit grünen Häkchen angezeigt wird.

    ![Aad-API-Berechtigung 7](../media/hybrid-cloud-print/AAD-AppRegistration-APIPermission-Verify.png)

4. Konfigurieren des Anwendungs Proxys für die Webanwendungen
    - Wechseln Sie zu **Azure Active Directory**  >  **Unternehmensanwendungen**  >  **alle Anwendungen**. Suchen Sie nach dem Dienst "mopria Discovery", und klicken Sie darauf.

    ![Aad-App-Proxy 1](../media/hybrid-cloud-print/AAD-EnterpriseApp-AllApps.png)

    - Klicken Sie auf **Anwendungs Proxy**. Geben Sie die interne URL im Format ein `https://<fully qualified domain name of the Print Server>/mcs/` . Klicken Sie zum Fertigstellen auf " **Speichern** ".

    ![Aad-App-Proxy 2](../media/hybrid-cloud-print/AAD-EnterpriseApp-Mopria-AppProxy.png)

    - Wiederholen Sie den Vorgang für den Enterprise Cloud Print Service Beachten Sie, dass die interne URL ist `https://<fully qualified domain name of the Print Server>/ecp/` .

    ![Aad-App-Proxy 3](../media/hybrid-cloud-print/AAD-EnterpriseApp-ECP-AppProxy.png)

    - Wechseln Sie zu **Azure Active Directory** > **App-Registrierungen**. Klicken Sie auf den mopria Discovery-Dienst. Beachten Sie, dass unter **Übersicht**der Anwendungs-ID-URI von der Standardeinstellung in die externe URL unter **Anwendungs Proxy**geändert wurde. Der URI wird bei der Druck Server Einrichtung, in der Client-MDM-Richtlinie und bei der Veröffentlichung des Druckers verwendet.

    ![Aad-App-Proxy 4](../media/hybrid-cloud-print/AAD-AppRegistration-Mopria-Overview.png)

5. Zuweisen von Benutzern zu Anwendungen
    - Wechseln Sie zu **Azure Active Directory**  >  **Unternehmensanwendungen**  >  **alle Anwendungen**. Suchen Sie nach dem mopria Discovery-Dienst, und klicken Sie darauf.
    - Klicken Sie entweder auf **Benutzer und Gruppen** , und weisen Sie **Benutzer zu,** oder klicken Sie auf **Eigenschaften** , und ändern Sie die **Benutzer Zuweisung erforderlich?**
    - Wiederholen Sie den Vorgang für den Enterprise Cloud Print Service

6. Umleitungs-URI in der nativen App konfigurieren
    - Wechseln Sie zu **Azure Active Directory** > **App-Registrierungen**. Klicken Sie auf die native app. Wechseln Sie zu **Übersicht** , und kopieren Sie die **Anwendungs-ID (Client)**.

    ![Aad-Umleitungs-URI 1](../media/hybrid-cloud-print/AAD-AppRegistration-Native-Overview.png)

    - Wechseln Sie zu **Authentifizierung**. Ändern Sie das Dropdown Feld **Typ** in `Public...` , und geben Sie zwei Umleitungs-URIs im folgenden Format ein, wobei `<NativeClientAppID>` aus dem vorherigen Schritt besteht:

        `ms-appx-web://Microsoft.AAD.BrokerPlugin/<NativeClientAppID>`

        `ms-appx-web://Microsoft.AAD.BrokerPlugin/S-1-15-2-3784861210-599250757-1266852909-3189164077-45880155-1246692841-283550366`

    ![Aad-Umleitungs-URI 2](../media/hybrid-cloud-print/AAD-AppRegistration-Native-Authentication.png)

    - Klicken Sie zum Fertigstellen auf **Speichern** .

### <a name="step-4---setup-the-print-server"></a>Schritt 4: Einrichten des Druck Servers

1. Stellen Sie sicher, dass alle verfügbaren Windows Update auf dem Druck Server installiert sind. Hinweis: Server 2019 muss für die Erstellung 17763,165 oder höher gepatcht werden.
    - Installieren Sie die folgenden Server Rollen:
        - Druck Server Rolle
        - Internetinformationsdienste (IIS)
    - Ausführliche Informationen zum Installieren von Server Rollen finden [Sie unter Installieren von Rollen, Rollen Diensten und Features mithilfe des Assistenten zum Hinzufügen von Rollen und Features](https://docs.microsoft.com/windows-server/administration/server-manager/install-or-uninstall-roles-role-services-or-features#BKMK_installarfw) .

    ![Druck Server Rollen](../media/hybrid-cloud-print/PrintServer-Roles.png)

2. Installieren Sie die PowerShell-Module für Hybrid Cloud Print.
    - Führen Sie die folgenden Befehle an einer PowerShell-Eingabeaufforderung mit erhöhten Rechten aus:

        `find-module -Name PublishCloudPrinter`So überprüfen Sie, ob der Computer die PowerShell-Katalog (psgallery) erreichen kann

        `install-module -Name PublishCloudPrinter`

    > Hinweis: möglicherweise wird ein Messaging angezeigt, das besagt, dass "psgallery" ein nicht vertrauenswürdiges Repository ist.  Geben Sie "y" ein, um die Installation fortzusetzen.

    ![Druck Server veröffentlichen des clouddruckers](../media/hybrid-cloud-print/PrintServer-PublishCloudPrinter.png)

3. Installieren Sie die Hybrid Cloud-Drucklösung.
    - Wechseln Sie in der gleichen PowerShell-Eingabeaufforderung mit erhöhten Rechten zum folgenden Verzeichnis (Anführungszeichen erforderlich):

        `C:\Program Files\WindowsPowerShell\Modules\PublishCloudPrinter\1.0.0.0`

    - Ausführen

        `.\CloudPrintDeploy.ps1 -AzureTenant <Azure Active Directory domain name> -AzureTenantGuid <Azure Active Directory ID>`

    - Informationen zum Azure Active Directory Domänen Namen finden Sie im folgenden Screenshot.

    ![Druck Server Vorgehensweise beim erhalten eines Aad-Domänen Namens](../media/hybrid-cloud-print/PrintServer-GetAADDomainName.png)

    - Die Azure Active Directory-ID finden Sie im nachfolgenden Screenshot.

    ![Druck Server-Cloud-Druck Bereitstellung](../media/hybrid-cloud-print/PrintServer-GetAADId.png)

    - Die Ausgabe des cloudprintbereitstellungs-Skripts sieht wie folgt aus:

    ![Druck Server-Cloud-Druck Bereitstellung](../media/hybrid-cloud-print/PrintServer-CloudPrintDeploy.png)

    - Überprüfen Sie die Protokolldatei, um festzustellen, ob ein Fehler vorliegt:`C:\Program Files\WindowsPowerShell\Modules\PublishCloudPrinter\1.0.0.0\CloudPrintDeploy.log`

4. Führen Sie **regitedit** an einer Eingabeaufforderung mit erhöhten Rechten aus. Wechseln Sie zu Computer \ HKEY_LOCAL_MACHINE \software\microsoft\windows\currentversion\cloudprint\enterprisecloudprintservice.
    - Stellen Sie sicher, dass azureaudience auf den Anwendungs-ID-URI der Unternehmens Cloud-Druck-App festgelegt ist
    - Stellen Sie sicher, dass für azuretenant der Azure AD Domänen Name festgelegt ist.

    ![ECP-Registrierungsschlüssel für den Druck Server](../media/hybrid-cloud-print/PrintServer-RegEdit-ECP.png)

5. Wechseln Sie zu "Computer \ HKEY_LOCAL_MACHINE \software\microsoft\windows\currentversion\cloudprint\mopriadiscoveryservice".
    - Stellen Sie sicher, dass azureaudience der Anwendungs-ID-URI der mopria Discovery Service-APP ist.
    - Stellen Sie sicher, dass azuretenant der Azure AD Domänen Name ist.
    - Stellen Sie sicher, dass URL der Anwendungs-ID-URI der mopria Discovery Service-APP ist.

    ![Druck Server-mopria-Registrierungsschlüssel](../media/hybrid-cloud-print/PrintServer-RegEdit-Mopria.png)

6. Führen Sie **iisreset** an einer PowerShell-Eingabeaufforderung mit erhöhten Rechte aus. Dadurch wird sichergestellt, dass alle im vorherigen Schritt vorgenommenen Registrierungs Änderungen wirksam werden.

7. Konfigurieren Sie die IIS-Endpunkte zur Unterstützung von SSL.
    - Das SSL-Zertifikat kann ein selbst signiertes Zertifikat oder ein von einer vertrauenswürdigen Zertifizierungsstelle ausgestelltes Zertifikat sein.
    - Wenn Sie ein selbst signiertes Zertifikat verwenden, **Stellen Sie sicher, dass das Zertifikat auf die Client Computer importiert**wurde.
    - Wenn Sie Ihre Domäne bei einem Drittanbieter registrieren, müssen Sie die IIS-Endpunkte mit SSL-Zertifikat konfigurieren. Ausführliche Informationen finden Sie in diesem [Handbuch](https://www.sslsupportdesk.com/microsoft-server-2016-iis-10-10-5-ssl-installation/) .

8. Installieren Sie das SQLite-Paket.
   - Öffnen Sie eine PowerShell-Eingabeaufforderung mit erhöhten Rechten.
   - Führen Sie den folgenden Befehl aus, um die nuget-Pakete System. Data. sqlite herunterzuladen.

        `Register-PackageSource -Name nuget.org -ProviderName NuGet -Location https://www.nuget.org/api/v2/ -Trusted -Force`

   - Führen Sie den folgenden Befehl aus, um die Pakete zu installieren.

        `Install-Package system.data.sqlite [-requiredversion x.x.x.x] -providername nuget`

   > Hinweis: Es wird empfohlen, die neueste Version herunterzuladen und zu installieren, indem Sie die Option-Requirements dversion verlassen.

    ![Druck Server-mopria-Registrierungsschlüssel](../media/hybrid-cloud-print/PrintServer-InstallSQLite.png)

9. Kopieren Sie die SQLite-DLLs in den Ordner "mopriacloudservice webapp bin" (c:\inetpub\wwwroot\mopriacloudservice\bin).
    - Erstellen Sie eine PS1-Datei, die das unten stehende PowerShell-Skript enthält.
    - Ändern Sie die $Version Variable in die SQLite-Version, die Sie im vorherigen Schritt installiert haben.
    - Führen Sie die PS1-Datei an einer PowerShell-Eingabeaufforderung mit erhöhten Rechten aus.

    ```powershell
    $source = \Program Files\PackageManagement\NuGet\Packages
    $core = System.Data.SQLite.Core
    $linq = System.Data.SQLite.Linq
    $ef6 = System.Data.SQLite.EF6
    $version = x.x.x.x
    $target = C:\inetpub\wwwroot\MopriaCloudService\bin

    xcopy /y $source\$core.$version\lib\net46\System.Data.SQLite.dll $target\
    xcopy /y $source\$core.$version\build\net46\x86\SQLite.Interop.dll $target\x86\
    xcopy /y $source\$core.$version\build\net46\x64\SQLite.Interop.dll $target\x64\
    xcopy /y $source\$linq.$version\lib\net46\System.Data.SQLite.Linq.dll $target\
    xcopy /y $source\$ef6.$version\lib\net46\System.Data.SQLite.EF6.dll $target\
    ```

10. Aktualisieren Sie die c:\inetpub\wwwroot\MopriaCloudService\web.config Datei so, dass Sie die SQLite-Version x. x. x. x in die folgenden `<runtime>/<assemblyBinding>` Abschnitte einschließt. Dies ist die gleiche Version, die im vorherigen Schritt verwendet wurde.

    ```xml
    ...
    <dependentAssembly>
    assemblyIdentity name=System.Data.SQLite culture=neutral publicKeyToken=db937bc2d44ff139 /
    <bindingRedirect oldVersion=0.0.0.0-x.x.x.x newVersion=x.x.x.x />
    </dependentAssembly>
    <dependentAssembly>
    <assemblyIdentity name=System.Data.SQLite.Core culture=neutral publicKeyToken=db937bc2d44ff139 />
    <bindingRedirect oldVersion=0.0.0.0-x.x.x.x newVersion=x.x.x.x />
    </dependentAssembly>
    <dependentAssembly>
    <assemblyIdentity name=System.Data.SQLite.EF6 culture=neutral publicKeyToken=db937bc2d44ff139 />
    <bindingRedirect oldVersion=0.0.0.0-x.x.x.x newVersion=x.x.x.x />
    </dependentAssembly>
    <dependentAssembly>
    <assemblyIdentity name=System.Data.SQLite.Linq culture=neutral publicKeyToken=db937bc2d44ff139 />
    <bindingRedirect oldVersion=0.0.0.0-x.x.x.x newVersion=x.x.x.x />
    </dependentAssembly>
    ...
    ```

11. Erstellen Sie die SQLite-Datenbank.
    - Laden Sie die Binärdateien von SQLite Tools herunter, und installieren Sie Sie `https://www.sqlite.org/` .
    - Wechseln Sie zum `c:\inetpub\wwwroot\MopriaCloudService\Database` Verzeichnis.
    - Führen Sie den folgenden Befehl aus, um die Datenbank in diesem Verzeichnis zu erstellen:

        `sqlite3.exe MopriaDeviceDb.db .read MopriaSQLiteDb.sql`

    - Öffnen Sie im Datei-Explorer die Eigenschaften der Datei "mopriadevicedb. DB", um Benutzer oder Gruppen hinzuzufügen, die auf der Registerkarte "Sicherheit" in der Datenbank "mopria" veröffentlichen dürfen. Die Benutzer oder Gruppen müssen lokal Active Directory vorhanden und mit Azure AD synchronisiert werden.
    - Wenn die Lösung in einer nicht Routing fähigen Domäne (z. b. *mydomain*. local) bereitgestellt wird, muss die Azure AD Domäne (z. b. Domain *Name*. onmicrosoft.com oder eine, die von einem Drittanbieter erworben wurde) als UPN-Suffix zu lokalen Active Directory hinzugefügt werden. Dies ist derselbe Benutzer, der Drucker veröffentlichen soll (z. b. admin@*Domain Name*. onmicrosoft.com), kann in der Sicherheitseinstellung der Datenbankdatei hinzugefügt werden. Weitere Informationen finden Sie unter [Vorbereiten einer nicht Routing fähigen Domäne für die Verzeichnis Synchronisierung](https://docs.microsoft.com/office365/enterprise/prepare-a-non-routable-domain-for-directory-synchronization).

    ![Druck Server-mopria-Registrierungsschlüssel](../media/hybrid-cloud-print/PrintServer-SQLiteDB.png)

### <a name="step-5-optional---configure-pre-authentication-with-azure-ad"></a>Schritt 5 \[ \] : Konfigurieren der Vorauthentifizierung mit Azure AD

1. Überprüfen Sie die [Eingeschränkte Kerberos-Delegierung für Single Sign-on zu ihren apps mit dem Anwendungs Proxy](https://docs.microsoft.com/azure/active-directory/manage-apps/application-proxy-configure-single-sign-on-with-kcd).

2. Konfigurieren Sie die lokale Active Directory.
    - Öffnen Sie auf dem Active Directory Computer Server-Manager, und navigieren Sie zu **Tools**  >  **Active Directory Benutzer und Computer**.
    - Navigieren Sie zum Knoten **Computer** , und wählen Sie den Connector-Server aus.
    - Klicken Sie mit der rechten **Properties**Maustaste, und wählen Sie  ->  **Delegation**   Registerkarte "Eigenschaften
    - Wählen Sie **Computer nur bei Delegierungen angegebener Dienste vertrauen aus**.
    - Wählen Sie **beliebiges Authentifizierungsprotokoll verwenden**aus.
    - Unter **Dienste, für die dieses Konto Delegierte Anmelde Informationen vorweisen kann**.
        - Fügen Sie den Dienst Prinzipal Namen (SPN) des Druck Server Computers hinzu.
        - Wählen Sie Host als Diensttyp aus.
    ![Active Directory Delegierung](../media/hybrid-cloud-print/AD-Delegation.png)

3. Vergewissern Sie sich, dass die Windows-Authentifizierung in IIS aktiviert ist.
    - Öffnen Sie auf dem Druck Server Server-Manager > Tools > Internet Informationsdienste-Manager (IIS).
    - Wechseln Sie zum Standort.
    - Doppelklicken Sie auf **Authentifizierung**.
    - Klicken Sie auf **Windows-Authentifizierung** und dann unter **Aktionen**auf **aktivieren** .
    ![IIS-Authentifizierung des Druck Servers](../media/hybrid-cloud-print/PrintServer-IIS-Authentication.png)

4. Einmaliges Anmelden konfigurieren.
    - Wechseln Sie auf Azure-Portal zu **Azure Active Directory**  >  **Unternehmensanwendungen**  >  **alle Anwendungen**.
    - Wählen Sie die app "mopriadiscoveryservice" aus.
    - Wechseln Sie zu **Anwendungs Proxy**. Ändern Sie die Methode für die Vorauthentifizierung in **Azure Active Directory**.
    - Navigieren Sie zu **Single sign-on** (Einmaliges Anmelden). Wählen Sie integrierte Windows-Authentifizierung als Single Sign-on-Methode aus.
    - Legen Sie **interner Anwendungs-SPN** auf den SPN des Druck Server Computers fest.
    - Legen Sie die **Delegierte Anmelde Identität** auf den Benutzer Prinzipal Namen fest.
    - Wiederholen Sie diesen Schritt für die entperiabdruck-app.
    ![Einmalige Anmeldung mit Aad-IWA](../media/hybrid-cloud-print/AAD-SingleSignOn-IWA.png)

### <a name="step-6---configure-the-required-mdm-policies"></a>Schritt 6: Konfigurieren der erforderlichen MDM-Richtlinien

1. Melden Sie sich bei Ihrem MDM-Anbieter an.
2. Suchen Sie nach der Unternehmens Cloud-druckrichtlinien Gruppe, und konfigurieren Sie die Richtlinien gemäß den folgenden Richtlinien:
    - Cloudprintoauthauthority = `https://login.microsoftonline.com/<Azure AD Directory ID>` . Die Verzeichnis-ID finden Sie unter Azure Active Directory > Eigenschaften.
    - Cloudprintoauthclientid = Anwendungs \( Client- \) ID-Wert der systemeigenen app. Sie finden diesen unter Azure Active Directory > App-Registrierungen, > Sie die systemeigene app > Übersicht auswählen.
    - Cloudprinterdiscoveryendpoint = externe URL der mopria Discovery Service-APP. Sie finden diesen unter Azure Active Directory > Unternehmensanwendungen > wählen Sie die app "mopria Discovery Service" > Anwendungs Proxy aus. **Sie muss genau gleich sein, aber ohne das nachfolgende/**.
    - Mopriadiscoveryresourceid = der Anwendungs-ID-URI der mopria Discovery Service-APP. Sie finden dies unter Azure Active Directory > App-Registrierungen > die > Übersicht über den Dienst "mopria Discovery Service APP" auswählen. **Der Wert muss mit dem nachfolgenden/identisch sein**.
    - Cloudprintresourceid = der Anwendungs-ID-URI der Unternehmens-Cloud-Druck-app. Sie finden diesen unter Azure Active Directory > App-Registrierungen > wählen Sie die > Übersicht der unternehmenscloud-Druck-App aus. **Der Wert muss mit dem nachfolgenden/identisch sein**.
    - Discoverymaxprinterlimit = \<a positive integer\> .

> [!NOTE]
> Wenn Sie Microsoft InTune-Dienst verwenden, finden Sie diese Einstellungen unter der Kategorie clouddrucker.

|InTune-Anzeige Name                     |Richtlinie                         |
|----------------------------------------|-------------------------------|
|URL für Drucker Ermittlung                   |Cloudprinterdiscoveryendpoint  |
|URL der Drucker Zugriffs Autorität            |Cloudprintoauthauthority       |
|Azure Native Client-App-GUID            |Cloudprin"authclientid"        |
|Ressourcen-URI des Druck Diensts              |Cloudprintresourceid           |
|Maximal abzufragende Drucker (nur Mobilgeräte)  |Discoverymaxprinterlimit       |
|Ressourcen-URI für Drucker Ermittlungsdienst  |Mopriadiscoveryresourceid      |

> [!NOTE]
> Wenn die clouddruckrichtliniengruppe nicht verfügbar ist, der MDM-Anbieter jedoch Oma-URI-Einstellungen unterstützt, können Sie dieselben Richtlinien festlegen.  Weitere Informationen finden Sie in [diesem](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-enterprisecloudprint#enterprisecloudprint-cloudprintoauthauthority) Artikel.

- Werte für OMA-URI
  - Cloudprintoauthauthority =./Vendor/MSFT/Policy/config/EnterpriseCloudPrint/CloudPrintOAuthAuthority
    - Wert =`https://login.microsoftonline.com/<Azure AD Directory ID>`
  - Cloudprindienst authclientid =./Vendor/MSFT/Policy/config/EnterpriseCloudPrint/CloudPrintOAuthClientId
    - Wert =`<Azure AD Native App's Application ID>`
  - Cloudprinterdiscoveryendpoint =./Vendor/MSFT/Policy/config/EnterpriseCloudPrint/CloudPrinterDiscoveryEndPoint
    - Value = externe URL der "mopria Discovery Service"-app (muss genau gleich sein, aber ohne nachfolgende `/` )
  - Mopriadiscoveryresourceid =./Vendor/MSFT/Policy/config/EnterpriseCloudPrint/MopriaDiscoveryResourceId
    - Value = der Anwendungs-ID-URI der mopria Discovery Service-APP
  - Cloudprintresourceid =./Vendor/MSFT/Policy/config/EnterpriseCloudPrint/CloudPrintResourceId
    - Wert = Anwendungs-ID-URI der Unternehmens-Cloud-Druck-App
  - Discoverymaxprinterlimit =./Vendor/MSFT/Policy/config/EnterpriseCloudPrint/DiscoveryMaxPrinterLimit
    - Value = eine positive ganze Zahl

### <a name="step-7---publish-the-shared-printer"></a>Schritt 7: Veröffentlichen des freigegebenen Druckers

1. Installieren Sie den gewünschten Drucker auf dem Drucker Server.
2. Geben Sie den Drucker über die Benutzeroberfläche der Druckereigenschaften frei.
3. Wählen Sie den gewünschten Benutzer Satz aus, dem der Zugriff gewährt werden soll.
4. Speichern Sie die Änderungen, und schließen Sie das Fenster Druckereigenschaften.
5. Vorbereiten eines Windows 10 Fall Creator-Updates oder eines späteren Computers. Verknüpfen Sie den Computer mit Azure AD, und melden Sie sich als Benutzer an, der mit der lokalen Active Directory synchronisiert ist und über die entsprechende Berechtigung für die Datei "mopriadevicedb. DB" verfügt.
6. Öffnen Sie auf dem Windows 10-Computer eine Windows PowerShell-Eingabeaufforderung mit erhöhten Rechten.
    - Führen Sie die folgenden Befehle aus.
        - `find-module -Name PublishCloudPrinter`So überprüfen Sie, ob der Computer die PowerShell-Katalog (psgallery) erreichen kann
        - `install-module -Name PublishCloudPrinter`

            > Hinweis: möglicherweise wird ein Messaging angezeigt, das besagt, dass "psgallery" ein nicht vertrauenswürdiges Repository ist.  Geben Sie "y" ein, um die Installation fortzusetzen.

        - `Publish-CloudPrinter`
        - Printer = der Name des freigegebenen Druckers. Dieser Name muss genau mit dem Freigabe Namen übereinstimmen, der auf der Registerkarte **Freigabe** der Druckereigenschaften angezeigt wird, die auf dem Druck Server geöffnet ist.

        ![Druckereigenschaften des Druck Servers](../media/hybrid-cloud-print/PrintServer-PrinterProperties.png)

        - Hersteller = Druckerhersteller.
        - Model = Drucker Modell.
        - Orgloation = eine JSON-Zeichenfolge, die den Drucker Speicherort angibt, z. b.

            `{attrs: [{category:country, vs:USA, depth:0}, {category:organization, vs:Microsoft, depth:1}, {category:site, vs:Redmond, WA, depth:2}, {category:building, vs:Building 1, depth:3}, {category:floor_number, vs:1, depth:4}, {category:room_name, vs:1111, depth:5}]}`

        - SDDL = SDDL-Zeichenfolge, die die Berechtigungen für den Drucker darstellt.
            - Melden Sie sich beim Druck Server als Administrator an, und führen Sie dann den folgenden PowerShell-Befehl für den Drucker aus, den Sie veröffentlichen möchten: `(Get-Printer PrinterName -full).PermissionSDDL` .
            - Fügen Sie dem Ergebnis aus dem obigen Befehl **o:BA** als Präfix hinzu. Beispiel: Wenn die Zeichenfolge, die vom vorherigen Befehl zurückgegeben wurde, g:DUD ist: (A; oici; FA;;; WD), dann SDDL = o:Bag: DUD: (A; oici; FA;;; WD).
        - DiscoveryEndpoint = melden Sie sich bei Azure-Portal an, und erhalten Sie dann die Zeichenfolge aus Unternehmensanwendungen > der mopria Discovery Service-APP > Anwendungs Proxy > externe URL. Lassen Sie das nachfolgende/aus.
        - Printserverendpoint = melden Sie sich bei Azure-Portal an, und erhalten Sie dann die Zeichenfolge aus Unternehmensanwendungen > der Unternehmens Cloud-Druck-App > Anwendungs Proxy > externe URL. Lassen Sie das nachfolgende/aus.
        - Azureclientid = Anwendungs-ID der registrierten systemeigenen Anwendung.
        - Azuretenantguid = Verzeichnis-ID Ihres Azure AD Mandanten.
        - Discoveryresourceid = Anwendungs-ID-URI der mopria Discovery Service-Anwendung.

    - Sie können auch alle erforderlichen Parameterwerte in der Befehlszeile eingeben. Die Syntax ist:

        `Publish-CloudPrinter -Printer <string> -Manufacturer <string> -Model <string> -OrgLocation <string> -Sddl <string> -DiscoveryEndpoint <string> -PrintServerEndpoint <string> -AzureClientId <string> -AzureTenantGuid <string> -DiscoveryResourceId <string>`

        Beispiel für einen Befehl:

        `Publish-CloudPrinter -Printer HcpTestPrinter -Manufacturer Manufacturer1 -Model Model1 -OrgLocation '{attrs: [{category:country, vs:USA, depth:0}, {category:organization, vs:MyCompany, depth:1}, {category:site, vs:MyCity, State, depth:2}, {category:building, vs:Building 1, depth:3}, {category:floor_name, vs:1, depth:4}, {category:room_name, vs:1111, depth:5}]}' -Sddl O:BAG:DUD:(A;OICI;FA;;;WD) -DiscoveryEndpoint https://mopriadiscoveryservice-contoso.msappproxy.net/mcs -PrintServerEndpoint https://enterprisecloudprint-contoso.msappproxy.net/ecp -AzureClientId dbe4feeb-cb69-40fc-91aa-73272f6d8fe1 -AzureTenantGuid 8de6a14a-5a23-4c1c-9ae4-1481ce356034 -DiscoveryResourceId https://mopriadiscoveryservice-contoso.msappproxy.net/mcs/`

    - Verwenden Sie den folgenden Befehl, um zu überprüfen, ob der Drucker veröffentlicht wurde.

        `Publish-CloudPrinter -Query -DiscoveryEndpoint <string> -AzureClientId <string> -AzureTenantGuid <string> -DiscoveryResourceId <string>`

        Beispiel für einen Befehl:

        `Publish-CloudPrinter -Query -DiscoveryEndpoint https://mopriadiscoveryservice-contoso.msappproxy.net/mcs -AzureClientId dbe4feeb-cb69-40fc-91aa-73272f6d8fe1 -AzureTenantGuid 8de6a14a-5a23-4c1c-9ae4-1481ce356034 -DiscoveryResourceId https://mopriadiscoveryservice-contoso.msappproxy.net/mcs/`

## <a name="verify-the-deployment"></a>Überprüfen der Bereitstellung

Auf einem Azure AD eingebundener Gerät, auf dem die MDM-Richtlinien konfiguriert sind:
- Öffnen Sie einen Webbrowser, und wechseln Sie zu " https://mopriadiscoveryservice- *Tenant-Name*. msappproxy.net/MCS/Services".
- Der JSON-Text, der den Funktions Satz dieses Endpunkts beschreibt, sollte angezeigt werden.
- Wechseln Sie zu **Einstellungen**  >  **Geräte**  >  **Drucker & Scanner**.
    - Klicken Sie auf **Drucker oder Scanner hinzufügen**.
    - Sie sollten eine Suche nach clouddruckern sehen (oder nach Druckern in meinem Unternehmen auf einem neueren Windows 10-Computer suchen).
    - Klicken Sie auf den Link.
    - Klicken Sie auf den Link Such Speicherort auswählen.
        - Die Hierarchie der Geräte Orte sollte angezeigt werden.
    - Wählen Sie einen Speicherort aus, und klicken Sie auf **OK** und dann auf die Schaltfläche **Suchen** , um die Drucker
    - Wählen Sie Drucker aus, **und klicken Sie** auf die Schaltfläche
    - Nachdem die Drucker Installation erfolgreich war, können Sie Sie aus Ihrer bevorzugten APP an den Drucker drucken.

> Hinweis: Wenn Sie den ecpprinttest-Drucker verwenden, finden Sie die Ausgabedatei auf dem Drucker Server Computer unter C: \\ ecptestoutput \\ ecptestprint. XPS Location.

## <a name="troubleshooting"></a>Problembehandlung

Im folgenden sind häufige Probleme bei der HCP-Bereitstellung

|Fehler |Empfohlene Schritte |
|------|------|
|Cloudprintbereitstellungs-PowerShell-Skript fehlgeschlagen | <ul><li>Stellen Sie sicher, dass Windows Server das neueste Update aufweist.</li><li>Wenn Windows Server Update Services (WSUS) verwendet wird, finden Sie unter Gewusst [wie: Bedarfs gesteuerte Features und Sprachpakete bei Verwendung von WSUS/SCCM](https://docs.microsoft.com/windows/deployment/update/fod-and-lang-packs)Weitere Informationen.</li></ul> |
|Fehler bei der SQLite-Installation mit der folgenden Meldung: Abhängigkeits Schleife für Paket "System. Data. sqlite" erkannt | Install-package System. Data. sqlite. Core-ProviderName nuget-skipdependen<br>Install-package System. Data. sqlite. EF6-ProviderName nuget-skipdependen<br>Install-package System. Data. sqlite. Linq-ProviderName nuget-skipdependen<br><br>Nachdem die Pakete erfolgreich heruntergeladen wurden, stellen Sie sicher, dass Sie die gleiche Version aufweisen. Wenn dies nicht der Wert ist, fügen Sie den-Requirements dversion-Parameter den obigen Befehlen hinzu, und legen Sie diese auf die gleiche Version fest. |
|Fehler beim Veröffentlichungs Drucker. | <ul><li>Stellen Sie für Passthrough-Vorauthentifizierung sicher, dass der Benutzer, der den Drucker veröffentlicht, die richtige Berechtigung für die Veröffentlichungs Datenbank erhält.</li><li>Stellen Sie für Azure AD Vorauthentifizierung sicher, dass die Windows-Authentifizierung in IIS aktiviert ist. Siehe Schritt 5,3. Versuchen Sie außerdem, die Passthrough-Vorauthentifizierung zu verwenden. Wenn die Passthrough-Vorauthentifizierung funktioniert, liegt das Problem wahrscheinlich im Zusammenhang mit dem Anwendungs Proxy. Weitere Informationen finden Sie unter [Beheben von Problemen mit Anwendungs Proxy und Fehlermeldungen](https://docs.microsoft.com/azure/active-directory/manage-apps/application-proxy-troubleshoot). Beachten Sie, dass der Wechsel zu Passthrough die Single Sign-on Einstellung zurücksetzt. Wiederholen Sie Schritt 5, um die Vorauthentifizierung erneut Azure AD.</li></ul> |
|Druckaufträge werden in den Drucker Zustand versetzt. | <ul><li>Stellen Sie sicher, dass TLS 1,2 auf dem Connector-Server aktiviert ist. Weitere Informationen finden Sie im verknüpften Artikel in Schritt 2,1.</li><li>Stellen Sie sicher, dass HTTP2 auf dem Connector-Server deaktiviert ist. Weitere Informationen finden Sie im verknüpften Artikel in Schritt 2,1.</li></ul> |

Im folgenden finden Sie Speicherorte von Protokollen zur Problembehandlung.

|Komponente |Speicherort des Protokolls |
|------|------|
|Windows 10-Client | <ul><li>Verwenden Sie Ereignisanzeige, um das Protokoll von Azure AD Vorgängen anzuzeigen. Klicken Sie auf **Start** , und geben Sie Ereignisanzeige ein. Navigieren Sie zu Anwendungs-und Dienst Protokolle > Microsoft > Windows > Aad-> Vorgang.</li><li>Verwenden Sie den Feedback-Hub, um Protokolle zu erfassen. Siehe [Senden von Feedback an Microsoft mit der Feedback-Hub-App](https://support.microsoft.com/help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub-app)</li></ul> |
|Connector-Server | Verwenden Sie Ereignisanzeige, um das Protokoll des Anwendungs Proxys anzuzeigen. Klicken Sie auf **Start** , und geben Sie Ereignisanzeige ein. Navigieren Sie zu Anwendungs-und Dienst Protokolle > Microsoft > aadapplicationproxy > Connector > admin. |
|Druckerserver | Die Protokolle für die "mopria Discovery Service"-App und die unternehmenscloud-Druck-App finden Sie unter "c:\inetpub\logs\logfiles\w3svc1.". |
