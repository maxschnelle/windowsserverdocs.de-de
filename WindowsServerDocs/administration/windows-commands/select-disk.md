---
title: select disk
description: Referenz Artikel für den Befehl "Datenträger auswählen", der den angegebenen Datenträger auswählt und dann den Fokus verschiebt.
ms.topic: reference
ms.assetid: a0da614b-09d9-433b-b4eb-9127f84431cb
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 194bd36305060c8adfec27435ef05bf87605b45c
ms.sourcegitcommit: e164aeffc01069b8f1f3248bf106fcdb7f64f894
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/26/2020
ms.locfileid: "91389243"
---
# <a name="select-disk"></a>select disk

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Wählt den angegebenen Datenträger aus und verschiebt den Fokus auf ihn.

## <a name="syntax"></a>Syntax

```
select disk={<n>|<disk path>|system|next}
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| `<n>` | Gibt die Nummer des Datenträgers an, der den Fokus erhalten soll. Sie können die Zahlen für alle Datenträger auf dem Computer anzeigen, indem Sie den Befehl Datenträger **auflisten** in DiskPart verwenden.<p>**HINWEIS**<br>Wenn Sie Systeme mit mehreren Datenträgern konfigurieren, verwenden **Sie SELECT Disk = 0** nicht, um den System Datenträger anzugeben. Der Computer kann die Datenträger Nummern beim Neustart neu zuweisen, und verschiedene Computer mit der gleichen Datenträger Konfiguration können über unterschiedliche Datenträger Nummern verfügen. |
| `<disk path>` | Gibt den Speicherort des Datenträgers an, der den Fokus erhält, z `PCIROOT(0)#PCI(0F02)#atA(C00T00L00)` . b.. Zum Anzeigen des Speicher Orts eines Datenträgers wählen Sie diesen aus, und geben Sie dann **Detail**Datenträger ein. |
| System | Auf BIOS-Computern gibt diese Option an, dass Datenträger 0 den Fokus erhält. Auf EFI-Computern erhält der Datenträger, der die für den aktuellen Start verwendete EFI-Systempartition (ESP) enthält, den Fokus. Auf EFI-Computern schlägt der Befehl fehl, wenn kein ESP vorhanden ist, wenn mehr als ein ESP vorhanden ist oder wenn der Computer von Windows Preinstallation Environment (Windows PE) gestartet wird. |
| Weiter | Nachdem ein Datenträger ausgewählt wurde, durchläuft diese Option Alle Datenträger in der Liste der Datenträger. Wenn Sie diese Option ausführen, erhält der nächste Datenträger in der Liste den Fokus. |

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

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Partitions Befehl auswählen](select-partition.md)

- [Vdisk-Befehl auswählen](select-vdisk.md)

- [Befehl "Volume auswählen"](select-volume.md)
