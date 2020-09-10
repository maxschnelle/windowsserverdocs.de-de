---
title: extend
description: Referenz Artikel für den Erweiterungs Befehl, der das Volume oder die Partition mit dem Fokus und dem zugehörigen Dateisystem auf freien (nicht zugeordneten) Speicherplatz auf einem Datenträger erweitert.
ms.topic: reference
ms.assetid: 2414e21d-fc0b-40e8-9e33-3e072f8ad76b
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: dd654f2a648c86268721a87619f7b8832eaa34fe
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89635876"
---
# <a name="extend"></a>extend

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Erweitert das Volume oder die Partition mit dem Fokus und dem zugehörigen Dateisystem in den freien (nicht zugeordneten) Speicherplatz auf einem Datenträger.

## <a name="syntax"></a>Syntax

```
extend [size=<n>] [disk=<n>] [noerr]
extend filesystem [noerr]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| Größe =`<n>` | Gibt die Größe des Speicherplatzes in Megabyte (MB) an, der dem aktuellen Volume oder der aktuellen Partition hinzugefügt werden soll. Wenn keine Größe angegeben wird, wird der gesamte zusammenhängende freie Speicherplatz verwendet, der auf dem Datenträger verfügbar ist. |
| Festplatte =`<n>` | Gibt den Datenträger an, auf dem das Volume oder die Partition erweitert wird. Wenn kein Datenträger angegeben ist, wird das Volume oder die Partition auf dem aktuellen Datenträger erweitert. |
| filesystem | Erweitert das Dateisystem des Volumes mit dem Fokus. Zur Verwendung nur auf Datenträgern, auf denen das Dateisystem nicht mit dem Volume erweitert wurde. |
| Noerr | Nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird. |

#### <a name="remarks"></a>Hinweise

- Auf Basis Datenträgern muss sich der freie Speicherplatz auf demselben Datenträger wie das Volume oder die Partition mit dem Fokus befinden. Er muss auch direkt auf das Volume oder die Partition mit dem Fokus folgen (d. h., er muss beim nächsten sektoroffset beginnen).

- Auf dynamischen Datenträgern mit einfachen oder übergreifenden Volumes kann ein Volume auf einen beliebigen freien Speicherplatz auf jedem dynamischen Datenträger erweitert werden. Mit diesem Befehl können Sie ein einfaches dynamisches Volume in ein übergreifendes dynamisches Volume konvertieren. Gespiegelte, RAID-5-und Stripesetvolumes können nicht erweitert werden.

- Wenn die Partition zuvor mit dem NTFS-Dateisystem formatiert wurde, wird das Dateisystem automatisch erweitert, um die größere Partition auszufüllen, und es tritt kein Datenverlust auf.

- Wenn die Partition zuvor mit einem anderen Dateisystem als NTFS formatiert wurde, tritt bei dem Befehl ein Fehler auf, und die Partition wird nicht geändert.

- Wenn die Partition zuvor nicht mit einem Dateisystem formatiert wurde, wird die Partition weiterhin erweitert.

- Die Partition muss über ein zugeordnetes Volume verfügen, bevor Sie erweitert werden kann.

## <a name="examples"></a>Beispiele

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
