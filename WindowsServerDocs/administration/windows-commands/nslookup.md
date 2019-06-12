---
title: nslookup
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 41516932-7833-434a-aa92-b4cf0f9a7ef7
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 194cb96846e42b175978a2f6fc7268a93875d315
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/07/2019
ms.locfileid: "66811096"
---
# <a name="nslookup"></a>nslookup

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Zeigt Informationen, die Sie zum Diagnostizieren der Domain Name System (DNS)-Infrastruktur verwenden können. Bevor Sie mit diesem Tool sollten Sie vertraut sein, mit der Funktionsweise von DNS. Das Befehlszeilentool "Nslookup" ist nur verfügbar, wenn Sie das TCP/IP-Protokoll installiert haben.
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

## <a name="parameters"></a>Parameter

|                       Parameter                       |                                                                                                         Beschreibung                                                                                                         |
|-------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   [Befehl „nslookup exit“](nslookup-exit-command.md)   |                                                                                                     beendet **Nslookup**.                                                                                                     |
| [Befehl „nslookup finger“](nslookup-finger-command.md) |                                                                                  Eine Verbindung mit dem Fingerserver, auf dem aktuellen Computer.                                                                                   |
|           [nslookup help](nslookup-help.md)           |                                                                                    Zeigt eine kurze Zusammenfassung der **Nslookup** Unterbefehle.                                                                                    |
|             [nslookup ls](nslookup-ls.md)             |                                                                                             Listet Informationen für eine DNS-Domäne.                                                                                             |
|        [nslookup lserver](nslookup-lserver.md)        |                                                                                   Ändert den Standardserver an der angegebenen DNS-Domäne an.                                                                                   |
|           [nslookup root](nslookup-root.md)           |                                                                     Ändert den Standardserver an den Server für den Stamm des DNS-Domänennamespace.                                                                     |
|         [nslookup server](nslookup-server.md)         |                                                                                   Ändert den Standardserver an der angegebenen DNS-Domäne an.                                                                                   |
|            [nslookup set](nslookup-set.md)            |                                                                              ändert Konfigurationseinstellungen, die beeinflussen wie Suchvorgänge-Funktion.                                                                               |
|        [nslookup set all](nslookup-set-all.md)        |                                                                                  Gibt die aktuellen Werte der Konfigurationseinstellungen.                                                                                   |
|      [nslookup set class](nslookup-set-class.md)      |                                                                     Ändert die Abfrageklasse. Die Klasse gibt die Protokollgruppe, der die Informationen an.                                                                     |
|         [nslookup set d2](nslookup-set-d2.md)         |                                                                     Vollständige Debugging-Modus aktiviert, aktivieren oder deaktivieren. Alle Felder jedes Pakets werden gedruckt.                                                                      |
|      [nslookup set debug](nslookup-set-debug.md)      |                                                                                               Schaltet den Debugmodus, ein- oder ausschalten.                                                                                               |
|                 Nslookup/set Defname                 |                                            Fügt den standardmäßigen DNS-Domänennamen an eine suchanforderung einzelne Komponente an. Eine einzelne Komponente ist eine Komponente, die keine Punkte enthält.                                            |
|     [nslookup set domain](nslookup-set-domain.md)     |                                                                                 Ändert den Standard-DNS-Domänennamen dem angegebenen Namen.                                                                                  |
|                 Nslookup/Set ignorieren                  |                                                                                              Fehler beim Abschneiden von Paket wird ignoriert.                                                                                              |
|       [nslookup set port](nslookup-set-port.md)       |                                                                          ändert sich der Standardport des TCP/UDP-DNS-Namen auf den angegebenen Wert.                                                                           |
|  [nslookup set querytype](nslookup-set-querytype.md)  |                                                                                       Ändert den Typ des Ressourcendatensatzes für die Abfrage an.                                                                                       |
|    [nslookup set recurse](nslookup-set-recurse.md)    |                                                                    Weist den DNS-Name-Server auf anderen Servern abzufragen, wenn sie nicht die Informationen verfügt.                                                                    |
|      [nslookup set retry](nslookup-set-retry.md)      |                                                                                                 Legt die Anzahl von Wiederholungen fest.                                                                                                 |
|       [nslookup set root](nslookup-set-root.md)       |                                                                                    Ändert den Namen des Stammservers für Abfragen verwendet.                                                                                    |
|     [nslookup set search](nslookup-set-search.md)     | Fügt die DNS-Domänennamen in der Suchliste für DNS-Domäne auf die Anforderung, bis eine Antwort empfangen wird. Dies gilt, wenn die Gruppe und die Suche nach Anforderung muss mindestens einen Punkt enthalten, aber nicht mit einem Punkt enden. |
|   [nslookup set srchlist](nslookup-set-srchlist.md)   |                                                                                    Ändert den Standard-DNS-Domäne Name "und" suchen.                                                                                     |
|    [nslookup set timeout](nslookup-set-timeout.md)    |                                                                           Ändert die anfängliche Anzahl von Sekunden zu warten, bis eine Antwort auf eine Anforderung an.                                                                           |
|       [nslookup set type](nslookup-set-type.md)       |                                                                                       Ändert den Typ des Ressourcendatensatzes für die Abfrage an.                                                                                       |
|         [nslookup set vc](nslookup-set-vc.md)         |                                                                     Gibt an, zu verwenden oder nicht verwenden, die eine virtuelle Verbindung, die beim Senden an den Server-Anforderungen.                                                                      |
|           [nslookup view](nslookup-view.md)           |                                                                          sortiert und zeigt die Ausgabe des vorherigen **ls** Unterbefehl oder Befehle.                                                                          |

## <a name="remarks"></a>Hinweise
- Wenn *Gesuchter* eine IP-Adresse und die Abfrage für ein A oder PTR Ressourceneintragstyp, den Namen des Computers zurückgegeben. Wenn *Gesuchter* ist ein Name und verfügt nicht über einen Punkt, der Standardwert, der DNS-Domänennamen an den Namen angefügt wird. Dieses Verhalten hängt von den Status der folgenden **festgelegt** Unterbefehle: **Domäne**, **Srchlist**, **Defname**, und  **Suche**.
- Wenn Sie anstelle von einem Bindestrich (-) eingeben *Gesuchter*, die Eingabeaufforderung ändert sich in **Nslookup** im interaktiven Modus.
- Die Länge der Befehlszeile muss weniger als 256 Zeichen sein.
- **Nslookup** verfügt über zwei Modi: interaktiven und einen.
  Wenn Sie nur ein einzelnes Datenelement suchen möchten, verwenden Sie nicht interaktiven Modus. Geben Sie den Namen oder die IP-Adresse des Computers, der Sie suchen möchten, für den ersten Parameter. Geben Sie für den zweiten Parameter den Namen oder die IP-Adresse eines DNS-Name-Servers ein. Wenn Sie das zweite Argument, weglassen **Nslookup** verwendet den Standard-DNS-Namenserver.
  Wenn Sie mehr als eine Dateneinheit suchen möchten, können Sie im interaktiven Modus. Geben Sie einen Bindestrich (-) für den ersten Parameter und den Namen oder die IP-Adresse eines DNS-Name-Servers für den zweiten Parameter ein. Oder lassen Sie beide Parameter und **Nslookup** verwendet den Standard-DNS-Namenserver. Es folgen einige Tipps zum Arbeiten im interaktiven Modus:
  -   Drücken Sie STRG + B, um interaktive Befehle jederzeit zu unterbrechen.
  -   Geben Sie zum Beenden **beenden**.
  -   Um einen integrierten Befehl als Computername verwenden, fügen sie davor das Escape-Zeichen (\\).
  -   Ein nicht erkannter Befehl wird als Computername interpretiert.
- Wenn die Anforderung für die Suche fehlschlägt, **Nslookup** druckt eine Fehlermeldung angezeigt. Die folgende Tabelle enthält mögliche Fehlermeldungen.
  |**Fehlermeldung**|**Beschreibung**|
  |-----------|----------|
  |`timed out`|Der Server hat nicht auf eine Anforderung nach einem bestimmten Zeitraum und eine bestimmte Anzahl von Wiederholungen reagiert. Sie können festlegen, das Timeout mit der **Timeout festlegen** Unterbefehl. Sie können festlegen, die Anzahl von Wiederholungen mit der **Satz Wiederholung** Unterbefehl.|
  |`No response from server`|Keine DNS-Namenserver wird auf dem Server-Computer ausgeführt.|
  |`No records`|Der DNS-Namenserver-Ressourceneinträge des aktuellen Abfragetyps für den Computer keinen auch den Namen des Computers gültig ist. Der Abfragetyp wird angegeben, mit der **festgelegt Querytype** Befehl.|
  |`Nonexistent domain`|Der Computer oder die DNS-Domänenname ist nicht vorhanden.|
  |`Connection refused`<br /><br />– oder –<br /><br />`Network is unreachable`|Die Verbindung mit dem DNS-Namenserver oder den Finger-Server konnte nicht hergestellt werden. Dieser Fehler tritt häufig bei **ls** und **Finger** Anforderungen.|
  |`Server failure`|Der DNS-Namenserver eine interne Inkonsistenz in der Datenbank gefunden und konnte keine gültige Antwort zurückgegeben.|
  |`Refused`|Der DNS-Namenserver für die Anforderung abgelehnt.|
  |`format error`|Der DNS-Namenserver gefunden, dass das Anforderungspaket nicht das richtige Format war. Dies ist möglicherweise einen Fehler in **Nslookup**.|
- Weitere Informationen zu den **Nslookup** Befehl und DNS finden Sie in den folgenden Ressourcen:
  - Lee, t, Davies, J. 2000. *Technische Referenz für Microsoft Windows 2000-TCP/IP-Protokolle und Dienste*. Redmond, Washington: Microsoft Press.
  - Albitz, P., Loukides, M. and C. Liu. 2001. *DNS und die BINDUNG, 4. Auflage*. Köln, Kalifornien, USA: O' Reilly und Partnern, Inc.
  - Larson, M. and C. Liu. 2001. *DNS in Windows 2000*. Köln, Kalifornien, USA: O' Reilly und Partnern, Inc.
    #### <a name="examples"></a>Beispiele
    Jede Befehlszeilenoption besteht aus einem Bindestrich (-), unmittelbar gefolgt von den Namen des Befehls in einigen Fällen, einem Gleichheitszeichen (=), und klicken Sie dann auf einen Wert. Um Informationen zum Host (Computer) und das ursprüngliche Timeout auf 10 Sekunden den Standardtyp für die Abfrage zu ändern, geben Sie zum Beispiel: **Nslookup - Querytype = Hinfo - Timeout = 10**
    ## <a name="see-also"></a>Siehe auch
    [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
