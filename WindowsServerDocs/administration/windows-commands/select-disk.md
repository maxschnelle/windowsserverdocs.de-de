---
title: select disk
description: Referenz Artikel für * * * *-
ms.topic: reference
ms.assetid: a0da614b-09d9-433b-b4eb-9127f84431cb
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: b9f6461d22fa6ffcc9914e8edc6644a4b9364ece
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89635493"
---
# <a name="select-disk"></a>select disk

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

wählt den angegebenen Datenträger aus und verschiebt den Fokus auf ihn.



## <a name="syntax"></a>Syntax

```
select disk={ <n> | <disk path> | system | next }
```

> [!NOTE]
> Die **<disk path>** Parameter, **System**und **Next** sind nur in Windows 7 und Windows Server 2008 R2 verfügbar.

### <a name="parameters"></a>Parameter

|  Parameter  |                                                                                                                                                                                                            BESCHREIBUNG                                                                                                                                                                                                            |
|-------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     <n>     | Gibt die Nummer des Datenträgers an, der den Fokus erhalten soll. Sie können die Zahlen für alle Datenträger auf dem Computer anzeigen, indem Sie den Befehl Datenträger **auflisten** in DiskPart verwenden. **Hinweis:** Wenn Sie Systeme mit mehreren Datenträgern konfigurieren, dürfen Sie den System Datenträger nicht mithilfe von **select disk \= 0** angeben. Der Computer kann die Datenträger Nummern beim Neustart neu zuweisen, und verschiedene Computer mit der gleichen Datenträger Konfiguration können über unterschiedliche Datenträger Nummern verfügen. |
| <disk path> |                                                                                                                 Gibt den Speicherort des Datenträgers an, der den Fokus erhält, z. b. **pciroot \( 0 \) \# PCI \( 0f02 \) \# atA \( C00T00L00 \) **. Zum Anzeigen des Speicher Orts eines Datenträgers wählen Sie diesen aus, und geben Sie dann **Detail**Datenträger ein.                                                                                                                  |
|   System    |                                 Gibt auf BIOS-Computern an, dass Datenträger 0 den Fokus erhält. Auf EFI-Computern erhält der Datenträger mit der EFI-Systempartition \( ESP \) , die für den aktuellen Start verwendet wird, den Fokus. Auf EFI-Computern schlägt der Befehl fehl, wenn kein ESP vorhanden ist, wenn mehrere ESP vorhanden sind oder der Computer von Windows Preinstallation Environment \( Windows PE gestartet wird \) .                                  |
|    Weiter     |                                                                                                                                     Sobald ein Datenträger ausgewählt ist, durchläuft dieser Befehl alle Datenträger in der Liste der Datenträger. Wenn Sie diesen Befehl ausführen, erhält der nächste Datenträger in der Liste den Fokus.                                                                                                                                      |

## <a name="examples"></a>Beispiele
Um den Fokus auf Datenträger 1 zu verschieben, geben Sie Folgendes ein:

```
select disk=1
```

Geben Sie Folgendes ein, um einen Datenträger unter Verwendung des Speicher Orts Pfads auszuwählen:

```
select disk=PCIROOT(0)#PCI(0100)#atA(C00T00L01)
```

Zum Verschieben des Fokus auf den System Datenträger geben Sie Folgendes ein:

```
select disk=system
```

Wenn Sie den Fokus auf den nächsten Datenträger des Computers verschieben möchten, geben Sie Folgendes ein:

```
select disk=next
```

## <a name="additional-references"></a>Weitere Verweise
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)




