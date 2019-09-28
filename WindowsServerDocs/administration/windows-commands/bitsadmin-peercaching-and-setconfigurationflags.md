---
title: bitadmin-Peer Caching und setconfigurationflags
description: 'Windows-Befehls Thema für **BITSAdmin-Peer Caching und setconfigurationflags** : legt die Konfigurationsflags fest, mit denen bestimmt wird, ob der Computer Inhalte für Peers bereitstellen und Inhalt von Peers herunterladen kann.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ff0a2b49-66e3-4d40-824c-6a3816055d2e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a65d54bcaa2bce26eb2b7c98250837ab09c7a423
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381111"
---
# <a name="bitsadmin-peercaching-and-setconfigurationflags"></a>bitadmin-Peer Caching und setconfigurationflags



Legt die Konfigurationsflags fest, die bestimmen, ob der Computer Inhalt für Peers bereitstellen kann und Inhalt von Peers herunterladen kann.

## <a name="syntax"></a>Syntax

```
bitsadmin /PeerCaching /SetConfigurationFlags <Job> <Value>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Der Anzeige Name oder GUID des Auftrags.|
|Wert|Der Wert ist eine ganze Zahl ohne Vorzeichen mit der folgenden Interpretation für die Bits in der binären Darstellung:</br>-Zulassen, dass die Daten des Auftrags von einem Peer heruntergeladen werden: Legen Sie das unwichtigste Bit fest.</br>: Zulassen, dass die Daten des Auftrags an Peers verarbeitet werden: Legen Sie das zweite Bit von rechts fest.|

## <a name="BKMK_examples"></a>Beispiele

Im folgenden Beispiel werden die Daten des Auftrags angegeben, die für den Auftrag *MyJob*von Peers heruntergeladen werden sollen.
```
C:\> Bitsadmin /PeerCaching /SetConfigurationFlags myJob 1
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)