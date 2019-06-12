---
title: Bitsadmin getpeercachingflags
description: Windows-Befehle Thema **Bitsadmin Getpeercachingflags** -Flags, die bestimmen, wenn die Dateien des Auftrags können zwischengespeichert und für Kollegen bereitgestellt und BITS download des Inhalts für den Auftrag von Peers abgerufen.
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 28f248bab3e3cc3f5c7dd4f5f878f0b6d776029b
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66434927"
---
# <a name="bitsadmin-getpeercachingflags"></a>Bitsadmin getpeercachingflags

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Ruft die Flags, die bestimmen, wenn die Dateien des Auftrags können zwischengespeichert und für Kollegen bereitgestellt und BITS für den Auftrag von Peers herunterladen können.

## <a name="syntax"></a>Syntax

```
bitsadmin /GetPeerCachingFlags <Job> 
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|-------|--------|
|Auftrag|Anzeigenamen oder die GUID des Auftrags|

## <a name="BKMK_examples"></a>Beispiele für
Im folgende Beispiel ruft die Flags für den Auftrag mit dem Namen *MyJob*.

```
C:\>bitsadmin /GetPeerCachingFlags myJob
```

## <a name="additional-references"></a>Zusätzliche Referenzen
[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)


