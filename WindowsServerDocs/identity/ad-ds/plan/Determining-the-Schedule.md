---
ms.assetid: 28ecaf5c-9131-406c-b211-a230162e462e
title: Bestimmen des Zeitplans
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 0ec953b34475c50e62553a9ba95e4d45d9904bf3
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="determining-the-schedule"></a>Bestimmen des Zeitplans

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Sie können Link websiteverfügbarkeit durch Festlegen eines Zeitplans für standortverknüpfungen steuern. Wenn die Replikation zwischen zwei Standorten mehrere standortverknüpfungen durchläuft, bestimmt die Überschneidung von Replikationszeitplänen für die auf alle relevanten Links den Verbindungszeitplan für die zwischen den beiden Standorten.  
  
Um zum Festlegen des standortverknüpfungs-Zeitplans zu planen, erstellen Sie zwei sich überschneidende Zeitpläne zwischen standortverknüpfungen, die Domänencontroller enthalten, die direkt miteinander zu replizieren. Verwenden Sie den Standardzeitplan (100Prozent verfügbar) auf die Links, wenn Sie während der Spitzenzeiten Replikations-Datenverkehr blockieren möchten. Replikation blockieren Sie den übrigen Datenverkehr Priorität zuweisen, doch Sie auch die Replikationswartezeit erhöhen.  
  
Domänencontroller speichern Uhrzeit in koordinierter Weltzeit (UTC). Uhrzeiteinstellungen im standortverknüpfungs-Zeitpläne Objekt entsprechen der lokalen Zeit des Standorts und der Computer, auf denen der Zeitplan festgelegt ist. Wenn ein Domänencontroller ein Computers, das in einem anderen Standort und die entsprechende Zeitzone ist kontaktiert, zeigt der Zeitplan auf dem Domänencontroller die Einstellung der lokalen Zeit für den Standort des Computers entsprechend an.  
  


