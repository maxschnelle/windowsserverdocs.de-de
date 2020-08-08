---
title: Hyper-V sollte die einzige aktivierte Rolle sein.
description: Enthält Anweisungen zum Beheben des Problems, das von dieser Best Practices Analyzer Regel gemeldet wird.
manager: dongill
ms.author: kathydav
ms.topic: article
ms.assetid: 5a0ed176-048f-40b1-b56c-8391b805fd37
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 2e2c392ad75f4f0c84216db637a0106be8821b41
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87968337"
---
# <a name="hyper-v-should-be-the-only-enabled-role"></a>Hyper-V sollte die einzige aktivierte Rolle sein.

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Überprüfungen finden Sie unter [Best Practices Analyzer](https://go.microsoft.com/fwlink/?LinkId=122786).

|Eigenschaft|Details|
|-|-|
|**Betriebssystem**|Windows Server 2016|
|**Produkt/Feature**|Hyper-V|
|**Schweregrad**|Warnung|
|**Kategorie**|Konfiguration|

In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.

## <a name="issue"></a>Problem

*Andere Rollen als Hyper-V sind auf diesem Server aktiviert.*

In den meisten Fällen ist es keine gute Idee, andere Rollen auf einem Server zu installieren, auf dem die Hyper-V-Rolle ausgeführt wird. Remotedesktop-Virtualisierungshost Rollen Dienst stellt eine Ausnahme dar, da Sie Teil der Remotedesktopdienste Rolle ist und Hyper-V auf dem gleichen Server installiert werden muss.

## <a name="impact"></a>Auswirkung

*Die Hyper-V-Rolle sollte die einzige Rolle sein, die auf einem Server aktiviert ist.*

Diese bewährte Vorgehensweise trägt dazu bei, das Host Betriebssystem für Rollen, Features und Anwendungen, die nicht zum Ausführen von Hyper-V erforderlich sind, frei zu halten. Wenn Sie diese bewährte Vorgehensweise befolgen und Hyper-v auf Nano Server ausführen, können Sie die Anzahl der benötigten Updates verringern, da nur Nano Server, die Hyper-v-Dienst Komponenten und der Windows-Hypervisor Software Updates unterliegen.

## <a name="resolution"></a>Lösung

*Verwenden Sie Server-Manager, um alle Rollen mit Ausnahme von Hyper-V zu entfernen.*

Server-Manager enthält den Assistenten zum Entfernen von Rollen. Mit diesem Assistenten können Sie mehrere Rollen gleichzeitig entfernen. Vor dem Entfernen von Rollen prüft der Assistent zum Entfernen von Rollen auf Abhängigkeiten, um das Risiko zu verringern, dass Software, auf der andere Rollen basieren, entfernt wird. Wenn Abhängigkeiten gefunden werden, werden Sie vom Assistenten aufgefordert, das Entfernen anderer Rollen, Rollen Dienste oder Software zu genehmigen, die für installierte Rollen erforderlich sind.

Wenn Sie Server-Manager verwenden möchten, müssen Sie auf dem Computer als Administrator angemeldet sein.

#### <a name="to-remove-a-role"></a>So entfernen Sie eine Rolle

1.  Öffnen Sie Server-Manager mithilfe von Verknüpfungen im **Startmenü** , auf der Windows-Taskleiste oder in "Verwaltung".
2.   Klicken Sie im Bereich **Rollen Zusammenfassung** des Server-Manager Hauptfensters auf **Rollen entfernen**. Befolgen Sie die Anweisungen im Assistenten, um die Rolle zu entfernen.





