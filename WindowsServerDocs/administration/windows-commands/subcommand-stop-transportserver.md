---
title: Stop-TransportServer Unterbefehl
description: Windows-Befehle Beenden-TransportServer-Thema
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: dc1b1eec-6893-445e-81dc-16b3fae287fa
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8f7410a8720337e509325b99863446bd8d19eb26
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59853451"
---
# <a name="subcommand-stop-transportserver"></a>Subcommand: stop-TransportServer

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Beendet alle Dienste auf einem Transport-Server.
## <a name="syntax"></a>Syntax
```
wdsutil [Options] /Stop-TransportServer [/Server:<Server name>]
```
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|[/Server:<Server name>]|Gibt den Namen des Transport-Servers. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Transport-Server angegeben wird, wird der lokale Server verwendet werden.|
## <a name="BKMK_examples"></a>Beispiele für
Geben Sie eine der folgenden Schritte aus, um die Dienste zu beenden:
```
wdsutil /Stop-TransportServer
wdsutil /verbose /Stop-TransportServer /Server:MyWDSServer
```
#### <a name="additional-references"></a>Zusätzliche Referenzen
[Befehlszeilen-Syntaxschlüssel](command-line-syntax-key.md)
[mit dem Disable-TransportServer-Befehl](using-the-disable-transportserver-command.md)
[mithilfe des Befehls Enable-TransportServer](using-the-enable-transportserver-command.md) 
 [ Mit dem Befehl Get-TransportServer](using-the-get-transportserver-command.md)
[Unterbefehl: Set-TransportServer](subcommand-set-transportserver.md)
[Unterbefehl: Start-TransportServer](subcommand-start-transportserver.md)
