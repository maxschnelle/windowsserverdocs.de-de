---
title: freedisk
description: Referenz Artikel für den Befehl "frei Platte", mit dem überprüft wird, ob die angegebene Menge an Speicherplatz verfügbar ist, bevor der Installationsvorgang fortgesetzt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 91c15166-5baa-4b80-9e0c-4cd815d00530
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d0cfce52c2eaf0917f8169d959b61832bd1779e0
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85924742"
---
# <a name="freedisk"></a>freedisk

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Prüft, ob die angegebene Menge an Speicherplatz verfügbar ist, bevor der Installationsvorgang fortgesetzt wird.

## <a name="syntax"></a>Syntax

```
freedisk [/s <computer> [/u [<domain>\]<user> [/p [<password>]]]] [/d <drive>] [<value>]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| /s`<computer>` | Gibt den Namen oder die IP-Adresse eines Remote Computers an (verwenden Sie keine umgekehrten Schrägstriche). Die Standardeinstellung ist der lokale Computer. Dieser Parameter gilt für alle Dateien und Ordner, die im Befehl angegeben sind. |
| /u`[<domain>\]<user>` | Führt das Skript mit den Berechtigungen des angegebenen Benutzerkontos aus. Der Standardwert sind System Berechtigungen. |
| /p [ <password> ] | Gibt das Kennwort des Benutzerkontos an, das in **/u**angegeben ist. |
| /d`<drive>` | Gibt das Laufwerk an, für das Sie die Verfügbarkeit von freiem Speicherplatz ermitteln möchten. Sie müssen `<drive>` für einen Remote Computer angeben. |
| `<value>` | Prüft, ob eine bestimmte Menge an freiem Speicherplatz verfügbar ist. Sie können `<value>` in Bytes, KB, MB, GB, TB, PB, EB, zB oder YB angeben. |

#### <a name="remarks"></a>Hinweise

- Die Befehlszeilenoptionen **/s**, **/u**und **/p** sind nur verfügbar, wenn Sie **/s**verwenden. Sie müssen **/p** mit **/u**verwenden, um das Kennwort des Benutzers anzugeben.

- Bei unbeaufsichtigten Installationen können Sie mithilfe von **freedisk** in den Installations Batch Dateien den freien Speicherplatz für den erforderlichen Speicherplatz überprüfen, bevor Sie die Installation fortsetzen.

- Wenn Sie in einer Batchdatei " **freiplatte** " verwenden, wird " **0** " zurückgegeben, wenn ausreichend Speicherplatz vorhanden ist, und **1** , wenn nicht genügend Speicherplatz vorhanden ist.

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um zu bestimmen, ob mindestens 50 MB freier Speicherplatz auf Laufwerk C: verfügbar ist:

```
freedisk 50mb
```

Auf dem Bildschirm wird eine Ausgabe ähnlich der folgenden angezeigt:

```
INFO: The specified 52,428,800 byte(s) of free space is available on current drive.
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
