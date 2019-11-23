---
title: bitadmin-eingabeflags
description: 'Windows-Befehls Thema für **BITSAdmin sethelpertokenflags** : legt die nutzungsflags für ein Hilfsobjekt fest, das einem Bits-Übertragungs Auftrag zugeordnet ist.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: 6047c63677fac3311634ababb675be5301b7f3b5
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380584"
---
# <a name="bitsadmin-sethelpertokenflags"></a>bitadmin-eingabeflags

Legt die nutzungsflags für ein [Hilfsobjekt](/windows/desktop/bits/helper-tokens-for-bits-transfer-jobs) fest, das einem Bits-Übertragungs Auftrag zugeordnet ist.

**Bits 3,0 und früher**: nicht unterstützt.

## <a name="syntax"></a>Syntax

```
bitsadmin /SetHelperTokenFlags <Job> <Flags>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Der Anzeige Name oder GUID des Auftrags.|
|Flags|Folgende Werte sind möglich: 0x0001&mdash;das Hilfsobjekt wird verwendet, um die lokale Datei eines uploadauftrags zu öffnen, um die temporäre Datei eines Download Auftrags zu erstellen oder umzubenennen oder um die Antwortdatei eines Upload-Antwort-Auftrags zu erstellen oder umzubenennen. 0x0002&mdash;das Hilfsobjekt wird zum Öffnen der Remote Datei eines Server Message Block (SMB) Upload-oder Download Auftrags oder als Reaktion auf eine HTTP-Server-oder Proxy Aufforderung für implizite NTLM-oder Kerberos-Anmelde Informationen verwendet. Sie müssen `/SetCredentialsJob TargetScheme NULL NULL` aufgerufen werden, damit die Anmelde Informationen über HTTP gesendet werden können.|

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
