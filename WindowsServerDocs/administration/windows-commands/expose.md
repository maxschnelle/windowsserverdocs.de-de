---
title: sichtbar
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 819484364e8375c4d58e4d022681eedeaa7084ab
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71377276"
---
# <a name="expose"></a>sichtbar



macht eine persistente Schatten Kopie als Laufwerk Buchstaben, Freigabe oder Einfügepunkt verfügbar.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
expose <ShadowID> {<Drive:> | <Share> | <MountPoint>}
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Shadowid|Gibt die Schatten-ID der Schatten Kopie an, die Sie verfügbar machen möchten.|
|\<laufwerk: >|Macht die angegebene Schatten Kopie als Laufwerk Buchstaben (z. b. P:) verfügbar.|
|\<freigabe >|Macht die angegebene Schatten Kopie in einer Freigabe verfügbar (z. b. \\ @ no__t-1*MachineName*\).|
|\<mountpoint >|Macht die angegebene Schatten Kopie für einen Einstellungspunkt verfügbar (z. b. c:\shadowcopy @ no__t-0.|

## <a name="remarks"></a>Hinweise

-   Anstelle von *shadowid*können Sie einen vorhandenen Alias oder eine Umgebungsvariable verwenden. Verwenden **Sie hinzufügen** ohne Parameter, um vorhandene Aliase anzuzeigen.

## <a name="BKMK_examples"></a>Beispiele

Geben Sie Folgendes ein, um die der VSS_SHADOW_1-Umgebungsvariablen zugeordnete persistente Schatten Kopie als Laufwerk X verfügbar zu machen:
```
expose %vss_shadow_1% x:
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)