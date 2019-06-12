---
title: freedisk
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: ac2f38fb1948a26ae55713ac6fb14254851b062a
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66439160"
---
# <a name="freedisk"></a>freedisk

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Überprüft, um festzustellen, ob es sich bei der angegebene Betrag an Speicherplatz verfügbar ist, bevor Sie einen Installationsvorgang fortsetzen.

## <a name="syntax"></a>Syntax
```
freedisk [/s <computer> [/u [<Domain>\]<User> [/p [<Password>]]]] [/d <Drive>] [<Value>]
```
## <a name="parameters"></a>Parameter

|       Parameter       |                                                                                         Beschreibung                                                                                          |
|-----------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     /s <computer>     | Gibt den Namen oder die IP-Adresse eines Remotecomputers (umgekehrte Schrägstriche nicht verwenden). Der Standardwert ist der lokale Computer. Dieser Parameter gilt für alle Dateien und Ordner im Befehl angegeben. |
| /u [<Domain>\\]<User> |                                            Führt das Skript mit den Berechtigungen des angegebenen Benutzerkontos. Der Standardwert ist die Systemberechtigungen.                                            |
|    /p [<Password>]    |                                                           Gibt das Kennwort des Benutzerkontos ein, die im angegebenen **/u**.                                                            |
|      /d <Drive>       |                              Gibt das Laufwerk für das Sie die Verfügbarkeit des freien Speicherplatzes ermitteln möchten. Sie müssen angeben, <Drive>für einen Remotecomputer.                               |
|        <Value>        |                                     Überprüft, ob eine bestimmte Menge an freiem Festplattenspeicher verfügbar. Sie können angeben <Value>in Byte, KB, MB, GB, TB, PB, "EB", ZB oder YB.                                      |

## <a name="remarks"></a>Hinweise
- Mithilfe der **/s**, **/u**, und **/p** Befehlszeilenoptionen stehen nur bei Verwendung von **/s**. Verwenden Sie **/p** mit **/u**das Kennwort des Benutzers s bereitstellen.
- Bei unbeaufsichtigten Installationen können Sie **Freedisk** in Batch-Installationsdateien für die erforderliche freie Speicherplatz verfügbar zu überprüfen, bevor Sie mit der Installation fortfahren.
- Bei Verwendung von **Freedisk** in einer Batchdatei wird eine **0** Wenn genügend Speicherplatz vorhanden ist und eine **1** Wenn nicht genügend Speicherplatz vorhanden ist.
  ## <a name="BKMK_examples"></a>Beispiele für
  Um zu bestimmen, ob mindestens 50 MB freien Speicherplatz auf Laufwerk C: vorhanden sind, geben Sie Folgendes ein:
  ```
  freedisk 50mb 
  ```
  Auf dem Bildschirm wird eine Ausgabe ähnlich der folgenden angezeigt:
  ```
  INFO: The specified 52,428,800 byte(s) of free space is available on current drive.
  ```
  ## <a name="additional-references"></a>Zusätzliche Referenzen
  [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
