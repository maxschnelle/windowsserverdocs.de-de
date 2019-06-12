---
ms.assetid: 385a2a7c-d6bd-4f11-9c18-fca0413f9e97
title: Fsutil geändert
ms.prod: windows-server-threshold
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: d8a5c4905991203a051fea360ed91c9b372f6993
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66439086"
---
# <a name="fsutil-dirty"></a>Fsutil geändert
>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, WindowsServer 2012, Windows 8, Windows Server 2008 R2, Windows 7

Abfragen, oder legt diesen fest dirty Bit des Volumes. Wenn ein Volume geändert ist Bit festgelegt ist, **Autochk** automatisch geprüft, ob das Volume für Fehler beim nächsten des Computers Neustart.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
fsutil dirty {query | set} <VolumePath>
```

## <a name="parameters"></a>Parameter

|   Parameter   |                                                 Beschreibung                                                  |
|---------------|--------------------------------------------------------------------------------------------------------------|
|     query     |                                  Fragt dirty Bit von dem angegebenen Volume.                                   |
|      set      |                                    Legt das angegebene Volume dirty Bit fest.                                    |
| \<VolumePath> | Gibt den Namen des Laufwerks, gefolgt von einem Doppelpunkt oder GUID im folgenden Format an: **Volume {** <em>GUID</em> **}** . |

## <a name="remarks"></a>Hinweise

-   Dirty Bit des Volumes gibt an, dass es sich bei das Dateisystem in einem inkonsistenten Zustand sein kann. Das dirty Bit kann festgelegt werden, da:

    -   Das Volume online ist und die ausstehenden Änderungen.

    -   Es wurden Änderungen vorgenommen, auf dem Volume, und der Computer wurde heruntergefahren, bevor die Änderungen auf den Datenträger geschrieben wurden.

    -   Auf dem Volume wurde eine Beschädigung festgestellt.

-   Wenn das dirty Bit festgelegt ist, wenn der Computer neu gestartet wird, **Chkdsk** ausgeführt wird, um die Integrität des Dateisystems zu überprüfen und versucht, Probleme mit dem Volume zu beheben.

## <a name="BKMK_examples"></a>Beispiele für
Um das dirty Bit auf Laufwerk C abzufragen, geben Sie Folgendes ein:

```
fsutil dirty query c:
```

-   Wenn das Volume geändert wurde, wird die folgende Ausgabe angezeigt:

    `Volume C: is dirty`

-   Wenn das Volume nicht geändert wurde, wird die folgende Ausgabe angezeigt:

    `Volume C: is not dirty`

Um das dirty Bit auf Laufwerk C festzulegen, geben Sie Folgendes ein:

```
fsutil dirty set C:
```

#### <a name="additional-references"></a>Weitere Verweise
[Erläuterung zur Befehlszeilensyntax](Command-Line-Syntax-Key.md)

[Fsutil](Fsutil.md)


