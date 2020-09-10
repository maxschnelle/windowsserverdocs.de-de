---
title: cacls
description: Referenz Artikel für den Befehl cacls. Dieser Befehl ist veraltet und wird in zukünftigen Versionen von Windows nicht mehr unterstützt.
ms.topic: reference
ms.assetid: b5bdbaaa-4557-48b8-80df-e75ee0d2f27d
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 32be46658f47b534c80a9d9a712914aa6d878792
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89630019"
---
# <a name="cacls"></a>cacls

>[!IMPORTANT]
> Dieser Befehl ist veraltet. Verwenden Sie stattdessen [icacls](icacls.md) .

Hiermit werden freigegebene Zugriffs Steuerungs Listen (DACL) für angegebene Dateien angezeigt oder geändert.

## <a name="syntax"></a>Syntax

```
cacls <filename> [/t] [/m] [/l] [/s[:sddl]] [/e] [/c] [/g user:<perm>] [/r user [...]] [/p user:<perm> [...]] [/d user [...]]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `<filename>` | Erforderlich. Zeigt ACLs der angegebenen Dateien an. |
| /t | Ändert ACLs der angegebenen Dateien im aktuellen Verzeichnis und allen Unterverzeichnissen. |
| /m | Ändert ACLs von Volumes, die in ein Verzeichnis eingebunden sind. |
| /l | Funktioniert an der symbolischen Verknüpfung selbst anstelle des Ziels. |
| /s: SDDL | Ersetzt die ACLs durch die in der SDDL-Zeichenfolge angegebenen. Dieser Parameter ist für die Verwendung mit den Parametern **/e**, **/g**, **/r**, **/p**oder **/d** ungültig. |
| /e | Bearbeiten Sie eine ACL, anstatt Sie zu ersetzen. |
| /C | Fortfahren nach Fehlern beim Zugriff verweigert. |
| `/g user:<perm>` | Erteilt angegebene Benutzer Zugriffsrechte, einschließlich dieser gültigen Werte für die Berechtigung:<ul><li>**n** nicht zutreffend</li><li>**r** -lesen</li><li>**w** -schreiben</li><li>**c** -ändern (schreiben)</li><li>**f** -Vollzugriff</li></ul> |
| /r Benutzer [...] | Die Zugriffsrechte für den angegebenen Benutzer widerrufen. Nur gültig, wenn es mit dem **/e** -Parameter verwendet wird. |
| `[/p user:<perm> [...]` | Ersetzen Sie die Zugriffsrechte des angegebenen Benutzers, einschließlich der gültigen Werte für die Berechtigung:<ul><li>**n** nicht zutreffend</li><li>**r** -lesen</li><li>**w** -schreiben</li><li>**c** -ändern (schreiben)</li><li>**f** -Vollzugriff</li></ul> |
| [/d User [...] | Der angegebene Benutzer Zugriff wird verweigert. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="sample-output"></a>Beispielausgabe

| Output | Zugriffs Steuerungs Eintrag (ACE) gilt für |
-------- | ------------------------------------- |
| Zählen | Objekt erben. Dieser Ordner und die Dateien. |
| CI | Der Container erbt. Dieser Ordner und Unterordner. |
| IO | Nur erben. Der ACE gilt nicht für die aktuelle Datei bzw. das aktuelle Verzeichnis. |
| Keine Ausgabe Meldung | Nur dieser Ordner. |
| Zählen RKI | Dieser Ordner, die Unterordner und die Dateien. |
| Zählen RKI Brasilianer | Nur Unterordner und Dateien. |
| RKI Brasilianer | Nur Unterordner. |
| Zählen Brasilianer | Nur Dateien. |

#### <a name="remarks"></a>Hinweise

- Sie können Platzhalter verwenden (**?** und **&#42;**), um mehrere Dateien anzugeben.

- Sie können mehr als einen Benutzer angeben.

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [icacls](icacls.md)
