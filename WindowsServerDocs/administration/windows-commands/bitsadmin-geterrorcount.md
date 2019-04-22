---
title: bitsadmin geterrorcount
description: Windows-Befehle Thema **Bitsadmin Geterrorcount** -Ruft die Anzahl wie oft einen vorübergehenden Fehler, der angegebene Auftrag generiert.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8840ae78-52b0-4c7e-b592-0547359a237e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 91045372931efec0e3189132a275eeacab584de4
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59818371"
---
# <a name="bitsadmin-geterrorcount"></a>bitsadmin geterrorcount



Ruft die Anzahl der Male, die der angegebene Auftrag um einen vorübergehenden Fehler generiert.

## <a name="syntax"></a>Syntax

```
bitsadmin /GetErrorCount <Job>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Anzeigenamen oder die GUID des Auftrags|

## <a name="BKMK_examples"></a>Beispiele für

Das folgende Beispiel ruft die Anzahl der Fehlerinformationen für den Auftrag mit dem Namen *MyDownloadJob*.
```
C:\>bitsadmin /GetErrorCount myDownloadJob
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)