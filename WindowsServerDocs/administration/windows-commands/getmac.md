---
title: getmac
description: Referenz Artikel für den Befehl getmac, der die Media Access Control (Mac)-Adresse und die Liste der Netzwerkprotokolle zurückgibt, die jeweils lokal oder über ein Netzwerk verknüpft sind.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: a749a348-7cd1-4336-9f33-bb42dd0e31e1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 345daa310b075f8a094dd8a87e7c1c0d3694ab10
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85932339"
---
# <a name="getmac"></a>getmac

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Gibt die Media Access Control (Mac)-Adresse und die Liste der Netzwerkprotokolle zurück, die jeder Adresse für alle Netzwerkkarten in den einzelnen Computern zugeordnet sind, entweder lokal oder über ein Netzwerk. Dieser Befehl ist besonders nützlich, wenn Sie die Mac-Adresse in eine Network Analyzer eingeben möchten oder wenn Sie wissen müssen, welche Protokolle derzeit auf den einzelnen Netzwerkadaptern auf einem Computer verwendet werden.

## <a name="syntax"></a>Syntax

```
getmac[.exe][/s <computer> [/u <domain\<user> [/p <password>]]][/fo {table | list | csv}][/nh][/v]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- |------------ |
| /s`<computer>` | Gibt den Namen oder die IP-Adresse eines Remote Computers an (verwenden Sie keine umgekehrten Schrägstriche). Die Standardeinstellung ist der lokale Computer. |
| /u`<domain>\<user>` | Führt den Befehl mit den Konto Berechtigungen des Benutzers aus, der von " *User* " oder " *Domäne \ Benutzer*" angegeben wurde. Der Standardwert sind die Berechtigungen des aktuell angemeldeten Benutzers auf dem Computer, von dem der Befehl ausgegeben wird. |
| /p`<password>` | Gibt das Kennwort des Benutzerkontos an, das im **/u** -Parameter angegeben ist. |
| /FO {Table | list | CSV | Gibt das Format an, das für die Abfrageausgabe verwendet werden soll. Gültige Werte sind " **Table**", " **List**" und " **CSV**". Das Standardformat für die Ausgabe ist **Table**. |
| /nh | Unterdrückt die Spalten Kopfzeile in der Ausgabe. Gültig, wenn der **/FO** -Parameter auf **Table** oder **CSV**festgelegt ist. |
| /v | Gibt an, dass in der Ausgabe ausführliche Informationen angezeigt werden. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

### <a name="examples"></a>Beispiele

In den folgenden Beispielen wird gezeigt, wie Sie den Befehl **getmac** verwenden können:

```
getmac /fo table /nh /v
```

```
getmac /s srvmain
```

```
getmac /s srvmain /u maindom\hiropln
```

```
getmac /s srvmain /u maindom\hiropln /p p@ssW23
```

```
getmac /s srvmain /u maindom\hiropln /p p@ssW23 /fo list /v
```

```
getmac /s srvmain /u maindom\hiropln /p p@ssW23 /fo table /nh
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
