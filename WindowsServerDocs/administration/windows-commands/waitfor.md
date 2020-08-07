---
title: waitfor
description: Referenz Artikel zu WAITFOR, der ein Signal an ein System sendet oder darauf wartet. **WAITFOR** wird zum Synchronisieren von Computern in einem Netzwerk verwendet.
ms.topic: article
ms.assetid: a48ef70d-4d28-4035-b6b0-7d7b46ac2157
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e061c36f7cdf949ea76d548a4ed804a0e12169bf
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87892248"
---
# <a name="waitfor"></a>waitfor



Sendet oder wartet auf ein Signal auf einem System. **WAITFOR** wird zum Synchronisieren von Computern in einem Netzwerk verwendet.



## <a name="syntax"></a>Syntax

```
waitfor [/s <Computer> [/u [<Domain>\]<User> [/p [<Password>]]]] /si <SignalName>
waitfor [/t <Timeout>] <SignalName>
```

### <a name="parameters"></a>Parameter

|       Parameter       |                                                                                         BESCHREIBUNG                                                                                          |
|-----------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    /s\<Computer>     | Gibt den Namen oder die IP-Adresse eines Remote Computers an (verwenden Sie keine umgekehrten Schrägstriche). Die Standardeinstellung ist der lokale Computer. Dieser Parameter gilt für alle Dateien und Ordner, die im Befehl angegeben sind. |
| u\<Domain>\]<User> |                              Führt das Skript mit den Anmelde Informationen des angegebenen Benutzerkontos aus. Standardmäßig verwendet **WAITFOR** die Anmelde Informationen des aktuellen Benutzers.                               |
|   /p [ \<Password> ]    |                                                    Gibt das Kennwort des Benutzerkontos an, das im **/u** -Parameter angegeben ist.                                                     |
|          /Si          |                                                                        Sendet das angegebene Signal über das Netzwerk.                                                                        |
|     /t\<Timeout>     |                                              Gibt die Anzahl der Sekunden an, die auf ein Signal gewartet werden soll. Standardmäßig wartet **WAITFOR** unbegrenzt.                                               |
|     \<SignalName>     |                                                Gibt das Signal an, das von **WAITFOR** gewartet oder gesendet wird. Bei *Signalname* wird keine Groß-/Kleinschreibung beachtet.                                                 |
|          /?           |                                                                             Zeigt die Hilfe an der Eingabeaufforderung an.                                                                             |

## <a name="remarks"></a>Bemerkungen

-   Signal Namen dürfen nicht länger als 225 Zeichen sein. Gültige Zeichen sind a-z, a-z, 0-9 und der erweiterte ASCII-Zeichensatz (128-255).
-   Wenn Sie **/s**nicht verwenden, wird das Signal an alle Systeme in einer Domäne übertragen. Wenn Sie **/s**verwenden, wird das Signal nur an das angegebene System gesendet.
-   Sie können mehrere Instanzen von **WAITFOR** auf einem einzelnen Computer ausführen, aber jede Instanz von **WAITFOR** muss auf ein anderes Signal warten. Nur eine Instanz von **WAITFOR** kann auf ein bestimmtes Signal auf einem bestimmten Computer warten.
-   Sie können ein Signal manuell aktivieren, indem Sie die Befehlszeilenoption **/Si** verwenden.
-   **WAITFOR** wird nur unter Windows XP und Servern ausgeführt, auf denen das Betriebssystem Windows Server 2003 ausgeführt wird, aber es kann Signale an jeden Computer senden, auf dem ein Windows-Betriebssystem ausgeführt wird.
-   Computer können nur Signale empfangen, wenn Sie sich in derselben Domäne befinden wie der Computer, der das Signal sendet.
-   Sie können **WAITFOR** verwenden, wenn Sie softwarebuilds testen. Beispielsweise kann der kompilierenden Computer ein Signal an mehrere Computer senden, auf denen **WAITFOR** ausgeführt wird, nachdem die Kompilierung erfolgreich abgeschlossen wurde. Beim Empfang des Signals kann die Batchdatei, die **WAITFOR** enthält, die Computer anweisen, sofort mit der Installation von Software zu beginnen oder Tests für den kompilierten Build ausführen.

## <a name="examples"></a>Beispiele

Um zu warten, bis das Signal espresso\build007 empfangen wurde, geben Sie Folgendes ein:
```
waitfor espresso\build007
```
Standardmäßig wartet **WAITFOR** unbegrenzt auf ein Signal.

Wenn Sie 10 Sekunden warten möchten, bis das Signal "espresso\compile007" empfangen wird, bevor ein Timeout auftritt, geben Sie Folgendes ein:
```
waitfor /t 10 espresso\build007
```
Um das espresso\build007-Signal manuell zu aktivieren, geben Sie Folgendes ein:
```
waitfor /si espresso\build007
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)