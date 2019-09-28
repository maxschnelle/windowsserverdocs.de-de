---
title: Dynamische virtuelle Festplatten im VHD-Format werden für virtuelle Maschinen, auf denen Server Arbeits Auslastungen in einer Produktionsumgebung ausgeführt werden, nicht empfohlen.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 324a60a0-1d15-4ef2-9f17-23cbd2eb42ce
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: bf5464208fc145a31571f01822bb5ba54efe89c4
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71364589"
---
# <a name="vhd-format-dynamic-virtual-hard-disks-are-not-recommended-for-virtual-machines-that-run-server-workloads-in-a-production-environment"></a>Dynamische virtuelle Festplatten im VHD-Format werden für virtuelle Maschinen, auf denen Server Arbeits Auslastungen in einer Produktionsumgebung ausgeführt werden, nicht empfohlen.

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
*Mindestens eine virtuelle Maschine verwendet dynamisch erweiterbare virtuelle Festplatten im VHD-Format.*  
  
## <a name="impact"></a>**Auswirkt**  
bei dynamischen virtuellen Festplatten im *vhd-Format können Konsistenzprobleme auftreten, wenn ein Stromausfall auftritt. Konsistenzprobleme können auftreten, wenn die physische Festplatte ein unvollständiges oder falsches Update eines Sektors in einer VHD-Datei ausführt, die bei einem Stromausfall geändert wird. Dies wirkt sich auf die folgenden virtuellen Computer aus:*  
  
\<list of Virtual Machines >  
  
## <a name="resolution"></a>**Auflösung**  
*fahren Sie den virtuellen Computer herunter, und konvertieren Sie die dynamische virtuelle Festplatte im VHD-Format in eine virtuelle Festplatte im vhdx-Format oder in eine virtuelle Festplatte mit fester Größe. (Das vhdx-Format verfügt über Zuverlässigkeits Mechanismen, mit denen der Datenträger vor Beschädigungen aufgrund von System Stromausfällen geschützt wird.) Konvertieren Sie die virtuelle Festplatte jedoch nicht, wenn Sie zu einem bestimmten Zeitpunkt wahrscheinlich an eine frühere Version von Windows angefügt wird. Ältere Windows-Versionen als Windows Server 2012 unterstützen das vhdx-Format nicht.*  
  


