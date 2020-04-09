---
title: Vermeiden Sie die Konfiguration virtueller Computer, um ungefilterte SCSI-Befehle zuzulassen
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: dd4a3d78-a77f-451e-a383-d5cf45ea17cf
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: ac059bce1704a4e72b2c373d8186dbd4e31f2164
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857793"
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
  
*Das umgehen der SCSI-Befehls Filterung stellt ein Sicherheitsrisiko dar. Diese Konfiguration sollte nur aktiviert werden, wenn Sie für die Kompatibilität mit Speicheranwendungen erforderlich ist, die im Gast Betriebssystem ausgeführt werden. Die folgenden virtuellen Computer sind so konfiguriert, dass Sie ungefilterte SCSI-Befehle zulassen:*  
  
\<Liste der Namen der virtuellen Computer >  
  
## <a name="resolution"></a>Auflösung  
  
*Wenden Sie sich an Ihren Speicher Anbieter, um zu ermitteln, ob diese Konfiguration erforderlich ist. Wenn das Verwaltungs Betriebssystem oder andere Gast Betriebssysteme kompromittiert sind oder ungewöhnliche Verhalten aufweisen, konfigurieren Sie den virtuellen Computer neu, damit die Befehle blockiert werden.*  
  


