---
title: Konfigurieren Sie einen virtuellen Computer mit einem SCSI-Controller, um das Plug-in und den Hot-trennen Sie-Speicher zu integrieren.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 511e1172-aeef-463d-b5dd-2bffae411ff1
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 5b901ee8f11942b8ad50a3c34c53354a5998e105
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71365068"
---
# <a name="configure-a-virtual-machine-with-a-scsi-controller-to-be-able-to-hot-plug-and-hot-unplug-storage"></a>Konfigurieren Sie einen virtuellen Computer mit einem SCSI-Controller, um das Plug-in und den Hot-trennen Sie-Speicher zu integrieren.

>Gilt für: Windows Server 2016


  
*Weitere Informationen zu bewährten Methoden und Scans finden Sie unter* [Best Practices Analyzer](https://go.microsoft.com/fwlink/?LinkId=122786).  
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt/Feature**|Hyper-V|  
|**Zunehmen**|Warnung|  
|**Kategorie**|Konfiguration|  
  
In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.  
  
## <a name="issue"></a>Problem  
  
*Ein virtueller Computer wurde gefunden, der nicht mit einem SCSI-Controller konfiguriert ist.*  
  
## <a name="impact"></a>Auswirkungen  
  
*Sie sind nicht in der Lage, den trennen Sie-in-Plug-in-Speicher für die folgenden virtuellen Computer zu schließen:*  
  
\<liste der Namen der virtuellen Computer >  
  
Durch die Fähigkeit, ein Hot-Plug-in oder Hot-trennen Sie-Speicher zu ermöglichen, ist es einfacher, die Speicheranforderungen eines virtuellen Computers ohne Ausfallzeiten zu verwalten Virtuelle Computer ohne SCSI-Controller müssen heruntergefahren werden, bevor Sie Speicher hinzufügen oder entfernen können.  
  
## <a name="resolution"></a>Auflösung  
  
*wenn Sie nicht für den virtuellen Computer einen Hot-Plug-in-oder Hot-trennen Sie-Speicher benötigen, ist keine Aktion erforderlich. Fahren Sie andernfalls den virtuellen Computer herunter, und fügen Sie der Konfiguration einen SCSI-Controller hinzu.*  
  
Um einen SCSI-Controller für das Hot-Plug-in und den Hot-trennen Sie-Speicher zu verwenden, muss auf dem Gast Betriebssystem die aktuelle Version von Integration Services ausgeführt werden.  
  


