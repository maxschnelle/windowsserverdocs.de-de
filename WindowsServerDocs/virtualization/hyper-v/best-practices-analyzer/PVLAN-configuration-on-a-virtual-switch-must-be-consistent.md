---
title: Die pvlan-Konfiguration auf einem virtuellen Switch muss konsistent sein.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 4db63bcc-7a54-4f19-98a6-c274c3956d51
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 36616a5c4d8e57ae929cdab846db65dcdda57b85
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71364748"
---
# <a name="pvlan-configuration-on-a-virtual-switch-must-be-consistent"></a>Die pvlan-Konfiguration auf einem virtuellen Switch muss konsistent sein.

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Scans finden Sie unter [Ausführen von Best Practices Analyzer Scans und Verwalten der Scan Ergebnisse](https://go.microsoft.com/fwlink/p/?LinkID=223177).  
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016| 
|**Produkt/Feature**|Hyper-V|  
|**Zunehmen**|Fehler|  
|**Kategorie**|Konfiguration|  
  
In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.
  
## <a name="issue"></a>**Problem:**  
*Privates virtuelles lokales Netzwerk (pvlan) ist auf einem oder mehreren virtuellen Netzwerkadaptern nicht ordnungsgemäß konfiguriert.*  
  
## <a name="impact"></a>**Auswirkt**  
*Pvlan isoliert den Netzwerk Datenverkehr zwischen den virtuellen Computern möglicherweise nicht ordnungsgemäß.*  
  
## <a name="resolution"></a>**Auflösung**  
*Verwenden Sie das Windows PowerShell-Cmdlet Set-vmnetworkadaptervlan, um pvlan ordnungsgemäß zu konfigurieren.*  
  


