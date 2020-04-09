---
title: bitsadmin Beschreibung
description: Windows-Befehls Thema für bitadmin setDescription, mit dem die Beschreibung des angegebenen Auftrags festgelegt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 1e46a5dd-4637-4a2e-b88f-d3f85b177db8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4a17f864e3bc3b3cdc8ba0d76d553bcfcef27d29
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80849563"
---
# <a name="bitsadmin-setdescription"></a>bitsadmin Beschreibung

Legt die Beschreibung des angegebenen Auftrags fest.

## <a name="syntax"></a>Syntax

```
bitsadmin /SetDescription <Job> <Description>
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Der Anzeige Name oder GUID des Auftrags.|
|Beschreibung|Der Text, der zur Beschreibung des Auftrags verwendet wird.|

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Im folgenden Beispiel wird die Beschreibung für den Auftrag mit dem Namen " *mydownloadjob*" abgerufen.
```
C:\>bitsadmin /SetDescription myDownloadJob Music Downloads
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)