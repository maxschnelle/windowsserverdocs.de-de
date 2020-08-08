---
title: Ein virtuelles San muss einem physischen Hostbus Adapter zugeordnet sein.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
manager: dongill
ms.author: kathydav
ms.topic: article
ms.assetid: 14bca69b-e779-4e90-b5c1-1b015625572f
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 344b3b60c0d4613b121ef7ed17447810e0d6293d
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87965587"
---
# <a name="a-virtual-san-should-be-associated-with-a-physical-host-bus-adapter"></a>Ein virtuelles San muss einem physischen Hostbus Adapter zugeordnet sein.

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
*Ein virtuelles Storage Area Network (San) wurde ohne Zuordnung zu einem Hostbus Adapter (HBA) konfiguriert.*

## <a name="impact"></a>**Auswirkungen**
*Ein virtueller Computer kann nicht gestartet werden, wenn er mit einem virtuellen Fibre Channel Adapter konfiguriert ist, der mit einem falsch konfigurierten virtuellen SAN verbunden ist. Dies wirkt sich auf die folgenden virtuellen Sans aus:*


\<list of virtual SANs>


## <a name="resolution"></a>**Lösung**
*Konfigurieren Sie das virtuelle San neu, indem Sie es mit einem Hostbus Adapter verbinden.*





