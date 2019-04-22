---
title: Bitsadmin setpeercachingflags
description: Windows-Befehle Thema **Bitsadmin Setpeercachingflags** -Flags, die bestimmen, wenn die Dateien des Auftrags können zwischengespeichert und für Kollegen bereitgestellt und der Auftrag von Peers herunterladen kann, legt sie fest.
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 2d50a6ccd83a6251808ca3d66437e52f641c60a7
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59814251"
---
# <a name="bitsadmin-setpeercachingflags"></a>Bitsadmin setpeercachingflags



Legt ein Kennzeichen, die bestimmen, wenn die Dateien des Auftrags können zwischengespeichert und für Kollegen bereitgestellt und der Auftrag herunterladen kann Inhalt von Peers fest.

## <a name="syntax"></a>Syntax

```
bitsadmin /SetPeerCachingFlags <Job> <value> 
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Anzeigenamen oder die GUID des Auftrags|
|Wert|Der Wert ist eine Ganzzahl ohne Vorzeichen, mit der folgenden Interpretation für die Bits in die binäre Darstellung.</br>1: der Auftrag kann Inhalte von Peers herunterladen.</br>2 – die Dateien des Auftrags können zwischengespeichert und für Kollegen bereitgestellt.|

## <a name="BKMK_examples"></a>Beispiele für

Im folgenden Beispiel wird die Flags für den Auftrag mit dem Namen *MyJob* zu ermöglichen, Inhalt von Peers herunterzuladen.
```
C:\>bitsadmin / SetPeerCachingFlags myJob 1 
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)