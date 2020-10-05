---
title: takeown
description: Referenz Artikel für den Befehl "takeown", der es einem Administrator ermöglicht, den Zugriff auf eine Datei wiederherzustellen, die zuvor verweigert wurde.
ms.topic: reference
ms.assetid: 0683cd65-a6db-4cab-962b-45a0ff61f43c
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 34fce5000a0a8c91123a2ebd4765bf4cbb00a289
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/05/2020
ms.locfileid: "91718237"
---
# <a name="takeown"></a>takeown

Ermöglicht einem Administrator, Besitzer einer Datei zu werden, um so den zuvor verweigerten Zugriff auf diese Datei wiederherzustellen. Dieser Befehl wird in der Regel für Batch Dateien verwendet.

## <a name="syntax"></a>Syntax

```
takeown [/s <computer> [/u [<domain>\]<username> [/p [<password>]]]] /f <filename> [/a] [/r [/d {Y|N}]]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| /s `<computer>` | Gibt den Namen oder die IP-Adresse eines Remote Computers an (verwenden Sie keine umgekehrten Schrägstriche). Der Standardwert ist der lokale Computer. Dieser Parameter gilt für alle Dateien und Ordner, die im Befehl angegeben sind. |
| /u `[<domain>\]<username>` | Führt das Skript mit den Berechtigungen des angegebenen Benutzerkontos aus. Der Standardwert ist System Berechtigungen. |
| /p `[<[password>]` | Gibt das Kennwort des Benutzerkontos an, das im **/u** -Parameter angegeben ist. |
| /f `<filename>` | Gibt den Dateinamen oder das Verzeichnis Namensmuster an. Sie können das Platzhalter Zeichen verwenden, `*` Wenn Sie das Muster angeben. Sie können auch die Syntax verwenden `<sharename>\<filename>` . |
| /a | Übergibt den Besitz der Gruppe "Administratoren" anstelle des aktuellen Benutzers. Wenn Sie diese Option nicht angeben, wird dem Benutzer, der derzeit am Computer angemeldet ist, der Dateibesitz erteilt. |
| /r | Führt einen rekursiven Vorgang für alle Dateien im angegebenen Verzeichnis und in den Unterverzeichnissen aus. |
| /d `{Y | N}` | Unterdrückt die Bestätigungsaufforderung, die angezeigt wird, wenn der aktuelle Benutzer nicht über die Berechtigung **Ordner auflisten** für ein bestimmtes Verzeichnis verfügt, und verwendet stattdessen den angegebenen Standardwert. Gültige Werte für die **/d** -Option sind:<ul><li>**Y** : übernimmt den Besitz des Verzeichnisses.</li><li>**N** -überspringen Sie das Verzeichnis.<p>**HINWEIS**<br>Sie müssen diese Option in Verbindung mit der **/r** -Option verwenden.</li></ul> |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="remarks"></a>Bemerkungen

- Gemischte Muster mithilfe von (**?** und **&#42;**) werden nicht vom Befehl " **takeown** " unterstützt.

- Nachdem Sie die Sperre mit **takeown**gelöscht haben, müssen Sie möglicherweise Windows-Explorer verwenden, um Ihnen vollständige Berechtigungen für die Dateien und Verzeichnisse zu vergeben, bevor Sie Sie löschen können.

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um den Besitz einer Datei namens *lostfile*zu übernehmen:

```
takeown /f lostfile
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
