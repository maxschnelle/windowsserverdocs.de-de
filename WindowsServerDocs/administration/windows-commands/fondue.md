---
title: Fondue
description: Referenz Artikel für den Fondue-Befehl, der optionale Windows-Funktionen ermöglicht, indem Sie erforderliche Dateien von Windows Update oder einer anderen durch Gruppenrichtlinie angegebenen Quelle herunterladen.
ms.topic: reference
ms.assetid: fc4467f6-ddbb-4d6d-b51e-5a50a957b8c0
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 132441d48ce1f65b38955130fe19535775d02377
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89035068"
---
# <a name="fondue"></a>Fondue

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Aktiviert optionale Windows-Features, indem erforderliche Dateien aus Windows Update oder einer anderen durch Gruppenrichtlinie angegebenen Quelle heruntergeladen werden. Die Manifest-Datei für das Feature muss bereits in Ihrem Windows-Abbild installiert sein.

## <a name="syntax"></a>Syntax

```
fondue.exe /enable-feature:<feature_name> [/caller-name:<program_name>] [/hide-ux:{all | rebootrequest}]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| /Enable-Feature`<feature_name>` | Gibt den Namen des optionalen Windows-Features an, das Sie aktivieren möchten. Sie können nur eine Funktion pro Befehlszeile aktivieren. Um mehrere Features zu aktivieren, verwenden Sie fondue.exe für die einzelnen Features. |
| /caller-name:`<program_name>` | Gibt den Programm-oder Prozessnamen an, wenn Sie fondue.exe aus einem Skript oder einer Batchdatei abrufen. Sie können diese Option verwenden, um den Programmnamen dem sqm-Bericht hinzuzufügen, wenn ein Fehler vorliegt. |
| /hide-ux:`{all | rebootrequest}` | Mit **all** können Sie alle Nachrichten für den Benutzer ausblenden, einschließlich Fortschritts-und Berechtigungsanforderungen für den Zugriff auf Windows Update. Wenn die Berechtigung erforderlich ist, schlägt der Vorgang fehl.<p>Verwenden Sie **rebootrequest** , um nur Benutzer Meldungen auszublenden, die die Berechtigung zum Neustarten des Computers anfordern. Verwenden Sie diese Option, wenn Sie über ein Skript zum Steuern von Neustart Anforderungen verfügen. |

### <a name="examples"></a>Beispiele

Um Microsoft .NET Framework 4,8 zu aktivieren, geben Sie Folgendes ein:

```
fondue.exe /enable-feature:NETFX4
```

Wenn Sie Microsoft .NET Framework 4,8 aktivieren möchten, fügen Sie dem sqm-Bericht den Programmnamen hinzu, und zeigen Sie dem Benutzer keine Meldungen an, geben Sie Folgendes ein:

```
fondue.exe /enable-feature:NETFX4 /caller-name:Admin.bat /hide-ux:all
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Download von Microsoft .NET Framework 4,8](https://dotnet.microsoft.com/download/dotnet-framework/net48)
