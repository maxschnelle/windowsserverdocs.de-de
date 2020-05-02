---
title: whoami
description: Referenz Thema für whoami, das Benutzer-, Gruppen-und Berechtigungsinformationen für den Benutzer anzeigt, der zurzeit am lokalen System angemeldet ist.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 6e3f4d5c-f1f5-4429-b602-afad2b3488bf
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2d672b3aaa20125c5c1da10fa3a5811fb5060d11
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725805"
---
# <a name="whoami"></a>whoami



Zeigt Benutzer-, Gruppen-und Berechtigungsinformationen für den Benutzer an, der derzeit am lokalen System angemeldet ist. Bei Verwendung ohne Parameter zeigt **whoami** die aktuelle Domäne und den Benutzernamen an.



## <a name="syntax"></a>Syntax

```
whoami [/upn | /fqdn | /logonid]
whoami {[/user] [/groups] [/priv]} [/fo <Format>] [/nh]
whoami /all [/fo <Format>] [/nh]
```

### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|/upn|Zeigt den Benutzernamen im UPN-Format (User Principal Name) an.|
|/fqdn|Zeigt den Benutzernamen im voll qualifizierten Domänen Namen (FQDN)-Format an.|
|/logonid|Zeigt die Anmelde-ID des aktuellen Benutzers an.|
|/User|Zeigt den aktuellen Domänen-und Benutzernamen sowie die Sicherheits-ID (SID) an.|
|/groups|Zeigt die Benutzergruppen an, zu denen der aktuelle Benutzer gehört.|
|/priv|Zeigt die Sicherheits Privilegien des aktuellen Benutzers an.|
|/FO \<-Format>|Gibt das Ausgabeformat an. Gültige Werte:</br>**Tabelle** Zeigt die Ausgabe in einer Tabelle an. Dies ist der Standardwert.</br>**Liste** Zeigt die Ausgabe in einer Liste an.</br>**CSV** Zeigt die Ausgabe im CSV-Format (Comma-Separated Value) an.|
|/all|Zeigt alle Informationen im aktuellen Zugriffs Token an, einschließlich des aktuellen Benutzernamens, der Sicherheits-IDs (SID), der Berechtigungen und der Gruppen, denen der aktuelle Benutzer angehört.|
|/nh|Gibt an, dass der Spaltenheader nicht in der Ausgabe angezeigt werden soll. Dies gilt nur für Tabellen-und CSV-Formate.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um die Domäne und den Benutzernamen der Person anzuzeigen, die zurzeit an diesem Computer angemeldet ist:
```
whoami
```
Daraufhin wird eine Ausgabe angezeigt, die in etwa wie folgt aussieht:
```
DOMAIN1\administrator
```
Wenn Sie alle Informationen im aktuellen Zugriffs Token anzeigen möchten, geben Sie Folgendes ein:
```
whoami /all
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)