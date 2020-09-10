---
title: bitsadmin addfile
description: Referenz Artikel für den bizadmin AddFile-Befehl, mit dem dem angegebenen Auftrag eine Datei hinzugefügt wird.
ms.topic: reference
ms.assetid: 1b31aa93-0364-465b-af36-754968825989
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 74e77f2af220a057ed0ad87da797e9ae88c7aef5
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89632746"
---
# <a name="bitsadmin-addfile"></a>bitsadmin addfile

Fügt dem angegebenen Auftrag eine Datei hinzu.

## <a name="syntax"></a>Syntax

```
bitsadmin /addfile <job> <remoteURL> <localname>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |
| RemoteURL | Die URL der Datei auf dem Server. |
| localname | Der Name der Datei auf dem lokalen Computer. " *Localname* " muss einen absoluten Pfad zur Datei enthalten. |

## <a name="examples"></a>Beispiele

So fügen Sie dem Auftrag eine Datei hinzu:

```
bitsadmin /addfile myDownloadJob http://downloadsrv/10mb.zip c:\10mb.zip
```

Wiederholen Sie diesen Vorgang für jede hinzu zufügende Datei. Wenn für mehrere Aufträge *mydownloadjob* als Name verwendet wird, müssen Sie *mydownloadjob* durch die GUID des Auftrags ersetzen, um den Auftrag eindeutig zu identifizieren.

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
