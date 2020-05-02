---
title: freedisk
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 91c15166-5baa-4b80-9e0c-4cd815d00530
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 102d829535eb6028b2a062234f280fd32ea48943
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725558"
---
# <a name="freedisk"></a>freedisk

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Prüft, ob die angegebene Menge an Speicherplatz verfügbar ist, bevor der Installationsvorgang fortgesetzt wird.

## <a name="syntax"></a>Syntax
```
freedisk [/s <computer> [/u [<Domain>\]<User> [/p [<Password>]]]] [/d <Drive>] [<Value>]
```
### <a name="parameters"></a>Parameter

|       Parameter       |                                                                                         BESCHREIBUNG                                                                                          |
|-----------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     /s<computer>     | Gibt den Namen oder die IP-Adresse eines Remote Computers an (verwenden Sie keine umgekehrten Schrägstriche). Der Standardwert ist der lokale Computer. Dieser Parameter gilt für alle Dateien und Ordner, die im Befehl angegeben sind. |
| /u [<Domain>\\]<User> |                                            Führt das Skript mit den Berechtigungen des angegebenen Benutzerkontos aus. Der Standardwert sind System Berechtigungen.                                            |
|    /p [<Password>]    |                                                           Gibt das Kennwort des Benutzerkontos an, das in **/u**angegeben ist.                                                            |
|      /d<Drive>       |                              Gibt das Laufwerk an, für das Sie die Verfügbarkeit von freiem Speicherplatz ermitteln möchten. Sie müssen für <Drive>einen Remote Computer angeben.                               |
|        <Value>        |                                     Prüft, ob eine bestimmte Menge an freiem Speicherplatz verfügbar ist. Sie können Folgendes bestimmen: <Value>in Bytes, KB, MB, GB, TB, PB, EB, zB oder YB.                                      |

## <a name="remarks"></a>Bemerkungen
- Die Befehlszeilenoptionen **/s**, **/u**und **/p** sind nur verfügbar, wenn Sie **/s**verwenden. Sie müssen **/p** mit **/u**verwenden, um das Kennwort des Benutzers anzugeben.
- bei unbeaufsichtigten Installationen können Sie mithilfe von **freedisk** in den Installations Batch Dateien den freien Speicherplatz für den erforderlichen Speicherplatz überprüfen, bevor Sie die Installation fortsetzen.
- Wenn Sie in einer Batchdatei " **freiplatte** " verwenden, wird " **0** " zurückgegeben, wenn ausreichend Speicherplatz vorhanden ist, und **1** , wenn nicht genügend Speicherplatz vorhanden ist.
  ## <a name="examples"></a>Beispiele
  Geben Sie Folgendes ein, um zu bestimmen, ob mindestens 50 MB freier Speicherplatz auf Laufwerk C: verfügbar ist:
  ```
  freedisk 50mb 
  ```
  Auf dem Bildschirm wird eine Ausgabe ähnlich der folgenden angezeigt:
  ```
  INFO: The specified 52,428,800 byte(s) of free space is available on current drive.
  ```
  ## <a name="additional-references"></a>Zusätzliche Referenzen
  - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
