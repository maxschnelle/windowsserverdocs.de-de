---
title: finger
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 907ea637-5c6c-4752-84c2-46bbf2a68a33
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8e16120eb19ff2f194fe2c8bdeb3af80ca459ebe
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71377164"
---
# <a name="finger"></a>finger

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt Informationen zu einem Benutzer oder Benutzern auf einem angegebenen Remote Computer an (in der Regel ein Computer, auf dem UNIX ausgeführt wird), auf dem der Fingerdienst oder der Daemon ausgeführt wird. Der Remote Computer gibt das Format und die Ausgabe der Anzeige der Benutzerinformationen an. Wird ohne Parameter verwendet **und zeigt** Hilfe an. 
## <a name="syntax"></a>Syntax
```
finger [-l] [<User>] [@<Host>] [...]
```
### <a name="parameters"></a>Parameter

| Parameter |                                                                            Beschreibung                                                                            |
|-----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    -l     |                                                          Zeigt Benutzerinformationen im langen Listenformat an.                                                           |
|  <User>   | Gibt den Benutzer an, zu dem Sie Informationen benötigen. Wenn Sie den Parameter " *User* " weglassen, zeigt **Finger** Informationen zu allen Benutzern auf dem angegebenen Computer an. |
|  @<Host>  |        Gibt den Remote Computer an, auf dem der Finger Dienst ausgeführt wird, auf dem Sie nach Benutzerinformationen suchen. Sie können einen Computernamen oder eine IP-Adresse angeben.        |
|    /?     |                                                               Zeigt die Hilfe an der Eingabeaufforderung an.                                                                |

## <a name="remarks"></a>Hinweise
Es können mehrere User@Host-Parameter angegeben werden.
Sie müssen **Finger** Parametern mit einem Bindestrich (-) anstelle eines Schrägstrichs (/) als Präfix versehen.
Dieser Befehl ist nur verfügbar, wenn das TCP/IP-Protokoll (Internet Protocol) als Komponente in den Eigenschaften eines Netzwerkadapters in Netzwerkverbindungen installiert ist.
Windows Server 2003 stellt keinen Finger Dienst bereit.
## <a name="BKMK_Examples"></a>Beispiele
Geben Sie Folgendes ein, um Informationen für user1 auf dem Computer users.Microsoft.com anzuzeigen:
```
finger user1@users.microsoft.com
```
Geben Sie Folgendes ein, um Informationen für alle Benutzer auf dem Computer users.Microsoft.com anzuzeigen:
```
finger @users.microsoft.com
```
## <a name="additional-references"></a>Weitere Verweise
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
