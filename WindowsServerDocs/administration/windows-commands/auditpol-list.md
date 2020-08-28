---
title: auditpol list
description: Referenz Artikel für den Befehl auditpol list, der Überwachungs Richtlinien Kategorien und Unterkategorien auflistet oder Benutzer auflistet, für die eine Überwachungsrichtlinie pro Benutzer definiert ist.
ms.topic: reference
ms.assetid: 45502abe-3d6e-4e13-94f0-8e6fcb6db860
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b49b138de8f25f25b00e593d6bd02620a3f2f624
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89029078"
---
# <a name="auditpol-list"></a>auditpol list

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Listet Überwachungs Richtlinien Kategorien und Unterkategorien auf oder listet Benutzer auf, für die eine Überwachungsrichtlinie pro Benutzer definiert ist.

Zum Ausführen von *Listen* Vorgängen für die Richtlinie *pro Benutzer* müssen Sie über die Berechtigung **Lesen** für das Objekt verfügen, das in der Sicherheits Beschreibung festgelegt ist. Sie können auch *Listen* Vorgänge ausführen, wenn Sie über das Benutzerrecht zum Verwalten von Überwachungs **-und Sicherheitsprotokollen** (SeSecurityPrivilege) verfügen. Dieses Recht ermöglicht jedoch zusätzlichen Zugriff, der nicht erforderlich ist, um die Gesamt *Liste* der Vorgänge auszuführen.

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

## <a name="examples"></a>Beispiele

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

- [Auditpol-Befehle](auditpol.md)
