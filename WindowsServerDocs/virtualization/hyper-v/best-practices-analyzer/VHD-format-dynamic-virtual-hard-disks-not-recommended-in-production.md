---
title: Dynamischer virtueller Festplatten für VHD-Format werden nicht für virtuelle Computer empfohlen, die Server-Workloads in einer produktionsumgebung ausgeführt werden.
description: Die Onlineversion des Texts für diese Best Practices Analyzer-Regel.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 324a60a0-1d15-4ef2-9f17-23cbd2eb42ce
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 6acd27fa0efa27ba74c28e290c789edca599f66f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59849881"
---
# <a name="vhd-format-dynamic-virtual-hard-disks-are-not-recommended-for-virtual-machines-that-run-server-workloads-in-a-production-environment"></a>Dynamischer virtueller Festplatten für VHD-Format werden nicht für virtuelle Computer empfohlen, die Server-Workloads in einer produktionsumgebung ausgeführt werden.

>Gilt für: Windows Server 2016

Weitere Informationen zu best Practices und Überprüfungen finden Sie unter [Run Best Practices Analyzer Scans und Manage Scan Results](https://go.microsoft.com/fwlink/p/?LinkID=223177).  
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt /-Funktion**|Hyper-V|  
|**Schweregrad**|Warnung|  
|**Kategorie**|Konfiguration|  
  
In den folgenden Abschnitten Kursivschrift gibt an Benutzeroberflächentext, die im Best Practices Analyzer-Tool für dieses Problem angezeigt wird.
  
## <a name="issue"></a>**Problem:**  
*Eine oder mehrere virtuelle verwenden Computer VHD-Format an, die dynamisch erweiterbare virtuelle Festplatten.*  
  
## <a name="impact"></a>**Auswirkungen**  
*Dynamischer virtueller Festplatten für VHD-Format kann Konsistenzprobleme auftreten, wenn der Strom ausfällt. Konsistenzprobleme möglich, wenn der physische Datenträger ein unvollständigen oder falsches Updates auf einen Sektor in eine VHD-Datei ausführt, die bei einem Stromausfall geändert wird. Dies wirkt sich auf die folgenden virtuellen Computer aus:*  
  
\<Liste der virtuellen Computer >  
  
## <a name="resolution"></a>**Lösung**  
*Fahren Sie den virtuellen Computer herunter, und die VHD-Format dynamische virtuelle Festplatte konvertieren, virtuelle Festplatte im VHDX-Format oder eine feste virtuelle Festplatte. (Das VHDX-Format hat zuverlässigkeitsmechanismen, mit deren Hilfe den Datenträger vor Beschädigungen System Stromausfälle zurückzuführen sind zu schützen.) Konvertieren Sie jedoch nicht die virtuelle Festplatte ist dies wahrscheinlich an einer früheren Version von Windows an einem bestimmten Punkt angefügt werden. Windows Versionen vor Windows Server 2012 unterstützen nicht das VHDX-Format.*  
  


