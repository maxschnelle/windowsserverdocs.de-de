---
title: tapicfg entfernen
description: Referenz Artikel für den Befehl "tapicfg Remove", der eine TAPI-Anwendungsverzeichnis Partition entfernt.
ms.topic: reference
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 09/29/2020
ms.openlocfilehash: 5d5b7e1cc5d362d66041a292e86e022187896dea
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/05/2020
ms.locfileid: "91730491"
---
# <a name="tapicfg-remove"></a>tapicfg entfernen

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Entfernt eine TAPI-Anwendungsverzeichnis Partition.

> [!IMPORTANT]
> Sie müssen Mitglied der Gruppe "Organisations-Admins" in Active Directory sein, um diesen Befehl ausführen zu können.

## <a name="syntax"></a>Syntax

```
tapicfg remove /directory:<partitionname>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| Entfernen Sie „`/directory:<partitionname>`“. | Erforderlich. Gibt den DNS-Namen der zu entfernenden TAPI-Anwendungsverzeichnis Partition an. Beachten Sie, dass es sich bei diesem Namen um einen voll qualifizierten Domänen Namen handeln muss. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Bemerkungen

- Dieses Befehlszeilen Tool kann auf einem beliebigen Computer ausgeführt werden, der Mitglied der Domäne ist.

- Vom Benutzer bereitgestellter Text (z. b. die Namen von TAPI-Anwendungsverzeichnis Partitionen, Servern und Domänen) mit internationalen oder Unicode-Zeichen werden nur ordnungsgemäß angezeigt, wenn entsprechende Schriftarten und Sprachunterstützung installiert ist.

- Sie können weiterhin Internet Locator Service (ILS)-Server in Ihrer Organisation verwenden, wenn ILS zur Unterstützung bestimmter Anwendungen benötigt wird, da TAPI-Clients unter Windows XP oder Windows Server 2003 Betriebssystem entweder ILS-Server oder TAPI-Anwendungsverzeichnis Partitionen Abfragen können.

- Sie können " **tapicfg** " verwenden, um Dienst Verbindungspunkte zu erstellen oder zu entfernen. Wenn die TAPI-Anwendungsverzeichnis Partition aus irgendeinem Grund umbenannt wird (z. b. Wenn Sie die Domäne umbenennen, in der Sie sich befindet), müssen Sie den vorhandenen Dienst Verbindungspunkt entfernen und einen neuen erstellen, der den neuen DNS-Namen der zu veröffentlichenden TAPI-Anwendungsverzeichnis Partition enthält. Andernfalls sind TAPI-Clients nicht in der Lage, die TAPI-Anwendungsverzeichnis Partition zu finden und darauf zuzugreifen. Sie können einen Dienst Verbindungspunkt auch zu Wartungs-oder Sicherheitszwecken entfernen (z. b. Wenn Sie TAPI-Daten nicht für eine bestimmte TAPI-Anwendungsverzeichnis Partition verfügbar machen möchten).

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [tapicfg-Installation](tapicfg-install.md)

- [tapicfg publishscp](tapicfg-publishscp.md)

- [tapicfg removescp](tapicfg-removescp.md)

- [tapicfg anzeigen](tapicfg-show.md)

- [tapicfg MakeDefault](tapicfg-makedefault.md)