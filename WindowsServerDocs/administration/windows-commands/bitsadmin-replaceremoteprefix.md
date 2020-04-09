---
title: bitsadmin replaceremoteprefix
description: Windows-Befehls Thema für **bigsadmin REPLACEREMOTEPREFIX**, das die Remote-URL für alle Dateien im Auftrag von *oldprefix* in *newprefix*ändert, je nach Bedarf.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: d0e0abb1-bdb4-4c74-abbc-16c809f5fd81
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0cea0108a292815e31e893e91dc4079305c1da9a
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80849813"
---
# <a name="bitsadmin-replaceremoteprefix"></a>bitsadmin replaceremoteprefix

Ändert die Remote-URL für alle Dateien im Auftrag bei Bedarf von *oldprefix* in *newprefix*.

## <a name="syntax"></a>Syntax

```
bitsadmin /replaceremoteprefix <job> <oldprefix> <newprefix>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |
| oldprefix | Vorhandenes URL-Präfix. |
| newprefix | Neues URL-Präfix. |

## <a name="examples"></a>Beispiele

Im folgenden Beispiel wird die Remote-URL für alle Dateien in Auftrag mit dem Namen *mydownloadjob*von *http://stageserver* in *http://prodserver* geändert.

```
C:\>bitsadmin /replaceremoteprefix myDownloadJob http://stageserver http://prodserver
```

## <a name="additional-information"></a>Zusätzliche Informationen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)