---
ms.assetid: 385a2a7c-d6bd-4f11-9c18-fca0413f9e97
title: Nicht geändert
ms.prod: windows-server
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: cf3685bae9ed76ede4da6df244139437d92250c0
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80844333"
---
# <a name="fsutil-dirty"></a>Nicht geändert
>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8, Windows Server 2008 R2, Windows 7

Fragt das geänderte Bit eines Volumes ab oder legt es fest. Wenn das geänderte Bit eines Volumes festgelegt ist, überprüft **Autochk** automatisch das Volume auf Fehler, wenn der Computer das nächste Mal neu gestartet wird.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
fsutil dirty {query | set} <VolumePath>
```

### <a name="parameters"></a>Parameter

|   Parameter   |                                                 Beschreibung                                                  |
|---------------|--------------------------------------------------------------------------------------------------------------|
|     Abfrage     |                                  Fragt das geänderte Bit des angegebenen Volumes ab.                                   |
|      set      |                                    Legt das geänderte Bit des angegebenen Volumes fest.                                    |
| \<volumepath > | Gibt den Namen des Laufwerks gefolgt von einem Doppelpunkt oder einer GUID im folgenden Format an: **Volume {** <em>GUID</em> **}** . |

## <a name="remarks"></a>Hinweise

-   Das geänderte Bit eines Volumes gibt an, dass sich das Dateisystem möglicherweise in einem inkonsistenten Zustand befindet. Das Dirty-Bit kann aus folgenden Gründen festgelegt werden:

    -   Das Volume ist online und weist ausstehende Änderungen auf.

    -   Am Volume wurden Änderungen vorgenommen, und der Computer wurde heruntergefahren, bevor die Änderungen an den Datenträger übertragen wurden.

    -   Auf dem Volume wurde eine Beschädigung festgestellt.

-   Wenn das geänderte Bit beim Neustart des Computers festgelegt wird, wird **chkdsk** ausgeführt, um die Integrität des Dateisystems zu überprüfen und zu versuchen, Probleme mit dem Volume zu beheben.

## <a name="examples"></a><a name="BKMK_examples"></a>Beispiele
Geben Sie Folgendes ein, um das geänderte Bit auf Laufwerk C abzufragen:

```
fsutil dirty query c:
```

-   Wenn das Volume geändert wird, wird die folgende Ausgabe angezeigt:

    `Volume C: is dirty`

-   Wenn das Volume nicht geändert wird, wird die folgende Ausgabe angezeigt:

    `Volume C: is not dirty`

Geben Sie Folgendes ein, um das Dirty Bit auf Laufwerk C festzulegen:

```
fsutil dirty set C:
```

## <a name="additional-references"></a>Weitere Verweise
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

[Fsutil](Fsutil.md)


