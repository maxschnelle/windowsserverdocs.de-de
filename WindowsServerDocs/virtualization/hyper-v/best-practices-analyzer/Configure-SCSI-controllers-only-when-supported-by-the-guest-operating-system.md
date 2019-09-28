---
title: SCSI-Controller nur konfigurieren, wenn dies vom Gast Betriebssystem unterstützt wird
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 861f194f-467e-4b07-a1c5-55b35f6327c4
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: da8d929a8f06f58610913d28d2f1e90299efb235
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71366418"
---
# <a name="configure-scsi-controllers-only-when-supported-by-the-guest-operating-system"></a>SCSI-Controller nur konfigurieren, wenn dies vom Gast Betriebssystem unterstützt wird

>Gilt für: Windows Server 2016


  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt/Feature**|Hyper-V|  
|**Zunehmen**|Warnung|  
|**Kategorie**|Konfiguration|  
  
In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.  
  
## <a name="issue"></a>Problem  
  
*Ein virtueller Computer wird mit einem SCSI-Controller konfiguriert, der nicht verwendet werden kann, da das Gast Betriebssystem SCSI-Controller nicht unterstützt.*  
  
## <a name="impact"></a>Auswirkungen  
  
virtuelle Computer mit @no__t 0können keinen mit dem SCSI-Controller verbundenen Speicher verwenden. Dies wirkt sich auf die folgenden virtuellen Computer aus: *  
  
\<list of Virtual Machines >  
  
## <a name="resolution"></a>Auflösung  
  
*fahren Sie den virtuellen Computer herunter, und entfernen Sie den SCSI-Controller mit dem Hyper-V-Manager von der virtuellen Maschine. Starten Sie dann den virtuellen Computer neu.*  
  


