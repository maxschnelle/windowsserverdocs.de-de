---
title: Konfigurieren der Zugriffssteuerung für Benutzer und Berechtigungen
description: Informationen Sie zum Konfigurieren der Zugriffssteuerung für Benutzer und Berechtigungen mithilfe von Active Directory oder Azure AD (Projekt Honolulu)
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.date: 06/07/2019
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: ef87a3bcc5bd0b924a938f055307a0a87cb60d0b
ms.sourcegitcommit: be243a92f09048ca80f85d71555ea6ee3751d712
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/11/2019
ms.locfileid: "67792317"
---
# <a name="configure-user-access-control-and-permissions"></a>Konfigurieren der Zugriffssteuerung für Benutzer und Berechtigungen

> Gilt für: Windows Admin Center, Windows Admin Center-Vorschau

Wenn Sie nicht bereits getan haben, informieren Sie sich über die [Benutzeroptionen Access-Steuerelement in Windows Admin Center](../plan/user-access-options.md)

> [!NOTE]
> Gruppe basierend auf Windows Admin Center wird nicht in arbeitsgruppenumgebungen oder in nicht vertrauenswürdigen Domänen unterstützt.

## <a name="gateway-access-role-definitions"></a>Rollendefinitionen für Gateway-Zugriff

Es gibt zwei Rollen für den Zugriff auf den Gateway-Dienst von Windows Admin Center:

**Datenverwaltungsgateway-Benutzer** können mit dem Gateway-Dienst von Windows Admin Center zum Verwalten von Servern über dieses Gateway verbinden, aber nicht über Zugriffsberechtigungen noch der Authentifizierungsmechanismus verwendet das Gateway zu authentifizieren.

**Gatewayadministratoren** können konfigurieren, wer Zugriff auch erhält, wie Benutzer mit dem Gateway zu authentifizieren. Nur die gatewayadministratoren können anzeigen und Konfigurieren der zugriffseinstellungen in Windows Admin Center. Lokale Administratoren auf dem Gatewaycomputer sind immer die Administratoren des Gatewaydiensts Windows Admin Center.

> [!NOTE]
> Zugriff auf das Gateway impliziert vom Gateway nicht auf verwalteten Servern angezeigt. Um einen Zielserver verwalten zu können, muss der verbindenden Benutzer Anmeldeinformationen verwenden (entweder über seine durchlaufenen-Windows-Anmeldeinformationen oder Anmeldeinformationen in der Windows Admin Center-Sitzung mit dem **verwalten als** Aktion) die Administratorzugriff auf diesem Zielserver.

## <a name="active-directory-or-local-machine-groups"></a>Active Directory oder lokale Benutzergruppen

Standardmäßig sind Active Directory oder lokale Benutzergruppen verwendet, um den Zugriff auf steuern. Wenn Sie Active Directory-Domäne verfügen, können Sie verwalten, Gateway-Benutzer und Administratoren auf der Benutzeroberfläche, die Windows Admin Center zugreifen.

Auf der **Benutzer** Registerkarte können Sie steuern, wer Windows Admin Center als Gateway Benutzer zugreifen kann. In der Standardeinstellung und wenn Sie eine Sicherheitsgruppe nicht angeben, hat jeder Benutzer, der die Gateway-URL zugreift Zugriff. Nachdem Sie der Liste der Benutzer eine oder mehrere Sicherheitsgruppen hinzugefügt haben, ist der Zugriff auf die Mitglieder dieser Gruppen beschränkt.

Wenn Sie nicht Active Directory-Domäne in Ihrer Umgebung verwenden, der Zugriff wird gesteuert durch die `Users` und `Administrators` lokalen Gruppen auf dem Gatewaycomputer Windows Admin Center.

### <a name="smartcard-authentication"></a>Smartcard-Authentifizierung

Sie können erzwingen, **Smartcard-Authentifizierung** durch eine zusätzliche Angabe _erforderlichen_ für Smartcard-basierte Sicherheitsgruppen. Nachdem Sie eine Smartcard-basierte Sicherheitsgruppe hinzugefügt haben, kann ein Benutzer nur den Windows Admin Center-Dienst zugreifen, wenn sie ein Mitglied einer Sicherheitsgruppe sind, und eine Smartcard-Gruppe in der Benutzerliste enthalten.

Auf der **Administratoren** Registerkarte können Sie steuern, wer Windows Admin Center als gatewayadministrator zugreifen kann. Die Gruppe der lokalen Administratoren auf dem Computer wird immer haben vollen Administratorzugriff und kann nicht aus der Liste entfernt werden. Hinzufügen von Sicherheitsgruppen, erteilen Sie Mitglieder der Gruppen Berechtigungen zum Ändern der Gateway-Einstellungen für Windows Admin Center. Die Administratorenliste, die Smartcard-Authentifizierung unterstützt, auf die gleiche Weise wie die Benutzerliste: mit dem AND-Bedingung für eine Sicherheitsgruppe und einer Smartcard-Gruppe.

## <a name="azure-active-directory"></a>Azure Active Directory

Wenn Ihre Organisation Azure Active Directory (Azure AD) verwendet, können Sie fügen eine **zusätzliche** Sicherheitsebene für Windows Admin Center durch das Anfordern von Azure AD-Authentifizierung auf dem Gateway. Um Windows Admin Center, dem Benutzer den Zugriff auf **Windows-Konto** müssen Sie auch den Zugriff auf Gateway-Server (auch wenn Azure AD-Authentifizierung verwendet wird). Bei Verwendung von Azure AD verwalten Windows Admin Center-Benutzer und Administratoren Berechtigungen aus dem Azure-Portal und nicht innerhalb der Windows Admin Center-Benutzeroberfläche.

### <a name="accessing-windows-admin-center-when-azure-ad-authentication-is-enabled"></a>Beim Zugriff auf Windows Admin Center, wenn es sich bei Azure AD-Authentifizierung aktiviert ist

Je nach Browser verwendet, erhalten einige Benutzer den Zugriff auf Windows Admin Center mit Azure AD-Authentifizierung konfiguriert eine zusätzliche Aufforderung **aus dem Browser** , in dem sie benötigen, geben Sie die Windows-Konto-Anmeldeinformationen für der Computer, auf dem Windows Admin Center installiert ist. Nach der Eingabe dieser Informationen, erhalten die Benutzer die zusätzliche authentifizierungseingabeaufforderung von Azure Active Directory, erfordert die Anmeldeinformationen für ein Azure-Konto, dem Zugriff in Azure AD-Anwendung in Azure gewährt wurden.

> [!NOTE]
> Benutzer, die die Windows-Konto verfügt **Administratorrechte** auf dem Gateway werden Computer nicht für die Azure AD-Authentifizierung aufgefordert werden.

### <a name="configuring-azure-active-directory-authentication-for-windows-admin-center-preview"></a>Konfigurieren der Azure Active Directory-Authentifizierung für Windows Admin Center (Vorschau)

Wechseln Sie zu Windows Admin Center **Einstellungen** > **Zugriff** und verwenden Sie den Umschalter zum Aktivieren "verwenden Sie Azure Active Directory auf dem Gateway eine weitere Sicherheitsstufe hinzufügen". Wenn Sie nicht das Gateway in Azure registriert haben, werden Sie zu diesem Zeitpunkt dazu geführt.

Standardmäßig haben alle Mitglieder der Azure AD-Mandanten Benutzerzugriff auf den Gateway-Dienst von Windows Admin Center. Nur lokale Administratoren auf dem Gatewaycomputer haben Administratorzugriff auf das Gateway Windows Admin Center. Beachten Sie, dass die Rechte eines lokalen Administratoren auf dem Gatewaycomputer können nicht eingeschränkt werden: lokale Administratoren können alle Aktionen für unabhängig davon, ob Azure AD für die Authentifizierung verwendet wird.

Sie gewähren bestimmten Azure AD-Benutzer oder Gruppen Gateway Benutzer oder Gateway-Administratorzugriff auf den Windows Admin Center-Dienst können, müssen Sie Folgendes ausführen:

1.  Wechseln Sie zu Ihrer Windows Admin Center, Azure AD-Anwendung im Azure-Portal, mithilfe des Links bereitgestellt, die in den Einstellungen für den Zugriff. Beachten Sie, dass dieser Link nur verfügbar ist, wenn Azure Active Directory-Authentifizierung aktiviert ist. 
    -   Sie können auch Ihre Anwendung im Azure-Portal finden, durch das Aufrufen **Azure Active Directory** > **unternehmensanwendungen** > **alle Anwendungen** und die Suche **WindowsAdminCenter** (Azure AD-app erhält WindowsAdminCenter -<gateway name>). Wenn Sie keine Suchergebnisse erhalten, stellen Sie sicher **anzeigen** nastaven NA hodnotu **alle Anwendungen**, **Anwendungsstatus** nastaven NA hodnotu **alle** , und klicken Sie auf Übernehmen, Wiederholen Sie dann Ihre Suche ein. Nachdem Sie die Anwendung gefunden haben, wechseln Sie zur **Benutzer und Gruppen**
2.  Legen Sie die Registerkarte "Eigenschaften" **benutzerzuweisung erforderlich** auf Ja.
    Sobald Sie dies getan haben, nur Mitglieder aufgeführt, der **Benutzer und Gruppen** Registerkarte kann das Gateway Windows Admin Center zugreifen.
3.  Wählen Sie in der Registerkarte Benutzer und Gruppen, **Benutzer hinzufügen**. Sie müssen einen Gateway-Benutzer oder die Gateway-Rolle "Administrator" für jeden Benutzer bzw. die Gruppe hinzugefügt zuweisen.

Nachdem Sie Azure AD-Authentifizierung aktivieren, müssen der Gateway-Dienst neu gestartet wird und Sie Ihren Browser aktualisieren. Sie können den Benutzerzugriff für die Anwendung SME Azure AD im Azure-Portal zu einem beliebigen Zeitpunkt aktualisieren.

Benutzer werden aufgefordert, melden Sie sich mit ihrer Azure Active Directory-Identität aus, wenn sie versuchen, die Gateway-URL des Windows Admin Center zugreifen. Denken Sie daran, dass Benutzer auch Mitglied der lokalen Benutzer auf dem Gateway-Server auf Windows Admin Center zugreifen müssen.

Benutzer und Administratoren können ihrem aktuell angemeldeten Konto anzeigen und auch als Abmeldung von diesem Azure AD-Konto aus der **Konto** Windows Admin Center-Einstellungen auf der Registerkarte.

### <a name="configuring-azure-active-directory-authentication-for-windows-admin-center"></a>Konfigurieren der Azure Active Directory-Authentifizierung für Windows Admin Center

[Um Azure AD-Authentifizierung einzurichten, müssen Sie zuerst Ihr Gateway bei Azure registrieren](azure-integration.md) (Sie müssen nur einmal für Ihr Gateway Windows Admin Center dazu). Dieser Schritt erstellt eine Azure AD-Anwendung, die aus der Gateway-Benutzer und Administrator-Gateway-Zugriff verwalten können.

Sie gewähren bestimmten Azure AD-Benutzer oder Gruppen Gateway Benutzer oder Gateway-Administratorzugriff auf den Windows Admin Center-Dienst können, müssen Sie Folgendes ausführen:

1.  Wechseln Sie zu Ihrer Anwendung SME Azure AD im Azure-Portal. 
    -   Beim Klicken auf **änderungszugriffssteuerung** und wählen Sie dann **Azure Active Directory** in den Einstellungen für Windows Admin Center zugreifen, können Sie den Link in der Benutzeroberfläche bereitgestellt, die Zugriff auf Ihre Azure AD die Anwendung im Azure-Portal. Dieser Link ist auch in den Einstellungen für den Zugriff verfügbar, nachdem Sie auf Speichern, und Azure AD als Identitätsanbieter Access-Steuerelement ausgewählt haben.
    -   Sie können auch Ihre Anwendung im Azure-Portal finden, durch das Aufrufen **Azure Active Directory** > **unternehmensanwendungen** > **alle Anwendungen** und die Suche **SME** (Azure AD-app erhält KMU -<gateway>). Wenn Sie keine Suchergebnisse erhalten, stellen Sie sicher **anzeigen** nastaven NA hodnotu **alle Anwendungen**, **Anwendungsstatus** nastaven NA hodnotu **alle** , und klicken Sie auf Übernehmen, Wiederholen Sie dann Ihre Suche ein. Nachdem Sie die Anwendung gefunden haben, wechseln Sie zur **Benutzer und Gruppen**
2.  Legen Sie die Registerkarte "Eigenschaften" **benutzerzuweisung erforderlich** auf Ja.
    Sobald Sie dies getan haben, nur Mitglieder aufgeführt, der **Benutzer und Gruppen** Registerkarte kann das Gateway Windows Admin Center zugreifen.
3.  Wählen Sie in der Registerkarte Benutzer und Gruppen, **Benutzer hinzufügen**. Sie müssen einen Gateway-Benutzer oder die Gateway-Rolle "Administrator" für jeden Benutzer bzw. die Gruppe hinzugefügt zuweisen.

Nachdem Sie die Azure AD speichern Zugriffssteuerung in der **änderungszugriffssteuerung** Bereich der Gatewaydienst neu gestartet wird und Sie müssen Ihren Browser aktualisieren. Sie können den Benutzerzugriff für die Anwendung Windows Admin Center, Azure AD im Azure-Portal zu einem beliebigen Zeitpunkt aktualisieren. 

Benutzer werden aufgefordert, melden Sie sich mit ihrer Azure Active Directory-Identität aus, wenn sie versuchen, die Gateway-URL des Windows Admin Center zugreifen. Denken Sie daran, dass Benutzer auch Mitglied der lokalen Benutzer auf dem Gateway-Server auf Windows Admin Center zugreifen müssen. 

Mithilfe der **Azure** auf der Registerkarte Allgemeine Einstellungen für Windows Admin Center, Benutzer und Administratoren kann ihrem aktuell angemeldeten Konto anzeigen und als auch für dieses Azure AD-Konto abmelden.

### <a name="conditional-access-and-multi-factor-authentication"></a>Für den bedingten Zugriff und Multi-Factor authentication

Einer der Vorteile der Verwendung von Azure AD als eine zusätzliche Sicherheitsebene zum Steuern des Zugriffs auf das Gateway Windows Admin Center ist, dass Sie Azure AD leistungsstarken Sicherheitsfunktionen wie bedingten Zugriff und Multi-Factor Authentication nutzen können. 

[Erfahren Sie mehr über das Konfigurieren des bedingten Zugriffs in Azure Active Directory.](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal-get-started)

## <a name="configure-single-sign-on"></a>Konfigurieren des einmaligen Anmeldens

**Einmaliges Anmelden bei der Bereitstellung als Dienst unter Windows Server**

Bei der Installation von Windows Admin Center unter Windows 10 kann sie einmaliges Anmelden verwenden. Wenn Sie Windows Admin Center in Windows Server verwenden also, müssen Sie jedoch eine Art von Kerberos-Delegierung in Ihrer Umgebung einrichten, bevor Sie einmaliges Anmelden verwenden können. Die Delegierung konfiguriert den Gatewaycomputer als vertrauenswürdig für die Delegierung an den Zielknoten. 

So konfigurieren Sie [ressourcenbasierte eingeschränkte Delegierung](https://docs.microsoft.com/windows-server/security/kerberos/kerberos-constrained-delegation-overview) in Ihrer Umgebung führen Sie die folgenden PowerShell-Cmdlets. Werden Sie (Beachten Sie, dass dies erfordert, dass einen Domänencontroller unter Windows Server 2012 oder höher).

```powershell
     $gateway = "WindowsAdminCenterGW" # Machine where Windows Admin Center is installed
     $node = "ManagedNode" # Machine that you want to manage
     $gatewayObject = Get-ADComputer -Identity $gateway
     $nodeObject = Get-ADComputer -Identity $node
     Set-ADComputer -Identity $nodeObject -PrincipalsAllowedToDelegateToAccount $gatewayObject
```

In diesem Beispiel das Windows Admin Center-Gateway installiert ist, auf Server **WindowsAdminCenterGW**, und der Name des Zielknotens ist **ManagedNode**.

Um diese Beziehung zu entfernen, führen Sie das folgende Cmdlet aus:

```powershell
Set-ADComputer -Identity $nodeObject -PrincipalsAllowedToDelegateToAccount $null
```

## <a name="role-based-access-control"></a>Rollenbasierte Zugriffsteuerung

Rollenbasierte Zugriffssteuerung können Sie Benutzern eingeschränkten Zugriff auf den Computer aus, anstatt Sie vollständige lokale Administratoren bereitzustellen.
[Weitere Informationen über die rollenbasierte Zugriffssteuerung und die verfügbaren Rollen.](../plan/user-access-options.md#role-based-access-control)

Einrichten von RBAC umfasst 2 Schritte aus: Aktivieren der Unterstützung für auf den Zielcomputern und Zuweisen von Benutzern zu der relevanten Rollen.

> [!TIP]
> Stellen Sie sicher, dass Sie über lokale Administratorrechte verfügen, auf den Computern, auf dem Sie Unterstützung für die rollenbasierte Zugriffssteuerung konfigurieren.

### <a name="apply-role-based-access-control-to-a-single-machine"></a>Rollenbasierte Zugriffssteuerung für einen einzelnen Computer anwenden

Das Bereitstellungsmodell für die einzelnen Computer ist ideal für einfache Umgebungen mit nur wenigen Computern verwalten.
Konfigurieren eines virtuellen Computers mit Unterstützung für die rollenbasierte Zugriffssteuerung führt die folgenden Änderungen:

-   PowerShell-Modulen mit Funktionen, die erforderlichen Windows Admin Center installiert werden auf dem Systemlaufwerk unter `C:\Program Files\WindowsPowerShell\Modules`. Alle Module beginnt mit **Microsoft.Sme**
-   Desired State Configuration, führt eine einmalige Konfiguration zum Konfigurieren von eines Just Enough Administration-Endpunkts auf dem Computer, mit dem Namen **Microsoft.Sme.PowerShell**. Dieser Endpunkt definiert die 3-Rollen, die von Windows Admin Center verwendet und wird als temporärer lokaler Administrator ausgeführt, wenn ein Benutzer, eine Verbindung herstellt.
-   3 neue lokale Gruppen werden an Steuerelement erstellt werden, welche Benutzer Zugriff auf welche Rollen zugewiesen werden:
    -   Administratoren für Windows Admin Center
    -   Windows Admin Center Hyper-V-Administratoren
    -   Windows Admin Center-Leser

Um die Unterstützung für die rollenbasierte Zugriffssteuerung auf einem einzelnen Computer zu aktivieren, gehen Sie folgendermaßen vor:

1.  Öffnen Sie Windows Admin Center, und Verbinden mit dem Computer, die, den Sie mit der rollenbasierten Zugriffssteuerung, die mit einem Konto mit lokalen Administratorrechten auf dem Zielcomputer konfigurieren möchten.
2.  Auf der **Übersicht** tool, klicken Sie auf **Einstellungen** > **Role-based Access Control,** .
3.  Klicken Sie auf **übernehmen** am unteren Rand der Seite, um Unterstützung für die rollenbasierte Zugriffssteuerung auf dem Zielcomputer aktivieren. Der Anwendungsprozess umfasst PowerShell-Skripts kopieren und das Aufrufen von einer Konfigurations (mithilfe von PowerShell Desired State Configuration) auf dem Zielcomputer an. Es dauert bis zu 10 Minuten in Anspruch und führt zu WinRM neu zu starten. Dadurch wird Windows Admin Center, PowerShell und WMI-Benutzer vorübergehend getrennt.
4.  Aktualisieren Sie die Seite zum Überprüfen des Status der rollenbasierten Zugriffssteuerung. Wenn es zur Verwendung bereit ist, der Status wird nun **angewendet**.

Nachdem die Konfiguration angewendet wurde, können Sie Benutzer den Rollen zuweisen:

1.  Öffnen der **lokale Benutzer und Gruppen** Konfigurationstool, und navigieren Sie zu der **Gruppen** Registerkarte.
2.  Wählen Sie die **Windows Admin Center Leser** Gruppe.
3.  In der *Details* unten, klicken Sie dann auf **Add User** und geben Sie den Namen einer nur-Lese Zugriff auf den Server über Windows Admin Center müssen Benutzer oder Sicherheitsgruppen-Gruppe. Die Benutzer und Gruppen können aus dem lokalen Computer oder Active Directory-Domäne stammen.
4.  Wiederholen Sie die Schritte 2 bis 3 für die **Windows Admin Center Hyper-V-Administratoren** und **Windows Admin Center Administratoren** Gruppen.

Sie können auch Ausfüllen dieser Gruppen durchgängig in Ihrer gesamten Domäne konfigurieren Sie ein Gruppenrichtlinienobjekt mit der [richtlinieneinstellung für eingeschränkte Gruppen](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc756802%28v=ws.10%29).

### <a name="apply-role-based-access-control-to-multiple-machines"></a>Anwenden der rollenbasierten Zugriffssteuerung auf mehreren Computern

In einer Bereitstellung für große Unternehmen können Sie Ihre vorhandenen Automatisierungstools auf Ihren Computern, die das rollenbasierte zugriffssteuerungsfeature auslasten, indem Sie das Konfigurationspaket aus dem Windows Admin Center-Gateway herunterladen.
Das clientkonfigurationspaket mit PowerShell Desired State Configuration verwendet werden soll, aber Sie können anpassen, es funktioniert mit Ihrer bevorzugten Automation-Lösung.

#### <a name="download-the-role-based-access-control-configuration"></a>Die rollenbasierte zugriffssteuerungskonfiguration herunterladen

Informationen zum Herunterladen des Konfigurationspakets für rollenbasierte Access Control müssen Sie eine PowerShell-Eingabeaufforderung zu Windows Admin Center zugreifen.

Wenn Sie das Gateway Windows Admin Center im Modus "Dienst" unter Windows Server ausführen, verwenden Sie den folgenden Befehl zum Herunterladen des clientkonfigurationspakets.
Achten Sie darauf, um die Gateway-Adresse mit die richtige Auswahl für Ihre Umgebung zu aktualisieren.

```powershell
$WindowsAdminCenterGateway = 'https://windowsadmincenter.contoso.com'
Invoke-RestMethod -Uri "$WindowsAdminCenterGateway/api/nodes/all/features/jea/endpoint/export" -Method POST -UseDefaultCredentials -OutFile "~\Desktop\WindowsAdminCenter_RBAC.zip"
```

Wenn Sie das Gateway Windows Admin Center auf Ihrem Windows 10-Computer ausführen, führen Sie stattdessen den folgenden Befehl aus:

```powershell
$cert = Get-ChildItem Cert:\CurrentUser\My | Where-Object Subject -eq 'CN=Windows Admin Center Client' | Select-Object -First 1
Invoke-RestMethod -Uri "https://localhost:6516/api/nodes/all/features/jea/endpoint/export" -Method POST -Certificate $cert -OutFile "~\Desktop\WindowsAdminCenter_RBAC.zip"
```

Wenn Sie das Zip-Archiv erweitern, sehen Sie die folgende Ordnerstruktur:

- InstallJeaFeatures.ps1
- JustEnoughAdministration (Verzeichnis)
- Module (Verzeichnis)
    - Microsoft.SME. \* (Verzeichnisse)
    - WindowsAdminCenter.Jea (directory)

Um Unterstützung für die rollenbasierte Zugriffssteuerung auf einem Knoten zu konfigurieren, müssen Sie die folgenden Aktionen ausführen:

1.  Kopieren Sie die JustEnoughAdministration, Microsoft.SME. \*, und WindowsAdminCenter.Jea Module in das Verzeichnis des PowerShell-Modul auf dem Zielcomputer. Dies ist in der Regel unter `C:\Program Files\WindowsPowerShell\Modules`.
2.  Update **InstallJeaFeature.ps1** Datei entsprechen die gewünschte Konfiguration für die RBAC-Endpunkt.
3.  Führen Sie InstallJeaFeature.ps1 zum Kompilieren der DSC-Ressource.
4.  Bereitstellen der DSC-Konfigurations auf alle Computer, die Konfiguration anzuwenden.

Der folgende Abschnitt erläutert, wie Sie dies mithilfe von PowerShell-Remoting.

#### <a name="deploy-on-multiple-machines"></a>Bereitstellen auf mehreren Computern

Um die Konfiguration bereitstellen, Sie auf mehreren Computern heruntergeladen haben, müssen Sie zum Aktualisieren der **InstallJeaFeatures.ps1** Skript für Ihre Umgebung die angemessenen Sicherheitsgruppen enthalten, kopieren die Dateien auf alle Computer, und rufen Sie die Konfigurationsskripts.
Sie können Ihrer bevorzugten Automation-Tools verwenden, um dies zu erreichen, jedoch in diesem Artikel auf einer reinen PowerShell-basierten Ansatzes Fokus wird.

Standardmäßig erstellt das Skript auf dem Computer zum Steuern des Zugriffs auf die einzelnen Rollen lokale Sicherheitsgruppen vorhanden sind.
Dies ist nützlich für die Arbeitsgruppe und die Domäne eingebundenen Computern, aber wenn Sie in einer Domäne nur die Umgebung, die Sie direkt implementieren können bereitstellen jede Rolle eine Domänensicherheitsgruppe zuordnen.
Öffnen Sie zum Aktualisieren der Konfigurations zur Verwendung von Sicherheitsgruppen einer Domäne **InstallJeaFeatures.ps1** , und stellen Sie die folgenden Änderungen:

1.  Entfernen Sie die 3 **Gruppe** Ressourcen aus der Datei:
    1.  "Group-MS-Leser-Gruppe"
    2.  "Group MS-Hyper-V-Administrators-Group"
    3.  "Gruppe MS-Administratoren-Gruppe"
2.  Entfernen Sie die 3 Gruppieren von Ressourcen aus der JeaEndpoint **"DependsOn"** Eigenschaft
    1.  "[Group]MS-Readers-Group"
    2.  "[Group]MS-Hyper-V-Administrators-Group"
    3.  "[Group] MS-Administratoren-Gruppe"
3.  Ändern Sie den Gruppennamen in der JeaEndpoint **RoleDefinitions** Eigenschaft zu Ihren gewünschten Sicherheitsgruppen. Für, wenn Sie z. B. eine Sicherheitsgruppe *CONTOSO\MyTrustedAdmins* , zugeordnet sein sollte Zugriff Administratorrolle Windows Admin Center, Änderung `'$env:COMPUTERNAME\Windows Admin Center Administrators'` zu `'CONTOSO\MyTrustedAdmins'`. Die drei Zeichenfolgen, die Sie aktualisieren müssen sind:
    1.  '$env:COMPUTERNAME\Windows Admin Center Administrators'
    2.  "$env: COMPUTERNAME\Windows Admin Center Hyper-V-Administratoren
    3.  '$env:COMPUTERNAME\Windows Admin Center Readers'

> [!NOTE]
> Achten Sie darauf, dass Sie eindeutige Sicherheits-Gruppen für jede Rolle zu verwenden. Konfiguration schlägt fehl, wenn die gleiche Sicherheitsgruppe mehrere Rollen zugewiesen ist.

Als Nächstes wird am Ende der **InstallJeaFeatures.ps1** Hinzufügen von PowerShell die folgenden Zeilen am Ende des Skripts:

```powershell
Copy-Item "$PSScriptRoot\JustEnoughAdministration" "$env:ProgramFiles\WindowsPowerShell\Modules" -Recurse -Force
$ConfigData = @{
    AllNodes = @()
    ModuleBasePath = @{
        Source = "$PSScriptRoot\Modules"
        Destination = "$env:ProgramFiles\WindowsPowerShell\Modules"
    }
}
InstallJeaFeature -ConfigurationData $ConfigData | Out-Null
Start-DscConfiguration -Path "$PSScriptRoot\InstallJeaFeature" -JobName "Installing JEA for Windows Admin Center" -Force
```

Schließlich können Sie den Ordner mit den Modulen, die DSC-Ressource und die Konfiguration auf jedem Zielknoten kopieren und Ausführen der **InstallJeaFeature.ps1** Skript.
Remotezugriff auf Ihre Administratorarbeitsstation dazu können Sie die folgenden Befehle ausführen:

```powershell
$ComputersToConfigure = 'MyServer01', 'MyServer02'

$ComputersToConfigure | ForEach-Object {
    $session = New-PSSession -ComputerName $_ -ErrorAction Stop
    Copy-Item -Path "~\Desktop\WindowsAdminCenter_RBAC\JustEnoughAdministration\" -Destination "$env:ProgramFiles\WindowsPowerShell\Modules\" -ToSession $session -Recurse -Force
    Copy-Item -Path "~\Desktop\WindowsAdminCenter_RBAC" -Destination "$env:TEMP\WindowsAdminCenter_RBAC" -ToSession $session -Recurse -Force
    Invoke-Command -Session $session -ScriptBlock { Import-Module JustEnoughAdministration; & "$env:TEMP\WindowsAdminCenter_RBAC\InstallJeaFeature.ps1" } -AsJob
    Disconnect-PSSession $session
}
```
