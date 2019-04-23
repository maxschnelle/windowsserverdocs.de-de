---
title: Problembehandlung von DirectAccess
description: Dieses Thema enthält Informationen zur Problembehandlung von DirectAccess-Bereitstellungen in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 61040e19-5960-4eb0-b612-d710627988f7
ms.author: pashort
author: shortpatti
ms.openlocfilehash: ec725eea286c359461b0f4a7b8763b97464e7067
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59867091"
---
# <a name="troubleshooting-directaccess"></a>Problembehandlung von DirectAccess

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Um den Remotezugriff (DirectAccess) Probleme zu beheben, gehen Sie wie folgt vor.  
  
|||  
|-|-|  
|**Problem:**|**Lösung**|  
|Remotezugriffs-Verwaltungskonsole wird kann nicht die DirectAccess-Konfiguration angezeigt|**Zum Wiederherstellen der fehlenden Konfigurationsinformationen**<br />– Wenn Sie eine Bereitstellung für mehrere Standorte behandeln möchten, stellen Sie sicher, dass der Domänencontroller am nächsten zum Einstiegspunkt verfügbar ist.<br />– Verwenden Sie die **Get-DAEntrypointDC** -Cmdlet zum Abrufen des Namens des Domänencontrollers, den Einstiegspunkt des am nächsten liegt. Wenn der Domänencontroller nicht ausgeführt wird, verwenden Sie die **Set-DAEntryPointDC** Cmdlet, um auf einen anderen Domänencontroller verweisen.<br />– Führen Sie **Gpresult** eine Eingabeaufforderung mit erhöhten Rechten auf dem Server, um sicherzustellen, dass der Server läuft die DirectAccess-Gruppenrichtlinienobjekte.<br />-Aktivieren der Protokollierung für Benutzer-Benutzeroberfläche (UI).<br />-Verwenden Sie den folgenden Befehl aus, um Windows PowerShell-Protokollierungen zu starten:<pre>logman create trace ETWTrace -ow -o c:\ETWTrace.etl -p {AAD4C46D-56DE-4F98-BDA2-B5EAEBDD2B04} 0xffffffffffffffff 0xff -nb 16 16 -bs 1024 -mode 0x2 -max 2048 -ets <br />logman update trace ETWTrace -p {62DFF3DA-7513-4FCA-BC73-25B111FBB1DB} 0xffffffffffffffff 0xff -ets</pre><repro>– Schließen Sie und öffnen Sie die Benutzeroberfläche.<br />-Windows Powershell-Protokollierung aktiviert werden. Die Event Trace Log-Dateien erfasst werden. Darüber hinaus alle Protokolle aus der **%windir%/tracing** Ordner.|  
|Anwenden der DirectAccess-Konfigurations schlägt fehl|**Um die DirectAccess-Konfiguration zu aktualisieren.**<br />– Wenn Sie eine Bereitstellung für mehrere Standorte behandeln möchten, stellen Sie sicher, dass der Domänencontroller am nächsten zum Einstiegspunkt verfügbar ist.<br />– Verwenden Sie die **Get-DAEntrypointDC** -Cmdlet zum Abrufen des Namens des Domänencontrollers, den Einstiegspunkt des am nächsten liegt. Wenn der Domänencontroller nicht ausgeführt wird, verwenden Sie die **Set-DAEntryPointDC** Cmdlet, um auf einen anderen Domänencontroller verweisen.<br />-Verwenden Sie den folgenden Befehl aus, um Windows Powershell-Protokollierungen zu starten:<br /><pre>logman create trace ETWTrace -ow -o c:\ETWTrace.etl -p {AAD4C46D-56DE-4F98-BDA2-B5EAEBDD2B04} 0xffffffffffffffff 0xff -nb 16 16 -bs 1024 -mode 0x2 -max 2048 -ets<br />logman update trace ETWTrace -p {62DFF3DA-7513-4FCA-BC73-25B111FBB1DB} 0xffffffffffffffff 0xff -ets</pre>    <repro><br />– Klicken Sie auf **anwenden**.<br />: Nachdem der Fehler auftritt, deaktivieren Sie Windows Powershell-Protokollierungen und erfassen Sie das Ereignisprotokoll für die Ablaufverfolgung zu.|  
|DirectAccess konfiguriert ist, aber Clients sind nicht mit internen Ressourcen herstellen|**Beheben von Verbindungsproblemen von Clients**<br />– Klicken Sie auf die **Vorgangsstatus** Registerkarte in der Remotezugriffs-Verwaltungskonsole, und stellen Sie sicher, dass alle Komponenten ein grünes Symbol angezeigt. Wenn dies nicht der Fall ist, überprüfen Sie die Fehlerdetails, und führen Sie die Schritten zur Behebung.<br />-Führen Sie den RAS-Server Best Practices Analyzer (BPA). Wenn Warnungen oder Fehler vorhanden sind, führen Sie die Schritte zum Beheben des Problems aus.|  
|Auftreten von Problemen im Zusammenhang mit einer Konfiguration für mehrere Standorte (z. B. eine für mehrere Standorte, Hinzufügen von Einstiegspunkten aktivieren oder Einrichten des Domänencontrollers als Einstiegspunkt)|Führen Sie die Schritte in [Problembehandlung bei einer Bereitstellung für mehrere Standorte](https://technet.microsoft.com/library/jj554657(v=ws.11).aspx).|  
|Konfiguration der statuskachel auf dem Dashboard zeigt eine Warnung oder Fehler|Führen Sie die Schritte in [Überwachen des konfigurationsverteilungsstatus des RAS-Servers](https://technet.microsoft.com/library/jj574221(v=ws.11).aspx).|  
|Unabhängig vom Probleme beim Konfigurieren des Lastenausgleichs (z. B. die Konfiguration schlägt fehl, wenn Sie den Lastenausgleich oder Probleme vorliegen, wenn Sie beim Hinzufügen oder Entfernen von Servern aus einem Cluster)|Wenn Sie aktivieren waren, den Lastenausgleich oder Hinzufügen eines Knotens und die Konfiguration aktualisiert wird, wenn auf Sie geklickt **übernehmen**, aber das Cluster nicht ordnungsgemäß auf dem Server, führen Sie den folgenden Befehl zu erstellen: **cmd.exe/c "Reg add HKLM\ SYSTEM\CurrentControlSet\Services\RaMgmtSvc\Parameters/f/v DebugFlag/t REG_DWORD/d "" 0xffffffff"" "** zum Sammeln von des Benutzers Schnittstelle, die auf dem neuen Server protokolliert.|  
|Vorgangsstatus zeigt eine Fehlermeldung oder Warnung nach der folgenden Schritte aus, um das Problem zu beheben|Wenn der Status der Vorgänge (z. B. Fehler auch nach dem Sie sie beheben) falsche Informationen angezeigt werden:<br /><br />-   Enable the registry key **cmd.exe /c "reg add HKLM\SYSTEM\CurrentControlSet\Services\RaMgmtSvc\Parameters /f /v EnableTracing /t REG_DWORD /d ""5"" "**.<br />– Aktualisieren des Betriebsstatus und Sammeln der Protokolle von **%windir%/tracing**.|  
|Melden Windows 8 und höher DirectAccess-Clientcomputer "No Internet" als Status für die DirectAccess-Verbindung und Network Connectivity Status Indicator (NCSI) meldet eingeschränkten Konnektivität.|Dies kann auftreten, wenn die Tunnelerzwingung aktiviert ist, in der DirectAccess-Konfiguration und aus diesem Grund nur IPHTTPS verwendet wird. Um dieses Problem zu beheben, können Sie erstellen und konfigurieren einen Proxyserver. NCSI verwendet dann den Proxyserver auf Internet-Verbindungen überprüft werden soll. Es wird empfohlen, dass Sie einen statischen Proxy, der Gruppenrichtlinien-Verwaltungskonsole (Name Resolution Richtlinie Table, NRPT) hinzufügen, indem mithilfe des folgenden Verfahrens.<br /><br />Bevor Sie die Befehle in diesem Verfahren ausführen, stellen Sie sicher, dass Sie alle Domänennamen, Computernamen und andere Windows PowerShell-Befehlsvariablen durch Werte ersetzen, die für Ihre Bereitstellung geeignet sind.<br /><br />**Konfigurieren Sie einen statischen Proxy für eine NRPT-Regel**<br />1.  Anzeigen der "." NRPT-Regel: `Get-DnsClientNrptRule -GpoName "corp.example.com\DirectAccess Client Settings" -Server <DomainControllerNetBIOSName>`<br />2.  Notieren Sie den Namen (GUID), der die "." NRPT-Regel. Der Name (GUID) sollten mit beginnen **DA-{.}**<br />3.  Legen Sie den Proxy für die "." NRPT-Regel zum **proxy.corp.example.com:8080**:  `Set-DnsClientNrptRule -Name "DA-{..}" -Server <DomainControllerNetBIOSName> -GPOName "corp.example.com\DirectAccess Client Settings" -DAProxyServerName "proxy.corp.example.com:8080" -DAProxyType "UseProxyName"`<br />4.  Anzeigen der "." NRPT-Regel erneut, indem Sie Ausführung `Get-DnsClientNrptRule`, und überprüfen Sie, ob **ProxyFQDN:port** ist jetzt ordnungsgemäß konfiguriert.<br />5.  Aktualisieren der Gruppenrichtlinie durch Ausführen `gpupdate /force` auf einem DirectAccess-Client, wenn der Client intern verbunden ist, klicken Sie dann zeigt die NRPT mit `Get-DnsClientNrptPolicy` und überprüfen Sie, ob die "." Regel zeigt **ProxyFQDN:port**.|  
  


