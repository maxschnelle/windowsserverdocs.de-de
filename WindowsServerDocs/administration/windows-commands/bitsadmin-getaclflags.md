---
title: bitsadmin getaclflags
description: Referenz Artikel für den BITSAdmin getaclflags-Befehl, der die weitergabeweitergabeflags der Zugriffs Steuerungs Liste (ACL) abruft.
ms.topic: reference
ms.assetid: 99266def-7479-4430-a61c-98ec433fa88b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5254d65bb5ba3e35fcf5368e24045530a76bfd95
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89033698"
---
# <a name="bitsadmin-getaclflags"></a>bitsadmin getaclflags

Ruft die weitergabeweitergabeflags der Zugriffs Steuerungs Liste (ACL) ab und gibt an, ob Elemente von untergeordneten Objekten geerbt werden.

## <a name="syntax"></a>Syntax

```
bitsadmin /getaclflags <job>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
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
