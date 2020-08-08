---
title: Die pvlan-Konfiguration auf einem virtuellen Switch muss konsistent sein.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
manager: dongill
ms.author: kathydav
ms.topic: article
ms.assetid: 4db63bcc-7a54-4f19-98a6-c274c3956d51
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 63780266fa23187e12bfd5d503a1f3c0306bc364
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87939027"
---
# <a name="pvlan-configuration-on-a-virtual-switch-must-be-consistent"></a>Die pvlan-Konfiguration auf einem virtuellen Switch muss konsistent sein.

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Scans finden Sie unter [Ausführen von Best Practices Analyzer-Scans und Verwalten der Scanergebnisse](https://go.microsoft.com/fwlink/p/?LinkID=223177).

|Eigenschaft|Details|
|-|-|
|**Betriebssystem**|Windows Server 2016|
|**Produkt/Feature**|Hyper-V|
|**Schweregrad**|Fehler|
|**Kategorie**|Konfiguration|

In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.

## <a name="issue"></a>**Problem**
*Privates virtuelles lokales Netzwerk (pvlan) ist auf einem oder mehreren virtuellen Netzwerkadaptern nicht ordnungsgemäß konfiguriert.*

## <a name="impact"></a>**Auswirkungen**
*Pvlan isoliert den Netzwerk Datenverkehr zwischen den virtuellen Computern möglicherweise nicht ordnungsgemäß.*

## <a name="resolution"></a>**Lösung**
*Verwenden Sie das Windows PowerShell-Cmdlet Set-vmnetworkadaptervlan, um pvlan ordnungsgemäß zu konfigurieren.*



