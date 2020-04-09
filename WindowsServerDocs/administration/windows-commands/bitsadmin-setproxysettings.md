---
title: bitsadmin setproxysettings
description: Windows-Befehls Thema für bitadmin setproxysettings, mit dem die Proxy Einstellungen für den angegebenen Auftrag festgelegt werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: be8edb1b-614e-4d0b-a8f8-64b4bde3e64b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4dea72d956d12070b2638f953a7a00dcb1ed7a9c
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80849203"
---
# <a name="bitsadmin-setproxysettings"></a>bitsadmin setproxysettings

Legt die Proxy Einstellungen für den angegebenen Auftrag fest.

## <a name="syntax"></a>Syntax

```
bitsadmin /SetProxySettings <Job> <Usage> [List] [Bypass]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Der Anzeige Name oder GUID des Auftrags.|
|Verwendung|Einer der folgenden Werte:</br>-Preconfig – verwendet die Internet Explorer-Standardeinstellungen des Besitzers.</br>-NO_PROXY – keinen Proxy Server verwenden.</br>-OVERRIDE – verwenden Sie eine explizite Proxy Liste und Umgehungs Liste. Eine Proxy-und Proxy Umgehungs Liste muss befolgt werden.</br>-Autodetect – automatische Erkennung von Proxy Einstellungen.|
|Liste|Wird verwendet, wenn der *Usage* -Parameter auf Override festgelegt ist – enthält eine durch Trennzeichen getrennte Liste der zu verwendenden Proxy Server.|
|Umgangen|Wird verwendet, wenn der *Usage* -Parameter auf Override festgelegt ist – enthält eine durch Leerzeichen getrennte Liste von Hostnamen oder IP-Adressen oder beides, bei der Übertragungen nicht über einen Proxy weitergeleitet werden. Dies kann **\<lokalen >** sein, um auf alle Server im gleichen LAN zu verweisen. Werte von NULL oder können für eine leere Proxy Umgehungs Liste verwendet werden.|

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Im folgenden Beispiel werden die Proxy Einstellungen für den Auftrag mit dem Namen *mydownloadjob*festgelegt.

```
C:\>bitsadmin /SetProxySettings myDownloadJob PRECONFIG
```

Im folgenden sind einige weitere Beispiele aufgeführt.

```
bitsadmin /setproxysettings myDownloadJob NO_PROXY
bitsadmin /setproxysettings myDownloadJob OVERRIDE proxy1:80 
bitsadmin /setproxysettings myDownloadJob OVERRIDE proxy1,proxy2,proxy3 NULL
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)