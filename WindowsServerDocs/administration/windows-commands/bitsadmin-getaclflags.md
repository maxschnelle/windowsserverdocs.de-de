---
title: bitsadmin getaclflags
description: Referenz Artikel für den BITSAdmin getaclflags-Befehl, der die weitergabeweitergabeflags der Zugriffs Steuerungs Liste (ACL) abruft.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 99266def-7479-4430-a61c-98ec433fa88b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0a05a0ed1c29e7cf1b0583ce9a0fcfdbe73e7a12
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85928330"
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
