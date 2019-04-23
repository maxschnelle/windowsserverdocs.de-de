---
title: regsvr32
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3345e964-7d3e-42b8-abeb-42ed6edfe2b2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 87d9291755ddb4484e85248cb01ad78b01a25965
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59889991"
---
# <a name="regsvr32"></a>regsvr32



Wird die DLL-Dateien als Befehlskomponenten in der Registrierung registriert.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
regsvr32 [/u] [/s] [/n] [/i[:cmdline]] <DllName>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/u|Hebt die Registrierung für Server.|
|/s|Ausführungen **Regsvr32** ohne Nachrichten anzeigen.|
|/n|Ausführungen **Regsvr32** ohne **DllRegisterServer**. (Erfordert die **/i** Parameter.)|
|/i:\<cmdline>|Eine optionale Befehlszeile Zeichenfolge übergeben (*Cmdline*) zu **DllInstall**. Wenn Sie diesen Parameter verwenden, in Verbindung mit der **/u** -Parameter ruft **DllUninstall**.|
|\<DllName>|Der Name der DLL-Datei, die registriert wird.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="BKMK_examples"></a>Beispiele für

Geben Sie Folgendes ein, um die DLL-Datei für die Active Directory-Schema zu registrieren:
```
regsvr32 schmmgmt.dll
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)