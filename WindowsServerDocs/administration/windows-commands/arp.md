---
title: ARP
description: Windows-Befehle Thema **Arp** -angezeigt und ändert die Einträge im Cache Resolution-Protokolls (Arp) Adresse verwendet, um die IP-Adressen und ihre aufgelösten, physischen Adressen zu speichern.
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 1f7393c993601a5e1990cde3e6bc6763811062f4
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66435291"
---
# <a name="arp"></a>ARP

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Ändert die Einträge im Cache (ARP – Address Resolution Protocol) und zeigt. Der ARP-Cache enthält eine oder mehrere Tabellen, die zum Speichern von IP-Adressen und ihre aufgelösten Ethernet oder Token Ring physischen Adressen verwendet werden. Es gibt eine separate Tabelle für jeden Netzwerkadapter Ethernet oder Token Ring auf Ihrem Computer installiert. Ohne Parameter verwendet **Arp** Zeigt Hilfeinformationen.
## <a name="syntax"></a>Syntax
```
arp [/a [<Inetaddr>] [/n <ifaceaddr>]] [/g [<Inetaddr>] [-n <ifaceaddr>]] [/d <Inetaddr> [<ifaceaddr>]] [/s <Inetaddr> <Etheraddr> [<ifaceaddr>]]
```
### <a name="parameters"></a>Parameter

|                Parameter                |                                                                                                                                                                                                                                                               Beschreibung                                                                                                                                                                                                                                                               |
|-----------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    /a [<Inetaddr>] [/n <ifaceaddr>]     | Zeigt die Tabellen für aktuelle Arp-Cache für alle Schnittstellen. Der/n-Parameter ist Groß-/Kleinschreibung beachtet.<br /><br />Verwenden Sie zum Anzeigen der Arp-Cacheeintrags für eine bestimmte IP-Adresse **Arp/a** mit der *IP-Adr* -Parameter, in denen *IP-Adr* eine IP-Adresse. Wenn *IP-Adr* nicht angegeben ist, wird die erste geeignete Schnittstelle verwendet.<br /><br />Verwenden Sie zum Anzeigen der Arp-Cache-Tabelle für eine bestimmte Schnittstelle die * */n** *IP-Adr_Schnittst* Parameter in Verbindung mit der **/a** Parameter, in denen *IP-Adr_Schnittst* die IP-Adresse die Schnittstelle zugewiesen. |
|    /g [<Inetaddr>] [/n <ifaceaddr>]     |                                                                                                                                                                                                                                                          Identisch mit **/a**.                                                                                                                                                                                                                                                           |
|      [/d <Inetaddr> [<ifaceaddr>]       |                                                                                           Löscht einen Eintrag mit einer bestimmten IP-Adresse, in denen *IP-Adr* die IP-Adresse.<br /><br />Um einen Eintrag in einer Tabelle für eine bestimmte Schnittstelle zu löschen, verwenden die *IP-Adr_Schnittst* Parameter, in denen *IP-Adr_Schnittst* ist die IP-Adresse der Schnittstelle.<br /><br />Um alle Einträge löschen möchten, verwenden Sie das Sternchen (\*) anstelle der Platzhalter-Spaltennamens *IP-Adr*.                                                                                           |
| /s <Inetaddr> <Etheraddr> [<ifaceaddr>] |                                                                                                                     Fügt einen statischen Eintrag in der Arp-Cache, der die IP-Adresse aufgelöst wird *IP-Adr* in die physische Adresse *EtherAdr*.<br /><br />Um eine statische Arp-Cacheeintrags, in der Tabelle für eine bestimmte Schnittstelle hinzuzufügen, verwenden die *IP-Adr_Schnittst* Parameter, in denen *IP-Adr_Schnittst* eine IP-Adresse der Schnittstelle zugewiesen.                                                                                                                     |
|                   /?                    |                                                                                                                                                                                                                                                  Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                                                                                                                                                                   |

## <a name="remarks"></a>Hinweise
- Die IP-Adressen für *IP-Adr* und *IP-Adr_Schnittst* in punktierter Dezimalschreibweise ausgedrückt werden.
- Die physische Adresse für *EtherAdr* besteht aus sechs Bytes in hexadezimaler Schreibweise und getrennt durch Bindestriche (z. B. 00-AA-00-4F-2A-9C) angegeben werden.
- Einträge hinzugefügt, mit der **/s** Parameter sind statisch und zeitlich nicht aus dem Arp-Cache. Die Einträge werden entfernt, wenn das TCP/IP-Protokoll beendet und gestartet wird. Um permanente statische Arp Einträge im Cache erstellen, platzieren Sie den entsprechenden **Arp** Befehle in einem Batch-Datei, und verwenden Sie geplante Tasks zum Ausführen der Batchdatei beim Start.
  ## <a name="BKMK_Examples"></a>Beispiele für
  Wenn die Arp-Cache-Tabellen für alle Schnittstellen anzeigen möchten, geben Sie Folgendes ein:
  ```
  arp /a
  ```
  Geben Sie zum Anzeigen der Arp-Cache-Tabelle für die Schnittstelle, die die IP-Adresse 10.0.0.99 zugewiesen ist:
  ```
  arp /a /n 10.0.0.99
  ```
  Um eine statische Arp-Cacheeintrags hinzuzufügen, die die IP-Adresse 10.0.0.80 in die physische Adresse 00-AA-00-4F-2A-9C aufgelöst wird, geben Sie Folgendes ein:
  ```
  arp /s 10.0.0.80 00-AA-00-4F-2A-9C 
  ```
  ## <a name="additional-references"></a>Zusätzliche Referenzen
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
