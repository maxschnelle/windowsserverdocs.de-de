---
title: Die Replikation für mindestens eine virtuelle Maschine auf diesem Server wurde angehalten.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
manager: dongill
ms.author: kathydav
ms.topic: article
ms.assetid: e1119a40-eda3-4058-8648-7df81cbc6c29
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: a40c4d45eea6d0c363cd03d5eef94543ddc1317d
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87948428"
---
# <a name="replication-is-paused-for-one-or-more-virtual-machines-on-this-server"></a>Die Replikation für mindestens eine virtuelle Maschine auf diesem Server wurde angehalten.

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Scans finden Sie unter [Ausführen von Best Practices Analyzer-Scans und Verwalten der Scanergebnisse](https://go.microsoft.com/fwlink/p/?LinkID=223177).

|Eigenschaft|Details|
|-|-|
|**Betriebssystem**|Windows Server 2016|
|**Produkt/Feature**|Hyper-V|
|**Schweregrad**|Warnung|
|**Kategorie**|Operationen (Operations)|

In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.

## <a name="issue"></a>Problem
*Die Replikation für mindestens einen virtuellen Computer wurde angehalten. Während der primäre virtuelle Computer angehalten wird, werden alle auftretenden Änderungen akkumuliert und an den virtuellen Replikat Computer gesendet, sobald die Replikation fortgesetzt wird.*

## <a name="impact"></a>Auswirkung
*Solange die Replikation angehalten ist, verbrauchen akkumulierte Änderungen, die auf dem primären virtuellen Computer auftreten, den verfügbaren Speicherplatz auf dem primären Server. Nach dem Fortsetzen der Replikation kann es zu einem großen Anstieg des Netzwerk Datenverkehrs zum Replikat Server kommen. Dies wirkt sich auf die folgenden virtuellen Computer aus:*

\<list of virtual machines>

## <a name="resolution"></a>Lösung
*Vergewissern Sie sich, dass das Anhalten der Replikation beabsichtigt war Wenn die Replikation angehalten wurde, um wenig Speicherplatz oder Netzwerk Konnektivität zu beheben, setzen Sie die Replikation fort, sobald diese Probleme behoben sind.*



