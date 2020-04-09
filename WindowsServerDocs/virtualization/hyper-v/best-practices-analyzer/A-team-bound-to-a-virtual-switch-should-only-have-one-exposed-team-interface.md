---
title: Ein Team, das an einen virtuellen Switch gebunden ist, darf nur über eine Team Schnittstelle verfügen.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 1074f086-1a2e-42e1-b58c-f55e657d5ce1
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 413448945d2598ba36bed646144a43e39a1a3159
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857943"
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
  
## <a name="issue"></a>Problem
*Ein oder mehrere virtuelle Switches sind an ein Team gebunden, das über mehrere Team Schnittstellen verfügt.*  
  
## <a name="impact"></a>Auswirkungen
*Die folgenden virtuellen Switches haben möglicherweise keinen Zugriff auf VLANs und Bandbreite, die von anderen Team Schnittstellen verwendet werden:*  
  
\<Liste der virtuellen Switches >  
  
## <a name="resolution"></a>Auflösung
*Verwenden Sie das Windows PowerShell-Cmdlet Remove-netlbfoteamnic, um alle Team Schnittstellen aus dem anderen Team als der standardmäßigen Team Schnittstelle zu entfernen.*  
  


