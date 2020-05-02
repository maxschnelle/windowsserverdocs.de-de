---
title: bitsadmin getnotifycmdline
description: Referenz Thema für den bizadmin getnotifycmdline-Befehl, der den Befehlszeilen Befehl abruft, der ausgeführt wird, wenn der Auftrag das Übertragen von Daten abgeschlossen hat.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 90fa33e6-aca5-4a23-82bd-19a9f13f8416
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4d4c47c4a1b9ea06fd804c8f2c48e9ac0ce1b319
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717800"
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

| Parameter | BESCHREIBUNG |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="examples"></a>Beispiele

Zum Abrufen des Befehlszeilen Befehls, der vom Dienst verwendet wird, wenn der Auftrag mit dem Namen *mydownloadjob* abgeschlossen ist.

```
bitsadmin /getnotifycmdline myDownloadJob
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
