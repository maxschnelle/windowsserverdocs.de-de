---
title: ipconfig
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 15071c2c-4815-4893-93b2-ab30232e312e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: fff4e5088e3e08cf2e9e742d8fb6aa2187bb9e83
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66438133"
---
# <a name="ipconfig"></a>ipconfig



Zeigt alle aktuelle TCP/IP-Netzwerkkonfiguration, und aktualisiert die Einstellungen für Dynamic Host Configuration-Protokoll (DHCP) und Domain Name System (DNS). Ohne Parameter verwendet **Ipconfig** zeigt Internet Protocol Version 4 (IPv4) und IPv6-Adressen, Subnetzmaske und Standardgateway für alle Adapter.

## <a name="syntax"></a>Syntax

```
ipconfig [/allcompartments] [/all] [/renew [<Adapter>]] [/release [<Adapter>]] [/renew6[<Adapter>]] [/release6 [<Adapter>]] [/flushdns] [/displaydns] [/registerdns] [/showclassid <Adapter>] [/setclassid <Adapter> [<ClassID>]]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/ all|Zeigt die vollständige TCP/IP-Konfiguration für alle Adapter. Adapter können für physikalische Schnittstellen, z. B. installierte Netzwerkadapter, oder logische Schnittstellen stehen, z. B. DFÜ-Verbindungen.|
|/allcompartments|Zeigt die vollständige TCP/IP-Konfiguration für alle Depots.|
|/displaydns|Zeigt den Inhalt des DNS-Clientauflösungscache, der beide Einträge enthält aus der lokalen Hosts-Datei und alle vorab geladenen abgerufen vor kurzem-Ressourceneinträge für Namensabfragen, die vom Computer aufgelöst wurden. Der DNS-Clientdienst verwendet diese Informationen zum Auflösen von häufig abgefragter Namen schnell vor dem Abfragen der konfigurierten DNS-Server.|
|/flushdns|Leert und setzt den Inhalt von den DNS-Clientauflösungscache zurück. Dieses Verfahren können Sie während der DNS-Problembehandlung verwerfen negative Cacheeinträge aus dem Cache sowie andere Einträge, die dynamisch hinzugefügt wurden.|
|/registerdns|Initiiert die manuelle dynamische Registrierung für die DNS-Namen und IP-Adressen, die auf einem Computer konfiguriert sind. Sie können diesen Parameter verwenden, Problembehandlung bei einer fehlerhaften Registrierung der DNS-Namen oder ein Problem mit dynamischen Updates zwischen einem Client und der DNS-Server ohne Neustart des Clientcomputers zu beheben. Die DNS-Einstellungen in den erweiterten Eigenschaften des TCP/IP-Protokolls bestimmen, welche Namen im DNS registriert werden.|
|/ release [\<Adapter >]|Der DHCP-Server, die aktuelle DHCP-Konfiguration und verwerfen die IP-Adresskonfiguration für entweder für alle Adapter (wenn ein Adapter nicht angegeben ist) oder für einen bestimmten Adapter eine DHCPRELEASE-Nachricht sendet, wenn die *Adapter* Parameter ist enthalten. Dieser Parameter deaktiviert die TCP/IP für Adapter, die so konfiguriert, dass eine IP-Adresse automatisch beziehen. Um einen Adapternamen angeben, geben Sie den Adapternamen, der angezeigt wird, bei der Verwendung **Ipconfig** ohne Parameter.|
|/RELEASE6 [\<Adapter >]|Der DHCPv6-Server, die aktuelle DHCP-Konfiguration und verwerfen die Konfiguration der IPv6-Adresse entweder für alle Adapter (wenn ein Adapter nicht angegeben ist) oder für einen bestimmten Adapter eine DHCPRELEASE-Nachricht sendet, wenn die *Adapter* Parameter ist enthalten. Dieser Parameter deaktiviert die TCP/IP für Adapter, die so konfiguriert, dass eine IP-Adresse automatisch beziehen. Um einen Adapternamen angeben, geben Sie den Adapternamen, der angezeigt wird, bei der Verwendung **Ipconfig** ohne Parameter.|
|/ renew [\<Adapter >]|DHCP-Konfiguration für alle Adapter (wenn ein Adapter nicht angegeben ist) oder für einen bestimmten Adapter erneuert, wenn die *Adapter* Parameter enthalten ist. Dieser Parameter ist nur auf Computern mit Adaptern, die konfiguriert werden, um eine IP-Adresse automatisch beziehen verfügbar. Um einen Adapternamen angeben, geben Sie den Adapternamen, der angezeigt wird, bei der Verwendung **Ipconfig** ohne Parameter.|
|/renew6 [\<Adapter >]|DHCPv6-Konfiguration für alle Adapter (wenn ein Adapter nicht angegeben ist) oder für einen bestimmten Adapter erneuert, wenn die *Adapter* Parameter enthalten ist. Dieser Parameter ist nur auf Computern mit Adaptern, die konfiguriert werden, um eine IPv6-Adresse automatisch beziehen verfügbar. Um einen Adapternamen angeben, geben Sie den Adapternamen, der angezeigt wird, bei der Verwendung **Ipconfig** ohne Parameter.|
|/setclassid \<Adapter>[ <ClassID>]|Konfiguriert die DHCP-Klassen-ID eines angegebenen Adapters. Um die DHCP-Klassen-ID für alle Adapter zu festzulegen, verwenden Sie das Sternchen ( **&#42;** ) anstelle der Platzhalter-Spaltennamens *Adapter*. Dieser Parameter ist nur auf Computern mit Adaptern, die konfiguriert werden, um eine IP-Adresse automatisch beziehen verfügbar. Wenn Sie eine DHCP-Klassen-ID nicht angegeben ist, wird die aktuelle Klassenid entfernt.|
|/ showclassid \<Adapter >|Zeigt die DHCP-Klassen-ID eines angegebenen Adapters. Um die DHCP-Klassen-ID für alle Adapter zu anzuzeigen, verwenden Sie das Sternchen ( **&#42;** ) anstelle der Platzhalter-Spaltennamens *Adapter*. Dieser Parameter ist nur auf Computern mit Adaptern, die konfiguriert werden, um eine IP-Adresse automatisch beziehen verfügbar.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

- Dieser Befehl eignet sich am besten auf Computern, die konfiguriert werden, um eine IP-Adresse automatisch beziehen. Dadurch können Benutzer, um zu bestimmen, welche Werte der TCP/IP-Konfiguration von DHCP, Private IP-Adressierung APIPA (Automatic) oder eine alternative Konfiguration konfiguriert wurden.
- Wenn Sie den Namen für angeben *Adapter* enthält Leerzeichen, Anführungszeichen der Name des Adapters verwenden (Beispiel: **"** <em>Adaptername</em> **"** ).
- Für den Adapternamen **Ipconfig** unterstützt die Verwendung des Sternchens ( *) Platzhalterzeichen, um die beiden Namen anzugeben, die mit einer angegebenen Zeichenfolge oder Netzwerkkarten mit Namen mit einer angegebenen Zeichenfolge beginnen. Z. B. **lokalen\\** *    entspricht allen Adaptern, die mit der Zeichenfolge lokal zu starten und  **\*Con\\** * entspricht allen Adaptern, die enthalten die Zeichenfolge bestätigen.

## <a name="examples"></a>Beispiele

Um die grundlegende TCP/IP-Konfiguration für alle Adapter anzuzeigen, geben Sie Folgendes ein:
```
ipconfig
```
Um die vollständige TCP/IP-Konfiguration für alle Adapter anzuzeigen, geben Sie Folgendes ein:
```
ipconfig /all
```
Geben Sie Folgendes ein, um eine per DHCP zugewiesene IP-Adresskonfiguration für den LAN-Verbindung-Adapter zu erneuern:
```
ipconfig /renew "Local Area Connection"
```
Geben Sie Folgendes ein, um den DNS-Auflösungscache zu leeren, bei der Problembehandlung von Problemen bei der DNS-namensauflösung:
```
ipconfig /flushdns
```
Um die DHCP-Klassen-ID für alle Netzwerkkarten mit Namen anzuzeigen, die mit lokalen beginnen, geben Sie Folgendes ein:
```
ipconfig /showclassid Local*
```
Um die DHCP-Klassen-ID für den LAN-Verbindung-Adapter für TEST festzulegen, geben Sie Folgendes ein:
```
ipconfig /setclassid "Local Area Connection" TEST
```

#### <a name="additional-references"></a>Weitere Verweise

-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)