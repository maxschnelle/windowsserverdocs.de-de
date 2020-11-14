---
title: Befehlssyntax und Formatierung von pktmon
description: Verwenden Sie diese Seite, um die Syntax, Befehle, die Formatierung und die Ausgabe von pktmon für Windows-vibrierungsbuilds nachzuvollziehen.
ms.topic: how-to
author: khdownie
ms.author: v-kedow
ms.date: 11/12/2020
ms.openlocfilehash: 3e4c73af3b00f42301b34e59493f25b6d2ccb95c
ms.sourcegitcommit: 8808f871c8cf131f819ef5540286218bd425da96
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/14/2020
ms.locfileid: "94632533"
---
# <a name="pktmon-command-syntax-and-formatting"></a>Befehlssyntax und Formatierung von pktmon

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows 10, Azure Stack HCI, Azure Stack Hub, Azure

Der Paket Monitor (pktmon) ist ein Komponenten übergreifendes Netzwerk Diagnosetool für Windows. Sie kann für die Paket Erfassung, die Paket Ablage Erkennung, das Filtern und zählen von Paketen verwendet werden. Das Tool ist besonders bei Virtualisierungsszenarien hilfreich, z. b. bei Container Netzwerken und Sdn, da es im Netzwerk Stapel sichtbar ist. Der Paket Monitor ist in-Box über pktmon.exe Befehl auf dem vibrianium-Betriebssystem (Build 19041) verfügbar. In diesem Thema erfahren Sie, wie Sie die pktmon-Syntax, die Formatierung und die Ausgabe von Befehlen verstehen.

## <a name="quick-start"></a>Schnellstart

Führen Sie die folgenden Schritte aus, um in generischen Szenarien zu beginnen:

1. Identifizieren Sie den Typ der für die Erfassung erforderlichen Pakete, d. h. bestimmte IP-Adressen, Ports oder Protokolle, die dem Paket zugeordnet sind. Überprüfen Sie dann die Syntax, um Erfassungs Filter anzuwenden, und wenden Sie die Filter für die Pakete an, die im vorherigen Schritt identifiziert wurden.

   ```PowerShell
   C:\Test> pktmon filter add help
   C:\Test> pktmon filter add <filters>
   ```

2. Starten Sie die Erfassung und aktivieren Sie die Paket Protokollierung.

   ```PowerShell
   C:\Test> pktmon start --etw
   ```

3. Reproduzieren Sie das Problem, das diagnostiziert wird. Abfrage Zähler, um zu bestätigen, dass erwarteter Datenverkehr vorhanden ist, und um eine allgemeine Übersicht darüber zu erhalten, wie der Datenverkehr auf dem Computer fließt.

   ```PowerShell
   C:\Test> pktmon counters
   ```

4. Halten Sie die Erfassung an, und rufen Sie die Protokolle zur Analyse im txt-Format ab.

   ```PowerShell
   C:\Test> pktmon stop
   C:\Test> pktmon format <etl file>
   ```

Anweisungen zum Analysieren der txt-Ausgabe finden Sie unter [Analysieren der Paket Monitor Ausgabe](#analyze-packet-monitor-output) .

## <a name="capture-filters"></a>Erfassungs Filter

Es wird dringend empfohlen, vor dem Starten einer Paket Erfassung Filter anzuwenden, da die Problembehandlung bei der Verbindung mit einem bestimmten Ziel einfacher ist, wenn Sie sich auf einen einzelnen Stream von Paketen konzentrieren. Wenn Sie den *gesamten* Netzwerk Datenverkehr erfassen, kann die Ausgabe für die Analyse zu stark ausfallen. Damit ein Paket gemeldet wird, muss es mit allen in mindestens einem Filter angegebenen Bedingungen identisch sein. Bis zu 32 Filter werden gleichzeitig unterstützt.

Der folgende Satz von Filtern erfasst z. b. den ICMP-Datenverkehr von oder zur IP-Adresse 10.0.0.10 sowie jeglichen Datenverkehr an Port 53.

```PowerShell
C:\Test> pktmon filter add -i 10.0.0.10 -t icmp
C:\Test> pktmon filter add -p 53
```

### <a name="filtering-capability"></a>Filterfunktion

- Der Paket Monitor unterstützt das Filtern nach Mac-Adressen, IP-Adressen, Ports, etherstyp, Transportprotokoll und VLAN-ID. 

- Der Paket Monitor unterscheidet nicht zwischen Quelle und Ziel, wenn es um Mac-Adresse, IP-Adresse oder Port Filter geht. 

- Zum weiteren Filtern von TCP-Paketen kann eine optionale Liste von TCP-Flags bereitgestellt werden. Unterstützte Flags sind FIN, SYN, RST, PSH, ACK, URG, ECE und CWR.

  - Beispielsweise werden mit dem folgenden Filter alle SYN-Pakete erfasst, die von der IP-Adresse 10.0.0.10 gesendet oder empfangen werden:

```PowerShell
C:\Test> pktmon filter add -i 10.0.0.10 -t tcp syn
```

- Der Paket Monitor kann einen Filter auf gekapselte innere Pakete anwenden, zusätzlich zum äußeren Paket, wenn das Flag [-e] einem beliebigen Filter hinzugefügt wurde. Unterstützte Kapselungs Methoden sind vxlan, GRE, nvgre und IP-in-IP. Der benutzerdefinierte vxlan-Port ist optional, und der Standardwert ist 4789.

### <a name="pktmon-filters-syntax"></a>Syntax von pktmon-Filtern

```PowerShell
C:\Test> pktmon filter help
pktmon filter { list | add | remove } [OPTIONS | help]

Commands
    list      Display active packet filters.
    add       Add a filter to control which packets are reported.
    remove    Removes all filters.

help
    Show help text for a command.

C:\Test> pktmon filter add help
pktmon filter add <name> [-m mac [mac2]] [-v vlan] [-d { IPv4 | IPv6 | number }]
                         [-t { TCP [flags...] | UDP | ICMP | ICMPv6 | number }]
                         [-i ip [ip2]] [-p port [port2]] [-e [port]]
    Add a filter to control which packets are reported. For a packet to be
    reported, it must match all conditions specified in at least one filter.
    Up to 8 filters can be active at once.

    NOTE1: When two MACs (-m), IPs (-i), or ports (-p) are specified, the filter
           matches packets that contain both. It will not distinguish between source
           or destination for this purpose.

name
    Optional name or description of the filter.

Ethernet frame
    -m, --mac[-address]
        Match source or destination MAC address. See NOTE1 above.

    -v, --vlan
        Match by VLAN Id (VID) in the 802.1Q header.

    -d, --data-link[-protocol], --ethertype
        Match by data link (layer 2) protocol. Can be IPv4, IPv6, ARP, or
        a protocol number.

IP header
    -t, --transport[-protocol], --ip-protocol
        Match by transport (layer 4) protocol. Can be TCP, UDP, ICMP, ICMPv6, or
        a protocol number.
        To further filter TCP packets, an optional list of TCP flags to match can
        be provided. Supported flags are FIN, SYN, RST, PSH, ACK, URG, ECE, and CWR.

    -i, --ip[-address]
        Match source or destination IP address. See NOTE1 above.
        To match by subnet, use CIDR notation with the prefix length.

TCP/UDP header
    -p, --port
        Match source or destination port number. See NOTE1 above.

Encapsulation
    -e, --encap
        This filter also applies to encapsulated inner packets, in addition to the outer
        packet. Supported encapsulation methods are VXLAN, GRE, NVGRE, and IP-in-IP.
        Custom VXLAN port is optional, and defaults to 4789.

Example 1: Ping filter
        pktmon filter add MyPing -i 10.10.10.10 -t ICMP

Example 2: TCP SYN filter for SMB traffic
    pktmon filter add MySmbSyn -i 10.10.10.10 -t TCP SYN -p 445

Example 3: Subnet filter
    pktmon filter add MySubnet -i 10.10.10.0/24
```

## <a name="packet-capture-and-logging"></a>Paket Erfassung und-Protokollierung

Mit dem Paket Monitor können Netzwerk Datenverkehr mit oder ohne Paket Protokollierung erfasst werden. Weitere Informationen zum Erfassen von Datenverkehr ohne Paket Protokollierung finden Sie im Abschnitt "Paket Zähler" weiter unten. Fügen Sie zum Erfassen und Protokollieren von Paketen den Parameter **[--etw]** zum Startbefehl hinzu.

Wählen Sie die zu überwachenden Komponenten mithilfe des Parameters **[-c]** aus. Dabei kann es sich um alle Komponenten, NICs oder eine Liste von Komponenten-IDs handeln. Der Standardwert ist die Erfassung von Datenverkehr an allen Komponenten. Überwachen von gelöschten Paketen nur mit dem Parameter [-d]. Der Standardwert ist die Erfassung von fließenden und gelöschten Paketen.

Mit dem folgenden Befehl werden z. b. Paket Zähler aller Netzwerkadapter ohne Protokollierungs Pakete aufgezeichnet:

```PowerShell
C:\Test> pktmon start -c nics
```

Mit dem folgenden Befehl werden jedoch nur die gelöschten Pakete erfasst, die die Komponenten 4 und 5 durchlaufen, und Sie werden protokolliert:

```PowerShell
C:\Test> pktmon start --etw -c 4,5 -d
```

### <a name="packet-logging-capability"></a>Paket Protokollierungsfunktion

- Der Paket Monitor unterstützt mehrere Protokollierungs Modi:

  - Zirkulär: neue Pakete überschreiben die ältesten, wenn die maximale Dateigröße erreicht ist. Dies ist der Standard Protokollierungs Modus.
  - Mehrere Dateien: eine neue Protokolldatei wird erstellt, wenn die maximale Dateigröße erreicht ist. Protokolldateien sind sequenziell nummeriert: PktMon1. ETL, PktMon2. ETL usw. Wenden Sie diesen Protokollierungs Modus an, um das gesamte Protokoll beizubehalten, aber seien Sie vorsichtig mit der Speicherauslastung. Hinweis: Verwenden Sie den Zeitstempel der Dateierstellung für jede Protokolldatei als Anzeichen für einen bestimmten Zeitrahmen in der Erfassung.
  - Echt Zeit: Pakete werden in Echtzeit auf dem Bildschirm angezeigt. Es wird keine Protokolldatei erstellt. Verwenden Sie STRG + C, um die Überwachung anzuhalten.
  - Arbeitsspeicher: Ereignisse werden in einen Zirkel Speicherpuffer geschrieben. Die Puffergröße wird durch den **[-s]-** Parameter angegeben. Puffer Inhalte werden nach dem Beenden der Erfassung in eine Protokolldatei geschrieben. Verwenden Sie diesen Protokollierungs Modus für sehr laute Szenarien, um große Mengen an Datenverkehr in sehr kurzer Zeit im Speicherpuffer aufzuzeichnen. Wenn Sie andere Protokollierungs Modi verwenden, kann der Datenverkehr möglicherweise verloren gehen.

- Geben Sie an, wie viel des Pakets durch den **[-p]** -Parameter protokolliert werden soll. Protokollieren Sie das gesamte Paket jedes Pakets, unabhängig von dessen Größe, indem Sie diesen Parameter auf 0 festlegen. Der Standardwert ist 128 Bytes, der die Header der meisten Pakete enthalten sollte.

- Geben Sie die Größe der Protokolldatei über den **[-s]-** Parameter an. Dabei handelt es sich um die maximale Größe der Datei in einem zirkulären Protokollierungs Modus, bevor der Paket Monitor mit dem Überschreiben der älteren Pakete mit den neueren Paketen beginnt. Dies ist auch die maximale Größe der einzelnen Dateien im Protokollierungs Modus für mehrere Dateien, bevor der Paket Monitor eine neue Datei zum Protokollieren der nächsten Pakete erstellt. Sie können diesen Parameter auch verwenden, um die Puffergröße für den Speicher Protokollierungs Modus festzulegen.

### <a name="pktmon-start-syntax"></a>Pktmon-Start Syntax

```PowerShell
C:\Test> pktmon start help
pktmon start [-c { all | nics | [ids...] }] [-d] [--etw [-p size] [-k keywords]]
             [-f] [-s] [--log-mode {circular | multi-file | real-time | memory}]
    Start packet monitoring.

-c, --components
    Select components to monitor. Can be all components, NICs only, or a
    list of component ids. Defaults to all.

-d, --drop-only
    Only report dropped packets. By default, successful packet propagation
    is reported as well.

ETW Logging
    --etw
        Start a logging session for packet capture.

    -p, --packet-size
        Number of bytes to log from each packet. To always log the entire
        packet, set this to 0. Default is 128 bytes.

    -k, --keywords
        Hexadecimal bitmask (i.e. sum of the below flags) that controls
        which events are logged. Default is 0x012.

        Flags:
        0x001 - Internal Packet Monitor errors.
        0x002 - Information about components, counters and filters.
                This information is added to the end of the log file.
        0x004 - Source and destination information for the first
                packet in NET_BUFFER_LIST group.
        0x008 - Select packet metadata from NDIS_NET_BUFFER_LIST_INFO
                enumeration.
        0x010 - Raw packet, truncated to the size specified in
                [--packet-size] parameter.

    -f, --file-name
        .etl log file. Default is PktMon.etl.

    -s, --file-size
        Maximum log file size in megabytes. Default is 512 MB.

    -l, --log-mode
        Select logging mode. Default is circular.

        circular
            New events overwrite the oldest ones when
            when the maximum file size is reached.

        multi-file
            A new log file is created when the maximum file size is reached.
            Log files are sequentially numbered. PktMon1.etl, PktMon2.etl, etc.

        real-time
            Display events and packets on screen at real time. No log file is created.
            Press Ctrl+C to stop monitoring.

        memory
            Events are written to a circular memory buffer.
            Buffer size is specified in [--file-size] parameter.
            Buffer contents is written to a log file during stop operation.

Example: pktmon start --etw -l real-time
```

## <a name="packet-analysis-and-formatting"></a>Paket Analyse und-Formatierung

Der Paket Monitor generiert Protokolldateien im ETL-Format. Es gibt mehrere Möglichkeiten, die ETL-Datei für die Analyse zu formatieren:

- Konvertieren Sie das Protokoll in das Textformat (die Standardoption), und analysieren Sie es mit dem Text-Editor-Tool wie TextAnalysisTool.net. Paketdaten werden im tcpdump-Format angezeigt. Befolgen Sie das nachfolgende Handbuch, um zu erfahren, wie Sie die Ausgabe in der Textdatei analysieren.
- Konvertieren des Protokolls in das pcapng-Format, um es mithilfe von [wireshark](pktmon-pcapng-support.md) zu analysieren*
- Öffnen Sie die ETL-Datei mit [Netzwerkmonitor](pktmon-netmon-support.md)*

>[!NOTE]
>* Verwenden Sie die obigen Links, um zu erfahren, wie Sie Paket Monitor Protokolle in **wireshark** und **Netzwerkmonitor** analysieren und analysieren.

### <a name="pktmon-format-syntax"></a>Pktmon-Format Syntax

```PowerShell
C:\Test> pktmon format help
pktmon format log.etl [-o log.txt] [-b] [-v [level]] [-x] [-e] [-l [port]
    Convert log file to text format.

-o, --out
    Name of the formatted text file.

-s, --stats-only
    Display log file statistical information.

Network packet formatting options

    -b, --brief
        Abbreviated packet format.

    -v, --verbose
        Verbosity level [1..3].

    -x, --hex
        Hexadecimal format.

    -e, --no-ethernet
        Don't print ethernet header.

    -l, --vxlan
        Custom VXLAN port.


Example: pktmon format C:\tmp\PktMon.etl

C:\Test> pktmon pcapng help
pktmon pcapng log.etl [-o log.pcapng]
    Convert log file to pcapng format.
    Dropped packets are not included by default.

-o, --out
    Name of the formatted pcapng file.

-d, --drop-only
    Convert dropped packets only.

-c, --component-id
    Filter packets by a specific component ID.

Example: pktmon pcapng C:\tmp\PktMon.etl -d -c nics
```

### <a name="analyze-packet-monitor-output"></a>Paket Monitor Ausgabe analysieren

Der Paket Monitor erfasst eine Momentaufnahme des Pakets von jeder Komponente des Netzwerk Stapels. Dementsprechend werden mehrere Momentaufnahmen der einzelnen Pakete angezeigt (in der Abbildung unten durch das blaue Feldlinien dargestellt).
Jede dieser Paket Momentaufnahmen wird durch ein paar Zeilen dargestellt (rote und grüne Felder). Es gibt mindestens eine Zeile, die einige Daten über die Paket Instanz enthält, beginnend mit dem Zeitstempel. Direkt nach gibt es mindestens eine Zeile (fett formatiert in der Abbildung unten), um das analysierte rohpaket im Textformat (ohne Zeitstempel) anzuzeigen. Es kann mehrere Zeilen sein, wenn das Paket gekapselt ist, wie z. b. das Paket im grünen Feld.

<center>

:::image type="content" source="media/pktmon-log-example.png" alt-text="Beispiel für die txt-Protokoll Ausgabe des Paket Monitors" border="false":::

</center>

Wenn Sie alle Momentaufnahmen derselben Pakete korrelieren, überwachen Sie die Werte pktgroupid und pktnumber (in gelb hervorgehoben). alle Momentaufnahmen desselben Pakets sollten diese beiden Werte gemeinsam haben. Der Darstellungs Wert (blau hervorgehoben) fungiert als Leistungsanzeige für jede nachfolgende Momentaufnahme desselben Pakets. Beispielsweise hat die erste Momentaufnahme des Pakets (bei dem das Paket zuerst im Netzwerk Stapel angezeigt wird) den Wert 1 für die Darstellung, die nächste Momentaufnahme den Wert 2 usw.

Jede Paket Momentaufnahme verfügt über eine Komponenten-ID (in der obigen Abbildung unterstrichen), die die der Momentaufnahme zugeordnete Komponente bezeichnet. Um den Komponentennamen und die Parameter aufzulösen, suchen Sie diese Komponenten-ID in der Liste Komponenten am Ende der Protokolldatei. Ein Teil der Komponenten Tabelle wird in der Abbildung unten mit der Markierung "Komponente 1" in gelb dargestellt (Dies war die Komponente, in der die letzte Momentaufnahme oben aufgezeichnet wurde).
Komponenten mit 2 Kanten melden zwei Momentaufnahmen an jedem Rand (z. b. die Momentaufnahmen mit Darstellung 3 und Darstellung 4, z. b. in der Abbildung oben).

Am Ende der einzelnen Protokolldateien wird die Filterliste angezeigt, wie in der folgenden Abbildung dargestellt (blau hervorgehoben). Jeder Filter zeigt die angegebenen Parameter (Protokoll-ICMP im folgenden Beispiel) und Nullen für die restlichen Parameter an.

<center>

:::image type="content" source="media/pktmon-log-example-components.png" alt-text="Beispiel für die txt-Protokoll Ausgabe Komponenten des Paket Monitors":::

</center>

Bei gelöschten Paketen wird das Wort "Drop" vor einer der Zeilen angezeigt, die die Momentaufnahme darstellen, in der das Paket gelöscht wurde. Jedes gelöschte Paket stellt auch einen dropreason-Wert bereit. Dieser dropreason-Parameter enthält eine kurze Beschreibung der Paket Ablage Ursache. beispielsweise Stimmen die MTU nicht überein, gefilterte VLANs usw.

<center>

:::image type="content" source="media/dropped-packet-log-example.png" alt-text="Beispiel eines gelöschten Paket Protokolls":::

</center>

## <a name="packet-counters"></a>Paketleistungsindikatoren

Paket Monitor Indikatoren bieten einen Überblick über den Netzwerk Datenverkehr im gesamten Netzwerk Stapel, ohne dass ein Protokoll analysiert werden muss, was ein kostspieliger Prozess sein kann. Überprüfen Sie die Datenverkehrs Muster, indem Sie nach dem Starten der Paket Monitor Erfassung Paket Zähler mit **pktmon** -Indikatoren Abfragen. Setzen Sie die Leistungsindikatoren mit der **pktmon-zurück** setzung auf NULL zurück, oder setzen Sie die Überwachung mit **pktmon-Stopps**

- Leistungsindikatoren werden durch Bindungs Stapel mit Netzwerkadaptern am oberen Rand und Protokolle unten angeordnet.
- TX/RX: Indikatoren werden in zwei Spalten für Sende-(TX) und RECEIVE-Anweisungen (RX) aufgeteilt.  
- Edges: Komponenten melden eine Paket Weitergabe, wenn ein Paket die Komponenten Begrenzung (Edge) überschreitet. Jede Komponente kann über einen oder mehrere Kanten verfügen. Miniport-Treiber verfügen in der Regel über einen einzelnen oberen Rand, Protokolle verfügen über einen einzelnen unteren Rand, und Filtertreiber verfügen über obere und untere Kanten.  
- DROPS: Paket Ablage Zähler werden in derselben Tabelle gemeldet.

Im folgenden Beispiel wurde eine neue Erfassung gestartet, dann wurde der Befehl **pktmon Counters** verwendet, um die Leistungsindikatoren abzufragen, bevor die Erfassung beendet wurde. Die Indikatoren zeigen ein einzelnes Paket, das aus dem Netzwerk Stapel stammt, beginnend mit der Protokollebene bis zum physischen Netzwerkadapter, und die Antwort wird in die andere Richtung zurückgegeben. Wenn das Ping oder die Antwort fehlte, ist es einfach, dies über die Leistungsindikatoren zu erkennen.

<center>

:::image type="content" source="media/pktmon-counters-with-perfect-flow.png" alt-text="Beispiel eines Paket Zählers mit perfektem Flow" border="false":::

</center>

Im nächsten Beispiel werden DROPS unter der Spalte "Counter" (Counter) gemeldet. Rufen Sie den letzten Ablage Grund für jede Komponente ab, indem Sie Leistungsindikator Daten im JSON-Format mit **pktmon-** Leistungsindikatoren (JSON) anfordern oder das Ausgabeprotokoll analysieren, um ausführlichere Informationen zu erhalten.

<center>

:::image type="content" source="media/pktmon-counters-drop-example.png" alt-text="Beispiel eines Paket Zählers mit einem gelöschten Paket" border="false":::

</center>

Wie in diesen Beispielen gezeigt, können die Leistungsindikatoren über ein Diagramm eine Menge von Informationen bereitstellen, die mit nur einem kurzen aussehen analysiert werden können.

### <a name="pktmon-counters-syntax"></a>Syntax der pktmon-Indikatoren

```PowerShell
C:\Test> pktmon counters help
pktmon [comp] counters [-t { all | drop | flow }] [-z] [--json]
    Display current per-component counters.

-t, --counter-type
    Select which types of counters to show.
    Supported values are all counters (default), drops only, or flows only.

-z, --show-zeros
    Show counters that are zero in both directions.

-i, --show-hidden
    Show components that are hidden by default.

--json
    Output the counters in JSON format.
```

## <a name="networking-stack-layout"></a>Netzwerk Stapel Layout

Überprüfen Sie das Netzwerk Stapel Layout mithilfe der Befehl **pktmon-Liste**.

:::image type="content" source="media/pktmon-networking-stack-example.png" alt-text="Beispiel für das Netzwerk Stapel Layout" border="false":::

Der Befehl zeigt Netzwerkkomponenten (Treiber) an, die von Adapter Bindungen angeordnet sind.

Eine typische Bindung besteht aus folgendem:

- Eine einzelne Netzwerkschnittstellenkarte (NIC)
- Einige (möglicherweise null) Filtertreiber
- Mindestens ein Protokoll Treiber (TCP/IP oder andere)

Jede Komponente wird durch eine Paket Monitor Komponenten-ID eindeutig identifiziert, die für einzelne Komponenten zur Überwachung verwendet wird.

>[!NOTE]
>IDs sind nicht persistent und können sich über Neustarts und den Treiber des Paket Monitors hinweg neu starten.

### <a name="pktmon-list-syntax"></a>Pktmon-Listen Syntax

```powershell
C:\Test> pktmon list help
pktmon [comp] list
    List all active components.

-i, --show-hidden
    Show components that are hidden by default.

--json
    Output the list in JSON format.
```