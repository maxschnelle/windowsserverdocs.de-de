---
title: Erweiterte Problembehandlung für Server Message Block (SMB)
description: In werden die erweiterten SMB-Methoden (Server Message Block) eingeführt.
author: Deland-Han
manager: dcscontentpm
audience: ITPro
ms.topic: article
ms.author: delhan
ms.date: 12/25/2019
ms.openlocfilehash: 88f707cc02514dc13c212c6462c47e4d3a94b5f5
ms.sourcegitcommit: 8cf04db0bc44fd98f4321dca334e38c6573fae6c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/03/2020
ms.locfileid: "75654581"
---
# <a name="advanced-troubleshooting-server-message-block-smb"></a>Erweiterte Problembehandlung für Server Message Block (SMB)

Server Message Block (SMB) ist ein Netzwerk Transportprotokoll für Dateisystem Vorgänge, mit denen ein Client auf Ressourcen auf einem Server zugreifen kann. Der Hauptzweck des SMB-Protokolls besteht darin, den Remote Dateisystem Zugriff zwischen zwei Systemen über TCP/IP zu aktivieren.

Die SMB-Problembehandlung kann sehr komplex sein. In diesem Artikel handelt es sich nicht um eine vollständige Anleitung zur Problembehandlung, sondern um die Grundlagen der effektiven Problembehandlung von SMB.

## <a name="tools-and-data-collection"></a>Tools und Datensammlung

Ein wichtiger Aspekt der Quality-SMB-Problembehandlung ist die Kommunikation der richtigen Terminologie. Daher wird in diesem Artikel grundlegende SMB-Terminologie eingeführt, um die Genauigkeit der Datenerfassung und-Analyse sicherzustellen.

> [!Note]
> Der *SMB-Server (SRV)* bezieht sich auf das System, das als Host für das Dateisystem dient, das auch als Datei Server bezeichnet wird. *Der SMB-Client (CLI)* bezieht sich auf das System, das versucht, auf das Dateisystem zuzugreifen, unabhängig von der Betriebssystemversion oder-Edition.

Wenn Sie z. b. Windows Server 2016 zum Erreichen einer SMB-Freigabe verwenden, die unter Windows 10 gehostet wird, ist Windows Server 2016 der SMB-Client und Windows 10 der SMB-Server.

### <a name="collect-data"></a>Sammeln von Daten

Bevor Sie SMB-Probleme beheben, sollten Sie zuerst eine Netzwerk Ablauf Verfolgung auf der Client-und der Serverseite erfassen. Es gelten die folgenden Richtlinien:

- Auf Windows-Systemen können Sie NetShell (Netsh), Netzwerkmonitor, Message Analyzer oder wireshark verwenden, um eine Netzwerk Ablauf Verfolgung zu erfassen.

- Geräte von Drittanbietern verfügen in der Regel über ein Paket Erfassungs Tool, wie z. b. tcpdump (Linux/FreeBSD/Unix) oder pktt (nettapp). Wenn der SMB-Client oder SMB-Server z. b. ein UNIX-Host ist, können Sie Daten erfassen, indem Sie den folgenden Befehl ausführen:
  
  ```cmd
  # tcpdump -s0 -n -i any -w /tmp/$(hostname)-smbtrace.pcap
  ```
  
  Das Sammeln von Daten wird beendet, indem **STRG + C** von Tastatur verwendet wird.

Um die Ursache des Problems zu ermitteln, können Sie die zweiseitigen Ablauf Verfolgungen überprüfen: CLI, SRV oder irgendwo dazwischen.

#### <a name="using-netshell-to-collect-data"></a>Verwenden von NetShell zum Sammeln von Daten

Dieser Abschnitt enthält die Schritte zum Verwenden von NetShell zum Erfassen der Netzwerk Ablauf Verfolgung.

> [!NOTE]  
> Eine Netsh-Ablauf Verfolgung erstellt eine ETL-Datei. ETL-Dateien können nur in Message Analyzer (MA) und Netzwerkmonitor 3,4 geöffnet werden (legen Sie den Parser auf Netzwerkmonitor Parser \> Fenster fest).

1. Erstellen Sie auf dem SMB-Server und dem SMB- **Client einen temporären** Ordner auf Laufwerk **C**. Führen Sie dann den folgenden Befehl aus:

   ```cmd
   netsh trace start capture=yes report=yes scenario=NetConnection level=5 maxsize=1024 tracefile=c:\\Temp\\%computername%\_nettrace.etl**
   ```
   
   Wenn Sie PowerShell verwenden, führen Sie die folgenden Cmdlets aus:
   
   ```PowerShell
   New-NetEventSession -Name trace -LocalFilePath "C:\Temp\$env:computername`_netCap.etl" -MaxFileSize 1024

   Add-NetEventPacketCaptureProvider -SessionName trace -TruncationLength 1500

   Start-NetEventSession trace
   ```
   
2. Reproduzieren Sie das Problem.

3. Führen Sie den folgenden Befehl aus, um die Ablauf Verfolgung anzuhalten:

   ```cmd
   netsh trace stop
   ```
   
   Wenn Sie PowerShell verwenden, führen Sie die folgenden Cmdlets aus:

   ```PowerShell
   Stop-NetEventSession trace  
   Remove-NetEventSession trace
   ```

> [!NOTE] 
> Sie sollten nur eine minimale Menge der übertragenen Daten verfolgen. Nehmen Sie bei Leistungsproblemen immer eine gute und schlechte Ablauf Verfolgung vor, wenn die Situation dies zulässt.

### <a name="analyze-the-traffic"></a>Analysieren des Datenverkehrs

SMB ist ein Protokoll auf Anwendungsebene, bei dem TCP/IP als Netzwerk Transportprotokoll verwendet wird. Daher kann ein SMB-Problem auch durch TCP/IP-Probleme verursacht werden.

Überprüfen Sie, ob bei TCP/IP folgende Probleme auftreten:

1. Der drei-Wege-Handshake von TCP wird nicht abgeschlossen. Dies weist in der Regel darauf hin, dass ein firewallblock vorhanden ist oder der Server Dienst nicht ausgeführt wird.

2. Erneute übertragen. Diese können aufgrund einer Verbund Einschränkung der TCP-Überlastung zu langsamen Dateiübertragungen führen.

3. Fünf Neusendungen, gefolgt von einer TCP-zurück setzung, können bedeuten, dass die Verbindung zwischen Systemen verloren gegangen ist oder einer der SMB-Dienste abgestürzt ist oder nicht mehr reagiert.

4. Das TCP-Empfangs Fenster wird verringert. Dies kann durch eine langsame Speicherung oder ein anderes Problem verursacht werden, das verhindert, dass Daten aus dem Winsock-Puffer des hilfsfunktionstreibers abgerufen werden.

Wenn kein auffälliges TCP/IP-Problem vorliegt, suchen Sie nach SMB-Fehlern. Gehen Sie hierzu folgendermaßen vor:

1. Überprüfen Sie immer SMB-Fehler anhand der MS-SMB2-Protokollspezifikation. Viele SMB-Fehler sind nicht schädlich (nicht schädlich). Beachten Sie die folgenden Informationen, um zu ermitteln, warum SMB den Fehler zurückgegeben hat, bevor Sie den Fehler mit einem der folgenden Probleme in Verbindung bringen:

   - Im Thema [MS-SMB2 Message-Syntax](https://docs.microsoft.com/openspecs/windows_protocols/ms-smb2/6eaf6e75-9c23-4eda-be99-c9223c60b181) werden die einzelnen SMB-Befehle und deren Optionen ausführlich erläutert.
    
   - Im Thema [MS-SMB2 Client processing](https://docs.microsoft.com/openspecs/windows_protocols/ms-smb2/df0625a5-6516-4fbe-bf97-01bef451cab2) wird erläutert, wie der SMB-Client Anforderungen erstellt und auf Server Nachrichten antwortet.

   - Im Thema [MS-SMB2 Server processing](https://docs.microsoft.com/openspecs/windows_protocols/ms-smb2/e1d08834-42e0-41ca-a833-fc26f5132a6f) wird erläutert, wie der SMB-Serveranforderungen erstellt und auf Client Anforderungen antwortet.

2. Überprüfen Sie, ob ein TCP-Reset-Befehl unmittelbar nach\_dem überprüfen\_aushandeln\_Info (Validate Aushandlungs)-Befehl gesendet wurde. Wenn dies der Fall ist, lesen Sie die folgenden Informationen:

   - Die SMB-Sitzung muss beendet werden (TCP Reset), wenn der Überprüfungs Aushandlungs Prozess auf dem Client oder dem Server fehlschlägt.

   - Dieser Vorgang kann fehlschlagen, weil ein WAN-Optimierer das SMB-Aushandlungs Paket ändert.

   - Wenn die Verbindung vorzeitig beendet wurde, identifizieren Sie die letzte Exchange-Kommunikation zwischen dem Client und dem Server.

#### <a name="analyze-the-protocol"></a>Analysieren des Protokolls

Sehen Sie sich die tatsächlichen SMB-Protokoll Details in der Netzwerk Ablauf Verfolgung an, um die exakt verwendeten Befehle und Optionen zu verstehen.

> [!NOTE]
> Die Befehle SMBv3 und spätere Version können nur von Message Analyzer analysiert werden.

- Denken Sie daran, dass SMB nur die Anforderungen erfüllt.

- Überprüfen Sie die SMB-Befehle, um zu erfahren, was die Anwendung tun soll.

Vergleichen Sie die Befehle und Vorgänge mit der Protokollspezifikation, um sicherzustellen, dass alles ordnungsgemäß funktioniert. Wenn dies nicht der Fall ist, erfassen Sie Daten, die näher an oder auf einer niedrigeren Ebene liegen, um nach weiteren Informationen zur Ursache zu suchen. Gehen Sie hierzu folgendermaßen vor:

1. Erfassen Sie eine Standardpaket Erfassung.

2. Führen Sie den **netsh** -Befehl aus, um zu verfolgen, ob Probleme im Netzwerk Stapel vorliegen oder ob in Windows Filter Platform (WFP)-Anwendungen, wie z. b. Firewall oder Antivirenprogramm, gelöscht werden.

3. Wenn alle anderen Optionen fehlschlagen, erfassen Sie eine t. cmd-Datei, wenn Sie vermuten, dass das Problem in SMB selbst auftritt oder wenn keine der anderen Daten ausreichend ist, um eine Grundursache zu ermitteln.

Zum Beispiel:

- Sie können langsame Dateiübertragungen zu einem einzelnen Dateiserver durcharbeiten.

- Die zweiseitigen Ablauf Verfolgungen zeigen, dass der SRV langsam auf eine Lese Anforderung antwortet.

- Wenn Sie ein Antivirenprogramm entfernen, werden die langsamen Dateiübertragungen aufgelöst.

- Um das Problem zu beheben, wenden Sie sich an das Hersteller Programm des Antivirenprogramms.

> [!NOTE]
> Optional können Sie das Antivirenprogramm **auch** während der Problembehandlung vorübergehend deinstallieren.

#### <a name="event-logs"></a>Ereignisprotokolle

Sowohl der SMB-Client als auch der SMB-Server verfügen über eine detaillierte Ereignisprotokoll Struktur, wie im folgenden Screenshot zu sehen. Sammeln Sie die Ereignisprotokolle, um die Ursache des Problems zu ermitteln.

![Ereignisprotokolle](media/troubleshooting-smb-1.png)

## <a name="smb-related-system-files"></a>SMB-bezogene Systemdateien

In diesem Abschnitt werden die SMB-bezogenen Systemdateien aufgelistet. Stellen Sie sicher, dass das aktuellste Updaterollup [](https://support.microsoft.com/en-us/help/4498140/windows-10-update-history) installiert ist, um die Systemdateien zu aktualisieren.

SMB-Client Binärdateien, die unter **% windir%\\System32\\-Treibern**aufgeführt sind:

- Rdbss. sys

- MRxSmb. sys

- MRXSMB10. sys

- MRXSMB20. sys

- MUP. sys

- Smbdirect. sys

SMB-Server-Binärdateien, die unter **% windir%\\System32\\-Treibern**aufgeführt sind:

- Srvnet. sys

- SRV. sys

- SRV2. sys

- Smbdirect. sys

- Unter **% windir%\\System32**

- srvsvc. dll

![SMB-Komponenten](media/troubleshooting-smb-2.png)

### <a name="update-suggestions"></a>Vorschläge aktualisieren

Es wird empfohlen, dass Sie die folgenden Komponenten aktualisieren, bevor Sie SMB-Probleme beheben:

- Ein Dateiserver erfordert Dateispeicher. Wenn Ihr Speicher über eine iSCSI-Komponente verfügt, aktualisieren Sie diese Komponenten.

- Aktualisieren Sie die Netzwerkkomponenten.

- Aktualisieren Sie Windows Core, um eine bessere Leistung und Stabilität zu erzielen.

## <a name="reference"></a>Referenz

[Microsoft SMB Protocol-Paket Austausch Szenario](https://docs.microsoft.com/windows/win32/fileio/microsoft-smb-protocol-packet-exchange-scenario)