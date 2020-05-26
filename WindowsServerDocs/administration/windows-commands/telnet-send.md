---
title: Telnet-Sendevorgang
description: Referenz Thema für Telnet Send, das Telnet-Befehle an den Telnet-Server sendet.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7c217abc-1182-466e-914c-1ff16755021b vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5dd4bf9828c4b71e7b2291dfd5d453c43679e059
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2020
ms.locfileid: "83821070"
---
# <a name="telnet-send"></a>Telnet: senden

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Sendet Telnet-Befehle an den Telnet-Server.

## <a name="syntax"></a>Syntax
```
sen[d] {ao | ayt | brk | esc | ip | synch | <string>} [?]
```
#### <a name="parameters"></a>Parameter

| Parameter |                     BESCHREIBUNG                      |
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
## <a name="additional-references"></a>Zusätzliche Referenzen
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
