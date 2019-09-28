---
ms.assetid: 28ecaf5c-9131-406c-b211-a230162e462e
title: Bestimmen des Zeitplans
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 04576a88825205398f1b555d9f5063ac26e2a76e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408869"
---
# <a name="determining-the-schedule"></a>Bestimmen des Zeitplans

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Sie können die Verfügbarkeit von Standort Links steuern, indem Sie einen Zeitplan für Standort Verknüpfungen festlegen. Wenn die Replikation zwischen zwei Standorten mehrere Standort Verknüpfungen durchläuft, bestimmt die Schnittmenge der Replikations Zeitpläne für alle relevanten Links den Verbindungs Zeitplan zwischen den beiden Standorten.  
  
Um das Festlegen des Zeitplans für die Standort Verknüpfung zu planen, erstellen Sie zwei überlappende Zeitpläne Zwischenstandort Verknüpfungen, die Domänen Controller enthalten, die direkt aufeinander repliziert werden Verwenden Sie den Standard Zeitplan (100-Prozent verfügbar) für diese Links, es sei denn, Sie möchten den Replikations Datenverkehr während der Spitzenzeiten blockieren. Wenn Sie die Replikation blockieren, legen Sie den anderen Datenverkehr Priorität, aber Sie erhöhen auch die Replikations Latenz.  
  
Domänen Controller speichern Zeit in koordinierter Weltzeit (UTC). Die Zeit Einstellungen in den Plänen für Standort Verknüpfungs Objekte entsprechen der Ortszeit des Standorts und des Computers, auf dem der Zeitplan festgelegt ist. Wenn ein Domänen Controller einen Computer kontaktiert, der sich in einem anderen Standort und einer anderen Zeitzone befindet, zeigt der Zeitplan auf dem Domänen Controller die Zeiteinstellung gemäß der Ortszeit für den Standort des Computers an.  
  


