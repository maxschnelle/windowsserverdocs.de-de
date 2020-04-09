---
title: bitsadmin setcredentials
description: Windows-Befehls Thema für bigsadmin setanmelde Informationen, mit dem einem Auftrag Anmelde Informationen hinzugefügt werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3cd099a4-9e85-46d8-8527-edb6dfab7f97
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 918bda93407e029cedaaf5eab937d1bb23dc3c4c
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80849643"
---
# <a name="bitsadmin-setcredentials"></a>bitsadmin setcredentials

Fügt einem Auftrag Anmelde Informationen hinzu.

**Bits 1,2 und früher**: nicht unterstützt.

## <a name="syntax"></a>Syntax

```
bitsadmin /SetCredentials <Job> <Target> <Scheme> <Username> <Password>
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Der Anzeige Name oder GUID des Auftrags.|
|Ziel|Server oder Proxy|
|Schema|Eine der folgenden Komponenten:</br>-Basic – das Authentifizierungsschema, in dem der Benutzername und das Kennwort in Klartext an den Server oder Proxy gesendet werden.</br>-Digest – ein Challenge-Response-Authentifizierungsschema, das eine vom Server angegebene Daten Zeichenfolge für die Abfrage verwendet.</br>-NTLM – ein Challenge-Response-Authentifizierungsschema, bei dem die Anmelde Informationen des Benutzers zur Authentifizierung in einer Windows-Netzwerkumgebung verwendet werden.</br>-Aushandlungen – auch als Simple and Protected Aushandlungs Protokoll (snego) bezeichnet, ist ein Challenge-Response-Authentifizierungsschema, das mit dem Server oder Proxy aushandelt, um zu bestimmen, welches Schema für die Authentifizierung verwendet werden soll. Beispiele sind das Kerberos-Protokoll und NTLM.</br>-Passport – ein von Microsoft bereitgestellter zentralisierter Authentifizierungsdienst, der eine einzelne Anmeldung für Mitglieder Standorte bietet.|
|Benutzername|Der Name der angegebenen Anmelde Informationen.|
|Kennwort|Das Kennwort, das dem angegebenen *Benutzernamen* zugeordnet ist.|

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Im folgenden Beispiel werden dem Auftrag mit dem Namen *mydownloadjob*Anmelde Informationen hinzugefügt.
```
C:\>bitsadmin /RemoveCredentials myDownloadJob SERVER BASIC Edward Password20
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)