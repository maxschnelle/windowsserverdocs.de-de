---
title: Die Anzahl der logischen Prozessoren darf die maximal unterstützte Anzahl nicht überschreiten.
description: Enthält Anweisungen zur Behebung des Problems gemeldet wird, die von dieser Best Practices Analyzer-Regel.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 66df8b02-91d1-424b-8934-a39c214d530e
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: d1275a17cc04494708f5ecfe9b708834b4233641
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59847071"
---
# <a name="the-number-of-logical-processors-in-use-must-not-exceed-the-supported-maximum"></a>Die Anzahl der logischen Prozessoren darf die maximal unterstützte Anzahl nicht überschreiten.

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Überprüfungen finden Sie unter [Best Practices Analyzer](https://go.microsoft.com/fwlink/?LinkId=122786).  
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt /-Funktion**|Hyper-V|  
|**Schweregrad**|Fehler|  
|**Kategorie**|Richtlinie|  
  
In den folgenden Abschnitten gibt Text erscheint in der Best Practices Analyzer-Tool zur Lösung dieses Problems Kursivdruck an.  
  
## <a name="issue"></a>Problem  
  
*Der Server wird über zu viele logische Prozessoren konfiguriert werden.*  
  
## <a name="impact"></a>Auswirkungen  
  
*Microsoft unterstützt keine Hyper-V auf diesem Computer ausgeführt.*  
  
## <a name="resolution"></a>Auflösung  
  
*Entfernen Sie einige Prozessoren von diesem Computer zu oder verwenden Sie Msconfig zu, um die Anzahl der verfügbaren Prozessoren zu beschränken.*  
  
Finden Sie unter den folgenden Anweisungen aus, um Msconfig verwenden. Weitere Informationen zum Entfernen von Prozessoren lesen Sie die Anweisungen, die mit dem Computer stammen, oder wenden Sie sich an den Hardwarehersteller. Weitere Informationen zur maximal unterstützten Konfigurationen für Hyper-V finden Sie unter [Planen der Hyper-V-Skalierbarkeit unter Windows Server 2016](../plan/Plan-for-Hyper-V-scalability-in-Windows-Server-2016.md).  
  
### <a name="to-limit-the-number-of-available-processors"></a>Um die Anzahl der verfügbaren Prozessoren zu beschränken.  
  
1.  Öffnen Sie das Konfigurations-app (Msconfig.exe). Zu diesem Zweck klicken Sie auf **starten**, Typ **Msconfig**, mit der rechten Maustaste die **Systemkonfiguration** desktop-app, und klicken Sie auf **als Administrator ausführen**.  
  
2.  Von der **Boot** auf **erweiterte Optionen**.  
  
3.  Wählen Sie **Anzahl der Prozessoren** , und wählen Sie eine Zahl in der Liste. Klicken Sie auf **OK**.  
  
4.  Neustart des Computers für die Ausführung mit der neuen Anzahl von Prozessoren.  
  


