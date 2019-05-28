---
title: tpmtool
description: Windows-Befehle Thema Tpmtool - Ruft Informationen über das Trusted Platform Module ab.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
author: ashleytqy
ms.author: ashleytqy
manager: ronaldai
ms.date: 05/07/2019
ms.openlocfilehash: d2939b693c3f9bd8d0d8c8e1fefdd5d8f892e4c9
ms.sourcegitcommit: 3582c38d87f23cc54467d63bf00c29ef07cdb7c8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/10/2019
ms.locfileid: "65517193"
---
>[!IMPORTANT]
>Einige Informationen beziehen sich auf die Vorabversion, an der bis zur kommerziellen Veröffentlichung unter Umständen noch grundsätzliche Änderungen vorgenommen werden. Microsoft übernimmt keine Garantie, weder ausdrücklich noch stillschweigend, für die hier bereitgestellten Informationen.

# <a name="tpmtool"></a>tpmtool

Dieses Hilfsprogramm kann verwendet werden, um Informationen zu erhalten, über die [Trusted Platform Module (TPM)](https://docs.microsoft.com/windows/security/information-protection/tpm/trusted-platform-module-overview).

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#tpmtool_examples).

## <a name="syntax"></a>Syntax

```
tpmtool /parameter [<arguments>]
```
## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|getdeviceinformation|Zeigt die grundlegende Informationen des TPM.|
|GatherLogs [Pfad des Ausgabeverzeichnisses]|TPM-Protokolle erfasst und in das angegebene Verzeichnis. Standardmäßig werden sie in das aktuelle Verzeichnis platziert.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="tpmtool_examples"></a>Beispiele für

Um die grundlegenden Informationen für das TPM anzuzeigen, geben Sie Folgendes ein:
```
tpmtool getdeviceinformation
```
Werden Sie zum TPM-Protokolle erfasst, und platzieren Sie diese im aktuellen Verzeichnis, Typ:
```
tpmtool gatherlogs
```
Werden Sie zum TPM-Protokolle erfasst und diese in `C:\Users\Public`, Typ:
```
tpmtool gatherlogs C:\Users\Public
```
