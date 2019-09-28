---
title: Vermeiden Sie die Konfiguration virtueller Computer, um ungefilterte SCSI-Befehle zuzulassen
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: dd4a3d78-a77f-451e-a383-d5cf45ea17cf
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 5deb20862ed0e359febd4a9b58202d53c85058ca
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71365272"
---
# <a name="avoid-configuring-virtual-machines-to-allow-unfiltered-scsi-commands"></a>Vermeiden Sie die Konfiguration virtueller Computer, um ungefilterte SCSI-Befehle zuzulassen

>Gilt für: Windows Server 2016


  
*Weitere Informationen zu bewährten Methoden und Scans finden Sie unter* [Best Practices Analyzer](https://go.microsoft.com/fwlink/?LinkId=122786).  
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt/Feature**|Hyper-V|  
|**Zunehmen**|Warnung|  
|**Kategorie**|Vorgänge|  
  
In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.  
  
## <a name="issue"></a>Problem  
  
*Ein virtueller Computer ist so konfiguriert, dass er ungefilterte SCSI-Befehle zulässt.*  
  
## <a name="impact"></a>Auswirkungen  
  
*umgehung der SCSI-Befehls Filterung stellt ein Sicherheitsrisiko dar. Diese Konfiguration sollte nur aktiviert werden, wenn Sie für die Kompatibilität mit Speicheranwendungen erforderlich ist, die im Gast Betriebssystem ausgeführt werden. Die folgenden virtuellen Computer sind so konfiguriert, dass ungefilterte SCSI-Befehle zulässig sind:*  
  
\<liste der Namen der virtuellen Computer >  
  
## <a name="resolution"></a>Auflösung  
  
*wenden Sie sich an Ihren Speicher Anbieter, um zu ermitteln, ob diese Konfiguration erforderlich ist. Wenn das Verwaltungs Betriebssystem oder andere Gast Betriebssysteme kompromittiert sind oder ungewöhnliche Verhalten aufweisen, konfigurieren Sie den virtuellen Computer neu, damit die Befehle blockiert werden.*  
  


