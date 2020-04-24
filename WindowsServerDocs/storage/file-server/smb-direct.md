---
title: Optimieren der Leistung von Dateiservern mit SMB Direct
description: Beschreibt das SMB Direct-Feature in Windows Server 2012 R2, Windows Server 2012 und Windows Server 2016.
ms.prod: windows-server
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 04/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 41126aa0d054607449d57928c1777679e5087e73
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2020
ms.locfileid: "71394455"
---
# <a name="smb-direct"></a>SMB Direct

>Gilt für: Windows Server 2012 R2, Windows Server 2012, Windows Server 2016

Windows Server 2012 R2, Windows Server 2012 und Windows Server 2016 beinhalten ein Feature namens „SMB Direct“, das die Verwendung von Netzwerkadaptern mit der Funktion für direkten Remotespeicherzugriff (Remote Direct Memory Access, RDMA) unterstützt. Netzwerkadapter mit RDMA können bei maximaler Geschwindigkeit mit sehr niedriger Latenz arbeiten – und das bei sehr geringer CPU-Nutzung. Für Arbeitsauslastungen wie Hyper-V oder Microsoft SQL Server bedeutet dies, dass ein Remotedateiserver einem lokalen Speicher gleichkommt. %%amp;quot;SMB Direct%%amp;quot; bietet Folgendes:

- Erhöhter Durchsatz: nutzt den gesamten Durchsatz von Hochgeschwindigkeitsnetzwerken, in denen die Netzwerkkarte die Übertragung großer Datenmengen mit Leitungsübertragungsrate koordiniert
- Geringe Latenz: bietet extrem schnelle Antworten auf Netzwerkanforderungen und erweckt demzufolge den Eindruck, dass die Remotespeicherung von Dateien genauso erfolgt wie das Speichern mit einem direkt angeschlossenen Blockspeicher.
- Geringe CPU-Auslastung: verwendet bei der Datenübertragung über das Netzwerk weniger CPU-Zyklen, sodass mehr Leistungsreserven für Serveranwendungen erhalten bleiben.

SMB Direct wird automatisch von Windows Server 2012 R2 und Windows Server 2012 konfiguriert.

## <a name="smb-multichannel-and-smb-direct"></a>%%amp;quot;SMB Multichannel%%amp;quot; und %%amp;quot;SMB Direct%%amp;quot;

Bei %%amp;quot;SMB Multichannel%%amp;quot; handelt es sich um das Feature zum Erkennen der RDMA-Funktion von Netzwerkadaptern, um %%amp;quot;SMB Direct%%amp;quot; zu aktivieren. Ohne %%amp;quot;SMB Multichannel,%%amp;quot; verwendet SMB reguläres TCP/IP für die RDMA-fähigen Netzwerkadapter (alle Netzwerkadapter stellen zusammen mit dem neuen RDMA-Stapel einen TCP/IP-Stapel bereit).

Mit %%amp;quot;SMB Multichannel%%amp;quot; erkennt SMB, ob ein Netzwerkadapter über die RDMA-Funktion verfügt. Anschließend werden mehrere RDMA-Verbindungen für diese eine Sitzung hergestellt (zwei pro Schnittstelle). Dies ermöglicht SMB die Nutzung des hohen Durchsatzes, der geringen Latenz sowie der geringen CPU-Auslastung, die RDMA-fähige Netzwerkadapter bieten können. Das Feature bietet zudem eine Fehlertoleranz, wenn Sie mehrere RDMA-Schnittstellen verwenden.

>[!NOTE]
>Sie sollten RDMA-fähige Netzwerkadapter nicht in Teams zusammenfassen, wenn Sie die RDMA-Funktion der Netzwerkadapter verwenden möchten. Bei einer Zusammenfassung in Teams bieten die Netzwerkadapter keine RDMA-Unterstützung.
>Nachdem mindestens eine RDMA-Netzwerkverbindung erstellt wurde, wird die für die ursprüngliche Protokollverhandlung verwendete TCP/IP-Verbindung nicht mehr verwendet. Für den Fall, dass die RDMA-Netzwerkverbindungen fehlschlagen, wird die TCP/IP-Verbindung jedoch aufrecht erhalten.

## <a name="requirements"></a>Anforderungen

Für %%amp;quot;SMB Direct%%amp;quot; gelten die folgenden Anforderungen:

- Mindestens zwei Computer, auf denen Windows Server 2012 R2 oder Windows Server 2012 ausgeführt wird.
- Ein oder mehrere Netzwerkadapter mit RDMA-Funktion.

### <a name="considerations-when-using-smb-direct"></a>Überlegungen zur Verwendung von %%amp;quot;SMB Direct%%amp;quot;

- Sie können %%amp;quot;SMB Direct%%amp;quot; in einem Failovercluster verwenden. Sie müssen jedoch sicherstellen, dass die für den Clientzugriff verwendeten Clusternetzwerke für %%amp;quot;SMB Direct%%amp;quot; geeignet sind. Die Failover-Clusterunterstützung ermöglicht die Verwendung mehrerer Netzwerke für den Clientzugriff zusammen mit Netzwerkadaptern, die sowohl RSS-fähig (empfangsseitige Skalierung) als auch RDMA-fähig sind.
- Sie können %%amp;quot;SMB Direct%%amp;quot; auf dem Hyper-V-Verwaltungsbetriebssystem verwenden, um Hyper-V über SMB zu unterstützen und um Speicher für einen virtuellen Computer bereitzustellen, für den der Hyper-V-Speicherstapel verwendet wird. RDMA-fähige Netzwerkadapter werden jedoch nicht direkt für einen Hyper-V-Client bereitgestellt. Wenn Sie eine Verbindung zwischen einem RDMA-fähigen Netzwerkadapter und einem virtuellen Switch herstellen, sind die virtuellen Netzwerkadapter des Switches nicht RDMA-fähig.
- Bei einer Deaktivierung von %%amp;quot;SMB Multichannel%%amp;quot; wird auch %%amp;quot;SMB Direct%%amp;quot; deaktiviert. Da %%amp;quot;SMB Multichannel%%amp;quot; Netzwerkadapterfunktionen erkennt und bestimmt, ob ein Netzwerkadapter RDMA-fähig ist, kann %%amp;quot;SMB Direct%%amp;quot; nicht vom Client verwendet werden, wenn %%amp;quot;SMB Multichannel%%amp;quot; deaktiviert ist.
- SMB Direct wird unter Windows RT nicht unterstützt. Für SMB Direct ist Unterstützung RDMA-fähiger Netzwerkadapter erforderlich, die nur unter Windows Server 2012 R2 und Windows Server 2012 verfügbar ist.
- In Vorgängerversionen von Windows Server wird %%amp;quot;SMB Direct%%amp;quot; nicht unterstützt. SMB Direct wird nur unter Windows Server 2012 R2 und Windows Server 2012 unterstützt.

## <a name="enabling-and-disabling-smb-direct"></a>Aktivieren und Deaktivieren von %%amp;quot;SMB Direct%%amp;quot;

SMB Direct ist standardmäßig aktiviert, wenn Windows Server 2012 R2 oder Windows Server 2012 installiert ist. Der SMB-Client erkennt und verwendet automatisch mehrere Netzwerkverbindungen, wenn eine entsprechende Konfiguration identifiziert wird.

### <a name="disable-smb-direct"></a>Deaktivieren von SMB Direct

Normalerweise müssen Sie %%amp;quot;SMB Direct%%amp;quot; nicht deaktivieren. Sie können das Feature jedoch deaktivieren, wenn Sie eines der folgenden Windows PowerShell-Skripts ausführen.

Wenn Sie RDMA für eine spezielle Schnittstelle deaktivieren möchten, geben Sie Folgendes ein:

```PowerShell
Disable-NetAdapterRdma <name>
```

Wenn Sie RDMA für eine alle Schnittstellen deaktivieren möchten, geben Sie Folgendes ein:

```PowerShell
Set-NetOffloadGlobalSetting -NetworkDirect Disabled
```

Wenn Sie RDMA entweder auf dem Client oder auf dem Server deaktivieren, kann RDMA von den Systemen nicht verwendet werden. *Network Direct* ist der interne Name für die grundlegende Netzwerkunterstützung in Windows Server 2012 R2 und Windows Server 2012 für RDMA-Schnittstellen.

### <a name="re-enable-smb-direct"></a>Erneutes Aktivieren von SMB Direct

Nach dem Deaktivieren von RDMA können Sie mithilfe eines der folgenden Windows PowerShell-Skripts eine Reaktivierung ausführen.

Wenn Sie RDMA für eine spezielle Schnittstelle reaktivieren möchten, geben Sie Folgendes ein:

```PowerShell
Enable-NetAdapterRDMA <name>
```

Wenn Sie RDMA für alle Schnittstellen reaktivieren möchten, geben Sie Folgendes ein:

```PowerShell
Set-NetOffloadGlobalSetting -NetworkDirect Enabled
```

Wenn Sie RDMA wieder verwenden möchten, müssen Sie das Feature sowohl auf dem Client als auch auf dem Server aktivieren.

## <a name="test-performance-of-smb-direct"></a>Testen der Leistung von %%amp;quot;SMB Direct%%amp;quot;

Mithilfe eines der folgenden Verfahren können Sie die Leistung testen.

### <a name="compare-a-file-copy-with-and-without-using-smb-direct"></a>Vergleichen einer Dateikopie mit und ohne Verwendung von %%amp;quot;SMB Direct%%amp;quot;

So messen Sie den erhöhten Durchsatz von SMB Direct:

1. Konfigurieren von %%amp;quot;SMB Direct%%amp;quot;
2. Messen Sie die Zeit, die zum Ausführen einer umfangreichen Dateikopie mit %%amp;quot;SMB Direct%%amp;quot; erforderlich ist.
3. Deaktivieren Sie RDMA auf dem Netzwerkadapter, siehe [Enabling and disabling SMB Direct](#enabling-and-disabling-smb-direct).
4. Messen Sie die Zeit, die zum Ausführen einer umfangreichen Dateikopie ohne %%amp;quot;SMB Direct%%amp;quot; erforderlich ist.
5. Reaktivieren Sie RDMA auf dem Netzwerkadapter, und vergleichen Sie dann die beiden Ergebnisse.
6. Wenn Sie die Auswirkungen der Zwischenspeicherung vermeiden möchten, sollten Sie die folgenden Schritte ausführen:
    1. Kopieren Sie eine große Datenmenge (mehr Daten, als der Arbeitsspeicher verarbeiten kann).
    2. Kopieren Sie die Daten zweimal. Nutzen Sie dabei die erste Kopie als Übung, und messen Sie dann beim zweiten Kopiervorgang die Zeit.
    3. Starten Sie den Server und den Client vor jedem Test neu, um sicherzustellen, dass gleiche Bedingungen vorherrschen.

### <a name="fail-one-of-multiple-network-adapters-during-a-file-copy-with-smb-direct"></a>Simulieren eines Fehlers für einen von mehreren Netzwerkadaptern während eines Dateikopiervorgangs mit %%amp;quot;SMB Direct%%amp;quot;

So überprüfen Sie die Failoverfunktion von SMB Direct:

1. Stellen Sie sicher, dass %%amp;quot;SMB Direct%%amp;quot; in einer Konfiguration mit mehreren Netzwerkadaptern funktioniert.
2. Führen Sie einen umfangreichen Dateikopiervorgang aus. Simulieren Sie während der Ausführung des Kopiervorgangs einen Fehler für einen der Netzwerkpfade, indem Sie eines der Kabel trennen (dazu können Sie auch einen der Netzwerkadapter trennen).
3. Stellen Sie mithilfe eines anderen Netzwerkadapters sicher, dass der Dateikopiervorgang fortgesetzt wird und dass beim Dateikopiervorgang keine Fehler auftreten.

>[!NOTE]
>Stellen Sie zum Vermeiden von Fehlern für eine Arbeitsauslastung, für die %%amp;quot;SMB Direct%%amp;quot; nicht verwendet wird, sicher, dass der getrennte Netzwerkpfad von keiner anderen Arbeitsauslastung verwendet wird.

## <a name="more-information"></a>Weitere Informationen

- [Server Message Block (Übersicht)](file-server-smb-overview.md)
- [Erhöhen der Server-, Speicher- und Netzwerkverfügbarkeit: Szenarioübersicht](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831437(v%3dws.11)>)
- [Bereitstellen von Hyper-V über SMB](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj134187(v%3dws.11)>)
