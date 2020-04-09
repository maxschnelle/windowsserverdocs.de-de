---
title: SCSI-Controller nur konfigurieren, wenn dies vom Gast Betriebssystem unterstützt wird
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 861f194f-467e-4b07-a1c5-55b35f6327c4
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: cf206d9568ef7634d724f3fce450985c34ebfac5
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80862163"
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
  
*Virtuelle Computer können keinen mit dem SCSI-Controller verbundenen Speicher verwenden. Dies wirkt sich auf die folgenden virtuellen Computer aus:*  
  
\<Liste der virtuellen Computer >  
  
## <a name="resolution"></a>Auflösung  
  
*Fahren Sie den virtuellen Computer herunter, und entfernen Sie den SCSI-Controller mit dem Hyper-V-Manager aus dem virtuellen Computer. Starten Sie dann den virtuellen Computer neu.*  
  


