---
title: repair-bde
description: Referenz Artikel zum Befehl "Repair-BDE", der versuchen kann, kritische Teile eines stark beschädigten Laufwerks zu rekonstruieren und wiederherstellbare Daten zu retten, wenn das Laufwerk mithilfe von BitLocker verschlüsselt wurde.
ms.topic: reference
ms.assetid: 534dca1a-05f7-4ea8-ac24-4fe5f14f988a
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: e7ebf0f2923e565e16e546a7804ee42771eec83d
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89640638"
---
# <a name="repair-bde"></a>repair-bde

Versucht, kritische Teile eines stark beschädigten Laufwerks zu rekonstruieren und wiederherstellbare Daten zu retten, wenn das Laufwerk mithilfe von BitLocker verschlüsselt wurde und über ein gültiges Wiederherstellungs Kennwort oder einen Wiederherstellungs Schlüssel zur Entschlüsselung verfügt.

> [!IMPORTANT]
> Wenn die BitLocker-metadatendaten auf dem Laufwerk beschädigt sind, müssen Sie zusätzlich zum Wiederherstellungs Kennwort oder Wiederherstellungs Schlüssel ein Sicherungs Schlüssel Paket angeben können. Wenn Sie die Standardeinstellung für die Schlüssel Sicherung für Active Directory Domain Services verwendet haben, wird Ihr Schlüssel Paket dort gesichert. Sie können den BitLocker [: BitLocker-Wiederherstellungs Kennwort-Viewer](https://docs.microsoft.com/windows/security/information-protection/bitlocker/bitlocker-use-bitlocker-recovery-password-viewer) verwenden, um das Schlüssel Paket aus AD DS abzurufen.
>
> Mithilfe des Schlüssel Pakets und des Wiederherstellungs Kennworts oder Wiederherstellungs Schlüssels können Sie Teile eines durch BitLocker geschützten Laufwerks entschlüsseln, auch wenn der Datenträger beschädigt ist. Jedes Schlüssel Paket funktioniert nur für ein Laufwerk mit dem entsprechenden Laufwerks Bezeichner.

## <a name="syntax"></a>Syntax

```
repair-bde <inputvolume> <outputvolumeorimage> [-rk] [–rp] [-pw] [–kp] [–lf] [-f] [{-?|/?}]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| `<inputvolume>` | Gibt den Laufwerk Buchstaben des zu reparierenden BitLocker-verschlüsselten Laufwerks an. Der Laufwerk Buchstabe muss einen Doppelpunkt enthalten. Beispiel: **C:**. Wenn der Pfad zu einem Schlüssel Paket nicht angegeben wird, durchsucht dieser Befehl das Laufwerk nach einem Schlüssel Paket. Wenn die Festplatte beschädigt ist, ist dieser Befehl möglicherweise nicht in der Lage, das Paket zu finden, und Sie werden aufgefordert, den Pfad anzugeben. |
| `<outputvolumeorimage>` | Gibt das Laufwerk an, auf dem der Inhalt des reparierten Laufwerks gespeichert werden soll. Alle Informationen auf dem Ausgabe Laufwerk werden überschrieben. |
| -RK | Gibt den Speicherort des Wiederherstellungs Schlüssels an, der zum Entsperren des Volumes verwendet werden soll. Dieser Befehl kann auch als **-Wiederherstellungsschlüssel**angegeben werden. |
| -RP | Identifiziert das numerische Wiederherstellungs Kennwort, das zum Entsperren des Volumes verwendet werden soll. Dieser Befehl kann auch als **-wiederherstellungkennwort**angegeben werden. |
| -PW | Gibt das Kennwort an, das zum Entsperren des Volumes verwendet werden soll. Dieser Befehl kann auch als **-Kennwort** angegeben werden. |
| -KP | Identifiziert das Wiederherstellungs Schlüssel Paket, das zum Entsperren des Volumes verwendet werden kann. Dieser Befehl kann auch als **-KeyPackage**angegeben werden. |
| -lf | Gibt den Pfad zu der Datei an, in der Fehler-, Warn-und Informationsmeldungen von Repair-bde gespeichert werden. Dieser Befehl kann auch als **-logfile**angegeben werden. |
| -f | Erzwingt das Aufheben der Bereitstellung eines Volumes, auch wenn es nicht gesperrt werden kann. Dieser Befehl kann auch als **-Force**angegeben werden. |
| -? oder /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

### <a name="limitations"></a>Einschränkungen

Für den folgenden Befehl gelten die folgenden Einschränkungen:

- Dieser Befehl kann ein Laufwerk nicht reparieren, das während des Verschlüsselungs-oder Entschlüsselungs Vorgangs fehlgeschlagen ist.

- Bei diesem Befehl wird davon ausgegangen, dass das Laufwerk vollständig verschlüsselt ist, wenn für das Laufwerk eine Verschlüsselung vorhanden ist.

## <a name="examples"></a>Beispiele

Zum Reparieren des Laufwerks c:, um den Inhalt von Laufwerk c: auf Laufwerk D: zu schreiben, indem Sie die Wiederherstellungs Schlüsseldatei (Wiederherstellungsschlüssel. Bek) verwenden, die auf Laufwerk F: gespeichert ist, und um die Ergebnisse dieses Versuchs in die Protokolldatei (log.txt) auf Laufwerk Z: zu schreiben, geben Sie Folgendes ein:

```
repair-bde C: D: -rk F:\RecoveryKey.bek –lf Z:\log.txt
```

Zum Reparieren des Laufwerks c: und zum Schreiben des Inhalts von Laufwerk c: auf Laufwerk D: Geben Sie unter Verwendung des angegebenen Wiederherstellungs Kennworts für 48-Ziffern Folgendes ein:

```
repair-bde C: D: -rp 111111-222222-333333-444444-555555-666666-777777-888888
```

>[!NOTE]
> Das Wiederherstellungs Kennwort sollte in acht Blöcken mit sechs Ziffern eingegeben werden, wobei ein Bindestrich die einzelnen Blöcke trennt.

Zum Erzwingen des Laufwerks c: zum Aufheben der Einbindung versuchen Sie, Laufwerk c: zu reparieren, und dann den Inhalt von Laufwerk c: in Laufwerk D: mithilfe des Wiederherstellungs Schlüssel Pakets und der Wiederherstellungs Schlüsseldatei (Wiederherstellungs Schlüssel. Bek) zu schreiben, die auf Laufwerk F: gespeichert ist, geben Sie Folgendes ein:

```
repair-bde C: D: -kp F:\RecoveryKeyPackage -rk F:\RecoveryKey.bek -f
```

Zum Reparieren des Laufwerks c: und zum Schreiben des Inhalts von Laufwerk c: in Laufwerk D:, wobei Sie ein Kennwort zum Entsperren des Laufwerks c: eingeben müssen (wenn Sie dazu aufgefordert werden), geben Sie Folgendes ein:

```
repair-bde C: D: -pw
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
