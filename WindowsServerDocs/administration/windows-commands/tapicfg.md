---
title: tapicfg
description: Referenz Artikel zu den tapicfg-Befehlen, die eine TAPI-Anwendungsverzeichnis Partition erstellen, entfernen oder anzeigen, oder eine standardmäßige TAPI-Anwendungsverzeichnis Partition festlegen.
ms.topic: reference
ms.assetid: c0e642ce-5d98-4edb-9a65-1dff09aef4e1
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 07/11/2018
ms.openlocfilehash: 17b596036251d6ea8588de3b70359ea161b67c58
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/05/2020
ms.locfileid: "91718127"
---
# <a name="tapicfg"></a>tapicfg

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Erstellt, entfernt oder zeigt eine TAPI-Anwendungsverzeichnis Partition an oder legt eine standardmäßige TAPI-Anwendungsverzeichnis Partition fest. TAPI 3,1-Clients können die Informationen in dieser Anwendungsverzeichnis Partition mit dem Verzeichnisdienst-Serverlocatorpunkt-Dienst verwenden, um TAPI-Verzeichnisse zu suchen und mit Ihnen zu kommunizieren. Sie können auch " **tapicfg** " verwenden, um Dienst Verbindungspunkte zu erstellen oder zu entfernen, die TAPI-Clients ermöglichen, die TAPI-Anwendungsverzeichnis Partitionen in einer Domäne effizient zu finden.

Dieses Befehlszeilen Tool kann auf einem beliebigen Computer ausgeführt werden, der Mitglied der Domäne ist.

## <a name="syntax"></a>Syntax

```
tapicfg install
tapicfg remove
tapicfg publishscp
tapicfg removescp
tapicfg show
tapicfg makedefault
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| [tapicfg-Installation](tapicfg-install.md) | Erstellt eine TAPI-Anwendungsverzeichnis Partition. |
| [tapicfg entfernen](tapicfg-remove.md) | Entfernt eine TAPI-Anwendungsverzeichnis Partition.|
| [tapicfg publishscp](tapicfg-publishscp.md) | Erstellt einen Dienst Verbindungspunkt zum Veröffentlichen einer TAPI-Anwendungsverzeichnis Partition. |
| [tapicfg removescp](tapicfg-removescp.md) | Entfernt einen Dienst Verbindungspunkt für eine TAPI-Anwendungsverzeichnis Partition. |
| [tapicfg anzeigen](tapicfg-show.md) | Zeigt die Namen und Speicherorte der TAPI-Anwendungsverzeichnis Partitionen in der Domäne an. |
| [tapicfg MakeDefault](tapicfg-makedefault.md) | Legt die standardmäßige TAPI-Anwendungsverzeichnis Partition für die Domäne fest. |

#### <a name="remarks"></a>Bemerkungen

- Sie müssen Mitglied der Gruppe "Organisations- **Admins** " in Active Directory sein, um entweder die Installation von " **tapicfg** " (zum Erstellen einer TAPI-Anwendungsverzeichnis Partition) oder " **tapicfg Remove** " (zum Entfernen einer TAPI-Anwendungsverzeichnis Partition) auszuführen.

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

- [tapicfg MakeDefault](tapicfg-makedefault.md)
