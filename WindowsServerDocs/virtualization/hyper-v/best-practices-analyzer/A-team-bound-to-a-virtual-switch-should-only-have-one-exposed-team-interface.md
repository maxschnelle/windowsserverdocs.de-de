---
title: Ein Team, das an einen virtuellen Switch gebunden ist, darf nur über eine Team Schnittstelle verfügen.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 1074f086-1a2e-42e1-b58c-f55e657d5ce1
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 6baa9e4ae900c9b671003872b4eb4589efb2f085
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71365401"
---
# <a name="a-team-bound-to-a-virtual-switch-should-only-have-one-exposed-team-interface"></a>Ein Team, das an einen virtuellen Switch gebunden ist, darf nur über eine Team Schnittstelle verfügen.

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
*Ein oder mehrere virtuelle Switches sind an ein Team gebunden, das über mehrere Team Schnittstellen verfügt.*  
  
## <a name="impact"></a>**Auswirkt**  
*Die folgenden virtuellen Switches haben möglicherweise keinen Zugriff auf VLANs und Bandbreite, die von anderen Team Schnittstellen verwendet werden:*  
  
\<list of Virtual Switches >  
  
## <a name="resolution"></a>**Auflösung**  
*Verwenden Sie das Windows PowerShell-Cmdlet Remove-netlbfoteamnic, um alle Team Schnittstellen aus dem anderen Team als der standardmäßigen Team Schnittstelle zu entfernen.*  
  


