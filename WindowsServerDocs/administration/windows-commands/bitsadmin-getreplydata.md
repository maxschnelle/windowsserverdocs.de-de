---
title: bitsadmin getreplydata
description: Windows-Befehls Thema für **BITSAdmin getreplydata**, das die uploadantwortdaten des Servers im Hexadezimal Format für den Auftrag abruft.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 819f97d5-b255-4b2d-9f63-0daa73915434
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: fb83ca93f8e73445788d926e0d5e6db4c774d759
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850503"
---
# <a name="bitsadmin-getreplydata"></a>bitsadmin getreplydata

Ruft die uploadantwortdaten des Servers im Hexadezimal Format für den Auftrag ab.

> [!NOTE]
> Dieser Befehl wird von Bits 1,2 und früheren Versionen nicht unterstützt.

## <a name="syntax"></a>Syntax

```
bitsadmin /getreplydata <job>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Im folgenden Beispiel werden die uploadantwortdaten für den Auftrag *mydownloadjob*abgerufen.

```
C:\>bitsadmin /getreplydata myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)