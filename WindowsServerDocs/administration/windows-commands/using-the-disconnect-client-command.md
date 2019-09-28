---
title: Verwenden des Disconnect-Client-Befehls
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: dbb96d64b47ec72ff0710bfb3684257c1bda2d04
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71363470"
---
# <a name="using-the-disconnect-client-command"></a>Verwenden des Disconnect-Client-Befehls



Trennt einen Client von einer Multicast Übertragung oder einem Namespace. Wenn Sie **/Force**nicht angeben, greift der Client auf eine andere Übertragungsmethode zurück (wenn Sie vom Client unterstützt wird).

## <a name="syntax"></a>Syntax

```
WDSUTIL /Disconnect-Client /ClientId:<Client ID> [/Server:<Server name>] [/Force]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/ClientID: \<client-ID >|Gibt die ID des Clients an, der getrennt werden soll. Zum Anzeigen der ID eines Clients geben Sie **WDSUTIL/Get-MulticastTransmission/Show: Clients**ein.|
|[/Server: \<Server Name >]|Gibt den Namen des Servers an. Dabei kann es sich um den NetBIOS-Namen oder den voll qualifizierten Domänen Namen (FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
|/Force|Beendet die Installation vollständig und verwendet keine Fall backmethode. Beachten Sie, dass "Wdsmcast. exe" keinen Fall Back Mechanismus unterstützt. Wenn Sie diese Option nicht verwenden, lautet das Standardverhalten wie folgt:</br>: Wenn Sie den Windows-Bereitstellungsdiensteserver verwenden, setzt der Client die Installation mit Unicasting fort.</br>Wenn Sie nicht den Windows-Bereitstellungsdiensteclient verwenden, tritt bei der Installation ein Fehler auf.</br>Wichtig: Verwenden Sie diese Option mit Vorsicht, da die Installation fehlschlägt und der Computer nicht mehr verwendet werden kann.|

## <a name="BKMK_examples"></a>Beispiele

Geben Sie zum Trennen der Verbindung mit einem Client Folgendes ein:
```
WDSUTIL /Disconnect-Client /ClientId:1
```
Geben Sie Folgendes ein, um die Verbindung mit einem Client zu trennen und die Installation zu erzwingen:
```
WDSUTIL /Disconnect-Client /Server:MyWDSServer /ClientId:1 /Force
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)