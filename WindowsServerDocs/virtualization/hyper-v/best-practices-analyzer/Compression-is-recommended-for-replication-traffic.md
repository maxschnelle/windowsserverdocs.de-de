---
title: Komprimierung wird für Replikations Datenverkehr empfohlen
description: Online Version des Texts für diese Best Practices Analyzer Regel.
manager: dongill
ms.author: kathydav
ms.topic: article
ms.assetid: cf8be6e9-2909-4e4a-bb63-d1e1ebbc6930
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 2184a2ec0441af7fdbfc7566d783bee82f6bbbb9
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87954527"
---
# <a name="compression-is-recommended-for-replication-traffic"></a>Komprimierung wird für Replikations Datenverkehr empfohlen

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Scans finden Sie unter [Ausführen von Best Practices Analyzer-Scans und Verwalten der Scanergebnisse](https://go.microsoft.com/fwlink/p/?LinkID=223177).

|Eigenschaft|Details|
|-|-|
|**Betriebssystem**|Windows Server 2016|
|**Produkt/Feature**|Hyper-V|
|**Schweregrad**|Warnung|
|**Kategorie**|Konfiguration|

In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.

## <a name="issue"></a>Problem
*Der Replikations Datenverkehr, der vom primären Server zum Replikat Server über das Netzwerk gesendet wird, ist nicht komprimiert.*

## <a name="impact"></a>Auswirkung
*Der Replikations Datenverkehr verwendet mehr Bandbreite als notwendig. Dies wirkt sich auf die folgenden virtuellen Computer aus:*

\<list of virtual machines>

## <a name="resolution"></a>Lösung
*Konfigurieren Sie das Hyper-v-Replikat, um die über das Netzwerk übertragenen Daten in den Einstellungen für den virtuellen Computer im Hyper-v-Manager zu komprimieren. Sie können auch Tools außerhalb von Hyper-V verwenden, um die Komprimierung auszuführen.*



