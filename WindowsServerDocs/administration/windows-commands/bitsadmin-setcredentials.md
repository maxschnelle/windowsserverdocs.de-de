---
title: bitsadmin setcredentials
description: Referenz Artikel für den Befehl "bizadmin setanmelde Informationen", mit dem einem Auftrag Anmelde Informationen hinzugefügt werden.
ms.topic: reference
ms.assetid: 3cd099a4-9e85-46d8-8527-edb6dfab7f97
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: f3045bc584e420da215b02111a61c3e7b8a50e8a
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89631010"
---
# <a name="bitsadmin-setcredentials"></a>bitsadmin setcredentials

Fügt einem Auftrag Anmelde Informationen hinzu.

> [!NOTE]
> Dieser Befehl wird von Bits 1,2 und früheren Versionen nicht unterstützt.

## <a name="syntax"></a>Syntax

```
bitsadmin /setcredentials <job> <target> <scheme> <username> <password>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |
| target | Verwenden Sie entweder den **Server** oder den **Proxy**. |
| scheme | Verwenden Sie einen der folgenden Werte:<ul><li>**Basic.** Das Authentifizierungsschema, in dem der Benutzername und das Kennwort in Klartext an den Server oder Proxy gesendet werden.</li><li>**Lich.** Ein Challenge-Response-Authentifizierungsschema, das eine vom Server angegebene Daten Zeichenfolge für die Abfrage verwendet.</li><li>**NTLM.** Ein Challenge-Response-Authentifizierungsschema, bei dem die Anmelde Informationen des Benutzers zur Authentifizierung in einer Windows-Netzwerkumgebung verwendet werden.</li><li>**Aushandeln (auch als einfaches und geschütztes Aushandlungs Protokoll bezeichnet).** Ein Challenge-Response-Authentifizierungsschema, das mit dem Server oder Proxy aushandiert, um zu bestimmen, welches Schema für die Authentifizierung verwendet werden soll. Beispiele sind das Kerberos-Protokoll und NTLM.</li><li>**BU.** Ein von Microsoft bereitgestellter zentralisierter Authentifizierungsdienst, der eine einzelne Anmeldung für Mitglieder Standorte bietet.</li></ul> |
| user_name | Der Name des Benutzers. |
| password | Das Kennwort, das dem angegebenen *Benutzernamen*zugeordnet ist. |

## <a name="examples"></a>Beispiele

So fügen Sie dem Auftrag mit dem Namen *mydownloadjob*Anmelde Informationen hinzu:

```
bitsadmin /setcredentials myDownloadJob SERVER BASIC Edward password20
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
