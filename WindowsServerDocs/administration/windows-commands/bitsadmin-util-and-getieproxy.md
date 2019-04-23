---
title: Bitsadmin Util und getieproxy
description: Windows-Befehle Thema **Bitsadmin Util und Getieproxy** -Ruft die Proxyverwendung für das angegebene Dienstkonto.
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: de4f86340b1163c4d8e3286d9c86c9df794a21c5
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59876871"
---
# <a name="bitsadmin-util-and-getieproxy"></a>Bitsadmin Util und getieproxy

> Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Ruft die Proxyverwendung für das angegebene Dienstkonto ab.

## <a name="syntax"></a>Syntax

```
bitsadmin /Util /GetIEProxy <Account> [/Conn <ConnectionName>]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|-------|--------|
|Konto|Gibt an, das Dienstkonto, dessen Proxyeinstellungen, die Sie abrufen möchten. Dabei sind folgende Werte möglich:<br /><br />-"LOCALSYSTEM"<br />-NETWORKSERVICE<br />-"LOCALSERVICE"|
|ConnectionName|Optional verwendet werden, mit der **/Conn** Parameter, um die zu verwendende modemverbindung anzugeben. Wenn Sie keinen angeben der **/Conn** BITS-Parameter wird die LAN-Verbindung verwendet. Geben Sie den Modem Verbindungsnamen an, die unmittelbar nach der **/Conn** Parameter.|

## <a name="remarks"></a>Hinweise

Diese Option zeigt den Wert für die Verwendung des einzelnen Proxys, nicht nur die Verwendung des Proxys für Sie angegeben für das Dienstkonto. Weitere Informationen zum Festlegen der proxynutzung für Dienstkonten finden Sie unter den [Bitsadmin Util und Setieproxy](bitsadmin-util-and-setieproxy.md) wechseln.

## <a name="BKMK_examples"></a>Beispiele für

Das folgende Beispiel zeigt die Proxyverwendung für das Netzwerkdienstkonto.

```
C:\>bitsadmin /Util /GetIEProxy NETWORKSERVICE
```

## <a name="additional-references"></a>Zusätzliche Referenzen

[Befehlszeilensyntax](command-line-syntax-key.md)
