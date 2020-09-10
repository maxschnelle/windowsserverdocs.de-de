---
title: ipxroute
description: Referenz Artikel für den ipxroute-Befehl, der Informationen zu den vom IPX-Protokoll verwendeten Routing Tabellen anzeigt und ändert.
ms.topic: reference
ms.assetid: 3a30304f-655e-43d2-a4ac-7568abf8975c
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: dbfc2df421429d4265cbcb425d189c4fd69de99d
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89634419"
---
# <a name="ipxroute"></a>ipxroute

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt Informationen zu den Routing Tabellen an, die vom IPX-Protokoll verwendet werden, und ändert diese. Wird ohne Parameter verwendet, zeigt **IPXRoute** die Standardeinstellungen für Pakete an, die an unbekannte, Broadcast-und Multicast Adressen gesendet werden.

## <a name="syntax"></a>Syntax

```
ipxroute servers [/type=x]
ipxroute ripout <network>
ipxroute resolve {guid | name} {GUID | <adaptername>}
ipxroute board= N [def] [gbr] [mbr] [remove=xxxxxxxxxxxx]
ipxroute config
```

### <a name="parameters"></a>Parameter
| Parameter | BESCHREIBUNG |
| ------- | -------- |
| Webserver`[/type=x]` | Zeigt die Tabelle für den Dienst Zugriffspunkt (SAP) für den angegebenen Servertyp an. **x** muss eine ganze Zahl sein. Zeigt beispielsweise `/type=4` alle Dateiserver an. Wenn Sie **/Type**nicht angeben, werden `ipxroute servers` alle Server Typen angezeigt, die nach Servernamen aufgelistet sind. |
| Auflösen `{GUID | name}``{GUID | adaptername}` | Löst den Namen der GUID in ihren anzeigen Amen oder den anzeigen Amen für die GUID auf. |
| Board = *n* | Gibt den Netzwerkadapter an, für den Parameter abgefragt oder festgelegt werden sollen. |
| def | Sendet Pakete an die Broadcast alle Routen. Wenn ein Paket an eine eindeutige MAC-Adresse (Media Access Card) übertragen wird, die sich nicht in der Quell Routing Tabelle befindet, sendet **IPXRoute** das Paket standardmäßig an die einzelnen Routen Broadcast. |
| GbR | Sendet Pakete an die Broadcast alle Routen. Wenn ein Paket an die Broadcast Adresse (FFFFFFFFFFFF) übertragen wird, sendet **IPXRoute** das Paket standardmäßig an die einzelnen Routen Broadcast. |
| MBR | Sendet Pakete an die Broadcast alle Routen. Wenn ein Paket an eine Multicast Adresse (C000xxxxxxxx) übertragen wird, sendet **IPXRoute** das Paket standardmäßig an die einzelnen Routen Broadcast. |
| Remove =*xxxxxxxxxxxx* | entfernt die angegebene Knotenadresse aus der Quell Routing Tabelle. |
| config | Zeigt Informationen zu allen Bindungen an, für die IPX konfiguriert ist. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um die Netzwerksegmente anzuzeigen, an die die Arbeitsstation angefügt ist, und den verwendeten Rahmentyp:

```
ipxroute config
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
