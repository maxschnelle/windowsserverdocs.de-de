---
title: wecutil
description: Windows-Befehls Thema für wecutil, mit dem Sie Abonnements für Ereignisse erstellen und verwalten können, die von Remote Computern weitergeleitet werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0c82a6cb-d652-429c-9c3d-0f568c78d54b
author: coreyp-at-msft
ms.author: coreyp
manager: dansimps
ms.openlocfilehash: 2bb397ace7cc99c8b8d6bbed3598346ff2d0801c
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80829436"
---
# <a name="wecutil"></a>wecutil



Ermöglicht das Erstellen und Verwalten von Abonnements für Ereignisse, die von Remote Computern weitergeleitet werden. Der Remote Computer muss das WS-Management-Protokoll unterstützen. Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).


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

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|{es \| Enum-Abonnement}|Zeigt die Namen aller vorhandenen Remote Ereignis Abonnements an.|
|{GS \| Get-Abonnement} \<subid > [/f:\<Format >] [/Uni:\<Unicode >]|Zeigt Konfigurationsinformationen für Remote Abonnements an. \<subid > ist eine Zeichenfolge, die ein Abonnement eindeutig identifiziert. \<subid > ist identisch mit der Zeichenfolge, die im \<abonnementid >-Tags der XML-Konfigurationsdatei angegeben wurde, das zum Erstellen des Abonnements verwendet wurde.|
|{Gr \| Get-abonneptionruntimestatus} \<subid > [\<eventSource >...]|Zeigt den Lauf Zeit Status eines Abonnements an. \<subid > ist eine Zeichenfolge, die ein Abonnement eindeutig identifiziert. \<subid > ist identisch mit der Zeichenfolge, die im \<abonnementid >-Tags der XML-Konfigurationsdatei angegeben wurde, das zum Erstellen des Abonnements verwendet wurde. \<eventSource > ist eine Zeichenfolge, die einen Computer identifiziert, der als Quelle für Ereignisse fungiert. \<eventSource-> muss ein voll qualifizierter Domänen Name, ein NetBIOS-Name oder eine IP-Adresse sein.|
|{SS \| Set-Abonnement} \<subid > [/e: [\<subenabled >]] [/ESA:\<Address >] [/ESE: [\<srcenabled >]] [/AES] [/res] [/un:\<username >] [/up:\<Password >] [/d:\<DESC >] [/URI:\<URI >] [/cm:\<configmode >] [/ex:\<läuft >] [/q:\<Query >] [/Dia:\<Dialekt >] [/TN:\<TransportName >] [/TP:\<transportport >] [/DM:\<DeliveryMode >] [/DMI:\<deliverymax >] [/dmlt:\<deliverytime >] [/Hi:\<heartbeat >] [/CF:\<Content >] [/l :\<locale >] [/Ree: [\<readexist >]] [/LF:\<Logfile >] [/PN:\<PublisherName >] [/ESSP:\<enableport >] [/HN:\<Hostname >] [/CT:\<Type >]</br>oder</br>{SS \| Set-Abonnement/c:\<configfile > [/Cun:\<comusername >/Cup:\<compassword >]|Ändert die Abonnement Konfiguration. Sie können die Abonnement-ID und die entsprechenden Optionen zum Ändern von Abonnement Parametern angeben, oder Sie können eine XML-Konfigurationsdatei angeben, um die Abonnement Parameter zu ändern.|
|{CS \| Create-Abonnement} \<configfile > [/Cun:\<username >/Cup:\<Password >]|Erstellt ein Remote Abonnement. \<configfile > gibt den Pfad zur XML-Datei an, die die Abonnement Konfiguration enthält. Der Pfad kann absolut oder relativ zum aktuellen Verzeichnis sein.|
|{DS \| DELETE-Abonnement} \<subid >|Löscht ein Abonnement und abonniert alle Ereignis Quellen, die Ereignisse im Ereignisprotokoll für das Abonnement übermitteln. Alle Ereignisse, die bereits empfangen und protokolliert wurden, werden nicht gelöscht. \<subid > ist eine Zeichenfolge, die ein Abonnement eindeutig identifiziert. \<subid > ist identisch mit der Zeichenfolge, die im \<abonnementid >-Tags der XML-Konfigurationsdatei angegeben wurde, das zum Erstellen des Abonnements verwendet wurde.|
|{RS \| Retry-Abonnement} \<subid > [\<eventSource >...]|Es wird erneut versucht, eine Verbindung herzustellen und eine Remote Abonnement Anforderung an ein inaktives Abonnement zu senden. Versucht, alle Ereignis Quellen oder angegebenen Ereignis Quellen erneut zu aktivieren. Deaktivierte Quellen werden nicht wiederholt. \<subid > ist eine Zeichenfolge, die ein Abonnement eindeutig identifiziert. \<subid > ist identisch mit der Zeichenfolge, die im \<abonnementid >-Tags der XML-Konfigurationsdatei angegeben wurde, das zum Erstellen des Abonnements verwendet wurde. \<eventSource > ist eine Zeichenfolge, die einen Computer identifiziert, der als Quelle für Ereignisse fungiert. \<eventSource-> muss ein voll qualifizierter Domänen Name, ein NetBIOS-Name oder eine IP-Adresse sein.|
|{QC \| Quick-Config} [/q: [\<quiet >]]|Konfiguriert den Windows-Ereignis Sammlungs Dienst, um sicherzustellen, dass ein Abonnement durch Neustarts erstellt und aufrechterhalten werden kann. Dies umfasst die folgenden Schritte:</br>1. Aktivieren Sie den Kanal ForwardedEvents, wenn er deaktiviert ist.</br>2. Legen Sie den Windows-Ereignis Sammlungs Dienst auf verzögerten Start fest.</br>3. Starten Sie den Windows-Ereignis Sammler Dienst, wenn er nicht ausgeführt wird.|

## <a name="options"></a>Optionen

|Option|Beschreibung|
|------|-----------|
|/f:\<Format >|Gibt das Format der angezeigten Informationen an. \<Format > kann XML oder Terse sein. Wenn <Format> XML-Code ist, wird die Ausgabe im XML-Format angezeigt. Wenn \<Format > Terse ist, wird die Ausgabe in Name-Wert-Paaren angezeigt. Der Standardwert ist "Terse".|
|/c:\<configfile >|Gibt den Pfad zur XML-Datei an, die eine Abonnement Konfiguration enthält. Der Pfad kann absolut oder relativ zum aktuellen Verzeichnis sein. Diese Option kann nur mit den Optionen **/Cun** und **/Cup** verwendet werden und schließt sich gegenseitig mit allen anderen Optionen aus.|
|/e: [\<Abled >]|Aktiviert oder deaktiviert ein Abonnement. \<untergeordnete > kann "true" oder "false" sein. Der Standardwert dieser Option ist true.|
|/ESA:\<Adresse >|Gibt die Adresse einer Ereignis Quelle an. \<Address > ist eine Zeichenfolge, die einen voll qualifizierten Domänen Namen, einen NetBIOS-Namen oder eine IP-Adresse enthält, mit der ein Computer identifiziert wird, der als Quelle für Ereignisse fungiert. Diese Option sollte mit den Optionen **/ESE**, **/AES**, **/Res**oder **/UN** und **/up** verwendet werden.|
|/ESE: [\<srcenabled >]|Aktiviert oder deaktiviert eine Ereignis Quelle. \<srcenabled-> kann "true" oder "false" sein. Diese Option ist nur zulässig, wenn die **/ESA** -Option angegeben wird. Der Standardwert dieser Option ist true.|
|/aes|Fügt die Ereignis Quelle hinzu, die durch die **/ESA** -Option angegeben wird, wenn Sie nicht bereits Teil des Abonnements ist. Wenn die durch die Option **/ESA** angegebene Adresse bereits Teil des Abonnements ist, wird ein Fehler gemeldet. Diese Option ist nur zulässig, wenn die **/ESA** -Option angegeben wird.|
|/res|Entfernt die Ereignis Quelle, die durch die **/ESA** -Option angegeben wird, wenn Sie bereits Teil des Abonnements ist. Wenn die durch die Option **/ESA** angegebene Adresse nicht Teil des Abonnements ist, wird ein Fehler gemeldet. Diese Option ist nur zulässig, wenn die **/ESA** -Option angegeben wird.|
|/UN:\<Benutzername >|Gibt die Benutzer Anmelde Informationen an, die mit der von der **/ESA** -Option angegebenen Ereignis Quelle verwendet werden sollen. Diese Option ist nur zulässig, wenn die **/ESA** -Option angegeben wird.|
|/up:\<Kennwort >|Gibt das Kennwort an, das den Benutzer Anmelde Informationen entspricht. Diese Option ist nur zulässig, wenn die **/UN** -Option angegeben wird.|
|/d:\<->|Gibt eine Beschreibung für das Abonnement an.|
|/URI:\<-URI >|Gibt den Typ der Ereignisse an, die vom Abonnement genutzt werden. \<URI-> enthält eine URI-Zeichenfolge, die mit der Adresse des Ereignis Quell Computers kombiniert wird, um die Quelle der Ereignisse eindeutig zu identifizieren. Die URI-Zeichenfolge wird für alle Ereignis Quelladressen im Abonnement verwendet.|
|/cm:\<configmode >|Legt den Konfigurations Modus fest. \<configmode > kann eine der folgenden Zeichen folgen sein: normal, Benutzer definiert, minlatency oder minbandwidth. Die Modi "Normal", "minlatency" und "minbandwidth" legen den Übermittlungs Modus, maximale Übermittlungs Elemente, das Takt Intervall und die maximale Latenzzeit der Übermittlung Die Optionen **/DM**, **/DMI**, **/Hi** oder **/dmlt** können nur angegeben werden, wenn der Konfigurations Modus auf Custom festgelegt ist.|
|/Ex:\<läuft ab >|Legt die Uhrzeit fest, zu der das Abonnement abläuft. \<läuft ab > muss im XML-Standardformat oder im ISO8601-Datums-/Uhrzeitformat definiert werden: yyyy-mm-ddThh: mm: SS [. sss] [Z], wobei t das Zeit Trennzeichen und Z die UTC-Zeit angibt.|
|/q:\<Abfrage >|Gibt die Abfrage Zeichenfolge für das Abonnement an. Das Format \<Abfrage > kann für unterschiedliche URI-Werte unterschiedlich sein und gilt für alle Quellen im Abonnement.|
|/Dia:\<Dialekt >|Definiert den Dialekt, der von der Abfrage Zeichenfolge verwendet wird.|
|/TN:\<TransportName >|Gibt den Namen des Transports an, der verwendet wird, um eine Verbindung mit einer Remote Ereignis Quelle herzustellen.|
|/TP:\<transportport >|Legt die Portnummer fest, die vom Transport verwendet wird, wenn eine Verbindung mit einer Remote Ereignis Quelle hergestellt wird.|
|/DM:\<DeliveryMode >|Gibt den Übermittlungs Modus an. \<DeliveryMode-> kann entweder Pull oder Push sein. Diese Option ist nur gültig, wenn die **/cm** -Option auf Custom festgelegt ist.|
|/DMI:\<deliverymax >|Legt die maximale Anzahl von Elementen für die Batch Übermittlung fest. Diese Option ist nur gültig, wenn **/cm** auf Custom festgelegt ist.|
|/dmlt:\<deliverytime >|Legt die maximale Latenzzeit bei der Übermittlung eines Ereignis Batches fest. \<deliverytime > die Anzahl der Millisekunden. Diese Option ist nur gültig, wenn **/cm** auf Custom festgelegt ist.|
|/Hi:\<Takt >|Definiert das Takt Intervall. \<Takt > ist die Anzahl von Millisekunden. Diese Option ist nur gültig, wenn **/cm** auf Custom festgelegt ist.|
|/CF:\<Inhalt >|Gibt das Format der zurückgegebenen Ereignisse an. \<Inhalts > können Ereignisse oder renderedtext sein. Wenn der Wert renderedtext lautet, werden die Ereignisse mit den lokalisierten Zeichen folgen (z. b. Ereignis Beschreibung) zurückgegeben, die an das Ereignis angefügt sind. Der Standardwert ist renderedtext.|
|/l:\<Gebiets Schema >|Gibt das Gebiets Schema für die Übermittlung der lokalisierten Zeichen folgen im renderedtext-Format an. \<Gebiets Schema > ist eine Sprach-und Länder-/Regions-Bezeichner, z. b. en-US. Diese Option ist nur gültig, wenn die **/CF** -Option auf renderedtext festgelegt ist.|
|/Ree: [\<readexist >]|Identifiziert die Ereignisse, die für das Abonnement übermittelt werden. \<readexist-> kann true oder false sein. Wenn die <Readexist> true ist, werden alle vorhandenen Ereignisse aus den Abonnement Ereignis Quellen gelesen. Wenn die <Readexist> false ist, werden nur zukünftige (eingehende) Ereignisse übermittelt. Der Standardwert für eine **/Ree** -Option ohne Wert ist true. Wenn keine **/Ree** -Option angegeben wird, ist der Standardwert false.|
|/LF:\<Protokolldatei >|Gibt das lokale Ereignisprotokoll an, das verwendet wird, um Ereignisse zu speichern, die von den Ereignis Quellen empfangen werden.|
|/PN:\<PublisherName >|Gibt den Herausgeber Namen an. Es muss sich um einen Verleger handeln, der das von der **/LF** -Option angegebene Protokoll besitzt oder importiert.|
|/ESSP:\<enableport >|Gibt an, dass die Portnummer an den Dienst Prinzipal Namen des Remote Dienstanbieter angehängt werden muss. \<enableport-> kann "true" oder "false" sein. Die Portnummer wird angehängt, wenn <Enableport> den Wert true hat. Wenn die Portnummer angehängt wird, sind möglicherweise einige Konfigurationen erforderlich, um zu verhindern, dass der Zugriff auf die Ereignis Quellen verweigert wird.|
|/HN:\<Hostname >|Gibt den DNS-Namen des lokalen Computers an. Dieser Name wird von der Remote Ereignis Quelle zum Zurücksetzen von Ereignissen verwendet und darf nur für ein Pushabonnement verwendet werden.|
|/CT:\<Typ >|Legt den Anmelde Informationstyp für den Remote Quell Zugriff fest. \<Typ > muss einer der folgenden Werte sein: Default, Aushandlungs, Digest, Basic oder LocalMachine. Der Standardwert ist default.|
|/Cun:\<comusername >|Legt die freigegebenen Benutzer Anmelde Informationen fest, die für Ereignis Quellen verwendet werden sollen, die über keine eigenen Benutzer Anmelde Informationen verfügen. Wenn diese Option mit der **/c** -Option angegeben wird, werden die Einstellungen für Benutzername und Benutzer Kennwort für die einzelnen Ereignis Quellen der Konfigurationsdatei ignoriert. Wenn Sie für eine bestimmte Ereignis Quelle andere Anmelde Informationen verwenden möchten, sollten Sie diesen Wert überschreiben, indem Sie die Optionen **/UN** und **/up** für eine bestimmte Ereignis Quelle in der Befehlszeile eines anderen **SS** -Befehls angeben.|
|/Cup:\<compassword >|Legt das Benutzer Kennwort für die freigegebenen Benutzer Anmelde Informationen fest. Wenn \<compassword-> auf * (Sternchen) festgelegt ist, wird das Kennwort aus der Konsole gelesen. Diese Option ist nur gültig, wenn die **/Cun** -Option angegeben wird.|
|/q: [\<quiet >]|Gibt an, ob die Konfigurations Prozedur zur Bestätigung aufgefordert wird. \<quiet > kann "true" oder "false" sein. Wenn <Quiet> den Wert true hat, wird die Konfigurations Prozedur nicht zur Bestätigung aufgefordert. Der Standardwert dieser Option ist false.|

## <a name="remarks"></a>Hinweise

> [!IMPORTANT]
> Wenn Sie die Meldung erhalten, dass der RPC-Server nicht verfügbar ist? Wenn Sie versuchen, wecutil auszuführen, müssen Sie den Windows-Ereignis Sammlungs Dienst (Wecsvc) starten. Um Wecsvc zu starten, geben Sie an einer Eingabeaufforderung mit erhöhten Rechten net Start Wecsvc ein.

- Das folgende Beispiel zeigt den Inhalt einer Konfigurationsdatei:  
  ```
  <Subscription xmlns=https://schemas.microsoft.com/2006/03/windows/events/subscription>
  <Uri>https://schemas.microsoft.com/wbem/wsman/1/windows/EventLog</Uri>
  <!-- Use Normal (default), Custom, MinLatency, MinBandwidth -->
  <ConfigurationMode>Normal</ConfigurationMode>
  <Description>Forward Sample Subscription</Description>
  <SubscriptionId>SampleSubscription</SubscriptionId>
  <Query><![CDATA[
  <QueryList>
  <Query Path=Application>
  <Select>*</Select>
  </Query>
  </QueryList>
  ]]></Query>
  <EventSources>
  <EventSource Enabled=true>
  <Address>mySource.myDomain.com</Address>
  <UserName>myUserName</UserName>
  <Password>*</Password>
  </EventSource>
  </EventSources>
  <CredentialsType>Default</CredentialsType>
  <Locale Language=EN-US></Locale>
  </Subscription>
  ```

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Ausgabe Konfigurationsinformationen für ein Abonnement mit dem Namen Sub1:
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
Anzeigen des Lauf Zeit Status eines Abonnements mit dem Namen Sub1:
```
wecutil gr sub1
```
Aktualisieren Sie die Abonnement Konfiguration mit dem Namen Sub1 aus einer neuen XML-Datei mit dem Namen WsSelRg2. XML:
```
wecutil ss sub1 /c:%Windir%\system32\WsSelRg2.xml
```
Aktualisieren Sie die Abonnement Konfiguration mit dem Namen sub2 mit mehreren Parametern:
```
wecutil ss sub2 /esa:myComputer /ese /un:uname /up:* /cm:Normal
```
Erstellen Sie ein Abonnement, um Ereignisse aus einem Windows Vista-Anwendungs Ereignisprotokoll eines Remote Computers unter MySource.mydomain.com an das ForwardedEvents-Protokoll weiterzuleiten (Weitere Informationen finden Sie in den Hinweisen zu einem Beispiel für eine Konfigurationsdatei):
```
wecutil cs subscription.xml
```
Löschen Sie ein Abonnement mit dem Namen Sub1:
```
wecutil ds sub1
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
