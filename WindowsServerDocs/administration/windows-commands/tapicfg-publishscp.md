---
title: tapicfg publishscp
description: Referenz Artikel für den Befehl "tapicfg publishscp", der einen Dienst Verbindungspunkt zum Veröffentlichen einer TAPI-Anwendungsverzeichnis Partition erstellt.
ms.topic: reference
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 09/29/2020
ms.openlocfilehash: 82e1773eda391cbce5f205ab12ae5f4eee0f383f
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/05/2020
ms.locfileid: "91730492"
---
# <a name="tapicfg-publishscp"></a>tapicfg publishscp

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Erstellt einen Dienst Verbindungspunkt zum Veröffentlichen einer TAPI-Anwendungsverzeichnis Partition.

## <a name="syntax"></a>Syntax

```
tapicfg publishscp /directory:<partitionname> [/domain:<domainname>] [/forcedefault]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| publishscp `/directory:<partitionname>` | Erforderlich. Gibt den DNS-Namen der TAPI-Anwendungsverzeichnis Partition an, die vom Dienst Verbindungspunkt veröffentlicht wird. |
| /Domain `<domainname>` | Gibt den DNS-Namen der Domäne an, in der der Dienst Verbindungspunkt erstellt wird. Wenn der Domänen Name nicht angegeben wird, wird der Name der lokalen Domäne verwendet. |
| /forcedefault | Gibt an, dass dieses Verzeichnis die standardmäßige TAPI-Anwendungsverzeichnis Partition für die Domäne ist. Es können mehrere TAPI-Anwendungsverzeichnis Partitionen in einer Domäne vorhanden sein. |
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

- [tapicfg removescp](tapicfg-removescp.md)

- [tapicfg anzeigen](tapicfg-show.md)

- [tapicfg MakeDefault](tapicfg-makedefault.md)