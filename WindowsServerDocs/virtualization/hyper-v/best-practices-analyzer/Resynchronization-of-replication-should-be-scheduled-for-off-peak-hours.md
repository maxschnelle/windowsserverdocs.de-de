---
title: Die erneute Synchronisierung der Replikation sollte außerhalb der Spitzenzeiten geplant werden.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: 093a7bb7-8e0a-486b-b42b-04edd8809710
ms.date: 8/16/2016
ms.openlocfilehash: 97df7945988f117ed16d59685cc60841775737da
ms.sourcegitcommit: dd1fbb5d7e71ba8cd1b5bfaf38e3123bca115572
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/17/2020
ms.locfileid: "90746155"
---
# <a name="resynchronization-of-replication-should-be-scheduled-for-off-peak-hours"></a>Die erneute Synchronisierung der Replikation sollte außerhalb der Spitzenzeiten geplant werden.

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Scans finden Sie unter [Ausführen von Best Practices Analyzer-Scans und Verwalten der Scanergebnisse](https://go.microsoft.com/fwlink/p/?LinkID=223177).

|Eigenschaft|Details|
|-|-|
|**Betriebssystem**|Windows Server 2016|
|**Produkt/Feature**|Hyper-V|
|**Severity**|Warnung|
|**Kategorie**|Operationen (Operations)|

In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.

## <a name="issue"></a>Problem
*Die erneute Synchronisierung der Replikation für die primären virtuellen Computer ist außerhalb der Spitzenzeiten nicht geplant.*

## <a name="impact"></a>Auswirkung
*Je länger sich ein virtueller Computer in einem Zustand befindet, der eine erneute Synchronisierung erfordert, desto länger werden die Replikations Protokolldateien vergrößert, und die nicht replizierten Änderungen erfolgen auf den primären virtuellen Computern. Dies wirkt sich auf die folgenden virtuellen Computer aus:*

\<list of virtual machines>

## <a name="resolution"></a>Lösung
*Verwenden Sie den Hyper-V-Manager, um die Replikationseinstellungen für die virtuelle Maschine zu ändern und die erneute Synchronisierung außerhalb der Spitzenzeiten automatisch auszuführen.*



