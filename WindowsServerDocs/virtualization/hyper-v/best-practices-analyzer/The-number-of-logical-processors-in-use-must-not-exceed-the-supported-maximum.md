---
title: Die Anzahl der verwendeten logischen Prozessoren darf den unterstützten maximalen Wert nicht überschreiten.
description: Enthält Anweisungen zum Beheben des Problems, das von dieser Best Practices Analyzer Regel gemeldet wird.
manager: dongill
ms.author: kathydav
ms.topic: article
ms.assetid: 66df8b02-91d1-424b-8934-a39c214d530e
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: d74fa49a3ce0015cb8ee819b537153519c498627
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87960463"
---
# <a name="the-number-of-logical-processors-in-use-must-not-exceed-the-supported-maximum"></a>Die Anzahl der verwendeten logischen Prozessoren darf den unterstützten maximalen Wert nicht überschreiten.

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Überprüfungen finden Sie unter [Best Practices Analyzer](https://go.microsoft.com/fwlink/?LinkId=122786).

|Eigenschaft|Details|
|-|-|
|**Betriebssystem**|Windows Server 2016|
|**Produkt/Feature**|Hyper-V|
|**Schweregrad**|Fehler|
|**Kategorie**|Richtlinie|

In den folgenden Abschnitten gibt Kursiv Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.

## <a name="issue"></a>Problem

*Der Server ist mit zu vielen logischen Prozessoren konfiguriert.*

## <a name="impact"></a>Auswirkung

*Die Ausführung von Hyper-V auf diesem Computer wird von Microsoft nicht unterstützt.*

## <a name="resolution"></a>Lösung

*Entfernen Sie einige Prozessoren von diesem Computer, oder verwenden Sie msconfig, um die Anzahl der verfügbaren Prozessoren einzuschränken.*

Weitere Informationen zur Verwendung von MSCONFIG finden Sie in den folgenden Anweisungen. Ausführliche Informationen zum Entfernen von Prozessoren finden Sie in den Anweisungen des Computers, oder wenden Sie sich an den Hardwarehersteller. Ausführliche Informationen zu den maximal unterstützten Konfigurationen für Hyper-v finden Sie unter [Planen der Hyper-v-Skalierbarkeit in Windows Server 2016](../plan/Plan-for-Hyper-V-scalability-in-Windows-Server-2016.md).

### <a name="to-limit-the-number-of-available-processors"></a>So begrenzen Sie die Anzahl der verfügbaren Prozessoren

1.  Öffnen Sie die Systemkonfigurations-app (Msconfig.exe). Klicken Sie hierzu auf **Start**, geben Sie **msconfig**ein, klicken Sie mit der rechten Maustaste auf die Desktop-App für die **System Konfiguration** , und klicken Sie auf **als Administrator**

2.  Klicken Sie auf der Registerkarte **Start** auf **Erweiterte Optionen**.

3.  Wählen Sie **Anzahl der Prozessoren aus** , und wählen Sie dann eine Zahl in der Liste aus. Klicken Sie auf **OK**.

4.  Starten Sie den Computer neu, um ihn mit der neuen Anzahl von Prozessoren auszuführen.



