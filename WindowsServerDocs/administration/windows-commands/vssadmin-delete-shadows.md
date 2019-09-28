---
title: Löschen von Schatten durch vssadmin
description: Eine Beschreibung des Befehls "vssadmin DELETE Shadows".
ms.prod: windows-server
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 05/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9779da98ecb43245fe206390d9b70471f15d706e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71362613"
---
# <a name="vssadmin-delete-shadows"></a>Löschen von Schatten durch vssadmin

>Gilt für: Windows 10, Windows 8.1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

Löscht die Schatten Kopien eines angegebenen Volumes.

## <a name="syntax"></a>Syntax

```PowerShell
vssadmin delete shadows /for=<ForVolumeSpec> [/oldest | /all | /shadow=<ShadowID>] [/quiet]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---|---|
|/for = \<forvolumespec >|Gibt an, welche Schattenkopie des Volumes gelöscht wird.|
|/oldest|Löscht nur die älteste Schatten Kopie.|
|/All|Löscht alle Schatten Kopien des angegebenen Volumes.|
|/Shadow = \<shadowid >|Löscht die Schatten Kopie, die von shadowid angegeben wird. Verwenden Sie den Befehl " **vssadmin list shadows** ", um die Schattenkopiekennung zu erhalten. Wenn Sie eine schattenkopienkennung eingeben, verwenden Sie das folgende Format, wobei jedes *X* ein hexadezimales Zeichen darstellt:<br><br>XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX|
|/quiet|Gibt an, dass der Befehl keine Meldungen anzeigt, wenn er ausgeführt wird.|

## <a name="remarks"></a>Hinweise

Schatten Kopien können nur mit dem vom Client zugänglichen Typ gelöscht werden.

## <a name="examples"></a>Beispiele

Um die älteste Schatten Kopie von Volume C zu löschen, geben Sie den folgenden Befehl ein:

```PowerShell
vssadmin delete shadows /for=c: /oldest
```

## <a name="additional-references"></a>Weitere Verweise

* [Befehlszeilen-Syntax Schlüssel](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/cc771080(v%3dws.11))
* [Vssadmin](vssadmin.md)
* [Schatten der vssadmin-Liste](vssadmin-list-shadows.md)