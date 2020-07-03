---
title: New-Namespace
description: Referenz Artikel für New-Namespace, der einen neuen Namespace erstellt und konfiguriert.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 6df60703-30bd-4d59-a8d9-9fe3efe96add
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3afbdd195f21450508bfa6992fc73c7d360092c6
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85932412"
---
# <a name="new-namespace"></a>New-Namespace

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Erstellt und konfiguriert einen neuen Namespace. Sie sollten diese Option verwenden, wenn nur der Transport Server-Rollen Dienst installiert ist. Wenn Sie sowohl den Rollen Dienst "Bereitstellungs Server" als auch den Transport Server-Rollen Dienst installiert haben (Dies ist die Standardeinstellung), verwenden Sie [den Befehl "New-MulticastTransmission](using-the-new-multicasttransmission-command.md)". Beachten Sie, dass Sie den Inhaltsanbieter registrieren müssen, bevor Sie diese Option verwenden.
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
### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Dabei kann es sich um den NetBIOS-Namen oder den voll qualifizierten Domänen Namen (FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
|FriendlyName<Friendly name>|Gibt den anzeigen Amen für den Namespace an.|
|/Description<Description>]|Legt die Beschreibung des Namespace fest.|
|Namespace<Namespace name>|Gibt den Namen des Namespace an. Beachten Sie, dass dies nicht der Anzeige Name ist und eindeutig sein muss.<p>-   **Rollen Dienst "Bereitstellungs Server**": die Syntax für diese Option lautet/Namespace: WDS: <Image group> / <Image name> / <Index> . Beispiel: **WDS: ImageGroup1/install. wim/1**<br />-   **Transport Server-Rollen Dienst**: dieser Wert sollte dem Namen entsprechen, der beim Erstellen des Namespace auf dem Server angegeben wurde.|
|/Contentprovider: <Name> ]|Gibt den Namen des Inhalts Anbieters an, der Inhalt für den Namespace bereitstellt.|
|[/ConfigString: <Configuration string> ]|Gibt die Konfigurations Zeichenfolge für den Inhaltsanbieter an.|
|/NamespaceType: {AutoCast &#124; ScheduledCast}|Gibt die Einstellungen für die Übertragung an. Sie geben die Einstellungen mithilfe der folgenden Optionen an:<p>-[/Time: <time> ]: legt fest, wie lange die Übertragung beginnen soll, indem Sie das folgende Format verwendet: yyyy/mm/dd: hh: mm. Diese Option gilt nur für geplante Umwandlungs Übertragungen.<br />-[/Clients: <Number of clients> ]: legt die Mindestanzahl von Clients fest, auf die gewartet werden soll, bevor die Übertragung beginnt. Diese Option gilt nur für geplante Umwandlungs Übertragungen.|
## <a name="examples"></a>Beispiele
Geben Sie Folgendes ein, um einen Namespace für die automatische Umwandlung zu erstellen:
```
wdsutil /New-Namespace /FriendlyName:Custom AutoCast Namespace /Namespace:Custom Auto 1 /ContentProvider:MyContentProvider /Namespacetype:AutoCast
```
Geben Sie Folgendes ein, um einen geplantes Cast-Namespace zu erstellen:
```
wdsutil /New-Namespace /Server:MyWDSServer /FriendlyName:Custom Scheduled Namespace /Namespace:Custom Auto 1 /ContentProvider:MyContentProvider
/Namespacetype:ScheduledCast /time:2006/11/20:17:00 /Clients:20
```
## <a name="additional-references"></a>Weitere Verweise
- [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md) 
 [Verwenden des Befehls](using-the-get-allnamespaces-command.md) 
 get-allnamespaces [Verwenden des Remove-Namespace-Befehls](using-the-remove-namespace-command.md) 
 [Unterbefehl: Start-Namespace](subcommand-start-namespace.md)
