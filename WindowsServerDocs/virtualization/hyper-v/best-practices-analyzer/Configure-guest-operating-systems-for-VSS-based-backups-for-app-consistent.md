---
title: Konfigurieren von Gastbetriebssystemen für VSS-basierte Sicherungen zum Aktivieren von Anwendungs konsistenten Momentaufnahmen für Hyper-V-Replikate
description: Online Version des Texts für diese Best Practices Analyzer Regel.
manager: dongill
ms.author: kathydav
ms.topic: article
ms.assetid: 7638e996-d42d-47b8-a670-1e09e7183850
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 5270584b6213ad59ef43c378e5aa7a5dbcc30a4e
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87939104"
---
# <a name="configure-guest-operating-systems-for-vss-based-backups-to-enable-application-consistent-snapshots-for-hyper-v-replica"></a>Konfigurieren von Gastbetriebssystemen für VSS-basierte Sicherungen zum Aktivieren von Anwendungs konsistenten Momentaufnahmen für Hyper-V-Replikate

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Scans finden Sie unter [Ausführen von Best Practices Analyzer-Scans und Verwalten der Scanergebnisse](https://go.microsoft.com/fwlink/p/?LinkID=223177).

|Eigenschaft|Details|
|-|-|
|**Betriebssystem**|Windows Server 2016|
|**Produkt/Feature**|Hyper-V|
|**Schweregrad**|Fehler|
|**Kategorie**|Konfiguration|

In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.

## <a name="issue"></a>Problem
*Anwendungs konsistente Momentaufnahmen erfordert, dass die Volumeschattenkopie-Dienste (VSS) in den Gastbetriebssystemen der an der Replikation beteiligten virtuellen Computer aktiviert und konfiguriert werden.*

## <a name="impact"></a>Auswirkung
*Auch wenn Anwendungs konsistente Momentaufnahmen in der Replikationskonfiguration angegeben werden, werden diese von Hyper-V nur verwendet, wenn VSS konfiguriert ist. Dies wirkt sich auf die folgenden virtuellen Computer aus:*

\<list of virtual machines>

## <a name="resolution"></a>Lösung
*Verwenden Sie die Verbindung mit dem virtuellen Computer, um Integration Services auf dem virtuellen Computer zu installieren.*



