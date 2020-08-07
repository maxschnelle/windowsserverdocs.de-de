---
title: bootcfg query
description: Referenz Artikel für den bootcfg-Abfragebefehl, mit dem die Start Lade-und Betriebssystem Abschnitts Einträge von Boot.ini abgefragt und angezeigt werden.
ms.topic: article
ms.assetid: a4cacfd1-10a6-4a11-b0c5-f8abde72bfc8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bb4ff06e8c0e5f31c0132f7fbc4fad49be53dd62
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87880566"
---
# <a name="bootcfg-query"></a>bootcfg query

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Hiermit werden die Abschnitts Einträge [Boot Loader] und [Betriebssysteme] aus Boot.ini abgefragt und angezeigt.

## <a name="syntax"></a>Syntax

```
bootcfg /query [/s <computer> [/u <domain>\<user> /p <password>]]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `/s <computer>` | Gibt den Namen oder die IP-Adresse eines Remote Computers an (verwenden Sie keine umgekehrten Schrägstriche). Die Standardeinstellung ist der lokale Computer. |
| `/u <domain>\<user>`  | Führt den Befehl mit den Konto Berechtigungen des Benutzers aus, der von oder angegeben wird `<user>` `<domain>\<user>` . Der Standardwert sind die Berechtigungen des aktuell angemeldeten Benutzers auf dem Computer, von dem der Befehl ausgegeben wird. |
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

- Der Bereich **Start Lade Lade-Einstellungen** zeigt jeden Eintrag im Abschnitt [Boot Loader] von Boot.ini an.

- Im Bereich **Start Einträge** werden weitere Details zu jedem Betriebssystem Eintrag im Abschnitt [Betriebssysteme] des Boot.ini angezeigt.

## <a name="examples"></a>Beispiele

So verwenden Sie den Befehl **bootcfg/query "aus** :

```
bootcfg /query
bootcfg /query /s srvmain /u maindom\hiropln /p p@ssW23
bootcfg /query /u hiropln /p p@ssW23
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [BOOTCFG-Befehl](bootcfg.md)
