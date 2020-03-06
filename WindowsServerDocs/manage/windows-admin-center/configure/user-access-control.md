---
title: Konfigurieren der Benutzerzugriffssteuerung und von Berechtigungen
description: Erfahre, wie du die Benutzerzugriffssteuerung und Berechtigungen mithilfe von Active Directory oder Azure AD (Project Honolulu) konfigurierst.
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.date: 06/07/2019
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: 39af45506ff7023cebe437992e90f6d4ec051333
ms.sourcegitcommit: 06ae7c34c648538e15c4d9fe330668e7df32fbba
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/05/2020
ms.locfileid: "78371712"
---
# <a name="configure-user-access-control-and-permissions"></a>Konfigurieren der Benutzerzugriffssteuerung und von Berechtigungen

> Gilt für: Windows Admin Center, Windows Admin Center Preview

Wenn du dies noch nicht getan haben, mache dich mit den [Benutzerzugriffssteuerungs-Optionen im Windows Admin Center](../plan/user-access-options.md) vertraut.

> [!NOTE]
> Gruppenbasierter Zugriff im Windows Admin Center wird in Arbeitsgruppenumgebungen oder über vertrauenswürdige Domänen hinweg nicht unterstützt.

## <a name="gateway-access-role-definitions"></a>Rollendefinitionen für Gatewayzugriff

Es gibt zwei Rollen für den Zugriff auf den Gatewaydienst von Windows Admin Center:

**Gatewaybenutzer** können eine Verbindung mit dem Windows Admin Center-Gateway herstellen, um Servern über dieses Gateway zu verwalten, aber sie können weder die Zugriffsberechtigungen noch den Authentifizierungsmechanismus ändern, der zum Authentifizieren des Gateways verwendet wird.

**Gatewayadministratoren** können konfigurieren, wer Zugriff erhält und wie sich Benutzer beim Gateway authentifizieren. Nur Gatewayadministratoren können die Zugriffseinstellungen im Windows Admin Center anzeigen und konfigurieren. Lokale Administratoren auf dem Gatewaycomputer sind immer Administratoren des Windows Admin Center-Gatewaydiensts.

> [!NOTE]
> Der Zugriff auf das Gateway impliziert nicht den Zugriff auf verwaltete Server, die durch das Gateway sichtbar sind. Um einen Zielserver zu verwalten, muss der sich verbindende Benutzer Anmeldeinformationen verwenden (entweder über seine weitergeleiteten Windows-Anmeldeinformationen oder über Anmeldeinformationen, die in der Windows Admin Center-Sitzung mit der Aktion **Verwalten als** bereitgestellt werden), die über Administratorzugriff auf diesen Zielserver verfügen.

## <a name="active-directory-or-local-machine-groups"></a>Active Directory- oder lokale Computergruppen

Standardmäßig werden Active Directory- oder lokale Computergruppen verwendet, um den Gatewayzugriff zu steuern. Wenn du über eine Active Directory-Domäne verfügst, kannst du den Gatewaybenutzer- und Administratorzugriff über die Windows Admin Center-Schnittstelle verwalten.

Auf der Registerkarte **Benutzer** kannst du steuern, wer als Gatewaybenutzer auf das Windows Admin Center zugreifen kann. Standardmäßig, und wenn du keine Sicherheitsgruppe angibst, hat jeder Benutzer, der auf die Gateway-URL zugreift, Zugriff. Nachdem du der Benutzerliste eine oder mehrere Sicherheitsgruppen hinzugefügt hast, ist der Zugriff auf die Mitglieder dieser Gruppen beschränkt.

Wenn du in deiner Umgebung keine Active Directory-Domäne verwendest, wird der Zugriff durch die lokalen Gruppen `Users` und `Administrators` auf dem Windows Admin Center-Gatewaycomputer gesteuert.

### <a name="smartcard-authentication"></a>Smartcard-Authentifizierung

Du kannst **Smartcard-Authentifizierung** erzwingen, indem du eine zusätzliche, für Smartcard-basierte Sicherheitsgruppen _erforderliche Gruppe_ angibst. Nachdem du eine Smartcard-basierte Sicherheitsgruppe hinzugefügt hast, kann ein Benutzer nur auf den Windows Admin Center-Dienst zugreifen, wenn er Mitglied einer beliebigen Sicherheitsgruppe UND einer in der Benutzerliste enthaltenen Smartcard-Gruppe ist.

Auf der Registerkarte **Administratoren** kannst du steuern, wer als Gatewaybenutzer auf das Windows Admin Center zugreifen kann. Die lokale Gruppe „Administratoren“" auf dem Computer hat immer vollständigen Administratorzugriff und kann nicht aus der Liste entfernt werden. Durch das Hinzufügen von Sicherheitsgruppen erteilst du Mitgliedern dieser Gruppen Berechtigungen zum Ändern der Einstellungen des Windows Admin Center-Gateways. Die Liste der Administratoren unterstützt Smartcard-Authentifizierung auf dieselbe Weise wie die Benutzerliste: mit der UND-Bedingung für eine Sicherheitsgruppe und eine Smartcard-Gruppe.

## <a name="azure-active-directory"></a>Azure Active Directory

Wenn deine Organisation Azure Active Directory (Azure AD) verwendet, kannst du dich dafür entscheiden, Windows Admin Center eine **zusätzliche** Sicherheitsschicht hinzuzufügen, indem du für den Zugriff auf das Gateway die Azure AD-Authentifizierung verlangst. Um auf das Windows Admin Center zuzugreifen muss das **Windows-Konto** des Benutzers auch Zugriff auf den Gatewayserver haben (selbst wenn Azure AD-Authentifizierung verwendet wird). Wenn du Azure AD verwendest, verwaltest du die Windows Admin Center-Zugriffsberechtigungen für Benutzer und Administratoren über das Azure-Portal, anstatt über die Windows Admin Center-Benutzeroberfläche.

### <a name="accessing-windows-admin-center-when-azure-ad-authentication-is-enabled"></a>Zugreifen auf das Windows Admin Center bei aktivierter Azure AD-Authentifizierung

Abhängig vom verwendeten Browser erhalten einige Benutzer, die mit konfigurierter Azure AD-Authentifizierung auf Windows Admin Center zugreifen, eine zusätzliche Eingabeaufforderung **aus dem Browser**, in der sie die Anmeldeinformationen ihres Windows-Kontos für den Computer angeben müssen, auf dem Windows Admin Center installiert ist. Nachdem du diese Informationen eingegeben hast, erhalten die Benutzer die zusätzliche Azure Active Directory-Authentifizierungsaufforderung, für die die Anmeldeinformationen eines Azure-Kontos erforderlich sind, dem Zugriff in der Azure AD-Anwendung in Azure gewährt wurde.

> [!NOTE]
> Benutzer, deren Windows-Konto auf dem Gatewaycomputer **Administratorrechte** besitzt, werden nicht zur Azure AD-Authentifizierung aufgefordert.

### <a name="configuring-azure-active-directory-authentication-for-windows-admin-center-preview"></a>Konfigurieren der Azure Active Directory-Authentifizierung für Windows Admin Center Preview

Wechsle im Windows Admin Center zu **Einstellungen** > **Zugriff**, und aktiviere über die Umschaltfläche „Verwenden von Azure Active Directory, um dem Gateway eine Sicherheitsschicht hinzuzufügen“. Wenn du das Gateway nicht bei Azure registriert hast, wirst du zu diesem Zeitpunkt dazu angeleitet.

Standardmäßig verfügen alle Mitglieder des Azure AD-Mandanten über Benutzerzugriff auf den Gatewaydienst von Windows Admin Center. Nur lokale Administratoren auf dem Gatewaycomputer besitzen Administratorzugriff auf das Windows Admin Center-Gateway. Beachte, dass die Rechte lokaler Administratoren auf dem Gatewaycomputer nicht eingeschränkt werden können. Lokale Administratoren können sämtliche Aktionen ausführen, unabhängig davon, ob Azure AD für die Authentifizierung verwendet wird.

Wenn du bestimmten Azure AD-Benutzern oder -Gruppen Gatewaybenutzer- oder Gatewayadministratorzugriff auf den Windows Admin Center-Dienst erteilen möchtest, gehe wie folgt vor:

1.  Wechsel zu deiner Windows Admin Center Azure AD-Anwendung im Azure-Portal, indem du den in den Zugriffseinstellungen bereitgestellten Link verwendest. Beachte, dass dieser Link nur verfügbar ist, wenn Azure Active Directory-Authentifizierung aktiviert ist. 
    -   Du kannst deine Anwendung auch im Azure-Portal finden, indem du zu **Azure Active Directory** > **Unternehmensanwendungen** > **Alle Anwendungen** wechselst und **WindowsAdminCenter** suchst (die Azure AD-App heißt „WindowsAdminCenter“<gateway name>). Wenn du keine Suchergebnisse erhältst, vergewissere dich, dass **Anzeigen** auf **Alle Anwendungen** festgelegt ist, dass **Anwendungsstatus** auf **Beliebig** festgelegt ist, klicke dann auf „Anwenden“, und versuche, deine Suche auszuführen. Nachdem du die Anwendung gefunden hast, wechsle zu **Benutzer und Gruppen**.
2.  Lege auf der Registerkarte „Eigenschaften“ **Benutzerzuweisung erforderlich** auf „Ja“ fest.
    Nachdem du dies getan hast, können nur Mitglieder, die auf der Registerkarte **Benutzer und Gruppen** aufgelistet sind, auf das Windows Admin Center-Gateway zugreifen.
3.  Wähle auf der Registerkarte „Benutzer und Gruppen“ **Benutzer hinzufügen** aus. Du musst für jede/n hinzugefügte/n Benutzer/Gruppe eine Gatewaybenutzer- oder Gatewayadministratorrolle zuweisen.

Sobald du Azure AD-Authentifizierung aktiviert hast, wird der Gatewaydienst neu gestartet, und du musst deinen Browser aktualisieren. Du kannst den Benutzerzugriff für die Azure AD-Anwendung SME jederzeit im Azure-Portal aktualisieren.

Benutzer werden aufgefordert, sich mit ihrer Azure Active Directory-Identität anzumelden, wenn sie versuchen, auf die Gateway-URL des Windows Admin Centers zuzugreifen. Denke daran, dass Benutzer ebenfalls Mitglied der lokalen Benutzergruppe auf dem Gatewayserver sein müssen, um auf das Windows Admin Center zugreifen zu können.

Benutzer und Administratoren können auf der Registerkarte **Konto** in den Windows Admin Center-Einstellungen sowohl ihr aktuell angemeldetes Konto anzeigen als auch sich bei diesem Azure AD-Konto abmelden.

### <a name="configuring-azure-active-directory-authentication-for-windows-admin-center"></a>Konfigurieren der Azure Active Directory-Authentifizierung für Windows Admin Center

[Um Azure AD-Authentifizierung einzurichten, musst du zuerst dein Gateway bei Azure registrieren](azure-integration.md) (du musst dies nur einmal für dein Windows Admin Center-Gateway durchführen). In diesem Schritt wird eine Azure AD Anwendung erstellt, mit der du den Gatewaybenutzer- und Gatewayadministratorzugriff verwalten kannst.

Wenn du bestimmten Azure AD-Benutzern oder -Gruppen Gatewaybenutzer- oder Gatewayadministratorzugriff auf den Windows Admin Center-Dienst erteilen möchtest, gehe wie folgt vor:

1.  Wechsle im Azure-Portal zu deiner Azure AD-Anwendung SME. 
    -   Wenn du auf **Zugriffssteuerung ändern** klickst und dann in den Zugriffseinstellungen des Windows Admin Centers **Azure Active Directory** auswählst, kannst du den in der Benutzeroberfläche bereitgestellten Link verwenden, um auf deine Azure AD-Anwendung im Azure-Portal zuzugreifen. Dieser Link ist auch in den Zugriffseinstellungen verfügbar, nachdem du auf „Speichern“ geklickt und Azure AD als Identitätsanbieter für die Zugriffssteuerung ausgewählt hast.
    -   Du kannst deine Anwendung auch im Azure-Portal finden, indem du zu **Azure Active Directory** > **Unternehmensanwendungen** > **Alle Anwendungen** wechselst und **SME** suchst (die Azure AD-App heißt „SME“<gateway>). Wenn du keine Suchergebnisse erhältst, vergewissere dich, dass **Anzeigen** auf **Alle Anwendungen** festgelegt ist, dass **Anwendungsstatus** auf **Beliebig** festgelegt ist, klicke dann auf „Anwenden“, und versuche, deine Suche auszuführen. Nachdem du die Anwendung gefunden hast, wechsle zu **Benutzer und Gruppen**.
2.  Lege auf der Registerkarte „Eigenschaften“ **Benutzerzuweisung erforderlich** auf „Ja“ fest.
    Nachdem du dies getan hast, können nur Mitglieder, die auf der Registerkarte **Benutzer und Gruppen** aufgelistet sind, auf das Windows Admin Center-Gateway zugreifen.
3.  Wähle auf der Registerkarte „Benutzer und Gruppen“ **Benutzer hinzufügen** aus. Du musst für jede/n hinzugefügte/n Benutzer/Gruppe eine Gatewaybenutzer- oder Gatewayadministratorrolle zuweisen.

Sobald du die Azure AD-Zugriffssteuerung im Bereich **Zugriffssteuerung ändern** gespeichert hast, wird der Gatewaydienst neu gestartet, und du musst deinen Browser aktualisieren. Du kannst den Benutzerzugriff für die Windows Admin Center Azure AD-Anwendung jederzeit im Azure-Portal aktualisieren. 

Benutzer werden aufgefordert, sich mit ihrer Azure Active Directory-Identität anzumelden, wenn sie versuchen, auf die Gateway-URL des Windows Admin Centers zuzugreifen. Denke daran, dass Benutzer ebenfalls Mitglied der lokalen Benutzergruppe auf dem Gatewayserver sein müssen, um auf das Windows Admin Center zugreifen zu können. 

Auf der Registerkarte **Azure** in den allgemeinen Windows Admin Center-Einstellungen können Benutzer und Administratoren sowohl ihr aktuell angemeldetes Konto anzeigen als auch sich bei diesem Azure AD-Konto abmelden.

### <a name="conditional-access-and-multi-factor-authentication"></a>Bedingter Zugriff und mehrstufige Authentifizierung

Einer der Vorteile der Verwendung von Azure AD als zusätzliche Sicherheitsschicht zum Steuern des Zugriffs auf das Windows Admin Center-Gateway besteht darin, dass du die leistungsstarken Sicherheitsfeatures von Azure AD nutzen kannst wie bedingten Zugriff und mehrstufige Authentifizierung. 

[Weitere Informationen zum Konfigurieren des bedingten Zugriffs mit Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal-get-started).

## <a name="configure-single-sign-on"></a>Einmaliges Anmelden konfigurieren

**Einmaliges Anmelden bei Bereitstellung als Dienst unter Windows Server**

Wenn du Windows Admin Center unter Windows 10 installierst, ist es bereit für die Verwendung der einmaligen Anmeldung. Wenn du Windows Admin Center unter Windows Server verwenden möchtest, musst du jedoch eine Form der Kerberos-Delegierung in deiner Umgebung einrichten, bevor du einmaliges Anmelden verwenden kannst. Die Delegierung konfiguriert den Gatewaycomputer als vertrauenswürdig für die Delegierung an den Zielknoten. 

Um [ressourcenbasierte eingeschränkte Delegierung](https://docs.microsoft.com/windows-server/security/kerberos/kerberos-constrained-delegation-overview) in deiner Umgebung zu konfigurieren, verwendest du folgendes PowerShell-Beispiel. Dieses Beispiel zeigt, wie Sie einen Windows-Server [node01.contoso.com] so konfigurieren, dass die Delegierung von Ihrem Windows Admin Center-Gateway [WAC.contoso.com] in der contoso.com-Domäne angenommen wird.

```powershell
Set-ADComputer -Identity (Get-ADComputer node01) -PrincipalsAllowedToDelegateToAccount (Get-ADComputer wac)
```

Um diese Beziehung zu entfernen, führst du das folgende Cmdlet aus:

```powershell
Set-ADComputer -Identity (Get-ADComputer node01) -PrincipalsAllowedToDelegateToAccount $null
```

## <a name="role-based-access-control"></a>Rollenbasierte Zugriffsteuerung

Mit der rollenbasierten Zugriffssteuerung (Role-Based Access Control, RBAC) kannst du Benutzern eingeschränkten Zugriff auf den Computer gewähren, anstatt sie zu vollständigen lokalen Administratoren zu machen.
[Weitere Informationen zur rollenbasierten Zugriffssteuerung und den verfügbaren Rollen](../plan/user-access-options.md#role-based-access-control).

Das Einrichten von RBAC besteht aus 2 Schritten: Aktivieren der Unterstützung auf den Zielcomputern und Zuweisen von Benutzern zu den relevanten Rollen.

> [!TIP]
> Stelle sicher, dass du über lokale Administratorrechte auf den Computern verfügst, auf denen du die Unterstützung für die rollenbasierte Zugriffssteuerung konfigurierst.

### <a name="apply-role-based-access-control-to-a-single-machine"></a>Anwenden der rollenbasierten Zugriffssteuerung auf einen einzelnen Computer

Das Modell für die Bereitstellung auf einem einzelnen Computer eignet sich ideal für einfache Umgebungen, in denen nur wenige Computer verwaltet werden.
Die Konfiguration eines Computers mit Unterstützung für die rollenbasierte Zugriffssteuerung führt zu folgenden Änderungen:

-   PowerShell-Module mit Funktionen, die für das Windows Admin Center erforderlich sind, werden auf deinem Systemlaufwerk unter `C:\Program Files\WindowsPowerShell\Modules` installiert. Alle Module beginnen mit **Microsoft.Sme**.
-   Die Desired State Configuration (Konfiguration des gewünschten Zustands, DSC) führt eine einmalige Konfiguration aus, um einen „Just Enough Administration“-Endpunkt (JEA) namens **Microsoft.Sme.PowerShell** auf dem Computer zu konfigurieren. Dieser Endpunkt definiert die 3 von Windows Admin Center verwendeten Rollen und wird als temporärer lokaler Administrator ausgeführt, wenn ein Benutzer eine Verbindung damit herstellt.
-   3 neue lokale Gruppen werden erstellt, um zu steuern, welchen Benutzern der Zugriff auf welche Rollen zugewiesen wird:
    -   Windows Admin Center-Administratoren
    -   Windows Admin Center Hyper-V-Administratoren
    -   Windows Admin Center-Leser

Um die Unterstützung für die rollenbasierte Zugriffssteuerung auf einem einzelnen Computer zu aktivieren, führe diese folgenden Schritte durch:

1.  Öffne das Windows Admin Center, und stelle mit einem Konto mit lokalen Administratorrechten auf dem Zielcomputer eine Verbindung mit dem Computer her, den du mit der rollenbasierten Zugriffssteuerung konfigurieren möchtest.
2.  Klicke im Tool **Übersicht** auf **Einstellungen** > **Rollenbasierte Zugriffssteuerung**.
3.  Klicke unten auf der Seite auf **Anwenden**, um die Unterstützung für die rollenbasierte Zugriffssteuerung auf dem Zielcomputer zu aktivieren. Der Anwendungsprozess umfasst das Kopieren von PowerShell-Skripts sowie das Aufrufen einer Konfiguration (mithilfe von PowerShell DSC) auf dem Zielcomputer. Bis zum Abschluss des Vorgangs kann es bis zu 10 Minuten dauern, und anschließend wird WinRM neu gestartet. Hierdurch werden Windows Admin Center-, PowerShell- und WMI-Benutzer vorübergehend getrennt.
4.  Aktualisiere die Seite, um den Status der rollenbasierten Zugriffssteuerung zu überprüfen. Wenn sie einsatzbereit ist, ändert sich der Status in **Angewendet**.

Nach dem Anwenden der Konfiguration kannst du den Rollen Benutzer zuweisen:

1.  Öffne das Tool **Lokale Benutzer und Gruppen**, und navigiere zur Registerkarte **Gruppen**.
2.  Wähle die Gruppe **Windows Admin Center-Leser** aus.
3.  Klicke im Bereich *Details* am unteren Rand auf **Benutzer hinzufügen**, und gib den Namen eines Benutzers oder einer Sicherheitsgruppe ein, der/die schreibgeschützten Zugriff über das Windows Admin Center auf den Server erhalten soll. Die Benutzer und Gruppen können von dem lokalen Computer oder aus deiner Active Directory-Domäne stammen.
4.  Wiederhole die Schritte 2 bis 3 für die Gruppen **Windows Admin Center Hyper-V-Administratoren** und **Windows Admin Center-Administratoren**.

Du kannst diese Gruppen auch konsistent in deiner ganzen Domäne auffüllen, indem du ein Gruppenrichtlinienobjekt mit der [Richtlinieneinstellung für eingeschränkte Gruppen](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc756802%28v=ws.10%29) konfigurierst.

### <a name="apply-role-based-access-control-to-multiple-machines"></a>Anwenden der rollenbasierten Zugriffssteuerung auf mehrere Computer

In einer großen Unternehmensbereitstellung kannst du deine vorhandenen Automatisierungstools verwenden, um die Funktion für rollenbasierte Zugriffssteuerung auf deine Computer zu übertragen, indem du das Konfigurationspaket vom Windows Admin Center-Gateway herunterlädst.
Das Konfigurationspaket ist für die Verwendung mit PowerShell DSC gedacht, aber du kannst es so anpassen, dass es mit deiner bevorzugten Automatisierungslösung arbeitet.

#### <a name="download-the-role-based-access-control-configuration"></a>Herunterladen der Konfiguration für die rollenbasierte Zugriffssteuerung

Um das Konfigurationspaket für die rollenbasierte Zugriffssteuerung herunterzuladen, benötigst du Zugriff auf das Windows Admin Center und eine PowerShell-Eingabeaufforderung.

Wenn du das Windows Admin Center-Gateway im Wartungsmodus unter Windows Server ausführst, verwende den folgenden Befehl, um das Konfigurationspaket herunterzuladen.
Stelle sicher, dass du die Gatewayadresse mit der richtigen für deine Umgebung aktualisierst.

```powershell
$WindowsAdminCenterGateway = 'https://windowsadmincenter.contoso.com'
Invoke-RestMethod -Uri "$WindowsAdminCenterGateway/api/nodes/all/features/jea/endpoint/export" -Method POST -UseDefaultCredentials -OutFile "~\Desktop\WindowsAdminCenter_RBAC.zip"
```

Wenn du das Windows Admin Center-Gateway auf deinem Windows 10-Computer ausführst, führe stattdessen den folgenden Befehl aus:

```powershell
$cert = Get-ChildItem Cert:\CurrentUser\My | Where-Object Subject -eq 'CN=Windows Admin Center Client' | Select-Object -First 1
Invoke-RestMethod -Uri "https://localhost:6516/api/nodes/all/features/jea/endpoint/export" -Method POST -Certificate $cert -OutFile "~\Desktop\WindowsAdminCenter_RBAC.zip"
```

Wenn du das ZIP-Archiv erweiterst, wird folgende Ordnerstruktur angezeigt:

- InstallJeaFeatures.ps1
- JustEnoughAdministration (Verzeichnis)
- Module (Verzeichnis)
    - Microsoft.SME.\* (Verzeichnisse)
    - WindowsAdminCenter.Jea (Verzeichnis)

Um die Unterstützung für rollenbasierte Zugriffssteuerung auf einem Knoten zu konfigurieren, musst du die folgenden Aktionen ausführen:

1.  Kopiere die JustEnoughAdministration-, Microsoft.SME.\*- und WindowsAdminCenter.Jea-Module in das PowerShell-Modulverzeichnis auf dem Zielcomputer. Normalerweise befindet sich dieses in `C:\Program Files\WindowsPowerShell\Modules`.
2.  Aktualisiere die Datei **InstallJeaFeature.ps1** so, dass sie deiner gewünschten Konfiguration für den RBAC-Endpunkt entspricht.
3.  Führe InstallJeaFeature.ps1 aus, um die DSC-Ressource zu kompilieren.
4.  Stelle die DSC-Konfiguration auf allen deinen Computern bereit, um die Konfiguration anzuwenden.

Im folgenden Abschnitt wird erläutert, wie dies mithilfe von PowerShell-Remoting durchzuführen ist.

#### <a name="deploy-on-multiple-machines"></a>Bereitstellen auf mehreren Computern

Um die heruntergeladene Konfiguration auf mehreren Computern bereitzustellen, musst du das Skript **InstallJeaFeatures.ps1** so aktualisieren, dass es die entsprechenden Sicherheitsgruppen für deine Umgebung enthält, die Dateien auf jeden deiner Computer kopieren und die Konfigurationsskripts aufrufen.
Hierfür kannst du deine bevorzugten Automatisierungstools verwenden. Dieser Artikel konzentriert sich jedoch auf einen reinen PowerShell-basierten Ansatz.

Standardmäßig erstellt das Konfigurationsskript lokale Sicherheitsgruppen auf dem Computer, um den Zugriff auf die einzelnen Rollen zu steuern.
Dies eignet sich für Arbeitsgruppen- und einer Domäne beigetretene Computer. Wenn du jedoch in einer reinen Domänenumgebung bereitstellst, solltest du eventuell jeder Rolle direkt eine Domänensicherheitsgruppe zuordnen.
Um die Konfiguration auf die Verwendung von Domänensicherheitsgruppen zu aktualisieren, öffne **InstallJeaFeatures.ps1**, und nimm die folgenden Änderungen vor:

1.  Entferne die 3 **Group**-Ressourcen aus der Datei:
    1.  "Group MS-Readers-Group"
    2.  "Group MS-Hyper-V-Administrators-Group"
    3.  "Group MS-Administrators-Group"
2.  Entferne die 3 Group-Ressourcen aus der JeaEndpoint-Eigenschaft **DependsOn**.
    1.  "[Group]MS-Readers-Group"
    2.  "[Group]MS-Hyper-V-Administrators-Group"
    3.  "[Group]MS-Administrators-Group"
3.  Ändere die Gruppennamen in der JeaEndpoint-Eigenschaft **RoleDefinitions** in deine gewünschten Sicherheitsgruppen. Wenn du z. B. über eine Sicherheitsgruppe *CONTOSO\MyTrustedAdmins* verfügst, der Zugriff auf die Rolle „Windows Admin Center-Administratoren“ zugewiesen werden soll, ändere `'$env:COMPUTERNAME\Windows Admin Center Administrators'` in `'CONTOSO\MyTrustedAdmins'`. Die drei Zeichen folgen, die du aktualisieren musst, lauten wie folgt:
    1.  '$env:COMPUTERNAME\Windows Admin Center Administrators'
    2.  '$env:COMPUTERNAME\Windows Admin Center Hyper-V Administrators'
    3.  '$env:COMPUTERNAME\Windows Admin Center Readers'

> [!NOTE]
> Achte darauf, dass du eindeutige Sicherheitsgruppen für jede Rolle verwendest. Die Konfiguration schlägt fehl, wenn dieselbe Sicherheitsgruppe mehreren Rollen zugewiesen wird.

Füge als Nächstes die folgenden PowerShell-Zeilen am Ende der Datei **InstallJeaFeatures.ps1** am Ende des Skripts hinzu:

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

Schließlich kannst du den Ordner, der die Module, die DSC-Ressource und die Konfiguration enthält, auf jeden Zielknoten kopieren und das Skript **InstallJeaFeature.ps1** ausführen.
Um dies remote von ihrer Administrator-Workstation aus auszuführen, kannst du die folgenden Befehle ausführen:

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
