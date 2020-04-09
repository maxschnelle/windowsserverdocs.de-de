---
title: bitsadmin getdisplayname
description: Windows-Befehls Thema für **bizadmin GetDisplayName**, der den anzeigen amen des angegebenen Auftrags abruft.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e5c0e76c-4cc6-42d8-ac30-30bf3dc11b9b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6944dc2b7a63ca986fb285d26796f350c1052295
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850713"
---
# <a name="bitsadmin-getdisplayname"></a>bitsadmin getdisplayname

Ruft den anzeigen amen des angegebenen Auftrags ab.

## <a name="syntax"></a>Syntax

```
bitsadmin /getdisplayname <job>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Im folgenden Beispiel wird der Anzeige Name für den Auftrag mit dem Namen " *mydownloadjob*" abgerufen.

```
C:\>bitsadmin /getdisplayname myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)