---
title: Mithilfe des neuen Namespace-Befehls
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6df60703-30bd-4d59-a8d9-9fe3efe96add
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 50d51101afe95c99b7034fc50b3d30b799ee02ce
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59871151"
---
# <a name="using-the-new-namespace-command"></a>Mithilfe des neuen Namespace-Befehls

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

erstellt und konfiguriert einen neuen Namespace. Sie sollten diese Option verwenden, wenn Sie lediglich der Transportserver-Rollendienst installiert haben. Wenn Sie sowohl die Bereitstellungsserver-Rollendienst, und der Transportserver-Rollendienst installiert (der Standardwert ist), verwenden Sie [mit dem Befehl new-MulticastTransmission](using-the-new-multicasttransmission-command.md). Beachten Sie, dass Sie auf den Inhaltsanbieter registrieren müssen, bevor Sie diese Option verwenden.
## <a name="syntax"></a>Syntax
```
wdsutil [Options] /New-Namespace [/Server:<Server name>]
     /FriendlyName:<Friendly name>
     [/Description:<Description>]
     /Namespace:<Namespace name>
     /ContentProvider:<Name>
     [/ConfigString:<Configuration string>]
     /Namespacetype: {AutoCast | ScheduledCast}
         [/time:<YYYY/MM/DD:hh:mm>]
         [/Clients:<Number of clients>]
```
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Dies kann den NetBIOS-Namen oder den vollständig qualifizierten Domänennamen (FQDN) sein. Wenn kein Servername angegeben wird, wird der lokale Server verwendet.|
|/FriendlyName:<Friendly name>|Gibt den Anzeigenamen des Namespaces an.|
|[/ Description:<Description>]|Legt die Beschreibung des Namespaces fest.|
|/Namespace:<Namespace name>|Gibt den Namen des Namespaces. Beachten Sie, dass dies nicht der Anzeigename, und muss eindeutig sein.<br /><br />-   **Deployment Server-Rollendienst**: Die Syntax für diese Option ist /Namespace:WDS:<Image group>/<Image name>/<Index>. Zum Beispiel: **WDS:ImageGroup1/install.wim/1**<br />-   **Transport-Server-Rollendienst**: Dieser Wert sollte der Name angegeben wird, wenn der Namespace, auf dem Server erstellt wurde übereinstimmen.|
|/ContentProvider:<Name>]|Gibt den Namen des Content-Anbieters, die Inhalt für den Namespace bereitstellen.|
|[/ConfigString:<Configuration string>]|Gibt die Konfigurationszeichenfolge für den Inhaltsanbieter an.|
|/Namespacetype: {AutoCast &#124; ScheduledCast}|Gibt die Einstellungen für die Übertragung. Sie geben Sie die Einstellungen, die mithilfe der folgenden Optionen:<br /><br />-[/ time: <time>] – die Zeit, die die Übertragung gestartet werden soll, mithilfe des folgenden Formats: YYYY/MM/DD:hh:mm. Diese Option gilt nur für Übertragungen mit geplanter Umwandlung.<br />-[/ Clients: <Number of clients>]-legt die minimale Anzahl von Clients warten, bevor die Übertragung gestartet wird. Diese Option gilt nur für Übertragungen mit geplanter Umwandlung.|
## <a name="BKMK_examples"></a>Beispiele für
Um einen automatischen Cast-Namespace zu erstellen, geben Sie Folgendes ein:
```
wdsutil /New-Namespace /FriendlyName:"Custom AutoCast Namespace" /Namespace:"Custom Auto 1" /ContentProvider:MyContentProvider /Namespacetype:AutoCast
```
Um einen geplanten Cast-Namespace zu erstellen, geben Sie Folgendes ein:
```
wdsutil /New-Namespace /Server:MyWDSServer /FriendlyName:"Custom Scheduled Namespace" /Namespace:"Custom Auto 1" /ContentProvider:MyContentProvider 
/Namespacetype:ScheduledCast /time:"2006/11/20:17:00" /Clients:20
```
#### <a name="additional-references"></a>Zusätzliche Referenzen
[Befehlszeilen-Syntaxschlüssel](command-line-syntax-key.md)
[mit dem Befehl Get-AllNamespaces](using-the-get-allnamespaces-command.md)
[mit dem Befehl Remove-Namespace](using-the-remove-namespace-command.md) 
 [ Unterbefehl: Start-Namespace](subcommand-start-namespace.md)
