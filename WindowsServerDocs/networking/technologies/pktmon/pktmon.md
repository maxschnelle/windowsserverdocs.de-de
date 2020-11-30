---
title: Paketüberwachung (Pktmon)
description: Dieses Thema enthält eine Übersicht über das Netzwerk Diagnosetool Paket Monitor (pktmon).
ms.topic: overview
author: khdownie
ms.author: v-kedow
ms.date: 11/12/2020
ms.openlocfilehash: cab9de79c1d53b505acb61020c71472365ded348
ms.sourcegitcommit: 3181fcb69a368f38e0d66002e8bc6fd9628b1acc
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/30/2020
ms.locfileid: "96330492"
---
# <a name="packet-monitor-pktmon"></a>Paket Monitor- \( pktmon\)

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows 10, Azure Stack HCI, Azure Stack Hub, Azure

Der Paket Monitor (pktmon) ist ein Komponenten übergreifendes Netzwerk Diagnosetool für Windows. Sie kann für die Paket Erfassung, die Paket Ablage Erkennung, das Filtern und zählen von Paketen verwendet werden. Das Tool ist besonders bei Virtualisierungsszenarien hilfreich, z. b. bei Container Netzwerken und Sdn, da es im Netzwerk Stapel sichtbar ist. Es ist in-Box über den Befehl pktmon.exe und über Erweiterungen des Windows Admin Centers verfügbar. 

## <a name="overview"></a>Übersicht

Jeder Computer, der über das Netzwerk kommuniziert, verfügt über mindestens einen Netzwerkadapter. Alle Komponenten zwischen diesem Adapter und einer Anwendung bilden einen Netzwerk Stapel: einen Satz von Netzwerkkomponenten, die Netzwerk Datenverkehr verarbeiten und verschieben. In herkömmlichen Szenarien ist der Netzwerk Stapel klein, und das gesamte Paket Routing und der Wechsel erfolgt auf externen Geräten.

<center>

:::image type="content" source="media/networking-stack.png" alt-text="Netzwerk Stapel in herkömmlichen Szenarien" border="false":::

</center>

Bei der Einführung der Netzwerkvirtualisierung hat sich die Größe des Netzwerk Stapels jedoch multipliziert. Dieser erweiterte Netzwerk Stapel enthält jetzt Komponenten wie den virtuellen Switch, die die Paketverarbeitung und den Wechsel verarbeiten. Eine solche flexible Umgebung ermöglicht eine viel bessere Ressourcennutzung und Sicherheits Isolation, aber auch mehr Platz für Konfigurationsfehler, die sich nur schwer diagnostizieren lassen. Der Paket Monitor bietet einen verbesserten Einblick in den Netzwerk Stapel, der häufig benötigt wird, um diese Fehler zu ermitteln.

<center>

:::image type="content" source="media/packet-capture.png" alt-text="Komponenten übergreifende Paket Erfassung in packetmon" border="false":::

</center>

Der Paket Monitor fängt Pakete an mehreren Speicherorten im Netzwerk Stapel ab und macht die Paket Route verfügbar. Wenn ein Paket von einer unterstützten Komponente im Netzwerk Stapel abgelegt wurde, meldet der Paket Monitor das Löschen des Pakets. Dies ermöglicht es Benutzern, eine Komponente zu unterscheiden, die das beabsichtigte Ziel für ein Paket ist, und eine Komponente, die ein Paket beeinträchtigt. Außerdem meldet der Paket Monitor Drop-Gründe. z. b. "MTU mistmatch" oder "gefiltertes VLAN" usw. Diese Ablage Gründe stellen die Grundursache für das Problem dar, ohne dass alle Möglichkeiten ausgeschöpft werden müssen. Der Paket Monitor stellt auch Paket Zähler für jeden Abfang Punkt bereit und ermöglicht eine Überprüfung auf einem übergeordneten Paketfluss, ohne dass zeitaufwändige Protokoll Analysen erforderlich sind.

<center>

:::image type="content" source="media/drop-detection.png" alt-text="Drop-Erkennung von packetmon" border="false":::

</center>

## <a name="best-practices"></a>Bewährte Methoden

Verwenden Sie diese bewährten Methoden, um die Netzwerkanalyse zu optimieren.

- Überprüfen Sie die Befehlszeilen Hilfe für Argumente und Funktionen (z. b. pktmon-Starthilfe).
- Konfigurieren von Paket Filtern, die Ihrem Szenario entsprechen (pktmon-Filter hinzufügen).
- Überprüfen Sie die Paket Zähler während des Experiments für die allgemeine Ansicht (pktmon-Indikatoren).
- Sehen Sie sich das Protokoll für eine ausführliche Analyse (pktmon-Format pktmon. ETL) an.

## <a name="functionality"></a>Funktionalität

Die Funktionalität des Paket Monitors wurde durch Windows-Releases weiterentwickelt. In der folgenden Tabelle werden die Hauptfunktionen und die zugehörige Windows-Version angezeigt.

| Funktion                                                                  | V 1809 (b:17763) | V 1903 (b:18362) | V 2004 (b:19041) |
|:---------------------------------------------------------------------------:|:----------------:|:----------------:|:----------------:|
| Paket Überwachung und-Zählung an mehreren Standorten entlang des Netzwerk Stapels | &#x2611;         | &#x2611;         | &#x2611;         |
| Löschen von Paketen an mehreren Stapel Standorten                          | &#x2611;         | &#x2611;         | &#x2611;         |
| Flexibles Filtern von Lauf Zeit Paketen                                           | &#x2611;         | &#x2611;         | &#x2611;         |
| Kapselungs Unterstützung                                                       | &#x2610;         | &#x2611;         | &#x2611;         |
| Netzwerkanalyse basierend auf der tcpdump-Paket Analyse                            | &#x2610;         | &#x2611;         | &#x2611;         |
| OOB-Analyse (Packet Metadata)                                              | &#x2610;         | &#x2610;         | &#x2611;         |
| Echtzeitüberwachung auf dem Bildschirm                                       | &#x2610;         | &#x2610;         | &#x2611;         |
| Hohe Protokollierung im Arbeitsspeicher                                               | &#x2610;         | &#x2610;         | &#x2611;         |
| Unterstützung für wireshark und Netzwerkmonitor-Format                                | &#x2610;         | &#x2610;         | &#x2611;         |

>[!NOTE]
>Azure Stack HCI-und Azure Stack Hub-Kunden sollten die vibrianium-Funktionalität erwarten.

## <a name="limitations"></a>Einschränkungen

Im folgenden finden Sie einige der wichtigsten Einschränkungen des Paket Monitors.

- Derzeit wird nur Ethernet-Datenverkehr unterstützt. Unterstützung für drahtlosen Datenverkehr wird in späteren Versionen hinzugefügt.
- Paket Abstürze von der Windows-Firewall sind noch nicht über den Paket Monitor sichtbar. 

## <a name="get-started-with-packet-monitor"></a>Einstieg in den Paket Monitor

Die folgenden Ressourcen sind verfügbar, um Sie bei den ersten Schritten mit der Paket Überwachung zu unterstützen.

### <a name="pktmon-command-syntax-and-formatting"></a>[Pktmon-Befehlssyntax und -formatierung](pktmon-syntax.md)

Der Paket Monitor ist in-Box über pktmon.exe Befehl auf dem vibrianium-Betriebssystem (Build 19041) verfügbar. Sie können [dieses Thema verwenden](pktmon-syntax.md) , um zu erfahren, wie Sie die Syntax, Befehle, Formatierung und Ausgabe von pktmon verstehen.

### <a name="packet-monitoring-extension-in-windows-admin-center"></a>[Paketüberwachungserweiterung im Windows Admin Center](pktmon-wac-extension.md)

Die Paket Überwachungs Erweiterung ermöglicht es Ihnen, den Paket Monitor über das Windows Admin Center zu betreiben und zu nutzen. Die Erweiterung unterstützt Sie bei der Diagnose Ihres Netzwerks durch erfassen und Anzeigen von Netzwerk Datenverkehr über den Netzwerk Stapel in einem Protokoll, das leicht zu befolgen und zu bearbeiten ist. In [diesem Thema](pktmon-wac-extension.md) erfahren Sie, wie Sie das Tool verwenden und seine Ausgabe verstehen.

### <a name="sdn-data-path-diagnostics-extension-in-windows-admin-center"></a>[SDN-Datenpfad-diagnoseerweiterung im Windows Admin Center](pktmon-sdn-data-path-wac-extension.md)

Die Sdn-Daten Pfad Diagnose ist ein Tool innerhalb der Sdn-Überwachungs Erweiterung von Windows Admin Center. Das Tool automatisiert Paket Erfassungs basierte Paket Erfassungen gemäß verschiedenen Sdn-Szenarien und zeigt die Ausgabe in einer einzelnen Ansicht an, die einfach zu befolgen und zu bearbeiten ist. In [diesem Thema](pktmon-sdn-data-path-wac-extension.md) erfahren Sie, wie Sie das Tool verwenden und seine Ausgabe verstehen.

### <a name="microsoft-network-monitor-netmon-support"></a>[Unterstützung für Microsoft Netzwerkmonitor (Netmon)](pktmon-netmon-support.md)

Der Paket Monitor generiert Protokolle im ETL-Format. Diese Protokolle können mithilfe von Microsoft-Netzwerkmonitor (NetMon) mithilfe spezieller Parser analysiert werden. In [diesem Thema](pktmon-netmon-support.md) wird erläutert, wie die vom Paket Monitor generierten ETL-Dateien in Netmon analysiert werden.

### <a name="wireshark-pcapng-format-support"></a>[Unterstützung für Wireshark (pcapng-Format)](pktmon-pcapng-support.md)

Der Paket Monitor kann Protokolle in das pcapng-Format konvertieren. Diese Protokolle können mithilfe von Wireshark (oder einem beliebigen pcapng Analyzer) analysiert werden. In [diesem Thema](pktmon-pcapng-support.md) wird die erwartete Ausgabe und deren Nutzung erläutert.

## <a name="provide-feedback-to-engineering-team"></a>Feedback an das Engineering-Team senden

Melden Sie alle Fehler, oder senden Sie Feedback über den Feedback-Hub, indem Sie die folgenden Schritte ausführen:

1. Starten Sie den  **Feedback-Hub**   über das **Startmenü** .

1. Wählen Sie entweder die Schaltfläche " **Problem melden** " oder die Schaltfläche " **Feature vorschlagen** " aus.

1. Geben Sie einen aussagekräftigen Feedback Titel im Feld zusammen **fassen Ihres Problems** ein   .

1. Geben Sie im Feld **Geben Sie weitere** Details Details und Schritte zum Reproduzieren des Problems an   .

1. Wählen Sie als obere Kategorie  **Netzwerk und Internet und**   dann als Unterkategorie **Paket Monitor (pktmon.exe)** aus.

1. Um uns bei der schnelleren Identifizierung und Behebung des Fehlers zu unterstützen, erfassen Sie Screenshots, fügen Sie das Ausgabeprotokoll von pktmons an, und/oder erstellen Sie das Problem erneut.

1. Klicken Sie auf **senden**.

Nach der Übermittlung des Feedbacks/Fehlers kann das Engineering-Team sich das Feedback ansehen und es beheben.
