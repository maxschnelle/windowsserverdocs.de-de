---
title: logman
description: Referenz Artikel für den Befehl logman, der Ereignis Ablauf Verfolgungs Sitzung und Leistungs Protokolle erstellt und verwaltet und viele Funktionen des System Monitors von der Befehlszeile aus unterstützt.
ms.topic: reference
ms.assetid: 574a5203-5b3b-4759-a678-f26d00dde447
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b155e3cca0b9f5e35c1c817cfee4e96ca79b6610
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89030548"
---
# <a name="logman"></a>logman

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Erstellt und verwaltet die Protokolle zu Ereignisablaufverfolgungssitzungen und die Leistungsprotokolle und unterstützt viele Funktionen des Systemmonitors von der Befehlszeile aus.

## <a name="syntax"></a>Syntax

```
logman [create | query | start | stop | delete| update | import | export | /?] [options]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| [logman create](logman-create.md) | Erstellt einen Counter, eine Ablauf Verfolgung, einen Konfigurationsdaten Sammler oder eine API. |
| [logman query](logman-query.md) | Fragt Datensammler Eigenschaften ab. |
| [logman start &#124; stop](logman-start-stop.md) | Startet oder beendet die Datensammlung. |
| [logman delete](logman-delete.md) | Löscht einen vorhandenen Datensammler. |
| [logman update](logman-update.md) | Aktualisiert die Eigenschaften eines vorhandenen Daten Sammlers. |
| [logman import &#124; export](logman-import-export.md) | Importiert einen Datensammler Satz aus einer XML-Datei oder exportiert einen Datensammler Satz in eine XML-Datei. |

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)