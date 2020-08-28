---
title: dnscmd
description: Referenz Artikel für den Befehl dnscmd, bei dem es sich um eine Befehlszeilenschnittstelle zum Verwalten von DNS-Servern handelt.
ms.topic: reference
ms.assetid: e7f31cb5-a426-4e25-b714-88712b8defd5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0e79d2cc2d5d014db197ab4bbeb0b24ff70fd145
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89030808"
---
# <a name="dnscmd"></a>Dnscmd

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Eine Befehlszeilenschnittstelle zum Verwalten von DNS-Servern. Dieses Hilfsprogramm ist hilfreich bei der Skripterstellung für Batch Dateien, um die Automatisierung von routinemäßigen DNS-Verwaltungsaufgaben oder das einfache unbeaufsichtigte einrichten und Konfigurieren neuer DNS-Server in Ihrem Netzwerk zu unterstützen.

## <a name="syntax"></a>Syntax

```
dnscmd <servername> <command> [<command parameters>]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| `<servername>` | Die IP-Adresse oder der Hostname eines Remote-oder lokalen DNS-Servers. |

## <a name="dnscmd-ageallrecords-command"></a>dnscmd/AgeAllRecords-Befehl

Legt die aktuelle Uhrzeit für einen Zeitstempel für Ressourcen Datensätze in einer angegebenen Zone bzw. einem angegebenen Knoten auf einem DNS-Server fest.

### <a name="syntax"></a>Syntax

```
dnscmd [<servername>] /ageallrecords <zonename>[<nodename>] | [/tree]|[/f]
```

#### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| ---------- | ----------- |
| `<servername>` | Gibt den DNS-Server an, der vom Administrator verwaltet werden soll, dargestellt durch IP-Adresse, voll qualifizierten Domänen Namen (FQDN) oder Hostname. Wenn dieser Parameter weggelassen wird, wird der lokale Server verwendet. |
| `<zonename>` | Gibt den voll qualifizierten Namen der Zone an. |
| `<nodename>` | Gibt einen bestimmten Knoten oder eine Unterstruktur in der Zone an und verwendet dabei Folgendes:<ul><li>**@** for Root Zone or FQDN</li><li>Der voll qualifizierte Name eines Knotens (der Name mit einem Punkt (.) am Ende)</li><li>Eine einzelne Bezeichnung für den Namen relativ zum Zonenstamm.</li></ul> |
| /tree | Gibt an, dass alle untergeordneten Knoten ebenfalls den Zeitstempel erhalten. |
| /f | Führt den Befehl aus, ohne zur Bestätigung aufzufordern. |

##### <a name="remarks"></a>Bemerkungen

- Der **AgeAllRecords** -Befehl dient der Abwärtskompatibilität zwischen der aktuellen Version des DNS und früheren DNS-Versionen, bei denen das Aging und das Bereinigung nicht unterstützt wurden. Er fügt einen Zeitstempel mit der aktuellen Uhrzeit zu Ressourcen Einträgen mit einem Zeitstempel hinzu und legt die aktuelle Zeit für Ressourcen Datensätze mit einem Zeitstempel fest.

- Das Aufzeichnen von Datensätzen tritt nicht auf, es sei denn, die Datensätze sind Zeitstempel. Ressourcen Einträge für Namen Server (NS), Ressourcen Einträge für Start of Authority (SOA) und WINS-Ressourcen Einträge (Windows Internet Name Service) werden nicht in den Prozess für die Prozesserstellung einbezogen, und Sie sind nicht Zeitstempel, auch wenn der **AgeAllRecords** -Befehl ausgeführt wird.

- Dieser Befehl schlägt fehl, es sei denn, für den DNS-Server und die Zone ist das Bereinigung aktiviert. Informationen dazu, wie Sie das Bereinigung für die Zone aktivieren, finden Sie unter dem **Aging** -Parameter in der Syntax des `dnscmd /config` Befehls in diesem Artikel.

- Durch das Hinzufügen eines Zeitstempels zu DNS-Ressourcen Einträgen werden diese mit DNS-Servern, die unter anderen Betriebssystemen als Windows Server ausgeführt werden, nicht kompatibel. Ein mit dem Befehl " **AgeAllRecords** " hinzugefügter Zeitstempel kann nicht rückgängig gemacht werden.

- Wenn keiner der optionalen Parameter angegeben wird, gibt der Befehl alle Ressourcen Datensätze auf dem angegebenen Knoten zurück. Wenn ein Wert für mindestens einen optionalen Parameter angegeben wird, listet **dnscmd** nur die Ressourcen Datensätze auf, die den Werten entsprechen, die in den optionalen Parametern oder Parametern angegeben sind.

### <a name="examples"></a>Beispiele

[Beispiel 1: Festlegen der aktuellen Uhrzeit eines Zeitstempels auf Ressourcen Einträge](/previous-versions/windows/it-pro/windows-server-2003/cc784399(v=ws.10)#example-1-set-the-current-time-on-a-time-stamp-to-resource-records)

## <a name="dnscmd-clearcache-command"></a>dnscmd/ClearCache-Befehl

Löscht den DNS-Cache Speicher der Ressourcen Einträge auf dem angegebenen DNS-Server.

### <a name="syntax"></a>Syntax

```
dnscmd [<servername>] /clearcache
```

#### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| ---------- | ----------- |
| `<servername>` | Gibt den zu verwaltenden DNS-Server an, der durch die IP-Adresse, den FQDN oder den Hostnamen repräsentiert wird. Wenn dieser Parameter weggelassen wird, wird der lokale Server verwendet. |

### <a name="example"></a>Beispiel

```
dnscmd dnssvr1.contoso.com /clearcache
```

## <a name="dnscmd-config-command"></a>dnscmd/config-Befehl

Ändert die Werte in der Registrierung für den DNS-Server und die einzelnen Zonen. Dieser Befehl ändert auch die Konfiguration des angegebenen Servers. Akzeptiert Einstellungen auf Serverebene und auf Zonenebene.

> [!CAUTION]
> Bearbeiten Sie die Registrierung nur dann direkt, wenn Sie keine Alternative haben. Der Registrierungs-Editor umgeht Standard-Sicherheitsvorkehrungen und ermöglicht Einstellungen, die die Leistung beeinträchtigen, das System beschädigen oder sogar die Neuinstallation von Windows erfordern. Sie können die meisten Registrierungs Einstellungen sicher ändern, indem Sie die Programme in der Systemsteuerung oder Microsoft Management Console (MMC) verwenden. Wenn Sie die Registrierung direkt bearbeiten müssen, sichern Sie Sie zuerst. Weitere Informationen finden Sie in der Hilfe zum Registrierungs-Editor.

### <a name="server-level-syntax"></a>Syntax auf Server Ebene

```
dnscmd [<servername>] /config <parameter>
```

#### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| ---------- | ----------- |
| `<servername>` | Gibt den DNS-Server an, den Sie verwalten möchten, dargestellt durch lokale Computer Syntax, IP-Adresse, FQDN oder Hostname. Wenn dieser Parameter weggelassen wird, wird der lokale Server verwendet. |
| `<parameter>` | Geben Sie eine Einstellung und als Option einen Wert an. Parameterwerte verwenden diese Syntax: *Parameter* [*value*]. |
| /addressanswerlimit`[0|5-28]` | Gibt die maximale Anzahl von Host Datensätzen an, die ein DNS-Server als Reaktion auf eine Abfrage senden kann. Der Wert kann NULL (0) sein, oder er kann im Bereich von 5 bis 28 Datensätzen liegen. Der Standardwert ist 0 (null). |
| /bindsecondaries`[0|1]` | Ändert das Format der Zonen Übertragung, sodass die maximale Komprimierung und Effizienz erreicht werden kann. Akzeptiert die Werte:<ul><li>**0** -verwendet maximale Komprimierung und ist kompatibel mit Bindungs Versionen 4.9.4 und höher</li><li>**1** : sendet nur einen Ressourcen Daten Satz pro Nachricht an nicht-Microsoft-DNS-Server und ist mit Bindungs Versionen vor 4.9.4 kompatibel. Dies ist die Standardeinstellung.</li></ul> |
| /bootmethod`[0|1|2|3]` | Bestimmt die Quelle, aus der der DNS-Server seine Konfigurationsinformationen erhält. Akzeptiert die Werte:<ul><li>**0** -löscht die Quelle der Konfigurationsinformationen.</li><li>**1** : lädt aus der Bindungs Datei, die sich im DNS-Verzeichnis befindet ( `%systemroot%\System32\DNS` standardmäßig).</li><li>**2** : lädt aus der Registrierung.</li><li>**3** : lädt aus AD DS und der Registrierung. Dies ist die Standardeinstellung.</li></ul> |
| /defaultagingstate`[0|1]` | Bestimmt, ob das DNS-Bereinigung-Feature für neu erstellte Zonen standardmäßig aktiviert ist. Akzeptiert die Werte:<ul><li>**0** -deaktiviert das Scavenging. Dies ist die Standardeinstellung.</li><li>**1** : aktiviert das scräging.</li></ul> |
| /defaultnorefreshinterval`[0x1-0xFFFFFFFF|0xA8]` | Legt einen Zeitraum fest, in dem keine Aktualisierungen für dynamisch aktualisierte Datensätze akzeptiert werden. Zonen auf dem Server erben diesen Wert automatisch.<p>Um den Standardwert zu ändern, geben Sie einen Wert im Bereich von **0x1-0xFFFFFFFF**ein. Der Standardwert des Servers ist **0xa8**. |
| /defaultrefreshinterval `[0x1-0xFFFFFFFF|0xA8]` | Legt einen Zeitraum fest, der für dynamische Updates für DNS-Einträge zulässig ist. Zonen auf dem Server erben diesen Wert automatisch.<p>Um den Standardwert zu ändern, geben Sie einen Wert im Bereich von **0x1-0xFFFFFFFF**ein. Der Standardwert des Servers ist **0xa8**. |
| /disableautoreversezones `[0|1]` | Aktiviert oder deaktiviert die automatische Erstellung von Reverse-Lookupzonen. Reverse-Lookupzonen bieten die Auflösung von IP-Adressen (Internet Protocol) für DNS-Domänen Namen. Akzeptiert die Werte:<ul><li>**0** : aktiviert die automatische Erstellung von Reverse-Lookupzonen. Dies ist die Standardeinstellung.</li><li>**1** : deaktiviert die automatische Erstellung von Reverse-Lookupzonen.</li></ul> |
| /disablensrecordsautocreation `[0|1]` | Gibt an, ob der DNS-Server automatisch Namen Server-Ressourcen Einträge (NS) für die von ihm gehosteten Zonen erstellt. Akzeptiert die Werte:<ul><li>**0** -erstellt automatisch Namen Server-Ressourcen Einträge für Zonen, die vom DNS-Server gehostet werden.</li><li>**1** : Es werden nicht automatisch Namen Server-Ressourcen Einträge für Zonen erstellt, die vom DNS-Server gehostet werden.</li></ul> |
| /dspollinginterval `[0-30]` | Gibt an, wie oft der DNS-Server AD DS nach Änderungen in den in Active Directory integrierten Zonen abruft. |
| /dstombstoneinterval `[1-30]` |Der Zeitraum in Sekunden, in dem gelöschte Datensätze in AD DS beibehalten werden. |
| /ednscachetimeout `[3600-15724800]` | Gibt die Anzahl der Sekunden an, für die erweiterte DNS-Informationen (EDNS) zwischengespeichert werden. Der Minimalwert ist **3600**, und der Höchstwert ist **15.724.800**. Der Standardwert ist **604.800** Sekunden (eine Woche). |
| /enableednsprobes `[0|1]` | Aktiviert oder deaktiviert den Server zum Prüfen anderer Server, um zu bestimmen, ob EDNS unterstützt werden. Akzeptiert die Werte:<ul><li>**0** -deaktiviert die aktive Unterstützung für EDNS-Tests.</li><li>**1** : aktiviert die aktive Unterstützung für EDNS-Tests.</li></ul> |
| /enablednssec `[0|1]` | Aktiviert oder deaktiviert die Unterstützung für DNS-Sicherheitserweiterungen (DNSSEC). Akzeptiert die Werte:<ul><li>**0** -deaktiviert DNSSEC.</li><li>**1** : aktiviert DNSSEC.</li></ul> |
| /enableglobalnamessupport `[0|1]` | Aktiviert oder deaktiviert die Unterstützung für die GlobalNames-Zone. Die GlobalNames-Zone unterstützt die Auflösung von DNS-Namen mit einer einzelnen Bezeichnung in einer Gesamtstruktur. Akzeptiert die Werte:<ul><li>**0** -deaktiviert die Unterstützung für die GlobalNames-Zone. Wenn Sie den Wert dieses Befehls auf 0 festlegen, werden die Namen mit einer einzelnen Bezeichnung in der GlobalNames-Zone nicht durch den DNS-Server Dienst aufgelöst.</li><li>**1** : aktiviert die Unterstützung für die GlobalNames-Zone. Wenn Sie den Wert dieses Befehls auf 1 festlegen, löst der DNS-Server Dienstnamen mit einer einzelnen Bezeichnung in der GlobalNames-Zone auf.</li></ul> |
| /enableglobalqueryblocklist `[0|1]` | Aktiviert oder deaktiviert die Unterstützung für die globale Abfrage Sperr Liste, die die Namensauflösung für Namen in der Liste blockiert. Der DNS-Server Dienst erstellt und aktiviert die globale Abfrage Sperr Liste standardmäßig, wenn der Dienst erstmalig gestartet wird. Verwenden Sie den Befehl dnscmd/Info **/globalqueryblocklist** , um die aktuelle Liste der globalen Abfrage Blöcke anzuzeigen. Akzeptiert die Werte:<ul><li>**0** -deaktiviert die Unterstützung für die globale Abfrage Sperr Liste. Wenn Sie den Wert dieses Befehls auf 0 festlegen, antwortet der DNS-Server Dienst auf Abfragen für Namen in der Sperr Liste.</li><li>**1** : aktiviert die Unterstützung für die globale Abfrage Sperr Liste. Wenn Sie den Wert dieses Befehls auf 1 festlegen, antwortet der DNS-Server Dienst nicht auf Abfragen für Namen in der Sperr Liste.</li></ul> |
| /eventloglevel `[0|1|2|4]` | Bestimmt, welche Ereignisse im DNS-Server Protokoll in Ereignisanzeige protokolliert werden. Akzeptiert die Werte:<ul><li>**0** -keine Ereignisse werden protokolliert.</li><li>**1** -nur Fehler werden protokolliert.</li><li>**2** : nur Fehler und Warnungen werden protokolliert.</li><li>**4** : protokolliert Fehler, Warnungen und Informations Ereignisse. Dies ist die Standardeinstellung.</li></ul> |
| /forwarddelegations `[0|1]` | Bestimmt, wie der DNS-Server eine Abfrage für eine delegierte unter Zone behandelt. Diese Abfragen können entweder an die unter Zone gesendet werden, auf die in der Abfrage verwiesen wird, oder an die Liste der Weiterleitungen, die für den DNS-Server benannt werden. Einträge in der-Einstellung werden nur verwendet, wenn die Weiterleitung aktiviert ist. Akzeptiert die Werte:<ul><li>**0** -sendet automatisch Abfragen, die auf delegierte Subzonen verweisen, auf die entsprechende unter Zone. Dies ist die Standardeinstellung.</li><li>**1** : leitet Abfragen, die auf die Delegierte teilzone verweisen, auf die vorhandenen Weiterleitungen weiter.</li></ul> |
| /forwardingtimeout `[<seconds>]` | Bestimmt, wie viele Sekunden (**0x1-0xFFFFFFFF**) ein DNS-Server darauf wartet, dass eine Weiterleitung antwortet, bevor versucht wird, eine andere Weiterleitung zu versuchen. Der Standardwert ist **0x5**. der Standardwert ist 5 Sekunden. |
| /globalneamesqueryorder `[0|1]` | Gibt an, ob der DNS-Server Dienst beim Auflösen von Namen zuerst in der GlobalNames-Zone oder in lokalen Zonen sucht. Akzeptiert die Werte:<ul><li>**0** -der DNS-Server Dienst versucht, Namen aufzulösen, indem er die GlobalNames-Zone abfragt, bevor er die Zonen abfragt, für die er autorisierend ist.</li><li>**1** -der DNS-Server Dienst versucht, Namen aufzulösen, indem er die Zonen abfragt, für die er autorisierend ist, bevor er die GlobalNames-Zone abfragt.</li></ul> |
| /globalqueryblocklist`[[<name> [<name>]...]` | Ersetzt die aktuelle globale Abfrage Sperr Liste durch eine Liste der Namen, die Sie angeben. Wenn Sie keine Namen angeben, löscht dieser Befehl die Sperr Liste. Standardmäßig enthält die globale Abfrage Sperr Liste die folgenden Elemente:<ul><li>ISATAP</li><li>WPAD</li></ul>Der DNS-Server Dienst kann einen oder beide dieser Namen beim ersten Start entfernen, wenn er diese Namen in einer vorhandenen Zone findet. |
| /isslave `[0|1]` | Bestimmt, wie der DNS-Server antwortet, wenn von ihm weiterleiten Abfragen keine Antwort erhalten. Akzeptiert die Werte:<ul><li>**0** -gibt an, dass der DNS-Server keine untergeordnete ist. Wenn die Weiterleitung nicht antwortet, versucht der DNS-Server, die Abfrage selbst aufzulösen. Dies ist die Standardeinstellung.</li><li>**1** : gibt an, dass der DNS-Server untergeordnet ist. Wenn die Weiterleitung nicht antwortet, beendet der DNS-Server die Suche und sendet eine Fehlermeldung an den Resolver.</li></ul> |
| /localnetpriority `[0|1]` | Legt die Reihenfolge fest, in der die Host Datensätze zurückgegeben werden, wenn der DNS-Server über mehrere Host Einträge für denselben Namen verfügt. Akzeptiert die Werte:<ul><li>**0** -gibt die Datensätze in der Reihenfolge zurück, in der Sie in der DNS-Datenbank aufgelistet sind.</li><li>**1** : gibt die Datensätze zurück, die über ähnliche IP-Netzwerkadressen verfügen. Dies ist die Standardeinstellung.</li></ul> |
| /logfilemaxsize `[<size>]` | Gibt die maximale Größe in Bytes (**0x10000-0xFFFFFFFF**) der Datei "DNS. log" an. Wenn die maximale Größe der Datei erreicht wird, werden die ältesten Ereignisse von DNS überschrieben. Die Standardgröße ist **0x400000**, d. h. 4 Megabyte (MB). |
| /LogFilePath `[<path+logfilename>]` | Gibt den Pfad der Datei "DNS. log" an. Der Standardpfad lautet `%systemroot%\System32\Dns\Dns.log`. Sie können einen anderen Pfad angeben, indem Sie das Format verwenden `path+logfilename` . |
| /logipfilterlist `<IPaddress> [,<IPaddress>...]` | Gibt an, welche Pakete in der Debug-Protokolldatei protokolliert werden. Bei den Einträgen handelt es sich um eine Liste von IP-Adressen. Es werden nur Pakete protokolliert, die an die IP-Adressen in der Liste geleitet werden. |
| /loglevel `[<eventtype>]` | Bestimmt, welche Ereignis Typen in der Datei "DNS. log" aufgezeichnet werden. Jeder Ereignistyp wird durch eine hexadezimale Zahl dargestellt. Wenn Sie mehr als ein Ereignis im Protokoll verwenden möchten, fügen Sie die Werte mithilfe der hexadezimalen Addition hinzu, und geben Sie dann die Summe ein. Akzeptiert die Werte:<ul><li>**0x0** -der DNS-Server erstellt kein Protokoll. Dies ist der Standardeintrag.</li><li>**0x10** -protokolliert Abfragen und Benachrichtigungen.</li><li>**0x20** : protokolliert Updates.</li><li>**0xFE** -protokolliert Transaktionen, die nicht abgefragt werden.</li><li>**0x100** -protokolliert Frage Transaktionen.</li><li>**0x200** : protokolliert Antworten.</li><li>**0x1000** -protokolliert Sende Pakete.</li><li>**0x2000** -protokolliert Pakete.</li><li>**0x4000** : protokolliert UDP (User Datagram Protocol)-Pakete.</li><li>**0X8000** -protokolliert TCP (Transmission Control Protocol)-Pakete.</li><li>**0xFFFF** -protokolliert alle Pakete.</li><li>**0x10000** -protokolliert Active Directory-Schreib Transaktionen.</li><li>**0x20000** -protokolliert Active Directory-Update Transaktionen.</li><li>**0x1000000** -protokolliert vollständige Pakete.</li><li>**0x80000000** : protokolliert Schreib Transaktionen.</li><li></ul> |
| /maxcachesize | Gibt die maximale Größe des Arbeitsspeicher Caches des DNS-Servers in Kilobyte (KB) an. |
| /maxcachettl `[<seconds>]` | Bestimmt, wie viele Sekunden (**0x0-0xFFFFFFFF**) ein Datensatz im Cache gespeichert wird. Wenn die **0x0** -Einstellung verwendet wird, speichert der DNS-Server keine Datensätze zwischen. Die Standardeinstellung ist **0x15180** (86.400 Sekunden oder 1 Tag). |
| /maxnegativecachettl `[<seconds>]` | Gibt an, wie viele Sekunden (**0x1-0xFFFFFFFF**) ein Eintrag, der eine negative Antwort auf eine Abfrage aufzeichnet, weiterhin im DNS-Cache gespeichert wird. Die Standardeinstellung ist **0x384** (900 Sekunden). |
| /namecheckflag `[0|1|2|3]` | Gibt an, welcher Zeichen Standard beim Überprüfen von DNS-Namen verwendet wird. Akzeptiert die Werte:<ul><li>**0** -verwendet ANSI-Zeichen, die die IETF (Internet Engineering Task Force)-Anforderung für Kommentare (RFCs) erfüllen.</li><li>**1** : verwendet ANSI-Zeichen, die nicht notwendigerweise mit IETF-RFCs übereinstimmen.</li><li>**2** : verwendet Multibytezeichen-UCS-Transformations Format 8 (UTF-8). Dies ist die Standardeinstellung.</li><li>**3** -verwendet alle Zeichen.</li></ul> |
| /norecursion `[0|1]` | Bestimmt, ob ein DNS-Server eine rekursive Namensauflösung ausführt. Akzeptiert die Werte:<ul><li>**0** -der DNS-Server führt eine rekursive Namensauflösung aus, wenn er in einer Abfrage angefordert wird. Dies ist die Standardeinstellung.</li><li>**1** -der DNS-Server führt keine rekursive Namensauflösung aus.</li></ul> |
| /notcp | Dieser Parameter ist veraltet und hat keine Auswirkung auf die aktuellen Versionen von Windows Server. |
| /recursionretry `[<seconds>]` | Bestimmt die Anzahl von Sekunden (**0x1-0xFFFFFFFF**), die ein DNS-Server wartet, bevor er erneut versucht, eine Verbindung mit einem Remote Server herzustellen. Die Standardeinstellung ist **0x3** (drei Sekunden). Dieser Wert sollte angehoben werden, wenn die Rekursion über eine langsame WAN-Verbindung (Wide Area Network) erfolgt. |
| /recursiontimeout `[<seconds>]` | Bestimmt die Anzahl von Sekunden (**0x1-0xFFFFFFFF**), die ein DNS-Server wartet, bevor versucht wird, einen Remote Server zu kontaktieren. Die Einstellungen liegen zwischen **0x1** und **0xFFFFFFFF**. Die Standardeinstellung ist **0xF** (15 Sekunden). Dieser Wert sollte angehoben werden, wenn die Rekursion über eine langsame WAN-Verbindung erfolgt. |
| /roundrobin `[0|1]` | Bestimmt die Reihenfolge, in der Host Datensätze zurückgegeben werden, wenn ein Server über mehrere Host Einträge für denselben Namen verfügt. Akzeptiert die Werte:<ul><li>**0** -der DNS-Server verwendet kein Roundrobin. Stattdessen wird der erste Datensatz an jede Abfrage zurückgegeben.</li><li>**1** -der DNS-Server wechselt zwischen den Datensätzen, die von oben nach unten in der Liste der übereinstimmenden Datensätze zurückgegeben werden. Dies ist die Standardeinstellung.</li></ul> |
| /rpcprotocol `[0x0|0x1|0x2|0x4|0xFFFFFFFF]` | Gibt das Protokoll an, das vom Remote Prozedur Aufruf (RPC) verwendet wird, wenn eine Verbindung vom DNS-Server hergestellt wird. Akzeptiert die Werte:<ul><li>**0x0** : deaktiviert RPC für DNS.</li><li>**0x01** : verwendet TCP/IP.</li><li>**0x2** -verwendet Named Pipes.</li><li>**0x4** -verwendet Local Procedure Call(LPC).</li><li>**0xFFFFFFFF** -alle Protokolle. Dies ist die Standardeinstellung.</li></ul> |
| /scavenginginterval `[<hours>]` | Bestimmt, ob das Bereinigung-Feature für den DNS-Server aktiviert ist, und legt die Anzahl von Stunden (**0x0-0xFFFFFFFF**) zwischen den Bereinigung-Zyklen fest. Die Standardeinstellung ist **0x0**, wodurch das Bereinigung für den DNS-Server deaktiviert wird. Eine Einstellung, die größer als **0x0** ist, ermöglicht das Bereinigung für den Server und legt die Anzahl von Stunden zwischen den Schleifen Zyklen fest. |
| /secureresponses `[0|1]` | Bestimmt, ob DNS Datensätze filtert, die in einem Cache gespeichert werden. Akzeptiert die Werte:<ul><li>**0** -speichert alle Antworten, um Abfragen in einem Cache zu benennen. Dies ist die Standardeinstellung.</li><li>**1** : speichert nur die Datensätze, die zur gleichen DNS-Unterstruktur gehören, in einem Cache.</li></ul> |
| /sendport `[<port>]` | Gibt die Portnummer (**0x0-0xFFFFFFFF**) an, die von DNS verwendet wird, um rekursive Abfragen an andere DNS-Server zu senden. Die Standardeinstellung ist **0x0**. Dies bedeutet, dass die Portnummer nach dem Zufallsprinzip ausgewählt wird. |
| /config-/serverlevelplugindll`[<dllpath>]` | Gibt den Pfad eines benutzerdefinierten Plug-ins an. Wenn DllPath den voll qualifizierten Pfadnamen eines gültigen DNS-Server-Plug-ins angibt, ruft der DNS-Serverfunktionen im Plug-in auf, um Namens Abfragen aufzulösen, die außerhalb des Bereichs aller lokal gehosteten Zonen liegen. Wenn ein abgefragten Name außerhalb des Gültigkeits Bereichs des Plug-ins liegt, führt der DNS-Server die Namensauflösung mithilfe der Weiterleitungs-oder Rekursion gemäß der Konfiguration aus. Wenn DllPath nicht angegeben ist, verwendet der DNS-Server kein benutzerdefiniertes Plug-in, wenn zuvor ein benutzerdefiniertes Plug-in konfiguriert wurde. |
| /strictfileparsing `[0|1]` | Bestimmt das Verhalten eines DNS-Servers, wenn beim Laden einer Zone ein fehlerhafter Datensatz auftritt. Akzeptiert die Werte:<ul><li>**0** -der DNS-Server lädt weiterhin die Zone, auch wenn auf dem Server ein fehlerhafter Datensatz auftritt. Der Fehler wird im DNS-Protokoll aufgezeichnet. Dies ist die Standardeinstellung.</li><li>**1** -der DNS-Server beendet das Laden der Zone und zeichnet den Fehler im DNS-Protokoll auf.</li></ul> |
| /updateoptions `<RecordValue>` | Untersagt dynamische Updates der angegebenen Daten Satz Typen. Wenn Sie möchten, dass im Protokoll mehrere Daten Satz Typen nicht zulässig sind, fügen Sie die Werte mit der hexadezimalen Addition hinzu, und geben Sie dann die Summe ein. Akzeptiert die Werte:<ul><li>**0x0** -beschränkt keine Daten Satz Typen.</li><li>**0x1** -schließt den Start der Autoritäts Ressourcen Einträge (SOA) aus.</li><li>**0x2** -schließt Namen Server-Ressourcen Einträge (NS) aus.</li><li>**0x4** -schließt die Delegierung von Namen Server-Ressourcen Einträgen (NS) aus.</li><li>**0x8** -schließt Server Host Einträge aus.</li><li>**0x100** : während des sicheren dynamischen Updates werden die Ressourcen Einträge für die Start-of-Authority (SOA) ausgeschlossen.</li><li>**0x200** : während des sicheren dynamischen Updates schließt Stamm Namen Server-Ressourcen Einträge (NS) aus.</li><li>**0x30f** : bei einem standardmäßigen dynamischen Update werden Namen Server Ressourcen Einträge (NS), Ressourcen Einträge für die Autoritäts Quelle (Start of Authority, SOA) und Server Host Einträge ausgeschlossen. Während des sicheren dynamischen Updates schließt Root Nameserver (NS)-Ressourcen Einträge und Ressourcen Einträge für den Start von Authority (SOA) aus. Ermöglicht Delegierungen und Server Host Updates.</li><li>**0x400** : beim sicheren dynamischen Update werden die NS-Ressourcen Einträge (Delegierungs Nameserver) ausgeschlossen.</li><li>**0x800** : während des sicheren dynamischen Updates schließt Server Host Einträge aus.</li><li>**0x1000000** -schließt Delegierungs Signatur Geber (DS)-Einträge aus.</li><li>**0x80000000** : deaktiviert das dynamische DNS-Update.</li></ul> |
| /writeauthorityns `[0|1]` | Bestimmt, wann der DNS-Servernamen Server-Ressourcen Einträge (NS) im Autorisierungs Abschnitt einer Antwort schreibt. Akzeptiert die Werte:<ul><li>**0** -Schreibvorgänge für Namen Server (NS)-Ressourcen Einträge werden nur im Autorisierungs Abschnitt der Verweise geschrieben. Diese Einstellung entspricht den Konzepten und Funktionen von RFC 1034, den Domänen Namen und RFC 2181 und erläutert die DNS-Spezifikation. Dies ist die Standardeinstellung.</li><li>**1** : schreibt Namen Server-Ressourcen Einträge (Nameserver, NS) im Autorisierungs Abschnitt aller erfolgreichen autorisierenden Antworten.</li></ul> |
| /xfrconnecttimeout `[<seconds>]` | Bestimmt die Anzahl von Sekunden (**0x0-0xFFFFFFFF**), die ein primärer DNS-Server auf eine Übertragungs Antwort vom sekundären Server wartet. Der Standardwert ist **0x1E** (30 Sekunden). Nachdem der Timeout Wert abgelaufen ist, wird die Verbindung beendet. |

### <a name="zone-level-syntax"></a>Syntax auf Zonenebene

Ändert die Konfiguration der angegebenen Zone. Der Zonenname muss nur für Parameter auf Zonenebene angegeben werden.

```
dnscmd /config <parameters>
```

#### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| ---------- | ----------- |
| `<parameter>` | Geben Sie eine Einstellung, einen Zonen Namen und als Option einen Wert an. Parameter Werte verwenden diese Syntax: `zonename parameter [value]` . |
| /aging `<zonename>`| Aktiviert oder deaktiviert das Bereinigung in einer bestimmten Zone. |
| /AllowNSRecordsAutoCreation `<zonename>``[value]` | Überschreibt die Einstellung für die automatische Erstellung des Namensserver-Ressourceneinsatzes des DNS-Servers. Name Server (NS)-Ressourcen Einträge, die zuvor für diese Zone registriert wurden, sind nicht betroffen. Daher müssen Sie Sie manuell entfernen, wenn Sie Sie nicht möchten. |
| /allowupdate `<zonename>` | Bestimmt, ob die angegebene Zone dynamische Updates akzeptiert. |
| /forwarderslave `<zonename>` | Überschreibt die **/isslave** -Einstellung des DNS-Servers. |
| /forwardertimeout `<zonename>` | Bestimmt, wie viele Sekunden eine DNS-Zone darauf wartet, dass eine Weiterleitung antwortet, bevor eine andere Weiterleitung versucht wird. Dieser Wert überschreibt den Wert, der auf Serverebene festgelegt wird. |
| /norefreshinterval `<zonename>` | Legt ein Zeitintervall für eine Zone fest, in der keine Aktualisierungen DNS-Einträge in einer angegebenen Zone dynamisch aktualisieren können. |
| /refreshinterval `<zonename>` | Legt ein Zeitintervall für eine Zone fest, in der Aktualisierungen DNS-Einträge in einer angegebenen Zone dynamisch aktualisieren können. |
| /securesecondaries `<zonename>` | Bestimmt, welche sekundären Server Zonen Aktualisierungen vom Master Server für diese Zone empfangen können. |

## <a name="dnscmd-createbuiltindirectorypartitions-command"></a>dnscmd/createbuiltindirectorypartitions-Befehl

Erstellt eine DNS-Anwendungsverzeichnis Partition. Wenn DNS installiert ist, wird eine Anwendungsverzeichnis Partition für den Dienst auf der Gesamtstruktur-und Domänen Ebene erstellt. Verwenden Sie diesen Befehl, um DNS-Anwendungsverzeichnis Partitionen zu erstellen, die gelöscht oder nie erstellt wurden. Ohne Parameter erstellt dieser Befehl eine integrierte DNS-Verzeichnis Partition für die Domäne.

### <a name="syntax"></a>Syntax

```
dnscmd [<servername>] /createbuiltindirectorypartitions [/forest] [/alldomains]
```

#### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| ---------- | ----------- |
| `<servername>` | Gibt den zu verwaltenden DNS-Server an, der durch die IP-Adresse, den FQDN oder den Hostnamen repräsentiert wird. Wenn dieser Parameter weggelassen wird, wird der lokale Server verwendet. |
| /forest | Erstellt eine DNS-Verzeichnis Partition für die Gesamtstruktur. |
| /alldomains | Erstellt DNS-Partitionen für alle Domänen in der Gesamtstruktur. |

## <a name="dnscmd-createdirectorypartition-command"></a>dnscmd/createdirectorypartition-Befehl

Erstellt eine DNS-Anwendungsverzeichnis Partition. Wenn DNS installiert ist, wird eine Anwendungsverzeichnis Partition für den Dienst auf der Gesamtstruktur-und Domänen Ebene erstellt. Mit diesem Vorgang werden zusätzliche DNS-Anwendungsverzeichnis Partitionen erstellt.

### <a name="syntax"></a>Syntax

```
dnscmd [<servername>] /createdirectorypartition <partitionFQDN>
```

#### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| ---------- | ----------- |
| `<servername>` | Gibt den zu verwaltenden DNS-Server an, der durch die IP-Adresse, den FQDN oder den Hostnamen repräsentiert wird. Wenn dieser Parameter weggelassen wird, wird der lokale Server verwendet. |
| `<partitionFQDN>` | Der voll qualifizierte Name der DNS-Anwendungsverzeichnis Partition, die erstellt wird. |

## <a name="dnscmd-deletedirectorypartition-command"></a>dnscmd/deletedirectorypartition-Befehl

Entfernt eine vorhandene DNS-Anwendungsverzeichnis Partition.

### <a name="syntax"></a>Syntax

```
dnscmd [<servername>] /deletedirectorypartition <partitionFQDN>
```

#### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| ---------- | ----------- |
| `<servername>` | Gibt den zu verwaltenden DNS-Server an, der durch die IP-Adresse, den FQDN oder den Hostnamen repräsentiert wird. Wenn dieser Parameter weggelassen wird, wird der lokale Server verwendet. |
| `<partitionFQDN>` | Der voll qualifizierte Name der DNS-Anwendungsverzeichnis Partition, die entfernt werden soll. |

## <a name="dnscmd-directorypartitioninfo-command"></a>dnscmd/directorypartitioninfo-Befehl

Listet Informationen zu einer angegebenen DNS-Anwendungsverzeichnis Partition auf.

### <a name="syntax"></a>Syntax

```
dnscmd [<servername>] /directorypartitioninfo <partitionFQDN> [/detail]
```

#### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| ---------- | ----------- |
| `<servername>` | Gibt den zu verwaltenden DNS-Server an, der durch die IP-Adresse, den FQDN oder den Hostnamen repräsentiert wird. Wenn dieser Parameter weggelassen wird, wird der lokale Server verwendet. |
| `<partitionFQDN>` | Der voll qualifizierte Name der DNS-Anwendungsverzeichnis Partition. |
| /detail | Listet alle Informationen zur Anwendungsverzeichnis Partition auf. |

## <a name="dnscmd-enlistdirectorypartition-command"></a>dnscmd/enlistdirectorypartition-Befehl

Fügt der Replikat Gruppe der angegebenen Verzeichnis Partition den DNS-Server hinzu.

### <a name="syntax"></a>Syntax

```
dnscmd [<servername>] /enlistdirectorypartition <partitionFQDN>
```

#### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| ---------- | ----------- |
| `<servername>` | Gibt den zu verwaltenden DNS-Server an, der durch die IP-Adresse, den FQDN oder den Hostnamen repräsentiert wird. Wenn dieser Parameter weggelassen wird, wird der lokale Server verwendet. |
| `<partitionFQDN>` | Der voll qualifizierte Name der DNS-Anwendungsverzeichnis Partition. |

## <a name="dnscmd-enumdirectorypartitions-command"></a>dnscmd/EnumDirectoryPartitions-Befehl

Listet die DNS-Anwendungsverzeichnis Partitionen für den angegebenen Server auf.

### <a name="syntax"></a>Syntax

```
dnscmd [<servername>] /enumdirectorypartitions [/custom]
```

#### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| ---------- | ----------- |
| `<servername>` | Gibt den zu verwaltenden DNS-Server an, der durch die IP-Adresse, den FQDN oder den Hostnamen repräsentiert wird. Wenn dieser Parameter weggelassen wird, wird der lokale Server verwendet. |
| /custom | Listet nur von Benutzern erstellte Verzeichnis Partitionen auf. |

## <a name="dnscmd-enumrecords-command"></a>dnscmd/enumrecords-Befehl

Listet die Ressourcen Einträge eines angegebenen Knotens in einer DNS-Zone auf.

### <a name="syntax"></a>Syntax

```
dnscmd [<servername>] /enumrecords <zonename> <nodename> [/type <rrtype> <rrdata>] [/authority] [/glue] [/additional] [/node | /child | /startchild<childname>] [/continue | /detail]
```

#### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| ---------- | ----------- |
| `<servername>` | Gibt den zu verwaltenden DNS-Server an, der durch die IP-Adresse, den FQDN oder den Hostnamen repräsentiert wird. Wenn dieser Parameter weggelassen wird, wird der lokale Server verwendet. |
| /enumrecords | Listet die Ressourcen Einträge in der angegebenen Zone auf. |
| `<zonename>` | Gibt den Namen der Zone an, zu der die Ressourcen Einträge gehören. |
| `<nodename>` | Gibt den Namen des Knotens der Ressourcen Datensätze an. |
| `[/type <rrtype> <rrdata>]` | Gibt den Typ der aufzurufenden Ressourcen Einträge und den Typ der erwarteten Daten an. Akzeptiert die Werte:<ul><li>`<rrtype>` : Gibt den Typ der Ressourcen Datensätze an, die aufgelistet werden sollen.</li><li>`<rrdata>` : Gibt den Typ der Daten an, die als Datensatz erwartet werden.</li></ul> |
| /authority | Schließt autorisierende Daten ein. |
| /glue | Enthält die Daten der Daten. |
| /additional | Enthält alle zusätzlichen Informationen über die aufgelisteten Ressourcen Einträge. |
| /Node | Listet nur die Ressourcen Datensätze des angegebenen Knotens auf. |
| /Child | Listet nur die Ressourcen Datensätze einer angegebenen untergeordneten Domäne auf. |
| /startchild`<childname>` | Startet die Liste in der angegebenen untergeordneten Domäne. |
| /Continue | Listet nur die Ressourcen Datensätze mit Ihrem Typ und den zugehörigen Daten auf. |
| /detail | Listet alle Informationen über die Ressourcen Datensätze auf. |

#### <a name="example"></a>Beispiel

```
dnscmd /enumrecords test.contoso.com test /additional
```

## <a name="dnscmd-enumzones-command"></a>dnscmd/enumzones-Befehl

Listet die Zonen auf, die auf dem angegebenen DNS-Server vorhanden sind. Die **enumzonenparameter** fungieren als Filter in der Liste der Zonen. Wenn keine Filter angegeben werden, wird eine komplette Liste der Zonen zurückgegeben. Wenn ein Filter angegeben wird, sind nur die Zonen, die die Kriterien dieses Filters erfüllen, in der zurückgegebenen Liste der Zonen enthalten.

### <a name="syntax"></a>Syntax

```
dnscmd [<servername>] /enumzones [/primary | /secondary | /forwarder | /stub | /cache | /auto-created] [/forward | /reverse | /ds | /file] [/domaindirectorypartition | /forestdirectorypartition | /customdirectorypartition | /legacydirectorypartition | /directorypartition <partitionFQDN>]
```

#### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| ---------- | ----------- |
| `<servername>` | Gibt den zu verwaltenden DNS-Server an, der durch die IP-Adresse, den FQDN oder den Hostnamen repräsentiert wird. Wenn dieser Parameter weggelassen wird, wird der lokale Server verwendet. |
| /primary | Listet alle Zonen auf, bei denen es sich entweder um Standard primäre Zonen oder integrierte Active Directory-Zonen handelt. |
| /secondary | Listet alle sekundären Standard Zonen auf. |
| /forwarder | Listet Zonen, die nicht aufgelöste Abfragen an einen anderen DNS-Server weiterleiten |
| /Stub | Listet alle Stub-Zonen auf. |
| /Cache | Listet nur die Zonen auf, die in den Cache geladen werden. |
| /auto-created] | Listet die Zonen auf, die während der Installation des DNS-Servers automatisch erstellt wurden. |
| /forward | Listet Forward-Lookupzonen auf. |
| /reverse | Listet Reverse-Lookupzonen auf. |
| /ds | Listet integrierte Active Directory-Zonen auf. |
| /file | Listet Zonen auf, die von Dateien unterstützt werden. |
| /domaindirectorypartition | Listet Zonen auf, die in der Domänen Verzeichnis Partition gespeichert sind. |
| /forestdirectorypartition | Listet Zonen auf, die in der DNS-Anwendungsverzeichnis Partition der Gesamtstruktur gespeichert sind. |
| /customdirectorypartition | Listet alle Zonen auf, die in einer benutzerdefinierten Anwendungsverzeichnis Partition gespeichert sind. |
| /legacydirectorypartition | Listet alle Zonen auf, die in der Domänen Verzeichnis Partition gespeichert sind. |
| /directorypartition `<partitionFQDN>` | Listet alle Zonen auf, die in der angegebenen Verzeichnis Partition gespeichert sind. |

#### <a name="examples"></a>Beispiele

- [Beispiel 2: Anzeigen einer kompletten Liste der Zonen auf einem DNS-Server](/previous-versions/windows/it-pro/windows-server-2003/cc784399(v=ws.10)#example-2-display-a-complete-list-of-zones-on-a-dns-server)

- [Beispiel 3: Anzeigen einer Liste automatisch erstellter Zonen auf einem DNS-Server](/previous-versions/windows/it-pro/windows-server-2003/cc784399(v=ws.10)#example-3-display-a-list-of-autocreated-zones-on-a-dns-server)

## <a name="dnscmd-exportsettings-command"></a>dnscmd/ExportSettings-Befehl

Erstellt eine Textdatei, in der die Konfigurationsdetails eines DNS-Servers aufgelistet sind. Die Textdatei hat den Namen *DnsSettings.txt*. Sie befindet sich im `%systemroot%\system32\dns` Verzeichnis des Servers. Mithilfe der Informationen in der von **dnscmd/ExportSettings** erstellten Datei können Sie Konfigurationsprobleme beheben oder sicherstellen, dass Sie mehrere Server identisch konfiguriert haben.

### <a name="syntax"></a>Syntax

```
dnscmd [<servername>] /exportsettings
```

#### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| ---------- | ----------- |
| `<servername>` | Gibt den zu verwaltenden DNS-Server an, der durch die IP-Adresse, den FQDN oder den Hostnamen repräsentiert wird. Wenn dieser Parameter weggelassen wird, wird der lokale Server verwendet. |

## <a name="dnscmd-info-command"></a>dnscmd/Info-Befehl

Zeigt Einstellungen aus dem DNS-Abschnitt der Registrierung des angegebenen Servers an `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\DNS\Parameters` . Verwenden Sie den Befehl, um Registrierungs Einstellungen auf Zonenebene anzuzeigen `dnscmd zoneinfo` .

### <a name="syntax"></a>Syntax

```
dnscmd [<servername>] /info [<settings>]
```

#### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| ---------- | ----------- |
| `<servername>` | Gibt den zu verwaltenden DNS-Server an, der durch die IP-Adresse, den FQDN oder den Hostnamen repräsentiert wird. Wenn dieser Parameter weggelassen wird, wird der lokale Server verwendet. |
| `<settings>` | Jede Einstellung, die der **Info** -Befehl zurückgibt, kann einzeln angegeben werden. Wenn keine Einstellung angegeben ist, wird ein Bericht mit allgemeinen Einstellungen zurückgegeben. |

#### <a name="example"></a>Beispiel

- [Beispiel 4: Anzeigen der isslave-Einstellung von einem DNS-Server](/previous-versions/windows/it-pro/windows-server-2003/cc784399(v=ws.10)#example-4-display-the-isslave-setting-from-a-dns-server)

- [Beispiel 5: Anzeigen der Einstellung "recursiontimeout" von einem DNS-Server](/previous-versions/windows/it-pro/windows-server-2003/cc784399(v=ws.10)#example-5-display-the-recursiontimeout-setting-from-a-dns-server)

## <a name="dnscmd-ipvalidate-command"></a>dnscmd/ipvalidate-Befehl

Testet, ob eine IP-Adresse einen funktionsfähigen DNS-Server identifiziert oder ob der DNS-Server als Weiterleitung, als root-Hinweis Server oder als Master Server für eine bestimmte Zone fungieren kann.

### <a name="syntax"></a>Syntax

```
dnscmd [<servername>] /ipvalidate <context> [<zonename>] [[<IPaddress>]]
```

#### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| ---------- | ----------- |
| `<servername>` | Gibt den zu verwaltenden DNS-Server an, der durch die IP-Adresse, den FQDN oder den Hostnamen repräsentiert wird. Wenn dieser Parameter weggelassen wird, wird der lokale Server verwendet. |
| `<context>` | Gibt den Typ des auszuführenden Tests an. Sie können einen der folgenden Tests angeben:<ul><li>**/DnsServers** : testet, ob die Computer mit den von Ihnen angegebenen Adressen funktionsfähige DNS-Server sind.</li><li>**/Forwarders** : testet, ob die von Ihnen angegebenen Adressen DNS-Server identifizieren, die als Weiterleitungen fungieren können.</li><li>**/roothints** : testet, ob die von Ihnen angegebenen Adressen DNS-Server identifizieren, die als Stamm Hinweis Server fungieren können.</li><li>**/zonemasters** : testet, ob die von Ihnen angegebenen Adressen DNS-Server identifizieren, die Master Server für *zonename*sind. |
| `<zonename>` | Identifiziert die Zone. Verwenden Sie diesen Parameter mit dem **/zonemasters** -Parameter. |
| `<IPaddress>` | Gibt die IP-Adressen an, die vom Befehl getestet werden. |

#### <a name="examples"></a>Beispiele

```
nscmd dnssvr1.contoso.com /ipvalidate /dnsservers 10.0.0.1 10.0.0.2
dnscmd dnssvr1.contoso.com /ipvalidate /zonemasters corp.contoso.com 10.0.0.2
```

## <a name="dnscmd-nodedelete-command"></a>dnscmd/nodedelete-Befehl

Löscht alle Datensätze für einen angegebenen Host.

### <a name="syntax"></a>Syntax

```
dnscmd [<servername>] /nodedelete <zonename> <nodename> [/tree] [/f]
```

#### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| ---------- | ----------- |
| `<servername>` | Gibt den zu verwaltenden DNS-Server an, der durch die IP-Adresse, den FQDN oder den Hostnamen repräsentiert wird. Wenn dieser Parameter weggelassen wird, wird der lokale Server verwendet. |
| `<zonename>` | Gibt den Namen der Zone an. |
| `<nodename>` | Gibt den Hostnamen des zu löschenden Knotens an. |
| /tree | Löscht alle untergeordneten Datensätze. |
| /f | Führt den Befehl aus, ohne zur Bestätigung aufzufordern. |

#### <a name="example"></a>Beispiel

[Beispiel 6: Löschen der Datensätze aus einem Knoten](/previous-versions/windows/it-pro/windows-server-2003/cc784399(v=ws.10)#example-6-delete-the-records-from-a-node)

## <a name="dnscmd-recordadd-command"></a>dnscmd/RecordAdd-Befehl

Fügt einer angegebenen Zone in einem DNS-Server einen Datensatz hinzu.

### <a name="syntax"></a>Syntax

```
dnscmd [<servername>] /recordadd <zonename> <nodename> <rrtype> <rrdata>
```

#### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| ---------- | ----------- |
| `<servername>` | Gibt den zu verwaltenden DNS-Server an, der durch die IP-Adresse, den FQDN oder den Hostnamen repräsentiert wird. Wenn dieser Parameter weggelassen wird, wird der lokale Server verwendet. |
| `<zonename>` | Gibt die Zone an, in der sich der Datensatz befindet. |
| `<nodename>` | Gibt einen bestimmten Knoten in der Zone an. |
| `<rrtype>` | Gibt den Typ des hinzu zufügenden Datensatzes an. |
| `<rrdata>` | Gibt den Typ der erwarteten Daten an. |

> [!NOTE]
> Nachdem Sie einen Datensatz hinzugefügt haben, stellen Sie sicher, dass Sie den richtigen Datentyp und das richtige Datenformat verwenden. Eine Liste der Ressourcen Daten Satz Typen und die entsprechenden Datentypen finden Sie unter [dnscmd examples](/previous-versions/windows/it-pro/windows-server-2003/cc784399(v=ws.10)).

#### <a name="examples"></a>Beispiele

```
dnscmd dnssvr1.contoso.com /recordadd test A 10.0.0.5
dnscmd /recordadd test.contoso.com test MX 10 mailserver.test.contoso.com
```

## <a name="dnscmd-recorddelete-command"></a>dnscmd/recorddelete-Befehl

Löscht einen Ressourcen Daten Satz in einer angegebenen Zone.

### <a name="syntax"></a>Syntax

```
dnscmd [<servername>] /recorddelete <zonename> <nodename> <rrtype> <rrdata> [/f]
```

#### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| ---------- | ----------- |
| `<servername>` | Gibt den zu verwaltenden DNS-Server an, der durch die IP-Adresse, den FQDN oder den Hostnamen repräsentiert wird. Wenn dieser Parameter weggelassen wird, wird der lokale Server verwendet. |
| `<zonename>` | Gibt die Zone an, in der sich der Ressourcen Daten Satz befindet. |
| `<nodename>` | Gibt den Namen des Hosts an. |
| `<rrtype>` | Gibt den Typ des zu löschenden Ressourcen Datensatzes an. |
| `<rrdata>` | Gibt den Typ der erwarteten Daten an. |
| /f | Führt den Befehl aus, ohne zur Bestätigung aufzufordern. Da Knoten mehr als einen Ressourcen Daten Satz aufweisen können, erfordert dieser Befehl, dass Sie sehr spezifisch für den Typ des Ressourcen Datensatzes sind, den Sie löschen möchten. Wenn Sie einen Datentyp angeben und keinen Typ von Ressourcen Daten Satz Daten angeben, werden alle Datensätze mit diesem spezifischen Datentyp für den angegebenen Knoten gelöscht. |

#### <a name="examples"></a>Beispiele

```
dnscmd /recorddelete test.contoso.com test MX 10 mailserver.test.contoso.com
```

## <a name="dnscmd-resetforwarders-command"></a>dnscmd/ResetForwarders-Befehl

Wählt die IP-Adressen aus, an die der DNS-Server DNS-Abfragen weiterleitet, wenn er Sie nicht lokal auflösen kann

### <a name="syntax"></a>Syntax

```
dnscmd [<servername>] /resetforwarders <IPaddress> [,<IPaddress>]...][/timeout <timeout>] [/slave | /noslave]
```

#### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| ---------- | ----------- |
| `<servername>` | Gibt den zu verwaltenden DNS-Server an, der durch die IP-Adresse, den FQDN oder den Hostnamen repräsentiert wird. Wenn dieser Parameter weggelassen wird, wird der lokale Server verwendet. |
| `<IPaddress>` | Listet die IP-Adressen, an die der DNS-Server nicht aufgelöste Abfragen weiterleitet. |
| /Timeout `<timeout>` | Legt die Anzahl von Sekunden fest, die der DNS-Server auf eine Antwort von der Weiterleitung wartet. Standardmäßig beträgt dieser Wert fünf Sekunden. |
| /slave | Verhindert, dass der DNS-Server seine eigenen iterativen Abfragen ausführt, wenn die Weiterleitung eine Abfrage nicht auflösen kann. |
| /noslave | Ermöglicht dem DNS-Server das Ausführen eigener iterativer Abfragen, wenn die Weiterleitung eine Abfrage nicht auflösen kann. Dies ist die Standardeinstellung. |
| /f | Führt den Befehl aus, ohne zur Bestätigung aufzufordern. Da Knoten mehr als einen Ressourcen Daten Satz aufweisen können, erfordert dieser Befehl, dass Sie sehr spezifisch für den Typ des Ressourcen Datensatzes sind, den Sie löschen möchten. Wenn Sie einen Datentyp angeben und keinen Typ von Ressourcen Daten Satz Daten angeben, werden alle Datensätze mit diesem spezifischen Datentyp für den angegebenen Knoten gelöscht. |

##### <a name="remarks"></a>Bemerkungen

- Standardmäßig führt ein DNS-Server iterative Abfragen aus, wenn er eine Abfrage nicht auflösen kann.

- Das Festlegen von IP-Adressen mithilfe des Befehls **ResetForwarders** bewirkt, dass der DNS-Server rekursive Abfragen an die DNS-Server bei den angegebenen IP-Adressen ausführt. Wenn die Weiterleitung die Abfrage nicht auflösen kann, kann der DNS-Server dann seine eigenen iterativen Abfragen ausführen.

- Wenn der **/Slave** -Parameter verwendet wird, führt der DNS-Server keine eigenen iterativen Abfragen aus. Dies bedeutet, dass der DNS-Server nicht aufgelöste Abfragen nur an die DNS-Server in der Liste weiterleitet und iterative Abfragen nicht versucht, wenn die Weiterleitungen diese nicht auflösen. Es ist effizienter, eine IP-Adresse als Weiterleitung für einen DNS-Server festzulegen. Sie können den Befehl **ResetForwarders** für interne Server in einem Netzwerk verwenden, um die nicht aufgelösten Abfragen an einen DNS-Server weiterzuleiten, der über eine externe Verbindung verfügt.

- Das doppelte Auflisten der IP-Adresse einer Weiterleitung bewirkt, dass der DNS-Server zweimal versucht, eine Weiterleitung an diesen Server auszuführen.

#### <a name="examples"></a>Beispiele

```
dnscmd dnssvr1.contoso.com /resetforwarders 10.0.0.1 /timeout 7 /slave
dnscmd dnssvr1.contoso.com /resetforwarders /noslave
```

## <a name="dnscmd-resetlistenaddresses-command"></a>dnscmd/ResetListenAddresses-Befehl

Gibt die IP-Adressen auf einem Server an, der auf DNS-Client Anforderungen lauscht. Standardmäßig lauschen alle IP-Adressen auf einem DNS-Server auf Client-DNS-Anforderungen.

### <a name="syntax"></a>Syntax

```
dnscmd [<servername>] /resetlistenaddresses <listenaddress>
```

#### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| ---------- | ----------- |
| `<servername>` | Gibt den zu verwaltenden DNS-Server an, der durch die IP-Adresse, den FQDN oder den Hostnamen repräsentiert wird. Wenn dieser Parameter weggelassen wird, wird der lokale Server verwendet. |
| `<listenaddress>` | Gibt eine IP-Adresse auf dem DNS-Server an, die auf DNS-Client Anforderungen lauscht. Wenn keine Abhör Adresse angegeben ist, lauschen alle IP-Adressen auf dem Server auf Client Anforderungen. |

#### <a name="examples"></a>Beispiele

```
dnscmd dnssvr1.contoso.com /resetlistenaddresses 10.0.0.1
```

## <a name="dnscmd-startscavenging-command"></a>dnscmd/startscavenging-Befehl

Weist einen DNS-Server an, eine sofortige Suche nach veralteten Ressourcen Einträgen in einem angegebenen DNS-Server zu versuchen.

### <a name="syntax"></a>Syntax

```
dnscmd [<servername>] /startscavenging
```

#### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| ---------- | ----------- |
| `<servername>` | Gibt den zu verwaltenden DNS-Server an, der durch die IP-Adresse, den FQDN oder den Hostnamen repräsentiert wird. Wenn dieser Parameter weggelassen wird, wird der lokale Server verwendet. |

##### <a name="remarks"></a>Bemerkungen

- Durch einen erfolgreichen Abschluss dieses Befehls wird ein Scavenge sofort gestartet. Wenn die Scavenge fehlschlägt, wird keine Warnmeldung angezeigt.

- Obwohl der Befehl zum Starten von Scavenge erfolgreich abgeschlossen wird, wird der Scavenge nicht gestartet, es sei denn, die folgenden Voraussetzungen sind erfüllt:

    - Das Scavenging ist sowohl für den Server als auch für die Zone aktiviert.

    - Die Zone wird gestartet.

    - Die Ressourcen Datensätze verfügen über einen Zeitstempel.

- Informationen zum Aktivieren von Bereinigung für den Server finden Sie im Abschnitt " **ScavengingInterval** " unter **Syntax auf Serverebene** im Abschnitt " **/config** ".

- Weitere Informationen zum Aktivieren von Bereinigung für die Zone finden Sie im Abschnitt über den **Aging** -Parameter unter **Syntax auf Zonenebene** im Abschnitt " **/config** ".

- Weitere Informationen zum Neustarten einer angehaltenen Zone finden Sie unter dem Parameter " **zoneresume** " in diesem Artikel.

- Informationen zum Überprüfen von Ressourcen Einträgen für einen Zeitstempel finden Sie unter dem Parameter " **AgeAllRecords** " in diesem Artikel.

#### <a name="examples"></a>Beispiele

```
dnscmd dnssvr1.contoso.com /startscavenging
```

## <a name="dnscmd-statistics-command"></a>dnscmd/Statistics-Befehl

Hiermit werden Daten für einen angegebenen DNS-Server angezeigt oder gelöscht.

### <a name="syntax"></a>Syntax

```
dnscmd [<servername>] /statistics [<statid>] [/clear]
```

#### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| ---------- | ----------- |
| `<servername>` | Gibt den zu verwaltenden DNS-Server an, der durch die IP-Adresse, den FQDN oder den Hostnamen repräsentiert wird. Wenn dieser Parameter weggelassen wird, wird der lokale Server verwendet. |
| `<statid>` | Gibt an, welche Statistik oder Kombination von Statistiken angezeigt werden soll. Der Befehl **Statistics** zeigt Indikatoren an, die beim Starten oder Fortsetzen des DNS-Servers beginnen. Eine Identifikationsnummer wird verwendet, um eine Statistik zu identifizieren. Wenn keine Statistik-ID-Nummer angegeben ist, werden alle Statistiken angezeigt. Die Zahlen, die angegeben werden können, sowie die entsprechende Statistik, die anzeigt, können Folgendes enthalten:<ul><li>**00000001** Zeit</li><li>**00000002** -Abfrage</li><li>**00000004** -query2</li><li>**00000008** -recurse</li><li>**00000010** -Master</li><li>**00000020** -Sekundär</li><li>**00000040** -WINS</li><li>**00000100** -Update</li><li>**00000200** -skwansec</li><li>**00000400** -DS</li><li>**00010000** -Arbeitsspeicher</li><li>**00100000** -packetmem</li><li>**00040000** -dBASE</li><li>**00080000** -Datensätze</li><li>**00200000** -nbstatus</li><li>**/Clear** : setzt den angegebenen Statistik Zählers auf NULL zurück.</li></ul> |

#### <a name="examples"></a>Beispiele

- [Beispiel 7: ](/previous-versions/windows/it-pro/windows-server-2003/cc784399(v=ws.10)#example-7-display-time-statistics-for-a-dns-server)

- [Beispiel 8: Anzeigen von nbstatus-Statistiken für einen DNS-Server](/previous-versions/windows/it-pro/windows-server-2003/cc784399(v=ws.10)#example-8-display-nbstatmem-statistics-for-a-dns-server)

## <a name="dnscmd-unenlistdirectorypartition-command"></a>dnscmd/unenlistdirectorypartition-Befehl

Entfernt den DNS-Server aus der Replikat Gruppe der angegebenen Verzeichnis Partition.

### <a name="syntax"></a>Syntax

```
dnscmd [<servername>] /unenlistdirectorypartition <partitionFQDN>
```

#### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| ---------- | ----------- |
| `<servername>` | Gibt den zu verwaltenden DNS-Server an, der durch die IP-Adresse, den FQDN oder den Hostnamen repräsentiert wird. Wenn dieser Parameter weggelassen wird, wird der lokale Server verwendet. |
| `<partitionFQDN>` | Der voll qualifizierte Name der DNS-Anwendungsverzeichnis Partition, die entfernt werden soll. |

## <a name="dnscmd-writebackfiles-command"></a>dnscmd/writebackfiles-Befehl

Hiermit wird der DNS-Server Arbeitsspeicher auf Änderungen überprüft und in den permanenten Speicher geschrieben. Mit dem Befehl " **Write Report Backfiles** " werden alle modifizierten Zonen oder eine angegebene Zone aktualisiert. Eine Zone ist geändert, wenn Änderungen im Speicher vorhanden sind, die noch nicht in den persistenten Speicher geschrieben wurden. Dies ist ein Vorgang auf Serverebene, mit dem alle Zonen überprüft werden. Sie können eine Zone in diesem Vorgang angeben, oder Sie können den **zonewrite-Back** -Vorgang verwenden.

### <a name="syntax"></a>Syntax

```
dnscmd [<servername>] /writebackfiles <zonename>
```

#### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| ---------- | ----------- |
| `<servername>` | Gibt den zu verwaltenden DNS-Server an, der durch die IP-Adresse, den FQDN oder den Hostnamen repräsentiert wird. Wenn dieser Parameter weggelassen wird, wird der lokale Server verwendet. |
| `<zonename>` | Gibt den Namen der zu aktualisierenden Zone an. |

#### <a name="examples"></a>Beispiele

```
dnscmd dnssvr1.contoso.com /writebackfiles
```

## <a name="dnscmd-zoneadd-command"></a>dnscmd/ZoneAdd-Befehl

Fügt dem DNS-Server eine Zone hinzu.

### <a name="syntax"></a>Syntax

```
dnscmd [<servername>] /zoneadd <zonename> <zonetype> [/dp <FQDN> | {/domain | enterprise | legacy}]
```

#### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| ---------- | ----------- |
| `<servername>` | Gibt den zu verwaltenden DNS-Server an, der durch die IP-Adresse, den FQDN oder den Hostnamen repräsentiert wird. Wenn dieser Parameter weggelassen wird, wird der lokale Server verwendet. |
| `<zonename>` | Gibt den Namen der Zone an. |
| `<zonetype>` | Gibt den Typ der zu erstellenden Zone an. Wenn Sie den Zonentyp **/Forwarder** oder **/DsForwarder** angeben, wird eine Zone erstellt, die eine bedingte Weiterleitung ausführt. Jeder Zonentyp verfügt über verschiedene erforderliche Parameter:<ul><li>**/DsPrimary** : erstellt eine integrierte Active Directory-Zone.</li><li>**/primary/file `<filename>` ** -Erstellt eine primäre Standard Zone und gibt den Namen der Datei an, in der die Zonen Informationen gespeichert werden.</li><li>**/Secondary `<masterIPaddress> [<masterIPaddress>...]` ** : Erstellt eine sekundäre Standard Zone.</li><li>**/Stub `<masterIPaddress> [<masterIPaddress>...]` /file `<filename>` ** -erstellt eine Datei gestützte Stubzone.</li><li>**/DsStub `<masterIPaddress> [<masterIPaddress>...]` ** -Erstellt eine Active Directory-integrierte Stub-Zone.</li><li>**/Forwarder `<masterIPaddress> [<masterIPaddress>]` .../file `<filename>` ** : gibt an, dass die erstellte Zone nicht aufgelöste Abfragen an einen anderen DNS-Server weiterleitet.</li><li>**/DsForwarder** : gibt an, dass die erstellte Active Directory Integrated Zone nicht aufgelöste Abfragen an einen anderen DNS-Server weiterleitet.</li></ul> |
| `<FQDN>` | Gibt den voll qualifizierten Namen der Verzeichnis Partition an. |
| /Domain | Speichert die Zone auf der Domänen Verzeichnis Partition. |
| /enterprise | Speichert die Zone in der Verzeichnis Partition des Unternehmens. |
| /legacy | Speichert die Zone auf einer Legacy-Verzeichnis Partition. |

#### <a name="examples"></a>Beispiele

```
dnscmd dnssvr1.contoso.com /zoneadd test.contoso.com /dsprimary
dnscmd dnssvr1.contoso.com /zoneadd secondtest.contoso.com /secondary 10.0.0.2
```

## <a name="dnscmd-zonechangedirectorypartition-command"></a>dnscmd/ZoneChangeDirectoryPartition-Befehl

Ändert die Verzeichnis Partition, in der sich die angegebene Zone befindet.

### <a name="syntax"></a>Syntax

```
dnscmd [<servername>] /zonechangedirectorypartition <zonename> {[<newpartitionname>] | [<zonetype>]}
```

#### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| ---------- | ----------- |
| `<servername>` | Gibt den zu verwaltenden DNS-Server an, der durch die IP-Adresse, den FQDN oder den Hostnamen repräsentiert wird. Wenn dieser Parameter weggelassen wird, wird der lokale Server verwendet. |
| `<zonename>` | Der voll qualifizierte Name der aktuellen Verzeichnis Partition, auf der sich die Zone befindet. |
| `<newpartitionname>` | Der FQDN der Verzeichnis Partition, in die die Zone verschoben wird. |
| `<zonetype>` | Gibt den Typ der Verzeichnis Partition an, in die die Zone verschoben wird. |
| /Domain | Verschiebt die Zone in die integrierte Domänen Verzeichnis Partition. |
| /forest | Verschiebt die Zone in die integrierte Gesamtstruktur-Verzeichnis Partition. |
| /legacy | Verschiebt die Zone in die Verzeichnis Partition, die für vorab Active Directory-Domänen Controller erstellt wurde. Diese Verzeichnis Partitionen sind für den einheitlichen Modus nicht erforderlich. |

## <a name="dnscmd-zonedelete-command"></a>dnscmd/ZoneDelete-Befehl

Löscht eine angegebene Zone.

### <a name="syntax"></a>Syntax

```
dnscmd [<servername>] /zonedelete <zonename> [/dsdel] [/f]
```

#### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| ---------- | ----------- |
| `<servername>` | Gibt den zu verwaltenden DNS-Server an, der durch die IP-Adresse, den FQDN oder den Hostnamen repräsentiert wird. Wenn dieser Parameter weggelassen wird, wird der lokale Server verwendet. |
| `<zonename>` | Gibt den Namen der zu löschenden Zone an. |
| /dsdel | Löscht die Zone aus den Azure-Verzeichnis Domänen Diensten (AD DS). |
| /f | Führt den Befehl aus, ohne zur Bestätigung aufzufordern. |

#### <a name="examples"></a>Beispiele

- [Beispiel 9: Löschen einer Zone von einem DNS-Server](/previous-versions/windows/it-pro/windows-server-2003/cc784399(v=ws.10)#example-9-delete-a-zone-from-a-dns-server)

## <a name="dnscmd-zoneexport-command"></a>dnscmd/zoneexport-Befehl

Erstellt eine Textdatei, die die Ressourcen Datensätze einer angegebenen Zone auflistet. Der **zoneexport** -Vorgang erstellt eine Datei mit Ressourcen Einträgen für eine integrierte Active Directory-Zone zu Problem Behandlungszwecken. Standardmäßig wird die Datei, die durch diesen Befehl erstellt wird, im DNS-Verzeichnis abgelegt. Dies ist standardmäßig das `%systemroot%/System32/Dns` Verzeichnis.

### <a name="syntax"></a>Syntax

```
dnscmd [<servername>] /zoneexport <zonename> <zoneexportfile>
```

#### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| ---------- | ----------- |
| `<servername>` | Gibt den zu verwaltenden DNS-Server an, der durch die IP-Adresse, den FQDN oder den Hostnamen repräsentiert wird. Wenn dieser Parameter weggelassen wird, wird der lokale Server verwendet. |
| `<zonename>` | Gibt den Namen der Zone an. |
| `<zoneexportfile>` | Gibt den Namen der zu erstellenden Datei an. |

#### <a name="examples"></a>Beispiele

- [Beispiel 10: Exportieren der Liste der Zonen Ressourcen Einträge in eine Datei](/previous-versions/windows/it-pro/windows-server-2003/cc784399(v=ws.10)#example-10-export-zone-resource-records-list-to-a-file)

## <a name="dnscmd-zoneinfo"></a>dnscmd/zoneinfo

Zeigt Einstellungen aus dem Abschnitt der Registrierung der angegebenen Zone an: `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\DNS\Parameters\Zones\<zonename>`

### <a name="syntax"></a>Syntax

```
dnscmd [<servername>] /zoneinfo <zonename> [<setting>]
```

#### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| ---------- | ----------- |
| `<servername>` | Gibt den zu verwaltenden DNS-Server an, der durch die IP-Adresse, den FQDN oder den Hostnamen repräsentiert wird. Wenn dieser Parameter weggelassen wird, wird der lokale Server verwendet. |
| `<zonename>` | Gibt den Namen der Zone an. |
| `<setting>` | Sie können einzeln eine beliebige Einstellung angeben, die vom **zoneinfo** -Befehl zurückgegeben wird. Wenn Sie keine Einstellung angeben, werden alle Einstellungen zurückgegeben. |

##### <a name="remarks"></a>Bemerkungen

- Verwenden Sie den **/Info** -Befehl, um Registrierungs Einstellungen auf Serverebene anzuzeigen.

- Eine Liste der Einstellungen, die Sie mit diesem Befehl anzeigen können, finden Sie unter dem **/config** -Befehl.

#### <a name="examples"></a>Beispiele

- [Beispiel 11: Anzeigen der Einstellung für das aktuaktuintervall aus der Registrierung](/previous-versions/windows/it-pro/windows-server-2003/cc784399(v=ws.10)#example-11-display-refreshinterval-setting-from-the-registry)

- [Beispiel 12: Anzeigen der Alterungs Einstellung aus der Registrierung](/previous-versions/windows/it-pro/windows-server-2003/cc784399(v=ws.10)#example-12-display-aging-setting-from-the-registry)

## <a name="dnscmd-zonepause-command"></a>dnscmd/zonepause-Befehl

Hält die angegebene Zone an, die dann Abfrage Anforderungen ignoriert.

### <a name="syntax"></a>Syntax

```
dnscmd [<servername>] /zonepause <zonename>
```

#### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| ---------- | ----------- |
| `<servername>` | Gibt den zu verwaltenden DNS-Server an, der durch die IP-Adresse, den FQDN oder den Hostnamen repräsentiert wird. Wenn dieser Parameter weggelassen wird, wird der lokale Server verwendet. |
| `<zonename>` | Gibt den Namen der Zone an, die angehalten werden soll. |

##### <a name="remarks"></a>Bemerkungen

- Verwenden Sie den **/zoneresume** -Befehl, um eine Zone fortzusetzen und verfügbar zu machen, nachdem Sie angehalten wurde.

#### <a name="examples"></a>Beispiele

```
dnscmd dnssvr1.contoso.com /zonepause test.contoso.com
```

## <a name="dnscmd-zoneprint-command"></a>dnscmd/zoneprint-Befehl

Listet die Datensätze in einer Zone auf.

### <a name="syntax"></a>Syntax

```
dnscmd [<servername>] /zoneprint <zonename>
```

#### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| ---------- | ----------- |
| `<servername>` | Gibt den zu verwaltenden DNS-Server an, der durch die IP-Adresse, den FQDN oder den Hostnamen repräsentiert wird. Wenn dieser Parameter weggelassen wird, wird der lokale Server verwendet. |
| `<zonename>` | Gibt den Namen der Zone an, die aufgelistet werden soll. |







## <a name="dnscmd-zonerefresh-command"></a>dnscmd/ZoneRefresh-Befehl

Erzwingt, dass eine sekundäre DNS-Zone aus der Masterzone aktualisiert wird.

### <a name="syntax"></a>Syntax

```
dnscmd [<servername>] /zonerefresh <zonename>
```

#### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| ---------- | ----------- |
| `<servername>` | Gibt den zu verwaltenden DNS-Server an, der durch die IP-Adresse, den FQDN oder den Hostnamen repräsentiert wird. Wenn dieser Parameter weggelassen wird, wird der lokale Server verwendet. |
| `<zonename>` | Gibt den Namen der zu aktualisierenden Zone an. |

##### <a name="remarks"></a>Bemerkungen

- Der **ZoneRefresh** -Befehl erzwingt eine Überprüfung der Versionsnummer im Ressourcen Daten Satz für den Start von Authority (Start of Authority, SOA) des Master Servers. Wenn die Versionsnummer auf dem Master Server höher ist als die Versionsnummer des sekundären Servers, wird eine Zonen Übertragung initiiert, die den sekundären Server aktualisiert. Wenn die Versionsnummer identisch ist, erfolgt keine Zonen Übertragung.

- Die erzwungene Überprüfung erfolgt standardmäßig alle 15 Minuten. Um den Standardwert zu ändern, verwenden Sie den `dnscmd config refreshinterval` Befehl.

#### <a name="examples"></a>Beispiele

```
dnscmd dnssvr1.contoso.com /zonerefresh test.contoso.com
```

## <a name="dnscmd-zonereload-command"></a>dnscmd/ZoneReload-Befehl

Kopiert Zonen Informationen aus der Quelle.

### <a name="syntax"></a>Syntax

```
dnscmd [<servername>] /zonereload <zonename>
```

#### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| ---------- | ----------- |
| `<servername>` | Gibt den zu verwaltenden DNS-Server an, der durch die IP-Adresse, den FQDN oder den Hostnamen repräsentiert wird. Wenn dieser Parameter weggelassen wird, wird der lokale Server verwendet. |
| `<zonename>` | Gibt den Namen der Zone an, die erneut geladen werden soll. |

##### <a name="remarks"></a>Bemerkungen

- Wenn die Zone in Active Directory integriert ist, wird Sie von Active Directory Domain Services (AD DS) erneut geladen.

- Wenn die Zone eine standardmäßig mit der Datei gesicherte Zone ist, wird Sie aus einer Datei geladen.

#### <a name="examples"></a>Beispiele

```
dnscmd dnssvr1.contoso.com /zonereload test.contoso.com
```

## <a name="dnscmd-zoneresetmasters-command"></a>dnscmd/ZoneResetMasters-Befehl

Setzt die IP-Adressen des Master Servers zurück, der Zonen Übertragungs Informationen für eine sekundäre Zone bereitstellt.

### <a name="syntax"></a>Syntax

```
dnscmd [<servername>] /zoneresetmasters <zonename> [/local] [<IPaddress> [<IPaddress>]...]
```

#### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| ---------- | ----------- |
| `<servername>` | Gibt den zu verwaltenden DNS-Server an, der durch die IP-Adresse, den FQDN oder den Hostnamen repräsentiert wird. Wenn dieser Parameter weggelassen wird, wird der lokale Server verwendet. |
| `<zonename>` | Gibt den Namen der zurück zusetzenden Zone an. |
| /local ein | Legt eine lokale Masterliste fest. Dieser Parameter wird für in Active Directory integrierte Zonen verwendet. |
| `<IPaddress>` | Die IP-Adressen der Master Server der sekundären Zone. |

##### <a name="remarks"></a>Bemerkungen

- Dieser Wert wird ursprünglich festgelegt, wenn die sekundäre Zone erstellt wird. Verwenden Sie den **ZoneResetMasters** -Befehl auf dem sekundären Server. Dieser Wert hat keine Auswirkung, wenn er auf dem DNS-Master Server festgelegt ist.

#### <a name="examples"></a>Beispiele

```
dnscmd dnssvr1.contoso.com /zoneresetmasters test.contoso.com 10.0.0.1
dnscmd dnssvr1.contoso.com /zoneresetmasters test.contoso.com /local
```

## <a name="dnscmd-zoneresetscavengeservers-command"></a>dnscmd/ZoneResetScavengeServers-Befehl

Ändert die IP-Adressen der Server, die die angegebene Zone abspülen können.

### <a name="syntax"></a>Syntax

```
dnscmd [<servername>] /zoneresetscavengeservers <zonename> [/local] [<IPaddress> [<IPaddress>]...]
```

#### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| ---------- | ----------- |
| `<servername>` | Gibt den zu verwaltenden DNS-Server an, der durch die IP-Adresse, den FQDN oder den Hostnamen repräsentiert wird. Wenn dieser Parameter weggelassen wird, wird der lokale Server verwendet. |
| `<zonename>` | Gibt die zu Scavenge Zone an. |
| /local ein | Legt eine lokale Masterliste fest. Dieser Parameter wird für in Active Directory integrierte Zonen verwendet. |
| `<IPaddress>` | Listet die IP-Adressen der Server auf, die das Scavenge ausführen können. Wenn dieser Parameter weggelassen wird, kann er von allen Servern, auf denen diese Zone gehostet wird, herunterskaliert werden. |

##### <a name="remarks"></a>Bemerkungen

- Standardmäßig kann diese Zone von allen Servern, die eine Zone hosten, skaliert werden.

- Wenn eine Zone auf mehreren DNS-Servern gehostet wird, können Sie mit diesem Befehl die Häufigkeit verringern, mit der eine Zone bereinigt wird.

- Das Scavenging muss auf dem DNS-Server und der Zone aktiviert werden, die von diesem Befehl betroffen sind.

#### <a name="examples"></a>Beispiele

```
dnscmd dnssvr1.contoso.com /zoneresetscavengeservers test.contoso.com 10.0.0.1 10.0.0.2
```

## <a name="dnscmd-zoneresetsecondaries-command"></a>dnscmd/zoneresetsecondaries-Befehl

Gibt eine Liste von IP-Adressen sekundärer Server an, auf die ein Master Server reagiert, wenn er nach einer Zonen Übertragung gefragt wird.

### <a name="syntax"></a>Syntax

```
dnscmd [<servername>] /zoneresetsecondaries <zonename> {/noxfr | /nonsecure | /securens | /securelist <securityIPaddresses>} {/nonotify | /notify | /notifylist <notifyIPaddresses>}
```

#### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| ---------- | ----------- |
| `<servername>` | Gibt den zu verwaltenden DNS-Server an, der durch die IP-Adresse, den FQDN oder den Hostnamen repräsentiert wird. Wenn dieser Parameter weggelassen wird, wird der lokale Server verwendet. |
| `<zonename>` | Gibt den Namen der Zone an, deren sekundäre Server zurückgesetzt werden sollen. |
| /local ein | Legt eine lokale Masterliste fest. Dieser Parameter wird für in Active Directory integrierte Zonen verwendet. |
| /noxfr | Gibt an, dass keine Zonenübertragungen zulässig sind. |
| /nonsecure | Gibt an, dass alle Zonen Übertragungsanforderungen erteilt werden. |
| /securens | Gibt an, dass nur der Server, der im Namen Server (NS)-Ressourcen Eintrag für die Zone aufgeführt ist, übertragen wird. |
| /securelist | Gibt an, dass Zonenübertragungen nur der Liste der Server erteilt werden. Auf diesen Parameter muss eine IP-Adresse oder Adressen folgen, die der Master Server verwendet. |
| `<securityIPaddresses>` | Listet die IP-Adressen auf, die Zonenübertragungen vom Master Server empfangen. Dieser Parameter wird nur mit dem **/Securelist** -Parameter verwendet. |
| /nonotify | Gibt an, dass keine Änderungs Benachrichtigungen an sekundäre Server gesendet werden. |
| /notify | Gibt an, dass Änderungs Benachrichtigungen an alle sekundären Server gesendet werden. |
| /notifylist | Gibt an, dass Änderungs Benachrichtigungen nur an die Liste der Server gesendet werden. Auf diesen Befehl muss eine IP-Adresse oder Adressen folgen, die der Master Server verwendet. |
| `<notifyIPaddresses>` | Gibt die IP-Adressen der sekundären Server oder Server an, an die Änderungs Benachrichtigungen gesendet werden. Diese Liste wird nur mit dem **/NotifyList** -Parameter verwendet. |

##### <a name="remarks"></a>Bemerkungen

- Geben Sie mit dem Befehl **zoneresetsecon-** Replikate auf dem Master Server an, wie er auf Zonen Übertragungsanforderungen von sekundären Servern reagiert.

#### <a name="examples"></a>Beispiele

```
dnscmd dnssvr1.contoso.com /zoneresetsecondaries test.contoso.com /noxfr /nonotify
dnscmd dnssvr1.contoso.com /zoneresetsecondaries test.contoso.com /securelist 11.0.0.2
```

## <a name="dnscmd-zoneresettype-command"></a>dnscmd/ZoneResetType-Befehl

Ändert den Typ der Zone.

### <a name="syntax"></a>Syntax

```
dnscmd [<servername>] /zoneresettype <zonename> <zonetype> [/overwrite_mem | /overwrite_ds]
```

#### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| ---------- | ----------- |
| `<servername>` | Gibt den zu verwaltenden DNS-Server an, der durch die IP-Adresse, den FQDN oder den Hostnamen repräsentiert wird. Wenn dieser Parameter weggelassen wird, wird der lokale Server verwendet. |
| `<zonename>` | Identifiziert die Zone, in der der Typ geändert wird. |
| `<zonetype>` | Gibt den Typ der zu erstellenden Zone an. Jeder Typ verfügt über verschiedene erforderliche Parameter, einschließlich:<ul><li>**/DsPrimary** : erstellt eine integrierte Active Directory-Zone.</li><li>**/primary/file `<filename>` ** : Erstellt eine primäre Standard Zone.</li><li>**/Secondary `<masterIPaddress> [,<masterIPaddress>...]` ** : Erstellt eine sekundäre Standard Zone.</li><li>**/Stub `<masterIPaddress>[,<masterIPaddress>...]` /file `<filename>` ** -erstellt eine Datei gestützte Stubzone.</li><li>**/DsStub `<masterIPaddress>[,<masterIPaddress>...]` ** -Erstellt eine Active Directory-integrierte Stub-Zone.</li><li>**/Forwarder `<masterIPaddress[,<masterIPaddress>]` .../file `<filename>` ** : gibt an, dass die erstellte Zone nicht aufgelöste Abfragen an einen anderen DNS-Server weiterleitet.</li><li>**/DsForwarder** : gibt an, dass die erstellte Active Directory Integrated Zone nicht aufgelöste Abfragen an einen anderen DNS-Server weiterleitet.</li></ul> |
| /OverWrite_Mem | Überschreibt DNS-Daten aus Daten in AD DS. |
| /OverWrite_Ds | Überschreibt vorhandene Daten in AD DS. |

##### <a name="remarks"></a>Bemerkungen

- Wenn Sie den Zonentyp auf **/DsForwarder** festlegen, wird eine Zone erstellt, die bedingte Weiterleitung ausführt.

#### <a name="examples"></a>Beispiele

```
dnscmd dnssvr1.contoso.com /zoneresettype test.contoso.com /primary /file test.contoso.com.dns
dnscmd dnssvr1.contoso.com /zoneresettype second.contoso.com /secondary 10.0.0.2
```

## <a name="dnscmd-zoneresume-command"></a>dnscmd/zoneresume-Befehl

Startet eine angegebene Zone, die zuvor angehalten wurde.

### <a name="syntax"></a>Syntax

```
dnscmd [<servername>] /zoneresume <zonename>
```

#### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| ---------- | ----------- |
| `<servername>` | Gibt den zu verwaltenden DNS-Server an, der durch die IP-Adresse, den FQDN oder den Hostnamen repräsentiert wird. Wenn dieser Parameter weggelassen wird, wird der lokale Server verwendet. |
| `<zonename>` | Gibt den Namen der fort zusetzenden Zone an. |

##### <a name="remarks"></a>Bemerkungen

- Mit diesem Vorgang können Sie einen Neustart des **/zonepause** -Vorgangs durchführen.

#### <a name="examples"></a>Beispiele

```
dnscmd dnssvr1.contoso.com /zoneresume test.contoso.com
```

## <a name="dnscmd-zoneupdatefromds-command"></a>dnscmd/ZoneUpdateFromDs-Befehl

Aktualisiert die angegebene Active Directory-integrierte Zone von AD DS.

### <a name="syntax"></a>Syntax

```
dnscmd [<servername>] /zoneupdatefromds <zonename>
```

#### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| ---------- | ----------- |
| `<servername>` | Gibt den zu verwaltenden DNS-Server an, der durch die IP-Adresse, den FQDN oder den Hostnamen repräsentiert wird. Wenn dieser Parameter weggelassen wird, wird der lokale Server verwendet. |
| `<zonename>` | Gibt den Namen der zu aktualisierenden Zone an. |

##### <a name="remarks"></a>Bemerkungen

- In Active Directory integrierte Zonen wird dieses Update standardmäßig alle fünf Minuten durchgeführt. Verwenden Sie den-Befehl, um diesen Parameter zu ändern `dnscmd config dspollinginterval` .

#### <a name="examples"></a>Beispiele

```
dnscmd dnssvr1.contoso.com /zoneupdatefromds
```

## <a name="dnscmd-zonewriteback-command"></a>dnscmd/zonewriteback-Befehl

Überprüft den DNS-Server Arbeitsspeicher auf Änderungen, die für eine bestimmte Zone relevant sind, und schreibt diese in den persistenten Speicher.

### <a name="syntax"></a>Syntax

```
dnscmd [<servername>] /zonewriteback <zonename>
```

#### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| ---------- | ----------- |
| `<servername>` | Gibt den zu verwaltenden DNS-Server an, der durch die IP-Adresse, den FQDN oder den Hostnamen repräsentiert wird. Wenn dieser Parameter weggelassen wird, wird der lokale Server verwendet. |
| `<zonename>` | Gibt den Namen der zu aktualisierenden Zone an. |

##### <a name="remarks"></a>Bemerkungen

- Dies ist ein Vorgang auf Zonenebene. Sie können alle Zonen auf einem DNS-Server mithilfe des **/writebackfiles** -Vorgangs aktualisieren.

#### <a name="examples"></a>Beispiele

```
dnscmd dnssvr1.contoso.com /zonewriteback test.contoso.com
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
