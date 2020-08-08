---
title: Vermeiden Sie die Verwendung von Prüfpunkten auf einem virtuellen Computer, auf dem eine Serverauslastung in einer Produktionsumgebung ausgeführt wird.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
manager: dongill
ms.author: kathydav
ms.topic: article
ms.assetid: 1be75890-d316-495a-b9b7-be75fc1aac10
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: dadff29461786a454dc8d7ee6b46f3b567ef6bd8
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87994997"
---
# <a name="avoid-using-checkpoints-on-a-virtual-machine-that-runs-a-server-workload-in-a-production-environment"></a>Vermeiden Sie die Verwendung von Prüfpunkten auf einem virtuellen Computer, auf dem eine Serverauslastung in einer Produktionsumgebung ausgeführt wird.

>Gilt für: Windows Server 2016



*Weitere Informationen zu bewährten Methoden und Scans finden Sie unter* [Best Practices Analyzer](https://go.microsoft.com/fwlink/?LinkId=122786).

|Eigenschaft|Details|
|-|-|
|**Betriebssystem**|Windows Server 2016|
|**Produkt/Feature**|Hyper-V|
|**Schweregrad**|Warnung|
|**Kategorie**|Operationen (Operations)|

In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.

> [!NOTE]
> In Windows Server 2012 R2 wurden Momentaufnahmen virtueller Computer in Hyper-V-Manager zu den Prüfpunkten virtueller Computer umbenannt, damit Sie der in der System Center Virtual Machine Management verwendeten Terminologie entsprechen. Weitere Informationen finden Sie unter [Übersicht über Prüfpunkte und Momentaufnahmen](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn818483(v=ws.11)).

## <a name="issue"></a>Problem

*Ein virtueller Computer mit einem oder mehreren Prüfpunkten wurde gefunden.*

## <a name="impact"></a>Auswirkung

*Verfügbarer Speicherplatz auf dem physischen Datenträger, auf dem die Prüf Punkt Dateien gespeichert sind In diesem Fall können keine weiteren Datenträger Vorgänge für den physischen Speicher ausgeführt werden. Jeder virtuelle Computer, der auf dem physischen Speicher basiert, kann beeinträchtigt werden.*

Wenn physischer Speicherplatz auf dem Datenträger ausgeführt wird, werden alle ausgeführten virtuellen Computer, die auf diesem Datenträger gespeicherte Prüfpunkte oder virtuelle Festplatten aufweisen, möglicherweise automatisch angehalten. Der Hyper-V-Manager zeigt den Status dieser virtuellen Computer als angehalten-kritisch an.

## <a name="resolution"></a>Lösung

*Wenn auf dem virtuellen Computer eine Server Arbeitsauslastung in einer Produktionsumgebung ausgeführt wird, schalten Sie den virtuellen Computer offline, und verwenden Sie dann den Hyper-V-Manager, um die Prüfpunkte anzuwenden oder zu löschen. Zum Löschen von Prüfpunkten müssen Sie den virtuellen Computer Herunterfahren, um den Vorgang abzuschließen.*

> [!NOTE]
> Produktions Prüfpunkte sind nun als Alternative zu Standard Prüfpunkten verfügbar. Weitere Informationen finden [Sie unter Auswählen zwischen Standard-oder Produktions Prüfpunkten](../manage/Choose-between-standard-or-production-checkpoints-in-Hyper-V.md).