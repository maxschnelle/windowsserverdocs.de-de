---
title: bitsadmin fortsetzen
description: Windows-Befehle Thema **Bitsadmin fortsetzen** -aktiviert einen neuen oder angehaltenen Auftrag in der Übertragungswarteschlange.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7c7540a9-a11a-4910-923a-2a2a61cbf11d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 76027ac927f8a9bb2558e3ce6d75e4f6692e56e7
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59842031"
---
# <a name="bitsadmin-resume"></a>bitsadmin fortsetzen



Aktiviert einen neuen oder angehaltenen Auftrag in der Übertragungswarteschlange.

## <a name="syntax"></a>Syntax

```
bitsadmin /Resume <Job>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Anzeigenamen oder die GUID des Auftrags|

## <a name="BKMK_examples"></a>Beispiele für

Im folgende Beispiel wird der Auftrag, der mit dem Namen fortgesetzt *MyDownloadJob*.
```
C:\>bitsadmin /Resume myDownloadJob
```
Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)