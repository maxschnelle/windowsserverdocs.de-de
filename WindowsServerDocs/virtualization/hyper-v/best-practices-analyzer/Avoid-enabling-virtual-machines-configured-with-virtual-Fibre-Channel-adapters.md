---
title: Vermeiden Sie das Aktivieren von virtuellen Computern, die mit virtuellen Fibre Channel Adaptern konfiguriert sind, damit Live Migrationen zulässig sind, wenn es weniger Pfade zu Fibre Channel logischen Einheiten (LUNs) auf dem Ziel als der Quelle gibt.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
manager: dongill
ms.author: kathydav
ms.topic: article
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 2b85793cd5a680b0fd13fca3da5881b8622710fb
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87963676"
---
# <a name="avoid-enabling-virtual-machines-configured-with-virtual-fibre-channel-adapters-to-allow-live-migrations-when-there-are-fewer-paths-to-fibre-channel-logical-units-luns-on-the-destination-than-on-the-source"></a>Vermeiden Sie das Aktivieren von virtuellen Computern, die mit virtuellen Fibre Channel Adaptern konfiguriert sind, damit Live Migrationen zulässig sind, wenn es weniger Pfade zu Fibre Channel logischen Einheiten (LUNs) auf dem Ziel als der Quelle gibt.

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Scans finden Sie unter [Ausführen von Best Practices Analyzer-Scans und Verwalten der Scanergebnisse](https://go.microsoft.com/fwlink/p/?LinkID=223177).

|Eigenschaft|Details|
|-|-|
|**Betriebssystem**|Windows Server 2016|
|**Produkt/Feature**|Hyper-V|
|**Schweregrad**|Warnung|
|**Kategorie**|Konfiguration|

In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.

## <a name="issue"></a>**Problem**
*Bei mindestens einer virtuellen Maschine ist die allowreducedfkredunancy-Eigenschaft im WMI-Anbieter für die Virtualisierung festgelegt.*

## <a name="impact"></a>**Auswirkungen**
*Die Live Migration der folgenden virtuellen Computer kann zu Datenverlusten oder Unterbrechungen des Speichers führen:*

\<list of virtual machines>

## <a name="resolution"></a>**Lösung**
*Löschen Sie ggf. die Eigenschaft allowreducedfkredundancy WMI auf den betroffenen virtuellen Computern. Wenn diese Eigenschaft deaktiviert ist, können Sie eine Live Migration auf virtuellen Computern, die mit virtuellen Fibre Channel Adaptern konfiguriert sind, nur dann ausführen, wenn die Anzahl der Pfade Fibre Channel auf dem Ziel gleich oder größer als die Anzahl der Pfade in der Quelle ist. Diese Überprüfungen helfen dabei, Datenverluste oder e/a-Vorgänge im Speicher zu vermeiden.*