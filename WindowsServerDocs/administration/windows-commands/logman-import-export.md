---
title: logman import and logman export
description: Referenz Artikel zu logman Import und logman Export, der einen Datensammler Satz aus einer XML-Datei importiert oder einen Datensammler Satz in eine XML-Datei exportiert.
ms.topic: reference
ms.assetid: c258daba-fb93-47c0-a53b-2fe83ed2c743
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: eeb0c30011b70a6fa72bffca18b16ec11e27b958
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89639985"
---
# <a name="logman-import-and-logman-export"></a>logman import and logman export

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Importiert einen Datensammler Satz aus einer XML-Datei oder exportiert einen Datensammler Satz in eine XML-Datei.

## <a name="syntax"></a>Syntax

```
logman import <[-n] <name> <-xml <name> [options]
logman export <[-n] <name> <-xml <name> [options]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| -s `<computer name>` | Führen Sie den Befehl auf dem angegebenen Remote Computer aus. |
| -config `<value>` | Gibt die Einstellungsdatei an, die Befehlsoptionen enthält. |
| [-n] `<name>` | Name des Zielobjekts |
| -XML `<name>` | Der Name der XML-Datei, die importiert oder exportiert werden soll. |
| -ETS | Sendet Befehle direkt an Ereignis Ablauf Verfolgungs Sitzungen, ohne zu speichern oder zu planen. |
| -[-] u `<user [password]>` | Gibt den Benutzer an, der als ausgeführt werden soll. Wenn Sie `*` für das Kennwort eingeben, wird eine Eingabeaufforderung für das Kennwort ausgegeben. Das Kennwort wird nicht angezeigt, während Sie es an der Eingabeaufforderung eingeben. |
| -y | Antworten auf Ja für alle Fragen ohne Aufforderung. |
| /? | Zeigt die kontextbezogene Hilfe an. |

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um die XML-Datei *c:\windows\perf_log.xml* vom Computer *server_1* als Datensammler Satz mit dem Namen *perf_log*zu importieren:

```
logman import perf_log -s server_1 -xml c:\windows\perf_log.xml
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [logman-Befehl](logman.md)
