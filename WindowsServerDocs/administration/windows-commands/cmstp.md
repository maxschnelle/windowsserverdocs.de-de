---
title: cmstp
description: Referenz Thema für Cmstp, bei dem ein Verbindungs-Manager-Dienst Profil installiert oder entfernt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 34aad544-11c3-4e85-8bbf-5bc5a971da93
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 11d2ec5b09cfd9440eb22d66578061ddfb157539
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82712087"
---
# <a name="cmstp"></a>cmstp

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Installiert oder entfernt ein Verbindungs-Manager-Dienst Profil. Wenn Sie ohne optionale Parameter verwendet wird, installiert **Cmstp** ein Dienst Profil mit den Standardeinstellungen, die für das Betriebssystem und die Berechtigungen des Benutzers geeignet sind.

## <a name="syntax"></a>Syntax

Syntax 1: Dies ist die typische Syntax, die in einer benutzerdefinierten Installationsanwendung verwendet wird. Um diese Syntax zu verwenden, müssen Sie **Cmstp** aus dem Verzeichnis ausführen, in `<serviceprofilefilename>.exe` dem die Datei enthalten ist.

```
<serviceprofilefilename>.exe /q:a /c:cmstp.exe <serviceprofilefilename>.inf [/nf] [/s] [/u]
```

Syntax 2
```
cmstp.exe [/nf] [/s] [/u] [drive:][path]serviceprofilefilename.inf
```

#### <a name="parameters"></a>Parameter
| Parameter | BESCHREIBUNG |
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

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
