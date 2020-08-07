---
title: bitsadmin getaclflags
description: Referenz Artikel für den BITSAdmin getaclflags-Befehl, der die weitergabeweitergabeflags der Zugriffs Steuerungs Liste (ACL) abruft.
ms.topic: article
ms.assetid: 99266def-7479-4430-a61c-98ec433fa88b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 437ad345ec778290499b7b128ee08ffd41be320c
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87894576"
---
# <a name="bitsadmin-getaclflags"></a>bitsadmin getaclflags

Ruft die weitergabeweitergabeflags der Zugriffs Steuerungs Liste (ACL) ab und gibt an, ob Elemente von untergeordneten Objekten geerbt werden.

## <a name="syntax"></a>Syntax

```
bitsadmin /getaclflags <job>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

### <a name="remarks"></a>Bemerkungen

Gibt einen oder mehrere der folgenden Flagwerte zurück:

- **o** -Besitzer Informationen mit Datei kopieren.

- **g** -Gruppeninformationen in Datei kopieren.

- **d** : Kopieren Sie die DACL-Informationen ("-Zugriffs Steuerungs Liste") mit der Datei.

- **s** -Informationen zur System Zugriffs Steuerungs Liste (SACL) mit Datei kopieren.

## <a name="examples"></a>Beispiele

Zum Abrufen der Weitergabeflags für die Zugriffs Steuerungs Liste für den Auftrag *mydownloadjob*:

```
bitsadmin /getaclflags myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
