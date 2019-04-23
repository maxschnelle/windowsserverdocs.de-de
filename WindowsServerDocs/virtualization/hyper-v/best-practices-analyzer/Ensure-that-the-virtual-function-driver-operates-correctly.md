---
title: Stellen Sie sicher, dass der Treiber für die virtuelle Funktion, die ordnungsgemäß ausgeführt wird, wenn SR-IOV verwendet ein virtuellen Computer konfiguriert ist
description: Die Onlineversion des Texts für diese Best Practices Analyzer-Regel.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: d21e4b93-29bf-423a-a635-71c6d48dc49e
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 8d3d0a5008b55d4823cef9a8dd2a7bce4a6a2a33
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59852081"
---
# <a name="ensure-that-the-virtual-function-driver-operates-correctly-when-a-virtual-machine-is-configured-to-use-sr-iov"></a>Stellen Sie sicher, dass der Treiber für die virtuelle Funktion, die ordnungsgemäß ausgeführt wird, wenn SR-IOV verwendet ein virtuellen Computer konfiguriert ist

>Gilt für: Windows Server 2016

Weitere Informationen zu best Practices und Überprüfungen finden Sie unter [Run Best Practices Analyzer Scans und Manage Scan Results](https://go.microsoft.com/fwlink/p/?LinkID=223177).  
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt /-Funktion**|Hyper-V|  
|**Schweregrad**|Warnung|  
|**Kategorie**|Konfiguration|  
  
In den folgenden Abschnitten Kursivschrift gibt an Benutzeroberflächentext, die im Best Practices Analyzer-Tool für dieses Problem angezeigt wird.  
  
## <a name="issue"></a>Problem  
*Der virtuelle Funktion, die Treiber ist im Gastbetriebssystem, das eine oder mehrere virtuelle Computer nicht ordnungsgemäß.*  
  
## <a name="impact"></a>Auswirkungen  
*Netzwerkleistung ist nicht optimal ist, auf die folgenden virtuellen Computer:*  
  
\<Liste der virtuellen Computer >  
  
## <a name="resolution"></a>Auflösung  
*Führen Sie im Gastbetriebssystem folgende Schritte aus: Stellen Sie sicher, dass die richtigen Treiber installiert sind, und alle Netzwerkgeräte sind aktiviert, und überprüfen Sie das Ereignisprotokoll auf Fehler oder Warnungen.*  
  


