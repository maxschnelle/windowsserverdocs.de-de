---
title: Problembehandlung bei allgemeinen Problemen
description: Dieses Thema ist Teil des Handbuchs bereitstellen mehrere RAS-Server in einer Bereitstellung für mehrere Standorte in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 354ae5e3-bae1-44f9-afd7-7eaba70f2346
ms.author: pashort
author: shortpatti
ms.openlocfilehash: fe1fdc4fb5aff2e34555b08d3b2c4347e643085e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59831081"
---
# <a name="troubleshooting-general-issues"></a>Problembehandlung bei allgemeinen Problemen

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Dieses Thema enthält Informationen zur Problembehandlung für allgemeine Probleme im Zusammenhang mit Remotezugriff.  
  
## <a name="gpo-retrieval-error"></a>Fehler beim Abrufen des Gruppenrichtlinienobjekts  
**Fehler**. DirectAccess-Server-GPO-Einstellungen können nicht abgerufen werden. Stellen Sie sicher, dass Sie über Bearbeitungsberechtigungen für das Gruppenrichtlinienobjekt verfügen.  
  
Die Remotezugriffs-Verwaltungskonsole ist nach dem Empfang dieser Fehler nicht mehr reagiert.  
  
**Ursache**  
  
Das Gruppenrichtlinienobjekt von einem der Einstiegspunkte in der Bereitstellung von DirectAccess kann nicht zugegriffen werden können, und daher die Konfiguration nicht geladen werden.  
  
**Lösung**  
  
Stellen Sie sicher, dass für jeden Einstiegspunkt in der Bereitstellung ein entsprechenden Gruppenrichtlinienobjekts auf einen Domänencontroller verfügt, und stellen Sie sicher, dass der angemeldete Benutzer über Lese- und Schreibberechtigungen für alle GPOs, die in der remotezugriffsbereitstellung konfiguriert.  
  
Dieses Problem zu umgehen verwenden Sie die Konfigurations-Cmdlets, statt mithilfe der Remotezugriffs-Verwaltungskonsole; Verwenden Sie beispielsweise `Get-RemoteAccess` und `Get-DAEntryPoint`.  
  
> [!NOTE]  
> Dieses Szenario tritt nicht auf, wenn das Server-GPO des aktuellen Einstiegspunkts nicht verfügbar ist.  
  
Können Sie die `Get-DAEntryPointDC` Cmdlet, um alle Domänencontroller aufgelistet, die der Server-GPOs zu speichern und `Get-DAMultiSite` in Verbindung mit `Get-RemoteAccess` um eine vollständige Liste der Server-GPOs in der Bereitstellung abzurufen. Zum Beispiel:  
  
```  
$ServerGpos = Get-DAEntryPointDC | ForEach-Object {   
   @{   
       GpoName = (Get-RemoteAccess -EntryPoint $_.EntryPointName).ServerGpoName;   
        DC = $_.DomainControllerName }   
}  
$ServerGpos | ForEach-Object { $GpoName = $_['GpoName'] ; $DC = $_['DC'] ; Write-Host "Server GPO '$GpoName' on DC '$DC'" }  
```  
  
## <a name="windows-7-to-windows-8-or-10-client-upgrade"></a>Windows 7 auf Windows 8 oder 10 clientupgrade  
**Symptom**. Nachdem ein Client für Windows 7 auf Windows 10 oder Windows 8 in einer Bereitstellung für mehrere Standorte aktualisiert wurde, wird die DirectAccess-Verbindung nicht in der Liste der Netzwerke angezeigt.  
  
**Ursache**  
  
Die Windows 7-Gruppenrichtlinienobjekte in einer Bereitstellung für mehrere Standorte enthalten nicht die Windows 8 Netzwerkkonnektivitäts-Assistent-Konfiguration.  
  
 Windows 7-Clients sollten DirectAccess Connectivity Assistant verwenden, um ihren DirectAccess-Konnektivitäts-Status erfordert eine separate manuelle Konfiguration in der Windows 7-Client-Gruppenrichtlinienobjekte zu überwachen. Wenn Windows 7-Clients auf Windows 10 oder Windows 8 aktualisiert werden, funktioniert den Netzwerkkonnektivitäts-Assistent nicht, wenn immer noch das Windows 7-Client-Gruppenrichtlinienobjekt angewendet wird.  
  
**Lösung**  
  
Wenn DirectAccess Connectivity Assistant Einstellungen in den Windows 7-Gruppenrichtlinienobjekten konfiguriert sind, können Sie dieses Problem beheben, vor dem Upgrade von Clientcomputern durch Ändern der Windows 7-GPOs mit den folgenden PowerShell-Cmdlets:  
  
```  
Set-GPRegistryValue -Name <Windows7GpoName> -Domain <DomainName> -Key "HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\NetworkConnectivityAssistant" -ValueName "TemporaryValue" -Type Dword -Value 1  
Remove-GPRegistryValue -Name <Windows7GpoName> -Domain <DomainName> -Key "HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\NetworkConnectivityAssistant"  
```  
  
Wenn ein Client bereits aktualisiert wurde, oder der DCA ist nicht konfiguriert, verschieben Sie den Clientcomputer, die Sicherheitsgruppe "Windows 10 oder Windows 8".  
  
## <a name="general-cmdlet-errors"></a>Cmdlet für allgemeine Fehler  
  
-   **Problem 1**  
  
    **Fehler**. Domänencontroller < Domänencontroller > kann nicht für < Servername oder Einstiegspunktname > erreicht werden.  
  
    **Ursache**  
  
    Um die Einheitlichkeit der Konfiguration in einer Bereitstellung für mehrere Standorte zu wahren, müssen Sie sicherstellen, dass jedes GPO von einem einzigen Domänencontroller verwaltet wird. Wenn der Domänencontroller, der einen Einstiegspunkt-Server-Gruppenrichtlinienobjekt verwaltet nicht verfügbar ist, können nicht RAS-Konfigurationseinstellungen gelesen oder geändert werden.  
  
    **Lösung**  
  
    Führen Sie das Verfahren "So ändern den Domänencontroller, die Server-GPOs verwaltet", die in beschriebenen [2.4. Konfigurieren der Gruppenrichtlinienobjekte](assetId:///b1960686-a81e-4f48-83f1-cc4ea484df43#ConfigGPOs).  
  
-   **Problem 2**  
  
    **Fehler**. Der primäre Domänencontroller in die Domäne < Domänenname > kann nicht erreicht werden.  
  
    **Ursache**  
  
    Um die Einheitlichkeit der Konfiguration in einer Bereitstellung für mehrere Standorte zu wahren, müssen Sie sicherstellen, dass jedes GPO von einem einzigen Domänencontroller verwaltet wird. Client-GPOs werden auf dem primären Domänencontroller verwaltet. Wenn der primäre Domänencontroller nicht verfügbar ist, können die RAS-Konfigurationseinstellungen nicht gelesen oder geändert werden.  
  
    **Lösung**  
  
    Folgen Sie das Verfahren "So übertragen die PDC-Emulatorrolle" in [2.4. Konfigurieren der Gruppenrichtlinienobjekte](assetId:///b1960686-a81e-4f48-83f1-cc4ea484df43#ConfigGPOs).  
  


