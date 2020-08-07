---
title: arp
description: Referenz Artikel für den ARP-Befehl, der Einträge im ARP-Cache (Address Resolution Protocol), die zum Speichern von IP-Adressen und deren aufgelösten physischen Adressen verwendet werden, anzeigt und ändert.
ms.topic: article
ms.assetid: 827e96eb-1945-483f-980f-714703456f7c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c3e44d471fc31b14bf37b1c4911c0f465e31b3ac
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87895563"
---
# <a name="arp"></a>arp

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt Einträge im ARP-Cache (Address Resolution Protocol) an und ändert diese. Der ARP-Cache enthält eine oder mehrere Tabellen, die zum Speichern von IP-Adressen und deren aufgelöster physischer Ethernet-oder TokenRing-Adressen verwendet werden. Es gibt eine separate Tabelle für jeden Ethernet-oder TokenRing-Netzwerkadapter, der auf Ihrem Computer installiert ist. Wenn Sie ohne Parameter verwendet wird, zeigt **ARP** Hilfe Informationen an.

## <a name="syntax"></a>Syntax

```
arp [/a [<inetaddr>] [/n <ifaceaddr>]] [/g [<inetaddr>] [-n <ifaceaddr>]] [/d <inetaddr> [<ifaceaddr>]] [/s <inetaddr> <etheraddr> [<ifaceaddr>]]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `[/a [<inetaddr>] [/n <ifaceaddr>]` | Zeigt die aktuellen ARP-Cache Tabellen für alle Schnittstellen an. Beim Parameter **/n** wird die Groß-/Kleinschreibung beachtet. Wenn Sie den ARP-Cache Eintrag für eine bestimmte IP-Adresse anzeigen möchten, verwenden Sie **ARP/a** mit dem **inetaddr** -Parameter, wobei **inetaddr** eine IP-Adresse ist. Wenn **inetaddr** nicht angegeben wird, wird die erste anwendbare Schnittstelle verwendet. Zum Anzeigen der ARP-Cache Tabelle für eine bestimmte Schnittstelle verwenden Sie den **/n ifaceaddr** -Parameter in Verbindung mit dem **/a** -Parameter, wobei **inetaddr** die der Schnittstelle zugewiesene IP-Adresse ist. |
| `[/g [<inetaddr>] [/n <ifaceaddr>]` | Identisch mit **/a**. |
| `[/d <inetaddr> [<ifaceaddr>]` | Löscht einen Eintrag mit einer bestimmten IP-Adresse, wobei **inetaddr** die IP-Adresse ist. Um einen Eintrag in einer Tabelle für eine bestimmte Schnittstelle zu löschen, verwenden Sie den **ifaceaddr** -Parameter, wobei **ifaceaddr** die der Schnittstelle zugewiesene IP-Adresse ist. Um alle Einträge zu löschen, verwenden Sie anstelle von **inetaddr**das Platzhalter Zeichen Sternchen (*). |
| `[/s <inetaddr> <etheraddr> [<ifaceaddr>]` | Fügt dem ARP-Cache einen statischen Eintrag hinzu, der die IP-Adresse **inetaddr** in die physische Adresse **etheraddr**auflöst. Wenn Sie der Tabelle einen statischen ARP-Cache Eintrag für eine bestimmte Schnittstelle hinzufügen möchten, verwenden Sie den **ifaceaddr** -Parameter, wobei **ifaceaddr** eine der Schnittstelle zugewiesene IP-Adresse ist. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

### <a name="remarks"></a>Bemerkungen

- Die IP-Adressen für **inetaddr** und **ifaceaddr** werden in punktierter Dezimal Schreibweise ausgedrückt.

- Die physische Adresse für **etheraddr** besteht aus sechs Bytes, die in Hexadezimal Schreibweise ausgedrückt und durch Bindestriche (z. b. 00-AA-00-4f-2a-9c) getrennt sind.

- Einträge, die mit dem **/s** -Parameter hinzugefügt werden, sind statisch und keinen Timeout für den ARP-Cache. Die Einträge werden entfernt, wenn das TCP/IP-Protokoll beendet und gestartet wird. Um permanente statische ARP-Cache Einträge zu erstellen, platzieren Sie die entsprechenden **ARP** -Befehle in einer Batchdatei, und verwenden Sie geplante Aufgaben, um die Batchdatei beim Start auszuführen.

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um die ARP-Cache Tabellen für alle Schnittstellen anzuzeigen:

```
arp /a
```

Zum Anzeigen der ARP-Cache Tabelle für die Schnittstelle, der die IP-Adresse *10.0.0.99*zugewiesen ist, geben Sie Folgendes ein:

```
arp /a /n 10.0.0.99
```

Um einen statischen ARP-Cache Eintrag hinzuzufügen, der die IP-Adresse *10.0.0.80* in die physische Adresse *00-AA-00-4f-2a-9c*auflöst, geben Sie Folgendes ein:

```
arp /s 10.0.0.80 00-AA-00-4F-2A-9C
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
