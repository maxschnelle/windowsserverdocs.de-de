---
title: Mindestens ein Netzwerkadapter muss als Ziel für die Port Spiegelung konfiguriert sein.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: b83c166d-f010-47c4-a4bb-02167f2e3361
ms.date: 8/16/2016
ms.openlocfilehash: cf1713bb6897f68c7bee839b4a3e4838aaa8a2fb
ms.sourcegitcommit: dd1fbb5d7e71ba8cd1b5bfaf38e3123bca115572
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/17/2020
ms.locfileid: "90745605"
---
# <a name="one-or-more-network-adapters-should-be-configured-as-the-destination-for-port-mirroring"></a>Mindestens ein Netzwerkadapter muss als Ziel für die Port Spiegelung konfiguriert sein.

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
*Für mindestens einen virtuellen Computer ist ein Netzwerkadapter als Quelle für die Port Spiegelung konfiguriert, aber es ist kein entsprechendes Ziel auf dem virtuellen Switch vorhanden.*

## <a name="impact"></a>**Auswirkungen**
*Die Port Spiegelung wird für die folgenden virtuellen Switches und virtuellen Maschinen nicht ordnungsgemäß ausgeführt:*

\<list of virtual machines>

## <a name="resolution"></a>**Lösung**
*Verwenden Sie Windows PowerShell oder Hyper-V-Manager, um die Port Spiegelungs Konfiguration abzuschließen oder zu korrigieren.*



