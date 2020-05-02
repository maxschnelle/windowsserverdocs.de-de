---
title: bootcfg query
description: Referenz Thema für den bootcfg-Abfragebefehl, der die Einträge des Start Lade Programms und des Betriebssystem Abschnitts in der Datei "Boot. ini" abfragt und anzeigt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: a4cacfd1-10a6-4a11-b0c5-f8abde72bfc8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 44c5ce60f55618d16e80d1f1efde3af1cbf6c609
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82709330"
---
# <a name="bootcfg-query"></a>bootcfg query

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Abfragen und Anzeigen der Abschnitts Einträge [Boot Loader] und [Betriebssysteme] aus der Datei "Boot. ini".

## <a name="syntax"></a>Syntax

```
bootcfg /query [/s <computer> [/u <domain>\<user> /p <password>]]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `/s <computer>` | Gibt den Namen oder die IP-Adresse eines Remote Computers an (verwenden Sie keine umgekehrten Schrägstriche). Der Standardwert ist der lokale Computer. |
| `/u <domain>\<user>`  | Führt den Befehl mit den Konto Berechtigungen des Benutzers aus, der `<user>` von `<domain>\<user>`oder angegeben wird. Der Standardwert sind die Berechtigungen des aktuell angemeldeten Benutzers auf dem Computer, von dem der Befehl ausgegeben wird. |
| `/p <password>` | Gibt das Kennwort des Benutzerkontos an, das im **/u** -Parameter angegeben ist. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="sample-output"></a>Beispielausgabe

Beispielausgabe für den Befehl **bootcfg/query "aus** :
  
```
Boot Loader Settings
----------
timeout: 30
default: multi(0)disk(0)rdisk(0)partition(1)\WINDOWS
Boot Entries
------
Boot entry ID:   1
Friendly Name:
path: multi(0)disk(0)rdisk(0)partition(1)\WINDOWS
OS Load Options: /fastdetect /debug /debugport=com1:
```

- Der Bereich **Start Lade Lade-Einstellungen** zeigt jeden Eintrag in der Datei Boot. ini im Abschnitt [Boot Loader] an.

- Im Bereich **Start Einträge** werden weitere Details zu jedem Betriebssystem Eintrag im Abschnitt [Betriebssysteme] der Datei "Boot. ini" angezeigt.

## <a name="examples"></a>Beispiele

So verwenden Sie den Befehl **bootcfg/query "aus** :

```
bootcfg /query
bootcfg /query /s srvmain /u maindom\hiropln /p p@ssW23
bootcfg /query /u hiropln /p p@ssW23
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [BOOTCFG-Befehl](bootcfg.md)
