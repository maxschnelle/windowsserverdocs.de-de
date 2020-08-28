---
title: Löschen von Schatten durch vssadmin
description: Eine Beschreibung des Befehls "vssadmin DELETE Shadows".
ms.topic: reference
author: JasonGerend
ms.author: jgerend
ms.date: 05/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: 667aaa7477666c6128aaed4ddb10a9f3695e571a
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89022864"
---
# <a name="vssadmin-delete-shadows"></a>Löschen von Schatten durch vssadmin

> Gilt für: Windows 10, Windows 8.1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

Löscht die Schatten Kopien eines angegebenen Volumes.

## <a name="syntax"></a>Syntax

```PowerShell
vssadmin delete shadows /for=<ForVolumeSpec> [/oldest | /all | /shadow=<ShadowID>] [/quiet]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---|---|
|/for =\<ForVolumeSpec>|Gibt an, welche Schattenkopie des Volumes gelöscht wird.|
|/oldest|Löscht nur die älteste Schatten Kopie.|
|/all|Löscht alle Schatten Kopien des angegebenen Volumes.|
|/Shadow =\<ShadowID>|Löscht die Schatten Kopie, die von shadowid angegeben wird. Verwenden Sie den Befehl " **vssadmin list shadows** ", um die Schattenkopiekennung zu erhalten. Wenn Sie eine schattenkopienkennung eingeben, verwenden Sie das folgende Format, wobei jedes *X* ein hexadezimales Zeichen darstellt:<br><br>xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx|
|/quiet|Gibt an, dass der Befehl keine Meldungen anzeigt, wenn er ausgeführt wird.|

## <a name="remarks"></a>Bemerkungen

Schatten Kopien können nur mit dem vom Client zugänglichen Typ gelöscht werden.

## <a name="examples"></a>Beispiele

Um die älteste Schatten Kopie von Volume C zu löschen, geben Sie den folgenden Befehl ein:

```PowerShell
vssadmin delete shadows /for=c: /oldest
```

## <a name="additional-references"></a>Weitere Verweise

* [Befehlszeilen-Syntax Schlüssel](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/cc771080(v%3dws.11))
* [Vssadmin](vssadmin.md)
* [Vssadmin list shadows](vssadmin-list-shadows.md)
