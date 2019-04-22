---
title: bitsadmin setproxysettings
description: Windows-Befehle Thema **Bitsadmin Setproxysettings** -die Proxyeinstellungen für den angegebenen Auftrag festgelegt.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: be8edb1b-614e-4d0b-a8f8-64b4bde3e64b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a3503aab55f5650cb9283ce8a9f1a17359bfd48b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59825591"
---
# <a name="bitsadmin-setproxysettings"></a>bitsadmin setproxysettings



Legt fest, die Proxyeinstellungen für den angegebenen Auftrag.

## <a name="syntax"></a>Syntax

```
bitsadmin /SetProxySettings <Job> <Usage> [List] [Bypass]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Anzeigenamen oder die GUID des Auftrags|
|Verwendung|Einer der folgenden Werte:</br>-PRECONFIG – des Besitzers der Standardeinstellungen von Internet Explorer verwenden.</br>-"No_proxy" – verwenden Sie einen Proxyserver nicht.</br>– AUßERKRAFTSETZEN – verwenden Sie eine explizite Proxyliste und bypass-Liste. Einen Proxy und Proxyumgehungsliste müssen folgen.</br>-AUTOERMITTLUNG: Proxyeinstellungen automatisch erkennen.|
|List|Wird verwendet, wenn die *Nutzung* Parameter zum ÜBERSCHREIBEN festgelegt ist – eine durch Trennzeichen getrennte Liste der zu verwendenden Proxyserver enthält.|
|Bypass|Wird verwendet, wenn die *Nutzung* Parameter zum ÜBERSCHREIBEN festgelegt ist – enthält eine durch Leerzeichen getrennte Liste von Hostnamen oder IP-Adressen oder beides, für die Übertragungen sind nicht über einen Proxy geleitet werden. Dies liegt möglicherweise  **\<lokalen >** auf allen Servern im selben LAN verweisen. NULL-Werte oder "" für eine leere Proxyumgehungsliste verwendet werden können.|

## <a name="BKMK_examples"></a>Beispiele für

Im folgenden Beispiel wird die Proxyeinstellungen für den Auftrag mit dem Namen *MyDownloadJob*.

```
C:\>bitsadmin /SetProxySettings myDownloadJob PRECONFIG
```

Hier sind einige weitere Beispiele.

```
bitsadmin /setproxysettings myDownloadJob NO_PROXY
bitsadmin /setproxysettings myDownloadJob OVERRIDE proxy1:80 ""
bitsadmin /setproxysettings myDownloadJob OVERRIDE proxy1,proxy2,proxy3 NULL
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)