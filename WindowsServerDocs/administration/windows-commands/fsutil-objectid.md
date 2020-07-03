---
title: fsutil objectid
description: Referenz Artikel für den Befehl fsutil objectid, mit dem Objekt Bezeichner zum Nachverfolgen anderer Objekte wie Dateien, Verzeichnisse und Links verwaltet werden.
ms.prod: windows-server
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
ms.assetid: 693ab895-9d0c-47c1-9f52-df5cd287842a
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: 5ab0b95bdcde8bce51e1d5a2c14888229621fcaa
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85925240"
---
# <a name="fsutil-objectid"></a>fsutil objectid

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8

Verwaltet Objekt-IDs (OIDs), bei denen es sich um interne Objekte handelt, die vom DLT-Client Dienst (DLT) und Datei Replikations Dienst (File Replication Service, FRS) verwendet werden, um andere Objekte wie Dateien, Verzeichnisse und Links nachzuververfolgen. Objekt-IDs sind für die meisten Programme unsichtbar und sollten nie geändert werden.

> [!WARNING]
> Löschen, festlegen oder anderweitig ändern Sie einen Objekt Bezeichner nicht. Das Löschen oder Festlegen eines Objekt Bezeichners kann zum Verlust von Daten aus Teilen einer Datei führen, bis zu und einschließlich ganzer Datenmengen. Außerdem können Sie im DLT-Client Dienst (DLT) und im Datei Replikations Dienst (File Replication Service, FRS) ein negatives Verhalten verursachen.

## <a name="syntax"></a>Syntax

```
fsutil objectid [create] <filename>
fsutil objectid [delete] <filename>
fsutil objectid [query] <filename>
fsutil objectid [set] <objectID> <birthvolumeID> <birthobjectID> <domainID> <filename>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| create | Erstellt einen Objekt Bezeichner, wenn die angegebene Datei nicht bereits über einen verfügt. Wenn die Datei bereits über einen Objekt Bezeichner verfügt, entspricht dieser Unterbefehl dem **Abfrage** Unterbefehl. |
| delete | Löscht einen Objekt Bezeichner. |
| Abfrage | Fragt einen Objekt Bezeichner ab. |
| set | Legt einen Objekt Bezeichner fest. |
| `<objectID>` | Legt einen Datei spezifischen hexadezimalen Bezeichner mit 16 Bytes fest, der innerhalb eines Volumes garantiert eindeutig ist. Der Objekt Bezeichner wird vom DLT-Client Dienst (DLT) und dem Datei Replikations Dienst (File Replication Service, FRS) verwendet, um Dateien zu identifizieren. |
| `<birthvolumeID>` | Gibt das Volume an, auf dem sich die Datei befand, als Sie zum ersten Mal einen Objekt Bezeichner abgerufen hat. Dieser Wert ist ein hexadezimal-16-Byte-Bezeichner, der vom DLT-Client Dienst verwendet wird. |
| `<birthobjectID>` | Gibt den ursprünglichen Objekt Bezeichner der Datei an (die *objectID* kann sich beim Verschieben einer Datei ändern). Dieser Wert ist ein hexadezimal-16-Byte-Bezeichner, der vom DLT-Client Dienst verwendet wird. |
| `<domainID>` | hexadezimale 16-Byte-Domänen Bezeichner. Dieser Wert wird derzeit nicht verwendet und muss auf alle Nullen festgelegt werden. |
| `<filename>` | Gibt den vollständigen Pfad zur Datei einschließlich des Datei namens und der Erweiterung an, z. b. *C:\documents\filename.txt*. |

#### <a name="remarks"></a>Hinweise

- Jede Datei mit einem Objekt Bezeichner verfügt auch über einen Geburts volumenbezeichner, einen Geburts Objekt Bezeichner und einen Domänen Bezeichner. Wenn Sie eine Datei verschieben, kann sich der Objekt Bezeichner ändern, aber das Geburts Volume und die Geburts Objekt-IDs bleiben unverändert. Dieses Verhalten ermöglicht es dem Windows-Betriebssystem, immer eine Datei zu finden, unabhängig davon, wohin Sie verschoben wurde.

### <a name="examples"></a>Beispiele

Zum Erstellen eines Objekt Bezeichners geben Sie Folgendes ein:

`fsutil objectid create c:\temp\sample.txt`

Zum Löschen eines Objekt Bezeichners geben Sie Folgendes ein:

`fsutil objectid delete c:\temp\sample.txt`

Zum Abfragen eines Objekt Bezeichners geben Sie Folgendes ein:

`fsutil objectid query c:\temp\sample.txt`

Zum Festlegen eines Objekt Bezeichners geben Sie Folgendes ein:

`fsutil objectid set 40dff02fc9b4d4118f120090273fa9fc f86ad6865fe8d21183910008c709d19e 40dff02fc9b4d4118f120090273fa9fc 00000000000000000000000000000000 c:\temp\sample.txt`

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [fsutil](fsutil.md)
