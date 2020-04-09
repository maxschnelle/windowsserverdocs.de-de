---
title: nslookup
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 41516932-7833-434a-aa92-b4cf0f9a7ef7
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 15062d81992ee1b6e55d47cb9e49822350e4f2bc
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80838093"
---
# <a name="nslookup"></a>nslookup

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt Informationen an, die Sie verwenden können, um Domain Name System (DNS)-Infrastruktur zu diagnostizieren. Bevor Sie dieses Tool verwenden, sollten Sie mit der Funktionsweise von DNS vertraut sein. Das Befehlszeilen Tool nslookup ist nur verfügbar, wenn Sie das TCP/IP-Protokoll installiert haben.
## <a name="syntax"></a>Syntax

```
nslookup [<-SubCommand ...>] [{<computerTofind> | -<Server>}]
nslookup /exit
nslookup /finger [<UserName>] [{[>] <FileName>|[>>] <FileName>}]
nslookup /{help | ?}
nslookup /ls [<Option>] <DNSDomain> [{[>] <FileName>|[>>] <FileName>}]
nslookup /lserver <DNSDomain> 
nslookup /root 
nslookup /server <DNSDomain>
nslookup /set <KeyWord>[=<Value>]
nslookup /set all 
nslookup /set class=<Class>
nslookup /set [no]d2
nslookup /set [no]debug
nslookup /set [no]defname
nslookup /set domain=<DomainName>
nslookup /set [no]ignore
nslookup /set port=<Port>
nslookup /set querytype=<ResourceRecordtype>
nslookup /set [no]recurse
nslookup /set retry=<Number>
nslookup /set root=<RootServer>
nslookup /set [no]search
nslookup /set srchlist=<DomainName>[/...]
nslookup /set timeout=<Number>
nslookup /set type=<ResourceRecordtype>
nslookup /set [no]vc
nslookup /view <FileName>
```

### <a name="parameters"></a>Parameter

|                       Parameter                       |                                                                                                         Beschreibung                                                                                                         |
|-------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   [Befehl „nslookup exit“](nslookup-exit-command.md)   |                                                                                                     Beendet **nslookup**.                                                                                                     |
| [Befehl „nslookup finger“](nslookup-finger-command.md) |                                                                                  Stellt eine Verbindung mit dem Finger Server auf dem aktuellen Computer her.                                                                                   |
|           [nslookup help](nslookup-help.md)           |                                                                                    Zeigt eine kurze Zusammenfassung der **nslookup** -Unterbefehle an.                                                                                    |
|             [nslookup ls](nslookup-ls.md)             |                                                                                             Listet Informationen für eine DNS-Domäne auf.                                                                                             |
|        [nslookup lserver](nslookup-lserver.md)        |                                                                                   Ändert den Standard Server in die angegebene DNS-Domäne.                                                                                   |
|           [nslookup root](nslookup-root.md)           |                                                                     Ändert den Standard Server für den Stamm des DNS-Domänen Namen-Speicherplatzes auf den Server.                                                                     |
|         [nslookup server](nslookup-server.md)         |                                                                                   Ändert den Standard Server in die angegebene DNS-Domäne.                                                                                   |
|            [nslookup set](nslookup-set.md)            |                                                                              Ändert die Konfigurationseinstellungen, die die Funktionsweise von suchen beeinflussen.                                                                               |
|        [nslookup set all](nslookup-set-all.md)        |                                                                                  Druckt die aktuellen Werte der Konfigurationseinstellungen.                                                                                   |
|      [nslookup set class](nslookup-set-class.md)      |                                                                     Ändert die Query-Klasse. Die-Klasse gibt die Protokoll Gruppe der Informationen an.                                                                     |
|         [nslookup set d2](nslookup-set-d2.md)         |                                                                     Schaltet einen umfassenden Debugmodus ein oder aus. Alle Felder jedes Pakets werden gedruckt.                                                                      |
|      [nslookup set debug](nslookup-set-debug.md)      |                                                                                               Schaltet den Debugmodus ein oder aus.                                                                                               |
|                 Nslookup/set defname                 |                                            Fügt den Standard-DNS-Domänen Namen an eine einzelne Komponenten Such Anforderung an. Bei einer einzelnen Komponente handelt es sich um eine Komponente, die keine Punkte enthält.                                            |
|     [nslookup set domain](nslookup-set-domain.md)     |                                                                                 Ändert den Standard-DNS-Domänen Namen in den angegebenen Namen.                                                                                  |
|                 Nslookup/Set ignorieren                  |                                                                                              Ignoriert Fehler beim Abschneiden von Paketen.                                                                                              |
|       [nslookup set port](nslookup-set-port.md)       |                                                                          Ändert den standardmäßigen TCP/UDP-DNS-Namen Serverport in den angegebenen Wert.                                                                           |
|  [nslookup set querytype](nslookup-set-querytype.md)  |                                                                                       Ändert den Ressourcen Daten Satz für die Abfrage.                                                                                       |
|    [nslookup set recurse](nslookup-set-recurse.md)    |                                                                    Weist den DNS-Namen Server an, andere Server abzufragen, wenn diese nicht über die Informationen verfügen.                                                                    |
|      [nslookup set retry](nslookup-set-retry.md)      |                                                                                                 Legt die Anzahl der Wiederholungen fest.                                                                                                 |
|       [nslookup set root](nslookup-set-root.md)       |                                                                                    Ändert den Namen des Stamm Servers, der für Abfragen verwendet wird.                                                                                    |
|     [nslookup set search](nslookup-set-search.md)     | Fügt die DNS-Domänen Namen in der DNS-Domänen Suchliste an die Anforderung an, bis eine Antwort empfangen wird. Dies gilt, wenn die Set-und die Suche-Anforderung mindestens einen Zeitraum enthalten, aber nicht mit einem nachfolgenden Zeitraum enden. |
|   [nslookup set srchlist](nslookup-set-srchlist.md)   |                                                                                    Ändert den Standard-DNS-Domänen Namen und die Suchliste.                                                                                     |
|    [nslookup set timeout](nslookup-set-timeout.md)    |                                                                           Ändert die anfängliche Anzahl von Sekunden, die auf eine Antwort auf eine Anforderung gewartet werden soll.                                                                           |
|       [nslookup set type](nslookup-set-type.md)       |                                                                                       Ändert den Ressourcen Daten Satz für die Abfrage.                                                                                       |
|         [nslookup set vc](nslookup-set-vc.md)         |                                                                     Gibt an, dass beim Senden von Anforderungen an den Server eine virtuelle Verbindung verwendet oder nicht verwendet werden soll.                                                                      |
|           [nslookup view](nslookup-view.md)           |                                                                          Sortiert die Ausgabe der vorherigen **ls** -Unterbefehle und listet Sie auf.                                                                          |

## <a name="remarks"></a>Hinweise
- Wenn *computertofind* eine IP-Adresse ist und die Abfrage für einen-oder PTR-Ressourcen Daten Satz-Typ ist, wird der Name des Computers zurückgegeben. Wenn *computertofind* ein Name ist und keinen nachfolgenden Zeitraum hat, wird der Standard-DNS-Domänen Name an den Namen angehängt. Dieses Verhalten ist abhängig vom Status der folgenden **Set** -Unterbefehle: " **Domain**", " **srchlist**", " **defname**" und " **Search**".
- Wenn Sie anstelle von *computertofind*einen Bindestrich (-) eingeben, wird die Eingabeaufforderung in den interaktiven **nslookup** -Modus geändert.
- Die Befehlszeilen Länge muss weniger als 256 Zeichen umfassen.
- **nslookup** verfügt über zwei Modi: interaktiv und nicht interaktiv.
  Wenn Sie nur ein einzelnes Datenelement suchen müssen, verwenden Sie den nicht interaktiven Modus. Geben Sie für den ersten Parameter den Namen oder die IP-Adresse des Computers ein, den Sie suchen möchten. Geben Sie für den zweiten Parameter den Namen oder die IP-Adresse eines DNS-Namensservers ein. Wenn Sie das zweite Argument weglassen, verwendet **nslookup** den Standard-DNS-Namen Server.
  Wenn Sie mehr als ein Datenelement suchen müssen, können Sie den interaktiven Modus verwenden. Geben Sie einen Bindestrich (-) für den ersten Parameter und den Namen oder die IP-Adresse eines DNS-Namen Servers für den zweiten Parameter ein. Oder lassen Sie beide Parameter aus, und **nslookup** verwendet den Standard-DNS-Namen Server. Im folgenden finden Sie einige Tipps zum Arbeiten im interaktiven Modus:
  -   Wenn Sie interaktive Befehle jederzeit unterbrechen möchten, drücken Sie STRG + B.
  -   Zum Beenden geben Sie **Exit**ein.
  -   Um einen integrierten Befehl als Computernamen zu behandeln, müssen Sie ihm das Escapezeichen (\\) voranstellen.
  -   Ein nicht erkannter Befehl wird als Computername interpretiert.
- Wenn die Such Anforderung fehlschlägt, gibt **nslookup** eine Fehlermeldung aus. In der folgenden Tabelle sind mögliche Fehlermeldungen aufgeführt.
  |**Fehlermeldung**|**Beschreibung**|
  |-----------|----------|
  |`timed out`|Der Server hat nach einem bestimmten Zeitraum und einer bestimmten Anzahl von Wiederholungen nicht auf eine Anforderung geantwortet. Sie können den Timeout Zeitraum mit dem Unterbefehl **Set Timeout** festlegen. Sie können die Anzahl der Wiederholungs Versuche mit dem untergeordneten Befehl **Set Wiederholen Sie** festlegen.|
  |`No response from server`|Auf dem Server Computer wird kein DNS-Namen Server ausgeführt.|
  |`No records`|Der DNS-Namen Server weist keine Ressourcen Einträge des aktuellen Abfrage Typs für den Computer auf, obwohl der Computername gültig ist. Der Abfragetyp wird mit dem **Set QueryType** -Befehl angegeben.|
  |`Nonexistent domain`|Der Computer-oder DNS-Domänen Name ist nicht vorhanden.|
  |`Connection refused`<p>\- oder -<p>`Network is unreachable`|Die Verbindung mit dem DNS-Namen Server oder dem Finger Server konnte nicht hergestellt werden. Dieser Fehler tritt häufig bei **ls** -und **Finger** Anforderungen auf.|
  |`Server failure`|Der DNS-Namen Server hat eine interne Inkonsistenzen in der Datenbank festgestellt und konnte keine gültige Antwort zurückgeben.|
  |`Refused`|Der DNS-Namen Server hat die Anforderung der Anforderung verweigert.|
  |`format error`|Der DNS-Namen Server hat festgestellt, dass das Anforderungspaket nicht im richtigen Format vorliegt. Dies kann auf einen Fehler in **nslookup**hindeuten.|
- Weitere Informationen zum Befehl **nslookup** und DNS finden Sie in den folgenden Ressourcen:
  - Lee, T., Davies, J. 2000. *Technische Referenz für Microsoft Windows 2000 TCP/IP-Protokolle und-Dienste*. Redmond, Washington: Microsoft Press.
  - Albitz, P., Loukides, M. und C. Liu. 2001. *DNS und BIND, vierte Ausgabe*. "Tsbastopol", Kalifornien: "...", Inc.
  - Larson, M. und C. Liu. 2001. *DNS unter Windows 2000*. "Tsbastopol", Kalifornien: "...", Inc.
    #### <a name="examples"></a>Beispiele
    Jede Befehlszeilenoption besteht aus einem Bindestrich (-), gefolgt vom Befehlsnamen und in einigen Fällen mit einem Gleichheitszeichen (=) und einem Wert. Wenn Sie z. b. den Standard Abfragetyp in Host (Computer) und den ursprünglichen Timeout Wert in 10 Sekunden ändern möchten, geben Sie Folgendes ein: **nslookup-querytype = hinfo-Timeout = 10**
    ## <a name="see-also"></a>Weitere Informationen
    - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
