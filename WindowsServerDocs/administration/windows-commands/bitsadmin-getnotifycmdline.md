---
title: bitsadmin getnotifycmdline
description: Referenz Artikel für den bizadmin getnotifycmdline-Befehl, der den Befehlszeilen Befehl abruft, der ausgeführt wird, wenn der Auftrag das Übertragen von Daten abgeschlossen hat.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 90fa33e6-aca5-4a23-82bd-19a9f13f8416
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 233186edcdb10d98e1d1139ebd63943647b84ae4
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85926999"
---
# <a name="bitsadmin-getnotifycmdline"></a>bitsadmin getnotifycmdline

Ruft den Befehlszeilen Befehl ab, der ausgeführt werden soll, nachdem der angegebene Auftrag das Übertragen von Daten abgeschlossen hat.

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

## <a name="examples"></a>Beispiele

Zum Abrufen des Befehlszeilen Befehls, der vom Dienst verwendet wird, wenn der Auftrag mit dem Namen *mydownloadjob* abgeschlossen ist.

```
bitsadmin /getnotifycmdline myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
