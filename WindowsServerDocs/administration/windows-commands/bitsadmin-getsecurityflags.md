---
title: Bitsadmin getsecurityflags
description: Windows-Befehle Thema **Bitsadmin Getsecurityflags** – meldet die HTTP-Security-Flags für die URL-Umleitung und für das Serverzertifikat überprüft, während der Übertragung.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c2e73519-34f4-487b-af11-97d5d08ef9bb
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6e1db167b12d47afccb8842da617f1e9fe72acff
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66434959"
---
# <a name="bitsadmin-getsecurityflags"></a>Bitsadmin getsecurityflags

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Berichte der HTTP-Security-Flags für URL-Umleitung und überprüft, die auf dem Serverzertifikat während der Übertragung ausgeführt wird.

## <a name="syntax"></a>Syntax

```
bitsadmin /GetSecurityFlags <Job> 
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|-------|--------|
|Auftrag|Anzeigenamen oder die GUID des Auftrags|

## <a name="BKMK_examples"></a>Beispiele für
Das folgende Beispiel ruft die Flags Securitly aus einem Auftrag mit dem Namen *MyJob*.

```
C:\>bitsadmin /GetSecurityFlags myJob 
```

## <a name="additional-references"></a>Zusätzliche Referenzen
[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)


