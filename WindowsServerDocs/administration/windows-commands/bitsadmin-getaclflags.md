---
title: bitsadmin getaclflags
description: Referenz Artikel für den BITSAdmin getaclflags-Befehl, der die weitergabeweitergabeflags der Zugriffs Steuerungs Liste (ACL) abruft.
ms.topic: reference
ms.assetid: 99266def-7479-4430-a61c-98ec433fa88b
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 4c5c7101db157b7fa5b56833b8d5f89619bd8d51
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89632321"
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

### <a name="remarks"></a>Hinweise

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
