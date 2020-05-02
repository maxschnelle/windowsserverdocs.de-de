---
title: regsvr32
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3345e964-7d3e-42b8-abeb-42ed6edfe2b2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: beadc9e9e614e2fe4cffad5dc263cfb1d4aecf67
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82722478"
---
# <a name="regsvr32"></a>regsvr32



Registriert dll-Dateien als Befehls Komponenten in der Registrierung.



## <a name="syntax"></a>Syntax

```
regsvr32 [/u] [/s] [/n] [/i[:cmdline]] <DllName>
```

### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|/U|Hebt die Registrierung des Servers auf.|
|/s|Führt **regsvr32** aus, ohne Meldungen anzuzeigen.|
|/n|Führt **regsvr32** ohne Aufrufen von **DllRegisterServer**aus. (Erfordert den **/i** -Parameter.)|
|/i:\<cmdline->|Übergibt eine optionale Befehlszeilen Zeichenfolge (*CmdLine*) an **DllInstall**. Wenn Sie diesen Parameter in Verbindung mit dem **/u** -Parameter verwenden, wird **DLLUninstall**aufgerufen.|
|\<Dllname->|Der Name der DLL-Datei, die registriert wird.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um die DLL für das Active Directory Schema zu registrieren:
```
regsvr32 schmmgmt.dll
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)