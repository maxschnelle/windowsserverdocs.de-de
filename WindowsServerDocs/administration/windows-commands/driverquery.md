---
title: driverquery
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 92ca4b84-e4e2-405b-9f31-bf6db9f66839
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 88a59f9da9927bb923418695bc760303c0fb00b0
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66439487"
---
# <a name="driverquery"></a>driverquery



Ermöglicht einem Administrator, um eine Liste der installierten Treiber und deren Eigenschaften anzuzeigen. Wenn Sie ohne Angabe von Parametern **Driverquery** auf dem lokalen Computer ausgeführt wird.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
driverquery [/s <System> [/u [<Domain>\]<Username> [/p <Password>]]] [/fo {table | list | csv}] [/nh] [/v | /si]
```

## <a name="parameters"></a>Parameter

|         Parameter         |                                                                                                                                         Beschreibung                                                                                                                                          |
|---------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|       /s \<System>        |                                                                                      Gibt den Namen oder die IP-Adresse eines Remotecomputers. Verwenden Sie keine umgekehrte Schrägstriche. Der Standardwert ist der lokale Computer.                                                                                       |
| /u [\<Domain>\]<Username> | Führt den Befehl mit den Anmeldeinformationen des Benutzerkontos laut *Benutzer* oder *Domäne*\*Benutzer<em>. In der Standardeinstellung \* \*/s</em> \* verwendet die Anmeldeinformationen des Benutzers, der derzeit auf dem Computer angemeldet ist, die den Befehl ausgegeben wird. **/ u** kann nicht verwendet werden, es sei denn, **/s** angegeben ist. |
|      / p \<Kennwort >       |                                                                           Gibt das Kennwort des Benutzerkontos ein, die im angegebenen die **/u** Parameter. **/ p** kann nicht verwendet werden, es sei denn, **/u** angegeben ist.                                                                            |
|        / FO {table         |                                                                                                                                             list                                                                                                                                             |
|            /nh            |                                                                                      Lässt die Headerzeile aus der angezeigten Treiberinformationen. Nicht gültig, wenn die **/Fo** Parametersatz zu **Liste**.                                                                                      |
|            /v             |                                                                                                               Zeigt eine ausführliche Ausgabe. **/ v** gilt nicht für signierte Treiber.                                                                                                               |
|            /si            |                                                                                                                          Enthält Informationen zu den signierten Treiber.                                                                                                                          |
|            /?             |                                                                                                                             Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                                             |

## <a name="BKMK_examples"></a>Beispiele für

Um eine Liste der installierten Gerätetreiber auf dem lokalen Computer anzuzeigen, geben Sie Folgendes ein:
```
driverquery 
```
Um die Ausgabe in einem Format mit kommagetrennten Werten (CSV) anzuzeigen, geben Sie Folgendes ein:
```
driverquery /fo csv 
```
Um die Kopfzeile in der Ausgabe auszublenden, geben Sie Folgendes ein:
```
driverquery /nh 
```
Verwenden der **Driverquery** Befehl auf einem Remoteserver mit dem Namen **server1** verwenden Ihre aktuellen Anmeldeinformationen auf dem lokalen Computer aus, geben Sie:
```
driverquery /s server1
```
Verwenden der **Driverquery** Befehl auf einem Remoteserver mit dem Namen **server1** mit den Anmeldeinformationen für **"user1"** in der Domäne **Maindom**, Typ:
```
driverquery /s server1 /u maindom\user1 /p p@ssw3d
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)