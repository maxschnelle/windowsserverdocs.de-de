---
title: Die Anzahl der verwendeten logischen Prozessoren darf den unterstützten maximalen Wert nicht überschreiten.
description: Enthält Anweisungen zum Beheben des Problems, das von dieser Best Practices Analyzer Regel gemeldet wird.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 66df8b02-91d1-424b-8934-a39c214d530e
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: b6cd948c47e58dec919cd946ad701f70403d6af3
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80859293"
---
# <a name="the-number-of-logical-processors-in-use-must-not-exceed-the-supported-maximum"></a>Die Anzahl der verwendeten logischen Prozessoren darf den unterstützten maximalen Wert nicht überschreiten.

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Überprüfungen finden Sie unter [Best Practices Analyzer](https://go.microsoft.com/fwlink/?LinkId=122786).  
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt/Feature**|Hyper-V|  
|**Zunehmen**|Error|  
|**Kategorie**|Policy (Richtlinie)|  
  
In den folgenden Abschnitten gibt Kursiv Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.  
  
## <a name="issue"></a>Problem  
  
*Der Server ist mit zu vielen logischen Prozessoren konfiguriert.*  
  
## <a name="impact"></a>Auswirkungen  
  
*Die Ausführung von Hyper-V auf diesem Computer wird von Microsoft nicht unterstützt.*  
  
## <a name="resolution"></a>Auflösung  
  
*Entfernen Sie einige Prozessoren von diesem Computer, oder verwenden Sie msconfig, um die Anzahl der verfügbaren Prozessoren einzuschränken.*  
  
Weitere Informationen zur Verwendung von MSCONFIG finden Sie in den folgenden Anweisungen. Ausführliche Informationen zum Entfernen von Prozessoren finden Sie in den Anweisungen des Computers, oder wenden Sie sich an den Hardwarehersteller. Ausführliche Informationen zu den maximal unterstützten Konfigurationen für Hyper-v finden Sie unter [Planen der Hyper-v-Skalierbarkeit in Windows Server 2016](../plan/Plan-for-Hyper-V-scalability-in-Windows-Server-2016.md).  
  
### <a name="to-limit-the-number-of-available-processors"></a>So begrenzen Sie die Anzahl der verfügbaren Prozessoren  
  
1.  Öffnen Sie die Systemkonfigurations-app (msconfig. exe). Klicken Sie hierzu auf **Start**, geben Sie **msconfig**ein, klicken Sie mit der rechten Maustaste auf die Desktop-App für die **System Konfiguration** , und klicken Sie auf **als Administrator**  
  
2.  Klicken Sie auf der Registerkarte **Start** auf **Erweiterte Optionen**.  
  
3.  Wählen Sie **Anzahl der Prozessoren aus** , und wählen Sie dann eine Zahl in der Liste aus. Klicken Sie auf **OK**.  
  
4.  Starten Sie den Computer neu, um ihn mit der neuen Anzahl von Prozessoren auszuführen.  
  


