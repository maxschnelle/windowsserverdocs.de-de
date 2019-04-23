---
title: Mithilfe des Befehls trennen-Client
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 876bbe6c-76ab-4de5-879b-d2066e700326
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b89f6c2ff6d41230afd0a2b251ad6982dfa235b1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59841751"
---
# <a name="using-the-disconnect-client-command"></a>Mithilfe des Befehls trennen-Client



Trennt einen Client aus einer Multicastübertragung oder einem Namespace an. Es sei denn, Sie geben **/Force**, der Client wird ein Fallback auf eine andere Übertragungsmethode (wenn es vom Client unterstützt wird).

## <a name="syntax"></a>Syntax

```
WDSUTIL /Disconnect-Client /ClientId:<Client ID> [/Server:<Server name>] [/Force]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/ClientId:\<Client ID>|Gibt die ID des Clients getrennt werden soll. Geben Sie zum Anzeigen der ID eines Clients **WDSUTIL /get-multicasttransmission /show:clients**.|
|[/ Server:\<Servername >]|Gibt den Namen des Servers an. Dies kann den NetBIOS-Namen oder den vollständig qualifizierten Domänennamen (FQDN) sein. Wenn kein Servername angegeben wird, wird der lokale Server verwendet.|
|[/Force]|Die Installation vollständig angehalten, und verwendet eine alternative Methode nicht. Beachten Sie, dass Wdsmcast.exe fallback-Mechanismus nicht unterstützt. Wenn Sie diese Option nicht verwenden, ist das Standardverhalten wie folgt:</br>– Wenn Sie die Windows-Bereitstellungsdienste-Client verwenden, wird der Client die Installation von per Unicasting fortgesetzt.</br>– Wenn Sie die Windows-Bereitstellungsdienste-Client nicht verwenden, schlägt die Installation.</br>Wichtig: Sie sollten diese Option mit Vorsicht verwenden, da die Installation fehl und der Computer in einem nicht verwendbaren Zustand bleibt womöglich.|

## <a name="BKMK_examples"></a>Beispiele für

Wenn einen Client trennen möchten, geben Sie Folgendes ein:
```
WDSUTIL /Disconnect-Client /ClientId:1
```
Trennen von einem Client, und erzwingen die Installation nicht mehr aus, geben Sie Folgendes ein:
```
WDSUTIL /Disconnect-Client /Server:MyWDSServer /ClientId:1 /Force
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)