---
title: rpcinfo
description: Erfahren Sie, wie Sie die Programme auf einem Remote Computer auflisten.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7c342232-a8f0-42ff-8f11-d18c4981f5ca
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: d25a806c63f959ec659a6dd692d9efd5b394a64c
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2020
ms.locfileid: "83820090"
---
# <a name="rpcinfo"></a>rpcinfo

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Listet Programme auf Remote Computern auf. Das Befehlszeilen-Hilfsprogramm **rpcinfo** führt einen Remote Prozedur Aufruf (RPC) zu einem RPC-Server durch und meldet, was er findet.

## <a name="syntax"></a>Syntax
```
rpcinfo [/p [<Node>]] [/b <Program version>] [/t <Node Program> [<version>]] [/u <Node Program> [<version>]]
```

#### <a name="parameters"></a>Parameter
|Parameter|BESCHREIBUNG|
|-------|--------|
|/p [ \< Knoten>]|Listet alle Programme auf, die bei der Port Zuordnung auf dem angegebenen Host registriert sind. Wenn Sie keinen Knoten Namen (Computer) angeben, fragt das Programm die Port Zuordnung auf dem lokalen Host ab.|
|/b- \< Programmversion>|Fordert eine Antwort von allen Netzwerkknoten an, für die das angegebene Programm und die angegebene Version beim Port-Mapper registriert sind. Sie müssen einen Programmnamen oder eine Nummer und eine Versionsnummer angeben.|
|/t \< Node-Programm> [ \< Version>]|Verwendet das TCP-Transportprotokoll, um das angegebene Programm aufzurufen. Sie müssen sowohl einen Knoten Namen (Computer) als auch einen Programmnamen angeben. Wenn Sie keine Version angeben, ruft das Programm alle Versionen auf.|
|/u \< Node-Programm> [ \< Version>]|Verwendet das UDP-Transportprotokoll, um das angegebene Programm aufzurufen. Sie müssen sowohl einen Knoten Namen (Computer) als auch einen Programmnamen angeben. Wenn Sie keine Version angeben, ruft das Programm alle Versionen auf.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="examples"></a>Beispiele
Geben Sie Folgendes ein, um alle Programme aufzulisten, die beim Port-Mapper registriert sind:
```
rpcinfo /p [<Node>]
```
Geben Sie Folgendes ein, um eine Antwort von Netzwerkknoten mit einem angegebenen Programm anzufordern:
```
rpcinfo /b <Program version>
```
Geben Sie Folgendes ein, um ein Programm mit dem Transmission Control Protocol (TCP) aufzurufen:
```
rpcinfo /t <Node Program> [<version>]
```
Verwenden Sie das User Datagram-Protokoll (UDP), um ein Programm aufzurufen:
```
rpcinfo /u <Node Program> [<version>]
```

## <a name="additional-references"></a>Zusätzliche Referenzen
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
