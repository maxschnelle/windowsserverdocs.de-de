---
title: Delegieren von AD FS Powershell-Cmdlet auf Benutzer ohne Administratorrechte
description: Dieses Dokument Descirbes Vorgehensweise beim Delegieren von Berechtigungen für nicht-Administratoren für AD FS-PowerShell-Dienstes.
author: billmath
ms.author: billmath
manager: daveba
ms.reviewer: zhvolosh
ms.date: 01/31/2019
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 265d22b045011e34192e56bdb970955b601cda56
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59883561"
---
# <a name="delegate-ad-fs-powershell-commandlet-access-to-non-admin-users"></a>Delegieren von AD FS Powershell-Cmdlet auf Benutzer ohne Administratorrechte 
Standardmäßig kann AD FS-Verwaltung über PowerShell nur von AD FS-Administratoren erreicht werden. Für viele große Organisationen kann dies keine geeignete Betriebsmodell beim Umgang mit anderen Rollen wie z. B. ein Helpdeskmitarbeiter.  

Mit Just Enough Administration (JEA), können Kunden jetzt spezifische Cmdlets für andere Mitarbeiter Gruppen delegieren.  
Ein gutes Beispiel in diesem Fall lässt das Helpdeskpersonal Abfrage AD FS Lockout Status des Datenquellenkontos und Konto-Sperrzustands in AD FS zurückgesetzt, sobald ein Benutzer überprüft wurde. In diesem Fall sind die Cmdlets, die delegiert werden müssten: 
- `Get-ADFSAccountActivity`
- `Set-ADFSAccountActivity` 
- `Reset-ADFSAccountLockout` 

Wir verwenden in diesem Beispiel wird im weiteren Verlauf dieses Dokuments. Allerdings kann eine anpassen, diese Option, um auch die Delegierung zu legen Sie Eigenschaften der vertrauenden Seiten, und übergeben dies aus an die Anwendungsbesitzer innerhalb der Organisation ermöglichen.  


##  <a name="create-the-required-groups-necessary-to-grant-users-permissions"></a>Erstellen Sie die erforderlichen Gruppen erforderlich, um Benutzerberechtigungen gewähren 
1. Erstellen Sie eine [Gruppenverwaltetes Dienstkonto](https://docs.microsoft.com/windows-server/security/group-managed-service-accounts/group-managed-service-accounts-overview). Das gMSA-Konto wird verwendet, um die JEA-Benutzer Zugriff auf Netzwerkressourcen als der andere Computer oder die Webdienste zu ermöglichen. Es bietet eine Domänenidentität, die zum Authentifizieren von Ressourcen auf einem beliebigen Computer innerhalb der Domäne verwendet werden kann. Das gMSA-Konto wird später im Setup die erforderlichen Administratorrechte gewährt werden. In diesem Beispiel rufen wir das Konto **gMSAContoso**. 
2. Erstellen einer Active Directory-Gruppe mit Benutzern, die die Rechte für die delegierte Befehle erteilt werden müssen aufgefüllt werden kann. In diesem Beispiel werden Helpdeskpersonal gewährt Berechtigungen zum Lesen, aktualisieren und den Status der AD FS-Sperre zurücksetzen. Wir bezeichnen diese Gruppe in der gesamten das Beispiel als **JEAContoso**. 

### <a name="install-the-gmsa-account-on-the-adfs-server"></a>Installieren Sie das gMSA-Konto auf dem AD FS-Server: 
Erstellen Sie ein Dienstkonto, das über Administratorrechte für AD FS-Server verfügt. Dies kann erfolgen auf dem Domänencontroller oder von einem Remotestandort, so lange wie das Active Directory-RSAT-Paket installiert wird.  Das Dienstkonto muss in derselben Gesamtstruktur wie der AD FS-Server erstellt werden. Ändern Sie die Beispielwerte an der Konfiguration der Farm. 

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

Installieren Sie das gMSA-Konto auf dem AD FS-Server.  Dies muss auf jedem AD FS-Knoten in der Farm ausgeführt werden. 
 
```powershell
Install-ADServiceAccount gMSAcontoso 
```

### <a name="grant-the-gmsa-account-admin-rights"></a>Das gMSA-Konto über Administratorrechte zu gewähren 
Wenn die Farm delegierte Verwaltung verwendet wird, gewähren Sie gMSA Konto über Administratorrechte, indem Sie es an die vorhandene Gruppe, die administrativen Zugriff delegiert hat.  
 
Wenn die Farm nicht delegierte Verwaltung verwendet wird, gewähren Sie gMSA Konto über Administratorrechte und es der lokalen Administratorgruppe auf allen AD FS-Server mit. 
 
 
### <a name="create-the-jea-role-file"></a>Erstellen Sie die Datei der JEA-Rolle 
 
Erstellen Sie die JEA-Rolle in eine Editor-Datei an. Anweisungen zum Erstellen der Rolle wird bereitgestellt, auf [JEA-rollenfunktionen](https://docs.microsoft.com/powershell/jea/role-capabilities). 
 
Die Cmdlets, die in diesem Beispiel delegiert werden `Reset-AdfsAccountLockout, Get-ADFSAccountActivity, and Set-ADFSAccountActivity`. 

Beispiel-JEA-Rolle delegieren des Zugriffs von "Get-ADFSAccountActivity", "Reset-ADFSAccountLockout" und "Set-ADFSAccountActivity"-Cmdlets:

```powershell
@{
GUID = 'b35d3985-9063-4de5-81f8-241be1f56b52'
ModulesToImport = 'adfs'
VisibleCmdlets = 'Reset-AdfsAccountLockout', 'Get-ADFSAccountActivity', 'Set-ADFSAccountActivity'
}
```


### <a name="create-the-jea-session-configuration-file"></a>Erstellen Sie die Konfigurationsdatei für JEA-Sitzung 
Führen Sie die Anweisungen zum Erstellen der [JEA-Sitzungskonfiguration](https://docs.microsoft.com/powershell/jea/session-configurations) Datei. Die Konfigurationsdatei bestimmt, die auf den JEA-Endpunkt verwenden können und welche Funktionen sie Zugriff haben. 

Rollenfunktionen werden durch den flachen Namen (Dateiname ohne Erweiterung), der die rollenfunktionsdatei auf die verwiesen wird. Wenn mehrere rollenfunktionen auf dem System mit dem gleichen flachen Namen verfügbar sind, verwendet PowerShell die implizite Suchreihenfolge, um die zutreffende rollenfunktionsdatei auszuwählen. Es wird kein Zugriff auf alle rollenfunktionsdateien mit dem gleichen Namen ermöglicht. 

Verwenden Sie zum Angeben einer Rollenfunktionsdatei mit einem Pfad der `RoleCapabilityFiles` Argument. Für einen Unterordner, JEA, sucht Sie nach gültigen Powershell-Modulen, die enthalten eine `RoleCapabilities` Unterordner, in denen die `RoleCapabilityFiles` Argument sollte geändert werden `RoleCapabilities`. 

Beispielkonfigurationsdatei Sitzung: 

```powershell
@{
SchemaVersion = '2.0.0.0'
GUID = '54c8d41b-6425-46ac-a2eb-8c0184d9c6e6'
SessionType = 'RestrictedRemoteServer'
GroupManagedServiceAccount =  'CONTOSO\gMSAcontoso'
RoleDefinitions = @{ JEAcontoso = @{ RoleCapabilityFiles = 'C:\Program Files\WindowsPowershell\Modules\AccountActivityJEA\RoleCapabilities\JEAAccountActivityResetRole.psrc' } }
}
```

Speichern Sie die Sitzungskonfigurationsdatei. 
 
Es wird dringend empfohlen, [testen Sie die Sitzungskonfigurationsdatei](https://docs.microsoft.com/powershell/module/Microsoft.PowerShell.Core/Test-PSSessionConfigurationFile?view=powershell-5.1) , wenn Sie die Pssc-Datei manuell bearbeitet haben, mit einem Text-Editor, um sicherzustellen, dass die Syntax korrekt ist. Wenn eine Sitzungskonfigurationsdatei den Test nicht bestanden, ist es nicht erfolgreich auf dem System registriert.  
 
### <a name="install-the-jea-session-configuration-on-the-ad-fs-server"></a>Installieren von JEA-Sitzungskonfiguration auf dem AD FS-Server 

Installieren von JEA-Sitzungskonfiguration auf dem AD FS-server 
 
```powershell
Register-PSSessionConfiguration -Path .\JEASessionConfig.pssc -name "AccountActivityAdministration" -force
``` 
## <a name="operational-instructions"></a>Operational-Anweisungen 
Nach der Einrichtung JEA, Protokollierung und Überwachung kann verwendet werden, um festzustellen, ob die richtigen Benutzer haben Zugriff auf den JEA-Endpunkt. 

So verwenden Sie die delegierte Befehle: 

```powershell
Enter-pssession -ComputerName server01.contoso.com -ConfigurationName "AccountActivityAdministration" -Credential <User Using JEA> 
Get-AdfsAccountActivity <User> 
```
