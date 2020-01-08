---
title: Problem mit hoher CPU-Auslastung auf dem SMB-Server
description: Erläutert, wie das Problem mit hoher CPU-Auslastung auf dem SMB-Server behoben wird.
author: Deland-Han
manager: dcscontentpm
audience: ITPro
ms.topic: article
ms.author: delhan
ms.date: 12/25/2019
ms.openlocfilehash: 8a14952ca90b6ee3bea901fd944d7c9843492fd4
ms.sourcegitcommit: 8cf04db0bc44fd98f4321dca334e38c6573fae6c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/03/2020
ms.locfileid: "75654341"
---
# <a name="high-cpu-usage-issue-on-the-smb-server"></a>Problem mit hoher CPU-Auslastung auf dem SMB-Server

In diesem Artikel wird erläutert, wie Sie das Problem mit hoher CPU-Auslastung auf dem SMB-Server beheben.

## <a name="high-cpu-usage-because-of-storage-performance-issues"></a>Hohe CPU-Auslastung aufgrund von Speicher Leistungsproblemen

Speicher Leistungsprobleme können zu einer hohen CPU-Auslastung auf SMB-Servern führen. Stellen Sie vor der Problembehandlung sicher, dass das aktuellste Updaterollup auf dem SMB-Server installiert ist, um bekannte Probleme in SRV2. sys auszuschließen.

In den meisten Fällen wird das Problem der hohen CPU-Auslastung im System Prozess festzustellen. Bevor Sie fortfahren, stellen Sie mithilfe des Prozess-Explorers sicher, dass SRV2. sys oder NTFS. sys übermäßig viele CPU-Ressourcen beansprucht.

### <a name="storage-area-network-san-scenario"></a>San-Szenario (Storage Area Network)

In Aggregat Ebenen scheint die allgemeine San-Leistung in Ordnung zu sein. Wenn Sie jedoch mit SMB-Problemen arbeiten, ist die Antwortzeit der einzelnen Anforderungen die höchste Bedeutung.

Im Allgemeinen kann dieses Problem durch eine Art von Befehls Warteschlange im San verursacht werden. Mit **Perfmon** können Sie eine **Microsoft-Windows-Storport-** Ablauf Verfolgung erfassen und analysieren, um die Speicher Reaktionsfähigkeit genau zu bestimmen.

### <a name="disk-io-latency"></a>E/a-Latenz

Die Datenträger-e/a-Latenz ist ein Maß für die Verzögerung zwischen dem Zeitpunkt, zu dem eine Datenträger-e/a angefordert wird

Die e/a-Latenzzeit, die in Perfmon gemessen wird, umfasst die gesamte Zeit, die in den Hardware Schichten aufgewendet wird, sowie die Zeit, die in der Microsoft Port Driver-Warteschlange aufgewendet wird (Storport. sys für SCSI). Wenn die laufenden Prozesse eine große Storport-Warteschlange generieren, erhöht sich die gemessene Latenz. Dies liegt daran, dass e/a warten muss, bevor es an die Hardware Schichten gesendet wird.

In Perfmon zeigen die folgenden Indikatoren die Wartezeit für physische Datenträger an:

- "Leistungs Objekt für physische Datenträger"-\> "Mittlere Sek./Lesevorgänge" – zeigt die durchschnittliche Lese Latenz an.

- "Leistungs Objekt für physische Datenträger"-\> "Mittlere Sek./Schreibvorgänge" – zeigt die durchschnittliche Schreib Latenz an.

- "Leistungs Objekt für physische Datenträger"-\> "Durchschn. Sek./Übertragung" – Dies zeigt die kombinierten Durchschnittswerte für Lese-und Schreibvorgänge.

Die "\_gesamt"-Instanz ist ein Durchschnitt der Wartezeiten für alle physischen Datenträger auf dem Computer. Jede andere Instanz stellt einen einzelnen physischen Datenträger dar.

> [!NOTE]
> Verwechseln Sie diese Leistungsindikatoren nicht mit Durchschnittl. Datenträger Übertragungen/Sek. Dabei handelt es sich um ganz andere Leistungsindikatoren.

### <a name="windows-storage-stack-follows"></a>Windows-Speicher Stapel folgt

Dieser Abschnitt enthält eine kurze Erläuterung zum Windows-Speicher Stapel.

Wenn eine Anwendung eine IO-Anforderung erstellt, sendet Sie die Anforderung an das Windows-e/a-Subsystem am Anfang des Stapels. Die e/a-Vorgänge werden dann bis zum Hardware-Subsystem "Disk" übertragen. Anschließend wird die Antwort alle nach oben bewegt. Während dieses Vorgangs führt jede Ebene ihre Funktion aus und übergibt dann die e/a-Vorgänge an die nächste Ebene.

![Stapel Fluss](media/high-cpu-usage-issue-on-smb-server-1.png)

Perfmon erstellt keine Leistungsdaten pro Sekunde. Stattdessen werden Daten verwendet, die von anderen Subsystemen innerhalb von Windows bereitgestellt werden.

Für das Leistungs Objekt "physischer Datenträger" werden die Daten auf der Ebene "Partitions-Manager" im Speicher Stapel aufgezeichnet.

Wenn wir die im vorherigen Abschnitt erwähnten Indikatoren messen, messen wir die Zeit, die für die Anforderung aufgewendet wird, unterhalb der Ebene "Partitions-Manager". Wenn die e/a-Anforderung vom Partitions-Manager nach unten im Stapel gesendet wird, wird Sie Zeitstempel versehen. Wenn der Wert zurückgegeben wird, versehen wir ihn erneut und berechnen den Zeitunterschied. Der Zeitunterschied ist die Latenzzeit.

Auf diese Weise wird die Zeit berücksichtigt, die in den folgenden Komponenten aufgewendet wird:

- Klassen Treiber: Hiermit wird der Gerätetyp verwaltet, z. b. Datenträger, Bänder usw.

- Port Treiber: Hiermit wird das Transportprotokoll, z. b. SCSI, FC, SATA usw., verwaltet.

- Geräte-Miniport-Treiber: Dies ist der Gerätetreiber für den Speicher Adapter. Sie wird vom Hersteller der Geräte, z. b. RAID-Controller und FC-HBA, bereitgestellt.

- Disk Subsystem: Dies schließt alle Elemente ein, die unter dem Geräte-Miniport-Treiber liegen. Dies kann so einfach wie ein Kabel sein, das mit einer einzelnen physischen Festplatte verbunden ist, oder so komplex wie ein Storage Area Network. Wenn das Problem durch diese Komponente verursacht wird, können Sie sich an den Hardwarehersteller wenden, um weitere Informationen zur Problembehandlung zu erhalten.

### <a name="disk-queuing"></a>Datenträger Warteschlangen

Es gibt eine begrenzte Menge an e/a-Vorgängen, die ein Datenträger Subsystem zu einem bestimmten Zeitpunkt annehmen kann. Die übermäßige e/a-Vorgänge werden in die Warteschlange eingereiht, bis der Datenträger Die Zeit, die e/a in den Warteschlangen unterhalb der Ebene des Partitions-Managers verbringt, wird in den Leistungsdaten für die Leistung physischer Datenträger berücksichtigt. Wenn Warteschlangen größer werden und die e/a-Vorgänge länger warten müssen, wächst auch die gemessene Latenz.

Unter der Ebene "Partitions-Manager" befinden sich mehrere Warteschlangen wie folgt:

- Warteschlange für Microsoft-Port Treiber-Scsiport oder Storport-Warteschlange

- Vom Hersteller bereitgestellte Gerätetreiber Warteschlange-OEM-Gerätetreiber

- Hardware Warteschlangen – z. b. Warteschlangen für Warteschlangen, SAN-Switches, Warteschlangen für Array Controller und Festplatten Warteschlange

Wir berücksichtigen auch den Zeitpunkt, an dem die Festplatte aktiv die e/a-Vorgänge verarbeitet, und die Reisezeit, die benötigt wird, bis die Anforderung zur Partition Manager-Ebene zurückkehrt, um als abgeschlossen markiert zu werden.

Schließlich müssen wir die Port Treiber Warteschlange (für SCSI-Storport. sys) besonders beachten. Der Port Treiber ist die letzte Microsoft-Komponente zum berühren einer e/a-Verbindung, bevor wir Sie an den vom Hersteller bereitgestellten Geräte-Miniport-Treiber übergeben.

Wenn der Geräte-Miniport-Treiber keine weiteren e/a-Vorgänge akzeptieren kann, weil die Warteschlange oder die darin enthaltenen Hardware Warteschlangen ausgelastet sind, beginnen wir damit, e/a-Vorgänge in der Port Die Größe der Warteschlange des Microsoft-Port Treibers wird nur durch den verfügbaren System Arbeitsspeicher (RAM) beschränkt und kann sehr groß werden. Dies verursacht eine große gemessene Latenz.

## <a name="high-cpu-caused-by-enumerating-folders"></a>Hohe CPU-Anzahl durch Aufzählen von Ordnern 

Um dieses Problem zu beheben, deaktivieren Sie das Feature Access based Enumeration (ABE).

Führen Sie den folgenden PowerShell-Befehl aus, um zu bestimmen, welche SMB-Freigaben von Abe aktiviert sind

```PowerShell
Get-SmbShare | Select Name, FolderEnumerationMode
```

Uneingeschränkt = Abe deaktiviert. <br />
Accessbase = Abe aktiviert.


Sie können Abe in **Server-Manager**aktivieren. Navigieren Sie zu **Datei-und Speicherdienste** > Freigaben, klicken Sie mit der rechten Maustaste auf die **Freigabe, wählen**Sie **Eigenschaften**aus, wechseln Sie zu **Einstellungen** , und wählen Sie dann **Zugriffs basierte Enumeration aktivieren**aus.

![UI-Optionen](media/high-cpu-usage-issue-on-smb-server-2.png)

Außerdem können Sie **abelevel** auf eine niedrigere Ebene verringern (1 oder 2), um die Leistung zu verbessern.

Sie können die Datenträger Leistung überprüfen, wenn die Enumeration langsam ist, indem Sie den Ordner lokal über eine-Konsole oder eine RDP-Sitzung öffnen.
