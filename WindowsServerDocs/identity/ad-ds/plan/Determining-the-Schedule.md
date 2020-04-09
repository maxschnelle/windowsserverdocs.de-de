---
ms.assetid: 28ecaf5c-9131-406c-b211-a230162e462e
title: Bestimmen des Zeitplans
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: d5c1c7c77304317bab2e80223dd745c88bc79efd
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80822543"
---
# <a name="determining-the-schedule"></a>Bestimmen des Zeitplans

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Sie können die Verfügbarkeit von Standort Links steuern, indem Sie einen Zeitplan für Standort Verknüpfungen festlegen. Wenn die Replikation zwischen zwei Standorten mehrere Standort Verknüpfungen durchläuft, bestimmt die Schnittmenge der Replikations Zeitpläne für alle relevanten Links den Verbindungs Zeitplan zwischen den beiden Standorten.  
  
Um das Festlegen des Zeitplans für die Standort Verknüpfung zu planen, erstellen Sie zwei überlappende Zeitpläne Zwischenstandort Verknüpfungen, die Domänen Controller enthalten, die direkt aufeinander repliziert werden Verwenden Sie den Standard Zeitplan (100-Prozent verfügbar) für diese Links, es sei denn, Sie möchten den Replikations Datenverkehr während der Spitzenzeiten blockieren. Wenn Sie die Replikation blockieren, legen Sie den anderen Datenverkehr Priorität, aber Sie erhöhen auch die Replikations Latenz.  
  
Domänen Controller speichern Zeit in koordinierter Weltzeit (UTC). Die Zeit Einstellungen in den Plänen für Standort Verknüpfungs Objekte entsprechen der Ortszeit des Standorts und des Computers, auf dem der Zeitplan festgelegt ist. Wenn ein Domänen Controller einen Computer kontaktiert, der sich in einem anderen Standort und einer anderen Zeitzone befindet, zeigt der Zeitplan auf dem Domänen Controller die Zeiteinstellung gemäß der Ortszeit für den Standort des Computers an.  
  


