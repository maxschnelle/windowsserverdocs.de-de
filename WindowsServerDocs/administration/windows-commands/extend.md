---
title: Erweitern
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2414e21d-fc0b-40e8-9e33-3e072f8ad76b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6fdf070a733392d89bafe5bed5a1bf23d8e24d57
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66439354"
---
# <a name="extend"></a>Erweitern

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Erweitert das Volume oder eine Partition mit einer Fokussierung und das Dateisystem in kostenlosen \(nicht zugeordneten\) Speicherplatz auf einem Datenträger.  
  
  
  
## <a name="syntax"></a>Syntax  
  
```  
extend [size=<n>] [disk=<n>] [noerr]  
extend filesystem [noerr]  
```  
  
## <a name="parameters"></a>Parameter  
  
| Parameter  |                                                                                             Beschreibung                                                                                              |
|------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Größe\=<n>  |      Gibt die Menge des Speicherplatzes in Megabyte \(MB\) so die aktuellen Volume oder eine Partition hinzu. Wenn keine Größe angegeben wird, werden alle dem freien Speicherplatz, der auf dem Datenträger verfügbar ist verwendet.       |
| disk\=<n>  |                          Gibt den Datenträger, auf dem das Volume oder die Partition erweitert wird. Wenn kein Laufwerk angegeben wird, wird das Volume oder eine Partition auf dem aktuellen Datenträger erweitert.                          |
| Dateisystem |                                   Erweitert das Dateisystem des Volumes mit dem Fokus. Für die Verwendung nur auf Datenträgern, in dem das Dateisystem mit dem Volume nicht erweitert wurde.                                    |
|   Diskpart    | nur für Skripts. Wenn ein Fehler gefunden wird, weiterhin DiskPart Befehle zu verarbeiten, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter wird ein Fehler DiskPart mit dem Fehlercode zu beenden. |
  
## <a name="remarks"></a>Hinweise  
  
-   Auf Basisdatenträgern muss der freie Speicherplatz auf dem gleichen Datenträger wie das Volume oder eine Partition mit dem Fokus. Es muss auch unmittelbar folgen, das Volume oder eine Partition mit dem Fokus \(, also müssen Sie sich an den nächsten Versatz von Sektor starten\).  
  
-   Auf dynamischen Datenträgern mit einfachen oder übergreifenden Volumes kann ein Volume in freie Bereiche auf jedem dynamischen Datenträger erweitert werden. Mit diesem Befehl können Sie ein einfaches dynamisches Volume in ein dynamisches übergreifendes Volume konvertieren. Gespiegelt, RAID\-5 und Stripesetvolumes können nicht erweitert werden.  
  
-   Wenn die Partition zuvor mit dem NTFS-Dateisystem formatiert wurde, im Dateisystem wird automatisch erweitert, um die größere Partition zu füllen, und es erfolgt keine Daten verloren gehen.  
  
-   Wenn die Partition bereits mit einem Dateisystem als NTFS formatiert wurde, schlägt der Befehl keine Änderung an der Partition.  
  
-   Wenn die Partition nicht zuvor mit einem Dateisystem formatiert wurde, wird die Partition noch erweitert werden.  
  
-   Die Partition benötigen eine zugehörige Volume aus, bevor es erweitert werden kann.  
  
## <a name="BKMK_examples"></a>Beispiele für  
Geben Sie Folgendes ein, um das Volume oder eine Partition mit dem Fokus von 500 MB an, auf dem Datenträger 3, zu erweitern:  
  
```  
extend size=500 disk=3  
```  
  
Um das Dateisystem eines Volumes zu erweitern, nachdem er erweitert wurde, geben Sie Folgendes ein:  
  
```  
extend filesystem  
```  
  
#### <a name="additional-references"></a>Zusätzliche Referenzen  
[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
  

  

