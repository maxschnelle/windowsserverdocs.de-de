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
ms.openlocfilehash: 97d889b54c4b0de0230c50e1d7c8d21617ea881a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59835851"
---
#<a name="bitsadmin-getsecurityflags"></a>Bitsadmin getsecurityflags

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
[Befehlszeilensyntax](command-line-syntax-key.md)


