---
title: bitadmin-setpeer-cachingflags
description: 'Windows-Befehls Thema für **BITSAdmin setpeercachingflags** : Legt Flags fest, die bestimmen, ob die Dateien des Auftrags zwischengespeichert und für Peers bereitgestellt werden können und ob der Auftrag Inhalt von Peers herunterladen kann.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3f54a127-fb68-49a5-b843-664ec833df67
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 147f28268f1b4dd6dfb40cff85f073feabbc35a0
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380462"
---
# <a name="bitsadmin-setpeercachingflags"></a>bitadmin-setpeer-cachingflags



Legt Flags fest, die bestimmen, ob die Dateien des Auftrags zwischengespeichert und für Peers bereitgestellt werden können und ob der Auftrag Inhalt von Peers herunterladen kann.

## <a name="syntax"></a>Syntax

```
bitsadmin /SetPeerCachingFlags <Job> <value> 
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Der Anzeige Name oder GUID des Auftrags.|
|Wert|Der Wert ist eine ganze Zahl ohne Vorzeichen mit der folgenden Interpretation für die Bits in der binären Darstellung.</br>1: der Auftrag kann Inhalt von Peers herunterladen.</br>2: die Dateien des Auftrags können zwischengespeichert und für Peers bereitgestellt werden.|

## <a name="BKMK_examples"></a>Beispiele

Im folgenden Beispiel werden Flags für den Auftrag mit dem Namen *MyJob* festgelegt, mit dem der Inhalt von Peers heruntergeladen werden kann.
```
C:\>bitsadmin / SetPeerCachingFlags myJob 1 
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)