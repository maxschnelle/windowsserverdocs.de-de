---
title: Virtuelle Computer sollten mindestens einmal pro Woche gesichert werden.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
manager: dongill
ms.author: kathydav
ms.topic: article
ms.assetid: 7dbd3dfc-c873-4a77-89f7-3166e18d9531
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: fccc0bb7c46206df210f699cdda84507343c342a
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87960203"
---
# <a name="virtual-machines-should-be-backed-up-at-least-once-every-week"></a>Virtuelle Computer sollten mindestens einmal pro Woche gesichert werden.

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
*Mindestens eine virtuelle Maschine wurde in der letzten Woche nicht gesichert.*

## <a name="impact"></a>Auswirkung
*Ein erheblicher Datenverlust kann auftreten, wenn auf dem virtuellen Computer ein Problem auftritt und keine aktuelle Sicherung vorhanden ist. Dies wirkt sich auf die folgenden virtuellen Computer aus:*

\<list of virtual machines>

## <a name="resolution"></a>Lösung
*Planen Sie eine Sicherung der virtuellen Computer so, dass Sie mindestens einmal pro Woche ausgeführt wird. Sie können diese Regel ignorieren, wenn diese virtuelle Maschine ein Replikat ist und der primäre virtuelle Computer gesichert wird, oder wenn dies der primäre virtuelle Computer ist und das zugehörige Replikat gesichert wird.*



