---
title: bitsadmin create
description: Windows-Befehle Thema **Bitsadmin erstellen** -Übertragungsauftrag erstellt, mit dem angegebenen Anzeigenamen.
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: d6ce5a4fdc21d879bf0a265e3c4185d83311464a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59817191"
---
# <a name="bitsadmin-create"></a>bitsadmin create

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Erstellen einen Übertragungsauftrag, mit dem angegebenen Anzeigenamen. Laden Sie Aufträge übertragen von Daten von einem Server in eine lokale Datei herunter. Laden Sie die Aufträge übertragen von Daten aus einer lokalen Datei auf einem Server hoch. Upload-Antwort-Aufträge übertragen von Daten aus einer lokalen Datei auf einem Server und eine Antwortdatei vom Server empfangen.

Verwenden der [Bitsadmin fortsetzen](bitsadmin-resume.md) wechseln, um den Auftrag in der Übertragungswarteschlange zu aktivieren.

## <a name="syntax"></a>Syntax

```
bitsadmin /create [type] DisplayName
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|-------|--------|
|Typ|-   **/ Herunterladen von** überträgt Daten von einem Server in einer lokalen Datei.<br />-   **/ Hochladen von** überträgt Daten aus einer lokalen Datei auf einem Server.<br />-   **/ Upload-Antwort** überträgt Daten aus einer lokalen Datei auf einem Server und eine Antwortdatei vom Server empfangen.<br />-Dieser Parameter ist standardmäßig **/herunterladen** Wenn in der Befehlszeile nicht angegeben.|
|DisplayName|Der Anzeigename, der neu erstellten Auftrag zugewiesen wird.|

**BITS-Version 1.2 und früher**: Die "/ Upload" und die /Upload-Reply-Typen sind nicht verfügbar.

## <a name="BKMK_examples"></a>Beispiele für

Erstellt einen Downloadauftrag mit dem Namen *MyDownloadJob*.

```
C:\>bitsadmin /create myDownloadJob
```

## <a name="additional-references"></a>Zusätzliche Referenzen

[Befehlszeilensyntax](command-line-syntax-key.md)
