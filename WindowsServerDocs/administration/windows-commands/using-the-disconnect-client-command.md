---
title: Disconnect-Client
description: Referenz Artikel für Disconnect-Client, der einen Client von einer Multicast Übertragung oder einem Namespace trennt.
ms.topic: reference
ms.assetid: 876bbe6c-76ab-4de5-879b-d2066e700326
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 902d488a20391cb4317931aeb2572655d9aa291a
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89622010"
---
# <a name="disconnect-client"></a>Disconnect-Client

Trennt einen Client von einer Multicast Übertragung oder einem Namespace. Wenn Sie **/Force**nicht angeben, greift der Client auf eine andere Übertragungsmethode zurück (wenn Sie vom Client unterstützt wird).

## <a name="syntax"></a>Syntax

```
WDSUTIL /Disconnect-Client /ClientId:<Client ID> [/Server:<Server name>] [/Force]
```

### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|ClientID\<Client ID>|Gibt die ID des Clients an, der getrennt werden soll. Zum Anzeigen der ID eines Clients geben Sie **WDSUTIL/Get-MulticastTransmission/Show: Clients**ein.|
|[/Server:\<Server name>]|Gibt den Namen des Servers an. Dabei kann es sich um den NetBIOS-Namen oder den voll qualifizierten Domänen Namen (FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
|/Force|Beendet die Installation vollständig und verwendet keine Fall backmethode. Beachten Sie, dass Wdsmcast.exe keinen Fall Back Mechanismus unterstützt. Wenn Sie diese Option nicht verwenden, lautet das Standardverhalten wie folgt:</br>: Wenn Sie den Windows-Bereitstellungsdiensteserver verwenden, setzt der Client die Installation mit Unicasting fort.</br>Wenn Sie nicht den Windows-Bereitstellungsdiensteclient verwenden, tritt bei der Installation ein Fehler auf.</br>Wichtig: Verwenden Sie diese Option mit Vorsicht, da die Installation fehlschlägt und der Computer in einem nicht verwendbaren Zustand belassen wird.|

## <a name="examples"></a>Beispiele

Geben Sie zum Trennen der Verbindung mit einem Client Folgendes ein:
```
WDSUTIL /Disconnect-Client /ClientId:1
```
Geben Sie Folgendes ein, um die Verbindung mit einem Client zu trennen und die Installation zu erzwingen:
```
WDSUTIL /Disconnect-Client /Server:MyWDSServer /ClientId:1 /Force
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)