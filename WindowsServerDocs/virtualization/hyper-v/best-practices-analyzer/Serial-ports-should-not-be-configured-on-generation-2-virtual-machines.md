---
title: Serielle Ports dürfen nicht auf virtuellen Maschinen der Generation 2 konfiguriert werden.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: 87061193-dd3f-4398-aa5d-4cee83cadfa3
ms.date: 8/16/2016
ms.openlocfilehash: 2dbb9aae488922daeff74242d74d38685a371497
ms.sourcegitcommit: dd1fbb5d7e71ba8cd1b5bfaf38e3123bca115572
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/17/2020
ms.locfileid: "90744105"
---
# <a name="serial-ports-should-not-be-configured-on-generation-2-virtual-machines"></a>Serielle Ports dürfen nicht auf virtuellen Maschinen der Generation 2 konfiguriert werden.

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Scans finden Sie unter [Ausführen von Best Practices Analyzer-Scans und Verwalten der Scanergebnisse](https://go.microsoft.com/fwlink/p/?LinkID=223177).

|Eigenschaft|Details|
|-|-|
|**Betriebssystem**|Windows Server 2016|
|**Produkt/Feature**|Hyper-V|
|**Severity**|Warnung|
|**Kategorie**|Konfiguration|

In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.

## <a name="issue"></a>**Problem**
*Für mindestens einen virtuellen Computer der Generation 2 ist ein serieller Port konfiguriert.*

## <a name="impact"></a>**Auswirkungen**
*Die Leistung kann für die folgenden virtuellen Computer beeinträchtigt werden:*

\<list of virtual machines>

## <a name="resolution"></a>**Lösung**
*Wenn dies beabsichtigt ist, ist keine weitere Aktion erforderlich. Andernfalls sollten Sie den Hyper-V-Manager oder Windows PowerShell verwenden, um die Verbindungs Zeichenfolge aus den seriellen Anschlüssen auf dem virtuellen Computer zu entfernen.*



