---
title: bitsadmin create
description: 'Windows-Befehls Thema für **bizadmin Create** : erstellt einen Übertragungs Auftrag mit dem angegebenen anzeigen Amen.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9a8c53af-900b-4c24-9265-5b8b08213fac
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9f6d641d44c56ea4ff11f48a725367de7dcf472a
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381809"
---
# <a name="bitsadmin-create"></a>bitsadmin create

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Erstellt einen Übertragungs Auftrag mit dem angegebenen anzeigen Amen. Download Aufträge übertragen von Daten von einem Server in eine lokale Datei. Hochladen von Aufträgen übertragen von Daten aus einer lokalen Datei auf einen-Server. Mit Upload-Antwort-Aufträgen werden Daten aus einer lokalen Datei auf einen Server übertragen, und es wird eine Antwortdatei vom Server empfangen.

Verwenden Sie den Schalter [bitadmin Resume](bitsadmin-resume.md) , um den Auftrag in der Übertragungs Warteschlange zu aktivieren.

## <a name="syntax"></a>Syntax

```
bitsadmin /create [type] DisplayName
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|-------|--------|
|Typ|-    **/Download** überträgt Daten von einem Server in eine lokale Datei.<br />-    **"/Upload"** überträgt Daten aus einer lokalen Datei auf einen-Server.<br />-    **/Upload-Reply** überträgt Daten aus einer lokalen Datei auf einen Server und empfängt eine Antwortdatei vom Server.<br />Dieser Parameter ist standardmäßig **/Download** , wenn er nicht in der Befehlszeile angegeben wird.|
|DisplayName|Der dem neu erstellten Auftrag zugewiesene Anzeige Name.|

**Bits 1,2 und früher**: Die Typen "/Upload" und/Upload-Reply sind nicht verfügbar.

## <a name="BKMK_examples"></a>Beispiele

Erstellt einen Download Auftrag mit dem Namen *mydownloadjob*.

```
C:\>bitsadmin /create myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
