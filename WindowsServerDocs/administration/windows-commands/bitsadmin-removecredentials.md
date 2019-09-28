---
title: bitsadmin removecredentials
description: Windows-Befehls Thema für **bitionadmin removecredenseins** -entfernt Anmelde Informationen aus einem Auftrag.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4a78ce9a-1feb-4811-a000-cce81287b22b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 34a5bae9304a9db9f47f437276270ca06b1ebeee
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380822"
---
# <a name="bitsadmin-removecredentials"></a>bitsadmin removecredentials

Entfernt Anmelde Informationen aus einem Auftrag.

**Bits 1,2 und früher**: Nicht unterstützt.

## <a name="syntax"></a>Syntax

```
bitsadmin /RemoveCredentials <Job> <Target> <Scheme>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Der Anzeige Name oder GUID des Auftrags.|
|Ziel|Server oder Proxy|
|Schrift|Eine der folgenden Möglichkeiten:</br>-Basic – das Authentifizierungsschema, in dem der Benutzername und das Kennwort in Klartext an den Server oder Proxy gesendet werden.</br>-Digest – ein Challenge-Response-Authentifizierungsschema, das eine vom Server angegebene Daten Zeichenfolge für die Abfrage verwendet.</br>-NTLM – ein Challenge-Response-Authentifizierungsschema, bei dem die Anmelde Informationen des Benutzers zur Authentifizierung in einer Windows-Netzwerkumgebung verwendet werden.</br>-Aushandlungen – auch als Simple and Protected Aushandlungs Protokoll (snego) bezeichnet, ist ein Challenge-Response-Authentifizierungsschema, das mit dem Server oder Proxy aushandelt, um zu bestimmen, welches Schema für die Authentifizierung verwendet werden soll. Beispiele sind das Kerberos-Protokoll und NTLM.</br>-Passport – ein von Microsoft bereitgestellter zentralisierter Authentifizierungsdienst, der eine einzelne Anmeldung für Mitglieder Standorte bietet.|

## <a name="BKMK_examples"></a>Beispiele

Im folgenden Beispiel werden die Anmelde Informationen aus dem Auftrag mit dem Namen *mydownloadjob*entfernt.
```
C:\>bitsadmin /RemoveCredentials myDownloadJob SERVER BASIC
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)