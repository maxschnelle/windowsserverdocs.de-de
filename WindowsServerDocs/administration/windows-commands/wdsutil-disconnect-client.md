---
title: WDSUTIL Disconnect-Client
description: Referenz Artikel für den Befehl WDSUTIL Disconnect-Client, der einen Client von einer Multicast Übertragung oder einem Namespace trennt.
ms.topic: reference
ms.assetid: 876bbe6c-76ab-4de5-879b-d2066e700326
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: dd837fd9a677f78b5890cd1f2092529d44a2bc68
ms.sourcegitcommit: b115e5edc545571b6ff4f42082cc3ed965815ea4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/30/2020
ms.locfileid: "93070332"
---
# <a name="wdsutil-disconnect-client"></a>WDSUTIL Disconnect-Client

Trennt einen Client von einer Multicast Übertragung oder einem Namespace. Wenn Sie **/Force** nicht angeben, greift der Client auf eine andere Übertragungsmethode zurück (wenn Sie vom Client unterstützt wird).

## <a name="syntax"></a>Syntax

```
wdsutil /Disconnect-Client /ClientId:<Client ID> [/Server:<Server name>] [/Force]
```

### <a name="parameters"></a>Parameter

| Parameter | Description |
|--|--|
| ClientID`<ClientID>` | Gibt die ID des Clients an, der getrennt werden soll. Um die ID eines Clients anzuzeigen, führen Sie den `wdsutil /get-multicasttransmission /show:clients` Befehl aus. |
| [/Server:`<Servername>`] | Gibt den Namen des Servers an. Dabei kann es sich um den NetBIOS-Namen oder den voll qualifizierten Domänen Namen (FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet. |
| /Force | Beendet die Installation vollständig und verwendet keine Fall backmethode. Da Wdsmcast.exe keinen Fall Back Mechanismus unterstützt, lautet das Standardverhalten wie folgt:<ul><li>**Wenn Sie den Windows-Bereitstellungsdiensteclient verwenden:** Der Client setzt die Installation mit Unicasting fort.</li><li>**Wenn Sie nicht den Windows-Bereitstellungsdiensteclient verwenden:** Die Installation schlägt fehl.</li></ul>**Wichtig:** Es wird dringend empfohlen, diesen Parameter vorsichtig zu verwenden, denn wenn die Installation fehlschlägt, kann der Computer in einem nicht verwendbaren Zustand bleiben. |

## <a name="examples"></a>Beispiele

Geben Sie zum Trennen der Verbindung mit einem Client Folgendes ein:

```
wdsutil /Disconnect-Client /ClientId:1
```

Geben Sie Folgendes ein, um die Verbindung mit einem Client zu trennen und die Installation zu erzwingen:

```
wdsutil /Disconnect-Client /Server:MyWDSServer /ClientId:1 /Force
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [WDSUTIL Get-MulticastTransmission-Befehl](wdsutil-get-multicasttransmission.md)

- [Cmdlets für die Windows-Bereitstellungs Dienste](/powershell/module/wds)
