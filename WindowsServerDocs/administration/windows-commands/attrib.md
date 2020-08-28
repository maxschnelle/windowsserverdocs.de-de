---
title: attrib
description: Referenz Artikel für den atzb-Befehl, mit dem Attribute angezeigt, festgelegt oder entfernt werden, die Dateien oder Verzeichnissen zugewiesen sind.
ms.topic: reference
ms.assetid: 5e763ca5-21a2-45d2-b26d-a9c44c99091a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: de5d045421bb71feff70ec608f6b438fbf73942b
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89029228"
---
# <a name="attrib"></a>attrib

Hiermit werden Attribute angezeigt, festgelegt oder entfernt, die Dateien oder Verzeichnissen zugewiesen sind. Bei Verwendung ohne Parameter zeigt **atyb** Attribute aller Dateien im aktuellen Verzeichnis an.

## <a name="syntax"></a>Syntax

```
attrib [{+|-}r] [{+|-}a] [{+|-}s] [{+|-}h] [{+|-}i] [<drive>:][<path>][<filename>] [/s [/d] [/l]]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| `{+|-}r` | Legt das schreibgeschützte **+** Datei Attribut fest () oder löscht **-** Sie (). |
| `{+\|-}a` | Legt **+** das Archivdatei Attribut fest () oder löscht es ( **-** ). Dieses Attribut legt die Dateien fest, die sich seit der letzten Sicherung geändert haben. Beachten Sie, dass der **xcopy** -Befehl Archiv Attribute verwendet. |
| `{+\|-}s` | Legt **+** das System Datei Attribut fest () oder löscht es ( **-** ). Wenn in einer Datei dieser Attribut Satz verwendet wird, müssen Sie das-Attribut löschen, bevor Sie andere Attribute für die Datei ändern können. |
| `{+\|-}h` | Legt das ausgeblendete **+** Datei Attribut fest () oder löscht es ( **-** ). Wenn in einer Datei dieser Attribut Satz verwendet wird, müssen Sie das-Attribut löschen, bevor Sie andere Attribute für die Datei ändern können. |
| `{+\|-}i` | Legt ( **+** ) oder löscht ( **-** ) das nicht-Inhalts indizierte Datei Attribut. |
| `[<drive>:][<path>][<filename>]` | Gibt den Speicherort und den Namen des Verzeichnisses, der Datei oder der Gruppe von Dateien an, für die Sie Attribute anzeigen oder ändern möchten.<p>Sie können den **?** und **&#42;** Platzhalter Zeichen im *filename* -Parameter, um die Attribute für eine Gruppe von Dateien anzuzeigen oder zu ändern. |
| /s | Wendet **atungb** und alle Befehlszeilenoptionen auf übereinstimmende Dateien im aktuellen Verzeichnis und allen Unterverzeichnissen an. |
| /d | Wendet **attrb** und alle Befehlszeilenoptionen auf Verzeichnisse an. |
| /l | Wendet **atungb** und alle Befehlszeilenoptionen auf die symbolische Verknüpfung anstelle des Ziels der symbolischen Verknüpfung an. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um die Attribute einer Datei mit dem Namen News86 anzuzeigen, die sich im aktuellen Verzeichnis befindet:

```
attrib news86
```

Um das Attribut "schreibgeschützt" der Datei mit dem Namen "report.txt" zuzuweisen, geben Sie Folgendes ein:

```
attrib +r report.txt
```

Geben Sie Folgendes ein, um das schreibgeschützte Attribut aus den Dateien im öffentlichen Verzeichnis und seinen Unterverzeichnissen auf einem Datenträger auf Laufwerk b: zu entfernen:

```
attrib -r b:\public\*.* /s
```

Um das Archive-Attribut für alle Dateien auf Laufwerk a: festzulegen, und löschen Sie dann das Archiv Attribut für Dateien mit der Erweiterung. bak, geben Sie Folgendes ein:

```
attrib +a a:*.* & attrib -a a:*.bak
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [xcopy-Befehl](xcopy.md)
