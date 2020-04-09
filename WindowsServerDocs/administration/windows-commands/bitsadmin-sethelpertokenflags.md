---
title: bitadmin-eingabeflags
description: Windows-Befehls Thema für BITSAdmin sethelpertokenflags, mit dem die nutzungsflags für ein Hilfsobjekt festgelegt werden, das einem Bits-Übertragungs Auftrag zugeordnet ist.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: c644e82026cfc1d62f3fb5d20e3925002b871036
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80849493"
---
# <a name="bitsadmin-sethelpertokenflags"></a>bitadmin-eingabeflags

Legt die nutzungsflags für ein [Hilfsobjekt](/windows/desktop/bits/helper-tokens-for-bits-transfer-jobs) fest, das einem Bits-Übertragungs Auftrag zugeordnet ist.

**Bits 3,0 und früher**: nicht unterstützt.

## <a name="syntax"></a>Syntax

```
bitsadmin /SetHelperTokenFlags <Job> <Flags>
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Der Anzeige Name oder GUID des Auftrags.|
|Flags|Folgende Werte sind möglich: 0x0001&mdash;das Hilfsobjekt wird verwendet, um die lokale Datei eines uploadauftrags zu öffnen, um die temporäre Datei eines Download Auftrags zu erstellen oder umzubenennen oder um die Antwortdatei eines Upload-Antwort-Auftrags zu erstellen oder umzubenennen. 0x0002&mdash;das Hilfsobjekt wird zum Öffnen der Remote Datei eines Server Message Block (SMB) Upload-oder Download Auftrags oder als Reaktion auf eine HTTP-Server-oder Proxy Aufforderung für implizite NTLM-oder Kerberos-Anmelde Informationen verwendet. Sie müssen `/SetCredentialsJob TargetScheme NULL NULL` aufgerufen werden, damit die Anmelde Informationen über HTTP gesendet werden können.|

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
