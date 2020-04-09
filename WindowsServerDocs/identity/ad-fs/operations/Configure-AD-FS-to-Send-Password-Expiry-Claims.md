---
ms.assetid: 03c82f43-ae2d-4038-b286-ae3858aed35a
title: Konfigurieren von AD FS zum Senden von Ansprüchen beim Kennwortablauf
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: a0c04f42cbe29b1ea36d09f1f148fb28280d7fec
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80859893"
---
# <a name="configure-ad-fs-to-send-password-expiry-claims"></a>Konfigurieren von AD FS zum Senden von Ansprüchen beim Kennwortablauf


Sie können Active Directory-Verbunddienste (AD FS) (AD FS) konfigurieren, um Kenn Wort Ablauf Ansprüche an die Vertrauens Stellungen der vertrauenden Seite (Anwendungen) zu senden, die durch AD FS geschützt werden. Wie diese Ansprüche verwendet werden, hängt von der jeweiligen Anwendung ab. Beispiel: Bei Office 365 als vertrauende Seite werden Updates in Exchange und Outlook implementiert, damit Verbundbenutzer über ihre bald ablaufenden Kennwörter benachrichtigt werden.

Um AD FS zum Senden von Kenn Wort Ablauf Ansprüchen an eine Vertrauensstellung der vertrauenden Seite zu konfigurieren, müssen Sie der Vertrauensstellung der vertrauenden Seite die folgenden Anspruchs Regeln hinzufügen:

```
@RuleName = "Issue Password Expiry Claims"
c1:[Type == "https://schemas.microsoft.com/ws/2012/01/passwordexpirationtime"]
 => issue(store = "_PasswordExpiryStore", types = ("https://schemas.microsoft.com/ws/2012/01/passwordexpirationtime", "https://schemas.microsoft.com/ws/2012/01/passwordexpirationdays", "https://schemas.microsoft.com/ws/2012/01/passwordchangeurl"), query = "{0};", param = c1.Value);
```

> [!NOTE]
> Ansprüche zum Ablauf von Kenn Wörtern sind nur für Benutzername-und Kennwort-und Microsoft Passport for Work Authentifizierungs Typen verfügbar.  Wenn sich der Benutzer mit der integrierten Windows-Authentifizierung authentifiziert und Passport nicht konfiguriert ist, sind die Ansprüche nicht verfügbar, und den Benutzern werden keine Benachrichtigungen zum Ablauf des Kennworts angezeigt.

> [!NOTE]
> Es gibt ein Fenster von 14 Tagen, sodass die gesendeten Ansprüche nur aufgefüllt werden, wenn das Kennwort innerhalb von 14 Tagen abläuft.

## <a name="see-also"></a>Weitere Informationen
[AD FS-Vorgänge](../../ad-fs/AD-FS-2016-Operations.md)
