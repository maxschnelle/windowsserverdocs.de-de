---
title: Erweitern
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 2414e21d-fc0b-40e8-9e33-3e072f8ad76b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 11991f9fc338dca5201d8f9c9c598b9d7dcf239b
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80844783"
---
# <a name="extend"></a>Erweitern

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

erweitert das Volume oder die Partition mit dem Fokus und dem zugehörigen Dateisystem in freien \(nicht zugeordneten\) Speicherplatz auf einem Datenträger.  
  
  
  
## <a name="syntax"></a>Syntax  
  
```  
extend [size=<n>] [disk=<n>] [noerr]  
extend filesystem [noerr]  
```  
  
### <a name="parameters"></a>Parameter  
  
| Parameter  |                                                                                             Beschreibung                                                                                              |
|------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Größe\=<n>  |      Gibt die Größe des Speicherplatzes in Megabyte \(MB an\) der dem aktuellen Volume oder der Partition hinzugefügt werden soll. Wenn keine Größe angegeben wird, wird der gesamte zusammenhängende freie Speicherplatz verwendet, der auf dem Datenträger verfügbar ist.       |
| Datenträger\=<n>  |                          Gibt den Datenträger an, auf dem das Volume oder die Partition erweitert wird. Wenn kein Datenträger angegeben ist, wird das Volume oder die Partition auf dem aktuellen Datenträger erweitert.                          |
| Verwendet |                                   erweitert das Dateisystem des Volumes mit dem Fokus. Zur Verwendung nur auf Datenträgern, auf denen das Dateisystem nicht mit dem Volume erweitert wurde.                                    |
|   Noerr    | Nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird. |
  
## <a name="remarks"></a>Hinweise  
  
-   Auf Basis Datenträgern muss sich der freie Speicherplatz auf demselben Datenträger wie das Volume oder die Partition mit dem Fokus befinden. Er muss auch unmittelbar auf das Volume oder die Partition mit dem Fokus \(, d. h., er muss beim nächsten sektoroffset\)beginnen.  
  
-   Auf dynamischen Datenträgern mit einfachen oder übergreifenden Volumes kann ein Volume auf einen beliebigen freien Speicherplatz auf jedem dynamischen Datenträger erweitert werden. Mit diesem Befehl können Sie ein einfaches dynamisches Volume in ein übergreifendes dynamisches Volume konvertieren. Gespiegelte RAID-\-5-und Stripesetvolumes können nicht erweitert werden.  
  
-   Wenn die Partition zuvor mit dem NTFS-Dateisystem formatiert wurde, wird das Dateisystem automatisch erweitert, um die größere Partition auszufüllen, und es tritt kein Datenverlust auf.  
  
-   Wenn die Partition zuvor mit einem anderen Dateisystem als NTFS formatiert wurde, tritt bei dem Befehl ein Fehler auf, und die Partition wird nicht geändert.  
  
-   Wenn die Partition zuvor nicht mit einem Dateisystem formatiert wurde, wird die Partition weiterhin erweitert.  
  
-   Die Partition muss über ein zugeordnetes Volume verfügen, bevor Sie erweitert werden kann.  
  
## <a name="examples"></a><a name=BKMK_examples></a>Beispiele  
Geben Sie Folgendes ein, um das Volume oder die Partition mit dem Fokus um 500 Megabyte zu erweitern:  
  
```  
extend size=500 disk=3  
```  
  
Um das Dateisystem eines Volumes nach der Erweiterung zu erweitern, geben Sie Folgendes ein:  
  
```  
extend filesystem  
```  
  
## <a name="additional-references"></a>Weitere Verweise  
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
  

  

