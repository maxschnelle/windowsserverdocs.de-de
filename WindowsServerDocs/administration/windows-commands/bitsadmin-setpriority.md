---
title: bitsadmin setpriority
description: Windows-Befehle Thema **Bitsadmin Setpriority** -legt die Priorität des angegebenen Auftrags fest.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 90788363-01a2-4d7c-a560-a3eba45b5e9e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 072f22ae8c928d427104062b8cbf0f8f42ac4416
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59882211"
---
# <a name="bitsadmin-setpriority"></a>bitsadmin setpriority



Legt die Priorität des angegebenen Auftrags fest.

## <a name="syntax"></a>Syntax

```
bitsadmin /SetPriority <Job> <Priority>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Anzeigenamen oder die GUID des Auftrags|
|Priority|Einer der folgenden Werte:</br>: VORDERGRUND</br>– HIGH</br>-   NORMAL</br>– NIEDRIG|

## <a name="BKMK_examples"></a>Beispiele für

Im folgenden Beispiel wird die Priorität für den Auftrag mit dem Namen *MyDownloadJob* Normal.
```
C:\>bitsadmin /SetPriority myDownloadJob NORMAL
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)