---
title: mountvol
description: 'Windows-Befehle Thema ****- '
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
ms.openlocfilehash: 07c57f7ab9c41d6155e4a8d38322176aabf3868f
ms.sourcegitcommit: 6f968368c12b9dd699c197afb3a3d13c2211f85b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/26/2019
ms.locfileid: "68544601"
---
# <a name="mountvol"></a>mountvol



Erstellt, löscht oder listet einen volumeeinstellungspunkt auf.

Beispiele für die Verwendung dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

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

|Parameter|Beschreibung|
|---------|-----------|
|[\<Laufwerk >:]<Path>|Gibt das vorhandene NTFS-Verzeichnis an, in dem sich der Einstellungspunkt befinden soll.|
|\<Volumename->|Gibt den Volumenamen an, der das Ziel des Bereitstellungs Punkts ist. Der Volumename verwendet die folgende Syntax, wobei *GUID* eine Globally Unique Identifier ist:</br>`\\\\?\Volume\{GUID}\`</br>Die Klammern "{}" sind erforderlich.|
|/d|Entfernt den volumeeinstellungspunkt aus dem angegebenen Ordner.|
|/l|Listet den Namen des bereitgestellten Volumes für den angegebenen Ordner auf.|
|/p|Der Volumebereitstellungspunkt wird aus dem angegebenen Verzeichnis entfernt, die Bereitstellung des Basis Volumes wird aufgehoben, und das Basis Volume wird offline geschaltet. Wenn das Volume von anderen Prozessen verwendet wird, schließt **mountvol** alle geöffneten Handles, bevor das Volume getrennt wird.|
|/r|Entfernt Volumes für das Volumebereitstellungspunkt und die Registrierungs Einstellungen für Volumes, die sich nicht mehr im System befinden, sodass Sie nicht automatisch bereitgestellt werden und ihre früheren Volumebereitstellungspunkte beim Hinzufügen wieder zum System erhalten.|
|/n|Deaktiviert die automatische Einbindung neuer Basisvolumes. Neue Volumes werden nicht automatisch bereitgestellt, wenn Sie dem System hinzugefügt werden.|
|/e|Aktiviert die automatische Einbindung neuer Basisvolumes erneut.|
|/s|Stellt die EFI-Systempartition auf dem angegebenen Laufwerk bereit.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Mithilfe von **mountvol** können Sie Volumes verknüpfen, ohne einen Laufwerk Buchstaben zu benötigen.
-   Volumes, die mit **/p** disbereit gestellt werden, werden in der Liste der Volumes als "nicht bereitgestellt, bis ein Volume-Einfügepunkt erstellt wurde" aufgeführt. Wenn das Volume über mehrere Einfügepunkte verfügt, verwenden Sie **/d** , um die zusätzlichen Einfügepunkte vor der Verwendung von **/p**zu entfernen. Sie können das Basisvolume erneut einbinden, indem Sie einen Volumebereitstellungspunkt zuweisen.
-   Wenn Sie den volumespeicherplatz erweitern müssen, ohne eine Festplatte neu zu formatieren oder zu ersetzen, können Sie einen Einfügungs Pfad einem anderen Volume hinzufügen. Der Vorteil der Verwendung eines Volumes mit mehreren einstellungenpfaden besteht darin, dass Sie mit einem einzelnen Laufwerk Buchstaben (z `C:`. b.) auf alle lokalen Volumes zugreifen können. Sie müssen nicht merken, welches Volume welchem Laufwerk Buchstaben entspricht – obwohl Sie trotzdem lokale Volumes einbinden und Ihnen Laufwerk Buchstaben zuweisen können.

## <a name="BKMK_examples"></a>Beispiele

Geben Sie zum Erstellen eines Einfügepunkts Folgendes ein:
```
mountvol \sysmount \\?\Volume\{2eca078d-5cbc-43d3-aff8-7e8511f60d0e}\
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
