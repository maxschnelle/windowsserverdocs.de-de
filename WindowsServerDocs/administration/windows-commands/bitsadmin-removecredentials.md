---
title: bitsadmin removecredentials
description: Windows-Befehle Thema **Bitsadmin Removecredentials** -Anmeldeinformationen aus einem Auftrag entfernt.
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: cbd65442ff0d74ec1179a49df5d4a94785f3dd25
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59822291"
---
# <a name="bitsadmin-removecredentials"></a>bitsadmin removecredentials

Entfernt Anmeldeinformationen eines Auftrags an.

**BITS-Version 1.2 und früher**: Nicht unterstützt.

## <a name="syntax"></a>Syntax

```
bitsadmin /RemoveCredentials <Job> <Target> <Scheme>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Anzeigenamen oder die GUID des Auftrags|
|Ziel|SERVER oder PROXY|
|Partitionsschema|Eine der folgenden Möglichkeiten:</br>-GRUNDLEGENDE –-Authentifizierungsschema, in denen der Benutzername und das Kennwort im Klartext an den Server oder Proxy gesendet werden.</br>-DIGEST, ein Abfrage / Rückmeldung-Authentifizierungsschema, das eine serverspezifische Zeichenfolge für die Abfrage verwendet.</br>-NTLM, ein Abfrage / Rückmeldung-Authentifizierungsschema, das die Anmeldeinformationen des Benutzers für die Authentifizierung in einer Windows-Netzwerkumgebung verwendet.</br>– NEGOTIATE – auch bekannt als das einfache und Aushandlung geschützt-Protokoll (Snego) ist ein Abfrage / Rückmeldung-Authentifizierungsschema, die mit dem Server oder Proxy ausgehandelt wird, das zu für die Authentifizierung zu verwendende Schema handelt. Beispiele sind das Kerberos-Protokoll und NTLM.</br>-PASSPORT – ein zentralisierter Authentifizierungsdienst von Microsoft, die einmaliges Anmelden für mitgliederstandorte ermöglicht bereitgestellt werden.|

## <a name="BKMK_examples"></a>Beispiele für

Im folgenden Beispiel wird die Anmeldeinformationen aus dem Auftrag mit dem Namen *MyDownloadJob*.
```
C:\>bitsadmin /RemoveCredentials myDownloadJob SERVER BASIC
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)