---
title: Wiederherstellungs Momentaufnahmen sollten nach dem Failover entfernt werden.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
manager: dongill
ms.author: kathydav
ms.topic: article
ms.assetid: 922115fa-e8dd-4055-aaf1-4a4437c5cf28
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 445a84b0b67cb4a36d107b4eb06e25fe80978ecd
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87957167"
---
# <a name="recovery-snapshots-should-be-removed-after-failover"></a>Wiederherstellungs Momentaufnahmen sollten nach dem Failover entfernt werden.

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Scans finden Sie unter [Ausführen von Best Practices Analyzer-Scans und Verwalten der Scanergebnisse](https://go.microsoft.com/fwlink/p/?LinkID=223177).

|Eigenschaft|Details|
|-|-|
|**Betriebssystem**|Windows Server 2016|
|**Produkt/Feature**|Hyper-V|
|**Schweregrad**|Warnung|
|**Kategorie**|Operationen (Operations)|

In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.

## <a name="issue"></a>**Problem**
*Für einen virtuellen Computer, für den ein Failover ausgeführt wurde, ist mindestens ein Wiederherstellungs*

## <a name="impact"></a>**Auswirkungen**
*Der verfügbare Speicherplatz kann auf dem physischen Datenträger, auf dem die Momentaufnahme Dateien gespeichert werden In diesem Fall können keine weiteren Datenträger Vorgänge für den physischen Speicher ausgeführt werden. Jeder virtuelle Computer, der auf dem physischen Speicher basiert, kann beeinträchtigt werden. Dies wirkt sich auf die folgenden virtuellen Computer aus:*

\<list of virtual machines>

## <a name="resolution"></a>**Lösung**
*Verwenden Sie für jeden virtuellen Computer, für den ein Failover ausgeführt wurde, das Complete-vmfailover-Cmdlet in Windows PowerShell, um die Wiederherstellungs Momentaufnahmen zu entfernen und die Failover*



