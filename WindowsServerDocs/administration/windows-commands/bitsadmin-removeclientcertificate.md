---
title: Bitsadmin removeclientcertificate
description: Windows-Befehle Thema **Bitsadmin Removeclientcertificate** -Zertifikats für den Client aus dem Auftrag entfernt.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b417c3e5-aadd-4fcc-968f-45d8b67ca516
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7b720800fe80037f38ff01ac3a90d5cbb41a6ec8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59868661"
---
# <a name="bitsadmin-removeclientcertificate"></a>Bitsadmin removeclientcertificate



Entfernt das Clientzertifikat aus dem Auftrag an.

## <a name="syntax"></a>Syntax

```
bitsadmin /RemoveClientCertificate <Job> 
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Anzeigenamen oder die GUID des Auftrags|

## <a name="BKMK_examples"></a>Beispiele für

Im folgenden Beispiel wird das Clientzertifikat aus dem Auftrag mit dem Namen *MyJob*.
```
C:\>Bitsadmin /RemoveClientCertificate myJob 
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)