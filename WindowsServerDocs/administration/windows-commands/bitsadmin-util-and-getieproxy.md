---
title: BIFS admin util und GETIEPROXY
description: 'Windows-Befehls Thema für **bizadmin util und GETIEPROXY** : Ruft die Proxy Verwendung für das angegebene Dienst Konto ab.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6d50c7e3-f4eb-4ca5-9f0c-4ed396087db6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6936e088ddcf467b5a8f931bc8217ba9da4662c2
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380271"
---
# <a name="bitsadmin-util-and-getieproxy"></a>BIFS admin util und GETIEPROXY

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ruft die Proxy Verwendung für das angegebene Dienst Konto ab.

## <a name="syntax"></a>Syntax

```
bitsadmin /Util /GetIEProxy <Account> [/Conn <ConnectionName>]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|-------|--------|
|Konto|Gibt das Dienst Konto an, dessen Proxy Einstellungen Sie abrufen möchten. Dabei sind folgende Werte möglich:<br /><br />-LOCALSYSTEM<br />-NETWORKSERVICE<br />-LOCALSERVICE|
|ConnectionName|Optional wird mit dem **/conn** -Parameter verwendet, um die zu verwendende Modemverbindung anzugeben. Wenn Sie den **/conn** -Parameter nicht angeben, verwendet Bits die LAN-Verbindung. Geben Sie den Namen der Modemverbindung direkt nach dem **/conn** -Parameter an.|

## <a name="remarks"></a>Hinweise

Dieser Schalter zeigt den Wert für jede Proxy Verwendung an, nicht nur die Proxy Verwendung, die Sie für das Dienst Konto angegeben haben. Ausführliche Informationen zum Festlegen der Proxy Verwendung für Dienst Konten finden Sie unter dem Schalter [bitadmin util und SETIEPROXY](bitsadmin-util-and-setieproxy.md) .

## <a name="BKMK_examples"></a>Beispiele

Im folgenden Beispiel wird die Proxy Verwendung für das Netzwerkdienst Konto angezeigt.

```
C:\>bitsadmin /Util /GetIEProxy NETWORKSERVICE
```

## <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
