---
title: Ein Team mit einem virtuellen Switch gebunden darf nur einen verfügbar gemachten teamschnittstelle enthalten.
description: Die Onlineversion des Texts für diese Best Practices Analyzer-Regel.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 1074f086-1a2e-42e1-b58c-f55e657d5ce1
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 108bbec1439959bb7ab4475b59c7231653952ea8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59838461"
---
# <a name="a-team-bound-to-a-virtual-switch-should-only-have-one-exposed-team-interface"></a>Ein Team mit einem virtuellen Switch gebunden darf nur einen verfügbar gemachten teamschnittstelle enthalten.

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
*Eine oder mehrere virtuelle Switches sind an ein Team gebunden, die über mehrere Teams Schnittstellen verfügt.*  
  
## <a name="impact"></a>**Auswirkungen**  
*Die folgenden virtuellen Switches möglicherweise nicht den Zugriff auf die VLANs und Bandbreite, die von anderen teamschnittstellen verwendet:*  
  
\<Liste virtueller Switches >  
  
## <a name="resolution"></a>**Lösung**  
*Verwenden Sie das Windows PowerShell-Cmdlet Remove-NetLbfoTeamNic, um alle teamschnittstellen aus dem Team als die Standardschnittstelle für das Team zu entfernen.*  
  


