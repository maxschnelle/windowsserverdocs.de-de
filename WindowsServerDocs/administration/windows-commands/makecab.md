---
title: makecab
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4da95297-c593-427b-9f76-2f389c46cbf4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e353f2f97ef55e806d991b45018755847fca0364
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59871401"
---
# <a name="makecab"></a>makecab

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Verpacken Sie vorhandene Dateien in einer CAB-Datei.
## <a name="syntax"></a>Syntax
```
makecab [/v[n]] [/d var=<value> ...] [/l <dir>] <source> [<destination>]
makecab [/v[<n>]] [/d var=<value> ...] /f <directives_file> [...]
```
### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|<source>|Datei komprimieren.|
|<destination>|Der Dateiname für komprimierte Datei ein. Wenn nicht angegeben, ist das letzte Zeichen der Name der Quelldatei mit einem Unterstrich (_) ersetzt und als Ziel verwendet.|
|/f <directives_file>|Eine Datei mit **Makecab** Directives (wiederholt werden).|
|/ d Var =<value>|Definiert die Variable mit dem angegebenen Wert.|
|/l <dir>|Speicherort für Ziel (die Standardeinstellung ist aktuelles Verzeichnis).|
|/v[<n>]|Ein debugging Ausführlichkeitsgrad festzulegen (0 = none gilt,..., 3 = full).|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|
## <a name="remarks"></a>Hinweise
-   Finden Sie unter [Microsoft Cabinet-Format](https://go.microsoft.com/fwlink/?LinkId=226852) auf MSDN, um Informationen zu Directive_file.

## <a name="additional-references"></a>Zusätzliche Referenzen
-   [Befehlszeilensyntax](command-line-syntax-key.md)

