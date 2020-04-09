---
title: regsvr32
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3345e964-7d3e-42b8-abeb-42ed6edfe2b2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d3b775b0c49e4191a9fee6dc9e2e91f968142085
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80836213"
---
# <a name="regsvr32"></a>regsvr32



Registriert dll-Dateien als Befehls Komponenten in der Registrierung.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
regsvr32 [/u] [/s] [/n] [/i[:cmdline]] <DllName>
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/u|Hebt die Registrierung des Servers auf.|
|/s|Führt **regsvr32** aus, ohne Meldungen anzuzeigen.|
|/n|Führt **regsvr32** ohne Aufrufen von **DllRegisterServer**aus. (Erfordert den **/i** -Parameter.)|
|/i:\<-cmdline->|Übergibt eine optionale Befehlszeilen Zeichenfolge (*CmdLine*) an **DllInstall**. Wenn Sie diesen Parameter in Verbindung mit dem **/u** -Parameter verwenden, wird **DLLUninstall**aufgerufen.|
|\<dllName >|Der Name der DLL-Datei, die registriert wird.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Geben Sie Folgendes ein, um die DLL für das Active Directory Schema zu registrieren:
```
regsvr32 schmmgmt.dll
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)