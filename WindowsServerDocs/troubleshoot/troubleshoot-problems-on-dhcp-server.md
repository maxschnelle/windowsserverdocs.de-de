---
title: Beheben von Problemen auf dem DHCP-Server
description: Diese Artilce bietet eine Einführung in die Behandlung von Problemen auf dem DHCP-Server und das Sammeln von Daten.
ms.prod: windows-server
ms.service: na
manager: dcscontentpm
ms.technology: server-general
ms.date: 5/26/2020
ms.topic: article
author: Deland-Han
ms.author: delhan
ms.openlocfilehash: ad70b03fcb6d703a0b99435ee8715319d09af941
ms.sourcegitcommit: ef089864980a1d4793a35cbf4cbdd02ce1962054
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/28/2020
ms.locfileid: "84150198"
---
# <a name="troubleshoot-problems-on-the-dhcp-server"></a>Beheben von Problemen auf dem DHCP-Server

In diesem Artikel wird erläutert, wie Sie Probleme beheben, die auf dem DHCP-Server auftreten.

## <a name="troubleshooting-checklist"></a>Checkliste zur Problembehandlung

Überprüfen Sie die folgenden Einstellungen:

  - Der DHCP-Server Dienst wird gestartet und ausgeführt. Um diese Einstellung zu überprüfen, führen Sie den Befehl **net Start** aus, und suchen Sie nach **DHCP-Server**.

  - Der DHCP-Server ist autorisiert. Weitere Informationen finden Sie [unter Windows-DHCP-Server Autorisierung in einer Domäne](https://docs.microsoft.com/openspecs/windows_protocols/ms-dhcpe/56f8870b-a7c1-4db1-8a86-f69079fe5077)

  - Vergewissern Sie sich, dass IP-Adressleases im DHCP-Serverbereich für das Subnetz verfügbar sind, in dem sich der DHCP-Client befindet. Informationen hierzu finden Sie in der Statistik für den entsprechenden Bereich in der DHCP-Server-Verwaltungskonsole.

  - Überprüfen Sie, ob \_ in Adressleases fehlerhafte Adress Auflistungen zu finden sind.

  - Überprüfen Sie, ob für Geräte im Netzwerk statische IP-Adressen vorhanden sind, die nicht aus dem DHCP-Bereich ausgeschlossen wurden.

  - Vergewissern Sie sich, dass sich die IP-Adresse, an die der DHCP-Server gebunden ist, innerhalb des Subnetzes der Bereiche befindet, von denen IP-Adressen geleast werden müssen. Dies ist der Fall, wenn kein Relay-Agent verfügbar ist. Führen Sie hierzu das **Get-DhcpServerv4Binding-** oder **Get-DhcpServerv6Binding-** Cmdlet aus.

  - Vergewissern Sie sich, dass nur der DHCP-Server an UDP-Port 67 und 68 lauscht. Diese Ports müssen von keinem anderen Prozess oder anderen Diensten (z. b. WDS oder PXE) belegt werden. Führen Sie hierzu den Befehl aus `netstat -anb` .

  - Vergewissern Sie sich, dass die IPsec-Ausnahme für den DHCP-Server hinzugefügt wird, wenn Sie eine IPSec-bereitgestellte Umgebung haben.

  - Vergewissern Sie sich, dass die IP-Adresse des Relay-Agents vom DHCP-Server aus gepingt werden kann

  - Auflisten und Überprüfen von konfigurierten DHCP-Richtlinien und-filtern.

## <a name="event-logs"></a>Ereignisprotokolle

Überprüfen Sie die Ereignisprotokolle für den System-und DHCP-Server Dienst (**Anwendungs-und Dienst Protokolle** \> **Microsoft** \> **Windows** - \> **DHCP-Server**) auf gemeldete Probleme, die mit dem beobachteten Problem zusammenhängen.  
Abhängig von der Art des Problems wird ein Ereignis in einem der folgenden Ereignis Kanäle protokolliert:  
[Betriebs Ereignisse des DHCP-Servers](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn800668\(v=ws.11\))  
[Verwaltungs Ereignisse für DHCP-Server](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn800668\(v=ws.11\))  
[DHCP-Server System Ereignisse](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn800668\(v=ws.11\))  
[DHCP-Server-Filter Benachrichtigungs Ereignisse](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn800668\(v=ws.11\))  
[DHCP-Server Überwachungs Ereignisse](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn800668\(v=ws.11\))

## <a name="data-collection"></a>Datensammlung

### <a name="dhcp-server-log"></a>DHCP-Server Protokoll

Die Debugprotokolle des DHCP-Server Dienstanbieter enthalten weitere Informationen zur IP-Adress Lease-Zuweisung und den dynamischen DNS-Updates, die vom DHCP-Server ausgeführt werden. Diese Protokolle befinden sich standardmäßig unter% windir% \\ system32 \\ DHCP.  
Weitere Informationen finden Sie unter [Analysieren von DHCP-Server Protokolldateien](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd183591\(v=ws.10\)).

### <a name="network-trace"></a>Netzwerkablaufverfolgung

Eine korrelierende Netzwerk Ablauf Verfolgung kann darauf hindeuten, was der DHCP-Server zum Zeitpunkt der Ereignisprotokollierung ausgeführt hat. Gehen Sie folgendermaßen vor, um eine solche Ablauf Verfolgung zu erstellen:

1.  Wechseln Sie zu [GitHub](https://github.com/CSS-Windows/WindowsDiag/tree/master/ALL/TSS), und laden Sie die Datei [TSS \_ Tools. zip](https://github.com/CSS-Windows/WindowsDiag/blob/master/ALL/TSS/tss_tools.zip) herunter.

2.  Kopieren Sie die Datei "TSS \_ Tools. zip", und erweitern Sie Sie auf einen Speicherort auf dem lokalen Datenträger, z. b. in den Ordner "C: \\ Tools".

3.  Führen Sie den folgenden Befehl in C: \\ Tools in einem Eingabe Aufforderungs Fenster mit erhöhten Rechten aus:  
    ```console
    TSS Ron Trace <Stop:Evt:>20321:<Other:>DhcpAdminEvents NoSDP NoPSR NoProcmon NoGPresult
    ```
      
    >[!Note]
    >Ersetzen Sie in diesem Befehl \<*Stop:Evt:*\> und \<*Other:*\> durch die Ereignis-ID und den Ereignis Kanal, auf den Sie sich in ihrer Ablauf Verfolgungs Sitzung konzentrieren werden.  
    >Die "TSS. cmd"- \_ \_ Infodatei Help. docx-Dateien, die in der Datei "TSS Tools. zip" enthalten sind, enthalten \_ Weitere Informationen zu allen verfügbaren Einstellungen.

4.  Nachdem das Ereignis ausgelöst wurde, erstellt das Tool einen Ordner mit dem Namen "C: \\ MS \_ Data". Dieser Ordner enthält einige nützliche Ausgabedateien, die allgemeine Informationen zur Netzwerk-und Domänen Konfiguration des Computers bereitstellen.  
    Die interessanteste Datei in diesem Ordner ist "% Computername% \_ Date \_ time \_ packetcapture \_ Internetclient \_ dbg. ETL".
    Wenn Sie die [Netzwerkmonitor](https://www.microsoft.com/download/4865) Anwendung verwenden, können Sie die Datei laden und den Anzeige Filter für das DHCP-oder DNS-Protokoll festlegen, um zu ermitteln, was im Hintergrund geschieht.
