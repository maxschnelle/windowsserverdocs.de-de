---
title: ipconfig
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 15071c2c-4815-4893-93b2-ab30232e312e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a4098da4e2ffb94db8cc1fa65b1cec69f5233f05
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724822"
---
# <a name="ipconfig"></a>ipconfig



Zeigt alle aktuellen TCP/IP-Netzwerk Konfigurationswerte an und aktualisiert Einstellungen für das Dynamic Host Configuration-Protokoll (DHCP) und die Domain Name System (DNS). Wird ohne Parameter verwendet, zeigt **ipconfig** IPv4 (Internet Protocol Version 4) und IPv6-Adressen, die Subnetzmaske und das Standard Gateway für alle Adapter an.

## <a name="syntax"></a>Syntax

```
ipconfig [/allcompartments] [/all] [/renew [<Adapter>]] [/release [<Adapter>]] [/renew6[<Adapter>]] [/release6 [<Adapter>]] [/flushdns] [/displaydns] [/registerdns] [/showclassid <Adapter>] [/setclassid <Adapter> [<ClassID>]]
```

#### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|/all|Zeigt die vollständige TCP/IP-Konfiguration für alle Adapter an. Adapter können für physikalische Schnittstellen, z. B. installierte Netzwerkadapter, oder logische Schnittstellen stehen, z. B. DFÜ-Verbindungen.|
|/allcompartments|Zeigt die vollständige TCP/IP-Konfiguration für alle Depots an.|
|/displaydns|Zeigt den Inhalt des DNS-Client Auflösungs Caches an. dieser enthält sowohl Einträge, die vorab aus der lokalen Hostdatei geladen wurden, als auch alle zuletzt erhaltenen Ressourcen Einträge für namens Abfragen, die vom Computer aufgelöst wurden. Der DNS-Client Dienst verwendet diese Informationen, um häufig abgefragte Namen schnell zu beheben, bevor die konfigurierten DNS-Server abgefragt werden.|
|/flushdns|Leert den Inhalt des DNS-Client Auflösungs Caches und setzt ihn zurück. Bei der DNS-Problembehandlung können Sie mithilfe dieses Verfahrens negative Cache Einträge aus dem Cache sowie alle anderen Einträge, die dynamisch hinzugefügt wurden, verwerfen.|
|/registerdns|Initiiert die manuelle dynamische Registrierung für die DNS-Namen und IP-Adressen, die auf einem Computer konfiguriert sind. Sie können diesen Parameter verwenden, um Probleme mit einer fehlgeschlagenen DNS-Namens Registrierung zu beheben oder ein dynamisches Update Problem zwischen einem Client und dem DNS-Server aufzulösen, ohne den Client Computer neu starten zu müssen. Die DNS-Einstellungen in den erweiterten Eigenschaften des TCP/IP-Protokolls bestimmen, welche Namen in DNS registriert sind.|
|/Release [\<Adapter>]|Sendet eine DHCPRELEASE-Meldung an den DHCP-Server, um die aktuelle DHCP-Konfiguration freizugeben und die IP-Adress Konfiguration für alle Adapter (wenn kein Adapter angegeben ist) oder für einen bestimmten Adapter zu verwerfen, wenn der *Adapter* Parameter enthalten ist. Dieser Parameter deaktiviert TCP/IP für Adapter, die so konfiguriert sind, dass eine IP-Adresse automatisch abgerufen wird. Wenn Sie einen Adapter Namen angeben möchten, geben Sie den Namen des Adapters ein, der angezeigt wird, wenn Sie **ipconfig** ohne Parameter verwenden.|
|/release6 [\<Adapter>]|Sendet eine DHCPRELEASE-Meldung an den DHCPv6-Server zum Freigeben der aktuellen DHCP-Konfiguration und verwerfen der IPv6-Adress Konfiguration für alle Adapter (wenn kein Adapter angegeben ist) oder für einen bestimmten Adapter, wenn der *Adapter* Parameter enthalten ist. Dieser Parameter deaktiviert TCP/IP für Adapter, die so konfiguriert sind, dass eine IP-Adresse automatisch abgerufen wird. Wenn Sie einen Adapter Namen angeben möchten, geben Sie den Namen des Adapters ein, der angezeigt wird, wenn Sie **ipconfig** ohne Parameter verwenden.|
|/Renew [\<Adapter>]|Erneuert die DHCP-Konfiguration für alle Adapter (wenn kein Adapter angegeben ist) oder für einen bestimmten Adapter, wenn der *Adapter* Parameter enthalten ist. Dieser Parameter ist nur auf Computern mit Adaptern verfügbar, die so konfiguriert sind, dass eine IP-Adresse automatisch abgerufen wird. Wenn Sie einen Adapter Namen angeben möchten, geben Sie den Namen des Adapters ein, der angezeigt wird, wenn Sie **ipconfig** ohne Parameter verwenden.|
|/renew6 [\<Adapter>]|Erneuert die DHCPv6-Konfiguration für alle Adapter (wenn kein Adapter angegeben ist) oder für einen bestimmten Adapter, wenn der *Adapter* Parameter enthalten ist. Dieser Parameter ist nur auf Computern mit Adaptern verfügbar, die so konfiguriert sind, dass eine IPv6-Adresse automatisch abgerufen wird. Wenn Sie einen Adapter Namen angeben möchten, geben Sie den Namen des Adapters ein, der angezeigt wird, wenn Sie **ipconfig** ohne Parameter verwenden.|
|/setclassid \<Adapter> [ <ClassID>]|Konfiguriert die DHCP-Klassen-ID für einen angegebenen Adapter. Um die DHCP-Klassen-ID für alle Adapter festzulegen, verwenden Sie das Platzhalter Zeichen (**&#42;**) anstelle des- *Adapters*. Dieser Parameter ist nur auf Computern mit Adaptern verfügbar, die so konfiguriert sind, dass eine IP-Adresse automatisch abgerufen wird. Wenn keine DHCP-Klassen-ID angegeben ist, wird die aktuelle Klassen-ID entfernt.|
|/showclassid \<Adapter>|Zeigt die DHCP-Klassen-ID für einen angegebenen Adapter an. Um die DHCP-Klassen-ID für alle Adapter anzuzeigen, verwenden Sie das Platzhalter Zeichen (**&#42;**) anstelle des *Adapters*. Dieser Parameter ist nur auf Computern mit Adaptern verfügbar, die so konfiguriert sind, dass eine IP-Adresse automatisch abgerufen wird.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Bemerkungen

- Dieser Befehl ist besonders nützlich auf Computern, die so konfiguriert sind, dass eine IP-Adresse automatisch abgerufen wird. Dadurch können Benutzer bestimmen, welche TCP/IP-Konfigurationswerte von DHCP, der automatischen privaten IP-Adressierung (APIPA) oder einer alternativen Konfiguration konfiguriert wurden.
- Wenn der von Ihnen für den *Adapter* bereitgestellte Name Leerzeichen enthält, verwenden Sie Anführungszeichen um den Adapter Namen (Beispiel: * * * *<em>Adapter Name</em>* * * *).
- Bei Adapter Namen unterstützt **ipconfig** die Verwendung des Platzhalter Zeichens\*Sternchen (), um entweder Adapter mit Namen anzugeben, die mit einer angegebenen Zeichenfolge beginnen, bzw. Adapter mit Namen, die eine angegebene Zeichenfolge enthalten. Beispielsweise findet **local\* ** Übereinstimmungen mit allen Adaptern, die mit der Zeichenfolge local beginnen, und ** \*con\* ** mit allen Adaptern überein, die die Zeichenfolge con enthalten

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um die grundlegende TCP/IP-Konfiguration für alle Adapter anzuzeigen:
```
ipconfig
```
Geben Sie Folgendes ein, um die vollständige TCP/IP-Konfiguration für alle Adapter anzuzeigen:
```
ipconfig /all
```
Geben Sie Folgendes ein, um eine durch DHCP zugewiesene IP-Adress Konfiguration nur für den lokalen Verbindungs Adapter zu erneuern:
```
ipconfig /renew Local Area Connection
```
Geben Sie Folgendes ein, um den DNS-Auflösungs Cache bei der Problembehandlung bei der DNS-Namensauflösung zu leeren
```
ipconfig /flushdns
```
Um die DHCP-Klassen-ID für alle Adapter anzuzeigen, deren Namen mit Local beginnen, geben Sie Folgendes ein:
```
ipconfig /showclassid Local*
```
Geben Sie Folgendes ein, um die DHCP-Klassen-ID für den zu testenden lokalen Verbindungs Adapter festzulegen:
```
ipconfig /setclassid Local Area Connection TEST
```

## <a name="additional-references"></a>Zusätzliche Referenzen

-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
