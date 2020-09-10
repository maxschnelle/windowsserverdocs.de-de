---
title: rpcinfo
description: Referenz Artikel für den Befehl rpcinfo, der die Programme auf einem Remote Computer auflistet.
ms.topic: reference
ms.assetid: 7c342232-a8f0-42ff-8f11-d18c4981f5ca
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 07/11/2018
ms.openlocfilehash: 3e5865bb976f71b9fbb90e4dd77008f00056a455
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89639830"
---
# <a name="rpcinfo"></a>rpcinfo

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Listet Programme auf Remote Computern auf. Das Befehlszeilen-Hilfsprogramm **rpcinfo** führt einen Remote Prozedur Aufruf (RPC) zu einem RPC-Server durch und meldet, was er findet.

## <a name="syntax"></a>Syntax

```
rpcinfo [/p [<node>]] [/b <program version>] [/t <node program> [<version>]] [/u <node program> [<version>]]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| /p `[<node>]` | Listet alle Programme auf, die bei der Port Zuordnung auf dem angegebenen Host registriert sind. Wenn Sie keinen Knoten Namen (Computer) angeben, fragt das Programm die Port Zuordnung auf dem lokalen Host ab. |
| /b `<program version>` | Fordert eine Antwort von allen Netzwerkknoten an, für die das angegebene Programm und die angegebene Version beim Port-Mapper registriert sind. Sie müssen einen Programmnamen oder eine Nummer und eine Versionsnummer angeben. |
| /t `<node program> [\<version>]` | Verwendet das TCP-Transportprotokoll, um das angegebene Programm aufzurufen. Sie müssen sowohl einen Knoten Namen (Computer) als auch einen Programmnamen angeben. Wenn Sie keine Version angeben, ruft das Programm alle Versionen auf. |
| /u `<node program> [\<version>]` | Verwendet das UDP-Transportprotokoll, um das angegebene Programm aufzurufen. Sie müssen sowohl einen Knoten Namen (Computer) als auch einen Programmnamen angeben. Wenn Sie keine Version angeben, ruft das Programm alle Versionen auf. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um alle Programme aufzulisten, die beim Port-Mapper registriert sind:

```
rpcinfo /p [<node>]
```

Geben Sie Folgendes ein, um eine Antwort von Netzwerkknoten mit einem angegebenen Programm anzufordern:

```
rpcinfo /b <program version>
```

Geben Sie Folgendes ein, um ein Programm mit dem Transmission Control Protocol (TCP) aufzurufen:

```
rpcinfo /t <node program> [<version>]
```

Verwenden Sie das User Datagram-Protokoll (UDP), um ein Programm aufzurufen:

```
rpcinfo /u <node program> [<version>]
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
