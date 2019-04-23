---
title: bitsadmin getaclflags
description: Windows-Befehle Thema **Bitsadmin Getaclflags** -Ruft die Access Control Liste zur Weitergabe von Würmern-Flags.
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 185445a97168344f910abc0e644718296de2c712
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59861451"
---
# <a name="bitsadmin-getaclflags"></a>bitsadmin getaclflags

Ruft die Access Control Zugriffssteuerungsliste (ACL) zur Weitergabe von Würmern-Flags ab.

## <a name="syntax"></a>Syntax

```
bitsadmin /GetAclFlags <Job>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Anzeigenamen oder die GUID des Auftrags|

## <a name="remarks"></a>Hinweise

Zeigt eine oder mehrere der folgenden Flags Werte an:
-   O: Kopieren Sie Informationen über den sperrbesitzer-Datei.
-   G: Kopieren Sie Informationen zur Datei.
-   D: Kopieren Sie DACL-Informationen, mit der Datei.
-   S: Kopieren Sie SACL-Informationen, mit der Datei.

## <a name="BKMK_examples"></a>Beispiele für

Das folgende Beispiel ruft die Access Control Liste Weitergabeflags für den Auftrag mit dem Namen *MyDownloadJob*.
```
C:\>bitsadmin /getaclflags myDownloadJob
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)