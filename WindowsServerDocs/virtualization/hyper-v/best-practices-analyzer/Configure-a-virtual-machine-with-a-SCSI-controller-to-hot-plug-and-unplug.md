---
title: Konfigurieren Sie einen virtuellen Computer mit einem SCSI-Controller, um das Plug-in und den Hot-trennen Sie-Speicher zu integrieren.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 511e1172-aeef-463d-b5dd-2bffae411ff1
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: bd49a911d278a1f07fe9630f39798204d760dd88
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80862153"
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
  
\<Liste der Namen der virtuellen Computer >  
  
Durch die Fähigkeit, ein Hot-Plug-in oder Hot-trennen Sie-Speicher zu ermöglichen, ist es einfacher, die Speicheranforderungen eines virtuellen Computers ohne Ausfallzeiten zu verwalten Virtuelle Computer ohne SCSI-Controller müssen heruntergefahren werden, bevor Sie Speicher hinzufügen oder entfernen können.  
  
## <a name="resolution"></a>Auflösung  
  
*Wenn Sie keine Hot-Plug-oder Hot-trennen Sie-Speicher für diesen virtuellen Computer benötigen, ist keine Aktion erforderlich. Fahren Sie andernfalls den virtuellen Computer herunter, und fügen Sie der Konfiguration einen SCSI-Controller hinzu.*  
  
Um einen SCSI-Controller für das Hot-Plug-in und den Hot-trennen Sie-Speicher zu verwenden, muss auf dem Gast Betriebssystem die aktuelle Version von Integration Services ausgeführt werden.  
  


