---
title: Importieren und logman-Export von logman
description: Referenz Thema für logman Import und logman Export, das einen Datensammler Satz aus einer XML-Datei importiert oder einen Datensammler Satz in eine XML-Datei exportiert.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c258daba-fb93-47c0-a53b-2fe83ed2c743
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ce18c615d45d4922c8819d30ff47d54328111170
ms.sourcegitcommit: 29bc8740e5a8b1ba8f73b10ba4d08afdf07438b0
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/30/2020
ms.locfileid: "84222939"
---
# <a name="logman-import-and-logman-export"></a>Importieren und logman-Export von logman

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Importiert einen Datensammler Satz aus einer XML-Datei oder exportiert einen Datensammler Satz in eine XML-Datei.

## <a name="syntax"></a>Syntax

```
logman import <[-n] <name>> <-xml <name>> [options]
logman export <[-n] <name>> <-xml <name>> [options]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| -s`<computer name>` | Führen Sie den Befehl auf dem angegebenen Remote Computer aus. |
| -config`<value>` | Gibt die Einstellungsdatei an, die Befehlsoptionen enthält. |
| [-n]`<name>` | Name des Zielobjekts |
| -XML`<name>` | Der Name der XML-Datei, die importiert oder exportiert werden soll. |
| -ETS | Sendet Befehle direkt an Ereignis Ablauf Verfolgungs Sitzungen, ohne zu speichern oder zu planen. |
| -[-] u`<user [password]>` | Gibt den Benutzer an, der als ausgeführt werden soll. Wenn Sie `*` für das Kennwort eingeben, wird eine Eingabeaufforderung für das Kennwort ausgegeben. Das Kennwort wird nicht angezeigt, während Sie es an der Eingabeaufforderung eingeben. |
| -y | Antworten auf Ja für alle Fragen ohne Aufforderung. |
| /? | Zeigt die kontextbezogene Hilfe an. |

### <a name="examples"></a>Beispiele

Um die XML-Datei " *c:\windows\ perf_log. XML* " vom Computer *server_1* als Datensammler Satz mit dem Namen *perf_log*zu importieren, geben Sie Folgendes ein:

```
logman import perf_log -s server_1 -xml c:\windows\perf_log.xml
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [logman-Befehl](logman.md)
