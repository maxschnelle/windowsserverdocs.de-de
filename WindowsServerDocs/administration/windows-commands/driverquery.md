---
title: driverquery
description: Referenz Artikel für den Befehl "driverquery", der es einem Administrator ermöglicht, eine Liste der installierten Gerätetreiber und deren Eigenschaften anzuzeigen.
ms.topic: reference
ms.assetid: 92ca4b84-e4e2-405b-9f31-bf6db9f66839
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: dbd8ca2de7f15a5b5fb8682dae3a3aa2e105d7cd
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89030798"
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
| /s `<system>` | Gibt den Namen oder die IP-Adresse eines Remote Computers an. Verwenden Sie keine umgekehrten Schrägstriche. Die Standardeinstellung ist der lokale Computer. |
| /u `[<domain>]<username>` | Führt den Befehl mit den Anmelde Informationen des Benutzerkontos aus, wie von " *User* " oder " *Domäne \ Benutzer*" angegeben. Standardmäßig verwendet */s* die Anmelde Informationen des Benutzers, der zurzeit auf dem Computer angemeldet ist, von dem der Befehl ausgegeben wird. **/u** kann nur verwendet werden, wenn **/s** angegeben wird. |
| /p `<password>` | Gibt das Kennwort des Benutzerkontos an, das im **/u** -Parameter angegeben ist. **/p** kann nur verwendet werden, wenn **/u** angegeben wird. |
| /FO-Tabelle | Formatiert die Ausgabe als Tabelle. Dies ist die Standardoption. |
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

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)