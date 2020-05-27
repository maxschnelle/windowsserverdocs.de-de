---
title: unlodctr
description: Referenz Thema für unlodctr, mit dem Namen von Leistungs Zählern und der erläuternde Text für einen Dienst oder einen Gerätetreiber aus der Systemregistrierung entfernt werden
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: fc8aa6f0-c1d9-47ea-937a-28152148e774
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8551b6fc76984b06f28bdda92dcd63791721ec90
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2020
ms.locfileid: "83821290"
---
# <a name="unlodctr"></a>unlodctr

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Entfernt die Namen von **Leistungs Zählern** und **erläutert** den Text für einen Dienst oder einen Gerätetreiber aus der Systemregistrierung.

## <a name="syntax"></a>Syntax
```
Unlodctr <DriverName>
```
#### <a name="parameters"></a>Parameter
|Parameter|BESCHREIBUNG|
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
## <a name="additional-references"></a>Zusätzliche Referenzen
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

