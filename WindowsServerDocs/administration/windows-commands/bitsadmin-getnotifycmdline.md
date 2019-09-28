---
title: bitsadmin getnotifycmdline
description: 'Thema Windows-Befehle für **bizadmin getnotifycmdline** : Ruft den Befehlszeilen Befehl ab, der ausgeführt wird, wenn der Auftrag das Übertragen von Daten abgeschlossen hat.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 90fa33e6-aca5-4a23-82bd-19a9f13f8416
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b91d2c71ad4bedaac65e23041ca78a70ade99977
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381488"
---
# <a name="bitsadmin-getnotifycmdline"></a>bitsadmin getnotifycmdline

Ruft den Befehlszeilen Befehl ab, der ausgeführt werden soll, wenn der Auftrag das Übertragen von Daten abgeschlossen hat.

**Bits 1,2 und früher**: Nicht unterstützt.

## <a name="syntax"></a>Syntax

```
bitsadmin /GetNotifyCmdLine <Job>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Der Anzeige Name oder GUID des Auftrags.|

## <a name="BKMK_examples"></a>Beispiele

Im folgenden Beispiel wird der Befehlszeilen Befehl abgerufen, der vom-Dienst verwendet wird, wenn der Auftrag mit dem Namen *mydownloadjob* abgeschlossen ist.
```
C:\>bitsadmin /GetNotifyCmdLine myDownloadJob
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)