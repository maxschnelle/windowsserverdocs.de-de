---
title: bitsadmin setcredentials
description: Windows-Befehle Thema **Bitsadmin Setcredentials** -Anmeldeinformationen zu einem Auftrag hinzugefügt.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3cd099a4-9e85-46d8-8527-edb6dfab7f97
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 923dcff7d268d40b72db3254e2a97c808c7c7253
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59877391"
---
# <a name="bitsadmin-setcredentials"></a>bitsadmin setcredentials

Fügt Anmeldeinformationen an einen Auftrag an.

**BITS-Version 1.2 und früher**: Nicht unterstützt.

## <a name="syntax"></a>Syntax

```
bitsadmin /SetCredentials <Job> <Target> <Scheme> <Username> <Password>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Anzeigenamen oder die GUID des Auftrags|
|Ziel|SERVER oder PROXY|
|Partitionsschema|Eine der folgenden Möglichkeiten:</br>-GRUNDLEGENDE –-Authentifizierungsschema, in denen der Benutzername und das Kennwort im Klartext an den Server oder Proxy gesendet werden.</br>-DIGEST, ein Abfrage / Rückmeldung-Authentifizierungsschema, das eine serverspezifische Zeichenfolge für die Abfrage verwendet.</br>-NTLM, ein Abfrage / Rückmeldung-Authentifizierungsschema, das die Anmeldeinformationen des Benutzers für die Authentifizierung in einer Windows-Netzwerkumgebung verwendet.</br>– NEGOTIATE – auch bekannt als das einfache und Aushandlung geschützt-Protokoll (Snego) ist ein Abfrage / Rückmeldung-Authentifizierungsschema, die mit dem Server oder Proxy ausgehandelt wird, das zu für die Authentifizierung zu verwendende Schema handelt. Beispiele sind das Kerberos-Protokoll und NTLM.</br>-PASSPORT – ein zentralisierter Authentifizierungsdienst von Microsoft, die einmaliges Anmelden für mitgliederstandorte ermöglicht bereitgestellt werden.|
|Benutzername|Der Name der angegebenen Anmeldeinformationen|
|Kennwort|Das Kennwort mit dem angegebenen *Benutzername*|

## <a name="BKMK_examples"></a>Beispiele für

Das folgenden Beispiel Adds-Anmeldeinformationen für den Auftrag mit dem Namen *MyDownloadJob*.
```
C:\>bitsadmin /RemoveCredentials myDownloadJob SERVER BASIC Edward Password20
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)