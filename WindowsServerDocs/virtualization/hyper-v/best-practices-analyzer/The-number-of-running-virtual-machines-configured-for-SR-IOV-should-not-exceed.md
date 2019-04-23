---
title: Die Anzahl der ausgeführten virtuellen Computer für SR-IOV konfiguriert sollte die Anzahl der virtuellen Funktionen, die zur Verfügung, die virtuellen Computer nicht überschreiten.
description: Die Onlineversion des Texts für diese Best Practices Analyzer-Regel.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 8bd4af5e-9e7d-4710-8950-39435a8bb373
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: e63df9283927437f9cfc62c052d83b07fe599b34
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59829751"
---
# <a name="the-number-of-running-virtual-machines-configured-for-sr-iov-should-not-exceed-the-number-of-virtual-functions-available-to-the-virtual-machines"></a>Die Anzahl der ausgeführten virtuellen Computer für SR-IOV konfiguriert sollte die Anzahl der virtuellen Funktionen, die zur Verfügung, die virtuellen Computer nicht überschreiten.

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
*Es sind nicht ausreichend virtuelle Funktionen verfügbar, für die Anzahl der ausgeführten virtuellen Maschinen, die für die Single-Root i/o-Virtualisierung (SR-IOV) konfiguriert.*  
  
## <a name="impact"></a>Auswirkungen  
*Netzwerkleistung möglicherweise nicht optimal auf die folgenden virtuellen Computer:*  
   
\<Liste der virtuellen Computer >  
  
## <a name="resolution"></a>Auflösung  
*Deaktivieren Sie ggf. die SR-IOV auf eine oder mehrere virtuelle Computer, die eine virtuellen SR-IOV-Funktion nicht benötigen.*  
  


