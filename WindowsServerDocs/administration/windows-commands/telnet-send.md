---
title: telnet send
description: Referenz Artikel für Telnet Send, bei dem Telnet-Befehle an den Telnet-Server gesendet werden.
ms.topic: reference
ms.assetid: 7c217abc-1182-466e-914c-1ff16755021b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4e8621d163e4f0bf7022f2cab1a67f188bc47dfd
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89024584"
---
# <a name="telnet-send"></a>Telnet: senden

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Sendet Telnet-Befehle an den Telnet-Server.

## <a name="syntax"></a>Syntax
```
sen[d] {ao | ayt | brk | esc | ip | synch | <string>} [?]
```
#### <a name="parameters"></a>Parameter

| Parameter |                     Beschreibung                      |
|-----------|------------------------------------------------------|
|    OS     |       Sendet die Ausgabe des Telnet-Befehls abgebrochen.        |
|    AYT    |       Sendet den Telnet-Befehl.       |
|    BRK    |            Sendet den Telnet-Befehl BRK.            |
|    ESC-TASTE    |      Sendet das aktuelle Telnet-Escapezeichen.      |
|    ip     |     Sendet den Telnet-Befehls Unterbrechungs Prozess.     |
|   synch   |           Sendet den Telnet-Befehl "Synch".           |
| <string>  | Sendet jede Zeichenfolge, die Sie an den Telnet-Server eingeben. |
|     ?     |     Zeigt die diesem Befehl zugeordnete Hilfe an.      |

## <a name="examples"></a>Beispiele
Senden Sie an den Telnet-Server.
```
sen ayt
```
## <a name="additional-references"></a>Weitere Verweise
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
