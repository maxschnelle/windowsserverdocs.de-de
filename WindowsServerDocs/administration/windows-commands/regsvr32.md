---
title: regsvr32
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 444af0ccf7c9bbe21c013f32b396997b7cb2e00f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71371630"
---
# <a name="regsvr32"></a>regsvr32



Registriert dll-Dateien als Befehls Komponenten in der Registrierung.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
regsvr32 [/u] [/s] [/n] [/i[:cmdline]] <DllName>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/u|Hebt die Registrierung des Servers auf.|
|/s|Führt **regsvr32** aus, ohne Meldungen anzuzeigen.|
|/n|Führt **regsvr32** ohne Aufrufen von **DllRegisterServer**aus. (Erfordert den **/i** -Parameter.)|
|/i: \<cmdline >|Übergibt eine optionale Befehlszeilen Zeichenfolge (*CmdLine*) an **DllInstall**. Wenn Sie diesen Parameter in Verbindung mit dem **/u** -Parameter verwenden, wird **DLLUninstall**aufgerufen.|
|\<dllname >|Der Name der DLL-Datei, die registriert wird.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="BKMK_examples"></a>Beispiele

Geben Sie Folgendes ein, um die DLL für das Active Directory Schema zu registrieren:
```
regsvr32 schmmgmt.dll
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)