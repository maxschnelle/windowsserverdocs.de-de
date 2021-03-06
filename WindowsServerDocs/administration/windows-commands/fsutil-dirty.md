---
title: fsutil dirty
description: Referenz Artikel für den Befehl "fehlerhaft", der das geänderte Bit eines Volumes abfragt oder festlegt.
manager: dmoss
ms.author: toklima
author: toklima
ms.assetid: 385a2a7c-d6bd-4f11-9c18-fca0413f9e97
ms.topic: reference
ms.date: 10/16/2017
ms.openlocfilehash: fa63ec550821f99dffa59f092bb0f0523bfb948b
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89030148"
---
# <a name="fsutil-dirty"></a>fsutil dirty

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8

Fragt das geänderte Bit eines Volumes ab oder legt es fest. Wenn das geänderte Bit eines Volumes festgelegt ist, überprüft **Autochk** automatisch das Volume auf Fehler, wenn der Computer das nächste Mal neu gestartet wird.

## <a name="syntax"></a>Syntax

```
fsutil dirty {query | set} <volumepath>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| Abfrage | Fragt das geänderte Bit des angegebenen Volumes ab. |
| set | Legt das geänderte Bit des angegebenen Volumes fest. |
| `<volumepath>` | Gibt den Namen des Laufwerks gefolgt von einem Doppelpunkt oder einer GUID im folgenden Format an: `volume{GUID}` . |

#### <a name="remarks"></a>Bemerkungen

- Das geänderte Bit eines Volumes gibt an, dass sich das Dateisystem möglicherweise in einem inkonsistenten Zustand befindet. Das Dirty-Bit kann aus folgenden Gründen festgelegt werden:

    - Das Volume ist online und weist ausstehende Änderungen auf.

    - Am Volume wurden Änderungen vorgenommen, und der Computer wurde heruntergefahren, bevor die Änderungen an den Datenträger übertragen wurden.

    - Auf dem Volume wurde eine Beschädigung festgestellt.

- Wenn das geänderte Bit beim Neustart des Computers festgelegt wird, wird **chkdsk** ausgeführt, um die Integrität des Dateisystems zu überprüfen und zu versuchen, Probleme mit dem Volume zu beheben.

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um das geänderte Bit auf Laufwerk C abzufragen:

```
fsutil dirty query c:
```

- Wenn das Volume geändert wird, wird die folgende Ausgabe angezeigt: `Volume C: is dirty`

- Wenn das Volume nicht geändert wird, wird die folgende Ausgabe angezeigt: `Volume C: is not dirty`

Geben Sie Folgendes ein, um das Dirty Bit auf Laufwerk C festzulegen:

```
fsutil dirty set C:
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [fsutil](fsutil.md)
