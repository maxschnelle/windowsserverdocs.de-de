---
title: Konfigurieren von Benutzer Zugriffs Steuerung und Berechtigungen
description: Erfahren Sie, wie Sie die Benutzer Zugriffs Steuerung und Berechtigungen mithilfe von Active Directory oder Azure AD (Project Honolulu) konfigurieren.
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.date: 06/07/2019
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: 20b311e9330880c2b26e2494aabe27bb04891868
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407032"
---
# <a name="configure-user-access-control-and-permissions"></a>Konfigurieren von Benutzer Access Control und Berechtigungen

> Gilt für: Windows Admin Center, Windows Admin Center-Vorschau

Wenn Sie dies noch nicht getan haben, machen Sie sich mit den [Benutzer Zugriffs Steuerungs Optionen im Windows Admin Center](../plan/user-access-options.md) vertraut.

> [!NOTE]
> Gruppen basierter Zugriff im Windows Admin Center wird in Arbeitsgruppen Umgebungen oder in nicht vertrauenswürdigen Domänen nicht unterstützt.

## <a name="gateway-access-role-definitions"></a>Gateway-Zugriffs Rollen Definitionen

Es gibt zwei Rollen für den Zugriff auf den Gateway-Dienst von Windows Admin Center:

**Gatewaybenutzer** können eine Verbindung mit dem Windows Admin Center Gateway-Dienst herstellen, um Server über dieses Gateway zu verwalten. Sie können jedoch weder die Zugriffsberechtigungen noch den Authentifizierungsmechanismus ändern, der für die Authentifizierung beim Gateway verwendet wird.

**Gatewayadministratoren** können konfigurieren, wer Zugriff erhält und wie sich Benutzer beim Gateway authentifizieren. Nur gatewayadministratoren können die Zugriffs Einstellungen im Windows Admin Center anzeigen und konfigurieren. Lokale Administratoren auf dem Gatewaycomputer sind immer Administratoren des Windows Admin Center-Gatewaydiensts.

> [!NOTE]
> Der Zugriff auf das Gateway impliziert nicht den Zugriff auf verwaltete Server, die durch das Gateway sichtbar sind. Um einen Zielserver zu verwalten, muss der Benutzer, der die Verbindung herstellt, Anmelde Informationen verwenden (entweder über die Pass-Through-Windows-Anmelde Informationen oder über die Anmelde Informationen, die in der Windows Admin Center-Sitzung mithilfe von " **verwalten als** " bereitgestellt werden auf diesen Zielserver.

## <a name="active-directory-or-local-machine-groups"></a>Active Directory oder lokale Computer Gruppen

Standardmäßig werden Active Directory oder lokale Computer Gruppen verwendet, um den Gatewayzugriff zu steuern. Wenn Sie über eine Active Directory Domäne verfügen, können Sie den gatewaybenutzer-und Administrator Zugriff über die Windows Admin Center-Schnittstelle verwalten.

Auf der Registerkarte **Benutzer** können Sie steuern, wer auf das Windows Admin Center als gatewaybenutzer zugreifen kann. Wenn Sie keine Sicherheitsgruppe angeben, hat jeder Benutzer, der auf die Gateway-URL zugreift, standardmäßig Zugriff. Nachdem Sie der Liste Benutzer eine oder mehrere Sicherheitsgruppen hinzugefügt haben, ist der Zugriff auf die Mitglieder dieser Gruppen beschränkt.

Wenn Sie in Ihrer Umgebung keine Active Directory Domäne verwenden, wird der Zugriff durch die lokalen Gruppen `Users` und `Administrators` auf dem Windows Admin Center-Gatewaycomputer gesteuert.

### <a name="smartcard-authentication"></a>Smartcardauthentifizierung

Sie können die **Smartcard-Authentifizierung** erzwingen, indem Sie eine zusätzliche _erforderliche_ Gruppe für Smartcard-basierte Sicherheitsgruppen angeben. Nachdem Sie eine smartcardbasierte Sicherheitsgruppe hinzugefügt haben, kann ein Benutzer nur auf den Windows Admin Center-Dienst zugreifen, wenn er Mitglied einer Sicherheitsgruppe und einer Smartcard-Gruppe in der Benutzerliste ist.

Auf der Registerkarte " **Administratoren** " können Sie steuern, wer auf das Windows Admin Center als gatewayadministrator zugreifen kann. Die lokale Gruppe "Administratoren" auf dem Computer hat immer vollen Administrator Zugriff und kann nicht aus der Liste entfernt werden. Durch das Hinzufügen von Sicherheitsgruppen erhalten Mitglieder dieser Gruppenberechtigungen zum Ändern der Einstellungen des Windows Admin Center-Gateways. Die Liste der Administratoren unterstützt die Smartcard-Authentifizierung auf die gleiche Weise wie die Benutzerliste: mit der and-Bedingung für eine Sicherheitsgruppe und eine smartcardgruppe.

## <a name="azure-active-directory"></a>Azure Active Directory

Wenn Ihre Organisation Azure Active Directory (Azure AD) verwendet, können Sie eine **zusätzliche** Sicherheitsebene zum Windows Admin Center hinzufügen, indem Sie für den Zugriff auf das Gateway Azure AD Authentifizierung benötigen. Um auf das Windows Admin Center zugreifen zu können, muss das **Windows-Konto** des Benutzers auch über Zugriff auf den Gatewayserver verfügen (auch wenn Azure AD Authentifizierung verwendet wird). Wenn Sie Azure AD verwenden, verwalten Sie die Zugriffsberechtigungen für Benutzer und Administratoren von Windows Admin Center über das Azure-Portal und nicht über die Benutzeroberfläche von Windows Admin Center.

### <a name="accessing-windows-admin-center-when-azure-ad-authentication-is-enabled"></a>Zugreifen auf das Windows Admin Center, wenn Azure AD Authentifizierung aktiviert ist

Abhängig vom verwendeten Browser erhalten einige Benutzer, die mit Azure AD Authentifizierung auf Windows Admin Center zugreifen, eine zusätzliche Eingabeaufforderung **vom Browser** , in der die Anmelde Informationen Ihres Windows-Kontos für den Computer bereitgestellt werden müssen, auf dem Windows Admin Center ist installiert. Nachdem Sie diese Informationen eingegeben haben, erhalten die Benutzer die zusätzliche Azure Active Directory Authentifizierungs Aufforderung, die die Anmelde Informationen eines Azure-Kontos erfordert, dem Zugriff in der Azure AD-Anwendung in Azure gewährt wurde.

> [!NOTE]
> Benutzer, die über **Administrator Rechte** auf dem Gatewaycomputer verfügen, werden nicht zur Azure AD Authentifizierung aufgefordert.

### <a name="configuring-azure-active-directory-authentication-for-windows-admin-center-preview"></a>Konfigurieren der Azure Active Directory Authentifizierung für das Windows Admin Center (Vorschau)

Wechseln Sie zu den **Einstellungen**des Windows Admin Centers  > **Access** , und schalten Sie mithilfe der UMSCHALT Fläche "verwenden Sie Azure Active Directory, um dem Gateway eine Sicherheitsebene hinzuzufügen". Wenn Sie das Gateway nicht bei Azure registriert haben, werden Sie zu diesem Zeitpunkt dazu geführt.

Standardmäßig verfügen alle Mitglieder des Azure AD Mandanten über Benutzer Zugriff auf den Gateway-Dienst von Windows Admin Center. Nur lokale Administratoren auf dem Gatewaycomputer verfügen über Administrator Zugriff auf das Windows Admin Center-Gateway. Beachten Sie, dass die Rechte lokaler Administratoren auf dem Gatewaycomputer nicht eingeschränkt werden können. lokale Administratoren können sämtliche Aktionen ausführen, unabhängig davon, ob Azure AD für die Authentifizierung verwendet wird.

Wenn Sie bestimmten Azure AD Benutzern oder Gruppen gatewaybenutzer oder gatewayadministrator Zugriff auf den Windows Admin Center-Dienst einräumen möchten, gehen Sie wie folgt vor:

1.  Navigieren Sie in der Azure-Portal zu Ihrem Windows Admin Center Azure AD Anwendung, indem Sie den in Zugriffs Einstellungen bereitgestellten Link verwenden. Beachten Sie, dass dieser Link nur verfügbar ist, wenn Azure Active Directory Authentifizierung aktiviert ist. 
    -   Sie können Ihre Anwendung auch im Azure-Portal finden, indem Sie zu **Azure Active Directory** > **Unternehmensanwendungen** > **alle Anwendungen** wechseln und **windowsadmincenter** suchen (die Azure AD App wird benannt Windowsadmincenter-<gateway name>). Wenn keine Suchergebnisse angezeigt werden, stellen Sie sicher, dass **alle Anwendungen** **anzeigen** , **Anwendungs Status** auf **beliebig** festgelegt ist, klicken Sie auf übernehmen, und versuchen Sie dann, die Suche auszuführen. Wenn Sie die Anwendung gefunden haben, wechseln Sie zu **Benutzer und Gruppen** .
2.  Legen Sie auf der Registerkarte Eigenschaften die **Benutzer Zuweisung erforderlich** auf Ja fest.
    Nachdem Sie dies getan haben, können nur Mitglieder, die auf der Registerkarte **Benutzer und Gruppen** aufgelistet sind, auf das Windows Admin Center-Gateway zugreifen.
3.  Wählen Sie auf der Registerkarte Benutzer und Gruppen die Option **Benutzer hinzufügen**aus. Sie müssen für jeden hinzugefügten Benutzer bzw. jede Gruppe eine gatewaybenutzerrolle oder Gateway-Administrator Rolle zuweisen

Wenn Sie Azure AD Authentifizierung aktivieren, wird der Gatewaydienst neu gestartet, und Sie müssen Ihren Browser aktualisieren. Sie können den Benutzer Zugriff für die Azure AD Anwendung für die KMU in der Azure-Portal jederzeit aktualisieren.

Benutzer werden aufgefordert, sich mit ihrer Azure Active Directory Identität anzumelden, wenn Sie versuchen, auf die Gateway-URL des Windows Admin Centers zuzugreifen. Beachten Sie, dass Benutzer auch Mitglied der lokalen Benutzer auf dem Gatewayserver sein müssen, um auf das Windows Admin Center zugreifen zu können.

Benutzer und Administratoren können das aktuell angemeldete Konto sowie die Abmeldung von diesem Azure AD Konto auf der Registerkarte **Konto** der Windows Admin Center-Einstellungen anzeigen.

### <a name="configuring-azure-active-directory-authentication-for-windows-admin-center"></a>Konfigurieren der Azure Active Directory Authentifizierung für das Windows Admin Center

Wenn [Sie Azure AD Authentifizierung einrichten möchten, müssen Sie Ihr Gateway zuerst bei Azure registrieren](azure-integration.md) (Sie müssen dies nur einmal für Ihr Windows Admin Center-Gateway durchführen). In diesem Schritt wird eine Azure AD Anwendung erstellt, mit der Sie den gatewaybenutzer-und Gateway-Administrator Zugriff verwalten können.

Wenn Sie bestimmten Azure AD Benutzern oder Gruppen gatewaybenutzer oder gatewayadministrator Zugriff auf den Windows Admin Center-Dienst einräumen möchten, gehen Sie wie folgt vor:

1.  Wechseln Sie in der Azure-Portal zu ihrer Azure AD Anwendung für die KMU. 
    -   Wenn Sie auf **Zugriffs Steuerung ändern** klicken und dann in den Zugriffs Einstellungen des Windows Admin Centers **Azure Active Directory** auswählen, können Sie den in der Benutzeroberfläche bereitgestellten Link verwenden, um auf die Azure AD Anwendung im Azure-Portal zuzugreifen. Dieser Link ist auch in den Zugriffs Einstellungen verfügbar, nachdem Sie auf Speichern klicken und Azure AD als Identitäts Anbieter für die Zugriffs Steuerung ausgewählt haben.
    -   Sie können Ihre Anwendung auch im Azure-Portal finden, indem Sie zu **Azure Active Directory** > **Unternehmensanwendungen** > **alle Anwendungen** wechseln und nach **KMU** suchen (die Azure AD-App wird als "SME-<gateway>" bezeichnet). Wenn keine Suchergebnisse angezeigt werden, stellen Sie sicher, dass **alle Anwendungen** **anzeigen** , **Anwendungs Status** auf **beliebig** festgelegt ist, klicken Sie auf übernehmen, und versuchen Sie dann, die Suche auszuführen. Wenn Sie die Anwendung gefunden haben, wechseln Sie zu **Benutzer und Gruppen** .
2.  Legen Sie auf der Registerkarte Eigenschaften die **Benutzer Zuweisung erforderlich** auf Ja fest.
    Nachdem Sie dies getan haben, können nur Mitglieder, die auf der Registerkarte **Benutzer und Gruppen** aufgelistet sind, auf das Windows Admin Center-Gateway zugreifen.
3.  Wählen Sie auf der Registerkarte Benutzer und Gruppen die Option **Benutzer hinzufügen**aus. Sie müssen für jeden hinzugefügten Benutzer bzw. jede Gruppe eine gatewaybenutzerrolle oder Gateway-Administrator Rolle zuweisen

Nachdem Sie die Azure AD Access Control im Bereich " **Zugriffs Steuerung ändern** " gespeichert haben, wird der Gatewaydienst neu gestartet, und Sie müssen Ihren Browser aktualisieren. Sie können den Benutzer Zugriff für das Windows Admin Center Azure AD Anwendung jederzeit in der Azure-Portal aktualisieren. 

Benutzer werden aufgefordert, sich mit ihrer Azure Active Directory Identität anzumelden, wenn Sie versuchen, auf die Gateway-URL des Windows Admin Centers zuzugreifen. Beachten Sie, dass Benutzer auch Mitglied der lokalen Benutzer auf dem Gatewayserver sein müssen, um auf das Windows Admin Center zugreifen zu können. 

Mithilfe der Registerkarte **Azure** in den allgemeinen Einstellungen des Windows Admin Centers können Benutzer und Administratoren ihr aktuell angemeldetes Konto anzeigen und sich bei diesem Azure AD Konto abmelden.

### <a name="conditional-access-and-multi-factor-authentication"></a>Bedingter Zugriff und Multi-Factor Authentication

Einer der Vorteile der Verwendung von Azure AD als zusätzliche Sicherheitsebene zum Steuern des Zugriffs auf das Windows Admin Center-Gateway besteht darin, dass Sie die leistungsstarken Sicherheitsfeatures von Azure AD nutzen können, wie z. b. bedingter Zugriff und Multi-Factor Authentication. 

[Weitere Informationen zum Konfigurieren des bedingten Zugriffs mit Azure Active Directory.](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal-get-started)

## <a name="configure-single-sign-on"></a>Konfigurieren des einmaligen Anmeldens

**Einmaliges Anmelden bei Bereitstellung als Dienst unter Windows Server**

Wenn Sie Windows Admin Center unter Windows 10 installieren, ist es für die Verwendung Single Sign-on bereit. Wenn Sie Windows Admin Center auf Windows Server verwenden möchten, müssen Sie jedoch eine Form der Kerberos-Delegierung in Ihrer Umgebung einrichten, bevor Sie Single Sign-on verwenden können. Die Delegierung konfiguriert den Gatewaycomputer als vertrauenswürdig für die Delegierung an den Zielknoten. 

Führen Sie die folgenden PowerShell-Cmdlets aus, um die [ressourcenbasierte eingeschränkte Delegierung](https://docs.microsoft.com/windows-server/security/kerberos/kerberos-constrained-delegation-overview) in Ihrer Umgebung zu konfigurieren. (Beachten Sie, dass dies einen Domänen Controller mit Windows Server 2012 oder höher erfordert).

```powershell
     $gateway = "WindowsAdminCenterGW" # Machine where Windows Admin Center is installed
     $node = "ManagedNode" # Machine that you want to manage
     $gatewayObject = Get-ADComputer -Identity $gateway
     $nodeObject = Get-ADComputer -Identity $node
     Set-ADComputer -Identity $nodeObject -PrincipalsAllowedToDelegateToAccount $gatewayObject
```

In diesem Beispiel wird das Windows Admin Center-Gateway auf dem Server **windowsadmincentergw**installiert, und der Name des Ziel Knotens lautet **managednode**.

Um diese Beziehung zu entfernen, führen Sie das folgende Cmdlet aus:

```powershell
Set-ADComputer -Identity $nodeObject -PrincipalsAllowedToDelegateToAccount $null
```

## <a name="role-based-access-control"></a>Rollenbasierte Zugriffsteuerung

Mit der rollenbasierten Zugriffs Steuerung können Sie Benutzern eingeschränkten Zugriff auf den Computer gewähren, anstatt sie vollständig als lokale Administratoren zu erstellen.
[Weitere Informationen finden Sie unter Rollenbasierte Zugriffs Steuerung und verfügbare Rollen.](../plan/user-access-options.md#role-based-access-control)

Das Einrichten von RBAC besteht aus zwei Schritten: Aktivieren der Unterstützung auf den Ziel Computern und Zuweisen von Benutzern zu den relevanten Rollen.

> [!TIP]
> Stellen Sie sicher, dass Sie über lokale Administratorrechte auf den Computern verfügen, auf denen Sie die Unterstützung für die rollenbasierte Zugriffs Steuerung konfigurieren.

### <a name="apply-role-based-access-control-to-a-single-machine"></a>Anwenden der rollenbasierten Zugriffs Steuerung auf einen einzelnen Computer

Das Bereitstellungs Modell mit einem einzelnen Computer eignet sich ideal für einfache Umgebungen, in denen nur wenige Computer verwaltet werden können.
Wenn Sie einen Computer mit Unterstützung für die rollenbasierte Zugriffs Steuerung konfigurieren, werden folgende Änderungen vorgenommen:

-   PowerShell-Module mit Funktionen, die für das Windows Admin Center erforderlich sind, werden auf dem Systemlaufwerk unter `C:\Program Files\WindowsPowerShell\Modules` installiert. Alle Module werden mit **Microsoft. SME gestartet.**
-   Die Konfiguration des gewünschten Zustands führt eine einmalige Konfiguration aus, um einen gerade ausreichenden Verwaltungs Endpunkt auf dem Computer mit dem Namen " **Microsoft. SME. PowerShell**" zu konfigurieren. Dieser Endpunkt definiert die drei von Windows Admin Center verwendeten Rollen und wird als temporärer lokaler Administrator ausgeführt, wenn ein Benutzer eine Verbindung mit dem Endpunkt herstellt.
-   drei neue lokale Gruppen werden erstellt, um zu steuern, welchen Benutzern der Zugriff auf welche Rollen zugewiesen wird:
    -   Administratoren des Windows Admin Centers
    -   Hyper-V-Administratoren für Windows Admin Center
    -   Leser des Windows Admin Centers

Führen Sie die folgenden Schritte aus, um die Unterstützung für die rollenbasierte Zugriffs Steuerung auf einem einzelnen Computer zu aktivieren:

1.  Öffnen Sie das Windows Admin Center, und stellen Sie eine Verbindung mit dem Computer her, den Sie mit der rollenbasierten Zugriffs Steuerung mit einem Konto mit lokalen Administratorrechten auf dem Zielcomputer konfigurieren möchten.
2.  Klicken Sie im **Übersichts** Tool auf **Einstellungen** > **rollenbasierte Zugriffs Steuerung**.
3.  Klicken Sie unten auf der Seite auf **anwenden** , um die Unterstützung für die rollenbasierte Zugriffs Steuerung auf dem Bereitstellungs Zielcomputer zu aktivieren. Der Anwendungsprozess umfasst das Kopieren von PowerShell-Skripts und das Aufrufen einer Konfiguration (mithilfe von PowerShell DSC) auf dem Zielcomputer. Es kann bis zu 10 Minuten dauern, bis WinRM neu gestartet wird. Dadurch werden Windows Admin Center, PowerShell und WMI-Benutzer vorübergehend getrennt.
4.  Aktualisieren Sie die Seite, um den Status der rollenbasierten Zugriffs Steuerung zu überprüfen. Wenn Sie einsatzbereit ist, ändert sich der Status in **angewendet**.

Nach dem Anwenden der Konfiguration können Sie den Rollen Benutzer zuweisen:

1.  Öffnen Sie das Tool **lokale Benutzer und Gruppen** , und navigieren Sie zur Registerkarte **Gruppen** .
2.  Wählen Sie die Gruppe **Leser des Windows Admin Centers** aus.
3.  Klicken Sie im *Detail* Bereich unten auf **Benutzer hinzufügen** , und geben Sie den Namen eines Benutzers oder einer Sicherheitsgruppe ein, der über das Windows Admin Center Lesezugriff auf den Server haben soll. Die Benutzer und Gruppen können von dem lokalen Computer oder Ihrer Active Directory Domäne stammen.
4.  Wiederholen Sie die Schritte 2-3 für die Gruppen **Windows Admin Center Hyper-V-Administratoren** und **Windows Admin Center-Administratoren** .

Sie können diese Gruppen auch einheitlich in Ihrer Domäne auffüllen, indem Sie ein Gruppenrichtlinie-Objekt mit der [Richtlinien Einstellung eingeschränkte Gruppen](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc756802%28v=ws.10%29)konfigurieren.

### <a name="apply-role-based-access-control-to-multiple-machines"></a>Anwenden der rollenbasierten Zugriffs Steuerung auf mehrere Computer

In einer großen Unternehmens Bereitstellung können Sie Ihre vorhandenen Automation-Tools verwenden, um das Feature der rollenbasierten Zugriffs Steuerung an Ihre Computer zu übermitteln, indem Sie das Konfigurations Paket vom Windows Admin Center-Gateway herunterladen.
Das Konfigurations Paket ist für die Verwendung mit der PowerShell-Konfiguration für den gewünschten Zustand konzipiert, aber Sie können es für Ihre bevorzugte Automatisierungslösung anpassen.

#### <a name="download-the-role-based-access-control-configuration"></a>Herunterladen der rollenbasierten Zugriffs Steuerungs Konfiguration

Um das rollenbasierte Zugriffs Steuerungs Paket herunterzuladen, benötigen Sie Zugriff auf das Windows Admin Center und eine PowerShell-Eingabeaufforderung.

Wenn Sie das Windows Admin Center-Gateway im Dienst Modus unter Windows Server ausführen, verwenden Sie den folgenden Befehl, um das Konfigurations Paket herunterzuladen.
Stellen Sie sicher, dass Sie die Gatewayadresse mit der richtigen für Ihre Umgebung aktualisieren.

```powershell
$WindowsAdminCenterGateway = 'https://windowsadmincenter.contoso.com'
Invoke-RestMethod -Uri "$WindowsAdminCenterGateway/api/nodes/all/features/jea/endpoint/export" -Method POST -UseDefaultCredentials -OutFile "~\Desktop\WindowsAdminCenter_RBAC.zip"
```

Wenn Sie das Windows Admin Center-Gateway auf Ihrem Windows 10-Computer ausführen, führen Sie stattdessen den folgenden Befehl aus:

```powershell
$cert = Get-ChildItem Cert:\CurrentUser\My | Where-Object Subject -eq 'CN=Windows Admin Center Client' | Select-Object -First 1
Invoke-RestMethod -Uri "https://localhost:6516/api/nodes/all/features/jea/endpoint/export" -Method POST -Certificate $cert -OutFile "~\Desktop\WindowsAdminCenter_RBAC.zip"
```

Wenn Sie das ZIP-Archiv erweitern, sehen Sie die folgende Ordnerstruktur:

- Installjeafeaturen. ps1
- Justenoughadministration (Verzeichnis)
- Module (Verzeichnis)
    - Microsoft. SME. \* (Verzeichnisse)
    - Windowsadmincenter. Jea (Verzeichnis)

Zum Konfigurieren der Unterstützung für die rollenbasierte Zugriffs Steuerung auf einem Knoten müssen Sie die folgenden Aktionen ausführen:

1.  Kopieren Sie die Module justenoughadministration, Microsoft. SME. \* und windowsadmincenter. Jea in das PowerShell-Modul Verzeichnis auf dem Zielcomputer. Dies befindet sich in der Regel auf `C:\Program Files\WindowsPowerShell\Modules`.
2.  Aktualisieren Sie die Datei " **installjeafeatur. ps1** " entsprechend der gewünschten Konfiguration für den RBAC-Endpunkt.
3.  Führen Sie installjeafekl. ps1 aus, um die DSC-Ressource zu kompilieren.
4.  Stellen Sie die DSC-Konfiguration auf allen ihren Computern bereit, um die Konfiguration anzuwenden.

Im folgenden Abschnitt wird erläutert, wie dies mithilfe von PowerShell-Remoting durchzuführen ist.

#### <a name="deploy-on-multiple-machines"></a>Auf mehreren Computern bereitstellen

Zum Bereitstellen der Konfiguration, die Sie auf mehrere Computer heruntergeladen haben, müssen Sie das Skript " **installjeafeaturen. ps1** " aktualisieren, um die entsprechenden Sicherheitsgruppen für Ihre Umgebung aufzunehmen, die Dateien auf jeden Computer kopieren und das Konfigurations Skripts.
Hierfür können Sie Ihre bevorzugten Automatisierungstools verwenden. dieser Artikel konzentriert sich jedoch auf einen reinen PowerShell-basierten Ansatz.

Standardmäßig werden vom Konfigurationsskript lokale Sicherheitsgruppen auf dem Computer erstellt, um den Zugriff auf die einzelnen Rollen zu steuern.
Dies eignet sich für Arbeitsgruppen und in die Domäne eingebundenen Computern. Wenn Sie jedoch in einer reinen Domänen Umgebung bereitstellen, möchten Sie möglicherweise jeder Rolle eine Domänen Sicherheitsgruppe direkt zuordnen.
Um die Konfiguration für die Verwendung von Domänen Sicherheitsgruppen zu aktualisieren, öffnen Sie **installjeafeaturen. ps1** , und nehmen Sie die folgenden Änderungen vor:

1.  Entfernen Sie die drei **Gruppen** Ressourcen aus der Datei:
    1.  "Gruppe MS-Readers-Group"
    2.  "Gruppe MS-Hyper-V-Administrators-Gruppe"
    3.  "Gruppe MS-Administratoren-Gruppe"
2.  Entfernen Sie die drei Gruppen Ressourcen aus der jeaendpoint **DependsOn** -Eigenschaft.
    1.  "[Gruppe] MS-Readers-Group"
    2.  "[Gruppe] MS-Hyper-V-Administrators-Gruppe"
    3.  "[Gruppe] MS-Administrators-Gruppe"
3.  Ändern Sie die Gruppennamen in der jeaendpoint **roledefinitions** -Eigenschaft in die gewünschten Sicherheitsgruppen. Wenn Sie z. b. die Sicherheitsgruppe *condeso\meinetretsdadmins* haben, denen der Zugriff auf die Administrator Rolle des Windows Admin Centers zugewiesen werden soll, ändern Sie `'$env:COMPUTERNAME\Windows Admin Center Administrators'` in `'CONTOSO\MyTrustedAdmins'`. Die drei Zeichen folgen, die Sie aktualisieren müssen, lauten wie folgt:
    1.  "$ENV: computername\windows Admin Center-Administratoren"
    2.  "$ENV: computername\windows Admin Center Hyper-V-Administratoren"
    3.  "$ENV: computername\windows Admin Center Readers"

> [!NOTE]
> Stellen Sie sicher, dass Sie für jede Rolle eindeutige Sicherheitsgruppen verwenden. Die Konfiguration schlägt fehl, wenn der gleichen Sicherheitsgruppe mehrere Rollen zugewiesen sind.

Fügen Sie dann am Ende der Datei " **installjeafeaturen. ps1** " am Ende des Skripts die folgenden PowerShell-Zeilen hinzu:

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

Schließlich können Sie den Ordner, der die Module, die DSC-Ressource und die Konfiguration enthält, auf jeden Zielknoten kopieren und das Skript " **installjeafeatur. ps1** " ausführen.
Um dies Remote von ihrer admin-Arbeitsstation aus auszuführen, können Sie die folgenden Befehle ausführen:

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
