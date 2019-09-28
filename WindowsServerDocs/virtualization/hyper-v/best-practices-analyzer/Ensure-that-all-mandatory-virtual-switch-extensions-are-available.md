---
title: Stellen Sie sicher, dass alle obligatorischen Erweiterungen für virtuelle Switches verfügbar sind.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 2f2f2698-f5ec-4cad-aa64-d6987e8142a1
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: c9363fbce35552a8f7d279662ae9072bcd7ea480
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71364824"
---
# <a name="ensure-that-all-mandatory-virtual-switch-extensions-are-available"></a>Stellen Sie sicher, dass alle obligatorischen Erweiterungen für virtuelle Switches verfügbar sind.

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Scans finden Sie unter [Ausführen von Best Practices Analyzer Scans und Verwalten der Scan Ergebnisse](https://go.microsoft.com/fwlink/p/?LinkID=223177).  
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt/Feature**|Hyper-V|  
|**Zunehmen**|Warnung|  
|**Kategorie**|Konfiguration|  
  
In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.  
  
## <a name="issue"></a>Problem  
*Mindestens ein virtueller Netzwerkadapter ist mit einem virtuellen Switch mit obligatorischen Erweiterungen verbunden, die deaktiviert oder nicht installiert sind.*  
  
## <a name="impact"></a>Auswirkungen  
*Der Netzwerk Datenverkehr wird auf einem oder mehreren virtuellen Netzwerkadaptern auf den folgenden virtuellen Computern blockiert:*  
  
\<list of Virtual Machines >  
  
## <a name="resolution"></a>Auflösung  
Stellen Sie *zuerst sicher, dass die obligatorische Erweiterung auf dem Host installiert ist, und installieren Sie die Erweiterung bei Bedarf. Wenn die obligatorische Erweiterung deaktiviert ist, verwenden Sie den Virtual Switch-Manager oder das Windows PowerShell-Cmdlet Enable-vmswitchextension, um die Erweiterung zu aktivieren.*  
  


