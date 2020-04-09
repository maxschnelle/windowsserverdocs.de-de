---
title: BIFS admin util und GETIEPROXY
description: Windows-Befehls Thema für bizadmin util und GETIEPROXY, das die Proxy Verwendung für das angegebene Dienst Konto abruft.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 6d50c7e3-f4eb-4ca5-9f0c-4ed396087db6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d0d2a8634f3b42d655632a280cb9b998111c800b
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80848973"
---
# <a name="bitsadmin-util-and-getieproxy"></a>BIFS admin util und GETIEPROXY

> Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ruft die Proxy Verwendung für das angegebene Dienst Konto ab.

## <a name="syntax"></a>Syntax

```
bitsadmin /Util /GetIEProxy <Account> [/Conn <ConnectionName>]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|-------|--------|
|Konto|Gibt das Dienst Konto an, dessen Proxy Einstellungen Sie abrufen möchten. Mögliche Werte:<p>-LocalSystem<br />-NetworkService<br />-LocalService|
|ConnectionName|Optional wird mit dem **/conn** -Parameter verwendet, um die zu verwendende Modemverbindung anzugeben. Wenn Sie den **/conn** -Parameter nicht angeben, verwendet Bits die LAN-Verbindung. Geben Sie den Namen der Modemverbindung direkt nach dem **/conn** -Parameter an.|

## <a name="remarks"></a>Hinweise

Dieser Schalter zeigt den Wert für jede Proxy Verwendung an, nicht nur die Proxy Verwendung, die Sie für das Dienst Konto angegeben haben. Ausführliche Informationen zum Festlegen der Proxy Verwendung für Dienst Konten finden Sie unter dem Schalter [bitadmin util und SETIEPROXY](bitsadmin-util-and-setieproxy.md) .

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Im folgenden Beispiel wird die Proxy Verwendung für das Netzwerkdienst Konto angezeigt.

```
C:\>bitsadmin /Util /GetIEProxy NETWORKSERVICE
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
