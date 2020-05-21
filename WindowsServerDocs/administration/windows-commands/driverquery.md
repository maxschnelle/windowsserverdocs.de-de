---
title: driverquery
description: Referenz Thema für den driverquery-Befehl, mit dem ein Administrator eine Liste der installierten Gerätetreiber und deren Eigenschaften anzeigen kann.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 92ca4b84-e4e2-405b-9f31-bf6db9f66839
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f4754cba8cf4cb3a5f01b0aeb0095f727a072a5c
ms.sourcegitcommit: bf887504703337f8ad685d778124f65fe8c3dc13
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/16/2020
ms.locfileid: "83436935"
---
# <a name="driverquery"></a>driverquery

Ermöglicht es einem Administrator, eine Liste der installierten Gerätetreiber und deren Eigenschaften anzuzeigen. Bei Verwendung ohne Parameter wird die Ausführung von **driverquery** auf dem lokalen Computer ausgeführt.

## <a name="syntax"></a>Syntax

```
driverquery [/s <system> [/u [<domain>\]<username> [/p <password>]]] [/fo {table | list | csv}] [/nh] [/v | /si]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- |------------ |
| /s`<system>` | Gibt den Namen oder die IP-Adresse eines Remote Computers an. Verwenden Sie keine umgekehrten Schrägstriche. Der Standardwert ist der lokale Computer. |
| /u`[<domain>]<username>` | Führt den Befehl mit den Anmelde Informationen des Benutzerkontos aus, wie von " *User* " oder " *Domäne \ Benutzer*" angegeben. Standardmäßig verwendet */s* die Anmelde Informationen des Benutzers, der zurzeit auf dem Computer angemeldet ist, von dem der Befehl ausgegeben wird. **/u** kann nur verwendet werden, wenn **/s** angegeben wird. |
| /p`<password>` | Gibt das Kennwort des Benutzerkontos an, das im **/u** -Parameter angegeben ist. **/p** kann nur verwendet werden, wenn **/u** angegeben wird. |
| /FO-Tabelle | Formatiert die Ausgabe als Tabelle. Dies ist der Standardwert. |
| /FO-Liste | Formatiert die Ausgabe als Liste. |
| CSV/FO | Formatiert die Ausgabe mit durch Trennzeichen getrennten Werten. |
| /nh | Lässt die Kopfzeile der angezeigten Treiber Informationen aus. Ungültig, wenn der **/FO** -Parameter auf **List**festgelegt ist. |
| /v | Zeigt die ausführliche Ausgabe an. **/v** ist für signierte Treiber nicht gültig. |
| /Si | Enthält Informationen zu signierten Treibern. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um eine Liste der installierten Gerätetreiber auf dem lokalen Computer anzuzeigen:

```
driverquery
```

Geben Sie Folgendes ein, um die Ausgabe in einem CSV-Format (Comma-Separated Values) anzuzeigen:

```
driverquery /fo csv
```

Um die Kopfzeile in der Ausgabe auszublenden, geben Sie Folgendes ein:

```
driverquery /nh
```

Geben Sie Folgendes ein, um den Befehl " **driverquery** " auf einem Remote Server mit dem Namen *Server1* mit ihren aktuellen Anmelde Informationen auf dem lokalen Computer zu verwenden:

```
driverquery /s server1
```

Wenn Sie den Befehl " **driverquery** " auf einem Remote Server mit dem Namen *Server1* mithilfe der Anmelde Informationen für *User1* im Domänen- *Maindom*verwenden möchten, geben Sie

```
driverquery /s server1 /u maindom\user1 /p p@ssw3d
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)