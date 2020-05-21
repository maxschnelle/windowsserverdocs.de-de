---
title: nicht geändert
description: Referenz Thema für den Befehl "bereinigen" mit dem Befehl "", der das geänderte Bit eines Volumes abfragt oder festlegt.
ms.prod: windows-server
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
ms.assetid: 385a2a7c-d6bd-4f11-9c18-fca0413f9e97
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: 72defd974177675f53e89fb8570f028580b7e167
ms.sourcegitcommit: bf887504703337f8ad685d778124f65fe8c3dc13
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/16/2020
ms.locfileid: "83435865"
---
# <a name="fsutil-dirty"></a>nicht geändert

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

#### <a name="remarks"></a>Hinweise

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

    If the volume is dirty, the following output displays:

    `Volume C: is dirty`

    If the volume isn't dirty, the following output displays:

    `Volume C: is not dirty`

Geben Sie Folgendes ein, um das Dirty Bit auf Laufwerk C festzulegen:

```
fsutil dirty set C:
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [fsutil](fsutil.md)
