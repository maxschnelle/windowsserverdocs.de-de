---
title: logman Start und logman beendet
description: Referenz Thema für die Befehle "Logman Start" und "Logman Stopp", die einen Datensammler starten und die Startzeit auf "manuell" festlegen oder einen Datensammler Satz beenden und die Endzeit auf "Manual" festlegen.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: a40006a1-876e-474b-aaf1-f365c730deea
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: db0111c4f58f0a28ad76affd3e4d8e24d4a927c2
ms.sourcegitcommit: 29bc8740e5a8b1ba8f73b10ba4d08afdf07438b0
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/30/2020
ms.locfileid: "84222918"
---
# <a name="logman-start-and-logman-stop"></a>logman Start und logman beendet

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
| -s`<computer name>` | Führen Sie den Befehl auf dem angegebenen Remote Computer aus. |
| -config`<value>` | Gibt die Einstellungsdatei an, die Befehlsoptionen enthält. |
| [-n]`<name>` | Gibt den Namen des Zielobjekts an. |
| -ETS | Sendet Befehle direkt an Ereignis Ablauf Verfolgungs Sitzungen, ohne zu speichern oder zu planen. |
| -AS | Führt den angeforderten Vorgang asynchron aus. |
| -? | Zeigt die kontextbezogene Hilfe an. |

### <a name="examples"></a>Beispiele

Geben Sie zum Starten des Daten Sammlers *perf_log*auf dem Remote Computer *server_1*Folgendes ein:

```
logman start perf_log -s server_1
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [logman-Befehl](logman.md)
