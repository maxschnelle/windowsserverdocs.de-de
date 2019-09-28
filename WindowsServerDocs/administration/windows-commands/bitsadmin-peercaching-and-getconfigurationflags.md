---
title: bitadmin-Peer Caching und getconfigurationflags
description: 'Windows-Befehls Thema für **BITSAdmin-Peer Caching und getconfigurationflags** : Ruft die Konfigurationsflags ab, die bestimmen, ob der Computer Inhalt für Peers bereitstellt und Inhalt von Peers herunterladen kann.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 124ddc15-3444-4bd5-96e5-c6bfabe4f9c2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 94c7eb1a115fe9152b149b8cf65765b179080cc3
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381090"
---
# <a name="bitsadmin-peercaching-and-getconfigurationflags"></a>bitadmin-Peer Caching und getconfigurationflags



Ruft die Konfigurationsflags ab, die bestimmen, ob der Computer Inhalt für Peers bereitstellt und Inhalt von Peers herunterladen kann.

## <a name="syntax"></a>Syntax

```
bitsadmin /PeerCaching /GetConfigurationFlags <Job> 
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Der Anzeige Name oder GUID des Auftrags.|

## <a name="BKMK_examples"></a>Beispiele

Im folgenden Beispiel werden die Konfigurationsflags für den Auftrag mit dem Namen " *MyJob*" abgerufen.
```
C:\> Bitsadmin /PeerCaching /GetConfigurationFlags myJob
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)