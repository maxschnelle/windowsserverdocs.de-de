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
ms.openlocfilehash: 80eef106452a45ac4f071446ec8d427b757c443d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59817021"
---
# <a name="bitsadmin-rawreturn"></a>bitsadmin rawreturn

Gibt Daten zurück, das für die Analyse geeignet ist.

## <a name="syntax"></a>Syntax

```
bitsadmin /RawReturn
```

## <a name="remarks"></a>Hinweise

Zeilenumbruchzeichen leisten und die Formatierung aus der Ausgabe.

Normalerweise verwenden Sie diesen Befehl in Verbindung mit der **erstellen** und **erhalten\***  Switches, um nur den Wert zu erhalten. Sie müssen diesen Switch vor anderen Schaltern angeben.

## <a name="BKMK_examples"></a>Beispiele für

Das folgende Beispiel ruft die Rohdaten für den Status des Auftrags mit dem Namen *MyDownloadJob*.
```
C:\>bitsadmin /RawReturn /GetState myDownloadJob
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)