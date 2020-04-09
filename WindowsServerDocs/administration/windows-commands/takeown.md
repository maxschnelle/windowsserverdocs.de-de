---
title: takeown
description: Erfahren Sie, wie Sie Zugriff auf eine Datei erhalten, indem Sie zum Besitzer der Datei werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0683cd65-a6db-4cab-962b-45a0ff61f43c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: af6952b8c4c14a717f7904ee0b77bf6ec9f5030e
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80833444"
---
# <a name="takeown"></a>takeown

Ermöglicht einem Administrator, Besitzer einer Datei zu werden, um so den zuvor verweigerten Zugriff auf diese Datei wiederherzustellen.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
takeown [/s <Computer> [/u [<Domain>\]<User name> [/p [<Password>]]]] /f <File name> [/a] [/r [/d {Y|N}]]
```

#### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/s \<Computer >|Gibt den Namen oder die IP-Adresse eines Remote Computers an (verwenden Sie keine umgekehrten Schrägstriche). Der Standardwert ist der lokale Computer. Dieser Parameter gilt für alle Dateien und Ordner, die im Befehl angegeben sind.|
|/u [\<Domänen >\]<User name>|Führt das Skript mit den Berechtigungen des angegebenen Benutzerkontos aus. Der Standardwert ist System Berechtigungen.|
|/p [\<Password >]|Gibt das Kennwort des Benutzerkontos an, das im **/u** -Parameter angegeben ist.|
|/f \<Dateiname >|Gibt den Dateinamen oder das Verzeichnis Namensmuster an. Sie können das Platzhalter Zeichen * verwenden, wenn Sie das Muster angeben. Sie können auch die Syntax *ShareName*\*filename * verwenden.|
|/a|Übergibt den Besitz der Gruppe "Administratoren" anstelle des aktuellen Benutzers.|
|/r|Führt einen rekursiven Vorgang für alle Dateien im angegebenen Verzeichnis und in den Unterverzeichnissen aus.|
|/d {Y \| N}|Unterdrückt die Bestätigungsaufforderung, die angezeigt wird, wenn der aktuelle Benutzer nicht über die Berechtigung "Ordner auflisten" für ein bestimmtes Verzeichnis verfügt, und verwendet stattdessen den angegebenen Standardwert. Gültige Werte für die **/d** -Option lauten wie folgt:</br>-Y: übernimmt den Besitz des Verzeichnisses.</br>-N: überspringen Sie das Verzeichnis.</br>Beachten Sie, dass Sie diese Option in Verbindung mit der **/r** -Option verwenden müssen.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Dieser Befehl wird in der Regel in Batch Dateien verwendet.
-   Wenn der **/a** -Parameter nicht angegeben wird, wird dem Benutzer, der derzeit am Computer angemeldet ist, der Dateibesitz erteilt.
-   Gemischte Muster mithilfe von ( **?** und **&#42;** ) werden vom Befehl " **takeown** " nicht unterstützt.
-   Nachdem Sie die Sperre mit **takeown**gelöscht haben, müssen Sie möglicherweise Windows-Explorer oder den Befehl **cacls** verwenden, um Ihnen vollständige Berechtigungen für die Dateien und Verzeichnisse zu übergeben, bevor Sie Sie löschen können. Weitere Informationen zu **cacls**finden Sie unter "Zusätzliche Verweise" am Ende dieses Themas.

## <a name="examples"></a><a name="BKMK_examples"></a>Beispiele

Geben Sie Folgendes ein, um den Besitz einer Datei namens lostfile zu übernehmen:
```
takeown /f lostfile
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)