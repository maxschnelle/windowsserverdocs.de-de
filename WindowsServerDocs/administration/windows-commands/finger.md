---
title: finger
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 42622fdf19cdd50b76d32989769874cbd05e9f4a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59826941"
---
# <a name="finger"></a>finger

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Zeigt Informationen zu einem Benutzer oder Benutzern auf einem angegebenen Remotecomputer (normalerweise ein Computer unter UNIX) an, die die Finger-Dienst oder -Daemon ausgeführt wird. Der Remotecomputer gibt das Format und die Ausgabe von dem Benutzer Informationen die Anzeige. Ohne Parameter verwendet **Finger** zeigt die Hilfe. 
## <a name="syntax"></a>Syntax
```
finger [-l] [<User>] [@<Host>] [...]
```
### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|-l|Werden die Benutzerinformationen in Form einer langen Liste angezeigt.|
|<User>|Gibt den Benutzer darüber, den welche Informationen angezeigt werden soll. Wenn Sie weglassen der *Benutzer* Parameter **Finger** zeigt Informationen zu allen Benutzern auf dem angegebenen Computer.|
|@<Host>|Gibt dem Remotecomputer mit dem Fingerdienst, in dem nach Benutzerinformationen möchten Sie an. Sie können einen Computernamen oder IP-Adresse angeben.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|
## <a name="remarks"></a>Hinweise
Mehrere User@Host Parameter können angegeben werden.
Sie müssen das Präfix **Finger** Parameter mit einem Bindestrich (-) statt mit einem Schrägstrich (/).
Dieser Befehl ist nur verfügbar, wenn das Internetprotokoll (TCP/IP)-Protokoll als Komponente in den Eigenschaften eines Netzwerkadapters in den Netzwerkverbindungen installiert ist.
Der Windows Server 2003 bietet keine Finger-Dienst.
## <a name="BKMK_Examples"></a>Beispiele für
Um Informationen für "user1" auf dem Computer users.microsoft.com anzuzeigen, geben Sie Folgendes ein:
```
finger user1@users.microsoft.com
```
Um Informationen für alle Benutzer auf dem Computer users.microsoft.com anzuzeigen, geben Sie Folgendes ein:
```
finger @users.microsoft.com
```
## <a name="additional-references"></a>Zusätzliche Referenzen
-   [Befehlszeilensyntax](command-line-syntax-key.md)
