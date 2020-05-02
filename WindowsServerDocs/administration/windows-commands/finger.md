---
title: finger
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 907ea637-5c6c-4752-84c2-46bbf2a68a33
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ec8040480a7cb75a5a42e051393e3db4a47f8e2f
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725617"
---
# <a name="finger"></a>finger

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt Informationen zu einem Benutzer oder Benutzern auf einem angegebenen Remote Computer an (in der Regel ein Computer, auf dem UNIX ausgeführt wird), auf dem der Fingerdienst oder der Daemon ausgeführt wird. Der Remote Computer gibt das Format und die Ausgabe der Anzeige der Benutzerinformationen an. Wird ohne Parameter verwendet **und zeigt** Hilfe an. 
## <a name="syntax"></a>Syntax
```
finger [-l] [<User>] [@<Host>] [...]
```
#### <a name="parameters"></a>Parameter

| Parameter |                                                                            BESCHREIBUNG                                                                            |
|-----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    -l     |                                                          Zeigt Benutzerinformationen im langen Listenformat an.                                                           |
|  <User>   | Gibt den Benutzer an, zu dem Sie Informationen benötigen. Wenn Sie den Parameter " *User* " weglassen, zeigt **Finger** Informationen zu allen Benutzern auf dem angegebenen Computer an. |
|  @<Host>  |        Gibt den Remote Computer an, auf dem der Finger Dienst ausgeführt wird, auf dem Sie nach Benutzerinformationen suchen. Sie können einen Computernamen oder eine IP-Adresse angeben.        |
|    /?     |                                                               Zeigt die Hilfe an der Eingabeaufforderung an.                                                                |

## <a name="remarks"></a>Bemerkungen
Es User@Host können mehrere Parameter angegeben werden.
Sie müssen **Finger** Parametern mit einem Bindestrich (-) anstelle eines Schrägstrichs (/) als Präfix versehen.
Dieser Befehl ist nur verfügbar, wenn das TCP/IP-Protokoll (Internet Protocol) als Komponente in den Eigenschaften eines Netzwerkadapters in Netzwerkverbindungen installiert ist.
Windows Server 2003 stellt keinen Finger Dienst bereit.
## <a name="examples"></a>Beispiele
Geben Sie Folgendes ein, um Informationen für user1 auf dem Computer users.Microsoft.com anzuzeigen:
```
finger user1@users.microsoft.com
```
Geben Sie Folgendes ein, um Informationen für alle Benutzer auf dem Computer users.Microsoft.com anzuzeigen:
```
finger @users.microsoft.com
```
## <a name="additional-references"></a>Zusätzliche Referenzen
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
