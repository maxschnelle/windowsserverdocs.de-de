---
title: enthalten, wobei
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0b3486a5-896b-4d92-84b8-e463a0b76487
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ff50405dd53ee383abc8e13f67befecf73e37c1d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59832451"
---
# <a name="where"></a>enthalten, wobei



Zeigt den Speicherort der Dateien, die das angegebenen Suchmuster entsprechen.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
where [/r <Dir>] [/q] [/f] [/t] [$<ENV>:|<Path>:]<Pattern>[ ...] 
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/r \<Dir>|Gibt an, eine rekursive Suche, die im angegebenen Verzeichnis ab.|
|/q|Gibt einen Exitcode zurück (**0** für Erfolg, **1** für Fehler) ohne die Liste der übereinstimmenden Dateien anzuzeigen.|
|/f|Zeigt die Ergebnisse der **, in denen** Befehl in Anführungszeichen ein.|
|/t|Zeigt die Größe und das Datum der letzten Änderung und die Uhrzeit der einzelnen übereinstimmenden Dateien.|
|[$\<ENV >:\|\<Pfad >:]\<Muster > [...]|Gibt das Suchmuster für die Dateien entsprechend an. Mindestens ein Muster ist erforderlich, und das Muster kann Platzhalterzeichen enthalten (**&#42;** und **?**). In der Standardeinstellung **, in denen** sucht das aktuelle Verzeichnis und den Pfaden, die in der PATH-Umgebungsvariablen angegeben werden. Sie können angeben, einen anderen Pfad suchen, indem Sie unter Verwendung der $ Format*ENV*:*Muster* (, in denen *ENV* ist eine vorhandene Umgebungsvariable, die eine oder mehrere Pfade enthalten) oder mithilfe von das Format *Pfad*:*Muster* (wobei *Pfad* ist der Verzeichnispfad, der Sie suchen möchten). Diese optionale Formate sollten nicht verwendet werden, mit der **/r** Befehlszeilenoption.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Wenn Sie keine Dateinamenerweiterung angeben, werden die Erweiterungen, die in der Umgebungsvariablen PATHEXT aufgelisteten Muster standardmäßig angefügt.
-   **Wo** können rekursive Suchvorgänge ausführen, Anzeigen von Informationen wie z. B. Datum oder die Größe und akzeptieren Sie die Umgebungsvariablen anstelle von Pfaden auf dem lokalen Computer.

## <a name="BKMK_examples"></a>Beispiele für

Um alle Dateien, die mit dem Namen "Test", in dem Laufwerk C des dem aktuellen Computer und seinen Unterverzeichnissen zu suchen, geben Sie Folgendes ein:
```
where /r c:\ test 
```
Um alle Dateien in das Verzeichnis öffentlich aufzuführen, geben Sie Folgendes ein:
```
where $public:*.*
```
Um alle Dateien, die mit dem Namen "Editor", in dem Laufwerk C des Remotecomputers, Computer1 und seinen Unterverzeichnissen zu suchen, geben Sie Folgendes ein:
```
where /r \\computer1\c notepad.*
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)