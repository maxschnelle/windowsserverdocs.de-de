---
title: BIFS admin util und SETIEPROXY
description: Windows-Befehls Thema für bizadmin util und SETIEPROXY, mit dem die Proxy Einstellungen festgelegt werden, die beim Übertragen von Dateien mithilfe eines Dienst Kontos verwendet werden sollen.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0e9f31ba-3070-4ffd-a94c-388c8d78f688
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4e7d8a9ff4e2388b61ee5ae00ae7afe421de68e6
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80848883"
---
# <a name="bitsadmin-util-and-setieproxy"></a>BIFS admin util und SETIEPROXY

Legen Sie die Proxy Einstellungen fest, die beim Übertragen von Dateien mithilfe eines Dienst Kontos verwendet werden.

**Bikadmin 1,5 und früher**: nicht unterstützt.

## <a name="syntax"></a>Syntax

```
bitsadmin /Util /SetIEProxy <Account> <Usage>[/Conn <ConnectionName>]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Konto|Gibt den Typ des Dienst Kontos an, dessen Proxy Einstellungen Sie definieren möchten. Mögliche Werte:</br>-LocalSystem</br>-NetworkService</br>-LocalService|
|Verwendung|Gibt die Art der zu verwendenden Proxy Erkennung an. Mögliche Werte:</br>-NO_PROXY – keinen Proxy Server verwenden.</br>-Autodetect – die Proxy Einstellungen werden automatisch erkannt.</br>-MANUAL_PROXY – verwenden Sie eine explizite Proxy Liste und Umgehungs Liste. Geben Sie die Proxy Liste und die Umgehungs Liste direkt nach dem Usage-Tag an. Beispielsweise MANUAL_PROXY Proxy1, Proxy2 NULL.</br>    -Die Proxy Liste ist eine durch Trennzeichen getrennte Liste der zu verwendenden Proxy Server.</br>    -Die Umgehungs Liste ist eine durch Leerzeichen getrennte Liste von Hostnamen oder IP-Adressen, für die keine Übertragungen über einen Proxy weitergeleitet werden sollen. Dies kann \<lokalen > sein, um auf alle Server im gleichen LAN zu verweisen. Werte von NULL oder können für eine leere Proxy Umgehungs Liste verwendet werden.</br>-AutoScript – identisch mit der automatischen Erkennung, mit dem Unterschied, dass auch ein Skript ausgeführt wird. Geben Sie die Skript-URL direkt nach dem Usage-Tag an. Beispiel: AutoScript http://server/proxy.js.</br>-Reset – identisch mit NO_PROXY, mit der Ausnahme, dass die manuellen Proxy-URLs (sofern angegeben) und die mit der automatischen Erkennung ermittelten URLs entfernt werden.|
|ConnectionName|Optional – wird mit dem **/conn** -Parameter verwendet, um die zu verwendende Modemverbindung anzugeben. Wenn Sie den **/conn** -Parameter nicht angeben, verwendet Bits die LAN-Verbindung. Geben Sie den Namen der Modemverbindung direkt nach dem **/conn** -Parameter an.|

## <a name="remarks"></a>Hinweise

Jeder aufeinanderfolgende-Rückruf, der diesen Switch verwendet, ersetzt die zuvor angegebene Verwendung, jedoch nicht die Parameter der zuvor definierten Verwendung. Wenn Sie z. b. NO_PROXY, Autodetect und MANUAL_PROXY bei separaten Aufrufen angeben, verwendet Bits die zuletzt angegebene Verwendung, behält jedoch die Parameter der zuvor definierten Verwendung bei.

> [!IMPORTANT]
> Sie müssen diesen Befehl an einer Eingabeaufforderung mit erhöhten Rechten ausführen, damit der Vorgang erfolgreich abgeschlossen werden kann.

## <a name="examples"></a>Beispiele

Im folgenden Beispiel wird die Proxy Verwendung für das Netzwerkdienst Konto festgelegt.

```
C:\>bitsadmin /Util /SetIEProxy localsystem AUTODETECT
```

Weitere Beispiele finden Sie hier.

```
bitsadmin /util /setieproxy localsystem MANUAL_PROXY proxy1,proxy2,proxy3 NULL
bitsadmin /util /setieproxy localsystem MANUAL_PROXY proxy1:80 
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)