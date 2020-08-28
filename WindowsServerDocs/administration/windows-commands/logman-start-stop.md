---
title: logman start and logman stop
description: Referenz Artikel für die Befehle "Logman Start" und "Logman Stopp", die einen Datensammler starten und die Startzeit auf "manuell" festlegen oder einen Datensammler Satz beenden und die Endzeit auf "manuell" festlegen.
ms.topic: reference
ms.assetid: a40006a1-876e-474b-aaf1-f365c730deea
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5b573ecd78ad9f062162d2c1ad16d59aebe740ee
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89038861"
---
# <a name="logman-start-and-logman-stop"></a>logman start and logman stop

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Der **logman Start** -Befehl startet einen Datensammler und legt die Startzeit auf Manual fest. Der " **logman Stopp** "-Befehl hält einen Datensammler Satz an und legt die Endzeit auf "Manual" fest.

## <a name="syntax"></a>Syntax

```
logman start <[-n] <name>> [options]
logman stop <[-n] <name>> [options]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| -s `<computer name>` | Führen Sie den Befehl auf dem angegebenen Remote Computer aus. |
| -config `<value>` | Gibt die Einstellungsdatei an, die Befehlsoptionen enthält. |
| [-n] `<name>` | Gibt den Namen des Zielobjekts an. |
| -ETS | Sendet Befehle direkt an Ereignis Ablauf Verfolgungs Sitzungen, ohne zu speichern oder zu planen. |
| -AS | Führt den angeforderten Vorgang asynchron aus. |
| -? | Zeigt die kontextbezogene Hilfe an. |

### <a name="examples"></a>Beispiele

Geben Sie zum Starten des Daten Sammlers *perf_log*auf dem Remote Computer *server_1*Folgendes ein:

```
logman start perf_log -s server_1
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [logman-Befehl](logman.md)
