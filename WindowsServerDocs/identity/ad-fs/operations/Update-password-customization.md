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
ms.openlocfilehash: cb5fd0ff432e441900e379d3fe798dbe6aef855f
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80816103"
---
# <a name="update-password-customization"></a>Aktualisieren der Kenn Wort Anpassung 


In einigen Fällen können Benutzer möglicherweise keine Verbindung mit dem Unternehmensnetzwerk herstellen, um ihr Kontokennwort zu ändern. Dieser Faktor kann besonders für Remotemitarbeiter, die weit vom nächsten Unternehmensbüro entfernt leben, problematisch sein. Für diese speziellen Fälle kann die Seite zum Aktualisieren des Kennworts verwendet werden, indem nur eine Verbindung mit dem Internet hergestellt wird.  
  
Sie können die Seite zum Aktualisieren des Kennworts anpassen, indem Sie eine eigene Beschreibung für die Seite bereitstellen.  
  
> Navigieren Sie zum Aktivieren der Seite zum Aktualisieren des Kennworts zur AD FS-Verwaltungs unter Endpunkte. Der Endpunkt für das Aktualisieren des Kennworts befindet sich im unteren Bereich unter „Andere – /adfs/portal/updatepassword/“. Nachdem Sie den Endpunkt aktiviert haben, müssen Sie den AD FS-Dienst neu starten. Dies muss manuell durchgeführt werden. Sie können dann auf einem mit dem Arbeitsplatz verbundenen Gerät zu https://<fqdn>/adfs/portal/updatepassword/ navigieren, wo die Seite zum Aktualisieren des Kennworts angezeigt werden sollte.  
  
![update](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom5.png)  
  
## <a name="customize-the-update-password-page-description"></a>Anpassen der Beschreibung für die Seite zum Aktualisieren des Kennworts  
Verwenden Sie zum Anpassen der Beschreibung der Seite zum Aktualisieren des Kennworts das folgende Windows PowerShell-Cmdlet und die folgende Syntax.  
  

    Set-AdfsGlobalWebContent -UpdatePasswordPageDescriptionText "This is the Contoso Update Password page."  

## <a name="additional-references"></a>Weitere Verweise 
[AD FS Anpassung der Benutzeranmeldung](AD-FS-user-sign-in-customization.md)  
