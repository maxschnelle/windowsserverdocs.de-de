---
title: bitsadmin rawreturn
description: Windows-Befehle Thema **Bitsadmin Rawreturn** – gibt Daten zurück, für die Analyse geeignet ist.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bbe97130-26f6-4cdd-84f1-baf530ce38b7
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4e12c8e621021d35ac618b4592515fe38c36be0e
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66434888"
---
# <a name="bitsadmin-rawreturn"></a>bitsadmin rawreturn

Gibt Daten zurück, das für die Analyse geeignet ist.

## <a name="syntax"></a>Syntax

```
bitsadmin /RawReturn
```

## <a name="remarks"></a>Hinweise

Zeilenumbruchzeichen leisten und die Formatierung aus der Ausgabe.

Normalerweise verwenden Sie diesen Befehl in Verbindung mit der **erstellen** und **erhalten\\** * Switches, um nur den Wert zu erhalten. Sie müssen diesen Switch vor anderen Schaltern angeben.

## <a name="BKMK_examples"></a>Beispiele für

Das folgende Beispiel ruft die Rohdaten für den Status des Auftrags mit dem Namen *MyDownloadJob*.
```
C:\>bitsadmin /RawReturn /GetState myDownloadJob
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)