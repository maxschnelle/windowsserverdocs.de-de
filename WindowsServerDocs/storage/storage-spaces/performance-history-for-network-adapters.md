---
title: Verlauf Netzwerkadapter
ms.author: cosdar
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 02/02/2018
Keywords: Storage Spaces Direct
ms.localizationpriority: medium
ms.openlocfilehash: 340999a8f440975d3736277b1a30dddbb942785d
ms.sourcegitcommit: d31e266130b3b082372f7af4024e6089cb347d74
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/28/2018
ms.locfileid: "4239237"
---
# Verlauf Netzwerkadapter

> Gilt für: Windows Server Insider Preview

Untergeordnete in diesem Thema von ["direkte Speicherplätze" Verlauf](performance-history.md) beschreibt ausführlich der Verlauf für Netzwerkadapter gesammelt. Netzwerk-Adapter Leistungsverlauf ist für alle physischen Netzwerkadapter in jedem Server im Cluster verfügbar. Remote Direct Memory Access (RDMA) Leistungsverlauf ist mit RDMA-fähig für alle physischen Netzwerkadapter verfügbar.

   > [!NOTE]
   > Leistungsverlauf kann nicht für Netzwerkadapter auf einem Server gesammelt werden, die nicht verfügbar ist. Sammlung wird automatisch fortgesetzt, wenn der Server wieder verfügbar ist.

## Seriennamen und Einheiten

Diese Serie werden für alle berechtigten Netzwerkadapter erfasst:

| Serie                               | Einheit            |
|--------------------------------------|-----------------|
| `netadapter.bandwidth.inbound`       | Bits pro Sekunde |
| `netadapter.bandwidth.outbound`      | Bits pro Sekunde |
| `netadapter.bandwidth.total`         | Bits pro Sekunde |
| `netadapter.bandwidth.rdma.inbound`  | Bits pro Sekunde |
| `netadapter.bandwidth.rdma.outbound` | Bits pro Sekunde |
| `netadapter.bandwidth.rdma.total`    | Bits pro Sekunde |

   > [!NOTE]
   > Netzwerk-Adapter Leistungsverlauf wird in **Bits** pro Sekunde, nicht Bytes pro Sekunde aufgezeichnet. Eine 10 GbE-Netzwerkadapter kann senden und Empfangen von ca. 1.000.000.000 Bits = 125,000,000 Bytes = 1,25 GB pro Sekunde am Maximalwert theoretische.

## Zum Interpretieren

| Serie                               | Zum Interpretieren                                                      |
|--------------------------------------|-----------------------------------------------------------------------|
| `netadapter.bandwidth.inbound`       | Die Anzahl der vom Netzwerkadapter empfangenen Daten.                         |
| `netadapter.bandwidth.outbound`      | Die Anzahl der von der Netzwerkadapter gesendet.                             |
| `netadapter.bandwidth.total`         | Gesamtanzahl der Daten empfangen oder der Netzwerkadapter gesendet.           |
| `netadapter.bandwidth.rdma.inbound`  | Die Anzahl der Daten, die über RDMA vom Netzwerkadapter empfangen.               |
| `netadapter.bandwidth.rdma.outbound` | Die Anzahl der Daten, die über RDMA vom Netzwerkadapter gesendet.                   |
| `netadapter.bandwidth.rdma.total`    | Gesamtanzahl der Daten empfangen oder über RDMA vom Netzwerkadapter gesendet. |

## Woher sie kommen

Die `bytes.*` Serie von gesammelt werden die `Network Adapter` Leistungsindikator auf dem Server festgelegt, in dem der Netzwerkadapter installiert ist, eine Instanz pro-Netzwerkadapter.

| Serie                           | Quelle counter           |
|----------------------------------|--------------------------|
| `netadapter.bandwidth.inbound`   | 8 x `Bytes Received/sec` |
| `netadapter.bandwidth.outbound`  | 8 x `Bytes Sent/sec`     |
| `netadapter.bandwidth.total`     | 8 x `Bytes Total/sec`    |

Die `rdma.*` Serie von gesammelt werden die `RDMA Activity` Leistungsindikator auf dem Server festgelegt, in dem der Netzwerkadapter installiert ist, eine Instanz pro Netzwerkadapter mit RDMA aktiviert bzw. deaktiviert.

| Serie                               | Quelle counter           |
|--------------------------------------|--------------------------|
| `netadapter.bandwidth.rdma.inbound`  | 8 x `Inbound bytes/sec`  |
| `netadapter.bandwidth.rdma.outbound` | 8 x `Outbound bytes/sec` |
| `netadapter.bandwidth.rdma.total`    | 8 x *Summe der oben genannten*   |

   > [!NOTE]
   > Leistungsindikatoren werden über das gesamte Intervall nicht gesampelt gemessen. Wenn der Netzwerkadapter für 9 Sekunden aber Übertragungen 200 Bits in der 10. zweiten im Leerlauf ist z. B. seine `netadapter.bandwidth.total` aufgezeichnet als 20 Bits pro Sekunde durchschnittlich während dieses Intervalls 10 Sekunden. Dadurch wird sichergestellt, dessen Leistungsverlauf alle Aktivität erfasst und robust, um Rauschen ist.

## Verwendung in PowerShell

Verwenden Sie das [Get-NetAdapter](https://docs.microsoft.com/powershell/module/netadapter/get-netadapter) -Cmdlet:

```PowerShell
Get-NetAdapter <Name> | Get-ClusterPerf
```

## Weitere Informationen:

- ["Direkte Speicherplätze" Verlauf](performance-history.md)
