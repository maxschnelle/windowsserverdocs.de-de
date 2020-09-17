---
title: Virtuelle Festplatten mit Auslagerungs Dateien sollten von der Replikation ausgeschlossen werden.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: c0be8a5f-64a1-488a-944e-bb913bb90517
ms.date: 8/16/2016
ms.openlocfilehash: 14729113ee2ba3694bcc29d50da5e7113c763268
ms.sourcegitcommit: dd1fbb5d7e71ba8cd1b5bfaf38e3123bca115572
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/17/2020
ms.locfileid: "90746565"
---
# <a name="virtual-hard-disks-with-paging-files-should-be-excluded-from-replication"></a>Virtuelle Festplatten mit Auslagerungs Dateien sollten von der Replikation ausgeschlossen werden.

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Scans finden Sie unter [Ausführen von Best Practices Analyzer-Scans und Verwalten der Scanergebnisse](https://go.microsoft.com/fwlink/p/?LinkID=223177).

|Eigenschaft|Details|
|-|-|
|**Betriebssystem**|Windows Server 2016|
|**Produkt/Feature**|Hyper-V|
|**Severity**|Information|
|**Kategorie**|Konfiguration|

In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.

## <a name="issue"></a>Problem
*Auslagerungs Dateien sollten von der Teilnahme an der Replikation ausgeschlossen werden, aber es wurden keine Datenträger ausgeschlossen.*

## <a name="impact"></a>Auswirkung
*Beim auslagern von Dateien kommt es zu einer hohen Menge an Eingabe-/Ausgabeaktivität, bei der unnötigerweise weniger Ressourcen für die Replikation erforderlich sind. Dies wirkt sich auf die folgenden virtuellen Computer aus:*

\<list of virtual machines>

## <a name="resolution"></a>Lösung
*Wenn Sie dies nicht bereits getan haben, erstellen Sie eine separate virtuelle Festplatte für die Windows-Auslagerungs Datei. Wenn die anfängliche Replikation bereits abgeschlossen ist, entfernen Sie die Replikation mit dem Hyper-V-Manager. Konfigurieren Sie dann die Replikation erneut, und schließen Sie die virtuelle Festplatte mit der Auslagerungs Datei von der Replikation aus.*



