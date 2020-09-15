---
title: Beheben von Problemen auf dem DHCP-Server
description: Diese Artilce bietet eine Einführung in die Behandlung von Problemen auf dem DHCP-Server und das Sammeln von Daten.
manager: dcscontentpm
ms.date: 5/26/2020
ms.topic: article
author: Deland-Han
ms.author: delhan
ms.openlocfilehash: a6b5e4128c2e07e51ab8a9c07155a8c0212fcad8
ms.sourcegitcommit: 7cacfc38982c6006bee4eb756bcda353c4d3dd75
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/14/2020
ms.locfileid: "90078587"
---
# <a name="troubleshoot-problems-on-the-dhcp-server"></a>Beheben von Problemen auf dem DHCP-Server

In diesem Artikel wird erläutert, wie Sie Probleme beheben, die auf dem DHCP-Server auftreten.

## <a name="troubleshooting-checklist"></a>Checkliste zur Problembehandlung

Überprüfen Sie die folgenden Einstellungen:

  - Der DHCP-Server Dienst wird gestartet und ausgeführt. Um diese Einstellung zu überprüfen, führen Sie den Befehl **net Start** aus, und suchen Sie nach **DHCP-Server**.

  - Der DHCP-Server ist autorisiert. Weitere Informationen finden Sie [unter Windows-DHCP-Server Autorisierung in einer Domäne](/openspecs/windows_protocols/ms-dhcpe/56f8870b-a7c1-4db1-8a86-f69079fe5077)

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
Abhängig von der Art des Problems wird ein Ereignis in einem der folgenden Ereignis Kanäle protokolliert: DHCP- [Server-Betriebs Ereignisse](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn800668\(v=ws.11\)) 
 [DHCP-Server administrative Ereignisse](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn800668\(v=ws.11\))DHCP- 
 [Server System Ereignisse](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn800668\(v=ws.11\))DHCP- 
 [Server Filter Benachrichtigungs Ereignisse](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn800668\(v=ws.11\)) 
 [DHCP Server Audit Events](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn800668\(v=ws.11\)) DHCP-Server Überwachungs Ereignisse

## <a name="data-collection"></a>Datensammlung

### <a name="dhcp-server-log"></a>DHCP-Server Protokoll

Die Debugprotokolle des DHCP-Server Dienstanbieter enthalten weitere Informationen zur IP-Adress Lease-Zuweisung und den dynamischen DNS-Updates, die vom DHCP-Server ausgeführt werden. Diese Protokolle befinden sich standardmäßig unter% windir% \\ system32 \\ DHCP.
Weitere Informationen finden Sie unter [Analysieren von DHCP-Server Protokolldateien](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd183591\(v=ws.10\)).

### <a name="network-trace"></a>Netzwerkablaufverfolgung

Eine korrelierende Netzwerk Ablauf Verfolgung kann darauf hindeuten, was der DHCP-Server zum Zeitpunkt der Ereignisprotokollierung ausgeführt hat. Gehen Sie folgendermaßen vor, um eine solche Ablauf Verfolgung zu erstellen:

1.  Wechseln Sie zu [GitHub](https://github.com/CSS-Windows/WindowsDiag/tree/master/ALL/TSS), und laden Sie die [TSS- \_tools.zip](https://github.com/CSS-Windows/WindowsDiag/blob/master/ALL/TSS/tss_tools.zip) Datei herunter.

2.  Kopieren Sie die TSS \_ -tools.zip Datei, und erweitern Sie Sie auf einen Speicherort auf dem lokalen Datenträger, z. b. in den Ordner "C: \\ Tools".

3.  Führen Sie den folgenden Befehl in C: \\ Tools in einem Eingabe Aufforderungs Fenster mit erhöhten Rechten aus:
    ```console
    TSS Ron Trace <Stop:Evt:>20321:<Other:>DhcpAdminEvents NoSDP NoPSR NoProcmon NoGPresult
    ```

    >[!Note]
    >Ersetzen Sie in diesem Befehl \<*Stop:Evt:*\> und \<*Other:*\> durch die Ereignis-ID und den Ereignis Kanal, auf den Sie sich in ihrer Ablauf Verfolgungs Sitzung konzentrieren werden.
    >Die TSS. cmd- \_ \_ InfodateiHelp.docx Dateien, die in der TSS-tools.zip Datei enthalten sind, enthalten \_ Weitere Informationen zu allen verfügbaren Einstellungen.

4.  Nachdem das Ereignis ausgelöst wurde, erstellt das Tool einen Ordner mit dem Namen "C: \\ MS \_ Data". Dieser Ordner enthält einige nützliche Ausgabedateien, die allgemeine Informationen zur Netzwerk-und Domänen Konfiguration des Computers bereitstellen.
    Die interessanteste Datei in diesem Ordner ist "% Computername% \_ Date \_ time \_ packetcapture \_ Internetclient \_ dbg. ETL".
    Wenn Sie die [Netzwerkmonitor](https://www.microsoft.com/download/4865) Anwendung verwenden, können Sie die Datei laden und den Anzeige Filter für das DHCP-oder DNS-Protokoll festlegen, um zu ermitteln, was im Hintergrund geschieht.