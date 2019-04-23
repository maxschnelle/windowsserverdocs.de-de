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
ms.openlocfilehash: eabcc5cacdcc5f7f4de7178b5afeff2acc89d7a8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59862811"
---
#<a name="bitsadmin-getpeercachingflags"></a>Bitsadmin getpeercachingflags

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
[Befehlszeilensyntax](command-line-syntax-key.md)


