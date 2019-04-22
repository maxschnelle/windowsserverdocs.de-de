---
title: rpcinfo
description: Erfahren Sie, wie Sie die Programme auf einem Remotecomputer auflisten.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7c342232-a8f0-42ff-8f11-d18c4981f5ca
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: 4aba1e57d5a61103310fbe7abcac391e543be5aa
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59826371"
---
# <a name="rpcinfo"></a>rpcinfo

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Die Programme aufgelistet, auf Remotecomputern. Die **Rpcinfo** Befehlszeilen-Hilfsprogramm stellt ein Remoteprozeduraufruf (RPC) an einen rpc_server aufrufen, und meldet, was es findet. 

## <a name="syntax"></a>Syntax
```
rpcinfo [/p [<Node>]] [/b <Program version>] [/t <Node Program> [<version>]] [/u <Node Program> [<version>]]
```

### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|/ p [\<Knoten >]|Listet alle Programme, die bei der Portmapper auf dem angegebenen Host registriert. Wenn Sie einen Knotennamen (Computer) nicht angeben, fragt das Programm die Portmapper auf dem lokalen Host.|
|/ b \<Programmversion >|Fordert eine Antwort von allen Netzwerkknoten, die das angegebene Programm und die Version, die bei der Portmapper registriert haben. Sie müssen sowohl einen Programmnamen oder Anzahl und eine Versionsnummer angeben.|
|/ t / \<Knoten Programm > [\<Version >]|Verwendet das TCP-Transportprotokoll, das angegebene Programm aufrufen. Sie müssen sowohl einen Knotennamen (Computer) und einen Programmnamen angeben. Wenn Sie keine Version angeben, ruft das Programm alle Versionen.|
|/ u \<Knoten Programm > [\<Version >]|Verwendet die UDP-Transportprotokoll verwendet das angegebene Programm aufrufen. Sie müssen sowohl einen Knotennamen (Computer) und einen Programmnamen angeben. Wenn Sie keine Version angeben, ruft das Programm alle Versionen.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="BKMK_Examples"></a>Beispiele für
Um alle Programme, die bei der Portmapper registriert aufzulisten, geben Sie Folgendes ein:
```
rpcinfo /p [<Node>]
```
Um eine Antwort von Netzwerkknoten anzufordern, die ein angegebenes Programm haben, geben Sie Folgendes ein:
```
rpcinfo /b <Program version>
```
Um das Protokoll TCP (Transmission Control) verwenden, um ein Programm aufrufen, geben Sie Folgendes ein:
```
rpcinfo /t <Node Program> [<version>]
```
Verwenden Sie User Datagram Protocol (UDP), um ein Programm aufrufen:
```
rpcinfo /u <Node Program> [<version>]
```

## <a name="additional-references"></a>Weitere Verweise
-   [Befehlszeilensyntax](command-line-syntax-key.md)
