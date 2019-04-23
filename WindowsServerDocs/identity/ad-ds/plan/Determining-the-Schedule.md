---
ms.assetid: 28ecaf5c-9131-406c-b211-a230162e462e
title: Bestimmen des Zeitplans
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: dee63ce0fb687b2b722ce64614c54388fc544433
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59839001"
---
# <a name="determining-the-schedule"></a>Bestimmen des Zeitplans

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Sie können Standort-Link-Verfügbarkeit durch Festlegen eines Zeitplans für standortverknüpfungen steuern. Bei der Replikation zwischen zwei Standorten mehrere standortverknüpfungen durchlaufen werden, bestimmt die Schnittmenge der Replikationszeitpläne auf alle relevanten Verknüpfungen, den Verbindungszeitplan zwischen den beiden Standorten.  
  
Informationen zur Planung für das Festlegen des standortverknüpfungs-Zeitplan erstellen Sie zwei sich überschneidende Zeitpläne zwischen standortverknüpfungen, die Domänencontroller enthalten, die direkt miteinander repliziert. Verwenden Sie den Standardzeitplan (100 - Prozent verfügbar) auf diese Links, es sei denn, Sie Replikations-Datenverkehr während der Spitzenzeiten blockieren möchten. Replikation blockieren Geben Sie Priorität auf anderen Datenverkehr, aber Sie wird auch der Replikationswartezeit erhöhen.  
  
Domänencontroller speichern Uhrzeit in Coordinated Universal Time (UTC). Uhrzeiteinstellungen im standortverknüpfungs-Zeitpläne Objekt entsprechen der lokalen Zeit des Standorts und der Computer, auf denen der Zeitplan festgelegt ist. Wenn ein Domänencontroller ein Computers, die in einem anderen Standort und die Zeitzone kontaktiert, wird der Zeitplan auf dem Domänencontroller die Einstellung nach der Ortszeit für den Standort des Computers angezeigt.  
  


