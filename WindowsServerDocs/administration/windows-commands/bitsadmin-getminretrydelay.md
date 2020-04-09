---
title: bitsadmin getminretrydelay
description: 'Windows-Befehls Thema für **bizadmin getminretrydelay**: Hiermit wird die Zeitspanne (in Sekunden) abgerufen, die der Dienst nach dem Auftreten eines vorübergehenden Fehlers wartet, bevor versucht wird, die Datei zu übertragen.'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 54f0abab-c129-40ed-a603-50f464d26011
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d79ffdf1f45b0198b4af535ed83154c3c2ec24f4
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850623"
---
# <a name="bitsadmin-getminretrydelay"></a>bitsadmin getminretrydelay

Ruft die Zeitdauer in Sekunden ab, die der Dienst nach dem Auftreten eines vorübergehenden Fehlers wartet, bevor versucht wird, die Datei zu übertragen.

## <a name="syntax"></a>Syntax

```
bitsadmin /getminretrydelay <job>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Im folgenden Beispiel wird die minimale Wiederholungs Verzögerung für den Auftrag mit dem Namen " *mydownloadjob*" abgerufen.

```
C:\>bitsadmin /getminretrydelay myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)