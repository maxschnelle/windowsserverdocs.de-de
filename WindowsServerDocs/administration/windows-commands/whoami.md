---
title: whoami
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6e3f4d5c-f1f5-4429-b602-afad2b3488bf
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6844ba001c2ebd7407b77f97204069a48a1b595b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59840151"
---
# <a name="whoami"></a>whoami



Zeigt Informationen von Benutzern, Gruppen und Berechtigungen für den Benutzer, die auf das lokale System angemeldet ist. Wenn Sie ohne Angabe von Parametern **Whoami** zeigt den aktuellen Domänen- und Benutzernamen an.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
whoami [/upn | /fqdn | /logonid]
whoami {[/user] [/groups] [/priv]} [/fo <Format>] [/nh]
whoami /all [/fo <Format>] [/nh]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/upn|Zeigt den Benutzernamen im Format User principal Name (UPN).|
|/fqdn|Zeigt den Benutzernamen im Format des vollständig qualifizierten Domänennamen (FQDN).|
|/logonid|Zeigt die Anmelde-ID des aktuellen Benutzers.|
|/ User|Zeigt den Namen des aktuellen Domänen- und Benutzernamen und die Sicherheits-ID (SID).|
|/groups|Zeigt die Benutzergruppen aus, zu denen der aktuelle Benutzer gehört.|
|/priv|Zeigt die Sicherheitsprivilegien des aktuellen Benutzers.|
|/ Fo \<Format >|Gibt das Ausgabeformat. Gültige Werte sind:</br>**Tabelle** wird die Ausgabe in Tabellenform angezeigt. Dies ist der Standardwert.</br>**Liste** wird die Ausgabe in einer Liste angezeigt.</br>**CSV** wird die Ausgabe im Format mit kommagetrennten Werten (CSV) angezeigt.|
|/ all|Zeigt alle Informationen in der aktuellen Zugriffstoken, einschließlich der aktuellen Benutzernamen, Sicherheits-IDs (SID), Berechtigungen und Gruppen, denen der aktuelle Benutzer angehört.|
|/nh|Gibt an, dass die Kopfzeile der Spalte nicht in der Ausgabe angezeigt werden soll. Dies gilt nur für Tabelle und im CSV-Format.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="BKMK_examples"></a>Beispiele für

Um die Domäne und den Namen der Person anzuzeigen, der zurzeit auf diesem Computer angemeldet ist, geben Sie Folgendes ein:
```
whoami
```
Es wird eine Ausgabe ähnlich der folgenden angezeigt:
```
DOMAIN1\administrator
```
Um alle Informationen, die in der aktuellen Zugriffstoken anzuzeigen, geben Sie Folgendes ein:
```
whoami /all
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)