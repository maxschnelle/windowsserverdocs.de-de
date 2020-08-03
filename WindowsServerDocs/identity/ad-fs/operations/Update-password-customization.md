---
ms.assetid: 7e804590-6d6c-4cca-ac14-02d4dff06cec
title: Aktualisieren der Kenn Wort Anpassung
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 42131ef5e149c62dd5449d8ada196b1068fd30ac
ms.sourcegitcommit: 3632b72f63fe4e70eea6c2e97f17d54cb49566fd
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/03/2020
ms.locfileid: "87519719"
---
# <a name="update-password-customization"></a>Aktualisieren der Kenn Wort Anpassung

In einigen Fällen können Benutzer möglicherweise keine Verbindung mit dem Unternehmensnetzwerk herstellen, um ihr Kontokennwort zu ändern. Dieser Faktor kann besonders für Remotemitarbeiter, die weit vom nächsten Unternehmensbüro entfernt leben, problematisch sein. Für diese speziellen Fälle kann die Seite zum Aktualisieren des Kennworts verwendet werden, indem nur eine Verbindung mit dem Internet hergestellt wird.

Sie können die Seite zum Aktualisieren des Kennworts anpassen, indem Sie eine eigene Beschreibung für die Seite bereitstellen.

Navigieren Sie zum Aktivieren der Seite zum Aktualisieren des Kennworts zur AD FS-Verwaltungs unter Endpunkte. Der Endpunkt für das Aktualisieren des Kennworts befindet sich im unteren Bereich unter „Andere – /adfs/portal/updatepassword/“. Nachdem Sie den Endpunkt aktiviert haben, müssen Sie den AD FS-Dienst neu starten. Dies muss manuell durchgeführt werden. Wenn Sie davon ausgehen, dass Sie die Webseite zum Aktualisieren von Kenn Wörtern extern verwenden und den webanwendungsproxy verwenden, müssen Sie diese Option auf dem Proxy aktivieren (auf dem Proxy aktivieren). Sie können dann `https://<fqdn>/adfs/portal/updatepassword/` auf einem mit dem Arbeitsplatz verbundenen Gerät zu navigieren, und die Seite "Kennwort aktualisieren" sollte angezeigt werden.

![aktualisieren](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom5.png)

## <a name="customize-the-update-password-page-description"></a>Anpassen der Beschreibung für die Seite zum Aktualisieren des Kennworts

Verwenden Sie zum Anpassen der Beschreibung der Seite zum Aktualisieren des Kennworts das folgende Windows PowerShell-Cmdlet und die folgende Syntax.

```powershell
Set-AdfsGlobalWebContent -UpdatePasswordPageDescriptionText "This is the Contoso Update Password page."
```

## <a name="additional-references"></a>Zusätzliche Verweise

[AD FS Anpassung der Benutzeranmeldung](AD-FS-user-sign-in-customization.md)
