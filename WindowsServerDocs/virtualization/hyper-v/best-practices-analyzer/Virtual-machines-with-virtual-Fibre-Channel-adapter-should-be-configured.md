---
title: Mit einem virtuellen Fibre Channel-Adapter konfigurierte virtuelle Computer sollte für hohe Verfügbarkeit in den Fibre Channel-basierten Speicher konfiguriert werden
description: Die Onlineversion des Texts für diese Best Practices Analyzer-Regel.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 73127bdd-8086-4268-a93c-2fdf1623e91b
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 203477a022f7c5f819ef7b99f1b8e37a0b8b0a9f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59816941"
---
# <a name="virtual-machines-configured-with-a-virtual-fibre-channel-adapter-should-be-configured-for-high-availability-to-the-fibre-channel-based-storage"></a>Mit einem virtuellen Fibre Channel-Adapter konfigurierte virtuelle Computer sollte für hohe Verfügbarkeit in den Fibre Channel-basierten Speicher konfiguriert werden

>Gilt für: Windows Server 2016

Weitere Informationen zu best Practices und Überprüfungen finden Sie unter [Run Best Practices Analyzer Scans und Manage Scan Results](https://go.microsoft.com/fwlink/p/?LinkID=223177).  
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt /-Funktion**|Hyper-V|  
|**Schweregrad**|Informationen|  
|**Kategorie**|Konfiguration|  
  
In den folgenden Abschnitten Kursivschrift gibt an Benutzeroberflächentext, die im Best Practices Analyzer-Tool für dieses Problem angezeigt wird.
  
## <a name="issue"></a>**Problem:**  
*Eine oder mehrere virtuelle Computer verfügen nicht über eine hoch verfügbare Verbindung mit Fibre Channel-basierten Speicher, da diese virtuellen Computer mit einem virtuellen Fibre Channel-Adapter konfiguriert sind, die mit nur ein Hostbusadapter (HBA) verbunden ist.*  
  
## <a name="impact"></a>**Auswirkungen**  
*Die Fibre Channel-Verbindung zwischen den Speicher und die virtuellen Computer kann ein Ausfall des Hostbusadapters blockiert werden. Dies wirkt sich auf die folgenden virtuellen Computer aus:*  
  
\<Liste der virtuellen Computer >  
  
## <a name="resolution"></a>**Lösung**  
*Dem Hostbusadapter eine andere Verbindung vom virtuellen Computer hinzu, und Konfigurieren von Multipfad-e/a (MPIO) in das Gastbetriebssystem, redundante Fibre Channel-Verbindungen herzustellen.*  
  


