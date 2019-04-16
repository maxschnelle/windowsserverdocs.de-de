---
title: Konfigurieren von Steuerung des Benutzerzugriffs und Berechtigungen
description: Enthält Informationen zum Konfigurieren der Steuerung des Benutzerzugriffs und Berechtigungen, die mit Active Directory oder Azure AD (Projekt Honolulu)
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.date: 03/19/2019
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: b19657f4ce1a1a2cfb94f7234f07805ba0abd42c
ms.sourcegitcommit: 4961576f2891600ef9a760ca7df650d14332e057
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/09/2019
ms.locfileid: "9152045"
---
# Konfigurieren Sie die Steuerung des Benutzerzugriffs und Berechtigungen

>Betrifft: Windows Admin Center, Windows Admin Center – Vorschau

Wenn Sie noch nicht geschehen, machen Sie sich mit dem [Steuerelement Zugriffsoptionen für Benutzer in Windows Admin Center](../plan/user-access-options.md)

>[!NOTE]
> Gruppenzugriff in Windows Admin Center wird in einer Arbeitsgruppe Umgebung oder in nicht vertrauenswürdigen Domänen nicht unterstützt.

## Gateway Zugriff Rollendefinitionen

Es gibt zwei Funktionen für den Zugriff auf dem Windows Admin Center Gateway-Dienst:

**Gateway-Benutzer** können mit dem Windows Admin Center Gateway-Dienst zum Verwalten von Servern über dieses Gateway verbinden, aber sie nicht ändern, Zugriffsberechtigungen noch den Authentifizierungsmechanismus verwendet, um das Gateway zu authentifizieren.

**Gateway-Administratoren** können konfigurieren, wer Zugriff sowie erhält, wie Benutzer Gateway-Authentifizierung. Nur die Gateway-Administratoren können anzeigen und konfigurieren Sie die Access-Einstellungen in Windows Admin Center. Lokale Administratoren auf dem Gateway-Computer sind immer Administratoren des Windows Admin Center Gateway-Diensts.

> [!NOTE]
> Zugriff auf das Gateway implizieren nicht den Zugriff auf den verwalteten Servern sichtbar vom Gateway. Um einen Zielserver verwalten zu können, muss der Verbindung Benutzer Anmeldeinformationen (entweder über ihre übergeben-through-Windows-Anmeldeinformationen oder Anmeldeinformationen in der Windows Admin Center-Sitzung mit der Aktion **verwalten als** ) verwenden, die über Administratorrechte verfügen dem Ziel-Server.

## Active Directory oder lokale Gruppen

Standardmäßig werden Active Directory oder lokale Gruppen zum Steuern des Zugriffs Gateway verwendet. Wenn Sie Active Directory-Domäne verfügen, können Sie verwalten, Gateway-Benutzer und Administrator in der Benutzeroberfläche von Windows Admin Center zugreifen.

Auf der Registerkarte " **Benutzer** " können Sie steuern, wer Windows Admin Center als Gateway Benutzer zugreifen kann. Standardmäßig und wenn Sie eine Sicherheitsgruppe angeben, kann jeder Benutzer, der die Gateway-URL greift auf zugreifen. Nachdem Sie die Liste der Benutzer eine oder mehrere Sicherheitsgruppen hinzufügen, ist der Zugriff auf die Mitglieder dieser Gruppen beschränkt.

Wenn Sie keine Active Directory-Domäne in Ihrer Umgebung verwenden, den Zugriff von gesteuert wird die ```Users``` und ```Administrators``` lokale Gruppen auf dem Windows Admin Center Gateway-Computer.

### Smartcard-Authentifizierung

Sie können **Smartcard-Authentifizierung** erzwingen, indem Sie eine zusätzliche _erforderliche_ Gruppe für Smartcard-basierte Sicherheitsgruppen angeben. Nachdem Sie eine Smartcard-basierte Sicherheitsgruppe hinzugefügt haben, kann ein Benutzer nur den Windows Admin Center-Dienst zugreifen, wenn sie ein Mitglied einer Sicherheitsgruppe sind und eine Smartcard-Gruppe in der Liste der Benutzer enthalten.

Auf der Registerkarte " **Administratoren** " können Sie steuern, wer Windows Admin Center als Gateway-Administrator zugreifen kann. Der lokalen Administratorgruppe auf dem Computer wird immer vollständigen Administratorzugriff haben und nicht aus der Liste entfernt werden. Durch das Hinzufügen von Sicherheitsgruppen, bieten Ihnen Mitglieder dieser Berechtigungen Windows Admin Center Gateway-Einstellungen zu ändern. Die Administratorenliste unterstützt Smartcard-Authentifizierung auf die gleiche Weise wie der Benutzerliste: mit der Bedingung und für eine Sicherheitsgruppe und eine Smartcard-Gruppe.

## Azure Active Directory

Wenn Ihre Organisation Azure Active Directory (Azure AD) verwendet, können Sie auswählen, eine **zusätzliche** Sicherheitsebene bei Windows Admin Center hinzufügen, durch die Verwendung von Azure AD-Authentifizierung auf das Gateway zugreifen. Um Windows Admin Center zugreifen zu können, müssen **Windows-Konto** auch auf Gateway-Server zugreifen (auch wenn Azure AD-Authentifizierung verwendet wird). Wenn Sie Azure AD verwenden, müssen Sie Windows Admin Center-Benutzer und Administrator Zugriffsberechtigungen verwalten, aus dem Azure-Portal, anstatt aus der Windows Admin Center-Benutzeroberfläche.

### Zugriff auf Windows Admin Center, wenn es sich bei Azure AD-Authentifizierung aktiviert ist.

Je nach den verwendeten Browser der Kontoanmeldeinformationen einige Benutzer den Zugriff auf Windows Admin Center mit Azure AD-Authentifizierung konfiguriert eine zusätzliche auffordern **vom Browser** erhalten, in denen sie ihre Windows bereitstellen müssen, für den Computer auf dem Windows Admin Center wird installiert. Nachdem Sie diese Informationen eingegeben, erhalten die Benutzer zusätzliche Azure Active Directory-Authentifizierung dazu aufgefordert werden, die Anmeldeinformationen des ein Azure-Konto benötigt, die in der Azure AD-Anwendung in Azure Zugriff gewährt wurde.

> [!NOTE]
> Benutzer, die Windows-Konto verfügt **über Administratorrechte** auf dem Gateway-Computer wird nicht für die Azure AD-Authentifizierung aufgefordert werden.

### Konfigurieren der Azure Active Directory-Authentifizierung für Windows Admin Center – Vorschau

Wechseln Sie zu Windows Admin Center- **Einstellungen** > **Zugriff auf** und verwenden den Umschalter aktivieren "verwenden Azure Active Directory eine Sicherheitsebene an das Gateway hinzufügen". Wenn Sie das Gateway nicht registriert haben, werden Sie zu diesem Zeitpunkt dazu geführt.

Standardmäßig verfügen alle Mitglieder der Azure AD-Mandanten des Benutzerzugriffs auf dem Windows Admin Center Gateway-Dienst. Nur lokale Administratoren auf dem Gatewaycomputer haben Administratorzugriff auf das Windows Admin Center-Gateway. Beachten Sie, dass der Rechte von lokalen Administratoren auf dem Gatewaycomputer können nicht eingeschränkt werden – lokale Administratoren können alle Aktionen für unabhängig davon, ob Azure AD für die Authentifizierung verwendet wird.

Wenn Sie bieten bestimmte Azure AD-Benutzer oder Gruppen Gateway Benutzer oder Administratorzugriff auf den Dienst Windows Admin Center Gateway möchten, müssen Sie Folgendes tun:

1.  Wechseln Sie auf Ihre Windows Administrationscenter Azure AD-Anwendung im Azure-Portal mit dem Link unter "Einstellungen" Zugriff bereitgestellt. Beachten Sie, dass dieser Link ist nur verfügbar, wenn die Azure Active Directory-Authentifizierung aktiviert ist. 
    -   Außerdem finden Sie Ihre Anwendung im Azure-Portal auf **Azure Active Directory** > **unternehmensanwendungen** > **Alle Anwendungen** und Suche **WindowsAdminCenter** (die Azure AD-app Namen WindowsAdminCenter-<gateway name>). Wenn Sie keine Suchergebnisse erhalten, stellen Sie sicher, **zeigen** auf **Alle Programme**festgelegt ist, **Anwendungsstatus** auf **Alle** festgelegt ist und klicken Sie auf Übernehmen, versuchen Sie dann die Suche. Wenn Sie die Anwendung gefunden haben, wechseln Sie zu **Benutzern und Gruppen**
2.  Legen Sie in der Registerkarte "Eigenschaften" **von Benutzerrechten erforderlich** auf "Ja" aus.
    Nachdem Sie dies getan haben, werden nur Mitglieder, die in der Registerkarte " **Benutzer und Gruppen** " auf das Windows Admin Center-Gateway zugreifen.
3.  Wählen Sie in der Benutzer und Gruppen-Registerkarte **Benutzer hinzufügen**. Sie müssen ein Gateway-Benutzer oder Gateway-Administratorrolle für jeden Benutzer/Gruppe hinzugefügt zuweisen.

Nachdem Sie Azure AD-Authentifizierung aktivieren, müssen der Gateway-Dienst neu gestartet wird und Sie Ihren Browser aktualisieren. Sie können den Benutzerzugriff für die SME Azure AD-Anwendung im Azure-Portal zu einem beliebigen Zeitpunkt aktualisieren.

Benutzer werden aufgefordert, melden Sie sich mit ihren Azure Active Directory-Identität, wenn sie versuchen, die Windows Admin Center Gateway-URL zuzugreifen. Denken Sie daran, dass Benutzer auch ein Mitglied der lokalen Benutzer auf dem Gatewayserver in Windows Admin Center zugreifen müssen.

Benutzer und Administratoren können ihrem aktuell angemeldeten Konto anzeigen und auch als Abmeldung von dieser Azure AD kontoeinstellungen aus der Registerkarte " **Konto** " Windows Admin Center.

### Konfigurieren der Azure Active Directory-Authentifizierung für Windows Admin Center

[Zum Einrichten von Azure AD-Authentifizierung, müssen Sie zuerst das Gateway mit Azure registrieren](azure-integration.md) (Sie müssen nur einmal für Ihr Windows Admin Center-Gateway dazu). Dieser Schritt erstellt eine Azure AD-Anwendung, die von der Sie Gateway-Benutzer und Gateway Administratorzugriff verwalten können.

Wenn Sie bieten bestimmte Azure AD-Benutzer oder Gruppen Gateway Benutzer oder Administratorzugriff auf den Dienst Windows Admin Center Gateway möchten, müssen Sie Folgendes tun:

1.  Wechseln Sie zu Ihrer SME Azure AD-Anwendung im Azure-Portal. 
    -   Wenn Sie auf der **Änderung Zugriffskontrolle** und Sie dann aus den Einstellungen der Windows Admin Center-Zugriff **Azure Active Directory wählen** , können Sie den Link in der Benutzeroberfläche bereitgestellt, auf Azure AD-Anwendung im Azure-Portal zugreifen. Dieser Link ist auch in den Einstellungen für den Zugriff verfügbar, nachdem Sie speichern und Azure AD als Identitätsanbieter Ihrer Access-Steuerelement ausgewählt haben.
    -   Außerdem finden Sie Ihre Anwendung im Azure-Portal auf **Azure Active Directory** > **unternehmensanwendungen** > **Alle Anwendungen** und Suche **SME** (die Azure AD-app erhält den Namen SME -<gateway>). Wenn Sie keine Suchergebnisse erhalten, stellen Sie sicher, **zeigen** auf **Alle Programme**festgelegt ist, **Anwendungsstatus** auf **Alle** festgelegt ist und klicken Sie auf Übernehmen, versuchen Sie dann die Suche. Wenn Sie die Anwendung gefunden haben, wechseln Sie zu **Benutzern und Gruppen**
2.  Legen Sie in der Registerkarte "Eigenschaften" **von Benutzerrechten erforderlich** auf "Ja" aus.
    Nachdem Sie dies getan haben, werden nur Mitglieder, die in der Registerkarte " **Benutzer und Gruppen** " auf das Windows Admin Center-Gateway zugreifen.
3.  Wählen Sie in der Benutzer und Gruppen-Registerkarte **Benutzer hinzufügen**. Sie müssen ein Gateway-Benutzer oder Gateway-Administratorrolle für jeden Benutzer/Gruppe hinzugefügt zuweisen.

Nachdem Sie die Azure AD-Zugriffssteuerung speichern im Bereich **Zugriffskontrolle Änderung** der Gateway-Dienst neu gestartet werden, und Sie müssen aktualisieren Sie Ihren Browser. Sie können den Benutzerzugriff für die Windows Administrationscenter Azure AD-Anwendung im Azure-Portal zu einem beliebigen Zeitpunkt aktualisieren. 

Benutzer werden aufgefordert, melden Sie sich mit ihren Azure Active Directory-Identität, wenn sie versuchen, die Windows Admin Center Gateway-URL zuzugreifen. Denken Sie daran, dass Benutzer auch ein Mitglied der lokalen Benutzer auf dem Gatewayserver in Windows Admin Center zugreifen müssen. 

Mithilfe des Registerkarte " **Azure** " Windows Admin Center Allgemeine Einstellungen Benutzer und Administratoren können anzeigen, ihr Konto aktuell angemeldeten und als auch von dieser Azure AD-Konto abmelden.

### Bedingter Zugriff und Multi-Factor authentication

Einer der Vorteile der Verwendung von Azure AD als eine zusätzliche Sicherheitsschicht zum Steuern des Zugriffs auf das Windows Admin Center-Gateway ist, dass Sie Azure AD leistungsstarke Sicherheitsfeatures wie bedingten Zugriff und Multi-Factor Authentication nutzen können. 

[Weitere Informationen zum Konfigurieren des bedingten Zugriffs mit Azure Active Directory.](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal-get-started)

## Einmaliges Anmelden konfigurieren

**Einmaliges Anmelden bei der Bereitstellung als Dienst unter Windows Server**

Wenn Sie Windows Admin Center auf Windows 10 installieren, ist es nun einmaliges Anmelden verwendet. Wenn Sie vorhaben, Windows Admin Center auf Windows Server verwenden, müssen Sie jedoch eine Form der Kerberos-Delegierung in Ihrer Umgebung einrichten, bevor Sie einmaliges Anmelden verwenden können. Die Delegierung konfiguriert Gateway-Computer als vertrauenswürdig ist und an den Zielknoten zu delegieren. 

Führen Sie die folgenden PowerShell-Cmdlets, um [Ressourcenbasierte eingeschränkte Delegierung](http://windowsitpro.com/security/how-windows-server-2012-eases-pain-kerberos-constrained-delegation-part-1) in Ihrer Umgebung zu konfigurieren. (Beachten Sie, dass dies erfordert, dass einen Domänencontroller unter Windows Server 2012 oder höher sein).

```powershell
     $gateway = "WindowsAdminCenterGW" # Machine where Windows Admin Center is installed
     $node = "ManagedNode" # Machine that you want to manage
     $gatewayObject = Get-ADComputer -Identity $gateway
     $nodeObject = Get-ADComputer -Identity $node
     Set-ADComputer -Identity $nodeObject -PrincipalsAllowedToDelegateToAccount $gatewayObject
```

In diesem Beispiel wird das Windows Admin Center-Gateway auf Server **WindowsAdminCenterGW**installiert ist, und der Ziel-Knoten-Name ist **ManagedNode**.

Um diese Beziehung zu entfernen, führen Sie das folgende Cmdlet:

```powershell
Set-ADComputer -Identity $nodeObject -PrincipalsAllowedToDelegateToAccount $null
```

## Rollenbasierte Zugriffssteuerung

Rollenbasierte Zugriffssteuerung können Sie Benutzern eingeschränkten Zugriff auf den Computer anstelle von machen Sie vollständige lokale Administratoren zu ermöglichen.
[Weitere Informationen über rollenbasierte Zugriffssteuerung und die verfügbaren Rollen.](../plan/user-access-options.md#role-based-access-control)

Einrichten von RBAC besteht aus 2 Schritte: Aktivieren der Unterstützung auf den Zielcomputern und relevanten Rollen Benutzer zuweisen.

> [!TIP]
> Stellen Sie sicher, dass Sie über lokale Administratorrechte verfügen, auf den Computern, in denen Sie Unterstützung für rollenbasierte Zugriffssteuerung konfigurieren.

### Rollenbasierte Zugriffssteuerung auf einen einzelnen Computer anwenden.

Das Modell der einzelnen Computer Bereitstellung ist ideal für einfache Umgebungen mit nur wenige Computer zu verwalten.
Konfigurieren eines Computers mit Unterstützung für die rollenbasierte Zugriffssteuerung führt die folgenden Änderungen:
-   PowerShell-Module mit Windows Admin Center erforderlichen Funktionen installiert werden auf dem Systemlaufwerk unter `C:\Program Files\WindowsPowerShell\Modules`. Alle Module werden mit **Microsoft.Sme** gestartet.
-   Konfiguration des gewünschten führt eine einmalige Konfiguration, um einen Endpunkt Just Enough Administration auf dem Computer, mit dem Namen **Microsoft.Sme.PowerShell**zu konfigurieren. Diesen Endpunkt definiert die 3-Rollen, die von Windows Admin Center verwendet und wird als temporäre lokaler Administrator ausgeführt, wenn ein Benutzer darauf zugreift.
-   3 neue lokale Gruppen werden in Steuerelement erstellt werden, welche Benutzer Zugriff auf welche Rollen zugewiesen sind:
    -   Windows Admin Center-Administratoren
    -   Windows Admin Center Hyper-V-Administratoren
    -   Windows Admin Center Leser

Gehen Sie folgendermaßen vor, um Unterstützung für die rollenbasierte Zugriffssteuerung auf einem einzelnen Computer:

1.  Öffnen Sie Windows Administrationscenter, und Verbinden mit dem Computer, die, den Sie mit der rollenbasierten Zugriffssteuerung mit einem Konto mit lokalen Administratorrechten auf dem Zielcomputer konfigurieren möchten.
2.  Klicken Sie auf das Tool **Übersicht** auf **Einstellungen** > **rollenbasierte Zugriffssteuerung**.
3.  Klicken Sie auf **Übernehmen** am unteren Rand der Seite zum Aktivieren der Unterstützung für rollenbasierte Zugriffssteuerung auf dem Zielcomputer. Der Anwendungsprozess umfasst das Kopieren von PowerShell-Skripts und Aufrufen einer Konfigurations (mit PowerShell Desired State Configuration) auf dem Zielcomputer. Es dauert bis zu 10 Minuten in Anspruch, und führt zu WinRM neu gestartet. Dies wird Windows Admin Center, PowerShell und WMI-Benutzer vorübergehend getrennt.
4.  Aktualisieren Sie die Seite, um den Status der rollenbasierten Zugriffssteuerung überprüfen. Wenn sie für die Verwendung bereit ist, ändert sich der Status in **wird angewendet**.

Nachdem die Konfiguration angewendet wird, können Sie Benutzer zu den Rollen zuweisen:

1.  Öffnen Sie das Tool **Lokale Benutzer und Gruppen** , und navigieren Sie zu der Registerkarte " **Gruppen** ".
2.  Wählen Sie die **Windows Admin Center Leser** -Gruppe.
3.  Klicken Sie im *Detailbereich unten* auf **Benutzer hinzufügen** , und geben Sie den Namen einer Benutzer oder Sicherheitsgruppe Gruppe, die über schreibgeschützten Zugriff auf den Server über Windows Admin Center verfügt. Die Benutzer und Gruppen können aus dem lokalen Computer oder Active Directory-Domäne stammen.
4.  Wiederholen Sie die Schritte 2 bis 3 für die **Windows Admin Center Hyper-V** und **Windows Admin Center-Administratoren** Gruppen.

Sie können diese Gruppen auch konsistent in Ihrer Domäne ausfüllen, konfigurieren Sie ein Gruppenrichtlinienobjekt mit der [Eingeschränkten Gruppen-Einstellung](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc756802%28v=ws.10%29).

### Rollenbasierte Zugriffssteuerung auf mehreren Computern anwenden

Bei einer Bereitstellung mit großen Unternehmen können Sie Ihre vorhandene Benutzeroberflächenautomatisierungs-Tools, die Funktion rollenbasierter Zugriff auf Ihre Computer übertragen, durch das Herunterladen des Konfigurationspakets in das Windows Admin Center-Gateway verwenden.
Das Konfigurationspaket mit PowerShell Desired State Configuration verwendet werden soll, jedoch können Sie sich mit Ihrer bevorzugten Automatisierung Lösung anpassen.

#### Herunterladen der rollenbasierter Zugriff Steuerelement-Konfigurations

Informationen zum Herunterladen des Konfigurationspakets Steuerelement rollenbasierter Zugriff müssen Sie eine PowerShell-Eingabeaufforderung zu Windows Admin Center zugreifen.

Wenn Sie das Windows Admin Center-Gateway im Service-Modus unter Windows Server ausführen, verwenden Sie den folgenden Befehl, um das Konfigurationspaket herunterzuladen.
Achten Sie darauf, dass Sie die Gatewayadresse mit den richtigen Eintrag für Ihre Umgebung zu aktualisieren.

```powershell
$WindowsAdminCenterGateway = 'https://windowsadmincenter.contoso.com'
Invoke-RestMethod -Uri "$WindowsAdminCenterGateway/api/nodes/all/features/jea/endpoint/export" -Method POST -UseDefaultCredentials -OutFile "~\Desktop\WindowsAdminCenter_RBAC.zip"
```

Wenn Sie das Windows Admin Center-Gateway auf Ihrem Windows 10-Computer ausführen, führen Sie stattdessen den folgenden Befehl aus:

```powershell
$cert = Get-ChildItem Cert:\CurrentUser\My | Where-Object Subject -eq 'CN=Windows Admin Center Client' | Select-Object -First 1
Invoke-RestMethod -Uri "https://localhost:6516/api/nodes/all/features/jea/endpoint/export" -Method POST -Certificate $cert -OutFile "~\Desktop\WindowsAdminCenter_RBAC.zip"
```

Wenn Sie das Zip-Archiv erweitern, sehen Sie die folgende Ordnerstruktur:
- InstallJeaFeatures.ps1
- JustEnoughAdministration (Verzeichnis)
- Module (Verzeichnis)
    - Microsoft.SME.\* (Verzeichnisse)
    - WindowsAdminCenter.Jea (Verzeichnis)

Um Unterstützung für die rollenbasierte Zugriffssteuerung auf einem Knoten zu konfigurieren, müssen Sie die folgenden Aktionen ausführen:
1.  Kopieren Sie die Module JustEnoughAdministration, Microsoft.SME.\* und WindowsAdminCenter.Jea in das PowerShell-Modul-Verzeichnis auf dem Zielcomputer. Dies ist in der Regel am `C:\Program Files\WindowsPowerShell\Modules`.
2.  Aktualisieren Sie **InstallJeaFeature.ps1** -Datei, um die gewünschte Konfiguration für den Endpunkt RBAC übereinstimmen.
3.  Führen Sie InstallJeaFeature.ps1 zum Kompilieren der DSC-Ressource.
4.  Stellen Sie die DSC-Konfiguration auf alle Computer, die Konfiguration übernehmen.

Im folgende Abschnitt wird erläutert, wie dies mithilfe von PowerShell-Remoting erledigen.

#### Bereitstellung auf mehreren Computern

Zum Bereitstellen der Konfiguration auf mehreren Computern heruntergeladen, Sie müssen aktualisieren Sie das Skript **InstallJeaFeatures.ps1** , um den entsprechenden Sicherheitsgruppen für Ihre Umgebung, enthalten die Dateien auf einzelnen Computern kopieren, und Aufrufen der Das Skript.
Sie können Ihre bevorzugte Benutzeroberflächenautomatisierungs-Tools verwenden, zu diesem Zweck jedoch eine reine PowerShell-basierten Ansatz in diesem Artikel konzentrieren wird.

Standardmäßig wird das Skript auf dem Computer zum Steuern des Zugriffs auf die Funktionen lokalen Sicherheitsgruppen erstellt.
Dies eignet sich für Arbeitsgruppe und Domäne verbundene Computer, aber wenn Sie bereitstellen möchten, in einer Domäne nur Umgebung, um direkt können Sie jede Rolle eine Domänensicherheitsgruppe zuordnen.
Um die Konfiguration, um die Domäne Sicherheitsgruppen zu aktualisieren, öffnen Sie **InstallJeaFeatures.ps1** , und nehmen Sie die folgenden Änderungen:

1.  Entfernen Sie die 3 **Gruppe** Ressourcen aus der Datei:
    1.  "Gruppe MS-Reader-Group"
    2.  "Gruppe MS-Hyper-V-Administratoren-Group"
    3.  "Gruppe MS-Administratoren-Group"
2.  Entfernen Sie die 3 Gruppenressourcen aus der JeaEndpoint **DependsOn** -Eigenschaft
    1.  "[Gruppe] MS-Reader-Group"
    2.  "[Gruppe] MS-Hyper-V-Administratoren-Group"
    3.  "[Gruppe] MS-Administratoren-Group"
3.  Ändern Sie den Gruppennamen in der JeaEndpoint **RoleDefinitions** -Eigenschaft in Ihren gewünschten Sicherheitsgruppen. Ändern Sie beispielsweise, wenn Sie eine Sicherheitsgruppe *CONTOSO\MyTrustedAdmins* , die die Rolle Windows Admin Center Administratoren Zugriff zugewiesen werden soll verfügen, `'$env:COMPUTERNAME\Windows Admin Center Administrators'` , `'CONTOSO\MyTrustedAdmins'`. Die drei Zeichenfolgen, die Sie benötigen, um zu aktualisieren sind:
    1.  "$env: COMPUTERNAME\Windows Admin Center-Administratoren
    2.  "$env: COMPUTERNAME\Windows Admin Center Hyper-V-Administratoren
    3.  "$env: COMPUTERNAME\Windows Admin Center Readers'

> [!NOTE]
> Achten Sie darauf, dass Sie eindeutige Sicherheitsgruppen für jede Rolle verwenden. Konfiguration schlägt fehl, wenn die gleichen Sicherheitsgruppe mehrere Rollen zugewiesen ist.

Am Ende der Datei **InstallJeaFeatures.ps1** , fügen Sie die folgenden Zeilen von PowerShell zum Ende des Skripts:

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

Schließlich können Sie kopieren Sie den Ordner mit der Module, die DSC-Ressource und die Konfiguration für jeden Zielknoten und führen Sie das Skript **InstallJeaFeature.ps1** .
Remote aus Ihrer Administratorarbeitsstation dazu können Sie die folgenden Befehle ausführen:

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
