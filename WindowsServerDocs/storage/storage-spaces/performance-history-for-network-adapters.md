---
title: Leistungsverlauf für Netzwerkadapter
ms.author: cosdar
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 02/02/2018
Keywords: Direkte Speicherplätze
ms.localizationpriority: medium
ms.openlocfilehash: 340999a8f440975d3736277b1a30dddbb942785d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59849981"
---
# <a name="performance-history-for-network-adapters"></a>Leistungsverlauf für Netzwerkadapter

> Gilt für: Windows Server-Insider – Vorschau

Dieser Unterabschnitt von [– Leistungsverlauf für "direkte Speicherplätze"](performance-history.md) beschreibt ausführlich den Leistungsverlauf für Netzwerkadapter erfasst. Leistungsverlauf für Netzwerkadapter wird für jede physische Netzwerkkarte auf jedem Server im Cluster verfügbar. Leistungsverlauf für Remote Direct Memory Access (RDMA) steht für alle physischen Netzwerkadapter mit RDMA-fähigen zur Verfügung.

   > [!NOTE]
   > Leistungsverlauf für kann nicht für die Netzwerkadapter auf einem Server gesammelt werden, die nicht verfügbar ist. Sammlung wird automatisch fortgesetzt, wenn der Server wieder verfügbar ist.

## <a name="series-names-and-units"></a>Namen von Datenreihen und Einheiten

Dieser Reihe werden für alle berechtigten Netzwerkadapter gesammelt:

| Serie                               | Einheit            |
|--------------------------------------|-----------------|
| `netadapter.bandwidth.inbound`       | Bits pro Sekunde |
| `netadapter.bandwidth.outbound`      | Bits pro Sekunde |
| `netadapter.bandwidth.total`         | Bits pro Sekunde |
| `netadapter.bandwidth.rdma.inbound`  | Bits pro Sekunde |
| `netadapter.bandwidth.rdma.outbound` | Bits pro Sekunde |
| `netadapter.bandwidth.rdma.total`    | Bits pro Sekunde |

   > [!NOTE]
   > Leistungsverlauf für Netzwerkadapter wird im aufgezeichnet **Bits** pro Sekunde, anstelle von Bytes pro Sekunde. Eine 10-GbE-Netzwerkadapter senden und empfangen ungefähr 1.000.000.000 Bits = 125,000,000 Bytes = 1,25 GB pro Sekunde und die theoretischen Maximum.

## <a name="how-to-interpret"></a>Gewusst wie: interpretieren

| Serie                               | Gewusst wie: interpretieren                                                      |
|--------------------------------------|-----------------------------------------------------------------------|
| `netadapter.bandwidth.inbound`       | Rate der vom Netzwerkadapter empfangenen Daten.                         |
| `netadapter.bandwidth.outbound`      | Rate der vom Netzwerkadapter gesendeten Daten.                             |
| `netadapter.bandwidth.total`         | Gesamtrate Daten empfangen, oder es vom Netzwerkadapter gesendet.           |
| `netadapter.bandwidth.rdma.inbound`  | Rate der Daten, die über RDMA vom Netzwerkadapter empfangen.               |
| `netadapter.bandwidth.rdma.outbound` | Rate der Daten, die über RDMA vom Netzwerkadapter gesendet.                   |
| `netadapter.bandwidth.rdma.total`    | Gesamtrate Daten empfangen oder gesendet, die über RDMA vom Netzwerkadapter. |

## <a name="where-they-come-from"></a>Wo diese herkommen

Die `bytes.*` Reihe werden gesammelt, aus der `Network Adapter` Leistungsindikator auf dem Server festgelegt werden, auf dem der Netzwerkadapter installiert ist, eine Instanz pro Netzwerkadapter.

| Serie                           | Source-Indikator           |
|----------------------------------|--------------------------|
| `netadapter.bandwidth.inbound`   | 8 × `Bytes Received/sec` |
| `netadapter.bandwidth.outbound`  | 8 × `Bytes Sent/sec`     |
| `netadapter.bandwidth.total`     | 8 × `Bytes Total/sec`    |

Der `rdma.*` Reihe werden gesammelt, aus der `RDMA Activity` Leistungsindikator auf dem Server festgelegt werden, auf dem der Netzwerkadapter installiert ist, eine Instanz pro Netzwerkadapter mit RDMA-fähig.

| Serie                               | Source-Indikator           |
|--------------------------------------|--------------------------|
| `netadapter.bandwidth.rdma.inbound`  | 8 × `Inbound bytes/sec`  |
| `netadapter.bandwidth.rdma.outbound` | 8 × `Outbound bytes/sec` |
| `netadapter.bandwidth.rdma.total`    | 8 x *Summe der oben genannten*   |

   > [!NOTE]
   > Leistungsindikatoren werden anhand des gesamten Intervalls, nicht entnommen gemessen. Wenn der Netzwerkadapter für 9 Sekunden aber 200 Bits-Übertragungen im zweiten 10. im Leerlauf ist z. B. die `netadapter.bandwidth.total` aufgezeichnet werden als 20 Bits pro Sekunde durchschnittliche Intervall 10 Sekunden. Dadurch wird der Leistungsverlauf erfasst alle Aktivitäten und ist stabil, um Rauschen.

## <a name="usage-in-powershell"></a>Verwendung in PowerShell

Verwenden der [Get-NetAdapter](https://docs.microsoft.com/powershell/module/netadapter/get-netadapter) Cmdlet:

```PowerShell
Get-NetAdapter <Name> | Get-ClusterPerf
```

## <a name="see-also"></a>Siehe auch

- [Leistungsverlauf für "direkte Speicherplätze"](performance-history.md)
