---
title: bitsadmin getreplyfilename
description: Windows-Befehls Thema für **BITSAdmin getreplyfilename**, mit dem der Pfad der Datei abgerufen wird, die die Server Upload-Antwort für den Auftrag enthält.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 85447184-1732-4816-a365-2e3599551bf8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 541a6e60d641405b5da2e65fecbbbe87468c8702
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850493"
---
# <a name="bitsadmin-getreplyfilename"></a>bitsadmin getreplyfilename

Ruft den Pfad der Datei ab, die die Server Upload-Antwort für den Auftrag enthält.

> [!NOTE]
> Dieser Befehl wird von Bits 1,2 und früheren Versionen nicht unterstützt.

## <a name="syntax"></a>Syntax

```
bitsadmin /getreplyfilename <job>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |


## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Im folgenden Beispiel wird der Upload-Antwort Dateiname für den Auftrag mit dem Namen *mydownloadjob*abgerufen.

```
C:\>bitsadmin /getreplyfilename myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)