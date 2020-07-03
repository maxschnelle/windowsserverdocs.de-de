---
title: logman import and logman export
description: Referenz Artikel zu logman Import und logman Export, der einen Datensammler Satz aus einer XML-Datei importiert oder einen Datensammler Satz in eine XML-Datei exportiert.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c258daba-fb93-47c0-a53b-2fe83ed2c743
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d5fbe0139a1c320056e4ba80a845b43755fc0026
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85934394"
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

Geben Sie Folgendes ein, um die XML-Datei *c:\windows\perf_log.xml* vom Computer *server_1* als Datensammler Satz mit dem Namen *perf_log*zu importieren:

```
logman import perf_log -s server_1 -xml c:\windows\perf_log.xml
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [logman-Befehl](logman.md)
