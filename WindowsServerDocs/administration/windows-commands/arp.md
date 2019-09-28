---
title: ARP
description: 'Thema Windows-Befehle für **ARP** : zeigt Einträge im ARP-Cache (Address Resolution Protocol) an, die zum Speichern von IP-Adressen und deren aufgelösten physischen Adressen verwendet werden.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 827e96eb-1945-483f-980f-714703456f7c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1e6d34ceaa56ed40a1083b710e0db01b106f49e2
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71382662"
---
# <a name="arp"></a>ARP

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt Einträge im ARP-Cache (Address Resolution Protocol) an und ändert diese. Der ARP-Cache enthält eine oder mehrere Tabellen, die zum Speichern von IP-Adressen und deren aufgelöster physischer Ethernet-oder TokenRing-Adressen verwendet werden. Es gibt eine separate Tabelle für jeden Ethernet-oder TokenRing-Netzwerkadapter, der auf Ihrem Computer installiert ist. Wenn Sie ohne Parameter verwendet wird, zeigt **ARP** Hilfe Informationen an.
## <a name="syntax"></a>Syntax
```
arp [/a [<Inetaddr>] [/n <ifaceaddr>]] [/g [<Inetaddr>] [-n <ifaceaddr>]] [/d <Inetaddr> [<ifaceaddr>]] [/s <Inetaddr> <Etheraddr> [<ifaceaddr>]]
```
### <a name="parameters"></a>Parameter

|                Parameter                |                                                                                                                                                                                                                                                               Beschreibung                                                                                                                                                                                                                                                               |
|-----------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    /a [<Inetaddr>] [/n <ifaceaddr>]     | Zeigt die aktuellen ARP-Cache Tabellen für alle Schnittstellen an. Beim Parameter/n wird die Groß-/Kleinschreibung beachtet.<br /><br />Wenn Sie den ARP-Cache Eintrag für eine bestimmte IP-Adresse anzeigen möchten, verwenden Sie **ARP/a** mit dem *inetaddr* -Parameter, wobei *inetaddr* eine IP-Adresse ist. Wenn *inetaddr* nicht angegeben wird, wird die erste anwendbare Schnittstelle verwendet.<br /><br />Zum Anzeigen der ARP-Cache Tabelle für eine bestimmte Schnittstelle verwenden Sie den **/n**_ifaceaddr_ -Parameter in Verbindung mit dem **/a** -Parameter, wobei *ifaceaddr* die der Schnittstelle zugewiesene IP-Adresse ist. |
|    /g [<Inetaddr>] [/n <ifaceaddr>]     |                                                                                                                                                                                                                                                          Identisch mit **/a**.                                                                                                                                                                                                                                                           |
|      [/d <Inetaddr> [<ifaceaddr>]       |                                                                                           Löscht einen Eintrag mit einer bestimmten IP-Adresse, wobei *inetaddr* die IP-Adresse ist.<br /><br />Um einen Eintrag in einer Tabelle für eine bestimmte Schnittstelle zu löschen, verwenden Sie den *ifaceaddr* -Parameter, wobei *ifaceaddr* die der Schnittstelle zugewiesene IP-Adresse ist.<br /><br />Um alle Einträge zu löschen, verwenden Sie anstelle von *inetaddr*das Platzhalter Zeichen Sternchen (\*).                                                                                           |
| /s <Inetaddr> <Etheraddr> [<ifaceaddr>] |                                                                                                                     Fügt dem ARP-Cache einen statischen Eintrag hinzu, der die IP-Adresse *inetaddr* in die physische Adresse *etheraddr*auflöst.<br /><br />Wenn Sie der Tabelle einen statischen ARP-Cache Eintrag für eine bestimmte Schnittstelle hinzufügen möchten, verwenden Sie den *ifaceaddr* -Parameter, wobei *ifaceaddr* eine der Schnittstelle zugewiesene IP-Adresse ist.                                                                                                                     |
|                   /?                    |                                                                                                                                                                                                                                                  Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                                                                                                                                                                   |

## <a name="remarks"></a>Hinweise
- Die IP-Adressen für *inetaddr* und *ifaceaddr* werden in punktierter Dezimal Schreibweise ausgedrückt.
- Die physische Adresse für *etheraddr* besteht aus sechs Bytes, die in Hexadezimal Schreibweise ausgedrückt und durch Bindestriche (z. b. 00-AA-00-4f-2a-9c) getrennt sind.
- Einträge, die mit dem **/s** -Parameter hinzugefügt werden, sind statisch und keinen Timeout für den ARP-Cache. Die Einträge werden entfernt, wenn das TCP/IP-Protokoll beendet und gestartet wird. Um permanente statische ARP-Cache Einträge zu erstellen, platzieren Sie die entsprechenden **ARP** -Befehle in einer Batchdatei, und verwenden Sie geplante Aufgaben, um die Batchdatei beim Start auszuführen.
  ## <a name="BKMK_Examples"></a>Beispiele
  Geben Sie Folgendes ein, um die ARP-Cache Tabellen für alle Schnittstellen anzuzeigen:
  ```
  arp /a
  ```
  Zum Anzeigen der ARP-Cache Tabelle für die Schnittstelle, der die IP-Adresse 10.0.0.99 zugewiesen ist, geben Sie Folgendes ein:
  ```
  arp /a /n 10.0.0.99
  ```
  Um einen statischen ARP-Cache Eintrag hinzuzufügen, der die IP-Adresse 10.0.0.80 in die physische Adresse 00-AA-00-4f-2a-9c auflöst, geben Sie Folgendes ein:
  ```
  arp /s 10.0.0.80 00-AA-00-4F-2A-9C 
  ```
  ## <a name="additional-references"></a>Weitere Verweise
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
