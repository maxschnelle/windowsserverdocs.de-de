---
title: bitadmin-setpeer-cachingflags
description: Windows-Befehls Thema für BITSAdmin setpeercachingflags, mit dem Flags festgelegt werden, die bestimmen, ob die Dateien des Auftrags zwischengespeichert und für Peers bereitgestellt werden können und ob der Auftrag Inhalt von Peers herunterladen kann.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3f54a127-fb68-49a5-b843-664ec833df67
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d19e4d14b47e4aa96e9ad9d4367e872350ad4d43
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80849243"
---
# <a name="bitsadmin-setpeercachingflags"></a>bitadmin-setpeer-cachingflags

Legt Flags fest, die bestimmen, ob die Dateien des Auftrags zwischengespeichert und für Peers bereitgestellt werden können und ob der Auftrag Inhalt von Peers herunterladen kann.

## <a name="syntax"></a>Syntax

```
bitsadmin /SetPeerCachingFlags <Job> <value> 
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Der Anzeige Name oder GUID des Auftrags.|
|Wert|Der Wert ist eine ganze Zahl ohne Vorzeichen mit der folgenden Interpretation für die Bits in der binären Darstellung.</br>1: der Auftrag kann Inhalt von Peers herunterladen.</br>2: die Dateien des Auftrags können zwischengespeichert und für Peers bereitgestellt werden.|

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Im folgenden Beispiel werden Flags für den Auftrag mit dem Namen *MyJob* festgelegt, mit dem der Inhalt von Peers heruntergeladen werden kann.
```
C:\>bitsadmin / SetPeerCachingFlags myJob 1 
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)