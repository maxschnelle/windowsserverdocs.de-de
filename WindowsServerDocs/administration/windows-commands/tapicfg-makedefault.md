---
title: tapicfg MakeDefault
description: Referenz Artikel für den tapicfg MakeDefault-Befehl, mit dem die standardmäßige TAPI-Anwendungsverzeichnis Partition für die Domäne festgelegt wird.
ms.topic: reference
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 09/29/2020
ms.openlocfilehash: 298abd8d649e30269bd1a4c984b6b04bfa919e6c
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/05/2020
ms.locfileid: "91730496"
---
# <a name="tapicfg-makedefault"></a>tapicfg MakeDefault

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Legt die standardmäßige TAPI-Anwendungsverzeichnis Partition für die Domäne fest.

## <a name="syntax"></a>Syntax

```
tapicfg makedefault /directory:<partitionname> [/domain:<domainname>]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| MakeDefault `/directory:<partitionname>` | Erforderlich. Gibt den DNS-Namen der TAPI-Anwendungsverzeichnis Partition an, die als Standard Partition für die Domäne festgelegt ist. Dieser Name muss ein voll qualifizierter Domänen Name sein. |
| /Domain `<domainname>` | Gibt den DNS-Namen der Domäne an, für die die TAPI-Anwendungsverzeichnis Partition als Standard festgelegt ist. Wenn der Domänen Name nicht angegeben wird, wird der Name der lokalen Domäne verwendet. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Bemerkungen

- Dieses Befehlszeilen Tool kann auf einem beliebigen Computer ausgeführt werden, der Mitglied der Domäne ist.

- Vom Benutzer bereitgestellter Text (z. b. die Namen von TAPI-Anwendungsverzeichnis Partitionen, Servern und Domänen) mit internationalen oder Unicode-Zeichen werden nur ordnungsgemäß angezeigt, wenn entsprechende Schriftarten und Sprachunterstützung installiert ist.

- Sie können weiterhin Internet Locator Service (ILS)-Server in Ihrer Organisation verwenden, wenn ILS zur Unterstützung bestimmter Anwendungen benötigt wird, da TAPI-Clients unter Windows XP oder Windows Server 2003 Betriebssystem entweder ILS-Server oder TAPI-Anwendungsverzeichnis Partitionen Abfragen können.

- Sie können " **tapicfg** " verwenden, um Dienst Verbindungspunkte zu erstellen oder zu entfernen. Wenn die TAPI-Anwendungsverzeichnis Partition aus irgendeinem Grund umbenannt wird (z. b. Wenn Sie die Domäne umbenennen, in der Sie sich befindet), müssen Sie den vorhandenen Dienst Verbindungspunkt entfernen und einen neuen erstellen, der den neuen DNS-Namen der zu veröffentlichenden TAPI-Anwendungsverzeichnis Partition enthält. Andernfalls sind TAPI-Clients nicht in der Lage, die TAPI-Anwendungsverzeichnis Partition zu finden und darauf zuzugreifen. Sie können einen Dienst Verbindungspunkt auch zu Wartungs-oder Sicherheitszwecken entfernen (z. b. Wenn Sie TAPI-Daten nicht für eine bestimmte TAPI-Anwendungsverzeichnis Partition verfügbar machen möchten).

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [tapicfg-Installation](tapicfg-install.md)

- [tapicfg entfernen](tapicfg-remove.md)

- [tapicfg publishscp](tapicfg-publishscp.md)

- [tapicfg removescp](tapicfg-removescp.md)

- [tapicfg anzeigen](tapicfg-show.md)