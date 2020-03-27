---
title: Problembehandlung bei allgemeinen Problemen
description: Dieses Thema ist Teil des Handbuchs Bereitstellen mehrerer Remote Zugriffs Server in einer Bereitstellung mit mehreren Standorten in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 354ae5e3-bae1-44f9-afd7-7eaba70f2346
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 513bcae13d4a8f3ab935d2bda77745baa1788fa9
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80313796"
---
# <a name="troubleshooting-general-issues"></a>Problembehandlung bei allgemeinen Problemen

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

Dieses Thema enthält Informationen zur Problembehandlung für allgemeine Probleme im Zusammenhang mit dem Remote Zugriff.  
  
## <a name="gpo-retrieval-error"></a>GPO-Abruf Fehler  
Der **Fehler wurde empfangen**. Die GPO-Einstellungen des DirectAccess-Servers können nicht abgerufen werden. Stellen Sie sicher, dass Sie über Bearbeitungs Berechtigungen für das GPO verfügen.  
  
Die Remote Zugriffs-Verwaltungskonsole reagiert nach dem Empfang dieses Fehlers nicht mehr.  
  
**Ursache**  
  
DirectAccess kann nicht auf das Gruppenrichtlinien Objekt eines der Einstiegspunkte in der Bereitstellung zugreifen. Daher kann die Konfiguration nicht geladen werden.  
  
**Lösung**  
  
Stellen Sie sicher, dass jeder Einstiegspunkt in der Bereitstellung über ein entsprechendes GPO auf seinem Domänen Controller verfügt, und überprüfen Sie, ob der angemeldete Benutzer über Lese-und Schreibberechtigungen für alle in der Remote Zugriffs Bereitstellung konfigurierten GPOs verfügt.  
  
Um dieses Problem zu umgehen, verwenden Sie die Configuration-Cmdlets anstelle der Remote Zugriffs-Verwaltungskonsole. beispielsweise mithilfe von `Get-RemoteAccess` und `Get-DAEntryPoint`.  
  
> [!NOTE]  
> Dieses Szenario tritt nicht ein, wenn das Server-GPO des aktuellen Einstiegs Punkts nicht verfügbar ist.  
  
Sie können das Cmdlet "`Get-DAEntryPointDC`" verwenden, um alle Domänen Controller aufzulisten, die Server-Gruppenrichtlinien Objekte speichern, und `Get-DAMultiSite` in Verbindung mit `Get-RemoteAccess`, um eine vollständige Liste der Server-Gruppenrichtlinien Objekte in der Bereitstellung abzurufen. Beispiel:  
  
```  
$ServerGpos = Get-DAEntryPointDC | ForEach-Object {   
   @{   
       GpoName = (Get-RemoteAccess -EntryPoint $_.EntryPointName).ServerGpoName;   
        DC = $_.DomainControllerName }   
}  
$ServerGpos | ForEach-Object { $GpoName = $_['GpoName'] ; $DC = $_['DC'] ; Write-Host "Server GPO '$GpoName' on DC '$DC'" }  
```  
  
## <a name="windows-7-to-windows-8-or-10-client-upgrade"></a>Client Upgrade für Windows 7 zu Windows 8 oder 10  
**Symptom**. Nachdem ein Windows 7-Client in einer Bereitstellung mit mehreren Standorten auf Windows 10 oder Windows 8 aktualisiert wurde, ist die DirectAccess-Verbindung in der Liste der Netzwerke nicht sichtbar.  
  
**Ursache**  
  
Die Windows 7-Gruppenrichtlinien Objekte in einer Bereitstellung mit mehreren Standorten enthalten nicht die Konfiguration des Windows 8-netzwerkkonnektivitätsassistenten  
  
 Bei Windows 7-Clients sollte der DirectAccess-Konnektivitätsassistent zum Überwachen Ihres DirectAccess-Verbindungsstatus verwendet werden, der eine separate manuelle Konfiguration in den Windows 7-Client-Gruppenrichtlinien Objekten Wenn Windows 7-Clients auf Windows 10 oder Windows 8 aktualisiert werden, funktioniert der netzwerkkonnektivitätsassistent nicht, wenn das Windows 7-Client-Gruppenrichtlinien Objekt weiterhin angewendet wird.  
  
**Lösung**  
  
Wenn die Einstellungen für den DirectAccess-konnektivitätsassistant in den Gruppenrichtlinien Objekten von Windows 7 konfiguriert sind, können Sie dieses Problem beheben, bevor Sie die Windows 7-Gruppenrichtlinien Objekte mithilfe der folgenden PowerShell-Cmdlets ändern:  
  
```  
Set-GPRegistryValue -Name <Windows7GpoName> -Domain <DomainName> -Key "HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\NetworkConnectivityAssistant" -ValueName "TemporaryValue" -Type Dword -Value 1  
Remove-GPRegistryValue -Name <Windows7GpoName> -Domain <DomainName> -Key "HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\NetworkConnectivityAssistant"  
```  
  
Wenn ein Client bereits aktualisiert wurde oder die DCA nicht konfiguriert ist, verschieben Sie den Client Computer in die Sicherheitsgruppe Windows 10 oder Windows 8.  
  
## <a name="general-cmdlet-errors"></a>Allgemeine Cmdlet-Fehler  
  
-   **Problem 1**  
  
    Der **Fehler wurde empfangen**. Domänen Controller < domain_controller > für < server_name oder entry_point_name > nicht erreicht werden.  
  
    **Ursache**  
  
    Um die Einheitlichkeit der Konfiguration in einer Bereitstellung für mehrere Standorte zu wahren, müssen Sie sicherstellen, dass jedes GPO von einem einzigen Domänencontroller verwaltet wird. Wenn der Domänen Controller, der das Server-Gruppenrichtlinien Objekt eines Einstiegs Punkts verwaltet, nicht verfügbar ist, können die RAS-Konfigurationseinstellungen nicht gelesen oder geändert werden.  
  
    **Lösung**  
  
    Befolgen Sie das Verfahren "so ändern Sie den Domänen Controller, der Server-Gruppenrichtlinien Objekte verwaltet" in [2,4. Konfigurieren Sie GPOs](assetId:///b1960686-a81e-4f48-83f1-cc4ea484df43#ConfigGPOs).  
  
-   **Problem 2**  
  
    Der **Fehler wurde empfangen**. Der primäre Domänen Controller in der Domänen < domain_name > kann nicht erreicht werden.  
  
    **Ursache**  
  
    Um die Einheitlichkeit der Konfiguration in einer Bereitstellung für mehrere Standorte zu wahren, müssen Sie sicherstellen, dass jedes GPO von einem einzigen Domänencontroller verwaltet wird. Client-GPOs werden auf dem primären Domänencontroller verwaltet. Wenn der primäre Domänencontroller nicht verfügbar ist, können die RAS-Konfigurationseinstellungen nicht gelesen oder geändert werden.  
  
    **Lösung**  
  
    Befolgen Sie das Verfahren "So übertragen Sie die PDC-Emulatorrolle" in [2,4. Konfigurieren Sie GPOs](assetId:///b1960686-a81e-4f48-83f1-cc4ea484df43#ConfigGPOs).  
  


