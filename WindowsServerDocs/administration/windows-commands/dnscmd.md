---
title: dnscmd
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e7f31cb5-a426-4e25-b714-88712b8defd5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 39478e9b7dd8e8c69ed07f5d431486a7ed96b9cb
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59815501"
---
# <a name="dnscmd"></a>dnscmd

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Eine Befehlszeilenschnittstelle zum Verwalten von DNS-Server. Dieses Dienstprogramm ist nützlich bei der Skripterstellung von Batchdateien, die zum Automatisieren von Routineaufgaben für DNS-Verwaltung oder um unbeaufsichtigtes Setup und Konfiguration des neuen DNS-Server in Ihrem Netzwerk durchzuführen.  
## <a name="syntax"></a>Syntax  
```  
dnscmd <ServerName> <command> [<command parameters>]  
```  
## <a name="parameters"></a>Parameter  
|Parameter|Beschreibung|  
|-------|--------|  
|<ServerName>|Der IP-Adresse oder Hostname Name eines Remote- oder lokalen DNS-Servers.|  
## <a name="commands"></a>Befehle  
|Befehl|Beschreibung|  
|------|--------|  
|[dnscmd /ageallrecords](#BKMK_1)|Legt die aktuelle Uhrzeit für alle Zeitstempel in einer Zone oder Knoten fest.|  
|[dnscmd /clearcache](#BKMK_2)|Löscht den Cache des DNS-Server.|  
|[dnscmd /config](#BKMK_3)|setzt die DNS-Server oder die Zone Konfiguration zurück.|  
|[dnscmd /createbuiltindirectorypartitions](#BKMK_4)|erstellt die integrierten DNS-Anwendungsverzeichnispartitionen.|  
|[dnscmd /createdirectorypartition](#BKMK_5)|erstellt eine DNS-Anwendungsverzeichnispartition.|  
|[dnscmd /deletedirectorypartition](#BKMK_6)|Löscht eine DNS-Anwendungsverzeichnispartition.|  
|[dnscmd /directorypartitioninfo](#BKMK_7)|Listet Informationen zu einer DNS-Anwendungsverzeichnispartition.|  
|[dnscmd /enlistdirectorypartition](#BKMK_8)|Fügt einen DNS-Server auf die Replikation eine DNS-Anwendungsverzeichnispartition.|  
|[dnscmd /enumdirectorypartitions](#BKMK_9)|Listet für einen Server der DNS-Anwendungsverzeichnispartitionen.|  
|[dnscmd /enumrecords](#BKMK_10)|Listet die Ressourceneinträge in einer Zone.|  
|[dnscmd /enumzones](#BKMK_11)|Listet die Zonen, die von dem angegebenen Server gehostet wird.|  
|[dnscmd /exportsettings](#BKMK_25a)|Schreibt Informationen zur Serverkonfiguration in eine Textdatei.|  
|[dnscmd /info](#BKMK_12)|Ruft die Serverinformationen ab.|  
|[dnscmd /ipvalidate](#BKMK_29a)|Remote-DNS-Server wird überprüft.|  
|[dnscmd /nodedelete](#BKMK_13)|Löscht alle Datensätze für einen Knoten in einer Zone.|  
|[dnscmd /recordadd](#BKMK_14)|Fügt einen Ressourceneintrag für eine Zone hinzu.|  
|[dnscmd /recorddelete](#BKMK_15)|Entfernt einen Ressourceneintrag aus einer Zone.|  
|[dnscmd /resetforwarders](#BKMK_16)|Legt die DNS-Server zum Weiterleiten von rekursiven Abfragen.|  
|[dnscmd /resetlistenaddresses](#BKMK_17)|Legt fest, die IP-Serveradressen, DNS-Anforderungen verarbeiten.|  
|[dnscmd /startscavenging](#BKMK_18)|Initiiert die Server durch eine Bereinigung.|  
|[dnscmd /statistics](#BKMK_19)|Abfragen, oder löscht die Daten für Server-Statistiken.|  
|[dnscmd /unenlistdirectorypartition](#BKMK_20)|Entfernt einen DNS-Server aus dem eine Anwendungsverzeichnispartition in DNS-Replikation.|  
|[dnscmd /writebackfiles](#BKMK_21)|Speichert alle Daten für Zone oder Root-Hinweis in einer Datei an.|  
|[dnscmd /zoneadd](#BKMK_22)|erstellt eine neue Zone auf dem DNS-Server an.|  
|[dnscmd /zonechangedirectorypartition](#BKMK_23)|Ändert die Verzeichnispartition, der auf der eine Zone befindet.|  
|[dnscmd /zonedelete](#BKMK_24)|Löscht eine Zone aus der DNS-Server an.|  
|[dnscmd /zoneexport](#BKMK_25)|Schreibt die Ressourceneinträge der Zone in eine Textdatei.|  
|[dnscmd /zoneinfo](#BKMK_26)|Zeigt Zoneninformationen an.|  
|[dnscmd /zonepause](#BKMK_27)|hält eine Zone an.|  
|[dnscmd /zoneprint](#BKMK_28)|Zeigt alle Datensätze in der Zone.|  
|[dnscmd /zonerefresh](#BKMK_30)|Erzwingt eine Aktualisierung der sekundären Zone aus der master-Zone.|  
|[dnscmd /zonereload](#BKMK_31)|Lädt eine Zone aus seiner Datenbank.|  
|[dnscmd /zoneresetmasters](#BKMK_32)|Ändert den Masterservern, die Zone Übertragung-Informationen für eine sekundäre Zone bereitzustellen.|  
|[dnscmd /zoneresetscavengeservers](#BKMK_33)|Ändert die Server, die eine Zone Aufräumen können.|  
|[dnscmd /zoneresetsecondaries](#BKMK_34)|setzt die sekundären Informationen für eine Zone zurück.|  
|[dnscmd /zoneresettype](#BKMK_29)|Ändert den Zonentyp.|  
|[dnscmd /zoneresume](#BKMK_35)|Setzt eine Zone an.|  
|[dnscmd /zoneupdatefromds](#BKMK_36)|Aktualisiert eine active Directory integrierte Zone mit Daten aus active Directory-Domänendienste (AD DS).|  
|[dnscmd /zonewriteback](#BKMK_37)|Speichert Zonendaten in einer Datei an.|  
### <a name="BKMK_1"></a>dnscmd /ageallrecords  
Legt die aktuelle Uhrzeit auf einem Zeitstempel-Ressourceneinträge bei einer bestimmten Zone oder Knoten auf einen DNS-Server fest.  
#### <a name="syntax"></a>Syntax  
```  
dnscmd [<ServerName>] /ageallrecords <ZoneName>[<NodeName>] | [/tree]|[/f]  
```  
#### <a name="parameters"></a>Parameter  
<ServerName>  
Gibt an, den DNS-Server, den der Administrator plant, für die Verwaltung, dargestellt durch IP-Adresse, vollqualifizierten Domänennamen (FQDN) oder Hostnamen. Wenn dieser Parameter ausgelassen wird, wird der lokale Server verwendet.  
<ZoneName>  
Gibt den FQDN der Zone.  
<NodeName>  
Gibt einen bestimmten Knoten oder eine Teilstruktur in der Zone an. *NodeName* gibt die Knoten oder eine Teilstruktur in der Zone mit dem folgenden an:  
-   @ für Stammzone oder FQDN  
-   Der FQDN eines Knotens (der Name mit einem Punkt (.) am Ende)  
-   Einer einzelnen Beschriftung für den Namen relativ zum Zonenstamm  
/Tree  
Gibt an, dass alle untergeordneten Knoten auch den Zeitstempel erhalten.  
/f  
Führt den Befehl ohne Aufforderung zur Bestätigung an.  
#### <a name="remarks"></a>Hinweise  
-   Die **Ageallrecords** Befehl bezieht sich auf die Abwärtskompatibilität zwischen der aktuellen Version von DNS und früheren Versionen von DNS in der altern und Aufräumen nicht unterstützt wurden. Einen Zeitstempel mit der aktuellen Zeit Ressourceneinträge, die nicht über einen Zeitstempel verfügen hinzugefügt, und wird die aktuelle Uhrzeit auf Ressourceneinträge, die einen Zeitstempel verfügen.  
-   Eintragsbereinigung wird nicht ausgeführt werden, es sei denn, die Datensätze mit einem Zeitstempel versehenen sind. Namenserver (NS)-Ressourceneinträge, Anfang Ressourceneinträge für Autoritätsursprung (SOA), und Windows Internet Name Service (WINS)-Ressourceneinträge in Aufräumvorgang nicht enthalten sind und sie sind nicht mit einem Zeitstempel versehenen, auch wenn die **Ageallrecords**-Befehl ausgeführt wird.  
-   Dieser Befehl schlägt fehl, es sei denn, die durch eine Bereinigung für den DNS-Server und die Zone aktiviert ist. Informationen zum Aktivieren der Aufräumvorgang für die Zone, finden Sie unter den **Alterung** Parameter unter auf Zonenebene-Syntax in der [Config](#BKMK_3) Befehl.  
-   Das Hinzufügen von nach dem Zeitstempel auf DNS-Ressourceneinträge sind sie nicht kompatibel mit DNS-Servern, die auf anderen Betriebssystemen als Windows 2000, Windows XP oder Windows Server 2003 ausgeführt. Nach dem Zeitstempel, die Sie hinzufügen, indem Sie mit der **Ageallrecords** Befehl kann nicht rückgängig gemacht.  
-   Wenn keine optionalen Parameter angegeben wurde, gibt der Befehl alle Ressourceneinträge auf dem angegebenen Knoten zurück. Wenn ein Wert, für mindestens eine optionale Parameter angegeben wird **Dnscmd** Listet nur die Ressourceneinträge, die entsprechen den oder die Werte, die in den oder die optionalen Parameter angegeben werden.  
#### <a name="example"></a>Beispiel  
Finden Sie unter [Beispiel 1: Legen Sie die aktuelle Zeit auf einen Zeitstempel, Ressourceneinträge](https://technet.microsoft.com/library/cc784399(v=ws.10).aspx).  
### <a name="BKMK_2"></a>dnscmd /clearcache  
Löscht den Cachespeicher DNS-Ressourceneinträge für den angegebenen DNS-Server an.  
#### <a name="syntax"></a>Syntax  
```  
dnscmd [<ServerName>] /clearcache  
```  
#### <a name="parameters"></a>Parameter  
<ServerName>  
Gibt an, den DNS-Server für die Verwaltung, durch die IP-Adresse, den FQDN oder Hostnamen dargestellt wird. Wenn dieser Parameter ausgelassen wird, wird der lokale Server verwendet.  
#### <a name="sample-usage"></a>Beispiel für die Verwendung  
`dnscmd dnssvr1.contoso.com /clearcache`  
### <a name="BKMK_3"></a>dnscmd /config  
Ändert die Werte in der Registrierung für die DNS-Server und eine einzelne Zonen. Akzeptiert Einstellungen für die auf Serverebene und auf Zonenebene.  
> [!CAUTION]  
> Bearbeiten Sie die Registrierung nicht direkt auf, es sei denn, es unbedingt erforderlich. Die Registrierungs-Editor umgehen Sie standardmäßige Schutzvorrichtungen, können die Einstellungen, die die Leistung beeinträchtigen, Schäden am System oder selbst müssen Sie Windows neu installieren können. Sie können die meisten registrierungseinstellungen für die sicher ändern, indem Sie die Programme in der Systemsteuerung oder Microsoft Management Console (Mmc). Wenn Sie die Registrierung direkt bearbeiten müssen, Sichern sie Sie vorher. Lesen Sie den Registrierungs-Editor-Hilfe für Weitere Informationen.  
#### <a name="server-level-syntax"></a>Auf Serverebene-syntax  
```  
dnscmd [<ServerName>] /config <Parameter>  
```  
#### <a name="dnscmd-config"></a>dnscmd /config  
Ändert die Konfiguration des angegebenen Servers.  
#### <a name="parameters"></a>Parameter  
<ServerName>  
Gibt den DNS-Server, den Sie verwalten möchten, die durch die Syntax für lokalen Computer, IP-Adresse, FQDN oder Hostnamen dargestellt wurden. Wenn dieser Parameter ausgelassen wird, wird der lokale Server verwendet.  
<Parameter>  
Geben Sie eine Einstellung und, optional einen Wert. Parameterwerte mit der folgenden Syntax: *Parameter* [*Wert*]  
Die folgenden Parameterwerte werden im weiteren Verlauf dieses Abschnitts beschrieben:  
-   **/addressanswerlimit**  
-   **/bindsecondaries**  
-   **/bootmethod**  
-   **/defaultagingstate**  
-   **/defaultnorefreshinterval**  
-   **/defaultrefreshinterval**  
-   **/disableautoreversezones**  
-   **/disablensrecordsautocreation**  
-   **/dspollinginterval**  
-   **/dstombstoneinterval**  
-   **/ednscachetimeout**  
-   **/enablednsprobes**  
-   **/enablednssec**  
-   **/enableglobalnamessupport**  
-   **/enableglobalqueryblocklist**  
-   **/eventloglevel**  
-   **/forwarddelegations**  
-   **/forwardingtimeout**  
-   **/globalnamesqueryorder**  
-   **/globalqueryblocklist**  
-   **/isslave**  
-   **/localnetpriority**  
-   **/logfilemaxsize**  
-   **/logfilepath**  
-   **/logipfilterlist**  
-   **/loglevel**  
-   **/maxcachesize**  
-   **/maxcachettl**  
-   **/namecheckflag**  
-   **/notcp**  
-   **/norecursion**  
-   **/recursionretry**  
-   **/recursiontimeout**  
-   **/roundrobin**  
-   **/rpcprotocol**  
-   **/scavenginginterval**  
-   **/secureresponses**  
-   **/sendport**  
-   **/strictfileparsing**  
-   **/updateoptions**  
-   **/writeauthorityns**  
-   **/xfrconnecttimeout**  
**/addressanswerlimit [0|5-28]**  
Gibt die maximale Anzahl von Hosteinträgen, die ein DNS-Server als Reaktion auf eine Abfrage senden kann. Der Wert kann 0 (null) sein, oder es kann sein, im Bereich von 5 bis 28 Einträge. Der Standardwert ist 0 (null).  
**/bindsecondaries[0|1]**  
Ändert das Format der zonenübertragung, sodass es eine maximale Komprimierung und Effizienz erzielen kann. Dieses Format ist jedoch nicht kompatibel mit früheren Versionen der Berkeley Internet Name Domain (BIND).  
**0**  
Verwendet die maximale Komprimierung. Dieses Format ist kompatibel mit BIND-Versionen 4.9.4 oder neuer.  
**1**  
Sendet nur ein Eintrag pro Nachricht, die auf Microsoft DNS - Server an. Dieses Format ist mit früheren Versionen BINDUNG als 4.9.4 kompatibel. Dies ist die Standardeinstellung.  
**/bootmethod[0|1|2|3]**  
Bestimmt die Quelle, aus der der DNS-Server seine Konfigurationsinformationen abruft.  
**0**  
Löscht die Quelle der Informationen zur Konfiguration.  
**1**  
Laden aus der BIND-Datei, die im DNS-Verzeichnis %systemroot%\System32\DNS in der Standardeinstellung wird befindet.  
**2**  
Laden aus der Registrierung.  
**3**  
Lädt von AD DS und der Registrierung. Dies ist die Standardeinstellung.  
**/defaultagingstate[0|1]**  
Bestimmt, ob die aufräumeinstellungen DNS-Funktion, wird standardmäßig auf den neu erstellten Zonen aktiviert ist.  
**0**  
Deaktiviert die durch eine Bereinigung. Dies ist die Standardeinstellung.  
**1**  
Ermöglicht, die durch eine Bereinigung.  
**/ DefaultNoRefreshInterval [0 x 1-0xFFFFFFFF | 0xA8]**  
Legt einen Zeitraum in denen keine Aktualisierungen akzeptiert werden für die dynamisch aktualisierten Datensätze fest. Dieser Wert wird automatisch von Zonen auf dem Server geerbt. Um den Standardwert zu ändern, geben Sie einen Wert im Bereich von **0 x 1-0xFFFFFFFF**. Der Standardwert des Servers ist **0xA8**.  
**/ DefaultRefreshInterval [0 x 1-0xFFFFFFFF | 0xA8]**  
Legt eine bestimmte Zeitspanne, die für dynamische Updates von DNS-Einträgen zulässig ist. Dieser Wert wird automatisch von Zonen auf dem Server geerbt. Um den Standardwert zu ändern, geben Sie einen Wert im Bereich von **0 x 1-0xFFFFFFFF**. Der Standardwert des Servers ist **0xA8**.  
**/disableautoreversezones [0 | 1]**  
Aktiviert oder deaktiviert die automatische Erstellung von reverse-Lookupzonen. Reverse-Lookupzonen bieten die Auflösung von IP (Internet Protocol)-Adressen in DNS-Domänennamen.  
**0**  
Ermöglicht die automatische Erstellung von reverse-Lookupzonen. Dies ist die Standardeinstellung.  
**1**  
Deaktiviert die automatische Erstellung von reverse-Lookupzonen.  
**/disablensrecordsautocreation {0|1}**  
Gibt an, ob der DNS-Server automatisch Namenserver (NS)-Ressourceneinträge für Zonen erstellt, die darunter gehostet.  
**0**  
Erstellt automatisch Namenserver (NS)-Ressourceneinträgen für Zonen, die den DNS-Server-Hosts.  
**1**  
Erstellt nicht automatisch Namenserver (NS)-Ressourceneinträgen für Zonen, die den DNS-Server-Hosts.  
**/dspollinginterval 0 bis 30**  
Gibt an, wie oft die DNS-Abfragen von AD DS auf Änderungen in active Directory Zonen integriert.  
**/dstombstoneinterval [1-30]**  
Die Zeitspanne in Sekunden, gelöschte Datensätze in AD DS beibehalten werden sollen.  
**/ EDNSCacheTimeout [<seconds>]**  
Gibt die Anzahl der Sekunden, die Informationen der erweiterten (DNS, EDNS) zwischengespeichert werden. Der minimale Wert beträgt 3600, und der maximale Wert beträgt 15,724,800. Der Standardwert ist 604.800 Sekunden (eine Woche).  
**enableednsprobes {0 | 1}**  
Aktiviert oder deaktiviert den Server zum Überprüfen von anderen Servern, um festzustellen, ob sie EDNS unterstützen.  
**0**  
Deaktiviert die active-Unterstützung für EDNS-Tests.  
**1**  
Aktiviert die active Unterstützung für EDNS-Tests.  
**/enablednssec {0|1}**  
Aktiviert oder deaktiviert die Unterstützung für DNS-Sicherheitserweiterungen (DNSSEC).  
**0**  
DNSSEC wird deaktiviert.  
**1**  
Ermöglicht die DNSSEC.  
**/enableglobalnamessupport {0|1}**  
Aktiviert oder deaktiviert die Unterstützung für die GlobalNames-Zone. Die GlobalNames-Zone unterstützt eine Auflösung von einteiligen DNS-Namen innerhalb der Gesamtstruktur.  
**0**  
Deaktiviert die Unterstützung für die GlobalNames-Zone. Beim Festlegen des Wert dieses Befehls auf **0**, einfache Bezeichnungen in der GlobalNames-Zone wird von der DNS-Serverdienst nicht aufgelöst.  
**1**  
Aktiviert die Unterstützung für die GlobalNames-Zone. Beim Festlegen des Wert dieses Befehls auf **1**, der DNS-Server-Dienst löst einteilige Namen in der GlobalNames-Zone.  
**/enableglobalqueryblocklist {0|1}**  
Aktiviert oder deaktiviert die Unterstützung für die globale Abfragesperrliste, die namensauflösung für Namen in der Liste blockiert. Der DNS-Serverdienst erstellt und beim Starten des Diensts beim ersten verwenden die globalen Abfragesperrliste sind standardmäßig aktiviert. Verwenden Sie zum Anzeigen der aktuellen globalen Abfragesperrliste der **Dnscmd/Info GlobalQueryBlockList** Befehl.  
**0**  
Deaktiviert die Unterstützung für die globale Abfragesperrliste. Beim Festlegen des Wert dieses Befehls auf **0**, antwortet der DNS-Server-Dienst, um Abfragen nach Namen in der Liste.  
**1**  
Aktiviert die Unterstützung für die globale Abfragesperrliste. Beim Festlegen des Wert dieses Befehls auf **1**, um Abfragen nach Namen in der Liste der DNS-Serverdienst nicht reagiert.  
**/EventlogLevel [0 | 1 | 2 | 4]**  
Bestimmt, welche Ereignisse im DNS-Server-Protokoll in der Ereignisanzeige protokolliert werden.  
**0**  
Protokolliert keine Ereignisse an.  
**1**  
Nur Fehler protokolliert.  
**2**  
Nur Fehler und Warnungen protokolliert.  
**4**  
Protokolliert Fehler, Warnungen und Informationsereignisse. Dies ist die Standardeinstellung.  
**/forwarddelegations [0 | 1]**  
Bestimmt, wie der DNS-Server eine Abfrage für eine delegierte Teilzone behandelt. Diese Abfragen können entweder die Teilzone, die in der Abfrage bezeichnet wird, oder der Liste der Weiterleitungen mit dem Namen gesendet werden, für den DNS-Server. Nur wenn Weiterleitung aktiviert ist, werden Einträge in der Einstellung verwendet.  
**0**  
Abfragen, die delegierte untergeordnete Zonen auf den entsprechenden Teilzone verweisen, automatisch gesendet. Dies ist die Standardeinstellung.  
**1**  
leitet Abfragen, die auf die delegierte Teilzone an die die vorhandenen Weiterleitungen verweisen.  
**/ForwardingTimeout [<seconds>]**  
Bestimmt, wie viele Sekunden (0 x 1-0xFFFFFFFF) ein DNS-Server für eine Weiterleitung zu reagieren, bevor Sie versuchen, eine andere Weiterleitung wartet. Der Standardwert ist **0 x 5**, d.h. auf 5 Sekunden.  
**/globalneamesqueryorder** {**0|1**}  
Gibt an, ob der DNS-Server-Dienst zuerst in der GlobalNames-Zone oder lokalen Zonen sucht bei der namensauflösung.  
**0**  
Der DNS-Server-Dienst versucht, Auflösen von Namen durch Abfragen der GlobalNames-Zone aus, bevor die Zonen abgefragt, die für die er autorisierend ist.  
**1**  
Der DNS-Server-Dienst versucht, Auflösen von Namen durch Abfragen der Zones, die für die er autorisierend ist vor dem Abfragen der GlobalNames-Zone.  
**GlobalQueryBlockList [[<name> [<name>]...]**  
ersetzt die aktuelle globale Abfragesperrliste mit einer Liste mit den Namen, die Sie angeben. Wenn Sie keinen Namen angeben, löscht dieser Befehl die Liste der Blöcke an. Standardmäßig enthält die globalen Abfragesperrliste die folgenden Elemente:  
-   isatap  
-   WPAD  
Der DNS-Serverdienst kann entfernen Sie eine oder beide dieser Namen beim ersten Mal starten, wenn sie diese Namen in einer vorhandenen Zone findet.  
**/IsSlave [0 | 1]**  
Bestimmt, wie der DNS-Server reagiert, wenn Abfragen, die es leitet keine Antwort erhalten.  
**0**  
Gibt an, dass der DNS-Server nicht untergeordnet ist (auch bekannt als eine *Slave*). Wenn die Weiterleitung nicht antwortet, versucht der DNS-Server ab, die Abfrage selbst aufzulösen. Dies ist die Standardeinstellung.  
**1**  
Gibt an, dass der DNS-Server eine Unterordnung ist. Wenn die Weiterleitung nicht antwortet, wird der DNS-Server beendet die Suche und sendet eine Fehlermeldung an den Resolver.  
**/localnetpriority [0 | 1]**  
Bestimmt die Reihenfolge, in der Hosteinträge zurückgegeben werden, wenn der DNS-Server mehrfach-Hosteinträge für denselben Namen hat.  
**0**  
Gibt die Datensätze in der Reihenfolge, in der sie in der DNS-Datenbank aufgeführt sind.  
**1**  
Gibt die Datensätze, die ähnlich wie IP-Adresse die Netzwerkadressen zuerst. Dies ist die Standardeinstellung.  
**/logfilemaxsize [<size>]**  
Gibt die maximale Größe in Bytes (0 x 10000-0xFFFFFFFF) der Datei Dns.log an. Wenn die Datei die maximale Größe erreicht, wird DNS die ältesten Ereignisse überschrieben. Die Standardgröße beträgt 0 x 400000, d.h. 4 Megabyte (MB).  
**/LogFilePath [< Pfad + Protokolldateiname >]**  
Gibt den Pfad der Datei Dns.log. Der Standardpfad lautet % systemroot%\System32\Dns\Dns.log. Sie können einen anderen Pfad angeben, mit dem Format *Pfad + LogFileName*.  
**/logipfilterlist <IPaddress> [,<IPaddress>...]**  
Gibt an, welche Pakete in der Debug-Protokolldatei protokolliert werden. Die Einträge sind eine Liste der IP-Adressen. Nur die Pakete zu und von der IP-Adressen in der Liste werden protokolliert.  
**/LogLevel [<Eventtype>]**  
Bestimmt, welche Arten von Ereignissen in der Datei Dns.log aufgezeichnet werden. Jeder Ereignistyp wird durch eine Hexadezimalzahl dargestellt. Wenn mehr als ein Ereignis im Protokoll werden sollen, verwenden Sie hexadezimale hinzufügen, fügen Sie die Werte, und geben die Summe.  
**0x0**  
Der DNS-Server erstellt ein Protokoll nicht. Dies ist der Standardeintrag.  
**0x10**  
Protokolliert Abfragen.  
**0x10**  
Protokolliert Benachrichtigungen.  
**0x20**  
Protokolliert von Updates.  
**0xFE**  
Protokolliert Nonquery Transaktionen an.  
**0x100**  
Protokolle Frage Transaktionen.  
**0x200**  
Protokolliert die Antworten.  
**0x1000**  
Senden von Protokollen Pakete.  
**0x2000**  
Protokolle werden die Pakete empfangen.  
**0x4000**  
User Datagram Protocol (UDP)-Paketen wird protokolliert.  
**0x8000**  
Transmission Control Protocol (TCP)-Paketen wird protokolliert.  
**0xFFFF**  
Protokolliert alle Pakete an.  
**0x10000**  
Protokolliert die active Directory-Write-Transaktionen.  
**0x20000**  
Protokolliert die active Directory-Update-Transaktionen.  
**0x1000000**  
Vollständige Protokolle-Pakete.  
**0x80000000**  
Protokolle Write-through-Transaktionen.  
**/maxcachesize**  
Gibt die maximale Größe in Kilobyte (KB), der den DNS-Server-s-Memory-Cache an.  
**/maxcachettl [<seconds>]**  
Bestimmt, wie viele Sekunden (0 x 0 – 0xFFFFFFFF) ein Eintrag im Cache gespeichert wird. Wenn die **0 x 0** Einstellung wird verwendet, der DNS-Server zwischenspeichert keine Datensätze. Die Standardeinstellung ist **0x15180** (86.400 Sekunden bzw. 1 Tag).  
**/maxnegativecachettl [<seconds>]**  
Gibt an, wie viele Sekunden (0 x 1-0xFFFFFFFF) ein Eintrag, der eine negative Antwort auf eine Abfrage zeichnet im DNS-Cache gespeicherte bleibt. Die Standardeinstellung ist **0 x 384** (900 Sekunden).  
**/namecheckflag [0 | 1 | 2 | 3].**  
Gibt an, welche Zeichen-Standard verwendet wird, bei der Überprüfung von DNS-Namen.  
**0**  
Verwendet ANSI-Zeichen, die Einhaltung der Internet Engineering Task force (IETF)-Anforderungen für Kommentare (Rfcs).  
**1**  
Verwendet ANSI-Zeichen, die nicht unbedingt IETF-Rfcs entsprechen.  
**2**  
Verwendet multibyte UCS-Transformation format 8 (UTF-8) Zeichen. Dies ist die Standardeinstellung.  
**3**  
Verwendet alle Zeichen.  
**/NoRecursion [0 | 1]**  
Bestimmt, ob die rekursive namensauflösung durch ein DNS-Server ausgeführt wird.  
**0**  
Der DNS-Server führt die rekursive namensauflösung, wenn diese in einer Abfrage angefordert werden. Dies ist die Standardeinstellung.  
**1**  
Der DNS-Server führt keine rekursive namensauflösung.  
**/notcp**  
Dieser Parameter ist veraltet, und wirkt sich nicht in aktuellen Versionen von Windows Server.  
**/recursionretry [<seconds>]**  
Bestimmt die Anzahl von Sekunden (0 x 1-0xFFFFFFFF), die ein DNS-Server wartet, bevor erneut versucht, einen Remoteserver zu kontaktieren. Die Standardeinstellung ist 0 x 3 (drei Sekunden). Dieser Wert sollte erhöht werden, wenn der Rekursion tritt auf, über eine langsame Netzwerkverbindung (WAN).  
**/RecursionTimeout [<seconds>]**  
Bestimmt die Anzahl von Sekunden (0 x 1-0xFFFFFFFF), die ein DNS-Server zu wartet, bevor ein Versuche, einen Remoteserver zu kontaktieren. Die Einstellungen sind z. B. **0 x 1** über **0xFFFFFFFF**. Die Standardeinstellung ist **0xF** (15 Sekunden). Dieser Wert sollte erhöht werden, wenn Rekursion über eine langsame WAN-Verbindung auftritt.  
**/Roundrobin [0 | 1]**  
Bestimmt die Reihenfolge, in der Hosteinträge zurückgegeben werden, wenn ein Server mit mehrfach-Hosteinträge für den gleichen Namen verfügt.  
0  
Round-Robin verwendet der DNS-Server nicht. Stattdessen wird den ersten Datensatz an jede Abfrage zurückgegeben.  
**1**  
Der DNS-Server dreht sich zwischen den Datensätzen, die vom oberen zum unteren Rand der Liste der übereinstimmenden Datensätze zurückgegeben. Dies ist die Standardeinstellung.  
**/RpcProtocol [0 x 0 | 0 x 1 | 0 x 2 | 0 x 4 | 0xFFFFFFFF]**  
Gibt das Protokoll, das einen Remoteprozeduraufruf (RPC) verwendet, wenn es sich um eine Verbindung von der DNS-Server herstellt.  
**0x0**  
Deaktiviert die RPC-DNS.  
**0x1**  
Verwendet die TCP/IP.  
**0x2**  
Named Pipes verwendet.  
**0x4**  
Lokaler Prozeduraufruf (LPC) wird verwendet.  
**0xFFFFFFFF**  
Alle Protokolle. Dies ist die Standardeinstellung.  
**/ ScavengingInterval [<hours>]**  
Bestimmt, ob die aufräumeinstellungen-Funktion für den DNS-Server aktiviert ist, und die Anzahl der Stunden (0 x 0 – 0xFFFFFFFF legt) zwischen den Aufräumvorgang Zyklen. Die Standardeinstellung ist **0 x 0**, wodurch deaktiviert Aufräumvorgang für den DNS-Server. Eine Einstellung größer als **0 x 0** können durch eine Bereinigung für den Server und die Anzahl der Stunden zwischen aufräumeinstellungen Zyklen.  
**/SecureResponses [0 | 1]**  
Bestimmt, ob die DNS-Datensätze Filter, die in einem Cache gespeichert werden.  
**0**  
Speichert alle Antworten auf Abfragen mit einem Cache. Dies ist die Standardeinstellung.  
**1**  
Speichert nur die Datensätze, die auf die gleiche DNS-Unterstruktur mit einem Cache gehören.  
**/SendPort [<port>]**  
Gibt die Portnummer (0 x 0 – 0xFFFFFFFF), die DNS verwendet, um rekursive Abfragen an andere DNS-Server zu senden. Die Standardeinstellung ist **0 x 0**, was bedeutet, dass die Portnummer nach dem Zufallsprinzip ausgewählt ist.  
**/serverlevelplugindll[<Dllpath>]**  
Gibt den Pfad einer benutzerdefinierten-Plug-in. Wenn *Dllpath* gibt den vollqualifizierten Pfad-Namen, der einen gültigen DNS-Server-Plug-in, der DNS-Server Ruft die Funktionen im plug-in zum Auflösen von Abfragen, die außerhalb des Bereichs aller lokal gehostete Zonen. Wenn abgefragten Namens außerhalb des Bereichs des Plug-Ins der ist, führt der DNS-Server namensauflösung mithilfe der Weiterleitung oder Rekursion entsprechend der Konfiguration. Wenn *Dllpath* nicht angegeben ist, wird der DNS-Server ist nicht mehr ein benutzerdefiniertes plug-in verwenden, wenn ein benutzerdefiniertes plug-in zuvor konfiguriert wurde.  
**/strictfileparsing [0 | 1]**  
Bestimmt das Verhalten von einem DNS-Server bei der es sich um einen fehlerhaften Datensatz trifft, beim Laden einer Zone.  
**0**  
Der DNS-Server weiterhin die Zone zu laden, auch wenn der Server einen fehlerhaften Datensatz auftreten. Der Fehler wird im DNS-Protokoll aufgezeichnet. Dies ist die Standardeinstellung.  
**1**  
Der DNS-Server beendet das Laden der Zone, und den Fehler im DNS-Protokoll aufgezeichnet.  
**/updateoptions <RecordValue>**  
Verhindert, dass dynamische Updates von der angegebenen Typen von Datensätzen. Wenn Sie mehr als ein Datensatztyp, den Sie in das Protokoll nicht zulässig sein möchten, verwenden Sie hexadezimale hinzufügen, fügen Sie die Werte, und geben dann die Summe.  
**0x0**  
Record-Typen nicht eingeschränkt.  
**0x1**  
Schließt Anfang Ressourceneinträge für Autoritätsursprung (SOA).  
**0x2**  
Schließt den Ressourceneinträgen Namenserver (NS).  
**0x4**  
Schließt die Delegierung der Namenserver (NS)-Ressourceneinträge.  
**0x8**  
Schließt die Host-Einträge.  
**0x100**  
Bei der sicheren dynamischen Updates schließt Anfang Ressourceneinträge für Autoritätsursprung (SOA).  
**0x200**  
Bei der sicheren dynamischen Updates schließt Stamm Namenserver (NS)-Ressourceneinträge.  
**0x30F**  
Während einer dynamischen Aktualisierung ist standard schließt Namenserver (NS)-Ressourceneinträge, Start der Ressourceneinträge für Autoritätsursprung (SOA), und der Server-Host-Datensätze. Bei der sicheren dynamischen Updates schließt Stamm Namenserver (NS)-Ressourceneinträgen und Starten der Ressourceneinträge für Autoritätsursprung (SOA). Ermöglicht es, Delegierungen und Server Updates zu hosten.  
**0x400**  
Bei der sicheren dynamischen Updates schließt Delegierung Namenserver (NS)-Ressourceneinträge.  
**0x800**  
Bei der sicheren dynamischen Updates schließt Host-Einträge.  
**0x1000000**  
Schließt die Delegierungseinträge-delegierungssignaturgebers (DS).  
**0x80000000**  
Deaktiviert die dynamische DNS-Updates.  
**/writeauthorityns [0 | 1]**  
Bestimmt, wenn der DNS-Server (NS)-Namenserver-Ressourceneinträge in die Authority-Abschnitt einer Antwort schreibt.  
**0**  
Schreibt die Authority-Abschnitt nur Weiterleitungen Namenserver (NS)-Ressourceneinträge. Diese Einstellung ist mit Rfc 1034, Domäne-Namen-Konzepte und Funktionen, und klicken Sie mit Rfc 2181, Erläuterungen der DNS-Spezifikation. Dies ist die Standardeinstellung.  
**1**  
Schreibt Namenserver (NS)-Ressourceneinträge in die Authority-Abschnitt von allen erfolgreichen autoritativen Antworten.  
**/xfrconnecttimeout [<seconds>]**  
Bestimmt die Anzahl von Sekunden (0 x 0 – 0xFFFFFFFF) ein primärer DNS-Server wartet, bis eine Übertragung-Antwort mit dem sekundären Server. Der Standardwert ist **0x1E** (30 Sekunden). Nachdem Sie den Wert der Timeoutzeitspanne abgelaufen ist, wird die Verbindung beendet.  
#### <a name="zone-level-syntax"></a>Auf Zonenebene-syntax  
```  
dnscmd /config <Parameters>  
```  
#### <a name="dnscmd-config"></a>dnscmd /config  
Ändert die Konfiguration der angegebenen Zone.  
#### <a name="parameters"></a>Parameter  
**<Parameters>**  
Geben Sie eine Einstellung, die einer Zone, Name und optional einen Wert an. Parameterwerte mit der folgenden Syntax: *Zonenname Parameter* [*Wert*]  
Die folgenden Parameterwerte werden in der übrige Teil dieses Abschnitts beschrieben:  
-   **/aging**  
-   **/allownsrecordsautocreation**  
-   **/allowupdate**  
-   **/forwarderslave**  
-   **/forwardertimeout**  
-   **/norefreshinterval**  
-   **/refreshinterval**  
-   **/securesecondaries**  
**/ Alterung <ZoneName>**  
Aktiviert oder deaktiviert, durch eine Bereinigung in einer bestimmten Zone.  
**AllowNSRecordsAutoCreation <ZoneName> [<Value>]**  
Überschreibt die DNS-Server Name Namenserver (NS) Ressource Datensatz Autocreation festlegen. Namenserver (NS)-Ressourceneinträge, die zuvor für diese Zone registriert wurden, sind nicht betroffen. Aus diesem Grund müssen Sie diese manuell entfernen, wenn Sie nicht möchten.  
**/allowupdate <ZoneName>**  
Bestimmt, ob die angegebene Zone dynamische Updates zulässt.  
**/forwarderslave <ZoneName>**  
Überschreibt die DNS-Server **/isslave** festlegen.  
**/forwardertimeout <ZoneName>**  
Bestimmt, wie viele Sekunden eine DNS-Zone für eine Weiterleitung zu reagieren, bevor Sie versuchen, eine andere Weiterleitung wartet. Dieser Wert überschreibt den Wert, der auf der Serverebene festgelegt ist.  
**/ NoRefreshInterval <ZoneName>**  
Legt ein Zeitintervall für eine Zone keine Aktualisierungen während, die dynamische DNS-Einträgen in einer bestimmten Zone aktualisieren können.  
**/ RefreshInterval <ZoneName>**  
Legt ein Zeitintervall für eine Zone, die während, die DNS-Einträgen in einer bestimmten Zone dynamisch zu Aktualisierungen aktualisieren können.  
**/securesecondaries <ZoneName>**  
Bestimmt, welche sekundäre Server Zonenupdates auf dem Masterserver für diese Zone empfangen können.  
#### <a name="remarks"></a>Hinweise  
-   Der Zonenname muss nur für auf Zonenebene-Parameter angegeben werden.  
### <a name="BKMK_4"></a>dnscmd /createbuiltindirectorypartitions  
erstellt eine DNS-Anwendungsverzeichnispartition. Wenn DNS installiert ist, wird eine Anwendungsverzeichnispartition für den Dienst auf den Ebenen Gesamtstruktur und Domäne erstellt. Verwenden Sie diesen Befehl zum Erstellen von DNS-Anwendungsverzeichnispartitionen, die nicht erstellt oder gelöscht wurden. Ohne Parameter erstellt der Befehl eine integrierten DNS-Verzeichnispartition für die Domäne.  
#### <a name="syntax"></a>Syntax  
```  
dnscmd [<ServerName>] /createbuiltindirectorypartitions [/forest] [/alldomains]   
```  
#### <a name="parameters"></a>Parameter  
**<ServerName>**  
Gibt an, den DNS-Server für die Verwaltung, durch die IP-Adresse, den FQDN oder Hostnamen dargestellt wird. Wenn dieser Parameter ausgelassen wird, wird der lokale Server verwendet.  
**/forest**  
erstellt eine DNS-Verzeichnispartition für die Gesamtstruktur.  
**/alldomains**  
erstellt von DNS-Partitionen für alle Domänen in der Gesamtstruktur.  
### <a name="BKMK_5"></a>dnscmd /createdirectorypartition  
erstellt eine DNS-Anwendungsverzeichnispartition. Wenn DNS installiert ist, wird eine Anwendungsverzeichnispartition für den Dienst auf den Ebenen Gesamtstruktur und Domäne erstellt. Dieser Vorgang erstellt zusätzliche DNS-Anwendungsverzeichnispartitionen.  
#### <a name="syntax"></a>Syntax  
```  
dnscmd [<ServerName>] /createdirectorypartition <PartitionFQDN>  
```  
#### <a name="parameters"></a>Parameter  
**<ServerName>**  
Gibt an, den DNS-Server für die Verwaltung, durch die IP-Adresse, den FQDN oder Hostnamen dargestellt wird. Wenn dieser Parameter ausgelassen wird, wird der lokale Server verwendet.  
**<PartitionFQDN>**  
Der FQDN des DNS-Anwendungsverzeichnispartition, die erstellt werden.  
### <a name="BKMK_6"></a>dnscmd /deletedirectorypartition  
Entfernt eine vorhandene DNS-Anwendungsverzeichnispartition.  
#### <a name="syntax"></a>Syntax  
```  
dnscmd [<ServerName>] /deletedirectorypartition <PartitionFQDN>  
```  
#### <a name="parameters"></a>Parameter  
**<ServerName>**  
Gibt an, den DNS-Server für die Verwaltung, durch die IP-Adresse, den FQDN oder Hostnamen dargestellt wird. Wenn dieser Parameter ausgelassen wird, wird der lokale Server verwendet.  
**<PartitionFQDN>**  
Der FQDN des DNS-Anwendungsverzeichnispartition, die entfernt werden.  
### <a name="BKMK_7"></a>dnscmd /directorypartitioninfo  
Listet Informationen zu einer angegebenen DNS-Anwendungsverzeichnispartition.  
#### <a name="syntax"></a>Syntax  
```  
dnscmd [<ServerName>] /directorypartitioninfo <PartitionFQDN> [/detail]   
```  
#### <a name="parameters"></a>Parameter  
**<ServerName>**  
Gibt an, den DNS-Server für die Verwaltung, durch die IP-Adresse, den FQDN oder Hostnamen dargestellt wird. Wenn dieser Parameter ausgelassen wird, wird der lokale Server verwendet.  
**<PartitionFQDN>**  
Der FQDN des DNS-Anwendungsverzeichnispartition.  
**/detail**  
enthält alle Informationen über die Anwendungsverzeichnispartition.  
### <a name="BKMK_8"></a>dnscmd /enlistdirectorypartition  
den DNS-Server und die angegebene Verzeichnispartition Replikatgruppe hinzugefügt.  
#### <a name="syntax"></a>Syntax  
```  
dnscmd [<ServerName>] /enlistdirectorypartition <PartitionFQDN>  
```  
#### <a name="parameters"></a>Parameter  
**<ServerName>**  
Gibt an, den DNS-Server für die Verwaltung, durch die IP-Adresse, den FQDN oder Hostnamen dargestellt wird. Wenn dieser Parameter ausgelassen wird, wird der lokale Server verwendet.  
**<PartitionFQDN>**  
Der FQDN des DNS-Anwendungsverzeichnispartition.  
### <a name="BKMK_9"></a>dnscmd /enumdirectorypartitions  
Listet die DNS-Anwendungsverzeichnispartitionen für den angegebenen Server.  
#### <a name="syntax"></a>Syntax  
```  
dnscmd [<ServerName>] /enumdirectorypartitions [/custom]   
```  
#### <a name="parameters"></a>Parameter  
**<ServerName>**  
Gibt an, den DNS-Server für die Verwaltung, durch die IP-Adresse, den FQDN oder Hostnamen dargestellt wird. Wenn dieser Parameter ausgelassen wird, wird der lokale Server verwendet.  
**/custom**  
Listet nur die Benutzer erstellte Verzeichnispartitionen an.  
### <a name="BKMK_10"></a>DNSCmd /enumrecords  
Listet die Ressourceneinträge für einen angegebenen Knoten in einer DNS-Zone.  
#### <a name="syntax"></a>Syntax  
```  
dnscmd [<ServerName>] /enumrecords <ZoneName> <NodeName> [/type <RRtype> <Rrdata>] [/authority] [/glue] [/additional] [/node | /child | /startchild<ChildName>] [/continue | /detail]   
```  
#### <a name="parameters"></a>Parameter  
**<ServerName>**  
Gibt den DNS-Server, den Sie verwalten möchten, die durch die IP-Adresse, den FQDN oder Hostnamen dargestellt wurden. Wenn dieser Parameter ausgelassen wird, wird der lokale Server verwendet.  
**/enumrecords**  
Listet die Ressourceneinträge in der angegebenen Zone.  
**<ZoneName>**  
Gibt den Namen der Zone, die die Ressourceneinträge angehören.  
**<NodeName>**  
Gibt den Namen des Knotens die Ressourceneinträge.  
**/type <RRtype> <Rrdata>**  
Gibt den Typ der Ressourceneinträge aufgelistet werden und den Typ der Daten, die erwartet wird:  
**<RRtype>**  
Gibt den Typ der Ressourceneinträge aufgelistet werden.  
**<Rrdata>**  
Gibt den Typ der Daten, die erwartete Datensatz ist.  
**/authority**  
Enthält die autorisierende Daten.  
**/glue**  
Enthält Daten der "Klebstoff".  
**/additional**  
Enthält alle zusätzlichen Informationen über die aufgeführten-Ressourceneinträge an.  
**{/node | /child | /startchild <ChildName>}**  
Filtert, oder die Anzeige der Ressource Datensätze Informationen hinzugefügt:  
**/node**  
Listet nur die Ressourceneinträge des angegebenen Knotens.  
**/child**  
Listet nur die Ressourceneinträge einer angegebenen untergeordneten Domäne an.  
**/StartChild <ChildName>**  
Beginnt die Liste in der angegebenen untergeordneten Domäne an.  
**/continue | /detail**  
Gibt an, wie die zurückgegebenen Daten angezeigt werden.  
**/continue**  
Listet nur die Ressourceneinträge mit den jeweiligen Typ und die Daten an.  
**/detail**  
Listet alle Informationen über die Ressourceneinträge an.  
#### <a name="sample-usage"></a>Beispiel für die Verwendung  
`dnscmd /enumrecords test.contoso.com test /additional`  
### <a name="BKMK_11"></a>DNSCmd /enumzones  
Listet die Zonen, die auf dem angegebenen DNS-Server vorhanden sind.  
#### <a name="syntax"></a>Syntax  
```  
dnscmd [<ServerName>] /enumzones [/primary | /secondary | /forwarder | /stub | /cache | /auto-created] [/forward | /reverse | /ds | /file] [/domaindirectorypartition | /forestdirectorypartition | /customdirectorypartition | /legacydirectorypartition | /directorypartition <PartitionFQDN>]  
```  
#### <a name="parameters"></a>Parameter  
**<ServerName>**  
Gibt an, den DNS-Server für die Verwaltung, durch die IP-Adresse, den FQDN oder Hostnamen dargestellt wird. Wenn dieser Parameter ausgelassen wird, wird der lokale Server verwendet.  
**/primary | /secondary | /forwarder | /stub | /cache | /auto-created**  
Filtert die Typen von Zonen angezeigt:  
**/primary**  
Listet alle-Zonen, die normale primäre Zonen oder active Directory-integrierte Zonen sind.  
**/secondary**  
Listet alle sekundäre Standardzonen an.  
**/forwarder**  
Listet die Zonen, die nicht aufgelöste Abfragen an einen anderen DNS-Server weiterleiten.  
**/stub**  
Listet alle Stubzonen an.  
**/cache**  
Listet nur die Zonen, die in den Cache geladen werden.  
**/auto-created**  
Listet die Zonen, die automatisch während der Installation der DNS-Server erstellt wurden.  
**/forward | /reverse | /ds | /file**  
Gibt zusätzliche Filter für die Typen von Zonen angezeigt:  
**/forward**  
enthält forward-Lookupzonen.  
**/reverse**  
enthält reverse-Lookupzonen.  
**/ds**  
Listet die active Directory-integrierte Zonen.  
**/file**  
Listen-Zonen, die durch Dateien gesichert werden.  
**/domaindirectorypartition**  
Listen-Zonen, die in der Domänenverzeichnispartition gespeichert sind.  
**/forestdirectorypartition**  
Listen-Zonen, die in der Gesamtstruktur-DNS-Anwendungsverzeichnispartition gespeichert sind.  
**/customdirectorypartition**  
Listet alle-Zonen, die in einer benutzerdefinierten Anwendungsverzeichnispartition gespeichert sind.  
**/legacydirectorypartition**  
Listet alle-Zonen, die in der Domänenverzeichnispartition gespeichert sind.  
**/directorypartition <PartitionFQDN>**  
Listet alle-Zonen, die in die angegebene Verzeichnispartition gespeichert sind.  
#### <a name="remarks"></a>Hinweise  
-   Die **Enumzones** Parametern als Filter in der Liste der Zonen zu fungieren. Wenn kein Filter angegeben werden, wird eine vollständige Liste der Zonen zurückgegeben. Wenn ein Filter angegeben wird, sind nur die Zonen, die dieser Filter andere Kriterien erfüllen, in der zurückgegebenen Liste von Zonen enthalten.  
#### <a name="example"></a>Beispiel  
Finden Sie unter [Beispiel 2: Zeigen Sie auf einem DNS-Server eine vollständige Liste der Zonen](https://technet.microsoft.com/library/cc784399(v=ws.10).aspx) oder [Beispiel 3: Anzeigen eine Liste der automatisch erstellt Zonen auf einem DNS-Server](https://technet.microsoft.com/library/cc784399(v=ws.10).aspx).  
### <a name="BKMK_25a"></a>dnscmd /exportsettings  
erstellt eine Textdatei, die die Konfigurationsdetails der DNS-Server werden aufgelistet. Die Textdatei heißt DnsSettings.txt. Es befindet sich im Verzeichnis %systemroot%\system32\dns des Servers.  
#### <a name="syntax"></a>Syntax  
```  
dnscmd [<ServerName>] /exportsettings   
```  
#### <a name="parameters"></a>Parameter  
**<ServerName>**  
Gibt den DNS-Server verwalten, dargestellt durch die Syntax für lokalen Computer, IP-Adresse, FQDN oder Hostnamen. Wenn dieser Parameter ausgelassen wird, wird der lokale Server verwendet.  
#### <a name="remarks"></a>Hinweise  
-   Sie können die Informationen in der Datei, die **Dnscmd /exportsettings** erstellt werden, um Konfigurationsprobleme zu beheben oder um sicherzustellen, dass Sie mehrere Server identisch konfiguriert haben.  
### <a name="BKMK_12"></a>DNSCmd/Info  
Zeigt die Einstellungen aus dem DNS-Abschnitt der Registrierung des angegebenen Servers: **HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\DNS\Parameters**  
#### <a name="syntax"></a>Syntax  
```  
dnscmd [<ServerName>] /info [<Setting>]  
```  
#### <a name="parameters"></a>Parameter  
**<ServerName>**  
Gibt an, den DNS-Server für die Verwaltung, durch die IP-Adresse, den FQDN oder Hostnamen dargestellt wird. Wenn dieser Parameter ausgelassen wird, wird der lokale Server verwendet.  
**<Setting>**  
Eine Einstellung, die die **Informationen** gibt der Befehl können einzeln angegeben werden. Wenn eine Einstellung nicht angegeben ist, wird die allgemeine Einstellungen für ein Bericht zurückgegeben.  
#### <a name="remarks"></a>Hinweise  
-   Dieser Befehl zeigt die registrierungseinstellungen, die auf der Ebene der DNS-Server befinden. Verwenden Sie zum Anzeigen auf Zonenebene-registrierungseinstellungen für die [zoneinfo der Anwendung](#BKMK_26) Befehl. Eine Liste der Einstellungen, die mit diesem Befehl angezeigt werden können, finden Sie unter den [Config](#BKMK_3) Beschreibung.  
#### <a name="example"></a>Beispiel  
Finden Sie unter [Beispiel 4: Anzeigen von einem DNS-Server die Einstellung für die IsSlave](https://technet.microsoft.com/library/cc784399(v=ws.10).aspx) oder [Beispiel 5: Zeigen Sie die Einstellung "RecursionTimeout" muss einen DNS-Server](https://technet.microsoft.com/library/cc784399(v=ws.10).aspx).  
### <a name="BKMK_29a"></a>DNSCmd /ipvalidate  
Testet, ob eine IP-Adresse identifiziert wird, ein funktionierender DNS-Server oder gibt an, ob der DNS-Server als eine Weiterleitung, einen Hinweis-Stammserver oder einen Masterserver für eine bestimmte Zone reagieren kann.  
#### <a name="syntax"></a>Syntax  
```  
dnscmd [<ServerName>] /ipvalidate <Context> [<ZoneName>] [[<IPaddress>]]  
```  
#### <a name="parameters"></a>Parameter  
**<ServerName>**  
Gibt den DNS-Server verwalten, dargestellt durch die Syntax für lokalen Computer, IP-Adresse, FQDN oder Hostnamen. Wenn dieser Parameter ausgelassen wird, wird der lokale Server verwendet.  
**<Context>**  
Gibt den Typ der durchzuführenden Tests. Sie können einen der folgenden Tests angeben:  
-   **/DNSServers** getestet, ob die Computer mit der die Adressen, die Sie angeben, DNS-Server funktionieren.  
-   **/Forwarders** getestet, ob die Adressen, die Sie angeben, DNS-Server identifizieren, die als Weiterleitungen fungieren kann.  
-   **/roothints** getestet, ob die Adressen, die Sie angeben, DNS-Server identifizieren, die als Hinweis Stammservern fungieren kann.  
-   **/zonemasters** getestet, ob die Adressen, die Sie angeben, DNS-Server identifizieren, die von Masterservern *ZoneName*.  
**<ZoneName>**  
Identifiziert die Zone an. Verwenden Sie diesen Parameter mit dem **/zonemasters** Parameter.  
**<IPaddress>**  
Gibt die IP-Adressen, die der Befehl testet.  
#### <a name="sample-usage"></a>Beispiel für die Verwendung  
<pre>dnscmd dnssvr1.contoso.com /ipvalidate /dnsservers 10.0.0.1 10.0.0.2  
dnscmd dnssvr1.contoso.com /ipvalidate /zonemasters corp.contoso.com 10.0.0.2</pre>  
### <a name="BKMK_13"></a>DNSCmd /nodedelete  
Löscht alle Datensätze für einen angegebenen Host. ### Syntax ```  
dnscmd [<ServerName>] /nodedelete <ZoneName> <NodeName> [/tree] [/ f] ```  
#### Parameters  
**<ServerName>**  
Gibt an, den DNS-Server für die Verwaltung, durch die IP-Adresse, den FQDN oder Hostnamen dargestellt wird. Wenn dieser Parameter ausgelassen wird, wird der lokale Server verwendet.  
**<ZoneName>**  
Gibt den Namen der Zone.  
**<NodeName>**  
Gibt den Hostnamen des Knotens, zu löschen.  
**/tree**  
Löscht alle untergeordneten Datensätze an.  
**/f**  
Führt den Befehl ohne Aufforderung zur Bestätigung an. ### Beispiel finden Sie unter [Beispiel 6: Löschen Sie die Datensätze aus einem Knoten](https://technet.microsoft.com/library/cc784399(v=ws.10).aspx).  
### <a name="BKMK_14"></a>dnscmd /recordadd  
Fügt einen Datensatz zu einer angegebenen Zone im DNS-Server an. ### Syntax ```  
dnscmd [<ServerName>] / RecordAdd <ZoneName> <NodeName> <RRtype> <Rrdata> ```  
#### Parameters  
**<ServerName>**  
Gibt den DNS-Server verwalten, dargestellt durch die Syntax für lokalen Computer, IP-Adresse, FQDN oder Hostnamen. Wenn dieser Parameter ausgelassen wird, wird der lokale Server verwendet.  
**<ZoneName>**  
Gibt an, die Zone, in der der Datensatz befindet.  
**<NodeName>**  
Gibt einen bestimmten Knoten in der Zone an.  
**<RRtype>**  
Gibt den Typ des Datensatzes, der hinzugefügt werden.  
**<Rrdata>**  
Gibt den Typ der Daten, die erwartet werden.  
> [!NOTE]  
Wenn Sie einen Eintrag hinzufügen, stellen Sie sicher, dass Sie die richtigen Daten und den-Format verwenden. Eine Liste der Resource Record-Typen und die entsprechenden Datentypen, finden Sie unter [-Ressourceneinträge Verweis](https://technet.microsoft.com/library/cc758321(v=ws.10).aspx). ### Beispiel für die Verwendung
<pre>dnscmd dnssvr1.contoso.com /recordadd test A 10.0.0.5  
dnscmd /recordadd test.contoso.com test MX 10 mailserver.test.contoso.com</pre>  
### <a name="BKMK_15"></a>dnscmd /recorddelete  
Löscht einen Ressourceneintrag aus einer bestimmten Zone an. ### Syntax ```  
dnscmd <ServerName> /recorddelete <ZoneName> <NodeName> <RRtype> <Rrdata>[/ f] ```  
#### Parameters  
**<ServerName>**  
> Gibt an, den DNS-Server für die Verwaltung, durch die IP-Adresse, den FQDN oder Hostnamen dargestellt wird. Wenn dieser Parameter ausgelassen wird, wird der lokale Server verwendet.  
**<ZoneName>**  
Gibt an, die Zone, in der sich der Ressourcendatensatz befindet.  
**<NodeName>**  
Gibt den Namen des Hosts.  
**<RRtype>**  
Gibt den Typ des Ressourceneintrags gelöscht werden soll.  
**<Rrdata>**  
Gibt den Typ der Daten, die erwartet werden.  
**/f**  
Führt den Befehl ohne zur Bestätigung aufzufordern:-Da Knoten mehr als ein Ressourcendatensatz verfügen können, dieser Befehl erfordert, dass Sie den Typ des Ressourceneintrags sehr spezifisch sein, die Sie löschen möchten. – Wenn Sie einen Datentyp angeben, und Sie einen Typ von Ressource Datensatzdaten, die nicht angeben, werden alle Datensätze mit diesem speziellen Datentyp für den angegebenen Knoten gelöscht. ### Beispiel für die Verwendung `dnscmd /recorddelete test.contoso.com test MX 10 mailserver.test.contoso.com`  
### <a name="BKMK_16"></a>dnscmd /resetforwarders  
aktiviert bzw. deaktiviert die IP-Adressen, der DNS-Server eine DNS-Abfragen weiterleitet, wenn es lokal auflösen kann nicht, zurückgesetzt. ### Syntax ```  
dnscmd [<ServerName>] /resetforwarders [<IPaddress> [,<IPaddress>]...] [/ Timeout <timeOut>] [zwischen Primär- und sekundärgerät | / Noslave] ```  
#### Parameters  
**<ServerName>**  
Gibt an, den DNS-Server für die Verwaltung, durch die IP-Adresse, den FQDN oder Hostnamen dargestellt wird. Wenn dieser Parameter ausgelassen wird, wird der lokale Server verwendet.  
**<IPaddress>**  
Listet die IP-Adressen, der DNS-Server nicht aufgelöste Abfragen weiterleitet.  
|**/Timeout <timeOut>**  
Legt die Anzahl der Sekunden an, denen der DNS-Server wartet, bis eine Antwort von der Weiterleitung fest. Standardmäßig ist dieser Wert über fünf Sekunden.  
**/slave|/noslave**  
Bestimmt, ob der DNS-Server eine eigene iterativen Abfragen ausführt, fällt die Weiterleitung zum Auflösen einer Abfrage:  
**/slave**  
Verhindert, dass den DNS-Server eine eigene iterativen Abfragen ausführen, wenn die Weiterleitung zum Auflösen einer Abfrage fehlschlägt.  
**/noslave**  
Ermöglicht dem DNS-Server eigene iterativen Abfragen ausführen, wenn die Weiterleitung zum Auflösen einer Abfrage fehlschlägt. Dies ist die Standardeinstellung. ### "Hinweise" - führt standardmäßig ein DNS-Server iterative Abfragen, wenn er eine Abfrage nicht auflösen kann. – Festlegen der IP-Adressen mithilfe der **Resetforwarders** Befehl bewirkt, dass den DNS-Server zum Ausführen von rekursiven Abfragen an die DNS-Server an den angegebenen IP-Adressen. Wenn die Weiterleitung die Abfrage nicht beheben, kann der DNS-Server dann eigene iterativen Abfragen ausführen. -Wenn die **zwischen Primär- und sekundärgerät** Parameter wird verwendet, der DNS-Server führt keine eigene iterativen Abfragen. Dies bedeutet, dass der DNS-Server nicht aufgelöste Abfragen nur für die DNS-Server in der Liste leitet aus, und iterative Abfragen wird nicht versucht, wenn die Weiterleitungen nicht behoben werden. Es ist sehr viel effizienter, eine IP-Adresse als Weiterleitung für einen DNS-Server festlegen. Sie können die **Resetforwarders** Befehl interne Server in einem Netzwerk, die nicht aufgelösten Abfragen an einen DNS-Server weiterzuleiten, die eine externe Verbindung besteht. – eine IP-Adresse der Weiterleitung zweimal auflisten bewirkt, dass den DNS-Server, um zu versuchen, zwei Mal auf diesem Server weiterleiten. ### Beispiel für die Verwendung
<pre>dnscmd dnssvr1.contoso.com /resetforwarders 10.0.0.1 /timeout 7 /slave  
dnscmd dnssvr1.contoso.com /resetforwarders /noslave</pre>  
### <a name="BKMK_17"></a>dnscmd /resetlistenaddresses  
Gibt die IP-Adressen auf einem Server, der DNS-Client-Anforderungen lauscht. ### Syntax ```  
dnscmd [<ServerName>] /resetlistenaddresses [<listenaddress>] ```  
#### Parameters  
**<ServerName>**  
Gibt an, den DNS-Server für die Verwaltung, durch die IP-Adresse, den FQDN oder Hostnamen dargestellt wird. Wenn dieser Parameter ausgelassen wird, wird der lokale Server verwendet.  
**<listenaddress>**  
Gibt eine IP-Adresse auf dem DNS-Server, der DNS-Client-Anforderungen lauscht. Wenn keine Adresse angegeben ist, Lauschen Clientanforderungen alle IP-Adressen auf dem Server. ### "Hinweise" - Lauschen standardmäßig alle IP-Adressen auf einem DNS-Server-DNS-Clientanforderungen. ### Beispiel für die Verwendung `dnscmd dnssvr1.contoso.com /resetlistenaddresses 10.0.0.1`  
### <a name="BKMK_18"></a>dnscmd /startscavenging  
Weist einen DNS-Server eine sofortige Suche nach veralteten Ressourceneinträgen in einen angegebenen DNS-Server versucht. ### Syntax ```  
dnscmd [<ServerName>] /startscavenging ```  
#### Parameter  
**<ServerName>**  
Gibt an, den DNS-Server für die Verwaltung, durch die IP-Adresse, den FQDN oder Hostnamen dargestellt wird. Wenn dieser Parameter ausgelassen wird, wird der lokale Server verwendet. ### "Hinweise" - erfolgreichen Abschluss dieses Befehls wird eine Aufräumen sofort gestartet. -Der Befehl zum Starten der Aufräumen scheint, zwar erfolgreich abgeschlossen werden die Aufräumen nicht gestartet, wenn die folgenden Voraussetzungen erfüllt sind:-Aufräumvorgang für den Server und die Zone aktiviert ist. : Die Zone wird gestartet. -Die-Ressourceneinträge müssen nach dem Zeitstempel. – Informationen dazu, wie Sie durch eine Bereinigung für den Server zu aktivieren, finden Sie unter der **Scavenginginterval** Parameter unter auf Serverebene-Syntax in der [Config](#BKMK_3) Abschnitt. -Informationen zum Aktivieren der Aufräumvorgang für die Zone, finden Sie unter den **Alterung** Parameter unter auf Zonenebene-Syntax in der [Config](#BKMK_3) Abschnitt. – Informationen zum Starten von einer Zone, die angehalten wird, finden Sie unter den [Zoneresume](#BKMK_35) Abschnitt. – Informationen zum Überprüfen der Ressourceneinträge für einen Zeitstempel, finden Sie unter den [Ageallrecords](#BKMK_1) Abschnitt. -Wenn die Aufräumen ein Fehler auftritt, keine Warnmeldung angezeigt wird. ### Beispiel für die Verwendung `dnscmd dnssvr1.contoso.com /startscavenging`  
### <a name="BKMK_19"></a>dnscmd /statistics  
Zeigt an, oder löscht die Daten für einen bestimmten DNS-Server. ### Syntax ```  
dnscmd [<ServerName>] Remotespeicherstatistik [<StatID>] [/ clear] ```  
#### Parameters  
**<ServerName>**  
Gibt an, den DNS-Server für die Verwaltung, durch die IP-Adresse, den FQDN oder Hostnamen dargestellt wird. Wenn dieser Parameter ausgelassen wird, wird der lokale Server verwendet.  
**<StatID>**  
Gibt an, welche Statistik oder eine Kombination von Statistiken angezeigt. Eine ID wird verwendet, um eine Statistik identifizieren. Wenn keine Statistik-ID-Nummer angegeben wird, werden alle Statistiken angezeigt.  
Im folgenden finden eine Liste mit Zahlen, die angegeben werden können und die entsprechenden Statistik, die anzeigt:  
**00000001**  
Zeit  
**00000002**  
query  
**00000004**  
query2  
**00000008**  
Recurse  
**00000010**  
Master  
**00000020**  
Sekundärer  
**00000040**  
WINS  
**00000100**  
Update/Aktualisieren  
**00000200**  
SkwanSec  
**00000400**  
Ds  
**00010000**  
Arbeitsspeicher  
**00100000**  
PacketMem  
**00040000**  
DBASE  
**00080000**  
Datensätze  
**00200000**  
NbstatMem  
**/clear**  
Setzt den angegebenen statistikleistungsindikator auf 0 (null) zurück. ### "Hinweise" – die **Statistiken** Befehl zeigt Leistungsindikatoren, die beginnen auf dem DNS-Server, wenn sie gestartet oder fortgesetzt wird. ### Beispiele finden Sie unter [Beispiel 7: Anzeigen von Statistiken für einen DNS-Server](https://technet.microsoft.com/library/cc784399(v=ws.10).aspx) oder [Beispiel 8: NbstatMem-Statistiken für einen DNS-Server anzeigen](https://technet.microsoft.com/library/cc784399(v=ws.10).aspx).  
### <a name="BKMK_20"></a>dnscmd /unenlistdirectorypartition  
Entfernt den DNS-Server aus der angegebenen Verzeichnispartition Replikatgruppe. ### Syntax ```  
dnscmd [<ServerName>] /unenlistdirectorypartition <PartitionFQDN> ```  
#### Parameters  
**<ServerName>**  
Gibt an, den DNS-Server für die Verwaltung, durch die IP-Adresse, den FQDN oder Hostnamen dargestellt wird. Wenn dieser Parameter ausgelassen wird, wird der lokale Server verwendet.  
**<PartitionFQDN>**  
Der FQDN des DNS-Anwendungsverzeichnispartition, die entfernt werden.  
### <a name="BKMK_21"></a>dnscmd /writebackfiles  
Den DNS-Server-Speicher auf Änderungen überprüft und schreibt sie in den persistenten Speicher. ### Syntax ```  
dnscmd [<ServerName>] /writebackfiles [<ZoneName>] ```  
#### Parameters  
**<ServerName>**  
Gibt an, den DNS-Server für die Verwaltung, durch die IP-Adresse, den FQDN oder Hostnamen dargestellt wird. Wenn dieser Parameter ausgelassen wird, wird der lokale Server verwendet.  
**<ZoneName>**  
Gibt den Namen der Zone, die aktualisiert werden. ### "Hinweise" – die **Writebackfiles** Befehl werden alle modifizierten Zonen oder einer bestimmten Zone. Eine Zone ist fehlerhaft, wenn Änderungen im Arbeitsspeicher, die noch nicht in den permanenten Speicher geschrieben wurden. Dies ist ein Vorgang auf Serverebene, der alle-Zonen überprüft. Sie können festlegen, dass eine Zone in diesem Vorgang, oder Verwenden der [Zonewriteback](#BKMK_37) Vorgang. ### Beispiel für die Verwendung `dnscmd dnssvr1.contoso.com /writebackfiles`  
### <a name="BKMK_22"></a>dnscmd /zoneadd  
Fügt eine Zone beim DNS-Server an. ### Syntax ```  
dnscmd [<ServerName>] / ZoneAdd <ZoneName> <Zonetype> [/ dp <FQDN>| {/ Domäne | / Enterprise | / ältere}] ```  
#### Parameters  
**<ServerName>**  
Gibt an, den DNS-Server für die Verwaltung, durch die IP-Adresse, den FQDN oder Hostnamen dargestellt wird. Wenn dieser Parameter ausgelassen wird, wird der lokale Server verwendet.  
**<ZoneName>**  
Gibt den Namen der Zone.  
**<Zonetype>**  
Gibt den Typ der Zone zu erstellen. Jeder Typ verfügt über verschiedene erforderliche Parameter:  
**/dsprimary**  
erstellt eine active Directory integrierte Zone an.  
**/primary/File <FileName>**  
eine primäre Standardzone erstellt und gibt den Namen der Datei, die die Zoneninformationen gespeichert werden.  
**/sekundären <MasterIPaddress> [<MasterIPaddress>...]**  
erstellt eine sekundäre Standardzone.  
**/stub <MasterIPaddress> [<MasterIPaddress>...] / file <FileName>**  
erstellt eine Stubzone mit zugrunde liegender Datei.  
**/Dsstub <MasterIPaddress> [<MasterIPaddress>...]**  
erstellt eine active Directory-integrierte Stub-Zone.  
**/Weiterleitung <MasterIPaddress> [<MasterIPaddress>]... / file <FileName>**  
Gibt an, dass die erstellte Zone nicht aufgelöste Abfragen an einen anderen DNS-Server weiterleitet.  
**/dsforwarder**  
Gibt an, dass die erstellten active Directory integrierte Zone nicht aufgelöste Abfragen an einen anderen DNS-Server weiterleitet.  
**/DP <FQDN> {/ Domäne | /enterprise | / ältere}**  
Gibt an, die Verzeichnispartition, auf dem die Zone gespeichert.  
**<FQDN>**  
Hiermit wird der FQDN der Verzeichnispartition.  
**/domain**  
Speichert die Zone in der Domänenverzeichnispartition an.  
**/enterprise**  
Speichert die Zone auf die Verzeichnispartition Enterprise.  
**/legacy**  
Speichert die Zone auf einer älteren Verzeichnispartition. ### "Hinweise" - Angeben eines Zone **/forwarder** oder **/dsforwarder** erstellt eine Zone, die für die bedingte Weiterleitung ausführt. ### Beispiel für die Verwendung
<pre>dnscmd dnssvr1.contoso.com /zoneadd test.contoso.com /dsprimary  
dnscmd dnssvr1.contoso.com /zoneadd secondtest.contoso.com /secondary 10.0.0.2</pre>  
### <a name="BKMK_23"></a>dnscmd /zonechangedirectorypartition  
Ändert die Verzeichnispartition, der auf der sich die angegebene Zone befindet. ### Syntax ```  
dnscmd [<ServerName>] /zonechangedirectorypartition <ZoneName>] {[<NewPartitionName>] | [<Zonetype>] } ```  
#### Parameters  
**<ServerName>**  
Gibt an, den DNS-Server für die Verwaltung, durch die IP-Adresse, den FQDN oder Hostnamen dargestellt wird. Wenn dieser Parameter ausgelassen wird, wird der lokale Server verwendet.  
**<ZoneName>**  
Der FQDN des von der aktuellen Verzeichnispartition, der auf der sich die Zone befindet.  
**<NewPartitionName>**  
Der FQDN der Verzeichnispartition, der die Zone verschoben wird.  
**<Zonetype>**  
Gibt den Typ der Verzeichnispartition, der die Zone verschoben wird.  
**/domain**  
wird die Zone in der integrierten Domänenverzeichnispartition verschoben.  
**/forest**  
Verschiebt die Zone für die integrierte Gesamtstrukturverzeichnispartition.  
**/legacy**  
Verschiebt die Zone für die Verzeichnispartition, die für active Directory-Domänencontroller vor erstellt wird. Dieser Verzeichnispartitionen sind nicht erforderlich, für den einheitlichen Modus.  
### <a name="BKMK_24"></a>dnscmd /zonedelete  
Löscht eine angegebene Zone. ### Syntax ```  
dnscmd [<ServerName>] /zonedelete <ZoneName> [/dsdel] [/ f] ```  
#### Parameters  
**<ServerName>**  
Gibt an, den DNS-Server für die Verwaltung, durch die IP-Adresse, den FQDN oder Hostnamen dargestellt wird. Wenn dieser Parameter ausgelassen wird, wird der lokale Server verwendet.  
**<ZoneName>**  
Gibt den Namen der Zone, die gelöscht werden.  
**/dsdel**  
Löscht die Zone aus AD DS.  
**/f**  
Führt den Befehl ohne Aufforderung zur Bestätigung an. ### Beispiel finden Sie unter [Beispiel 9: Löschen einer Zone aus einem DNS-Server](https://technet.microsoft.com/library/cc784399(v=ws.10).aspx).  
### <a name="BKMK_25"></a>dnscmd /zoneexport  
erstellt eine Textdatei, die die Ressourceneinträge der Zone angegebene auflistet. ### Syntax "Dnscmd [<ServerName>] /zoneexport <ZoneName> <ZoneExportFile>' ### Parameter **<ServerName>**  
Gibt den DNS-Server verwalten, dargestellt durch die Syntax für lokalen Computer, IP-Adresse, FQDN oder Hostnamen. Wenn dieser Parameter ausgelassen wird, wird der lokale Server verwendet.  
**<ZoneName>**  
Gibt den Namen der Zone.  
**<ZoneExportFile>**  
Gibt den Namen des zu erstellenden Datei. ### "Hinweise" – die **Zoneexport** Vorgang erstellt eine Datei von Ressourceneinträgen für eine active Directory integrierte Zone für die Problembehandlung. Standardmäßig wird die Datei, die mit diesem Befehl wird im DNS-Verzeichnis platziert, die wird standardmäßig das Verzeichnis %systemroot%/System32/Dns. ### Beispiel finden Sie unter [Beispiel 10: Liste der Zone Ressource Datensätze in eine Datei exportieren](https://technet.microsoft.com/library/cc784399(v=ws.10).aspx).  
### <a name="BKMK_26"></a>dnscmd /zoneinfo  
Zeigt die Einstellungen aus dem Abschnitt der Registrierung der angegebenen Zone: **HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\DNS\Parameters\Zones\\<ZoneName>** ### Syntax ```  
dnscmd [<ServerName>] / zoneinfo <ZoneName> [<Setting>] ```  
#### Parameters  
**<ServerName>**  
Gibt an, den DNS-Server für die Verwaltung, durch die IP-Adresse, den FQDN oder Hostnamen dargestellt wird. Wenn dieser Parameter ausgelassen wird, wird der lokale Server verwendet.  
**<ZoneName>**  
Gibt den Namen der Zone.  
**<Setting>**  
Sie können einzeln angeben, eine Einstellung, die die **zoneinfo der Anwendung** -Befehl zurückgegeben. Wenn Sie eine Einstellung nicht angeben, werden alle Einstellungen zurückgegeben. ### "Hinweise" – die **zoneinfo der Anwendung** Befehl zeigt die registrierungseinstellungen, die auf die DNS-Zone auf **HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\DNS\Parameters\Zones\\<ZoneName>**. -Wenn Sie registrierungseinstellungen auf Serverebene anzeigen zu können, verwenden die [Informationen](#BKMK_12) Befehl. -Eine Liste der Einstellungen, die Sie mit dem folgenden Befehl anzeigen können, finden Sie unter den [Config](#BKMK_3) Befehl. ### Beispiel finden Sie unter [Beispiel 11: RefreshInterval-Einstellung aus der Registrierung anzeigen](https://technet.microsoft.com/library/cc784399(v=ws.10).aspx) oder [Beispiel 12: Anzeigen, die Einstellung aus der Registrierung altern](https://technet.microsoft.com/library/cc784399(v=ws.10).aspx).  
### <a name="BKMK_27"></a>dnscmd /zonepause  
hält an die angegebene Zone, die dann abfrageanforderungen ignoriert. ### Syntax ```  
dnscmd [<ServerName>] /zonepause <ZoneName> ```  
#### Parameters  
**<ServerName>**  
Gibt an, den DNS-Server für die Verwaltung, durch die IP-Adresse, den FQDN oder Hostnamen dargestellt wird. Wenn dieser Parameter ausgelassen wird, wird der lokale Server verwendet.  
**<ZoneName>**  
Gibt den Namen der Zone, die angehalten werden. ### "Hinweise" - Fortsetzen einer Zone und macht sie verfügbar, nachdem sie angehalten wurde, verwenden Sie die [Zoneresume](#BKMK_35) Befehl. ### Beispiel für die Verwendung `dnscmd dnssvr1.contoso.com /zonepause test.contoso.com`  
### <a name="BKMK_28"></a>dnscmd /zoneprint  
Listet die Datensätze in einer Zone. ### Syntax ```  
dnscmd [<ServerName>] /zoneprint <ZoneName> ```  
#### Parameters  
**<ServerName>**  
Gibt den DNS-Server verwalten, dargestellt durch die Syntax für lokalen Computer, IP-Adresse, FQDN oder Hostnamen. Wenn dieser Parameter ausgelassen wird, wird der lokale Server verwendet.  
**<ZoneName>**  
Identifiziert die Zone aufgelistet werden.  
### <a name="BKMK_30"></a>dnscmd /zonerefresh  
Erzwingt, dass eine sekundäre DNS-Zone aus der master-Zone zu aktualisieren. ### Syntax ```  
dnscmd <ServerName> /zonerefresh <ZoneName> ```  
#### Parameters  
**<ServerName>**  
Gibt an, den DNS-Server für die Verwaltung, durch die IP-Adresse, den FQDN oder Hostnamen dargestellt wird. Wenn dieser Parameter ausgelassen wird, wird der lokale Server verwendet.  
**<ZoneName>**  
Gibt den Namen der Zone, die aktualisiert werden. ### "Hinweise" – die **Zonerefresh** Befehl zwingt eine Überprüfung der Versionsnummer der Masterserver s zu Beginn des Ressourceneintrags Autoritätsursprung (SOA). Wenn die Versionsnummer auf dem übergeordneten Server höher als Versionsnummer des sekundären Servers ist, wird eine zonenübertragung initiiert, die den sekundären Server aktualisiert. Wenn die Versionsnummer übereinstimmt, tritt auf, keine zonenübertragung. -Die erzwungene Prüfung erfolgt standardmäßig alle 15 Minuten. Um die Standardeinstellung zu ändern, verwenden die **Dnscmd-Config "RefreshInterval"** Befehl. ### Beispiel für die Verwendung `dnscmd dnssvr1.contoso.com /zonerefresh test.contoso.com`  
### <a name="BKMK_31"></a>dnscmd /zonereload  
Kopiert die Zeitzoneninformationen aus der Quelle. ### Syntax ```  
dnscmd <ServerName> /zonereload <ZoneName> ```  
#### Parameters  
**<ServerName>**  
Gibt an, den DNS-Server für die Verwaltung, durch die IP-Adresse, den FQDN oder Hostnamen dargestellt wird. Wenn dieser Parameter ausgelassen wird, wird der lokale Server verwendet.  
**<ZoneName>**  
Gibt den Namen der Zone neu geladen werden. ### "Hinweise": Wenn die Zone active Directory integriert ist, lädt sie aus AD DS. -Wenn die Zone einer Standardzone zugrunde liegender Datei ist, lädt Sie aus einer Datei. ### Beispiel für die Verwendung `dnscmd dnssvr1.contoso.com /zonereload test.contoso.com`  
### <a name="BKMK_32"></a>dnscmd /zoneresetmasters  
setzt die IP-Adressen der Masterserver, der Zone Übertragungsinformationen auf eine sekundäre Zone enthält. ### Syntax ```  
dnscmd <ServerName> /zoneresetmasters <ZoneName> [/ lokale] [<IPaddress> [<IPaddress>]...] ```  
#### Parameters  
**<ServerName>**  
Gibt an, den DNS-Server für die Verwaltung, durch die IP-Adresse, den FQDN oder Hostnamen dargestellt wird. Wenn dieser Parameter ausgelassen wird, wird der lokale Server verwendet.  
**<ZoneName>**  
Gibt den Namen der Zone neu geladen werden.  
**/local**  
Legt eine Liste der lokale master fest. Dieser Parameter wird für die active Directory-integrierte Zonen verwendet.  
**<IPaddress>**  
Die IP-Adressen der Masterserver der sekundären Zone. ### "Hinweise": Dieser Wert wird ursprünglich festgelegt, wenn die sekundäre Zone erstellt wird. Verwenden der **Zoneresetmasters** Befehl auf dem sekundären Server. Dieser Wert hat keine Auswirkungen, wenn sie auf dem DNS-Masterserver festgelegt ist. ### Beispiel für die Verwendung
<pre>dnscmd dnssvr1.contoso.com /zoneresetmasters test.contoso.com 10.0.0.1  
dnscmd dnssvr1.contoso.com /zoneresetmasters test.contoso.com /local</pre>  
### <a name="BKMK_33"></a>dnscmd /zoneresetscavengeservers  
ändert sich die IP-Adressen der Server, die die angegebene Zone Aufräumen können. ### Syntax ```  
dnscmd [<ServerName>] /zoneresetscavengeservers <ZoneName> [<IPaddress> [<IPaddress>]...] ```  
#### Parameters  
**<ServerName>**  
Gibt den DNS-Server verwalten, dargestellt durch die Syntax für lokalen Computer, IP-Adresse, FQDN oder Hostnamen. Wenn dieser Parameter ausgelassen wird, wird der lokale Server verwendet.  
**<ZoneName>**  
Identifiziert die Zone zu löschen sind.  
**<IPaddress>**  
Listet die IP-Adressen der Server, die das Aufräumen ausführen können. Wenn dieser Parameter ausgelassen wird, können Sie durch alle Server, die diese Zone hosten, aufräumen. ### Remarks - standardmäßig alle Server, die eine Zone zu hosten, diese Zone Aufräumen können. – Wenn eine Zone auf mehr als ein DNS-Server gehostet wird, können Sie diesen Befehl verwenden, um die Anzahl der zu reduzieren, eine Zone geleert wird. – Durch eine Bereinigung muss aktiviert sein, auf dem DNS-Server und die Zone, die mit diesem Befehl betroffen ist. ### Beispiel für die Verwendung `dnscmd dnssvr1.contoso.com /zoneresetscavengeservers test.contoso.com 10.0.0.1 10.0.0.2`  
### <a name="BKMK_34"></a>dnscmd /zoneresetsecondaries  
Gibt eine Liste der IP-Adressen der sekundären Server, auf ein Masterserver auf die reagiert, wenn es für eine zonenübertragung angefordert wird. ### Syntax ```  
dnscmd [<ServerName>] /zoneresetsecondaries <ZoneName> {/ Noxfr | / nicht sichere | /securens | / SecureList <SecurityIPaddresses>} {/ Nonotify | / benachrichtigen | /notifylist <NotifyIPaddresses>} ```  
#### Parameters  
**<ServerName>**  
Gibt an, den DNS-Server für die Verwaltung, durch die IP-Adresse, den FQDN oder Hostnamen dargestellt wird. Wenn die ist der Parameter ausgelassen wird, wird der lokale Server verwendet.  
**<ZoneName>**  
Gibt den Namen der Zone, die die sekundären Server haben, werden zurückgesetzt.  
**/Noxfr | / nicht sichere | /securens | / SecureList <SecurityIPaddresses>**  
Gibt an, ob alle oder nur einige der sekundären Server ein Update angefordert ein Update zu erhalten.  
**/noxfr**  
Gibt an, dass keine zonenübertragungen zulässig sind.  
**/nonsecure**  
Gibt an, dass alle zonenübertragungsanforderungen gewährt werden.  
**/securens**  
Gibt an, dass nur an der Server, der in der Namenserver (NS)-Ressourceneintrag für die Zone aufgeführt ist, eine Übertragung gewährt wird.  
**/securelist**  
Gibt an, dass zonenübertragungen nur die Liste der Server gewährt werden. Dieser Parameter muss eine IP-Adressen, die der Masterserver verwendet gefolgt werden.  
**<SecurityIPaddresses>**  
Listet die IP-Adressen, die auf dem Masterserver zonenübertragungen empfangen. Dieser Parameter wird verwendet, nur mit der **/SecureList** Parameter.  
**/nonotify | /notify | /notifylist <NotifyIPaddresses>**  
Gibt an, dass nur zu bestimmten sekundären Servern eine änderungsbenachrichtigung gesendet wird:  
**/nonotify**  
Gibt an, dass keine änderungsbenachrichtigungen an sekundären Server gesendet werden.  
**/notify**  
Gibt an, dass Benachrichtigungen an alle sekundären Server gesendet werden.  
**/notifylist**  
Gibt an, dass Benachrichtigungen nur die Liste der Server gesendet werden. Dieser Befehl muss von einer IP-Adressen, die der Masterserver verwendet folgen.  
**<NotifyIPaddresses>**  
Gibt an, die IP-Adresse oder des sekundären Servers oder der Server, auf welche, die Änderung Benachrichtigungen gesendet werden. Diese Liste wird verwendet, nur mit der **/notifylist** Parameter. ### "Hinweise" – Verwenden der **Zoneresetsecondaries** Befehl auf dem Masterserver aus, um anzugeben, wie es auf zonenübertragungsanforderungen vom sekundären Server reagiert. ### Beispiel für die Verwendung
<pre>dnscmd dnssvr1.contoso.com /zoneresetsecondaries test.contoso.com /noxfr /nonotify  
dnscmd dnssvr1.contoso.com /zoneresetsecondaries test.contoso.com /securelist 11.0.0.2</pre>  
### <a name="BKMK_29"></a>dnscmd /zoneresettype  
Ändert den Typ der Zone. ### Syntax ```  
dnscmd [<ServerName>] /zoneresettype <ZoneName> <Zonetype> [/ Overwrite_mem | / OverWrite_Ds] ```  
#### Parameters  
**<ServerName>**  
Gibt den DNS-Server verwalten, dargestellt durch die Syntax für lokalen Computer, IP-Adresse, FQDN oder Hostnamen. Wenn dieser Parameter ausgelassen wird, wird der lokale Server verwendet.  
**<ZoneName>**  
Identifiziert die Zone, die auf der der Typ geändert werden.  
**<Zonetype>**  
Gibt den Typ der Zone zu erstellen. Jeder Typ verfügt über verschiedene erforderliche Parameter:  
**/dsprimary**  
erstellt eine active Directory integrierte Zone an.  
**/primary/File <FileName>**  
erstellt eine primäre Standardzone.  
**/sekundären <MasterIPaddress> [,<MasterIPaddress>...]**  
erstellt eine sekundäre Standardzone.  
**/stub <MasterIPaddress>[,<MasterIPaddress>...] / file <FileName>**  
erstellt eine Stubzone mit zugrunde liegender Datei.  
**/Dsstub <MasterIPaddress>[,<MasterIPaddress>...]**  
erstellt eine active Directory-integrierte Stub-Zone.  
**/Weiterleitung <MasterIPaddress[,<MasterIPaddress>]... / file<FileName>**  
Gibt an, dass die erstellte Zone nicht aufgelöste Abfragen an einen anderen DNS-Server weiterleitet.  
**/dsforwarder**  
Gibt an, dass die erstellten active Directory integrierte Zone nicht aufgelöste Abfragen an einen anderen DNS-Server weiterleitet.  
**/overwrite_mem | /overwrite_ds**  
Gibt an, wie vorhandene Daten überschrieben werden sollen:  
**/overwrite_mem**  
Überschreibt die DNS-Daten aus den Daten in AD DS.  
**/overwrite_ds**  
Überschreibt vorhandene Daten in AD DS. ### Geben Sie "Hinweise" – Festlegen der Zone als **/dsforwarder** erstellt eine Zone, die für die bedingte Weiterleitung ausführt. ### Beispiel für die Verwendung
<pre>dnscmd dnssvr1.contoso.com /zoneresettype test.contoso.com /primary /file test.contoso.com.dns  
dnscmd dnssvr1.contoso.com /zoneresettype second.contoso.com /secondary 10.0.0.2</pre>  
### <a name="BKMK_35"></a>dnscmd /zoneresume  
Startet eine bestimmte Zone, die zuvor angehalten wurde. #### Syntax ```  
dnscmd <ServerName> /zoneresume <ZoneName> ```  
#### Parameters  
**<ServerName>**  
Gibt an, den DNS-Server für die Verwaltung, durch die IP-Adresse, den FQDN oder Hostnamen dargestellt wird. Wenn dieser Parameter ausgelassen wird, wird der lokale Server verwendet.  
**<ZoneName>**  
Gibt den Namen der Zone, setzen Sie fort. ### Remarks - Sie können diesen Vorgang Umkehren der [Zonepause](#BKMK_27) Vorgang. ### Beispiel für die Verwendung `dnscmd dnssvr1.contoso.com /zoneresume test.contoso.com`  
### <a name="BKMK_36"></a>dnscmd /zoneupdatefromds  
Aktualisiert die angegebene active Directory integrierte Zone aus AD DS. ### Syntax ```  
dnscmd <ServerName> /zoneupdatefromds <ZoneName> ```  
#### Parameters  
**<ServerName>**  
Gibt an, den DNS-Server für die Verwaltung, durch die IP-Adresse, den FQDN oder Hostnamen dargestellt wird. Wenn dieser Parameter ausgelassen wird, wird der lokale Server verwendet.  
**<ZoneName>**  
Gibt den Namen der Zone zu aktualisieren. ### "Hinweise" - active Directory integrierte Zonen führen Sie dieses Update wird standardmäßig alle fünf Minuten. Um diesen Parameter zu ändern, verwenden die **Dnscmd Config Dspollinginterval** Befehl. ### Beispiel für die Verwendung `dnscmd dnssvr1.contoso.com /zoneupdatefromds`  
### <a name="BKMK_37"></a>dnscmd /zonewriteback  
Überprüft die DNS-Server-Arbeitsspeicher für die Änderungen, die auf eine bestimmte Zone relevant sind, und schreibt sie in den persistenten Speicher. #### Syntax ```  
dnscmd <ServerName> /zonewriteback <ZoneName> ```  
#### Parameters  
**<ServerName>**  
Gibt an, den DNS-Server für die Verwaltung, durch die IP-Adresse, den FQDN oder Hostnamen dargestellt wird. Wenn dieser Parameter ausgelassen wird, wird der lokale Server verwendet.  
**<ZoneName>**  
Gibt den Namen der Zone zu aktualisieren. ### Remarks - sieht ein Vorgang auf Zonenebene. Sie können alle Zonen auf einem DNS-Server mit aktualisieren die [Writebackfiles](#BKMK_21) Vorgang. ### Beispiel für die Verwendung `dnscmd dnssvr1.contoso.com /zonewriteback test.contoso.com`  
