---
title: bitsadmin setpriority
description: Windows-Befehls Thema für bitadmin SetPriority, mit dem die Priorität des angegebenen Auftrags festgelegt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 90788363-01a2-4d7c-a560-a3eba45b5e9e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7d007c62402a3d70910e1c79fab5c406295a63a5
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80849213"
---
# <a name="bitsadmin-setpriority"></a>bitsadmin setpriority

Legt die Priorität des angegebenen Auftrags fest.

## <a name="syntax"></a>Syntax

```
bitsadmin /SetPriority <Job> <Priority>
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Der Anzeige Name oder GUID des Auftrags.|
|Priority|Einer der folgenden Werte:</br>-Vordergrund</br>-Hoch</br>-NORMAL</br>-Niedrig|

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Im folgenden Beispiel wird die Priorität für den Auftrag mit dem Namen *mydownloadjob* auf Normal festgelegt.
```
C:\>bitsadmin /SetPriority myDownloadJob NORMAL
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)