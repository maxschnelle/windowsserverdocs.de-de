---
title: nslookup
description: Referenz Artikel für den Befehl "nslookup", in dem Informationen angezeigt werden, die Sie verwenden können, um die DNS-Infrastruktur (Domain Name System) zu diagnostizieren.
ms.topic: article
ms.assetid: 41516932-7833-434a-aa92-b4cf0f9a7ef7
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7d01f167a198803db269e97e806a6d2867074d60
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87885322"
---
# <a name="nslookup"></a>nslookup

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt Informationen an, die Sie verwenden können, um Domain Name System (DNS)-Infrastruktur zu diagnostizieren. Bevor Sie dieses Tool verwenden, sollten Sie mit der Funktionsweise von DNS vertraut sein. Das Befehlszeilen Tool nslookup ist nur verfügbar, wenn Sie das TCP/IP-Protokoll installiert haben.

Das Befehlszeilen Tool nslookup weist zwei Modi auf: interaktiv und nicht interaktiv.

Wenn Sie nur ein einzelnes Datenelement suchen müssen, empfiehlt es sich, den nicht interaktiven Modus zu verwenden. Geben Sie für den ersten Parameter den Namen oder die IP-Adresse des Computers ein, den Sie suchen möchten. Geben Sie für den zweiten Parameter den Namen oder die IP-Adresse eines DNS-Namensservers ein. Wenn Sie das zweite Argument weglassen, verwendet **nslookup** den Standard-DNS-Namen Server.

Wenn Sie mehr als ein Datenelement suchen müssen, können Sie den interaktiven Modus verwenden. Geben Sie einen Bindestrich (-) für den ersten Parameter und den Namen oder die IP-Adresse eines DNS-Namen Servers für den zweiten Parameter ein. Wenn Sie beide Parameter weglassen, verwendet das Tool den Standard-DNS-Namen Server. Wenn Sie den interaktiven Modus verwenden, können Sie Folgendes tun:

- Unterbrechen Sie interaktive Befehle jederzeit, indem Sie STRG + B drücken.

- Beenden Sie, indem Sie **Exit**eingeben.

- Behandeln Sie einen integrierten Befehl als Computernamen, indem Sie ihm das Escapezeichen () voranstellt \) . Ein nicht erkannter Befehl wird als Computername interpretiert.

## <a name="syntax"></a>Syntax

```
nslookup [exit | finger | help | ls | lserver | root | server | set | view] [options]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| [Nslookup beenden](nslookup-exit-command.md) | Beendet das Befehlszeilen Tool Nslookup. |
| [Nslookup-Finger](nslookup-finger-command.md) | Stellt eine Verbindung mit dem Finger Server auf dem aktuellen Computer her. |
| [nslookup help](nslookup-help.md) | Zeigt eine kurze Zusammenfassung der Unterbefehle an. |
| [nslookup ls](nslookup-ls.md) | Listet Informationen für eine DNS-Domäne auf. |
| [nslookup lserver](nslookup-lserver.md) | Ändert den Standard Server in die angegebene DNS-Domäne. |
| [nslookup root](nslookup-root.md) | Ändert den Standard Server für den Stamm des DNS-Domänen Namen-Speicherplatzes auf den Server. |
| [nslookup server](nslookup-server.md) | Ändert den Standard Server in die angegebene DNS-Domäne. |
| [nslookup set](nslookup-set.md) | Ändert die Konfigurationseinstellungen, die die Funktionsweise von suchen beeinflussen. |
| [nslookup set all](nslookup-set-all.md) | Druckt die aktuellen Werte der Konfigurationseinstellungen. |
| [nslookup set class](nslookup-set-class.md) | Ändert die Query-Klasse. Die-Klasse gibt die Protokoll Gruppe der Informationen an. |
| [nslookup set d2](nslookup-set-d2.md) | Schaltet einen umfassenden Debugmodus ein oder aus. Alle Felder jedes Pakets werden gedruckt. |
| [nslookup set debug](nslookup-set-debug.md) | Schaltet den Debugmodus ein oder aus. |
| [nslookup set domain](nslookup-set-domain.md) | Ändert den Standard-DNS-Domänen Namen in den angegebenen Namen. |
| [nslookup set port](nslookup-set-port.md) | Ändert den standardmäßigen TCP/UDP-DNS-Namen Serverport in den angegebenen Wert. |
| [nslookup set querytype](nslookup-set-querytype.md) | Ändert den Ressourcen Daten Satz für die Abfrage. |
| [nslookup set recurse](nslookup-set-recurse.md) | Weist den DNS-Namen Server an, andere Server abzufragen, wenn diese nicht über die Informationen verfügen. |
| [nslookup set retry](nslookup-set-retry.md) | Legt die Anzahl der Wiederholungen fest. |
| [nslookup set root](nslookup-set-root.md) | Ändert den Namen des Stamm Servers, der für Abfragen verwendet wird. |
| [nslookup set search](nslookup-set-search.md) | Fügt die DNS-Domänen Namen in der DNS-Domänen Suchliste an die Anforderung an, bis eine Antwort empfangen wird. Dies gilt, wenn die Set-und die Suche-Anforderung mindestens einen Zeitraum enthalten, aber nicht mit einem nachfolgenden Zeitraum enden. |
| [nslookup set srchlist](nslookup-set-srchlist.md) | Ändert den Standard-DNS-Domänen Namen und die Suchliste. |
| [nslookup set timeout](nslookup-set-timeout.md) | Ändert die anfängliche Anzahl von Sekunden, die auf eine Antwort auf eine Anforderung gewartet werden soll. |
| [nslookup set type](nslookup-set-type.md) | Ändert den Ressourcen Daten Satz für die Abfrage. |
| [nslookup set vc](nslookup-set-vc.md) | Gibt an, dass beim Senden von Anforderungen an den Server eine virtuelle Verbindung verwendet oder nicht verwendet werden soll. |
| [nslookup view](nslookup-view.md) | Sortiert die Ausgabe der vorherigen **ls** -Unterbefehle und listet Sie auf. |

### <a name="remarks"></a>Bemerkungen

- Wenn *computertofind* eine IP-Adresse ist und die Abfrage **für einen-** oder **ptr** -Ressourcen Daten Satz-Typ ist, wird der Name des Computers zurückgegeben.

- Wenn *computertofind* ein Name ist und keinen nachfolgenden Zeitraum hat, wird der Standardname der DNS-Domäne an den Namen angehängt. Dieses Verhalten ist abhängig vom Status der folgenden **Set** -Unterbefehle: " **Domain**", " **srchlist**", " **defname**" und " **Search**".

- Wenn Sie anstelle von *computertofind*einen Bindestrich (-) eingeben, wird die Eingabeaufforderung in den interaktiven **nslookup** -Modus geändert.

- Wenn die Such Anforderung fehlschlägt, stellt das Befehlszeilen Tool eine Fehlermeldung bereit, einschließlich der folgenden:

  | Fehlermeldung | BESCHREIBUNG |
  | ------------- | ----------- |
  | Timeout |Der Server hat nach einem bestimmten Zeitraum und einer bestimmten Anzahl von Wiederholungen nicht auf eine Anforderung geantwortet. Sie können den Timeout Zeitraum mit dem Befehl [nslookup Set Timeout](nslookup-set-timeout.md) festlegen. Sie können die Anzahl der Wiederholungs Versuche mit dem Befehl [nslookup Set Wiederholen Sie](nslookup-set-retry.md) festlegen. |
  | Keine Antwort vom Server | Auf dem Server Computer wird kein DNS-Namen Server ausgeführt. |
  | Keine Datensätze | Der DNS-Namen Server weist keine Ressourcen Einträge des aktuellen Abfrage Typs für den Computer auf, obwohl der Computername gültig ist. Der Abfragetyp wird mit dem Befehl [nslookup Set QueryType](nslookup-set-querytype.md) angegeben. |
  | Nicht vorhandene Domäne | Der Computer-oder DNS-Domänen Name ist nicht vorhanden. |
  | Die Verbindung wurde verweigert, oder das Netzwerk ist nicht erreichbar. | Die Verbindung mit dem DNS-Namen Server oder dem Finger Server konnte nicht hergestellt werden. Dieser Fehler tritt häufig bei den **ls** -und **Finger** Anforderungen auf. |
  | Server Fehler | Der DNS-Namen Server hat eine interne Inkonsistenzen in der Datenbank festgestellt und konnte keine gültige Antwort zurückgeben. |
  | Verweigerte | Der DNS-Namen Server hat die Anforderung der Anforderung verweigert. |
  | Formatierungs Fehler | Der DNS-Namen Server hat festgestellt, dass das Anforderungspaket nicht im richtigen Format vorliegt. Dies kann auf einen Fehler in **nslookup**hindeuten. |

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
