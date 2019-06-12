---
title: getmac
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a749a348-7cd1-4336-9f33-bb42dd0e31e1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b1266b7368f1b073e00735a8d3362c75305d7c0f
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66438269"
---
# <a name="getmac"></a>getmac

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Gibt das Medium auf Control (MAC)-Adresse und Liste Netzwerkprotokollen, die mit jeder Adresse verknüpfte für alle Netzwerkkarten in jedem Computer, entweder lokal oder über ein Netzwerk zugreifen. 
## <a name="syntax"></a>Syntax
```
getmac[.exe][/s <computer> [/u <Domain\<User> [/p <Password>]]][/fo {TABLE | list | CSV}][/nh][/v]
```
### <a name="parameters"></a>Parameter

|             Parameter              |                                                                                          Beschreibung                                                                                          |
|------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|           /s <computer>            |                                      Gibt den Namen oder die IP-Adresse eines Remotecomputers (umgekehrte Schrägstriche nicht verwenden). Der Standardwert ist der lokale Computer.                                       |
|        /u <Domain>\\<User>         | Führt den Befehl mit den Berechtigungen des Benutzers von einem Benutzer oder "Domäne\Benutzer" angegeben. Der Standardwert ist die Berechtigungen von der aktuell angemeldete Benutzer auf dem Computer, die der Befehl ausgegeben wird. |
|           /p <Password>            |                                                     Gibt das Kennwort des Benutzerkontos ein, die im angegebenen die **/u** Parameter.                                                     |
| /fo { TABLE &#124; list&#124; CSV} |                       Gibt das Format für die Ausgabe der Abfrage verwendet. Gültige Werte sind **Tabelle**, **Liste**, und **CSV**. Das Standardformat für die Ausgabe ist **Tabelle**.                        |
|                /nh                 |                                             Unterdrückt die Kopfzeile der Spalte in der Ausgabe. Gültig, wenn die **/Fo** Parametersatz zu **Tabelle** oder **CSV**.                                              |
|                 /v                 |                                                                    Gibt an, dass die Ausgabe ausführliche Informationen anzuzeigen.                                                                     |
|                 /?                 |                                                                                                                                                                                               |

## <a name="remarks"></a>Hinweise
**Getmac** kann nützlich sein, wenn Sie die MAC-Adresse in einer Netzwerkanalyse eingeben möchten oder wenn Sie wissen, welche Protokolle derzeit auf jeden Netzwerkadapter auf einem Computer müssen.
## <a name="BKMK_Examples"></a>Beispiele für
Die folgenden Beispiele zeigen Informationen zur Verwendung der **Getmac** Befehl:
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
## <a name="additional-references"></a>Zusätzliche Referenzen
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
