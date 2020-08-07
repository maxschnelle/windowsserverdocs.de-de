---
title: bitsadmin addfile
description: Referenz Artikel für den bizadmin AddFile-Befehl, mit dem dem angegebenen Auftrag eine Datei hinzugefügt wird.
ms.topic: article
ms.assetid: 1b31aa93-0364-465b-af36-754968825989
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c9bc00f1b63c559d048c9ae590df29f7421e42ec
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87894939"
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
