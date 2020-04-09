---
title: bitsadmin getreplyprogress
description: Windows-Befehls Thema für **BITSAdmin getreplyprogress**, das die Größe und den Fortschritt der Server Upload-Antwort abruft.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7f7cb0b4-ad95-44fd-a35d-0ddf5fc0b0d0
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 195ed669817bc0aca7ebc432e7f3c66ab1548162
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850483"
---
# <a name="bitsadmin-getreplyprogress"></a>bitsadmin getreplyprogress

Ruft die Größe und den Fortschritt der Server Upload-Antwort ab.

> [!NOTE]
> Dieser Befehl wird von Bits 1,2 und früheren Versionen nicht unterstützt.

## <a name="syntax"></a>Syntax

```
bitsadmin /getreplyprogress <job>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |


## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Im folgenden Beispiel wird der Status der Upload-Antwort für den Auftrag mit dem Namen " *mydownloadjob*" abgerufen.

```
C:\>bitsadmin /getreplyprogress myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)