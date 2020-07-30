---
title: Problembehandlung bei einem Clusterproblem mit Ereignis-ID 1135
description: Hier wird beschrieben, wie Sie das Start Problem des Cluster Dienstanbieter mit der Ereignis-ID 1135 beheben.
ms.date: 05/28/2020
author: Deland-Han
ms.author: delhan
ms.openlocfilehash: 2836fc9385d57ff076828ab5cf6a1e341a7d88a8
ms.sourcegitcommit: 145cf75f89f4e7460e737861b7407b5cee7c6645
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/29/2020
ms.locfileid: "87409831"
---
# <a name="troubleshooting-cluster-issue-with-event-id-1135"></a>Problembehandlung bei einem Clusterproblem mit Ereignis-ID 1135

Dieser Artikel unterstützt Sie bei der Diagnose und Behebung der Ereignis-ID 1135, die während des Starts der Clusterdienst in der Failoverclustering-Umgebung protokolliert werden kann.

## <a name="start-page"></a>Startseite

Die Ereignis-ID 1135 zeigt an, dass mindestens ein Cluster Knoten aus der aktiven failoverclustermitgliedschaft entfernt wurde. Möglicherweise werden die folgenden Symptome angezeigt:

- Cluster failover\knoten werden aus der aktiven failoverclustermitgliedschaft entfernt: [Probleme mit Knoten, die aus der aktiven failoverclustermitgliedschaft entfernt werden](/problem-nodes-failover-cluster.md)
- Ereignis-ID 1069 [Ereignis-ID 1069 – geclusterte Dienst-oder Anwendungs Verfügbarkeit](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc756225(v=ws.10))
- Ereignis-ID 1177 für Quorum Verlust [Ereignis-ID 1177 – Quorum und Konnektivität, die für das Quorum erforderlich](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc773498(v=ws.10)) sind
- Ereignis-ID 1006 für Clusterdienst angehalten: [Ereignis-ID 1006 – Cluster Dienst Start](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc773418(v=ws.10))

Eine Überprüfung und die Netzwerktests werden als einer der ersten Schritte zur Problembehandlung empfohlen, um sicherzustellen, dass keine Konfigurationsprobleme vorliegen, die eine Ursache für Probleme darstellen könnten.

### <a name="check-if-installed-the-recommended-hot-fixes"></a>Überprüfen, ob die empfohlenen Hotfixes installiert sind

Der Clusterdienst ist die wesentliche Softwarekomponente, die alle Aspekte des failoverclustervorgangs steuert und die Cluster Konfigurations Datenbank verwaltet. Wenn Sie die Ereignis-ID 1135 sehen, empfiehlt Microsoft Ihnen, die in den folgenden KB-Artikeln erwähnten Korrekturen zu installieren und alle Knoten des Clusters neu zu starten. Überprüfen Sie dann, ob das Problem erneut auftritt.

- [Hotfix für Windows Server 2012 R2](https://support.microsoft.com/help/2920151)
- [Hotfix für Windows Server 2012](https://support.microsoft.com/help/2784261)
- [Hotfix für Windows Server 2008 R2](https://support.microsoft.com/help/2545685)

### <a name="check-if-the-cluster-service-running-on-all-the-nodes"></a>Überprüfen Sie, ob der Cluster Dienst auf allen Knoten ausgeführt wird.

Führen Sie den folgenden Befehl gemäß Ihrem Windows-Betriebssystem aus, um zu überprüfen, ob der Cluster Dienst kontinuierlich ausgeführt wird und verfügbar ist.

#### <a name="for-windows-server-2008-r2-cluster"></a>Für Windows Server 2008 R2-Cluster

Ausführen von cmd-Eingabeaufforderung mit erhöhten Rechten: **cluster.exe Knoten/stat**

#### <a name="for-windows-server-2012-and-windows-server-2012-r2-cluster"></a>Für Windows Server 2012 \ und Windows Server 2012 R2-Cluster

Ausführen des PS-Befehls: **Cluster Knoten/Status**

Wird der Cluster Dienst fortlaufend ausgeführt und ist auf allen Knoten verfügbar?

## <a name="solution-for-cluster-service-is-failing"></a>Fehler bei der Lösung für den Cluster Dienst.

Wenn der Cluster Dienst ausfällt, beheben Sie die Problembehandlung in diesem Artikel: [Windows Server 2008 und 2008R2-failoverclusterstartschalter](/archive/blogs/askcore/windows-server-2008-and-2008r2-failover-cluster-startup-switches).


## <a name="several-scenarios-of-event-id-1135"></a>Mehrere Szenarien der Ereignis-ID 1135

Wir möchten, dass Sie sich die System Ereignisprotokolle auf allen Knoten des Clusters genauer ansehen. Überprüfen Sie die Ereignis-ID 1135, die auf den Knoten angezeigt wird, und kopieren Sie alle Instanzen dieses Ereignisses. Dies erleichtert es Ihnen, Sie zu sehen und zu überprüfen.

```console
Event ID 1135
Cluster node ' **NODE A** ' was removed from the active failover cluster membership. The Cluster service on this node may have stopped. This could also be due to the node having lost communication with other active nodes in the failover cluster. Run the Validate a Configuration wizard to check your network configuration. If the condition persists, check for hardware or software errors related to the network adapters on this node. Also check for failures in any other network components to which the node is connected such as hubs, switches, or bridges.
```

Es gibt drei typische Szenarien:

### <a name="scenario-a"></a>Szenario A

Sie sehen sich alle Ereignisse an, und alle Knoten im Cluster weisen darauf hin, dass die Kommunikation von Knoten A verloren gegangen ist.

![Szenario a ](media/troubleshooting-cluster-event-id-1135/18647.png)
 ![](media/troubleshooting-cluster-event-id-1135/18648.png)

Möglicherweise ist es möglich, dass beim Anzeigen der Systemprotokolle auf Knoten A Ereignisse für alle verbleibenden Knoten im Cluster angezeigt werden.

#### <a name="solution"></a>Lösung

Dies deutet darauf hin, dass zum Zeitpunkt des Problems entweder aufgrund einer Überlastung des Netzwerks oder andernfalls die Kommunikation mit dem Knoten A verloren gegangen ist.

Sie sollten die Probleme mit der Netzwerkkonfiguration und der Kommunikation überprüfen und überprüfen. Denken Sie daran, nach Problemen im Zusammenhang mit Knoten A zu suchen.

### <a name="scenario-b"></a>Szenario B

Sie sehen sich die Ereignisse auf den Knoten an, und wir sagen, dass Ihr Cluster auf zwei Standorte verteilt ist. Knoten a, Knoten B und Knoten C an Standort 1 und Knoten D & Knoten E an Standort 2.

![Szenario B](media/troubleshooting-cluster-event-id-1135/18649.png)

Auf den Knoten A, B und C werden Sie feststellen, dass die protokollierten Ereignisse für die Konnektivität mit den Knoten D & E stehen. Wenn die Ereignisse auf Knoten D & E angezeigt werden, wird auf ähnliche Weise empfohlen, die Kommunikation mit A, B und C zu verlieren.

![Szenario B](media/troubleshooting-cluster-event-id-1135/18650.png)

#### <a name="solution"></a>Lösung

Wenn eine ähnliche Aktivität angezeigt wird, weist dies darauf hin, dass ein Kommunikationsfehler aufgetreten ist, über den Link, der diese Standorte verbindet. Wir empfehlen Ihnen, die Verbindung über die Websites hinweg zu überprüfen. wenn es sich um eine WAN-Verbindung handelt, sollten Sie die Verbindung mit Ihrem ISP über die Konnektivität überprüfen.

### <a name="scenario-c"></a>Szenario C

Sie sehen sich die Ereignisse auf den Knoten an, und Sie sehen, dass die Namen der Knoten nicht mit einem bestimmten Muster übereinstimmen. Nehmen wir an, dass Ihr Cluster auf zwei Standorte verteilt ist. Knoten a, Knoten B und Knoten C an Standort 1 und Knoten D & Knoten E an Standort 2.

- Auf Knoten A: Sie sehen Ereignisse für die Knoten B, D, E.
- Auf Knoten B: Sie sehen Ereignisse für die Knoten C, D, E.
- Auf Knoten C: werden Ereignisse für die Knoten A, B, E angezeigt.
- Auf Knoten D: Sie sehen Ereignisse für die Knoten A, C, E.
- Auf Knoten E: Es werden Ereignisse für die Knoten B, C, D angezeigt.
- Oder eine beliebige andere Kombination.

![Szenario C](media/troubleshooting-cluster-event-id-1135/18651.png)

#### <a name="solution"></a>Lösung

Solche Ereignisse sind möglich, wenn die Netzwerk Kanäle zwischen den Knoten unterstrichen sind und die Cluster Kommunikations Nachrichten nicht rechtzeitig erreicht werden. Dadurch kann der Cluster die Kommunikation zwischen den Knoten verlieren, was dazu führt, dass Knoten aus der Cluster Mitgliedschaft entfernt werden.

## <a name="review-cluster-networks"></a>Überprüfen von Cluster Netzwerken

Es wird empfohlen, dass Sie die Cluster Netzwerke überprüfen, indem Sie die folgenden drei Optionen nacheinander überprüfen, um dieses Handbuch zur Problembehandlung fortzusetzen.

### <a name="check-for-antivirus-exclusion"></a>Auf antivirenausschluss überprüfen

Schließen Sie die folgenden Dateisystem Speicherorte von der Viren Überprüfung auf einem Server aus, auf dem Cluster Dienste ausgeführt werden:

- Der Pfad des Dateifreigabe Zeugen.

- Der *Ordner "%systemroot%\cluster* "

Konfigurieren Sie die Echt Zeit Scan Komponente in der Antivirussoftware, um die folgenden Verzeichnisse und Dateien auszuschließen:

- Standard Konfigurationsverzeichnis für virtuelle Maschinen (c:\ProgramData\Microsoft\Windows\Hyper-v)

- Konfigurations Verzeichnisse für benutzerdefinierte virtuelle Computer

- Standardverzeichnis für virtuelle Festplattenlaufwerke (c:\Users\Public\Documents\Hyper-v\virtuelle Festplatten)

- Benutzerdefinierte virtuelle Festplatten Laufwerks Verzeichnisse

- Benutzerdefinierte Replikations Datenverzeichnisse bei Verwendung des Hyper-V-Replikats

- Momentaufnahme Verzeichnisse

- mms.exe

    > [!NOTE]
    > Diese Datei muss möglicherweise als Prozess Ausschluss innerhalb der Antivirussoftware konfiguriert werden.)

- Vmwp.exe

    > [!NOTE]
    > Diese Datei muss möglicherweise als Prozess Ausschluss innerhalb der Antivirussoftware konfiguriert werden.

Wenn Sie Livemigration in Verbindung mit freigegebenen Clustervolumes verwenden, schließen Sie außerdem den CSV-Pfad *c:\ClusterStorage* und alle zugehörigen Unterverzeichnisse aus. Wenn Sie Failoverprobleme beheben oder allgemeine Probleme bei der Installation von Cluster Diensten und Antivirussoftware auftreten, deinstallieren Sie die Antivirussoftware vorübergehend, oder überprüfen Sie den Hersteller der Software, um zu ermitteln, ob die Antivirensoftware mit den Cluster Diensten Die Deaktivierung der Antivirussoftware ist in den meisten Fällen nicht ausreichend. Auch wenn Sie die Antivirussoftware deaktivieren, wird der Filtertreiber immer noch geladen, wenn Sie den Computer neu starten.

### <a name="check-for-network-port-configuration-in-firewall"></a>Überprüfen der Netzwerk Port Konfiguration in der Firewall

Der Clusterdienst steuert Server Cluster Vorgänge und verwaltet die Cluster Datenbank. Bei einem Cluster handelt es sich um eine Sammlung von unabhängigen Computern, die als einzelner Computer fungieren. Vorgesetzten, Programmierern und Benutzern wird der Cluster als einzelnes System angezeigt. Die Software verteilt Daten zwischen den Knoten des Clusters. Wenn ein Knoten ausfällt, stellen andere Knoten die Dienste und Daten bereit, die zuvor vom fehlenden Knoten bereitgestellt wurden. Wenn ein Knoten hinzugefügt oder repariert wird, werden von der Cluster Software einige Daten zu diesem Knoten migriert.

System Dienst Name: **ClusSvc**

|Application|Protocol|Ports|
|---|---|---|
|Cluster Dienst|UDP|3343|
|Cluster Dienst|TCP|3343 (dieser Port ist bei einem Knoten Verknüpfungs Vorgang erforderlich.)|
|RPC|TCP|135|
|Cluster Verwaltung|UDP|137|
|Kerberos|udp\tcp|464 *|
|SMB|TCP|445|
|Nach dem Zufallsprinzip zugewiesene hohe UDP-Ports * *|UDP|Zufällige Portnummer zwischen 1024 und 65535<br/>Zufällige Portnummer zwischen 49152 und 65535 * * *|
||||

> [!NOTE]
> Außerdem sollten Sie für die erfolgreiche Überprüfung von Windows-Failoverclustern unter Windows Server 2008 und höher eingehenden und ausgehenden Datenverkehr für ICMP4, ICMP6 zulassen.

- Weitere Informationen finden Sie unter [Erstellen eines Windows Server 2012-Failoverclusters schlägt fehl mit Fehler 0xc000005e](https://support.microsoft.com/help/2830510).

- Weitere Informationen zum Anpassen dieser Ports finden Sie unter [Dienst Übersicht und Netzwerk Port Anforderungen für Windows](https://support.microsoft.com/help/832017/) im Abschnitt "Verweise".

Dies ist der Bereich in Windows Server 2012, Windows 8, Windows Server 2008 R2, Windows 7, Windows Server 2008 und Windows Vista.

Führen Sie außerdem den folgenden Befehl aus, um die Konfiguration des Netzwerk Ports in der Firewall zu überprüfen. Beispiel: Dieser Befehl hilft bei der Ermittlung von Port 3343 available\open, der für den Failovercluster verwendet wird:

```console
netsh advfirewall firewall show rule name="Failover Clusters (UDP-In)" verbose
```

### <a name="run-the-cluster-validation-report-for-any-errors-or-warnings"></a>Ausführen des Cluster Validierungs Berichts für Fehler oder Warnungen

Das Cluster Überprüfungs Tool führt eine Reihe von Tests aus, um zu überprüfen, ob Ihre Hardware und Einstellungen mit dem Failoverclustering kompatibel sind.

Befolgen Sie diese Anweisungen:

1. Führen Sie den Cluster Validierungsbericht für Fehler oder Warnungen aus. Weitere Informationen finden Sie Untergrund Legendes zu [Cluster Validierungs Tests: Netzwerk](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771323(v=ws.11)?redirectedfrom=MSDN)

    ![subhatt1](media/troubleshooting-cluster-event-id-1135/18653.png)

2. Überprüfen Sie Warnungen und Fehler für Netzwerke. Weitere Informationen finden Sie Untergrund Legendes zu [Cluster Validierungs Tests: Netzwerk](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771323(v=ws.11)?redirectedfrom=MSDN).

    ![Ergebnisse nach ](media/troubleshooting-cluster-event-id-1135/18654.png) ![ kategorienetzwerk](media/troubleshooting-cluster-event-id-1135/18655.png)

#### <a name="check-the-list-network-binding-order"></a>Überprüfen der Liste der Netzwerk Bindungs Reihenfolge

Dieser Test listet die Reihenfolge auf, in der Netzwerke an die Adapter auf jedem Knoten gebunden werden.

Auf der Registerkarte Adapter und Bindungen werden die Verbindungen in der Reihenfolge aufgelistet, in der von Netzwerkdiensten auf die Verbindungen zugegriffen wird. Die Reihenfolge dieser Verbindungen gibt die Reihenfolge an, in der generische TCP/IP-Aufrufe/-Pakete an das Netzwerk gesendet werden.

Führen Sie die folgenden Schritte aus, um die Bindungs Reihenfolge der Netzwerkadapter zu ändern:

1. Klicken Sie im **Startmenü**auf **Ausführen**, geben Sie ncpa.cpl ein, und klicken Sie dann auf **OK**. Sie können die verfügbaren Verbindungen im **LAN-und Hochgeschwindigkeits-Internet** Abschnitt des Fensters **Netzwerkverbindungen** sehen.

2. Klicken Sie im Menü **erweitert** auf **Erweiterte Einstellungen**, und klicken Sie dann auf die Registerkarte **Adapter und Bindungen** .

3. Wählen Sie im Bereich **Verbindungen** die Verbindung aus, die Sie in der Liste nach oben verschieben möchten. Verwenden Sie die Pfeil Schaltflächen, um die Verbindung zu verschieben. Als allgemeine Regel gilt: die Karte, die mit dem Netzwerk kommuniziert (Domänen Konnektivität, Routing an andere Netzwerke usw.), sollte die erste gebundene Karte (oben auf der Liste) sein.

Cluster Knoten sind mehrfach vernetzte Systeme. Netzwerk Priorität wirkt sich auf den DNS-Client für ausgehende Netzwerk Konnektivität aus. Netzwerkadapter, die für die Client Kommunikation verwendet werden, sollten sich in der Bindungs Reihenfolge am Anfang befinden. Nicht weitergeleitete Netzwerke können mit niedrigerer Priorität platziert werden. In Windows Server 2012 und Windows Server2012 R2 wird der Cluster Netzwerktreiber (NETFT.SYS) automatisch unten in der Liste der Bindungs Reihenfolge platziert.

#### <a name="check-the-validate-network-communication"></a>Überprüfen Sie die Netzwerkkommunikation überprüfen

Dies kann auch dazu führen, dass die Latenz in Ihrem Netzwerk auftritt. Die Pakete können zwischen den Knoten nicht verloren gehen, Sie werden jedoch möglicherweise nicht schnell genug auf die Knoten übergegangen, bevor das Timeout abläuft.

Mit diesem Test wird überprüft, ob getestete Server mit akzeptabler Latenz in allen Netzwerken kommunizieren können.

Beispiel: unter Überprüfen der Netzwerkkommunikation werden möglicherweise folgende Meldungen zu Problemen mit der Netzwerk Latenz angezeigt.

```console
Succeeded in pinging network interface node003.contoso.com IP Address 192.168.0.2 from network interface node004.contoso.com IP Address 192.168.0.3 with maximum delay 500 after 1 attempt(s).
Either address 10.0.0.96 is not reachable from 192.168.0.2 or **the ping latency is greater than the maximum allowed 2000 ms** This may be expected, since network interfaces node003.contoso.com - Heartbeat Network and node004.contoso.com - Production Network are on different cluster networks
Either address 192.168.0.2 is not reachable from 10.0.0.96 or **the ping latency is greater than the maximum allowed 2000 ms** This may be expected, since network interfaces node004.contoso.com - Production Network and node003.contoso.com - Heartbeat Network for MSCS are on different cluster networks
```

Bei einem Cluster mit mehreren Standorten können Sie die Timeout Werte erhöhen. Weitere Informationen finden Sie unter [Konfigurieren von Takt-und DNS-Einstellungen in einem Failovercluster mit mehreren Stand](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd197562(v=ws.10)?redirectedfrom=MSDN)Orten.

Wenden Sie sich an den ISP, um WAN-Verbindungsprobleme

Überprüfen Sie, ob die folgenden Probleme auftreten.

##### <a name="network-packets-lost-between-nodes"></a>Zwischen Knoten verlorene Netzwerkpakete

1. Überprüfen von Paket Verlusten mithilfe der Leistung

    Wenn das Paket bei der Übertragung irgendwo zwischen den Knoten verloren geht, schlagen die Takte fehl. Wir können mühelos feststellen, ob es sich um ein Problem handelt. verwenden Sie hierzu den System Monitor, um den Leistungsindikatoren "Netzwerkschnittstelle\Empfangene Pakete erhalten" zu betrachten Wenn Sie diesen Leistungs Besatz hinzugefügt haben, sehen Sie sich die durchschnittlichen, minimalen und maximalen Zahlen an, und wenn es sich um einen Wert handelt, der größer als 0 (null) ist, muss der Empfangs Puffer für den Adapter angepasst werden.

    ![Leistungsindikatoren hinzufügen](media/troubleshooting-cluster-event-id-1135/18652.png)

    Wenn Sie das Netzwerk Paket auf der VMware-Virtualisierungsplattform verloren haben, finden Sie weitere Informationen im Abschnitt "auf der VMware-Virtualisierungsplattform installierter Cluster

2. Aktualisieren der NIC-Treiber

    Dieses Problem kann aufgrund veralteter NIC-drivers\integration Components (IC) \vmtools oder fehlerhafter NIC-Adapter auftreten.
    Wenn zwischen den Knoten auf physischen Computern Netzwerkpakete verloren gehen, sollten Sie die Treiber Updates für den Netzwerkadapter durchführen. Alte oder veraltete Netzwerkkarten Treiber und/oder Firmware.
    Manchmal kann eine einfache Fehlkonfiguration der Netzwerkkarte oder des Schalters auch zu einem Verlust von Takten führen.

##### <a name="cluster-installed-in-the-vmware-virtualization-platform"></a>Cluster auf der VMware-Virtualisierungsplattform installiert

Überprüfen Sie die VMware-Adapter Probleme im Falle einer VMware-Umgebung.

Dieses Problem tritt möglicherweise auf, wenn die Pakete bei hohem Datenverkehrs aufkommen gelöscht werden. Stellen Sie sicher, dass keine Datenverkehrs Filterung stattfindet (z. b. mit einem e-Mail-Filter). Nachdem Sie diese Möglichkeit beseitigt haben, erhöhen Sie die Anzahl von Puffern im Gast Betriebssystem schrittweise, und überprüfen Sie, ob

Führen Sie die folgenden Schritte aus, um Burst Datenverkehr zu verringern:

1. Öffnen Sie das Testfeld mit der Windows-Taste + R.
2. Geben Sie devmgmt. msc ein, und drücken **Sie Eingabe**Taste.
3. Erweitern von **Netzwerkadaptern**
4. Klicken Sie mit der rechten Maustaste auf **vmxnet3, und klicken Sie**
5. Klicken Sie auf die Registerkarte **Erweitert**.
6. Klicken Sie auf **kleine RX-Puffer** , und erhöhen Sie den Wert. Der Standardwert ist 512, und der Höchstwert beträgt 8192.
7. Klicken Sie auf **RX-Ring #1** Größe, und erhöhen Sie den Wert. Der Standardwert ist 1024, und der Höchstwert beträgt 4096.

Überprüfen Sie die folgenden URLs, um Probleme bei VMware-Adaptern bei der VMware-Umgebung zu überprüfen

- [Knoten werden aus der failoverclustermitgliedschaft in VMware ESX entfernt?](/archive/blogs/askcore/nodes-being-removed-from-failover-cluster-membership-on-vmware-esx)

- [Großer Paketverlust auf der Ebene des Gast Betriebssystems auf der VMXNET3-vNIC in ESXi](https://kb.vmware.com/s/article/2039495)

##### <a name="noticed-any-network-congestion"></a>Netzwerk Überlastung bemerkt

Netzwerk Überlastung kann auch Probleme mit der Netzwerkverbindung verursachen.

Überprüfen Sie, ob Ihr Netzwerk gemäß MS und den Empfehlungen des Anbieters konfiguriert ist, siehe [Konfigurieren von Windows-failoverclusternetzwerken](/archive/blogs/askcore/configuring-windows-failover-cluster-networks)

##### <a name="check-the-network-configuration"></a>Überprüfen Sie die Netzwerkkonfiguration.

Wenn dies immer noch nicht funktioniert, überprüfen Sie, ob Sie ein partitioniertes Netzwerk in der Cluster-GUI oder NIC-Team Vorgang auf der Takt-NIC aktiviert haben.

Wenn Sie ein partitioniertes Netzwerk in der Cluster-GUI sehen, finden Sie weitere Informationen unter ["partitionierte" Cluster Netzwerke](/archive/blogs/askcore/partitioned-cluster-networks) , um das Problem zu beheben.

Wenn Sie NIC-Team Vorgang auf der Takt-NIC aktiviert haben, überprüfen Sie die Funktion "Team Vorgang Software" gemäß der Empfehlung des Hersteller Anbieters.

##### <a name="upgrade-the-nic-drivers"></a>Aktualisieren der NIC-Treiber

Dieses Problem kann aufgrund veralteter NIC-Treiber oder fehlerhafter NIC-Adapter auftreten.

Wenn zwischen den Knoten auf physischen Computern Netzwerkpakete verloren gehen, lassen Sie den Treiber für den Netzwerkadapter aktualisieren. Alte oder veraltete Netzwerkkarten Treiber und/oder Firmware.

Manchmal kann eine einfache Fehlkonfiguration der Netzwerkkarte oder des Schalters auch zu einem Verlust von Takten führen.

##### <a name="check-the-network-configuration"></a>Überprüfen Sie die Netzwerkkonfiguration.

Wenn dies immer noch nicht funktioniert, überprüfen Sie, ob Sie ein partitioniertes Netzwerk in der Cluster-GUI gesehen haben oder ob NIC-Team Vorgang auf der Takt-NIC aktiviert ist.
