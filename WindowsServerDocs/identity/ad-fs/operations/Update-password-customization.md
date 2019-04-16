---
ms.assetid: 7e804590-6d6c-4cca-ac14-02d4dff06cec
title: Anpassen von Update-Kennwort
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 4b06992bfb398b66988ad4882217a8a83738365e
ms.sourcegitcommit: 78d8839ccafa9530784cb9e38c3127ed2c215423
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/09/2018
---
# <a name="update-password-customization"></a>Anpassen von Update-Kennwort 

>Gilt für: Windows Server 2016, Windows Server2012 R2

In einigen Fällen Benutzer eine Verbindung mit dem Unternehmensnetzwerk so ändern Sie das Kennwort für ihr möglicherweise nicht. Dieser Faktor kann besonders für Remotemitarbeiter, die weit vom nächsten live möglicherweise problematisch sein, Büro. Für diese speziellen Fälle kann die Seite zum Aktualisieren von Kennwort verwendet werden, indem nur eine Verbindung mit dem Internet herstellen.  
  
Sie können die Update-Seite "Kennwort" anpassen, indem Sie eine eigene Beschreibung für die Seite bereitstellen.  
  
> Um die Seite zum Aktualisieren von Kennwort zu aktivieren, wechseln Sie zu AD FS-Verwaltungs unter Endpunkte. Der Endpunkt für das Aktualisieren des Kennworts befindet sich im unteren Bereich unter andere – / Adfs/Portal/Updatepassword/zur Verfügung. Nachdem Sie den Endpunkt aktiviert haben, müssen Sie die AD FS-Dienst neu starten. Dies muss manuell erfolgen. Navigieren Sie dann zum https://<fqdn>/Adfs/Portal/Updatepassword/auf einem Arbeitsplatz verbundenen Gerät und die Seite zum Aktualisieren von Kennwort sollte angezeigt werden.  
  
![Aktualisieren](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom5.png)  
  
## <a name="customize-the-update-password-page-description"></a>Anpassen der Beschreibung für die Seite Aktualisieren des Kennworts  
Um die Beschreibung der Update-Kennwort-Seite anzupassen, verwenden Sie die folgenden Windows PowerShell-Cmdlet und die folgende Syntax.  
  

    Set-AdfsGlobalWebContent -UpdatePasswordPageDescriptionText "This is the Contoso Update Password page."  

## <a name="additional-references"></a>Weitere Verweise 
[AD FS-Anmeldung Anpassung durch den Benutzer](AD-FS-user-sign-in-customization.md)  
