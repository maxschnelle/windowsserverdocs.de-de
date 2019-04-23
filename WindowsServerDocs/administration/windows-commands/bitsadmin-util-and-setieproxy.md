---
title: Bitsadmin Util und setieproxy
description: Windows-Befehle Thema **Bitsadmin Util und Setieproxy** -Proxyeinstellungen verwenden, beim Übertragen von Dateien, die über ein Dienstkonto festgelegt.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0e9f31ba-3070-4ffd-a94c-388c8d78f688
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d4f6ab2e52284895d2e7918364c24bbb69f2b1c9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59853511"
---
# <a name="bitsadmin-util-and-setieproxy"></a>Bitsadmin Util und setieproxy

Legen Sie Proxy-Einstellungen verwenden, beim Übertragen von Dateien, die über ein Dienstkonto an.

**BITSAdmin 1.5 und früher**: Nicht unterstützt.

## <a name="syntax"></a>Syntax

```
bitsadmin /Util /SetIEProxy <Account> <Usage>[/Conn <ConnectionName>]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Konto|Gibt den Typ des Dienstkontos, dessen Proxyeinstellungen, die Sie definieren möchten. Dabei sind folgende Werte möglich:</br>-"LOCALSYSTEM"</br>-NETWORKSERVICE</br>-"LOCALSERVICE"|
|Verwendung|Gibt an, die Form der Proxyerkennung zu verwenden. Dabei sind folgende Werte möglich:</br>-"No_proxy" – verwenden Sie einen Proxyserver nicht.</br>-AUTOERMITTLUNG: der Proxyeinstellungen automatisch erkennen.</br>-MANUAL_PROXY – verwenden Sie eine explizite Proxyliste und bypass-Liste. Geben Sie die Proxyliste und bypass-Liste, die unmittelbar nach dem Tag Nutzung. Z. B. MANUAL_PROXY proxy1, proxy2 NULL.</br>    – Die Proxyliste ist eine durch Trennzeichen getrennte Liste der zu verwendenden Proxyserver.</br>    -Die Bypass-Liste ist ein Leerzeichen getrennte Liste von Hostnamen oder IP-Adressen oder beides, für die Übertragungen sind nicht über einen Proxy geleitet werden. Dies liegt möglicherweise \<lokalen > auf allen Servern im selben LAN verweisen. NULL-Werte oder "" für eine leere Proxyumgehungsliste verwendet werden können.</br>-AUTOSCRIPT – Identisch mit AUTOERMITTLUNG, außer es auch ein Skript ausgeführt wird. Geben Sie unmittelbar nach dem Tag für die Verwendung die Skript-URL ein. Z. B. AUTOSCRIPT http://server/proxy.js.</br>-KENNWORTZURÜCKSETZUNG – Identisch mit "no_proxy", es sei denn entfernt die manuelle Proxy-URLs, (falls angegeben), und URLs ermittelt mithilfe der automatischen Erkennung.|
|ConnectionName|Optional – verwendet mit der **/Conn** Parameter, um die zu verwendende modemverbindung anzugeben. Wenn Sie keinen angeben der **/Conn** BITS-Parameter wird die LAN-Verbindung verwendet. Geben Sie den Modem Verbindungsnamen an, die unmittelbar nach der **/Conn** Parameter.|

## <a name="remarks"></a>Hinweise

Jeder nachfolgende Aufruf, der diesen Schalter verwenden, ersetzt die zuvor angegebene Verwendung, aber nicht die Parameter, die zuvor definierte bei Verwendung. Beispielsweise bei Angabe von "no_proxy" Automatische Erkennung und MANUAL_PROXY auf separaten aufrufen BITS verwendet die letzte angegebene Verwendung jedoch speichert die Parameter aus der zuvor definierten Syntax.

> [!IMPORTANT]
> Sie müssen diesen Befehl ausführen, eine Eingabeaufforderung mit erhöhten Rechten, damit er erfolgreich abgeschlossen.

## <a name="BKMK_examples"></a>Beispiele für

Im folgenden Beispiel wird die Proxyverwendung für das Netzwerkdienstkonto.

```
C:\>bitsadmin /Util /SetIEProxy localsystem AUTODETECT
```

Hier sind weitere Beispiele.

```
bitsadmin /util /setieproxy localsystem MANUAL_PROXY proxy1,proxy2,proxy3 NULL
bitsadmin /util /setieproxy localsystem MANUAL_PROXY proxy1:80 ""
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)