---
title: bitsadmin addfile
description: Windows-Befehle Thema **Bitsadmin Addfile** -Fügt eine Datei zum angegebenen Auftrag.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1b31aa93-0364-465b-af36-754968825989
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1c3027bdc4f3f8f3e3ca50400b2c5dbf33bf2bc5
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59861751"
---
# <a name="bitsadmin-addfile"></a>bitsadmin addfile

Fügt eine Datei zum angegebenen Auftrag.

## <a name="syntax"></a>Syntax

```
bitsadmin /AddFile <Job> <RemoteURL> <LocalName>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Anzeigenamen oder die GUID des Auftrags|
|RemoteURL|Die URL der Datei auf dem Server.|
|LocalName|Der Name der Datei auf dem lokalen Computer. *LocalName* muss einen absoluten Pfad zu der Datei enthalten.|

## <a name="BKMK_examples"></a>Beispiele für

Fügen Sie eine Datei für den Auftrag an. Wiederholen Sie diesen Aufruf für jede Datei, die Sie hinzufügen möchten. Wenn mehrere Aufträge verwenden *MyDownloadJob* als Name, ersetzen Sie *MyDownloadJob* durch die Auftrags GUID zur eindeutigen Identifizierung des Auftrags.
```
C:\>bitsadmin /addfile myDownloadJob http://downloadsrv/10mb.zip c:\10mb.zip
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)