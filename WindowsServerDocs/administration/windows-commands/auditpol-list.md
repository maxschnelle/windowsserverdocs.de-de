---
title: Auditpol-Liste
description: Windows-Befehls Thema für **auditpol list**, das Überwachungs Richtlinien Kategorien und Unterkategorien auflistet oder Benutzer auflistet, für die eine Überwachungsrichtlinie pro Benutzer definiert ist.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 45502abe-3d6e-4e13-94f0-8e6fcb6db860
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9e0aff46e62ea4e4259360b78aae223dfcd66ef7
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851183"
---
# <a name="auditpol-list"></a>Auditpol-Liste

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Listet Überwachungs Richtlinien Kategorien und/oder Unterkategorien auf oder listet Benutzer auf, für die eine Überwachungsrichtlinie pro Benutzer definiert ist.

## <a name="syntax"></a>Syntax

```
auditpol /list
[/user|/category|subcategory[:<categoryname>|<{guid}>|*]]
[/v] [/r]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| ------- | -------- |
| /User | Ruft alle Benutzer ab, für die die Überwachungsrichtlinie pro Benutzer definiert wurde. Wenn Sie mit dem/v-Parameter verwendet wird, wird auch die Sicherheits-ID (SID) des Benutzers angezeigt. |
| /category | Zeigt die Namen der Kategorien an, die vom System interpretiert werden. Wenn Sie mit dem/v-Parameter verwendet wird, wird auch die Kategorie Globally Unique Identifier (GUID) angezeigt. |
| /SubCategory | Zeigt die Namen von Unterkategorien und ihre zugeordnete GUID an. |
| /v | Zeigt die GUID mit der Kategorie oder Unterkategorie an oder zeigt bei Verwendung mit/User die SID der einzelnen Benutzer an. |
| /r | Zeigt die Ausgabe als Bericht im CSV-Format (Comma-Separated Value, Komma getrennte Werte) an. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="remarks"></a>Hinweise

Für alle Listen Vorgänge für die Richtlinie pro Benutzer müssen Sie über die Berechtigung Lesen für das Objekt verfügen, das in der Sicherheits Beschreibung festgelegt ist. Sie können Listen Vorgänge auch durchführen, indem Sie das Benutzerrecht zum Verwalten von Überwachungs **-und Sicherheitsprotokollen** (SeSecurityPrivilege) besitzen. Dieses Recht ermöglicht jedoch zusätzlichen Zugriff, der nicht erforderlich ist, um den Auflistungs Vorgang auszuführen.

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Geben Sie Folgendes ein, um alle Benutzer mit einer definierten Überwachungsrichtlinie aufzulisten:

```
auditpol /list /user
```

Geben Sie Folgendes ein, um alle Benutzer mit einer definierten Überwachungsrichtlinie und ihrer zugeordneten sid aufzulisten:

```
auditpol /list /user /v
```

Um alle Kategorien und Unterkategorien im Berichtsformat aufzulisten, geben Sie Folgendes ein:

```
auditpol /list /subcategory:* /r
```

Geben Sie Folgendes ein, um die Unterkategorien der detaillierten nach Verfolgungs-und DS-Zugriffs Kategorien aufzulisten:

```
auditpol /list /subcategory:detailed Tracking,DS Access
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
