---
ms.assetid: 7e804590-6d6c-4cca-ac14-02d4dff06cec
title: Aktualisieren Sie das Kennwort anpassen
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: e67c04c98a53f4f1db36e6586fa77bcf181a8d5a
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66188976"
---
# <a name="update-password-customization"></a>Aktualisieren Sie das Kennwort anpassen 


In einigen Fällen können Benutzer möglicherweise keine Verbindung mit dem Unternehmensnetzwerk herstellen, um ihr Kontokennwort zu ändern. Dieser Faktor kann besonders für Remotemitarbeiter, die weit vom nächsten Unternehmensbüro entfernt leben, problematisch sein. Für diese speziellen Fälle kann die Seite zum Aktualisieren des Kennworts verwendet werden, indem nur eine Verbindung mit dem Internet hergestellt wird.  
  
Sie können die Seite zum Aktualisieren des Kennworts anpassen, indem Sie eine eigene Beschreibung für die Seite bereitstellen.  
  
> Navigieren Sie zum Aktivieren der Seite zum Aktualisieren des Kennworts zur AD FS-Verwaltungs unter Endpunkte. Der Endpunkt für das Aktualisieren des Kennworts befindet sich im unteren Bereich unter „Andere – /adfs/portal/updatepassword/“. Nachdem Sie den Endpunkt aktiviert haben, müssen Sie den AD FS-Dienst neu starten. Dies muss manuell durchgeführt werden. Sie können dann auf einem mit dem Arbeitsplatz verbundenen Gerät zu https://<fqdn>/adfs/portal/updatepassword/ navigieren, wo die Seite zum Aktualisieren des Kennworts angezeigt werden sollte.  
  
![Update](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom5.png)  
  
## <a name="customize-the-update-password-page-description"></a>Anpassen der Beschreibung für die Seite zum Aktualisieren des Kennworts  
Um die Beschreibung der Update-Kennwort-Seite anzupassen, verwenden Sie die folgenden Windows PowerShell-Cmdlets und Syntax.  
  

    Set-AdfsGlobalWebContent -UpdatePasswordPageDescriptionText "This is the Contoso Update Password page."  

## <a name="additional-references"></a>Weitere Verweise 
[AD FS-Anmeldung Benutzeranpassung](AD-FS-user-sign-in-customization.md)  
