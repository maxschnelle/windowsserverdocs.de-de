---
title: bitsadmin getminretrydelay
description: Referenz Thema für den bizadmin getminretrydelay-Befehl, der die Zeitspanne (in Sekunden) abruft, die der Dienst nach einem vorübergehenden Fehler wartet, bevor er versucht, die Datei zu übertragen.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 54f0abab-c129-40ed-a603-50f464d26011
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a50b9d98fe0b873dc58b8e86dc672a8f4157208a
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717845"
---
# <a name="bitsadmin-getminretrydelay"></a>bitsadmin getminretrydelay

Ruft die Zeitdauer in Sekunden ab, die der Dienst nach dem Auftreten eines vorübergehenden Fehlers wartet, bevor versucht wird, die Datei zu übertragen.

## <a name="syntax"></a>Syntax

```
bitsadmin /getminretrydelay <job>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="examples"></a>Beispiele

So rufen Sie die minimale Wiederholungs Verzögerung für den Auftrag mit dem Namen *mydownloadjob*ab:

```
bitsadmin /getminretrydelay myDownloadJob
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
