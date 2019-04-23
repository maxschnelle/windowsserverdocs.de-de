---
title: Mithilfe des Befehls Disable-TransportServer
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a009706b-8e89-486b-8e3d-512cd9f4de74
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d653aacf225333ac8a8b090ef53fb6826e84ab5c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59836981"
---
# <a name="using-the-disable-transportserver-command"></a>Mithilfe des Befehls Disable-TransportServer

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Deaktiviert alle Dienste für einen Transport-Server an.
## <a name="syntax"></a>Syntax
```
wdsutil [Options] /Disable-TransportServer [/Server:<Server name>]
```
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|[/Server:<Server name>]|Gibt den Namen der dem Transport-Server deaktiviert werden soll. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Transport-Server-Name angegeben ist, wird der lokale Server verwendet werden.|
## <a name="BKMK_examples"></a>Beispiele für
Um den Server zu deaktivieren, geben Sie Folgendes ein:
```
wdsutil /Disable-TransportServer
wdsutil /verbose /Disable-TransportServer /Server:MyWDSServer
```
#### <a name="additional-references"></a>Zusätzliche Referenzen
[Befehlszeilen-Syntaxschlüssel](command-line-syntax-key.md)
[mithilfe des Befehls Enable-TransportServer](using-the-enable-transportserver-command.md)
[mit dem Befehl Get-TransportServer](using-the-get-transportserver-command.md) 
 [Unterbefehl: Set-TransportServer](subcommand-set-transportserver.md)
[Unterbefehl: Start-TransportServer](subcommand-start-transportserver.md)
[Unterbefehl: Stop-TransportServer](subcommand-stop-transportserver.md)
