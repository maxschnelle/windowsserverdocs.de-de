---
title: klist
description: Referenz Artikel für den klist-Befehl, der eine Liste der derzeit zwischengespeicherten Kerberos-Tickets anzeigt.
ms.topic: reference
ms.assetid: 4689b4a9-1740-47dd-9240-02105efca428
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d5284feae5da9c8c7fcdab90dd34ce7855128d5f
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89037718"
---
# <a name="klist"></a>klist

Zeigt eine Liste der derzeit zwischengespeicherten Kerberos-Tickets an.

> [!IMPORTANT]
> Sie müssen mindestens ein **Domänen Administrator**oder eine entsprechende Gruppe sein, um alle Parameter dieses Befehls ausführen zu können.

## <a name="syntax"></a>Syntax

```
klist [-lh <logonID.highpart>] [-li <logonID.lowpart>] tickets | tgt | purge | sessions | kcd_cache | get | add_bind | query_bind | purge_bind
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| -LH | Gibt den hohen Teil des lokalen eindeutigen Bezeichners (LUID) des Benutzers an, ausgedrückt als hexadezimal. Wenn weder **– LH** noch **– Li** vorhanden ist, wird für den Befehl standardmäßig die LUID des aktuell angemeldeten Benutzers verwendet. |
| -Li | Gibt den unteren Teil des lokalen eindeutigen Bezeichners (LUID) des Benutzers an, ausgedrückt als hexadezimal. Wenn weder **– LH** noch **– Li** vorhanden ist, wird für den Befehl standardmäßig die LUID des aktuell angemeldeten Benutzers verwendet. |
| Tickets | Listet die derzeit zwischengespeicherten Ticket-Zuteilungs Tickets (TGTs) und Dienst Tickets der angegebenen Anmelde Sitzung auf. Dies ist die Standardoption. |
| TGT | Zeigt das erste Kerberos-TGT an. |
| Löschen | Hiermit können Sie alle Tickets der angegebenen Anmelde Sitzung löschen. |
| Sitzungen | Zeigt eine Liste der Anmelde Sitzungen auf diesem Computer an. |
| kcd_cache | Zeigt die Informationen zur eingeschränkten Kerberos-Delegierung im Cache an. |
| get | Ermöglicht das Anfordern eines Tickets für den Zielcomputer, der durch den Dienst Prinzipal Namen (SPN) angegeben wird. |
| add_bind | Ermöglicht es Ihnen, einen bevorzugten Domänen Controller für die Kerberos-Authentifizierung anzugeben. |
| query_bind | Zeigt eine Liste der zwischengespeicherten bevorzugten Domänen Controller für jede Domäne an, mit der Kerberos eine Verbindung hergestellt hat. |
| purge_bind | Entfernt die zwischengespeicherten bevorzugten Domänen Controller für die angegebenen Domänen. |
| kdcoptions | Zeigt die in RFC 4120 angegebenen Optionen für das Schlüsselverteilungscenter (KDC) an. |
| /? | Zeigt die Hilfe für diesen Befehl an. |

#### <a name="remarks"></a>Bemerkungen

- Wenn keine Parameter angegeben werden, ruft **klist** alle Tickets für den aktuell angemeldeten Benutzer ab.

- In den Parametern werden die folgenden Informationen angezeigt:

  - **Tickets** : Listet die derzeit zwischengespeicherten Tickets von Diensten auf, für die Sie sich seit der Anmeldung authentifiziert haben. Zeigt die folgenden Attribute aller zwischengespeicherten Tickets an:

    - Anmelde- **ID:** Die LUID.

    - **Client:** Die Verkettung des Client namens und des Domänen Namens des Clients.

    - **Server:** Die Verkettung des Dienst namens und des Domänen Namens des Dienstanbieter.

    - **Kerbticket-Verschlüsselungstyp:** Der Verschlüsselungstyp, der zum Verschlüsseln des Kerberos-Tickets verwendet wird.

    - **Ticket-Flags:** Die Kerberos-Ticket-Flags.

    - **Startzeit:** Der Zeitpunkt, ab dem das Ticket gültig ist.

    - **Endzeit:** Der Zeitpunkt, zu dem das Ticket nicht mehr gültig ist. Wenn ein Ticket zu diesem Zeitpunkt abgelaufen ist, kann es nicht mehr verwendet werden, um sich bei einem Dienst zu authentifizieren oder für die Verlängerung zu verwenden.

    - Erneuerungs **Zeit:** Der Zeitpunkt, zu dem eine neue anfängliche Authentifizierung erforderlich ist.

    - **Sitzungs Schlüsseltyp:** Der Verschlüsselungsalgorithmus, der für den Sitzungsschlüssel verwendet wird.

  - **TGT** -listet das erste Kerberos-TGT und die folgenden Attribute des aktuell zwischengespeicherten Tickets auf:

    - Anmelde- **ID:** Identifiziert in Hexadezimal Zahl.

    - **ServiceName:** krbtgt

    - **TargetName `<SPN>` :** krbtgt

    - **Domain Name:** Der Name der Domäne, die das TGT ausgibt.

    - **TargetDomainName:** Die Domäne, für die das TGT ausgegeben wird.

    - **Alttargetdomainname:** Die Domäne, für die das TGT ausgegeben wird.

    - **Ticket-Flags:** Address-und Target-Aktionen und-Typ.

    - **Sitzungsschlüssel:** Schlüssellänge und Verschlüsselungsalgorithmus.

    - **StartTime:** Lokale Computerzeit, an der das Ticket angefordert wurde.

    - **EndTime:** Uhrzeit, zu der das Ticket nicht mehr gültig ist. Wenn ein Ticket zu diesem Zeitpunkt abgelaufen ist, kann es nicht mehr zum Authentifizieren bei einem Dienst verwendet werden.

    - **Erneuteste Verlängerung:** Stichtag für die Verlängerung des Tickets.

    - **Timeskew:** Zeitunterschied zum Schlüsselverteilungscenter (KDC).

    - **Encode-Ticket:** Codiertes Ticket.

  - Löschen **: Hiermit** können Sie ein bestimmtes Ticket löschen. Wenn Sie Tickets löschen, werden alle von Ihnen zwischengespeicherten Tickets zerstört. verwenden Sie daher dieses Attribut mit Vorsicht. Möglicherweise werden Sie nicht mehr in der Lage sein, sich bei Ressourcen zu authentifizieren. Wenn dies geschieht, müssen Sie sich ab-und wieder anmelden.

    - Anmelde- **ID:** Identifiziert in Hexadezimal Zahl.

  - **Sitzungen** : Hiermit können Sie die Informationen für alle Anmelde Sitzungen auf diesem Computer auflisten und anzeigen.

    - Anmelde- **ID:** Wenn angegeben, wird die Anmelde Sitzung nur durch den angegebenen Wert angezeigt. Wenn nicht angegeben, werden alle Anmelde Sitzungen auf diesem Computer angezeigt.

  - **kcd_cache** : Hiermit können Sie die Informationen zum eingeschränkten Kerberos-Delegierungs Cache anzeigen.

    - Anmelde- **ID:** Wenn angegeben, werden die Cache Informationen für die Anmelde Sitzung mit dem angegebenen Wert angezeigt. Wenn nicht angegeben, werden die Cache Informationen für die Anmelde Sitzung des aktuellen Benutzers angezeigt.

  - **Get** : Hiermit können Sie ein Ticket für das Ziel anfordern, das vom SPN angegeben wird.

    - Anmelde- **ID:** Wenn angegeben, wird ein Ticket angefordert, indem die Anmelde Sitzung mit dem angegebenen Wert verwendet wird. Wenn nicht angegeben, fordert ein Ticket mithilfe der Anmelde Sitzung des aktuellen Benutzers an.

    - **kdcoptions:** Fordert ein Ticket mit den angegebenen KDC-Optionen an.

  - **add_bind** : Hiermit können Sie einen bevorzugten Domänen Controller für die Kerberos-Authentifizierung angeben.

  - **query_bind** : ermöglicht das Anzeigen von zwischengespeicherten, bevorzugten Domänen Controllern für die Domänen.

  - **purge_bind** : ermöglicht das Entfernen von zwischengespeicherten, bevorzugten Domänen Controllern für die Domänen.

  - **kdcoptions** : Informationen zur aktuellen Liste der Optionen und deren Erläuterungen finden Sie unter [RFC 4120](http://www.ietf.org/rfc/rfc4120.txt).

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um den Kerberos-Ticket Cache abzufragen und zu ermitteln, ob Tickets fehlen, wenn der Zielserver oder das Konto fehlerhaft ist oder der Verschlüsselungstyp aufgrund eines Fehlers der Ereignis-ID 27 nicht unterstützt wird:

```
klist
```

```
klist –li 0x3e7
```

Geben Sie Folgendes ein, um mehr über die Besonderheiten der einzelnen Ticket Erteilungs Tickets zu erfahren, die auf dem Computer für eine Anmelde Sitzung zwischengespeichert werden:

```
klist tgt
```

Wenn Sie den Kerberos-Ticket Cache bereinigen möchten, melden Sie sich ab, und melden Sie sich dann wieder an.

```
klist purge
```

```
klist purge –li 0x3e7
```

Geben Sie Folgendes ein, um eine Anmelde Sitzung zu diagnostizieren und eine Anmelde-ID für einen Benutzer oder Dienst zu finden:

```
klist sessions
```

Geben Sie Folgendes ein, um den Fehler bei der eingeschränkten Kerberos-Delegierung zu diagnostizieren und den letzten aufgetretenen Fehler zu ermitteln:

```
klist kcd_cache
```

Geben Sie Folgendes ein, um zu diagnostizieren, ob ein Benutzer oder ein Dienst ein Ticket an einen Server übernehmen oder ein Ticket für einen bestimmten SPN anfordern kann:

```
klist get host/%computername%
```

Zum Diagnostizieren von Replikations Problemen zwischen Domänen Controllern benötigen Sie in der Regel den Client Computer als Ziel für einen bestimmten Domänen Controller. Geben Sie Folgendes ein, um den Client Computer mit dem jeweiligen Domänen Controller zu erreichen:

```
klist add_bind CONTOSO KDC.CONTOSO.COM
```

```
klist add_bind CONTOSO.COM KDC.CONTOSO.COM
```

Geben Sie Folgendes ein, um abzufragen, welche Domänen Controller zuletzt von diesem Computer kontaktiert wurden:

```
klist query_bind
```

Wenn Sie Domänen Controller wiederentdecken oder den Cache leeren möchten, bevor Sie neue Domänen Controller Bindungen mit erstellen, geben Sie Folgendes ein `klist add_bind` :

```
klist purge_bind
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)