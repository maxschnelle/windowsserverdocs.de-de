---
title: wecutil
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0c82a6cb-d652-429c-9c3d-0f568c78d54b
author: coreyp-at-msft
ms.author: coreyp
manager: dansimps
ms.openlocfilehash: 04fb86d813049dc5f0aa6d4fba51e45dccbd1b80
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66440179"
---
# <a name="wecutil"></a>wecutil



Ermöglicht Ihnen das Erstellen und Verwalten von Abonnements für Ereignisse, die weitergeleitet werden, der von Remotecomputern. Der Remotecomputer muss das WS-Management-Protokoll unterstützen. Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).


## <a name="syntax"></a>Syntax

```
wecutil  [{es | enum-subscription}] 
[{gs | get-subscription} <Subid> [/f:<Format>] [/uni:<Unicode>]] 
[{gr | get-subscriptionruntimestatus} <Subid> [<Eventsource> …]] 
[{ss | set-subscription} [<Subid> [/e:[<Subenabled>]] [/esa:<Address>] [/ese:[<Srcenabled>]] [/aes] [/res] [/un:<Username>] [/up:<Password>] [/d:<Desc>] [/uri:<Uri>] [/cm:<Configmode>] [/ex:<Expires>] [/q:<Query>] [/dia:<Dialect>] [/tn:<Transportname>] [/tp:<Transportport>] [/dm:<Deliverymode>] [/dmi:<Deliverymax>] [/dmlt:<Deliverytime>] [/hi:<Heartbeat>] [/cf:<Content>] [/l:<Locale>] [/ree:[<Readexist>]] [/lf:<Logfile>] [/pn:<Publishername>] [/essp:<Enableport>] [/hn:<Hostname>] [/ct:<Type>]] [/c:<Configfile> [/cun:<Username> /cup:<Password>]]] 
[{cs | create-subscription} <Configfile> [/cun:<Username> /cup:<Password>]] 
[{ds | delete-subscription} <Subid>] 
[{rs | retry-subscription} <Subid> [<Eventsource>…]] 
[{qc | quick-config} [/q:[<Quiet>]]].
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|{es \| Enum-Subscription}|Zeigt die Namen aller remoteereignis-Abonnements, die vorhanden sind.|
|{gs \| Get-Subscription} \<Subid > [/ f:\<Format >] [/ Uni:\<Unicode >]|Zeigt die Konfigurationsinformationen für die remote-Abonnement. \<Subid > ist eine Zeichenfolge, die ein Abonnement eindeutig identifiziert. \<Subid > ist identisch mit die Zeichenfolge, die im angegebenen die \<SubscriptionId >-Tag der XML-Konfigurationsdatei, die zum Erstellen des Abonnements verwendet wurde.|
|{Gr \| Get-Subscriptionruntimestatus} \<Subid > [\<Eventsource >...]|Zeigt den runtimestatus eines Abonnements. \<Subid > ist eine Zeichenfolge, die ein Abonnement eindeutig identifiziert. \<Subid > ist identisch mit die Zeichenfolge, die im angegebenen die \<SubscriptionId >-Tag der XML-Konfigurationsdatei, die zum Erstellen des Abonnements verwendet wurde. \<EventSource > ist eine Zeichenfolge, die einen Computer identifiziert, die als Quelle von Ereignissen dient. \<EventSource > muss einen vollqualifizierten Domänennamen, einen NetBIOS-Namen oder eine IP-Adresse.|
|{ss \| Set-Subscription} \<Subid > [/ e: [\<Subenabled >]] [/ Esa:\<Adresse >] [/ ese: [\<Srcenabled >]] [/aes] [/ Res] [/ aufheben:\<Benutzername >] [/ bis:\< Kennwort >] [/ d:\<Desc >] [/ Uri:\<Uri >] [/ cm:\<Configmode >] [/ ex:\<Expires >] [/ f:\<Abfrage >] [/ Dia:\<Dialekt >] [/ tn:\< TransportName >] [/ Tp:\<Transportport >] [/ dm:\<Deliverymode >] [/ Dmi:\<Deliverymax >] [/ Dmlt:\<Deliverytime >] [/ Hallo:\<Takt >] [/ Cf:\< Content >] [/ l:\<Gebietsschema >] [/ Ree: [\<Readexist >]] [/ lf:\<Protokolldatei >] [/ Pn:\<Publishername >] [/ Essp:\<Enableport >] [/ hn:\< Hostname >] [/ ct:\<Typ >]</br>oder</br>{ss \| Set-Subscription/c:\<Configfile > [/ Cun:\<Comusername >/Cup:\<Compassword >]|Ändert die Konfiguration des Abonnements an. Sie können die Abonnement-ID und die entsprechenden Optionen zum Ändern der Parameter für Abonnements angeben, oder Sie können eine XML-Konfigurationsdatei zum Ändern der Parameter für Abonnements angeben.|
|{Cs \| erstellen-Subscription} \<Configfile > [/ Cun:\<Benutzername >/Cup:\<Kennwort >]|Erstellt eine remote-Abonnement. \<ConfigFile > Gibt den Pfad der XML-Datei, die die Konfiguration des Abonnements enthält. Der Pfad kann absolut oder relativ zum aktuellen Verzeichnis sein.|
|{ds \| Delete-Subscription} \<Subid >|Löscht ein Abonnement aus, und hebt das Abonnement vom alle Ereignisquellen, die Ereignisse im Ereignisprotokoll für das Abonnement zu übermitteln. Alle Ereignisse, die bereits empfangen und protokolliert werden nicht gelöscht werden. \<Subid > ist eine Zeichenfolge, die ein Abonnement eindeutig identifiziert. \<Subid > ist identisch mit die Zeichenfolge, die im angegebenen die \<SubscriptionId >-Tag der XML-Konfigurationsdatei, die zum Erstellen des Abonnements verwendet wurde.|
|{Rs \| Retry-Subscription} \<Subid > [\<Eventsource >...]|Zum Herstellen einer Verbindung und senden Sie eine remote abonnementanforderung an ein inaktives Abonnement wiederholt. Versucht, alle Ereignisquellen reaktivieren oder Ereignisquellen angegeben. Deaktivierte Quellen werden nicht erneut versucht. \<Subid > ist eine Zeichenfolge, die ein Abonnement eindeutig identifiziert. \<Subid > ist identisch mit die Zeichenfolge, die im angegebenen die \<SubscriptionId >-Tag der XML-Konfigurationsdatei, die zum Erstellen des Abonnements verwendet wurde. \<EventSource > ist eine Zeichenfolge, die einen Computer identifiziert, die als Quelle von Ereignissen dient. \<EventSource > muss einen vollqualifizierten Domänennamen, einen NetBIOS-Namen oder eine IP-Adresse.|
|{qc \| Quick-Config} [/ f: [\<Quiet >]]|Konfiguriert den Windows Event Collector-Dienst, um sicherzustellen, dass ein Abonnement erstellt und Neustarts aufrechterhalten werden kann. Dies umfasst die folgenden Schritte aus:</br>1.  Aktivieren Sie den Protokoll "ForwardedEvents"-Kanal, wenn er deaktiviert ist.</br>2.  Legen Sie die Windows-Ereignissammlungsdienst Start zu verzögern.</br>3.  Starten Sie den Windows Event Collector-Dienst aus, wenn er nicht ausgeführt wird.|

## <a name="options"></a>Optionen

|Option|Beschreibung|
|------|-----------|
|/f:\<Format>|Gibt das Format der Informationen, die angezeigt wird. \<Format > kann sein, XML oder Terse. Wenn <Format> XML ist, wird die Ausgabe im XML-Format angezeigt. Wenn \<Format > Terse, wird die Ausgabe wird angezeigt, in dem Name-Wert-Paaren. Der Standardwert ist Terse.|
|/c:\<Configfile>|Gibt den Pfad der XML-Datei, die eine abonnementkonfiguration enthält. Der Pfad kann absolut oder relativ zum aktuellen Verzeichnis sein. Diese Option kann nur verwendet werden, mit der **/cun** und **/Cup** "Optionen", und ist mit allen anderen Optionen gegenseitig.|
|e: [\<Subenabled >]|Aktiviert oder deaktiviert ein Abonnement. \<Subenabled > kann "true" oder "false" sein. Der Standardwert für diese Option ist "true".|
|/esa:\<Address>|Gibt die Adresse einer Ereignisquelle. \<Adresse > ist eine Zeichenfolge, enthält einen vollständig qualifizierten Domänennamen, einen NetBIOS-Namen oder IP-Adresse, die einen Computer identifiziert, die als Quelle von Ereignissen dient. Diese Option sollte verwendet werden, mit der **/ese**, **/aes**, **/res**, oder **/un** und **/up** Optionen.|
|/ESE: [\<Srcenabled >]|Aktiviert oder deaktiviert eine Ereignisquelle. \<Srcenabled > kann "true" oder "false" sein. Diese Option ist nur zulässig, wenn die **/esa** angegeben wird. Der Standardwert für diese Option ist "true".|
|/AES|Fügt die Ereignisquelle, die angegeben wird die **/esa** option, wenn sie nicht bereits ein Teil des Abonnements ist. Wenn die Adresse, wird angegeben die **/esa** Option ist bereits Teil des Abonnements, wird ein Fehler gemeldet. Diese Option ist nur zulässig, wenn die **/esa** angegeben wird.|
|/ Res|Entfernt die Ereignisquelle, die angegeben wird die **/esa** option, wenn es bereits einen Teil des Abonnements ist. Wenn die Adresse, wird angegeben die **/esa** Option ist nicht Teil des Abonnements, wird ein Fehler gemeldet. Diese Option ist nur zulässig, wenn **/esa** angegeben wird.|
|/un:\<Benutzername >|Gibt an, die Anmeldeinformationen des Benutzers für die Verwendung mit der Ereignisquelle, die gemäß der **/esa** Option. Diese Option ist nur zulässig, wenn die **/esa** angegeben wird.|
|/ up:\<Kennwort >|Gibt das Kennwort, das die Anmeldeinformationen des Benutzers entspricht. Diese Option ist nur zulässig, wenn die **/un** angegeben wird.|
|/d:\<Desc>|Enthält eine Beschreibung für das Abonnement.|
|/uri:\<Uri>|Gibt den Typ der Ereignisse, die das Abonnement verwendet werden. \<URI > enthält eine URI-Zeichenfolge, die mit der Adresse des Ereignisquellcomputers zur eindeutigen Identifizierung der Quelle der Ereignisse kombiniert wird. Die URI-Zeichenfolge wird für alle Adressen der Ereignis-Quelle in das Abonnement verwendet.|
|/cm:\<Configmode>|Legt fest, den Konfigurationsmodus zu wechseln. \<Configmode > kann eine der folgenden Zeichenfolgen: Normal "," Benutzerdefiniert "," MinLatency "oder" MinBandwidth ". Die normale MinLatency und MinBandwidth Modi festgelegt Übermittlungsmodus, maximale Delivery-Elemente, Taktintervall und maximale Wartezeit Übermittlungszeit. Die **/dm**, **/dmi**, **/hi** oder **/dmlt** Optionen möglicherweise nur angegeben, wenn es sich bei der Konfigurationsmodus auf Custom festgelegt ist.|
|/ ex:\<abläuft >|Legt fest, die Uhrzeit des Abonnements abläuft. \<Läuft ab > sollte im XML-Index oder ISO8601 DateTime-Standardformat definiert werden: JJJJ-MM-TTThh [.sss] [Z], wobei "T" ist das Trennzeichen für Zeitangaben und UTC-Zeit "Z" steht.|
|/q:\<Query>|Gibt die Abfragezeichenfolge für das Abonnement an. Das Format der \<Abfrage > kann für andere URI-Werte unterschiedlich sein und gilt für alle Quellen im Abonnement.|
|/Dia:\<Dialekt >|Definiert den Dialekt, den die Abfragezeichenfolge verwendet.|
|TN:\<Transportname >|Gibt den Namen des Transports, die zur Verbindung mit einer remote-Ereignisquelle verwendet wird.|
|/ TP:\<Transportport >|Legt fest, die Nummer des Ports, die vom Transport verwendet wird, wenn eine remote-Ereignisquelle zu verbinden.|
|/dm:\<Deliverymode>|Gibt den Übermittlungsmodus. \<DeliveryMode > kann sein, Pull- oder pushmodus. Diese Option ist nur gültig Wenn der **/cm** Option wird auf Custom festgelegt.|
|/dmi:\<Deliverymax>|Legt die maximale Anzahl von Elementen für die im Batchmodus Übermittlung fest. Diese Option ist nur gültig Wenn **/cm** wird auf Custom festgelegt.|
|/dmlt:\<Deliverytime>|Legt die maximale Latenz bei der Bereitstellung eines Batches von Ereignissen fest. \<Deliverytime > ist die Anzahl der Millisekunden. Diese Option ist nur gültig Wenn **/cm** wird auf Custom festgelegt.|
|/hi:\<Heartbeat>|Definiert das Taktintervall fest. \<Takt > ist die Anzahl der Millisekunden. Diese Option ist nur gültig Wenn **/cm** wird auf Custom festgelegt.|
|/ CF:\<content >|Gibt das Format der Ereignisse, die zurückgegeben werden. \<Content > kann sein, Ereignisse oder RenderedText. Wenn der Wert RenderedText ist, werden die Ereignisse mit den lokalisierten Zeichenfolgen (z. B. die Beschreibung des Ereignisses), der dem Ereignis zugeordnet zurückgegeben. Der Standardwert ist RenderedText.|
|/l:\<Locale>|Gibt das Gebietsschema für die Übermittlung von lokalisierten Zeichenfolgen im RenderedText-Format an. \<Gebietsschema > ist ein Sprache und Land/Region-Bezeichner, z. B. "EN-us". Diese Option ist nur gültig Wenn der **/CF** RenderedText Option festgelegt.|
|/Ree: [\<Readexist >]|Identifiziert die Ereignisse, die für das Abonnement übermittelt werden. \<Readexist > kann "true" oder "false". Wenn die <Readexist> true ist, werden alle vorhandenen Ereignisse aus dem Abonnement-Ereignisquellen gelesenen. Wenn die <Readexist> ist "false" erst auf zukünftige (eingehenden) Ereignisse übermittelt werden. Der Standardwert ist "true" für eine **/ree** Option keinen Wert. Wenn kein **/ree** angegeben wird, der Standardwert ist "false".|
|/lf:\<Logfile>|Gibt an, das lokale Ereignisprotokoll, das zum Speichern von Ereignissen aus Ereignisquellen empfangen verwendet wird.|
|/ PN:\<Publishername >|Gibt den Herausgebernamen an. Es muss sich auf einen Verleger, die der Besitzer ist oder importiert das Protokoll, das gemäß der **/LF** Option.|
|/essp:\<Enableport >|Gibt an, dass die Nummer des Ports an den Dienstprinzipalnamen des Remotediensts angefügt werden muss. \<Enableport > kann "true" oder "false" sein. Die Portnummer wird angefügt. wenn <Enableport> ist "true". Wenn die Nummer des Ports angefügt wird, möglicherweise einige Konfigurationsschritte erforderlich, um zu verhindern, dass den Zugriff auf Ereignisquellen von verweigert wird.|
|/hn:\<Hostname>|Gibt den DNS-Namen des lokalen Computers. Dieser Name wird von remote-Ereignisquelle Pushback Ereignisse verwendet und muss nur bei einem Pushabonnement verwendet werden.|
|/ CT:\<Typ >|Legt den Typ der Anmeldeinformationen für den Remotequelle Zugriff fest. \<Typ > sollte einen der folgenden Werte sein: Standard, negotiate und digest, Basic "oder" Localmachine. Der Standardwert ist die Standardeinstellung.|
|/CUN:\<Comusername >|Legt fest, die freigegebene Benutzeranmeldeinformationen für Ereignisquellen verwendet werden, die nicht mit ihrer eigenen Anmeldeinformationen verfügen. Wenn diese Option angegeben wird, mit der **/c** option, UserName und UserPassword-Einstellungen für die einzelnen Ereignisquellen aus der Konfigurationsdatei ignoriert werden. Wenn Sie andere Anmeldeinformationen für ein bestimmtes Ereignis-Quelle verwenden möchten, sollten Sie diesen Wert überschreiben, durch Angabe der **/un** und **/up** Optionen für eine bestimmte Ereignisquelle in der Befehlszeile von einem anderen **ss** Befehl.|
|/ Cup:\<Compassword >|Legt fest, das Benutzerkennwort für die freigegebene Benutzeranmeldeinformationen. Wenn \<Compassword > nastaven NA hodnotu * (Sternchen), das Kennwort wird in der Konsole gelesen. Diese Option ist nur gültig, wenn die **/cun** angegeben wird.|
|/q:[\<Quiet>]|Gibt an, ob die Verfahren zur Bestätigung aufgefordert. \<Quiet > kann "true" oder "false" sein. Wenn <Quiet> ist "true", welches Konfigurationsverfahren nicht zur Bestätigung aufgefordert. Der Standardwert für diese Option ist "false".|

## <a name="remarks"></a>Hinweise

> [!IMPORTANT]
> Wenn Sie die Meldung erhalten "der RPC-Server ist nicht verfügbar? Wenn Sie versuchen, Wecutil ausführen, müssen Sie den Windows Event Collector-Dienst (Wecsvc) zu starten. Um Wecsvc zu starten, starten Sie an einer Eingabeaufforderung mit erhöhten Rechten Folgendes net Wecsvc.

- Das folgende Beispiel zeigt den Inhalt einer Konfigurationsdatei:  
  ```
  <Subscription xmlns="https://schemas.microsoft.com/2006/03/windows/events/subscription">
  <Uri>https://schemas.microsoft.com/wbem/wsman/1/windows/EventLog</Uri>
  <!-- Use Normal (default), Custom, MinLatency, MinBandwidth -->
  <ConfigurationMode>Normal</ConfigurationMode>
  <Description>Forward Sample Subscription</Description>
  <SubscriptionId>SampleSubscription</SubscriptionId>
  <Query><![CDATA[
  <QueryList>
  <Query Path="Application">
  <Select>*</Select>
  </Query>
  </QueryList>
  ]]></Query>
  <EventSources>
  <EventSource Enabled="true">
  <Address>mySource.myDomain.com</Address>
  <UserName>myUserName</UserName>
  <Password>*</Password>
  </EventSource>
  </EventSources>
  <CredentialsType>Default</CredentialsType>
  <Locale Language="EN-US"></Locale>
  </Subscription>
  ```

## <a name="BKMK_examples"></a>Beispiele für

Ausgabe-Konfigurationsinformationen für ein Abonnement mit der Bezeichnung sub1:
```
wecutil gs sub1
```
Beispielausgabe:
```
EventSource[0]:
Address: localhost
Enabled: true
Description: Subscription 1
Uri: wsman:microsoft/logrecord/sel
DeliveryMode: pull
DeliveryMaxSize: 16000
DeliveryMaxItems: 15
DeliveryMaxLatencyTime: 1000
HeartbeatInterval: 10000
Locale:
ContentFormat: renderedtext
LogFile: HardwareEvents
```
Anzeigen des Laufzeitstatus eines Abonnements, die mit der Bezeichnung sub1:
```
wecutil gr sub1
```
Aktualisieren Sie die Konfiguration des Abonnements, die mit der Bezeichnung sub1 aus einer neuen XML-Datei WsSelRg2.xml aufgerufen:
```
wecutil ss sub1 /c:%Windir%\system32\WsSelRg2.xml
```
Aktualisieren Sie die Konfiguration des Abonnements, die mit dem Namen sub2 mit mehreren Parametern:
```
wecutil ss sub2 /esa:myComputer /ese /un:uname /up:* /cm:Normal
```
Erstellen eines Abonnements zum Weiterleiten von Ereignissen aus einem Ereignisprotokoll von Windows Vista-Anwendung eines Remotecomputers unter mySource.myDomain.com in das Protokoll "ForwardedEvents"-Protokoll (siehe "Hinweise" ein Beispiel einer Konfigurationsdatei):
```
wecutil cs subscription.xml
```
Löschen Sie ein Abonnement namens sub1:
```
wecutil ds sub1
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
