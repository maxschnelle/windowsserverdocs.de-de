---
title: bitsadmin util and setieproxy
description: Referenz Artikel für den Befehl bizadmin util und SETIEPROXY, der die Proxy Einstellungen festlegt, die beim Übertragen von Dateien mithilfe eines Dienst Kontos verwendet werden sollen.
ms.topic: reference
ms.assetid: 0e9f31ba-3070-4ffd-a94c-388c8d78f688
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 7c341a3fffad0951b800c618605c15b47d4d9308
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89630426"
---
# <a name="bitsadmin-util-and-setieproxy"></a>bitsadmin util and setieproxy

Legen Sie die Proxy Einstellungen fest, die beim Übertragen von Dateien mithilfe eines Dienst Kontos verwendet werden. Sie müssen diesen Befehl an einer Eingabeaufforderung mit erhöhten Rechten ausführen, damit der Vorgang erfolgreich abgeschlossen werden kann.

> [!NOTE]
> Dieser Befehl wird von Bits 1,5 und früheren Versionen nicht unterstützt.

## <a name="syntax"></a>Syntax

```
bitsadmin /util /setieproxy <account> <usage> [/conn <connectionname>]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ---------- |
| account | Gibt das Dienst Konto an, dessen Proxy Einstellungen Sie definieren möchten. Mögliche Werte sind:<ul><li>LOCALSYSTEM</li><li>   Network Service</li><li>LOCALSERVICE.</li></ul> |
| Nutzung | Gibt die Art der zu verwendenden Proxy Erkennung an. Mögliche Werte sind:<ul><li>**NO_PROXY.** Verwenden Sie keinen Proxy Server.</li><li>**Auto Ermittlung.** Die Proxy Einstellungen werden automatisch erkannt.</li><li>**MANUAL_PROXY.** Verwenden Sie eine angegebene Proxy Liste und Umgehungs Liste. Sie müssen die Listen direkt nach dem Nutzungstag angeben. Beispiel: `MANUAL_PROXY proxy1,proxy2 NULL`.<ul><li>**Proxy Liste.** Eine durch Trennzeichen getrennte Liste der zu verwendenden Proxy Server.</li><li>**Umgehungs Liste.** Eine durch Leerzeichen getrennte Liste von Hostnamen oder IP-Adressen, für die Übertragungen nicht über einen Proxy weitergeleitet werden sollen. Dies kann dazu führen, dass auf \<local> alle Server im gleichen LAN verwiesen wird. Werte von NULL oder können für eine leere Proxy Umgehungs Liste verwendet werden.</li></ul><li>**AutoScript.** Identisch mit **Autodetect**, mit dem Unterschied, dass auch ein Skript ausgeführt wird. Sie müssen die Skript-URL direkt nach dem Nutzungstag angeben. Beispiel: `AUTOSCRIPT http://server/proxy.js`.</li><li>**Festlegen.** Identisch mit **NO_PROXY**, mit der Ausnahme, dass die manuellen Proxy-URLs (sofern angegeben) und alle URLs, die mithilfe der automatischen Erkennung ermittelt wurden, entfernt werden</li></ul> |
| ConnectionName | (Optional) Wird zusammen mit dem **/conn** -Parameter verwendet, um anzugeben, welche Modemverbindung verwendet werden soll. Wenn Sie den **/conn** -Parameter nicht angeben, verwendet Bits die LAN-Verbindung. |

### <a name="remarks"></a>Hinweise

Jeder aufeinanderfolgende-Rückruf, der diesen Switch verwendet, ersetzt die zuvor angegebene Verwendung, jedoch nicht die Parameter der zuvor definierten Verwendung. Wenn Sie z. b. **NO_PROXY**, **Autodetect**und **MANUAL_PROXY** bei separaten Aufrufen angeben, verwendet Bits die zuletzt bereitgestellte Verwendung, behält jedoch die Parameter von der zuvor definierten Verwendung bei.

## <a name="examples"></a>Beispiele

So legen Sie die Proxy Verwendung für das Konto "LocalSystem" fest:

```
bitsadmin /util /setieproxy localsystem AUTODETECT
```

```
bitsadmin /util /setieproxy localsystem MANUAL_PROXY proxy1,proxy2,proxy3 NULL
```

```
bitsadmin /util /setieproxy localsystem MANUAL_PROXY proxy1:80
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Befehl "BIFS admin util"](bitsadmin-util.md)

- [Bider admin-Befehl](bitsadmin.md)
