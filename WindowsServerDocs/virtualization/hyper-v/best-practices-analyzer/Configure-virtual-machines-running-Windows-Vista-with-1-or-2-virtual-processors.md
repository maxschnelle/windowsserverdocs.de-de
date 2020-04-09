---
title: Konfigurieren virtueller Computer, auf denen Windows Vista ausgeführt wird, mit 1 oder 2 virtuellen Prozessoren
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: e562bce3-fd68-42c9-821c-12022ae4746c
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 0319039dfc26d59b1045ffc60f52e56eb900ff76
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80862023"
---
# <a name="configure-virtual-machines-running-windows-vista-with-1-or-2-virtual-processors"></a>Konfigurieren virtueller Computer, auf denen Windows Vista ausgeführt wird, mit 1 oder 2 virtuellen Prozessoren

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Scans finden Sie unter [Ausführen von Best Practices Analyzer Scans und Verwalten der Scan Ergebnisse](https://go.microsoft.com/fwlink/p/?LinkID=223177).  
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt/Feature**|Hyper-V|  
|**Zunehmen**|Konfiguration|  
|**Kategorie**|Error|  
  
In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.  
  
## <a name="issue"></a>Problem  
  
*Ein virtueller Computer, auf dem Windows Vista ausgeführt wird, ist mit mehr als zwei virtuellen Prozessoren konfiguriert.*  
  
## <a name="impact"></a>Auswirkungen  
  
*Microsoft unterstützt nicht die Konfiguration der folgenden virtuellen Computer:*  
  
\<Liste der Namen der virtuellen Computer >  
  
## <a name="resolution"></a>Auflösung  
  
*Fahren Sie den virtuellen Computer herunter, und entfernen Sie einen oder mehrere virtuelle Prozessoren.*  
  
### <a name="to-remove-virtual-processors"></a>So entfernen Sie virtuelle Prozessoren  
  
1.  Öffnen Sie den Hyper-V-Manager. Klicken Sie auf **Start**, zeigen Sie auf **Verwaltung**, und klicken Sie dann auf **Hyper-V-Manager**.  
  
2.  Wählen Sie im Ergebnisbereich unter **Virtual Machines**den virtuellen Computer aus, den Sie konfigurieren möchten. Der Status der virtuellen Maschine sollte als **Off**aufgeführt werden. Wenn dies nicht der Fall ist, klicken Sie mit der rechten Maustaste auf den virtuellen Computer und dann auf **herunter**fahren.  
  
3.  Klicken Sie im Bereich **Aktion** unter dem Namen des virtuellen Computers auf **Einstellungen**.  
  
4.  Klicken Sie im Navigationsbereich auf **Prozessor**.  
  
5.  Legen Sie auf der Seite **Prozessor** die Anzahl der Prozessoren auf **1** oder **2** fest, und klicken Sie dann auf **OK**.  
  


