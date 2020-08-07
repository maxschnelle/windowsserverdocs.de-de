---
title: fsutil 8dot3name
description: Referenz Artikel für den Befehl "bsutil 8dot3name", der die Einstellungen für das Verhalten von Kurznamen (8dot3-Name) abfragt oder ändert.
manager: dmoss
ms.author: toklima
author: toklima
ms.assetid: a0c6dbfe-d898-496d-9356-825f7fbd90ec
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: 15d6b323248a51102b2ddcd6b2620722f22ae47a
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87890083"
---
# <a name="fsutil-8dot3name"></a>fsutil 8dot3name

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8

Abfragen oder Ändern der Einstellungen für das Verhalten des Kurznamens (8dot3 Name), das Folgendes umfasst:

- Abfragen der aktuellen Einstellung für das Kurznamen Verhalten.

- Der angegebene Verzeichnispfad wird auf Registrierungsschlüssel überprüft, die möglicherweise betroffen sind, wenn Kurznamen aus dem angegebenen Verzeichnispfad entfernt wurden.

- Ändern der Einstellung, die das Kurznamen Verhalten steuert. Diese Einstellung kann auf ein angegebenes Volume oder auf die standardvolumeeinstellung angewendet werden.

- Entfernen der Kurznamen für alle Dateien in einem Verzeichnis.

> [!IMPORTANT]
> Das permanente Entfernen von 8.3-Dateinamen und das Ändern von Registrierungs Schlüsseln, die auf die Dateinamen von 8.3 verweisen, kann zu unerwarteten Anwendungsfehlern führen, einschließlich der Unfähigkeit, eine Anwendung zu deinstallieren. Es wird empfohlen, zuerst das Verzeichnis oder das Volume zu sichern, bevor Sie versuchen, die Dateinamen von 8.3 zu entfernen.

## <a name="syntax"></a>Syntax

```
fsutil 8dot3name [query] [<volumepath>]
fsutil 8dot3name [scan] [/s] [/l [<log file>] ] [/v] <directorypath>
fsutil 8dot3name [set] { <defaultvalue> | <volumepath> {1|0}}
fsutil 8dot3name [strip] [/t] [/s] [/f] [/l [<log file.] ] [/v] <directorypath>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| Such`[<volumepath>]` | Fragt das Dateisystem nach dem Status des "8.3 Short Name Creation"-Verhaltens ab.<p>Wenn ein *volumepath* nicht als Parameter angegeben wird, wird die Standardeinstellung "8dot3name Creation Behavior" für alle Volumes angezeigt. |
| fein`<directorypath>` | Scannt die Dateien im angegebenen *directerypath* nach Registrierungs Schlüsseln, die möglicherweise betroffen sind, wenn 8.3-Kurznamen aus den Dateinamen entfernt wurden. |
| Set`<defaultvalue> | <volumepath>}` | Ändert das Dateisystem Verhalten für die 8.3-namens Erstellung in den folgenden Instanzen:<ul><li>Wenn *DefaultValue* angegeben wird, wird der Registrierungsschlüssel " **hklm\system\currentcontrolset\control\filesystem\ntfsdisable8dot3namecreationntfsdisable8dot3namecreationntfsdisable8dot3namecreation**" auf " *DefaultValue*" festgelegt.<p>Der *DefaultValue* kann die folgenden Werte aufweisen:<ul><li>**0**: aktiviert die Erstellung von 8.3-Namen für alle Volumes im System.</li><li>**1**: Hiermit wird die Erstellung von 8.3-Namen für alle Volumes im System deaktiviert.</li><li>**2**: legt die Erstellung eines 8.3-namens auf pro Volume fest.</li><li>**3**: Hiermit wird die Erstellung von 8.3-Namen für alle Volumes mit Ausnahme des System Volumes deaktiviert.</li></ul><li>Wenn ein *volumepath* angegeben wird, werden die angegebenen Volumes auf dem datenträgerflag 8dot3name-Eigenschaften so festgelegt, dass die Erstellung von 8.3-Namen für ein angegebenes**Volume (****0**) aktiviert wird.<p>Sie müssen das standardmäßige Dateisystem Verhalten für die Erstellung von 8.3-Namen auf den Wert **2** festlegen, bevor Sie die Erstellung von 8.3-Namen für ein bestimmtes Volume aktivieren oder deaktivieren können.</li></ul> |
| Platz`<directorypath>` | Entfernt die 8.3-Dateinamen für alle Dateien, die sich im angegebenen *Directoren Pfad*befinden. Der Dateiname 8.3 wird für keine Dateien entfernt, in denen *directoriypath* in Kombination mit dem Dateinamen mehr als 260 Zeichen enthält.<p>Dieser Befehl listet die Registrierungsschlüssel auf, die auf die Dateien verweisen, die 8.3-Dateinamen dauerhaft entfernt haben, jedoch nicht. |
| `<volumepath>` | Gibt den Namen des Laufwerks gefolgt von einem Doppelpunkt oder der GUID im Format an `volume{GUID}` . |
| /f | Gibt an, dass alle Dateien, die sich im angegebenen *directerypath* befinden, die 8.3-Dateinamen entfernt haben, auch wenn Registrierungsschlüssel vorhanden sind, die auf Dateien mit dem Dateinamen 8.3 verweisen. In diesem Fall entfernt der Vorgang die 8.3-Dateinamen, ändert jedoch keine Registrierungsschlüssel, die auf die Dateien verweisen, die die 8.3-Dateinamen verwenden. **Warnung:** Es wird empfohlen, dass Sie vor der Verwendung des Parameters **/f** das Verzeichnis oder das Volume sichern, da dies zu unerwarteten Anwendungsfehlern führen kann, einschließlich der Unfähigkeit, Programme zu deinstallieren. |
| /l`[<log file>]` | Gibt eine Protokolldatei an, in der Informationen geschrieben werden.<p>Wenn der **/l** -Parameter nicht angegeben wird, werden alle Informationen in die Standardprotokoll Datei geschrieben: `%temp%\8dot3_removal_log@(GMT YYYY-MM-DD HH-MM-SS)` . log * * |
| /s | Gibt an, dass der Vorgang auf die Unterverzeichnisse des angegebenen *directoryPath*angewendet werden soll. |
| /t | Gibt an, dass das Entfernen von 8 DOT3-Dateinamen im Testmodus ausgeführt werden soll. Alle Vorgänge außer dem tatsächlichen Entfernen der 8.3-Dateinamen werden ausgeführt. Sie können den Testmodus verwenden, um zu ermitteln, welche Registrierungsschlüssel auf Dateien verweisen, die die 8.3-Dateinamen verwenden. |
| /v | Gibt an, dass alle Informationen, die in die Protokolldatei geschrieben werden, auch in der Befehlszeile angezeigt werden. |

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um das namens Verhalten von 8.3 für ein Datenträger Volume abzufragen, das mit der GUID {928842df-5a01-11de-a85c-806e6f6e6963} angegeben ist:

```
fsutil 8dot3name query volume{928842df-5a01-11de-a85c-806e6f6e6963}
```

Sie können das 8.3-namens Verhalten auch mit dem Unterbefehl **Verhalten** Abfragen.

Wenn Sie die Dateinamen von 8.3 im Verzeichnis " *d:\mydata* " und in allen Unterverzeichnissen entfernen möchten, während Sie die Informationen in die Protokolldatei schreiben, die als *MyLogFile. log*angegeben ist, geben Sie Folgendes ein:

```
fsutil 8dot3name strip /l mylogfile.log /s d:\MyData
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [fsutil](fsutil.md)

- [fsutil behavior](fsutil-behavior.md)
