---
title: WAITFOR
description: Referenz Artikel für den Befehl "WAITFOR", der ein Signal an ein System sendet oder darauf wartet.
ms.topic: reference
ms.assetid: a48ef70d-4d28-4035-b6b0-7d7b46ac2157
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 157861a02abe8fbf851a6ef12460b257a7628803
ms.sourcegitcommit: f45640cf4fda621b71593c63517cfdb983d1dc6a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2020
ms.locfileid: "92156122"
---
# <a name="waitfor"></a>WAITFOR

Sendet oder wartet auf ein Signal auf einem System. Mit diesem Befehl werden Computer in einem Netzwerk synchronisiert.

## <a name="syntax"></a>Syntax

```
waitfor [/s <computer> [/u [<domain>\]<user> [/p [<password>]]]] /si <signalname>
waitfor [/t <timeout>] <signalname>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| /s `<computer>` | Gibt den Namen oder die IP-Adresse eines Remote Computers an (verwenden Sie keine umgekehrten Schrägstriche). Die Standardeinstellung ist der lokale Computer. Dieser Parameter gilt für alle Dateien und Ordner, die im Befehl angegeben sind. Wenn Sie diesen Parameter nicht verwenden, wird das Signal an alle Systeme in einer Domäne übertragen. Wenn Sie diesen Parameter verwenden, wird das Signal nur an das angegebene System gesendet. |
| /u `[<domain>]<user>` | Führt das Skript mit den Anmelde Informationen des angegebenen Benutzerkontos aus. Standardmäßig verwendet **WAITFOR** die Anmelde Informationen des aktuellen Benutzers. |
| /p `[\<password>]` | Gibt das Kennwort des Benutzerkontos an, das im **/u** -Parameter angegeben ist. |
| /Si | Sendet das angegebene Signal über das Netzwerk. Mit diesem Parameter können Sie auch ein Signal manuell aktivieren. |
| /t `<timeout>` | Gibt die Anzahl der Sekunden an, die auf ein Signal gewartet werden soll. Standardmäßig wartet **WAITFOR** unbegrenzt. |
| `<signalname>` | Gibt das Signal an, das von **WAITFOR** gewartet oder gesendet wird. Bei diesem Parameter wird die Groß-/Kleinschreibung nicht beachtet, und es dürfen 225 Zeichen Gültige Zeichen sind a-z, a-z, 0-9 und der erweiterte ASCII-Zeichensatz (128-255). |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Hinweise

- Sie können mehrere Instanzen von **WAITFOR** auf einem einzelnen Computer ausführen, aber jede Instanz von **WAITFOR** muss auf ein anderes Signal warten. Nur eine Instanz von **WAITFOR** kann auf ein bestimmtes Signal auf einem bestimmten Computer warten.

- Computer können nur Signale empfangen, wenn Sie sich in derselben Domäne befinden wie der Computer, der das Signal sendet.

- Sie können diesen Befehl verwenden, wenn Sie softwarebuilds testen. Beispielsweise kann der kompilierenden Computer ein Signal an mehrere Computer senden, auf denen **WAITFOR** ausgeführt wird, nachdem die Kompilierung erfolgreich abgeschlossen wurde. Beim Empfang des Signals kann die Batchdatei, die **WAITFOR** enthält, die Computer anweisen, sofort mit der Installation von Software zu beginnen oder Tests für den kompilierten Build ausführen.

## <a name="examples"></a>Beispiele

Um zu warten, bis das Signal *espresso\build007* empfangen wurde, geben Sie Folgendes ein:

```
waitfor espresso\build007
```

Standardmäßig wartet **WAITFOR** unbegrenzt auf ein Signal.

Wenn Sie *10 Sekunden* warten möchten, bis das Signal " *espresso\compile007* " empfangen wird, bevor ein Timeout auftritt, geben Sie Folgendes ein:

```
waitfor /t 10 espresso\build007
```

Um das *espresso\build007* -Signal manuell zu aktivieren, geben Sie Folgendes ein:

```
waitfor /si espresso\build007
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
