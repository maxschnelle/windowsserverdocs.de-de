---
title: bitsadmin getnoprogresstimeout
description: 'Windows-Befehls Thema für **bistiadmin getnoprogresstimeout**: Hiermit wird die Zeitspanne (in Sekunden) abgerufen, die der Dienst versucht, die Datei zu übertragen, nachdem ein vorübergehender Fehler aufgetreten ist.'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 9cd9b19b-cbb4-4352-8419-978080f016b6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: cf2cfd77b494e221b60c8816ff46eed5f9252f39
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850603"
---
# <a name="bitsadmin-getnoprogresstimeout"></a>bitsadmin getnoprogresstimeout

Ruft die Zeitdauer in Sekunden ab, die der Dienst versucht, die Datei zu übertragen, nachdem ein vorübergehender Fehler aufgetreten ist.

## <a name="syntax"></a>Syntax

```
bitsadmin /getnoprogresstimeout <job>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Im folgenden Beispiel wird der Wert für den Status Timeout für den Auftrag mit dem Namen " *mydownloadjob*" abgerufen.

```
C:\>bitsadmin /getnoprogresstimeout myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)