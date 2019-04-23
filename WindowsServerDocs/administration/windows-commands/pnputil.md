---
title: pnputil
description: Erfahren Sie, wie mit dem Hilfsprogramm pnputil.exe Driver Store verwalten.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fab686b8-09d3-4f6c-afa2-630e6036f44c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: 5bde78d97be8def9f8594572869c34ef213db480
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59862541"
---
# <a name="pnputil"></a>pnputil

Pnputil.exe ist ein Befehlszeilenprogramm, mit denen Sie Driver Store verwalten. Pnputil können Sie Treiberpakete hinzufügen, entfernen, Treiberpakete und Treiberpakete auflisten, die sich im Speicher befinden.

## <a name="syntax"></a>Syntax

```
pnputil.exe [-f | -i] [ -? | -a | -d | -e ] <INF name>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|-a|Gibt an, um die identifizierten INF-Datei hinzuzufügen.|
|-d|Gibt an, um die identifizierte INF-Datei zu löschen.|
|-e|Gibt an, um alle Drittanbieter-INF-Dateien aufzulisten.|
|-f|Gibt an, um das Löschen der gefundenen INF-Datei zu erzwingen. Kann nicht verwendet werden, in Verbindung mit der **– i** Parameter.|
|-i|Gibt an, um die identifizierte INF-Datei zu installieren. Kann nicht verwendet werden, in Verbindung mit der **-f** Parameter.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|


## <a name="examples"></a>Beispiele

-   pnputil.exe – ein a:\usbcam\USBCAM. INF fügt die INF-Datei, die durch USBCAM angegeben wird. INF
-   – ein c:\drivers pnputil.exe\*INF fügt alle INF-Dateien in c:\drivers\
-   pnputil.exe – i – ein a:\usbcam\USBCAM. INF hinzugefügt und der angegebenen Treiber installiert.
-   pnputil.exe – e Listet alle Treiber von Drittanbietern.
-   -d oem0.inf pnputil.exe löscht die angegebene.
-   pnputil.exe -f ' -d oem0.inf erzwingt, dass das Löschen der angegebenen INF-Datei.

## <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)

[Popd](popd.md)