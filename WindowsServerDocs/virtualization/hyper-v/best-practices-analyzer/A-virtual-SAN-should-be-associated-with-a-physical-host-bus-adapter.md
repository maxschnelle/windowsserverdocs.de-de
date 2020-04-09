---
title: Ein virtuelles San muss einem physischen Hostbus Adapter zugeordnet sein.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 14bca69b-e779-4e90-b5c1-1b015625572f
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 10a17f8661f1436f5b4db317648edde57a0dfe74
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857933"
---
# <a name="a-virtual-san-should-be-associated-with-a-physical-host-bus-adapter"></a>Ein virtuelles San muss einem physischen Hostbus Adapter zugeordnet sein.

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Scans finden Sie unter [Ausführen von Best Practices Analyzer Scans und Verwalten der Scan Ergebnisse](https://go.microsoft.com/fwlink/p/?LinkID=223177).  
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt/Feature**|Hyper-V|  
|**Zunehmen**|Warnung|  
|**Kategorie**|Konfiguration|  
  
  
In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.  
  
## <a name="issue"></a>**Problem:**  
*Ein virtuelles Storage Area Network (San) wurde ohne Zuordnung zu einem Hostbus Adapter (HBA) konfiguriert.*  
  
## <a name="impact"></a>**Auswirkt**  
*Ein virtueller Computer kann nicht gestartet werden, wenn er mit einem virtuellen Fibre Channel Adapter konfiguriert ist, der mit einem falsch konfigurierten virtuellen SAN verbunden ist. Dies wirkt sich auf die folgenden virtuellen Sans aus:*  
  
  
\<Liste der virtuellen Sans >  
  
  
## <a name="resolution"></a>**Lösung**  
*Konfigurieren Sie das virtuelle San neu, indem Sie es mit einem Hostbus Adapter verbinden.*  
  
  
  


