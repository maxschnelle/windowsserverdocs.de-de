---
ms.assetid: 03c82f43-ae2d-4038-b286-ae3858aed35a
title: Konfigurieren von AD FS zum Senden von Ansprüchen beim Kennwortablauf
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 3be14b824038e9424b86c40bfd657dd988fa99e9
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66189870"
---
# <a name="configure-ad-fs-to-send-password-expiry-claims"></a>Konfigurieren von AD FS zum Senden von Ansprüchen beim Kennwortablauf


Sie können konfigurieren, dass Active Directory Federation Services (AD FS) zum Senden von Kennwort Ablauf Ansprüche an die Partei Vertrauensstellungen der vertrauenden Seite (Anwendungen), die durch AD FS geschützt sind. Wie diese Ansprüche verwendet werden, hängt von der Anwendung ab. Beispielsweise wurden mit Office 365 als vertrauende Seite Ihrer Updates auf Exchange Online und Outlook verbundene Benutzer über ihre Kennwörter bald-zu--abgelaufen informiert implementiert.

Zum Konfigurieren von AD FS zum Senden von Kennwort Ablauf Ansprüche, um eine Vertrauensstellung der vertrauenden Seite müssen Sie die folgenden Anspruchsregeln auf diese Vertrauensstellung der vertrauenden Seite hinzufügen:

```
@RuleName = "Issue Password Expiry Claims"
c1:[Type == "http://schemas.microsoft.com/ws/2012/01/passwordexpirationtime"]
 => issue(store = "_PasswordExpiryStore", types = ("http://schemas.microsoft.com/ws/2012/01/passwordexpirationtime", "http://schemas.microsoft.com/ws/2012/01/passwordexpirationdays", "http://schemas.microsoft.com/ws/2012/01/passwordchangeurl"), query = "{0};", param = c1.Value);
```

> [!NOTE]
> Kennwort Ablauf Ansprüche sind nur verfügbar für Benutzernamen und das Kennwort und Microsoft Passport für die Arbeit Authentifizierungstypen.  Wenn der Benutzer authentifiziert sich mithilfe der integrierten Windows-Authentifizierung und Passport ist nicht konfiguriert, die Ansprüche nicht zur Verfügung, und die Benutzer sehen keine Benachrichtigungen zum Kennwortablauf.

> [!NOTE]
> Es ist ein 14 Tage d. h. die gesendeten Ansprüche nur aufgefüllt, werden, wenn das Kennwort innerhalb von 14 Tagen abläuft.

## <a name="see-also"></a>Siehe auch
[AD FS-Vorgänge](../../ad-fs/AD-FS-2016-Operations.md)
