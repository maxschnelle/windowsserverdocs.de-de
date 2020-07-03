---
title: unlodctr
description: Referenz Artikel zu unlodctr, mit dem Leistungs Leistungsdaten und der Text für einen Dienst oder einen Gerätetreiber aus der Systemregistrierung entfernt werden
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: fc8aa6f0-c1d9-47ea-937a-28152148e774
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a054673ada197c6b116abc7eda49c0e755f22af0
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85937275"
---
# <a name="unlodctr"></a>unlodctr

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Entfernt die Namen von **Leistungs Zählern** und **erläutert** den Text für einen Dienst oder einen Gerätetreiber aus der Systemregistrierung.

## <a name="syntax"></a>Syntax
```
Unlodctr <DriverName>
```
#### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|\<DriverName>|entfernt die Namen Einstellungen des Leistungs Zählers und den erläuternden Text für Treiber oder Dienst <DriverName> aus der Windows Server 2003-Registrierung.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise
> [!WARNING]
> Durch eine fehlerhafte Bearbeitung der Registrierung können schwerwiegende Schäden am System verursacht werden. Bevor Sie Änderungen an der Registrierung vornehmen, sollten Sie alle wichtigen Computerdaten sichern.

Wenn die Informationen, die Sie angeben, Leerzeichen enthalten, verwenden Sie den Text in Anführungszeichen (z <DriverName> . b.).

## <a name="examples"></a>Beispiele
So entfernen Sie die aktuellen Registrierungs Einstellungen für die Leistung und den leistungsstarken Text für den Simple Mail Transfer Protocol (SMTP)-Dienst:
```
unlodctr SMTPSVC
```
## <a name="additional-references"></a>Weitere Verweise
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

