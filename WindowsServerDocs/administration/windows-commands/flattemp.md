---
title: flattemp
description: Referenz Artikel für den Befehl "flattemp", mit dem flattemporäre Ordner aktiviert oder deaktiviert werden.
ms.topic: reference
ms.assetid: 059a0960-1fd9-4382-87fe-a85d5dccdaea
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ac9a3ec390318d52d17f8e537eb10aad4bb1540c
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89030619"
---
# <a name="flattemp"></a>flattemp

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Aktiviert oder deaktiviert flattemporäre Ordner. Sie müssen über Administrator Anmelde Informationen verfügen, um diesen Befehl ausführen zu können.

> [!NOTE]
> Dieser Befehl ist nur verfügbar, wenn Sie den Remotedesktop-Sitzungshost-Rollen Dienst installiert haben.

## <a name="syntax"></a>Syntax

```
flattemp {/query | /enable | /disable}
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| /Query "aus | Fragt die aktuelle-Einstellung ab. |
| /enable | Aktiviert flattemporäre Ordner. Benutzer geben den temporären Ordner frei, es sei denn, der temporäre Ordner befindet sich im Basisordner des Benutzers. |
| /Disable | Deaktiviert flache temporäre Ordner. Der temporäre Ordner jedes Benutzers befindet sich in einem separaten Ordner (festgelegt durch die Sitzungs-ID des Benutzers). |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Bemerkungen

- Nachdem jeder Benutzer über einen eindeutigen temporären Ordner verfügt, verwenden `flattemp /enable` Sie, um flache temporäre Ordner zu aktivieren.

- Die Standardmethode zum Erstellen temporärer Ordner für mehrere Benutzer (in der Regel durch die Umgebungsvariablen TEMP und tmp) besteht darin, Unterordner im Ordner **\temp** zu erstellen, indem Sie die LogonId als Unterordner Namen verwenden. Wenn beispielsweise die Temp-Umgebungsvariable auf c:\temp zeigt, lautet der temporäre Ordner, der der Benutzer Anmelde-ID 4 zugewiesen ist, c:\Temp\4..

    Mithilfe von **flattemp**können Sie direkt auf den Ordner "\temp" zeigen und verhindern, dass Unterordner gebildet werden. Dies ist hilfreich, wenn Sie möchten, dass die temporären Benutzerordner in Basis Ordnern enthalten sind, egal ob auf einem lokalen Laufwerk Remotedesktop-Sitzungshost Server oder einem freigegebenen Netzwerklaufwerk. Verwenden Sie den `flattemp /enable*` Befehl nur, wenn jeder Benutzer über einen separaten temporären Ordner verfügt.

- Möglicherweise treten App-Fehler auf, wenn sich der temporäre Ordner des Benutzers auf einem Netzlaufwerk befindet. Dieser Fehler tritt auf, wenn das freigegebene Netzwerklaufwerk im Netzwerk vorübergehend nicht mehr verfügbar ist. Da die temporären Dateien der App entweder nicht zugänglich sind oder nicht synchronisiert sind, antwortet sie so, als ob der Datenträger angehalten wurde. Es wird nicht empfohlen, den temporären Ordner auf ein Netzwerklaufwerk zu verschieben. Der Standardwert besteht darin, temporäre Ordner auf der lokalen Festplatte beizubehalten. Wenn bei bestimmten Anwendungen unerwartetes Verhalten oder Datenträger Beschädigungs Fehler auftreten, stabilisieren Sie das Netzwerk, oder verschieben Sie die temporären Ordner zurück auf die lokale Festplatte.

- Wenn Sie die Verwendung separater temporärer Ordner pro Sitzung deaktivieren, werden die **flattemp** -Einstellungen ignoriert. Diese Option wird im Remotedesktopdienste-Konfigurationstool festgelegt.

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um die aktuelle Einstellung für flattemporär Ordner anzuzeigen:

```
flattemp /query
```

Geben Sie Folgendes ein, um flache temporäre Ordner zu aktivieren:

```
flattemp /enable
```

Um flache temporäre Ordner zu deaktivieren, geben Sie Folgendes ein:

```
flattemp /disable
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

