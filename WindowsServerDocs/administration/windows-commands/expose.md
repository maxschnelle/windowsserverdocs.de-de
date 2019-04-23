---
title: verfügbar machen
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9b0a21cf-3bef-4ade-b8f1-ac42f9203947
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 51cc744bc2b61862ed05ca2e7d0aaa8f70d38692
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59886661"
---
# <a name="expose"></a>verfügbar machen



Stellt eine permanente Schattenkopie als Laufwerkbuchstaben, Freigabe oder Bereitstellungspunkt an.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
expose <ShadowID> {<Drive:> | <Share> | <MountPoint>}
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|ShadowID|Gibt die Schattenkopie-ID der Schattenkopie, die Sie verfügbar machen möchten.|
|\<Drive:>|Stellt die angegebenen Schattenkopie als einen bestimmten Laufwerkbuchstaben (z. B. P:) bereit.|
|\<Share>|Macht die angegebene Schattenkopie auf einer Freigabe (z. B. \\ \\ *"MachineName"*\).|
|\<MountPoint>|Macht die angegebene Schattenkopie in einen Bereitstellungspunkt (z. B. C:\shadowcopy\).|

## <a name="remarks"></a>Hinweise

-   Sie können einen vorhandenen Alias oder eine Umgebungsvariable anstelle von *ShadowID*. Verwendung **hinzufügen** ohne Parameter, um die vorhandenen Aliase finden Sie unter.

## <a name="BKMK_examples"></a>Beispiele für

Um die permanente Schattenkopie der VSS_SHADOW_1-Umgebungsvariablen als Laufwerk X zugeordnet verfügbar zu machen, geben Sie Folgendes ein:
```
expose %vss_shadow_1% x:
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)