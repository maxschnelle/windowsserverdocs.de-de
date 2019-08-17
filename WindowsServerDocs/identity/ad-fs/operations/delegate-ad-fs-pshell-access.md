---
title: Delegieren AD FS PowerShell-Commandlets Zugriff für Benutzer ohne Administratorrechte
description: In diesem Dokument wird beschrieben, wie Berechtigungen für AD FS PowerShell-cmdlts an nicht-Administratoren delegiert werden.
author: billmath
ms.author: billmath
manager: daveba
ms.reviewer: zhvolosh
ms.date: 01/31/2019
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 86bbb562e223fdf61dac3ce5646d97a57b2eba4c
ms.sourcegitcommit: 0467b8e69de66e3184a42440dd55cccca584ba95
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/16/2019
ms.locfileid: "69546305"
---
# <a name="delegate-ad-fs-powershell-commandlet-access-to-non-admin-users"></a>Delegieren AD FS PowerShell-Commandlets Zugriff für Benutzer ohne Administratorrechte 
Standardmäßig kann AD FS Verwaltung über PowerShell nur AD FS Administratoren durchgeführt werden. Für viele große Organisationen ist dies möglicherweise kein funktionierendes Betriebsmodell, wenn Sie mit anderen Personen wie einem Helpdeskpersonal beschäftigt sind.  

Mit Just Enough Administration (Jea) können Kunden jetzt bestimmte Cmdlets an verschiedene personalgruppen delegieren.  
Ein gutes Beispiel für diesen Anwendungsfall besteht darin, dass das Helpdesk-Personal AD FS Konto Sperr Statusabfragen und den Konto Sperrungs Status in AD FS zurücksetzen kann, sobald ein Benutzer eine Prüfung durchführen kann. In diesem Fall müssen folgende Cmdlets delegiert werden: 
- `Get-ADFSAccountActivity`
- `Set-ADFSAccountActivity` 
- `Reset-ADFSAccountLockout` 

Wir verwenden dieses Beispiel für den Rest dieses Dokuments. Dies kann jedoch angepasst werden, um auch die Delegierung zu ermöglichen, Eigenschaften Vertrauender Seiten festzulegen und diese an die Besitzer der Anwendung in der Organisation zu übergeben.  


##  <a name="create-the-required-groups-necessary-to-grant-users-permissions"></a>Erstellen der erforderlichen Gruppen zum Erteilen von Berechtigungen für Benutzer 
1. Erstellen Sie ein [Gruppen verwaltetes Dienst Konto](https://docs.microsoft.com/windows-server/security/group-managed-service-accounts/group-managed-service-accounts-overview). Das GMSA-Konto wird verwendet, um dem Jea-Benutzer den Zugriff auf Netzwerkressourcen als andere Computer oder Webdienste zu ermöglichen. Sie stellt eine Domänen Identität bereit, die für die Authentifizierung mit Ressourcen auf jedem Computer in der Domäne verwendet werden kann. Das GMSA-Konto erhält später in der Einrichtung die erforderlichen Administratorrechte. In diesem Beispiel nennen wir das Konto **gmsacontoso**. 
2. Erstellen Sie eine Active Directory Gruppe kann mit Benutzern aufgefüllt werden, denen die Rechte für die Delegierten Befehle erteilt werden müssen. In diesem Beispiel werden Helpdeskmitarbeiter Berechtigungen zum Lesen, aktualisieren und Zurücksetzen des AD FS-Sperr Zustands erteilt. Wir bezeichnen diese Gruppe im gesamten Beispiel als **jeaconto**. 

### <a name="install-the-gmsa-account-on-the-adfs-server"></a>Installieren Sie das GMSA-Konto auf dem ADFS-Server: 
Erstellen Sie ein Dienst Konto, das über Administratorrechte für die AD FS-Server verfügt. Dies kann auf dem Domänen Controller oder Remote ausgeführt werden, solange das AD RSAT-Paket installiert ist.  Das Dienst Konto muss in derselben Gesamtstruktur wie der AD FS-Server erstellt werden. Ändern Sie die Beispiel Werte in die Konfiguration der Farm. 

```powershell
 # This command should only be run if this is the first time gMSA accounts are enabled in the forest 
Add-KdsRootKey -EffectiveTime ((get-date).addhours(-10))  
 
# Run this on every node that you want to have JEA configured on  
$adfsServer = Get-ADComputer server01.contoso.com  
 
# Run targeted at domain controller  
$serviceaccount = New-ADServiceAccount gMSAcontoso -DNSHostName <FQDN of the domain containing the KDS key> - PrincipalsAllowedToRetrieveManagedPassword $adfsServer –passthru 
 
# Run this on every node 
Add-ADComputerServiceAccount -Identity server01.contoso.com -ServiceAccount $ServiceAccount 
```

Installieren Sie das GMSA-Konto auf dem ADFS-Server.  Diese muss auf jedem AD FS-Knoten in der Farm ausgeführt werden. 
 
```powershell
Install-ADServiceAccount gMSAcontoso 
```

### <a name="grant-the-gmsa-account-admin-rights"></a>Erteilen von Administratorrechten für das GMSA-Konto 
Wenn die Farm die delegierte Administration verwendet, erteilen Sie dem GMSA-Konto Administratorrechte, indem Sie Sie der vorhandenen Gruppe hinzufügen, die über delegierten Administrator Zugriff verfügt.  
 
Wenn die Farm keine delegierte Administration verwendet, erteilen Sie dem GMSA-Konto Administratorrechte, indem Sie Sie auf allen AD FS-Servern zur lokalen Administrator Gruppe machen. 
 
 
### <a name="create-the-jea-role-file"></a>Erstellen der Jea-Rollen Datei 
 
Erstellen Sie auf dem AD FS Server die Jea-Rolle in einer Editor-Datei. Anweisungen zum Erstellen der Rolle werden für [Jea-Rollen Funktionen](https://docs.microsoft.com/powershell/jea/role-capabilities)bereitgestellt. 
 
Die in diesem Beispiel Delegierten Cmdlets sind `Reset-AdfsAccountLockout, Get-ADFSAccountActivity, and Set-ADFSAccountActivity`. 

Beispiel für eine Jea-Rolle, die den Zugriff auf die Commandlets "Reset-adfsaccountlockout", "Get-adfsaccountactivity" und "Set-adfsaccountactivity" delegiert:

```powershell
@{
GUID = 'b35d3985-9063-4de5-81f8-241be1f56b52'
ModulesToImport = 'adfs'
VisibleCmdlets = 'Reset-AdfsAccountLockout', 'Get-ADFSAccountActivity', 'Set-ADFSAccountActivity'
}
```


### <a name="create-the-jea-session-configuration-file"></a>Erstellen der Jea-Sitzungs Konfigurationsdatei 
Befolgen Sie die Anweisungen zum Erstellen der [Jea-Sitzungs](https://docs.microsoft.com/powershell/jea/session-configurations) Konfigurationsdatei. Die Konfigurationsdatei bestimmt, wer den Jea-Endpunkt verwenden kann und auf welche Funktionen Sie zugreifen können. 

Auf Rollen Funktionen wird durch den flachen Namen (Dateiname ohne Erweiterung) der Rollen Funktions Datei verwiesen. Wenn mehrere Rollen Funktionen auf dem System mit dem gleichen flatname verfügbar sind, verwendet PowerShell die implizite Such Reihenfolge, um die effektive Rollen Funktions Datei auszuwählen. Er gewährt keinen Zugriff auf alle Rollen Funktions Dateien mit demselben Namen. 

Um eine Rollen Funktions Datei mit einem Pfad anzugeben, verwenden Sie `RoleCapabilityFiles` das-Argument. Für einen Unterordner sucht Jea nach gültigen PowerShell-Modulen, die einen `RoleCapabilities` Unterordner enthalten, in `RoleCapabilityFiles` dem das Argument in geändert werden `RoleCapabilities`sollte. 

Beispiel für eine Sitzungs Konfigurationsdatei: 

```powershell
@{
SchemaVersion = '2.0.0.0'
GUID = '54c8d41b-6425-46ac-a2eb-8c0184d9c6e6'
SessionType = 'RestrictedRemoteServer'
GroupManagedServiceAccount =  'CONTOSO\gMSAcontoso'
RoleDefinitions = @{ JEAcontoso = @{ RoleCapabilityFiles = 'C:\Program Files\WindowsPowershell\Modules\AccountActivityJEA\RoleCapabilities\JEAAccountActivityResetRole.psrc' } }
}
```

Speichern Sie die Sitzungs Konfigurationsdatei. 
 
Es wird dringend empfohlen, die [Sitzungs Konfigurationsdatei zu testen](https://docs.microsoft.com/powershell/module/Microsoft.PowerShell.Core/Test-PSSessionConfigurationFile?view=powershell-5.1) , wenn Sie die PSSC-Datei manuell mithilfe eines Text-Editors bearbeitet haben, um sicherzustellen, dass die Syntax korrekt ist. Wenn eine Sitzungs Konfigurationsdatei den Test nicht bestanden hat, wird Sie nicht erfolgreich auf dem System registriert.  
 
### <a name="install-the-jea-session-configuration-on-the-ad-fs-server"></a>Installieren der Jea-Sitzungs Konfiguration auf dem AD FS Server 

Installieren der Jea-Sitzungs Konfiguration auf dem AD FS Server 
 
```powershell
Register-PSSessionConfiguration -Path .\JEASessionConfig.pssc -name "AccountActivityAdministration" -force
``` 
## <a name="operational-instructions"></a>Betriebsanweisungen 
Nach der Einrichtung kann die Jea-Protokollierung und-Überwachung verwendet werden, um zu bestimmen, ob die richtigen Benutzer Zugriff auf den Jea-Endpunkt haben. 

So verwenden Sie die Delegierten Befehle: 

```powershell
Enter-pssession -ComputerName server01.contoso.com -ConfigurationName "AccountActivityAdministration" -Credential <User Using JEA> 
Get-AdfsAccountActivity <User> 


```
