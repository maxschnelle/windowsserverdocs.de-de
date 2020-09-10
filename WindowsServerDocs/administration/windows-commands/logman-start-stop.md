---
title: logman start and logman stop
description: Referenz Artikel für die Befehle "Logman Start" und "Logman Stopp", die einen Datensammler starten und die Startzeit auf "manuell" festlegen oder einen Datensammler Satz beenden und die Endzeit auf "manuell" festlegen.
ms.topic: reference
ms.assetid: a40006a1-876e-474b-aaf1-f365c730deea
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 9a684eb010d52e5aba01fee609f878cc5485a7d5
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89639969"
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

| Parameter | BESCHREIBUNG |
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
