---
title: bitadmin getsecurityflags
description: Windows-Befehls Thema für **bitadmin getsecurityflags** -meldet die http-sicherheitsflags für die URL-Umleitung und Überprüfungen, die für das Serverzertifikat während der Übertragung ausgeführt werden.
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: fb53664a6366b411ae1eb9b0fe7c93392d60b542
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381458"
---
# <a name="bitsadmin-getsecurityflags"></a>bitadmin getsecurityflags

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Meldet die http-sicherheitsflags für die URL-Umleitung und Überprüfungen, die für das Serverzertifikat während der Übertragung ausgeführt werden.

## <a name="syntax"></a>Syntax

```
bitsadmin /GetSecurityFlags <Job> 
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|-------|--------|
|Auftrag|Der Anzeige Name oder GUID des Auftrags.|

## <a name="BKMK_examples"></a>Beispiele
Im folgenden Beispiel werden die "securitly"-Flags aus einem Auftrag mit dem Namen " *MyJob*" abgerufen.

```
C:\>bitsadmin /GetSecurityFlags myJob 
```

## <a name="additional-references"></a>Weitere Verweise
[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)


