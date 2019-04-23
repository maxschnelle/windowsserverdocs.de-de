---
title: Vermeiden Sie die Verwendung von Prüfpunkten auf einem virtuellen Computer, der eine arbeitsauslastung in einer produktionsumgebung ausgeführt wird.
description: Die Onlineversion des Texts für diese Best Practices Analyzer-Regel.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 1be75890-d316-495a-b9b7-be75fc1aac10
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 166ef839a40452cc4156144e10e9c666e7ce3472
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59856151"
---
# <a name="avoid-using-checkpoints-on-a-virtual-machine-that-runs-a-server-workload-in-a-production-environment"></a>Vermeiden Sie die Verwendung von Prüfpunkten auf einem virtuellen Computer, der eine arbeitsauslastung in einer produktionsumgebung ausgeführt wird.

>Gilt für: Windows Server 2016


  
*Weitere Informationen zu best Practices und Überprüfungen finden Sie unter* [Best Practices Analyzer](https://go.microsoft.com/fwlink/?LinkId=122786).  
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt /-Funktion**|Hyper-V|  
|**Schweregrad**|Warnung|  
|**Kategorie**|Vorgänge|  

In den folgenden Abschnitten Kursivschrift gibt an Benutzeroberflächentext, die im Best Practices Analyzer-Tool für dieses Problem angezeigt wird.

> [!NOTE]  
> In Windows Server 2012 R2 wurden Momentaufnahmen von virtuellen Computern in Prüfpunkte für virtuelle Maschinen in Hyper-V-Manager in System Center Virtual Machine Management verwendete Terminologie entsprechend umbenannt. Weitere Informationen finden Sie unter [Checkpoints and Snapshots Overview](https://technet.microsoft.com/library/dn818483.aspx).  
  
## <a name="issue"></a>Problem  
  
*Ein virtueller Computer mit der eine oder mehrere Prüfpunkte wurde gefunden.*  
  
## <a name="impact"></a>Auswirkungen  
  
*Speicherplatz kann auf dem physischen Datenträger erschöpft, die Dateien der Prüfpunkte gespeichert. In diesem Fall können keine zusätzlichen Datenträger-Operationen auf dem physischen Speicher ausgeführt werden. Eine virtuelle Maschine, die auf den physischen Speicher basieren, kann beeinträchtigt werden.*  
  
Wenn der physische Speicherplatz verbraucht ist, kann virtuelle Maschine, die Prüfpunkte oder virtuelle Festplatten, die auf diesem Datenträger gespeichert wurde automatisch angehalten werden. Hyper-V-Manager zeigt den Status dieser virtuellen Computer als "angehalten-kritisch".  
  
## <a name="resolution"></a>Auflösung  
  
*Wenn der virtuelle Computer eine serverarbeitsauslastung in einer produktionsumgebung ausgeführt wird, wird schalten Sie der virtuelle Computer offline, und verwenden Sie Hyper-V-Manager anwenden oder löschen Sie die Prüfpunkte. Um Prüfpunkte zu löschen, müssen Sie den virtuellen Computer bis zum Abschluss der Herunterfahren.*  
  
> [!NOTE]  
> Produktionsprüfpunkte sind nun als Alternative zu standardprüfpunkten verfügbar. Weitere Informationen finden Sie unter [wählen zwischen Standard- und produktionsprüfpunkten](../manage/Choose-between-standard-or-production-checkpoints-in-Hyper-V.md).  
  


