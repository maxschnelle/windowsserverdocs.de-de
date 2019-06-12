---
title: mountvol
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fea8ad4d-f04a-4aaa-a3e5-75931e867b39
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 03e7cefc7c7a00338972fc365b7c25d9c795c83e
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66437280"
---
# <a name="mountvol"></a>mountvol



Erstellt, löscht oder einen Volumebereitstellungspunkt aufgeführt.

Beispiele zur Verwendung mit diesem Befehl finden Sie [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
mountvol [<Drive>:]<Path VolumeName>
mountvol [<Drive>:]<Path> /d
mountvol [<Drive>:]<Path> /l
mountvol [<Drive>:]<Path> /p
mountvol /r
mountvol [/n | /e]
mountvol <Drive>: /s
```

## <a name="parameters"></a>Parameter

|     Parameter     |                                                                                                                           Beschreibung                                                                                                                            |
|-------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [\<Drive>:]<Path> |                                                                                             Gibt an, der vorhandenen NTFS-Verzeichnis, in dem der Bereitstellungspunkt gespeichert wird.                                                                                             |
|   \<VolumeName>   |                     Gibt an, die Volumename, die das Ziel des Bereitstellungspunkts ist. Die Volumename verwendet die folgende Syntax, wobei *GUID* ist ein global eindeutiger Bezeichner:</br>`\\\\?\Volume\{GUID}\`</br>Die Klammern {} sind erforderlich.                      |
|        /d         |                                                                                                    Entfernt den Volumebereitstellungspunkt aus dem angegebenen Ordner.                                                                                                     |
|        /l         |                                                                                                     Listet den Namen des bereitgestellten Volumes, für den angegebenen Ordner.                                                                                                      |
|        /p         | Entfernt den Volumebereitstellungspunkt im angegebenen Verzeichnis, hebt die Bereitstellung der Basisvolumes und nimmt das einfache Volume offline, somit unmountable. Wenn das Volume von anderen Prozessen verwendet werden **Mountvol** schließt alle offenen Handles vor der Bereitstellung des Volumes aufgehoben. |
|        /r         |             Entfernt Volume Punkt Bereitstellungsverzeichnisse und registrierungseinstellungen für Volumes, die nicht mehr im System verhindert, dass sie automatisch bereitgestellt werden und ihre erste Volumebereitstellungspunkt erhalten, wenn das System wieder hinzugefügt.              |
|        /n         |                                                                      Deaktiviert die automatische Bereitstellung von neuen Basisvolumes. Neue Volumes werden nicht automatisch bereitgestellt werden, wenn dem System hinzugefügt.                                                                       |
|        / e         |                                                                                                       Wird die automatische Bereitstellung von neuen Basisvolumes erneut aktiviert.                                                                                                        |
|        /s         |                                                                                Bindet die EFI-Systempartition auf dem angegebenen Laufwerk. Nur Itanium-basierten Computern verfügbar.                                                                                |
|        /?         |                                                                                                               Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                               |

## <a name="remarks"></a>Hinweise

-   **Mountvol** können Sie Volumes ohne einen Laufwerkbuchstaben zu verknüpfen.
-   Volumes, deren Bereitstellung aufgehoben werden, mithilfe von **/p** finden Sie in der Volumeliste als "Nicht bereitgestellt UNTIL ein Volumebereitstellungspunkt erstellt wird." Wenn das Volume mehrere Bereitstellungspunkte zeigen aufweist, verwenden Sie **/d** So entfernen Sie die zusätzlichen Bereitstellungspunkte vor der Verwendung von **/p**. Sie können das Basisvolume erneut bereitgestellt werden können, indem ein Volumebereitstellungspunkt zuweisen.
-   Wenn Sie der Speicherplatz eines Datenträgers zu erweitern, ohne zu formatieren oder eine Festplatte zu ersetzen müssen, können Sie einen Bereitstellungspfad auf ein anderes Volume hinzufügen. Der Vorteil der Verwendung von einem Volume mit mehreren Bereitstellungspfaden ist, dass Sie alle lokalen Volumes zugreifen können, mit einem einzelnen Laufwerkbuchstaben (z. B. `C:`). Sie müssen nicht daran denken, welches Volume der Laufwerkbuchstabe entspricht – Obwohl Sie immer noch können lokale Volumes bereitstellen und diese Laufwerkbuchstaben zuweisen.

## <a name="BKMK_examples"></a>Beispiele für

Um einen Bereitstellungspunkt erstellen möchten, geben Sie Folgendes ein:
```
mountvol \sysmount \\?\Volume\{2eca078d-5cbc-43d3-aff8-7e8511f60d0e}\
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)