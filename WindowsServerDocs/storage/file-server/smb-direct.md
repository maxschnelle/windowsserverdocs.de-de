---
title: Verbessern der Leistung eines Dateiservers mit SMB Direct
description: Beschreibt das SMB Direct-Feature in Windows Server 2012 R2, Windows Server 2012 und Windows Server 2016.
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 04/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: ed8fd5b4114fc9fd9c7dc278a98cea8cc67a8749
ms.sourcegitcommit: d31e266130b3b082372f7af4024e6089cb347d74
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/28/2018
ms.locfileid: "4239227"
---
# SMB Direct

>Gilt für: Windows Server 2012 R2, WindowsServer 2012, WindowsServer 2016

Windows Server 2012 R2, Windows Server 2012 und Windows Server 2016 enthalten eine Funktion namens SMB Direct, das die Verwendung der Netzwerkadapter unterstützt, die Remote Direct Memory Access (RDMA)-Funktion haben. Netzwerkadapter, die über RDMA verfügen können bei voller Geschwindigkeit mit sehr geringer Latenz bei der Verwendung von nur sehr wenig CPU fungieren. Für Workloads z. B. Hyper-V- oder Microsoft SQL Server ermöglicht dies einem Remotedateiserver, die den lokalen Speicher ähnelt. SMB Direct stehen zur Verfügung:

- Eine höhere Durchsatz: nutzt den vollständige Durchsatz mit hoher Geschwindigkeit Netzwerke Netzwerkadapter, in denen die Übertragung großer Mengen von Daten auf Geschwindigkeit koordinieren.
- Niedrige Latenz: bietet äußerst schnelle Antworten auf Netzwerkanfragen und, daher wird remote-Datei-Speicher aussehen, als ob es direkt angeschlossene Blockspeicher ist.
- Niedrig CPU-Auslastung: verwendet weniger CPU-Zyklen beim Einschalten, Daten über das Netzwerk, die verlässt für serveranwendungen verfügbar.

SMB Direct wird automatisch von Windows Server 2012 R2 und Windows Server 2012 konfiguriert.

## SMB Multichannel und SMB Direct

SMB Multichannel ist das Feature zum Erkennen von RDMA-Funktionen der Netzwerkadapter zum Aktivieren von SMB Direct verantwortlich. Ohne SMB Multichannel verwendet SMB regulären TCP/IP mit der RDMA-fähigen Netzwerkkarten (alle Netzwerkadapter bieten einen TCP/IP-Stapel zusammen mit dem neuen RDMA-Stapel).

Mit SMB Multichannel erkennt SMB, ob ein Adapter die RDMA-Funktion, und dann mehrere RDMA-Verbindungen für die einzelnen Sitzung (zwei pro Schnittstelle erstellt). Dadurch können SMB verwenden, den mit hohem Durchsatz, geringe Latenz und niedrigen CPU-Auslastung von RDMA-fähigen Netzwerkkarten angeboten. Es bietet außerdem Fehlertoleranz, wenn Sie mehrere RDMA-Schnittstellen verwenden.

>[!NOTE]
>Sie sollten nicht RDMA-fähigen Netzwerkkarten team, wenn Sie beabsichtigen, die RDMA-Funktion der Netzwerkadapter verwenden. Wenn hat, werden die Netzwerkadapter RDMA nicht unterstützt.
>Nachdem mindestens eine Verbindung von RDMA-Netzwerk erstellt wurde, ist die TCP/IP-Verbindung für die ursprüngliche Protokollaushandlung verwendet nicht mehr verwendet. Die TCP/IP-Verbindung wird jedoch beibehalten, für den Fall, dass Sie die RDMA-Netzwerkverbindungen fehl.

## Anforderungen

SMB Direct ist Folgendes erforderlich:

- Mindestens zwei Computern unter Windows Server 2012 R2 oder Windows Server 2012
- Eine oder mehrere Netzwerkadapter mit RDMA-Funktion.

### Überlegungen zur Verwendung von SMB Direct

- Sie können in einem Failovercluster SMB Direct verwenden. Allerdings müssen Sie sicherstellen, dass die Clusternetzwerke, die für den Clientzugriff verwendet für SMB Direct geeignet sind. Failover-Clusterunterstützung unterstützt die Verwendung von mehreren Netzwerken für den Clientzugriff zusammen mit Netzwerkadapter, sind (Receive Side Scaling) RSS-fähig und RDMA-fähig.
- Sie können SMB Direct auf dem Hyper-V-Management-Betriebssystem für die Unterstützung von Hyper-V über SMB und Speicher auf einem virtuellen Computer bereitstellen, die den Hyper-V-Speicherstapel verwendet. RDMA-fähigen Netzwerkkarten sind jedoch nicht direkt auf einen Hyper-V-Client verfügbar. Wenn Sie einen RDMA-fähigen Netzwerkadapter mit einem virtuellen Switch verbinden, kann die virtuellen Netzwerkadapter des Switches nicht RDMA-fähig.
- Wenn Sie SMB Multichannel deaktivieren, wird ebenfalls SMB Direct deaktiviert. Da SMB Multichannel-Adapter Netzwerkfunktionen erkennt und bestimmt, ob ein Netzwerkadapter RDMA-fähig ist, kann nicht SMB Direct vom Client verwendet werden, wenn SMB Multichannel deaktiviert ist.
- SMB Direct wird nicht auf Windows RT zum Download zur unterstützt SMB Direct erfordert die Unterstützung für RDMA-fähigen Netzwerkkarten, die nur auf Windows Server 2012 R2 und Windows Server 2012 verfügbar ist.
- SMB Direct wird nicht auf älteren Versionen von Windows Server unterstützt. Es wird nur unter Windows Server 2012 R2 und Windows Server 2012 unterstützt.

## Aktivieren und Deaktivieren von SMB Direct

SMB Direct ist standardmäßig aktiviert, wenn Windows Server 2012 R2 oder Windows Server 2012 installiert ist. Der SMB-Client erkennt und mehrere Netzwerkverbindungen verwendet, wenn eine entsprechende Konfiguration identifiziert wird.

### SMB Direct deaktivieren

In der Regel müssen Sie nicht SMB Direct zu deaktivieren, Sie können jedoch deaktivieren sie durch die Ausführung eines der folgenden Windows PowerShell-Skripts.

Um RDMA für eine bestimmte Schnittstelle zu deaktivieren, geben Sie Folgendes ein:

```PowerShell
Disable-NetAdapterRdma <name>
```

Um RDMA für alle Schnittstellen zu deaktivieren, geben Sie Folgendes ein:

```PowerShell
Set-NetOffloadGlobalSetting -NetworkDirect Disabled
```

Wenn Sie RDMA auf dem Client oder Server deaktivieren, Verwendung die Systeme ist nicht möglich. *Netzwerk-Direct* ist der interne Name für Windows Server 2012 R2 und Windows Server 2012 grundlegende Netzwerk Unterstützung für RDMA-Schnittstellen.

### SMB Direct erneut zu aktivieren

Nach dem Deaktivieren RDMA, können Sie ihn wieder aktivieren durch die Ausführung eines der folgenden Windows PowerShell-Skripts.

Um RDMA für eine bestimmte Schnittstelle wieder zu aktivieren, geben Sie Folgendes ein:

```PowerShell
Enable-NetAdapterRDMA <name>
```

Um RDMA für alle Schnittstellen erneut zu aktivieren, geben Sie Folgendes ein:

```PowerShell
Set-NetOffloadGlobalSetting -NetworkDirect Enabled
```

Sie müssen so aktivieren Sie RDMA auf dem Client und dem Server starten Sie es erneut zu verwenden.

## Testen Sie die Leistung von SMB Direct

Sie können testen, wie die Leistung arbeitet, indem Sie eine der folgenden Verfahren.

### Vergleichen Sie kopieren mit und ohne Verwendung von SMB Direct

Hier ist den höheren Durchsatz von SMB Direct zu messen:

1. Konfigurieren von SMB Direct
2. Messen Sie die Zeitspanne für eine große Dateikopie mit SMB Direct ausführen.
3. Deaktivieren Sie RDMA auf dem Netzwerkadapter, finden Sie unter [Aktivieren und Deaktivieren von SMB Direct](#enabling-and-disabling-smb-direct).
4. Messen Sie die Zeitspanne, eine große Dateikopie ohne mit SMB Direct auszuführen.
5. Aktivieren Sie RDMA erneut auf den Netzwerkadapter, und vergleichen Sie die beiden Ergebnisse.
6. Um die Auswirkung des Zwischenspeicherns zu vermeiden, sollten Sie die folgenden Schritte ausführen:
    1. Kopieren Sie eine große Menge an Daten (mehr Daten als Speicher in der Lage ist).
    2. Kopieren Sie die Daten zweimal mit der ersten Kopie als Praxis und dann die zweite Kopie timing.
    3. Starten Sie den Server und den Client vor jedem Test, um sicherzustellen, dass sie ähnliche Bedingungen ausgeführt werden.

### Eine mehrerer Netzwerkkarten während eine Dateikopie mit SMB Direct fehl

Hier ist die Failover-Funktion von SMB Direct zu überprüfen:

1. Stellen Sie sicher, dass SMB Direct in einer Konfiguration mit mehreren Netzwerkkarten funktioniert.
2. Führen Sie eine große Datei kopieren. Während das Kopieren ausgeführt wird, einen Fehler bei einer der Netzwerkpfade zu simulieren von Trennen einer Kabel (oder indem Sie eine der Netzwerkadapter deaktivieren).
3. Stellen Sie sicher, dass das Kopieren der Dateien weiterhin mit einer der verbleibenden Netzwerkadapter, und es gibt keine Kopieren der Dateifehler.

>[!NOTE]
>Zur Vermeidung von Fehlern bei einer Workload, die keine SMB Direct verwendet, stellen Sie sicher, dass keine andere Workloads, die mit dem Netzwerk unterbrochen Pfad.

## Weitere Informationen

- [Server Message Block (Übersicht)](file-server-smb-overview.md)
- [Steigerung der Server, Speicher und Netzwerkverfügbarkeit: Scenario Overview](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831437(v%3dws.11)>)
- [Bereitstellen von Hyper-V über SMB](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj134187(v%3dws.11)>)
