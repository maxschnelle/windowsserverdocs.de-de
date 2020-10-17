---
title: unlodctr
description: Referenz Artikel für den unlodctr-Befehl, der die Namen von Leistungs Zählern und die Erläuterung von Text für einen Dienst oder einen Gerätetreiber aus der Systemregistrierung entfernt.
ms.topic: reference
ms.assetid: fc8aa6f0-c1d9-47ea-937a-28152148e774
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 3983f98df0de6a8048f78b6ebdb16cccafea8da4
ms.sourcegitcommit: f45640cf4fda621b71593c63517cfdb983d1dc6a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2020
ms.locfileid: "92156657"
---
# <a name="unlodctr"></a>unlodctr

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Entfernt die **Namen von Leistungs Zählern** und **erläutert den Text** für einen Dienst oder einen Gerätetreiber aus der Systemregistrierung.

> [!WARNING]
> Durch eine fehlerhafte Bearbeitung der Registrierung können schwerwiegende Schäden am System verursacht werden. Bevor Sie Änderungen an der Registrierung vornehmen, sollten Sie alle wichtigen Computerdaten sichern.

## <a name="syntax"></a>Syntax

```
unlodctr <drivername>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| `<drivername>` | Entfernt die **Namen Einstellungen des Leistungs Zählers** und den **erläuternden Text** für Treiber oder Dienst `<drivername>` aus der Windows Server-Registrierung. Wenn `<drivername>` das Leerzeichen enthält, müssen Sie den Text in Anführungszeichen setzen, z. b. "Treiber Name". |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um die Namen und den **erläuternden Text** des aktuellen **Leistungs Zählers** für den Simple Mail Transfer Protocol (SMTP) zu entfernen:

```
unlodctr SMTPSVC
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
