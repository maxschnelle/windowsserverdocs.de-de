---
title: bitsadmin getaclflags
description: Windows-Befehls Thema für **BITSAdmin getaclflags**, das die weitergabesteuerungsflags der Zugriffs Steuerungs Liste (ACL) abruft.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 99266def-7479-4430-a61c-98ec433fa88b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d53018e2fa5c659c8cf4b0ec985beda848a8c1af
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850793"
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

## <a name="remarks"></a>Hinweise

Zeigt einen oder mehrere der folgenden Flagwerte an:

- **o** -Besitzer Informationen mit Datei kopieren.

- **g** -Gruppeninformationen in Datei kopieren.

- **d** : Kopieren Sie die DACL-Informationen ("-Zugriffs Steuerungs Liste") mit der Datei.

- **s** -Informationen zur System Zugriffs Steuerungs Liste (SACL) mit Datei kopieren.

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Im folgenden Beispiel werden die Weitergabeflags für die Zugriffs Steuerungs Liste für den Auftrag mit dem Namen *mydownloadjob*abgerufen.

```
C:\>bitsadmin /getaclflags myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)