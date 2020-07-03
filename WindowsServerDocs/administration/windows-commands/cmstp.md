---
title: cmstp
description: Referenz Artikel für Cmstp, bei dem ein Verbindungs-Manager-Dienst Profil installiert oder entfernt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 34aad544-11c3-4e85-8bbf-5bc5a971da93
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8f7bc7bc4b90dced8074fa685ad79c65747e0ded
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85929814"
---
# <a name="cmstp"></a>cmstp

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Installiert oder entfernt ein Verbindungs-Manager-Dienst Profil. Wenn Sie ohne optionale Parameter verwendet wird, installiert **Cmstp** ein Dienst Profil mit den Standardeinstellungen, die für das Betriebssystem und die Berechtigungen des Benutzers geeignet sind.

## <a name="syntax"></a>Syntax

Syntax 1: Dies ist die typische Syntax, die in einer benutzerdefinierten Installationsanwendung verwendet wird. Um diese Syntax zu verwenden, müssen Sie **Cmstp** aus dem Verzeichnis ausführen, in dem die Datei enthalten ist `<serviceprofilefilename>.exe` .

```
<serviceprofilefilename>.exe /q:a /c:cmstp.exe <serviceprofilefilename>.inf [/nf] [/s] [/u]
```

Syntax 2
```
cmstp.exe [/nf] [/s] [/u] [drive:][path]serviceprofilefilename.inf
```

#### <a name="parameters"></a>Parameter
| Parameter | Beschreibung |
| --------- | ----------- |
| `<serviceprofilefilename>.exe` | Gibt anhand des Namens das Installationspaket an, das das zu installierende Profil enthält.<p>Erforderlich für Syntax 1, aber nicht gültig für Syntax 2. |
| /q:a | Gibt an, dass das Profil installiert werden soll, ohne den Benutzer aufzufordern. Die Überprüfungs Meldung, dass die Installation erfolgreich war, wird weiterhin angezeigt.<p>Erforderlich für Syntax 1, aber nicht gültig für Syntax 2. |
| [Laufwerk:] ADS`<serviceprofilefilename>.inf` | Erforderlich. Gibt den Namen der Konfigurationsdatei an, die bestimmt, wie das Profil installiert werden soll.<p>Der [Laufwerk:] [Pfad]-Parameter ist für Syntax 1 ungültig. |
| /nf | Gibt an, dass die Unterstützungs Dateien nicht installiert werden sollen. |
| /s | Gibt an, dass das Dienst Profil im Hintergrund installiert oder deinstalliert werden soll (ohne Aufforderung zur Eingabe eines Benutzers oder zum Anzeigen der Überprüfungs Meldung). Dies ist der einzige Parameter, den Sie in Kombination mit **/u**verwenden können.|
| /U | Gibt an, dass das Dienst Profil deinstalliert werden soll. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um das *unfiktive* Dienst Profil ohne Unterstützungs Dateien zu installieren:

```
fiction.exe /c:cmstp.exe fiction.inf /nf
```

Geben Sie Folgendes ein, *um das Benutzer* Profil für einen einzelnen Benutzer automatisch zu installieren:

```
fiction.exe /c:cmstp.exe fiction.inf /s /su
```

Geben Sie Folgendes ein, *um das Dienst* Profil für den-Typ im Hintergrund

```
fiction.exe /c:cmstp.exe fiction.inf /s /u
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
