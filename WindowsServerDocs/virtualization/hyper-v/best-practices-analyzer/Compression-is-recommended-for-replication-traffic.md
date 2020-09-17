---
title: Komprimierung wird für Replikations Datenverkehr empfohlen
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: cf8be6e9-2909-4e4a-bb63-d1e1ebbc6930
ms.date: 8/16/2016
ms.openlocfilehash: 61f1b56720af3583745960073823fef7b7b5173f
ms.sourcegitcommit: dd1fbb5d7e71ba8cd1b5bfaf38e3123bca115572
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/17/2020
ms.locfileid: "90745845"
---
# <a name="compression-is-recommended-for-replication-traffic"></a>Komprimierung wird für Replikations Datenverkehr empfohlen

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Scans finden Sie unter [Ausführen von Best Practices Analyzer-Scans und Verwalten der Scanergebnisse](https://go.microsoft.com/fwlink/p/?LinkID=223177).

|Eigenschaft|Details|
|-|-|
|**Betriebssystem**|Windows Server 2016|
|**Produkt/Feature**|Hyper-V|
|**Severity**|Warnung|
|**Kategorie**|Konfiguration|

In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.

## <a name="issue"></a>Problem
*Der Replikations Datenverkehr, der vom primären Server zum Replikat Server über das Netzwerk gesendet wird, ist nicht komprimiert.*

## <a name="impact"></a>Auswirkung
*Der Replikations Datenverkehr verwendet mehr Bandbreite als notwendig. Dies wirkt sich auf die folgenden virtuellen Computer aus:*

\<list of virtual machines>

## <a name="resolution"></a>Lösung
*Konfigurieren Sie das Hyper-v-Replikat, um die über das Netzwerk übertragenen Daten in den Einstellungen für den virtuellen Computer im Hyper-v-Manager zu komprimieren. Sie können auch Tools außerhalb von Hyper-V verwenden, um die Komprimierung auszuführen.*



