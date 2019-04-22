---
title: Bitsadmin Peercaching und getconfigurationflags
description: Windows-Befehle Thema **Bitsadmin Peercaching und Getconfigurationflags** – Ruft die konfigurationsflags ab, die bestimmen, wenn der Computer-Inhalte an Peers bereitstellt und Herunterladen von Inhalten von Peers können.
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 6afa39993cf90b2d71b6b681680c3b4e1fd9b56b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59826351"
---
# <a name="bitsadmin-peercaching-and-getconfigurationflags"></a>Bitsadmin Peercaching und getconfigurationflags



Ruft die konfigurationsflags, die bestimmen, wenn der Computer Inhalt an Peers stellt und Herunterladen von Inhalten von Peers kann.

## <a name="syntax"></a>Syntax

```
bitsadmin /PeerCaching /GetConfigurationFlags <Job> 
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Anzeigenamen oder die GUID des Auftrags|

## <a name="BKMK_examples"></a>Beispiele für

Im folgenden Beispiel wird die konfigurationsflags für den Auftrag mit dem Namen *MyJob*.
```
C:\> Bitsadmin /PeerCaching /GetConfigurationFlags myJob
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)