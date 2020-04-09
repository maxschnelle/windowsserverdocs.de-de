---
title: bitsadmin getnotifycmdline
description: Windows-Befehls Thema für **bizadmin getnotifycmdline**, das den Befehlszeilen Befehl abruft, der ausgeführt wird, wenn der Auftrag das Übertragen von Daten abgeschlossen hat.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 90fa33e6-aca5-4a23-82bd-19a9f13f8416
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 24b49b3fa0c2dafb999d8cb9c6e0c13ae68bf6f4
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850593"
---
# <a name="bitsadmin-getnotifycmdline"></a>bitsadmin getnotifycmdline

Ruft den Befehlszeilen Befehl ab, der ausgeführt werden soll, wenn der Auftrag das Übertragen von Daten abgeschlossen hat.

> [!NOTE]
> Dieser Befehl wird von Bits 1,2 und früheren Versionen nicht unterstützt.

## <a name="syntax"></a>Syntax

```
bitsadmin /getnotifycmdline <job>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Im folgenden Beispiel wird der Befehlszeilen Befehl abgerufen, der vom-Dienst verwendet wird, wenn der Auftrag mit dem Namen *mydownloadjob* abgeschlossen ist.

```
C:\>bitsadmin /getnotifycmdline myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)