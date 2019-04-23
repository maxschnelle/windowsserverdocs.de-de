---
title: set_2
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: acf24663-1a50-4321-b48d-1717655e9476
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3f5523646fddbfec31cb3900fc09230efc1c7813
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59862611"
---
# <a name="set2"></a>set_2



Legt fest, der Kontext, Optionen, ausführlichen Modus und Metadatendatei für die Erstellung von Schattenkopien. Wenn Sie ohne Angabe von Parametern **festgelegt** Listet alle aktuelle Einstellungen.

## <a name="syntax"></a>Syntax

```
set
set context {clientaccessible | persistent [nowriters] | volatile [nowriters]}
set option {[differential | plex] [transportable] [[rollbackrecover] [txfrecover] | [noautorecover]]}
set verbose {on|off}
set metadata <MetaData.cab>
```

## <a name="set-sub-commands"></a>Untergeordnete "Set"-Befehlen

|Unterbefehl|Beschreibung|
|-----------|-----------|
|Kontext|Legt den Kontext für die Erstellung von Schattenkopien fest. Finden Sie unter [Kontext festlegen](set-context.md) für die Syntax und Parameter.|
|option|Legt Optionen für die Erstellung von Schattenkopien fest. Finden Sie unter [legen Option](set-option.md) für die Syntax und Parameter.|
|Ausführlich|Aktiviert die ausführliche Ausgabe-Modus an, aktivieren oder deaktivieren. Finden Sie unter [festgelegt ausführliche](set-verbose.md) für die Syntax und Parameter.|
|metadata|Legt fest, den Namen und Speicherort der Datei mit den Schatten erstellen. Finden Sie unter [Resultsetmetadaten](set-metadata.md) für die Syntax und Parameter.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)