---
title: Verwalten von-Bde-KeyPackage
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c631ef10-2a2f-4541-8578-292f2d4e9e80
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8fb49ce8fbe4be076151b203560e62f44a78c9d4
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59886901"
---
# <a name="manage-bde-keypackage"></a>Verwalten von-Bde: KeyPackage



Generiert ein Schlüsselpaket für ein Laufwerk an. Das Schlüsselpaket kann in Verbindung mit dem Reparaturtool verwendet werden, um beschädigte Laufwerke zu reparieren. Beispiele wie dieser Befehl verwendet werden kann, finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
manage-bde -KeyPackage [<Drive>] [-ID <KeyProtectoryID>] [-path <PathToExternalKeyDirectory>] [-computername <Name>] [{-?|/?}] [{-help|-h}]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<Drive>|Stellt einen von einem Doppelpunkt gefolgten Laufwerkbuchstaben dar.|
|-ID|Erstellen Sie ein Schlüsselpaket mithilfe der Schlüsselschutzvorrichtung mit dem Bezeichner, die von dieser ID-Wert angegeben.|
|-path|Speicherort aus, um das Schlüsselpaket erstellt zu speichern.|
|-computername|Gibt an, dass bde.exe verwendet wird, um die BitLocker-Schutz auf einem anderen Computer zu ändern. Sie können auch **- Cn** als eine verkürzte Version des mit diesem Befehl.|
|\<Name>|Stellt den Namen des Computers, auf dem BitLocker-Schutz zu ändern. Akzeptierte Werte sind die NetBIOS-Namen des Computers und die IP-Adresse des Computers.|
|-? oder /?|Zeigt eine kurze Hilfe an der Eingabeaufforderung.|
|---Help oder-h|Führen Sie zeigt Hilfe an der Eingabeaufforderung ein.|

## <a name="BKMK_Examples"></a>Beispiele für

Das folgende Beispiel veranschaulicht die Verwendung der **- KeyPackage** Befehl erstellen Sie ein Schlüsselpaket für Laufwerk C: basierend auf der Schlüsselschutzvorrichtung GUID angegeben wird und das Schlüsselpaket in F:\Folder zu speichern.
```
manage-bde -KeyPackage C: -id {84E151C1...7A62067A512} -path "f:\Folder"
```

> [!TIP]
> Verwenden Sie **verwalten-Bde – Schutzvorrichtungen – erste** zusammen mit den Laufwerkbuchstaben, der ein Schlüssel-Paket zu erstellen, um eine Liste der verfügbaren GUIDs für die Verwendung als ID-Wert zu erhalten soll.

#### <a name="additional-references"></a>Weitere Verweise

-   [Befehlszeilensyntax](command-line-syntax-key.md)
-   [Verwalten von-bde](manage-bde.md)