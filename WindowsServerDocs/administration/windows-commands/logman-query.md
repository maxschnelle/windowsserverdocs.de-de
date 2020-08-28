---
title: logman query
description: Referenz Artikel für den Logman Query-Befehl, der die Eigenschaften des Daten Sammlers oder des Datensammler Satzes abfragt.
ms.topic: reference
ms.assetid: 1116a0f0-5415-4369-a045-12f79f8f66de
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e7d3d9da5b5885c15135b764454bd68818c4aded
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89023784"
---
# <a name="logman-query"></a>logman query

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Fragt Eigenschaften des Daten Sammlers oder des Datensammler Satzes ab.

## <a name="syntax"></a>Syntax

```
logman query [providers|Data Collector Set name] [options]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| -s `<computer name>` | Führen Sie den Befehl auf dem angegebenen Remote Computer aus. |
| -config `<value>` | Gibt die Einstellungsdatei an, die Befehlsoptionen enthält. |
| [-n] `<name>` | Name des Zielobjekts |
| -ETS | Sendet Befehle direkt an Ereignis Ablauf Verfolgungs Sitzungen, ohne zu speichern oder zu planen. |
| /? | Zeigt die kontextbezogene Hilfe an. |

### <a name="examples"></a>Beispiele

Um alle auf dem Zielsystem konfigurierten Datensammler Sätze aufzulisten, geben Sie Folgendes ein:

```
logman query
```

Um die Datensammler aufzulisten, die im Datensammler Satz mit dem Namen *perf_log*enthalten sind, geben Sie Folgendes ein:

```
logman query perf_log
```

Um alle verfügbaren Anbieter von Datensammlern auf dem Zielsystem aufzulisten, geben Sie Folgendes ein:

```
logman query providers
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [logman-Befehl](logman.md)
