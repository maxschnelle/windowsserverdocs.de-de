---
title: Die Anzahl der für SR-IOV konfigurierten virtuellen Computer sollte nicht die Anzahl der virtuellen Funktionen überschreiten, die für die virtuellen Maschinen verfügbar sind.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: 8bd4af5e-9e7d-4710-8950-39435a8bb373
ms.date: 8/16/2016
ms.openlocfilehash: 432bf4132e8c19a326fda646960b30315d3952b1
ms.sourcegitcommit: dd1fbb5d7e71ba8cd1b5bfaf38e3123bca115572
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/17/2020
ms.locfileid: "90745805"
---
# <a name="the-number-of-running-virtual-machines-configured-for-sr-iov-should-not-exceed-the-number-of-virtual-functions-available-to-the-virtual-machines"></a>Die Anzahl der für SR-IOV konfigurierten virtuellen Computer sollte nicht die Anzahl der virtuellen Funktionen überschreiten, die für die virtuellen Maschinen verfügbar sind.

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Scans finden Sie unter [Ausführen von Best Practices Analyzer-Scans und Verwalten der Scanergebnisse](https://go.microsoft.com/fwlink/p/?LinkID=223177).

|Eigenschaft|Details|
|-|-|
|**Betriebssystem**|Windows Server 2016|
|**Produkt/Feature**|Hyper-V|
|**Severity**|Warnung|
|**Kategorie**|Konfiguration|

In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.

## <a name="issue"></a>Problem
*Für die Anzahl der für die e/a-Virtualisierung mit Einzel Stamm (Single-root I/O Virtualization, SR-IOV) konfigurierten virtuellen Maschinen sind nicht genügend virtuelle Funktionen verfügbar.*

## <a name="impact"></a>Auswirkung
*Die Netzwerkleistung ist auf den folgenden virtuellen Computern möglicherweise nicht optimal:*

\<list of virtual machines>

## <a name="resolution"></a>Lösung
*Deaktivieren Sie ggf. SR-IOV auf einem oder mehreren virtuellen Computern, für die keine virtuelle SR-IOV-Funktion erforderlich ist.*



