---
title: bitadmin getPeer Cache-Flags
description: Windows-Befehls Thema für **BITSAdmin getpeercachingflags** -Ruft Flags ab, die bestimmen, ob die Dateien des Auftrags zwischengespeichert und für Peers bereitgestellt werden können, und ob Bits Inhalt für den Auftrag von Peers herunterladen kann.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3c3c9f28-4c04-4c49-a23a-dee5bbcc8981
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6b86214b5289a59e8db2ecff065ab3b8cd17007e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381436"
---
# <a name="bitsadmin-getpeercachingflags"></a>bitadmin getPeer Cache-Flags

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ruft Flags ab, die bestimmen, ob die Dateien des Auftrags zwischengespeichert und für Peers bereitgestellt werden können, und ob Bits Inhalt für den Auftrag von Peers herunterladen kann.

## <a name="syntax"></a>Syntax

```
bitsadmin /GetPeerCachingFlags <Job> 
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|-------|--------|
|Auftrag|Der Anzeige Name oder GUID des Auftrags.|

## <a name="BKMK_examples"></a>Beispiele
Im folgenden Beispiel werden die Flags für den Auftrag mit dem Namen " *MyJob*" abgerufen.

```
C:\>bitsadmin /GetPeerCachingFlags myJob
```

## <a name="additional-references"></a>Weitere Verweise
[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)


