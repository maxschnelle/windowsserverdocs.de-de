---
ms.assetid: 03c82f43-ae2d-4038-b286-ae3858aed35a
title: "Konfigurieren von AD FS Kennwort Ablauf Ansprüche senden"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 386a5ac921ba609c371121b8657351667628951b
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="configure-ad-fs-to-send-password-expiry-claims"></a>Konfigurieren von AD FS Kennwort Ablauf Ansprüche senden

>Gilt für: Windows Server 2016, Windows Server2012 R2

Sie können konfigurieren, dass Active Directory Federation Services (AD FS), um das Kennwort Ablauf Ansprüche, die Vertrauensstellungen vertrauenden Seite (Anwendungen) zu senden, die durch AD FS geschützt sind. Wie diese Ansprüche verwendet werden, hängt von der Anwendung. Mit Office365 als der vertrauenden haben z.B. Updates in Exchange und Outlook verbundene Benutzer ihre Kennwörter bald-zu--abgelaufen sein benachrichtigen implementiert wurde.

Zum Konfigurieren von AD FS Kennwort Ablauf Ansprüche eine Vertrauensstellung für vertrauende Seiten, müssen Sie die folgenden Anspruchsregeln diese Vertrauensstellung der vertrauenden Seite hinzufügen:

```
c1:[Type == "https://schemas.microsoft.com/ws/2012/01/passwordexpirationtime"]
=> issue(store = "_PasswordExpiryStore", types = ("https://schemas.microsoft.com/ws/2012/01/passwordexpirationtime", "https://schemas.microsoft.com/ws/2012/01/passwordexpirationdays", "https://schemas.microsoft.com/ws/2012/01/passwordchangeurl"), query = "{0};", param = c1.Value);
```

> [!NOTE]
> Kennwort Ablauf Ansprüche sind nur verfügbar für Benutzernamen und das Kennwort und Microsoft Passport für Arbeit Authentifizierungstypen.  Wenn der Benutzer authentifiziert mit integrierten Windows-Authentifizierung und Passport ist nicht konfiguriert, die Ansprüche nicht zur Verfügung, und die Benutzer sehen keine Kennwort Ablauf Benachrichtigungen.

> [!NOTE]
> Es ist ein Fenster 14Tage die gesendete Ansprüche nur aufgefüllt werden, wenn das Kennwort innerhalb von 14Tagen abläuft.

## <a name="see-also"></a>Siehe auch
[AD FS-Vorgänge](../../ad-fs/AD-FS-2016-Operations.md)
