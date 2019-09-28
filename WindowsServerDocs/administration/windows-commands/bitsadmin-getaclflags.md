---
title: bitsadmin getaclflags
description: Windows-Befehls Thema für **BITSAdmin getaclflags** -Ruft die weitergabeweitergabeflags der Zugriffs Steuerungs Liste ab.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 99266def-7479-4430-a61c-98ec433fa88b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ad98cd742161ae06be5cba7acde7b810eaf199d6
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381791"
---
# <a name="bitsadmin-getaclflags"></a>bitsadmin getaclflags

Ruft die weitergabeweitergabeflags der Zugriffs Steuerungs Liste (ACL) ab.

## <a name="syntax"></a>Syntax

```
bitsadmin /GetAclFlags <Job>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Der Anzeige Name oder GUID des Auftrags.|

## <a name="remarks"></a>Hinweise

Zeigt einen oder mehrere der folgenden Flagwerte an:
-   ' Besitzer Informationen in Datei kopieren.
-   SELBST Kopieren Sie Gruppeninformationen mit der Datei.
-   D: Kopieren Sie DACL-Informationen mit der Datei.
-   HYMNEN Kopieren Sie SACL-Informationen in die Datei.

## <a name="BKMK_examples"></a>Beispiele

Im folgenden Beispiel werden die Weitergabeflags für die Zugriffs Steuerungs Liste für den Auftrag mit dem Namen *mydownloadjob*abgerufen.
```
C:\>bitsadmin /getaclflags myDownloadJob
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)