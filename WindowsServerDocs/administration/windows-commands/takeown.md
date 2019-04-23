---
title: takeown
description: Erfahren Sie, wie Sie Zugriff auf eine Datei zu erhalten, indem Sie zu der Besitzer der Datei.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0683cd65-a6db-4cab-962b-45a0ff61f43c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4b5a4874edf9fa4406d4643e686fed2b725699dd
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59854361"
---
# <a name="takeown"></a>takeown

Ermöglicht einem Administrator, Besitzer einer Datei zu werden, um so den zuvor verweigerten Zugriff auf diese Datei wiederherzustellen.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
takeown [/s <Computer> [/u [<Domain>\]<User name> [/p [<Password>]]]] /f <File name> [/a] [/r [/d {Y|N}]]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/ s \<Computer >|Gibt den Namen oder die IP-Adresse eines Remotecomputers (umgekehrte Schrägstriche nicht verwenden). Der Standardwert ist der lokale Computer. Dieser Parameter gilt für alle Dateien und Ordner, die im Befehl angegeben.|
|/u [\<Domain>\]<User name>|Führt das Skript mit den Berechtigungen des angegebenen Benutzerkontos. Der Standardwert ist die Systemberechtigungen.|
|/ p [\<Kennwort >]|Gibt das Kennwort des Benutzerkontos ein, die im angegebenen die **/u** Parameter.|
|/ f \<Dateiname >|Gibt an, die Datei- oder Verzeichnisname Muster. Sie können das Platzhalterzeichen * Wenn Sie das Muster angeben. Sie können auch die Syntax *ShareName*\*FileName *.|
|/a|Überträgt den Besitz der Gruppe "Administratoren" anstelle des aktuellen Benutzers.|
|/r|Führt einen Vorgang rekursiv für alle Dateien im angegebenen Verzeichnis und den Unterverzeichnissen.|
|/d {Y \| N}|Unterdrückt die bestätigungsaufforderung, die angezeigt wird, wenn der aktuelle Benutzer verfügt nicht über die "Ordner auflisten"-Berechtigung in einem angegebenen Verzeichnis und stattdessen den angegebenen Standardwert verwendet. Gültige Werte für die **/d** Option lauten wie folgt:</br>-   Y: Übernehmen des Besitzes des Verzeichnisses.</br>-   N: Überspringen Sie das Verzeichnis an.</br>Beachten Sie, dass Sie diese Option verwenden müssen, in Verbindung mit der **/r** Option.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Mit diesem Befehl wird in der Regel in Batchdateien verwendet.
-   Wenn die **/a** Parameter nicht angegeben ist, Dateibesitz erhält der Benutzer, die derzeit auf dem Computer angemeldet ist.
-   Mithilfe von Mustern (**?** und **&#42;**) werden nicht unterstützt, indem **Takeown** Befehl.
-   Nach dem Löschen der Sperre mit **Takeown**, möglicherweise müssen Sie die Windows-Explorer verwenden, oder die **"Cacls" ein** Befehl aus, um sich selbst Vollzugriff auf die Dateien und Verzeichnisse erteilen, bevor Sie sie löschen können. Weitere Informationen zu **"Cacls" ein**, finden Sie unter "Weitere Referenzen" am Ende dieses Themas.

## <a name="BKMK_examples"></a>Beispiele für

Um den Besitz einer Datei mit dem Namen Dateiname nutzen zu können, geben Sie Folgendes ein:
```
takeown /f lostfile
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)