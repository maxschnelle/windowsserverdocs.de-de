---
title: Konfigurieren von virtuellen Computern mit Windows 7 mit mehr als 4 virtuelle Prozessoren
description: Die Onlineversion des Texts für diese Best Practices Analyzer-Regel.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 8fcf0868-b543-4f94-aee7-35324346da55
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: ee450f3510e6dcc1d0a32ed5d5a0be549ac8809e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59848041"
---
# <a name="configure-virtual-machines-running-windows-7-with-no-more-than-4-virtual-processors"></a>Konfigurieren von virtuellen Computern mit Windows 7 mit mehr als 4 virtuelle Prozessoren

>Gilt für: Windows Server 2016

Weitere Informationen zu best Practices und Überprüfungen finden Sie unter [Run Best Practices Analyzer Scans und Manage Scan Results](https://go.microsoft.com/fwlink/p/?LinkID=223177).  
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt /-Funktion**|Hyper-V|  
|**Schweregrad**|Fehler|  
|**Kategorie**|Konfiguration|  
  
In den folgenden Abschnitten Kursivschrift gibt an Benutzeroberflächentext, die im Best Practices Analyzer-Tool für dieses Problem angezeigt wird.  
  
## <a name="issue"></a>**Problem:**  
*Ein virtuellen Computer mit Windows 7 ist mit mehr als 4 virtuellen Prozessoren konfiguriert werden.*  
  
## <a name="impact"></a>**Auswirkungen**  
*Microsoft unterstützt nicht die Konfiguration der folgenden virtuellen Computer:*  
  
\<Liste der virtuellen Computer >  
  
## <a name="resolution"></a>**Lösung**  
*Der virtuelle Computer heruntergefahren Sie, und entfernen Sie eine oder mehrere virtuelle Prozessoren.*  
  
#### <a name="to-remove-virtual-processors"></a>So entfernen Sie die virtuelle Prozessoren  
  
1.  Öffnen Sie den Hyper-V-Manager. Klicken Sie auf **Start**, zeigen Sie auf **Verwaltung**, und klicken Sie dann auf **Hyper-V-Manager**.  
  
2.  Klicken Sie im Ergebnisbereich unter **VMs**, wählen Sie den virtuellen Computer, die Sie konfigurieren möchten. Der Status des virtuellen Computers sollte als aufgelistet werden **aus**. Wenn sie nicht der Fall ist, mit der rechten Maustaste den virtuellen Computer, und klicken Sie dann auf **Herunterfahren**.  
  
3.  Klicken Sie im Bereich **Aktion** unter dem Namen des virtuellen Computers auf **Einstellungen**.  
  
4.  Klicken Sie im Navigationsbereich auf **Prozessor**.  
  
5.  Auf der **Prozessor** Seite, legen Sie die Anzahl der Prozessoren **3** oder weniger, und klicken Sie dann auf **OK**.  
  


