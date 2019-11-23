---
title: freedisk
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 91c15166-5baa-4b80-9e0c-4cd815d00530
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8e417a8f9768706fe391f705adde37c62ceaa818
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71377033"
---
# <a name="freedisk"></a>freedisk

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Prüft, ob die angegebene Menge an Speicherplatz verfügbar ist, bevor der Installationsvorgang fortgesetzt wird.

## <a name="syntax"></a>Syntax
```
freedisk [/s <computer> [/u [<Domain>\]<User> [/p [<Password>]]]] [/d <Drive>] [<Value>]
```
## <a name="parameters"></a>Parameter

|       Parameter       |                                                                                         Beschreibung                                                                                          |
|-----------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     /s <computer>     | Gibt den Namen oder die IP-Adresse eines Remote Computers an (verwenden Sie keine umgekehrten Schrägstriche). Der Standardwert ist der lokale Computer. Dieser Parameter gilt für alle Dateien und Ordner, die im Befehl angegeben sind. |
| /u [<Domain>\\]<User> |                                            Führt das Skript mit den Berechtigungen des angegebenen Benutzerkontos aus. Der Standardwert sind System Berechtigungen.                                            |
|    /p [<Password>]    |                                                           Gibt das Kennwort des Benutzerkontos an, das in **/u**angegeben ist.                                                            |
|      /d <Drive>       |                              Gibt das Laufwerk an, für das Sie die Verfügbarkeit von freiem Speicherplatz ermitteln möchten. Sie müssen <Drive>für einen Remote Computer angeben.                               |
|        <Value>        |                                     Prüft, ob eine bestimmte Menge an freiem Speicherplatz verfügbar ist. Sie können <Value>in Bytes, KB, MB, GB, TB, PB, EB, zB oder YB.                                      |

## <a name="remarks"></a>Hinweise
- Die Befehlszeilenoptionen **/s**, **/u**und **/p** sind nur verfügbar, wenn Sie **/s**verwenden. Sie müssen **/p** mit **/u**verwenden, um das Kennwort des Benutzers anzugeben.
- bei unbeaufsichtigten Installationen können Sie mithilfe von **freedisk** in den Installations Batch Dateien den freien Speicherplatz für den erforderlichen Speicherplatz überprüfen, bevor Sie die Installation fortsetzen.
- Wenn Sie in einer Batchdatei " **freiplatte** " verwenden, wird " **0** " zurückgegeben, wenn ausreichend Speicherplatz vorhanden ist, und **1** , wenn nicht genügend Speicherplatz vorhanden ist.
  ## <a name="BKMK_examples"></a>Beispiele
  Geben Sie Folgendes ein, um zu bestimmen, ob mindestens 50 MB freier Speicherplatz auf Laufwerk C: verfügbar ist:
  ```
  freedisk 50mb 
  ```
  Auf dem Bildschirm wird eine Ausgabe ähnlich der folgenden angezeigt:
  ```
  INFO: The specified 52,428,800 byte(s) of free space is available on current drive.
  ```
  ## <a name="additional-references"></a>Weitere Verweise
  [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
