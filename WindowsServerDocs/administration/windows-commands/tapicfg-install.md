---
title: tapicfg-Installation
description: Referenz Artikel für den Befehl "tapicfg install", der eine TAPI-Anwendungsverzeichnis Partition erstellt.
ms.topic: reference
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 09/29/2020
ms.openlocfilehash: 4f1f208406e7f616eb317687c24bb45218f3ba06
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/05/2020
ms.locfileid: "91730504"
---
# <a name="tapicfg-install"></a>tapicfg-Installation

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Erstellt eine TAPI-Anwendungsverzeichnis Partition.

> [!IMPORTANT]
> Sie müssen Mitglied der Gruppe "Organisations-Admins" in Active Directory sein, um diesen Befehl ausführen zu können.

## <a name="syntax"></a>Syntax

```
tapicfg install /directory:<partitionname> [/server:<DCname>] [/forcedefault]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| Installieren `/directory:<partitionname>` | Erforderlich. Gibt den DNS-Namen der zu erstellenden TAPI-Anwendungsverzeichnis Partition an. Dieser Name muss ein voll qualifizierter Domänen Name sein. |
| /Server `<DCname>` | Gibt den DNS-Namen des Domänen Controllers an, auf dem die TAPI-Anwendungsverzeichnis Partition erstellt wird. Wenn der Domänen Controller Name nicht angegeben wird, wird der Name des lokalen Computers verwendet. |
| /forcedefault | Gibt an, dass dieses Verzeichnis die standardmäßige TAPI-Anwendungsverzeichnis Partition für die Domäne ist. Es können mehrere TAPI-Anwendungsverzeichnis Partitionen in einer Domäne vorhanden sein.<p>Wenn dieses Verzeichnis die erste TAPI-Anwendungsverzeichnis Partition ist, die in der Domäne erstellt wurde, wird es automatisch als Standard festgelegt, unabhängig davon, ob Sie die Option **/forcedefault** verwenden. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Bemerkungen

- Dieses Befehlszeilen Tool kann auf einem beliebigen Computer ausgeführt werden, der Mitglied der Domäne ist.

- Vom Benutzer bereitgestellter Text (z. b. die Namen von TAPI-Anwendungsverzeichnis Partitionen, Servern und Domänen) mit internationalen oder Unicode-Zeichen werden nur ordnungsgemäß angezeigt, wenn entsprechende Schriftarten und Sprachunterstützung installiert ist.

- Sie können weiterhin Internet Locator Service (ILS)-Server in Ihrer Organisation verwenden, wenn ILS zur Unterstützung bestimmter Anwendungen benötigt wird, da TAPI-Clients unter Windows XP oder Windows Server 2003 Betriebssystem entweder ILS-Server oder TAPI-Anwendungsverzeichnis Partitionen Abfragen können.

- Sie können " **tapicfg** " verwenden, um Dienst Verbindungspunkte zu erstellen oder zu entfernen. Wenn die TAPI-Anwendungsverzeichnis Partition aus irgendeinem Grund umbenannt wird (z. b. Wenn Sie die Domäne umbenennen, in der Sie sich befindet), müssen Sie den vorhandenen Dienst Verbindungspunkt entfernen und einen neuen erstellen, der den neuen DNS-Namen der zu veröffentlichenden TAPI-Anwendungsverzeichnis Partition enthält. Andernfalls sind TAPI-Clients nicht in der Lage, die TAPI-Anwendungsverzeichnis Partition zu finden und darauf zuzugreifen. Sie können einen Dienst Verbindungspunkt auch zu Wartungs-oder Sicherheitszwecken entfernen (z. b. Wenn Sie TAPI-Daten nicht für eine bestimmte TAPI-Anwendungsverzeichnis Partition verfügbar machen möchten).

## <a name="examples"></a>Beispiele

Wenn Sie eine TAPI-Anwendungsverzeichnis Partition namens *tapifiction.testDom.Microsoft.com* auf einem Server mit dem Namen *testdc.testDom.Microsoft.com*erstellen und diese dann als standardmäßige TAPI-Anwendungsverzeichnis Partition für die neue Domäne festlegen möchten, geben Sie Folgendes ein:

```
tapicfg install /directory:tapifiction.testdom.microsoft.com /server:testdc.testdom.microsoft.com /forcedefault
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [tapicfg entfernen](tapicfg-remove.md)

- [tapicfg publishscp](tapicfg-publishscp.md)

- [tapicfg removescp](tapicfg-removescp.md)

- [tapicfg anzeigen](tapicfg-show.md)

- [tapicfg MakeDefault](tapicfg-makedefault.md)