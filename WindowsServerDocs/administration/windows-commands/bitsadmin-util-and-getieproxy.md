---
title: bitsadmin util and getieproxy
description: Referenz Artikel für den Befehl bizadmin util und GETIEPROXY, der die Proxy Verwendung für das angegebene Dienst Konto abruft.
ms.topic: reference
ms.assetid: 6d50c7e3-f4eb-4ca5-9f0c-4ed396087db6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 87a67dbdf1495b3cb8398fdbc0cc3cfed1c4e577
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89033258"
---
# <a name="bitsadmin-util-and-getieproxy"></a>bitsadmin util and getieproxy

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ruft die Proxy Verwendung für das angegebene Dienst Konto ab. Dieser Befehl zeigt den Wert für jede Proxy Verwendung an, nicht nur die Proxy Verwendung, die Sie für das Dienst Konto angegeben haben. Ausführliche Informationen zum Festlegen der Proxy Verwendung für bestimmte Dienst Konten finden Sie unter dem Befehl [bizadmin util und SETIEPROXY](bitsadmin-util-and-setieproxy.md) .

## <a name="syntax"></a>Syntax

```
bitsadmin /util /getieproxy <account> [/conn <connectionname>]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ---------- |
| account | Gibt das Dienst Konto an, dessen Proxy Einstellungen Sie abrufen möchten. Mögliche Werte sind:<ul><li>LOCALSYSTEM</li><li>   Network Service</li><li>LOCALSERVICE.</li></ul> |
| ConnectionName | Optional. Wird zusammen mit dem **/conn** -Parameter verwendet, um anzugeben, welche Modemverbindung verwendet werden soll. Wenn Sie den **/conn** -Parameter nicht angeben, verwendet Bits die LAN-Verbindung. |

## <a name="examples"></a>Beispiele

So zeigen Sie die Proxy Verwendung für das Netzwerkdienst Konto an

```
bitsadmin /util /getieproxy NETWORKSERVICE
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Befehl "BIFS admin util"](bitsadmin-util.md)

- [Bider admin-Befehl](bitsadmin.md)
