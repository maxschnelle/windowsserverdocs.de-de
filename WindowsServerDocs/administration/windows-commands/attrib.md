---
title: attrib
description: Windows-Befehle Thema **Attrib** -zeigt, Mengen oder entfernt Attribute zugewiesen werden, in Dateien oder Verzeichnisse.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5e763ca5-21a2-45d2-b26d-a9c44c99091a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0f640af2c7957e43dd3f31dfa732bfc887112651
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59841091"
---
# <a name="attrib"></a>attrib



Zeigt an, legt diese fest oder entfernt Attribute, die Dateien oder Verzeichnisse zugewiesen. Wenn Sie ohne Angabe von Parametern **Attrib** zeigt die Attribute aller Dateien im aktuellen Verzeichnis an.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
attrib [{+|-}r] [{+|-}a] [{+|-}s] [{+|-}h] [{+|-}i] [<Drive>:][<Path>][<FileName>] [/s [/d] [/l]]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|{+\|-}r|Legt (**+**) oder deaktiviert (**-**) das Attribut für schreibgeschützte Datei.|
|{+\|-}a|Legt (**+**) oder deaktiviert (**-**) das Archivattribut für die Datei.|
|{+\|-}s|Legt (**+**) oder deaktiviert (**-**) das Attribut für Systemdatei.|
|{+\|-}h|Legt (**+**) oder deaktiviert (**-**) das Dateiattribut ausgeblendet.|
|{+\|-}i|Legt (**+**) oder deaktiviert (**-**) das Dateiattribut nicht Inhalt indiziert.|
|[\<Drive>:][<Path>][<FileName>]|Gibt den Speicherort und Namen des Verzeichnisses, Datei, oder der Gruppe von Dateien, die für die Sie anzeigen oder ändern möchten. Sie können die **?** und **&#42;** Platzhalterzeichen den *FileName* Parameter zum Anzeigen oder ändern Sie die Attribute für eine Gruppe von Dateien.|
|/s|Wendet **Attrib** und keine Befehlszeilenoptionen, die auf die entsprechenden Dateien im aktuellen Verzeichnis und alle seine Unterverzeichnisse.|
|/d|Wendet **Attrib** und keine Befehlszeilenoptionen zu Verzeichnissen.|
|/l|Wendet **Attrib** und keine Befehlszeilenoptionen, die die symbolische Verknüpfung, anstatt das Ziel der symbolischen Verknüpfung.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Sie können Platzhalterzeichen verwenden (**?** und **&#42;**) mit der *FileName* Parameter zum Anzeigen oder ändern Sie die Attribute für eine Gruppe von Dateien.
-   Wenn eine Datei auf das System verfügt (**s**) oder ausgeblendet (**h**)-Attribut festgelegt wurde, müssen Sie das Attribut löschen, bevor Sie alle anderen Attribute für diese Datei ändern können.
-   Das Attribut "Archive" (**eine**) Dateien, die sie gesichert wurden seit dem letzten geändert markiert. Beachten Sie, dass die **Xcopy** Befehl verwendet Attribute zu archivieren.

## <a name="BKMK_examples"></a>Beispiele für

Zum Anzeigen der Attribute einer Datei mit dem Namen News86, die im aktuellen Verzeichnis befindet, geben Sie Folgendes ein:
```
attrib news86 
```
Um das Schreibschutzattribut der Datei mit dem Namen Report.txt zuzuweisen, geben Sie Folgendes ein:
```
attrib +r report.txt 
```
Um das Schreibschutzattribut aus Dateien in der öffentlichen Verzeichnisses und seiner Unterverzeichnisse auf einem Datenträger im Laufwerk B zu entfernen, geben Sie Folgendes ein:
```
attrib -r b:\public\*.* /s 
```
Um das Archivattribut für alle Dateien auf Laufwerk A festgelegt, und deaktivieren Sie das Archivattribut für Dateien mit der BAK-Erweiterung, geben Sie Folgendes ein:
```
attrib +a a:*.* & attrib -a a:*.bak 
```
