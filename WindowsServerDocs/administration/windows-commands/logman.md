---
title: logman
description: Referenz Thema für den Befehl logman, mit dem Ereignis Ablauf Verfolgungs Sitzung und Leistungs Protokolle erstellt und verwaltet werden und die zahlreiche Funktionen des System Monitors von der Befehlszeile aus unterstützt werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 574a5203-5b3b-4759-a678-f26d00dde447
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 44b5e134440d71eed61ca8e03739abcc962df1f9
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2020
ms.locfileid: "83820550"
---
# <a name="logman"></a>logman

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Erstellt und verwaltet die Protokolle zu Ereignisablaufverfolgungssitzungen und die Leistungsprotokolle und unterstützt viele Funktionen des Systemmonitors von der Befehlszeile aus.

## <a name="syntax"></a>Syntax

```
logman [create | query | start | stop | delete| update | import | export | /?] [options]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| [logman create](logman-create.md) | Erstellt einen Counter, eine Ablauf Verfolgung, einen Konfigurationsdaten Sammler oder eine API. |
| [logman query](logman-query.md) | Fragt Datensammler Eigenschaften ab. |
| [logman start &#124; stop](logman-start-stop.md) | Startet oder beendet die Datensammlung. |
| [logman delete](logman-delete.md) | Löscht einen vorhandenen Datensammler. |
| [logman update](logman-update.md) | Aktualisiert die Eigenschaften eines vorhandenen Daten Sammlers. |
| [logman import &#124; export](logman-import-export.md) | Importiert einen Datensammler Satz aus einer XML-Datei oder exportiert einen Datensammler Satz in eine XML-Datei. |

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)