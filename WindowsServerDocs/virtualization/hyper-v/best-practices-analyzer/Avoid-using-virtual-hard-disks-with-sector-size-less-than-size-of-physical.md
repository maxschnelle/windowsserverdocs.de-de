---
title: Vermeiden Sie die Verwendung von virtuellen Festplatten mit einer Sektorgröße, der kleiner als die Sektorgröße des physischen Speichers, in der Datei der virtuellen Festplatte gespeichert.
description: Die Onlineversion des Texts für diese Best Practices Analyzer-Regel.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: b7cf994e-bf4b-4b1b-bad6-ecf7d46d105e
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: b6ec2e0995180ecf9ae5986447fdd460a1c7a337
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59846261"
---
# <a name="avoid-using-virtual-hard-disks-with-a-sector-size-less-than-the-sector-size-of-the-physical-storage-that-stores-the-virtual-hard-disk-file"></a>Vermeiden Sie die Verwendung von virtuellen Festplatten mit einer Sektorgröße, der kleiner als die Sektorgröße des physischen Speichers, in der Datei der virtuellen Festplatte gespeichert.

>Gilt für: Windows Server 2016

Weitere Informationen zu best Practices und Überprüfungen finden Sie unter [Run Best Practices Analyzer Scans und Manage Scan Results](https://go.microsoft.com/fwlink/p/?LinkID=223177).  
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem** <br />**System**|Windows Server 2016|  
|**Produkt /-Funktion**|Hyper-V|  
|**Schweregrad**|Warnung|  
|**Kategorie**|Konfiguration|  
  
In den folgenden Abschnitten Kursivschrift gibt an Benutzeroberflächentext, die im Best Practices Analyzer-Tool für dieses Problem angezeigt wird.  
  
## <a name="issue"></a>**Problem:**  
*Eine oder mehrere virtuelle Festplatten müssen eine physische Sektorgröße, die kleiner als die physische Sektorgröße des Speichers auf dem die VHD-Datei gespeichert ist.*  
  
## <a name="impact"></a>**Auswirkungen**  
*Auf dem virtuellen Computer oder eine Anwendung, die die virtuelle Festplatte verwenden, können Leistungsprobleme auftreten. Dies wirkt sich auf die folgenden virtuellen Computer aus:*  
  
\<Liste der virtuellen Computer >  
  
## <a name="resolution"></a>**Lösung**  
*Führen Sie eine der folgenden:*  
  
-   *Führen Sie eine Storage-Migration zum Verschieben der virtuellen Festplatte auf einem neuen physischen system*  
  
-   *Verwenden von Windows PowerShell oder WMI So aktivieren Sie die virtuelle Festplatte im VHDX-Format eine bestimmten Sektorgröße melden*  
  
-   *Verwenden Sie eine registrierungseinstellung, um eine VHD-Format virtuelle Festplatte eine physische Sektorgröße von 4 KB melden aktivieren*  
  


