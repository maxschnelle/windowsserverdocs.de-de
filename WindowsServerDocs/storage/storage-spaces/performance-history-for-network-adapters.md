---
title: Leistungs Verlauf für Netzwerkadapter
ms.author: cosdar
manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 02/02/2018
ms.localizationpriority: medium
ms.openlocfilehash: e2379ce540cb26c02bc79f591d2a597874ab287c
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80856213"
---
# <a name="performance-history-for-network-adapters"></a>Leistungs Verlauf für Netzwerkadapter

> Gilt für: Windows Server 2019

In diesem Unterthema des [Leistungs Verlaufs für direkte Speicherplätze](performance-history.md) wird der Leistungs Verlauf ausführlich beschrieben, der für Netzwerkadapter erfasst wurde. Der Leistungs Verlauf für Netzwerkadapter ist für jeden physischen Netzwerkadapter auf jedem Server im Cluster verfügbar. Der RDMA (Remote Direct Memory Access)-Leistungs Verlauf ist für jeden physischen Netzwerkadapter mit aktiviertem RDMA verfügbar.

   > [!NOTE]
   > Der Leistungs Verlauf kann für Netzwerkadapter auf einem nicht herunter zufügenden Server nicht erfasst werden. Die Sammlung wird automatisch fortgesetzt, wenn der Server wieder verfügbar ist.

## <a name="series-names-and-units"></a>Reihen Namen und Einheiten

Diese Reihen werden für jeden berechtigten Netzwerkadapter erfasst:

| Reihe                               | Einheit            |
|--------------------------------------|-----------------|
| `netadapter.bandwidth.inbound`       | Bits pro Sekunde |
| `netadapter.bandwidth.outbound`      | Bits pro Sekunde |
| `netadapter.bandwidth.total`         | Bits pro Sekunde |
| `netadapter.bandwidth.rdma.inbound`  | Bits pro Sekunde |
| `netadapter.bandwidth.rdma.outbound` | Bits pro Sekunde |
| `netadapter.bandwidth.rdma.total`    | Bits pro Sekunde |

   > [!NOTE]
   > Der Leistungs Verlauf für Netzwerkadapter wird in **Bits** pro Sekunde aufgezeichnet, nicht in Bytes pro Sekunde. 1 10 der GbE-Netzwerkadapter kann ungefähr 1 Milliarde Bits = 125 Millionen Bytes = 1,25 GB pro Sekunde an das theoretische Maximum senden und empfangen.

## <a name="how-to-interpret"></a>Interpretieren

| Reihe                               | Interpretieren                                                      |
|--------------------------------------|-----------------------------------------------------------------------|
| `netadapter.bandwidth.inbound`       | Rate der vom Netzwerkadapter empfangenen Daten.                         |
| `netadapter.bandwidth.outbound`      | Rate der vom Netzwerkadapter gesendeten Daten.                             |
| `netadapter.bandwidth.total`         | Die Gesamtrate der vom Netzwerkadapter empfangenen oder gesendeten Daten.           |
| `netadapter.bandwidth.rdma.inbound`  | Rate der Daten, die über RDMA vom Netzwerkadapter empfangen werden.               |
| `netadapter.bandwidth.rdma.outbound` | Rate der über RDMA vom Netzwerkadapter gesendeten Daten.                   |
| `netadapter.bandwidth.rdma.total`    | Gesamtrate der vom Netzwerkadapter über RDMA empfangenen oder gesendeten Daten. |

## <a name="where-they-come-from"></a>Woher Sie stammen

Die `bytes.*` Reihe wird auf dem Server, auf dem der Netzwerkadapter installiert ist, auf dem Server, auf dem der Netzwerkadapter installiert ist, und einer Instanz pro Netzwerkadapter `Network Adapter` erfasst.

| Reihe                           | Quellen Counter           |
|----------------------------------|--------------------------|
| `netadapter.bandwidth.inbound`   | 8 × `Bytes Received/sec` |
| `netadapter.bandwidth.outbound`  | 8 × `Bytes Sent/sec`     |
| `netadapter.bandwidth.total`     | 8 × `Bytes Total/sec`    |

Die `rdma.*` Reihe wird auf dem Server, auf dem der Netzwerkadapter installiert ist, auf dem Server, auf dem der Netzwerkadapter installiert ist, und einer Instanz pro Netzwerkadapter mit aktiviertem RDMA `RDMA Activity` gesammelt.

| Reihe                               | Quellen Counter           |
|--------------------------------------|--------------------------|
| `netadapter.bandwidth.rdma.inbound`  | 8 × `Inbound bytes/sec`  |
| `netadapter.bandwidth.rdma.outbound` | 8 × `Outbound bytes/sec` |
| `netadapter.bandwidth.rdma.total`    | 8 × *Summe der oben genannten*   |

   > [!NOTE]
   > Leistungsindikatoren werden über das gesamte Intervall gemessen, nicht als Stichprobe. Wenn sich der Netzwerkadapter z. b. für 9 Sekunden im Leerlauf befindet, aber 200 Bits in der 10. Sekunde überträgt, wird sein `netadapter.bandwidth.total` im Durchschnitt in diesem 10-Sekunden-Intervall als 20 Bits pro Sekunde aufgezeichnet. Dadurch wird sichergestellt, dass der Leistungs Verlauf alle Aktivitäten erfasst und stabil ist.

## <a name="usage-in-powershell"></a>Verwendung in PowerShell

Verwenden Sie das Cmdlet " [Get-netadapter](https://docs.microsoft.com/powershell/module/netadapter/get-netadapter) ":

```PowerShell
Get-NetAdapter <Name> | Get-ClusterPerf
```

## <a name="see-also"></a>Siehe auch

- [Leistungs Verlauf für direkte Speicherplätze](performance-history.md)
