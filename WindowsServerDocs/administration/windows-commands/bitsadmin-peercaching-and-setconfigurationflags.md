---
title: Bitsadmin Peercaching und setconfigurationflags
description: Windows-Befehle Thema **Bitsadmin Peercaching und Setconfigurationflags** -legt die konfigurationsflags, die bestimmen, wenn der Computer von Inhalten die Peers bereitstellen kann und Herunterladen von Inhalten von Peers kann.
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 22408d4aab7f5ea374511bc16751d911a84644f2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59813331"
---
# <a name="bitsadmin-peercaching-and-setconfigurationflags"></a>Bitsadmin Peercaching und setconfigurationflags



Legt die konfigurationsflags, die bestimmen, wenn der Computer von Inhalten die Peers bereitstellen kann und Herunterladen von Inhalten von Peers kann.

## <a name="syntax"></a>Syntax

```
bitsadmin /PeerCaching /SetConfigurationFlags <Job> <Value>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Anzeigenamen oder die GUID des Auftrags|
|Wert|Der Wert ist eine Ganzzahl ohne Vorzeichen, mit der folgenden Interpretation für die Bits in die binäre Darstellung:</br>: Zulassen des Auftrags Daten von einem Peer heruntergeladen werden: Legen Sie das unwichtigste bit</br>: Zulassen des Auftrags für Peers bereitgestellt werden: Legen Sie die 2. Bit von rechts.|

## <a name="BKMK_examples"></a>Beispiele für

Im folgenden Beispiel wird die Auftrags Daten, die von Peers, die für den Auftrag mit dem Namen heruntergeladen werden *MyJob*.
```
C:\> Bitsadmin /PeerCaching /SetConfigurationFlags myJob 1
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)