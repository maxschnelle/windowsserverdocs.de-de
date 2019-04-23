---
title: 'AD-Gesamtstruktur-Wiederherstellung: den RID-Pool ungültig'
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 2f5f84df-bd85-4ca4-bdd3-835bd1d45c11
ms.technology: identity-adds
ms.openlocfilehash: 46115991e48da301a8a739009bac27415ebe73df
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59842511"
---
# <a name="ad-forest-recovery---invalidating-the-current-rid-pool"></a>AD-Gesamtstruktur-Wiederherstellung: den aktuelle RID-Pool ungültig  

>Gilt für: Windows Server 2016, Windows Server 2012 und 2012 R2, Windows Server 2008 und 2008 R2

Gehen Sie mit uns Windows PowerShell auf einem Domänencontroller den aktuelle RID-Pool ungültig gemacht werden. Windows PowerShell ist standardmäßig aktiviert, auf Windows Server 2012 und Windows Server 2008 R2, aber nicht Windows Server 2008, in dem er installiert werden mithilfe von **Features hinzufügen**. Es kann sein [heruntergeladen](https://www.microsoft.com/download/details.aspx?id=20020) unter Windows Server 2003 ausführen.  

Den Befehl erfolgreich abgeschlossen wurde, prüfen 16654 der Ereignis-ID (Quelle ist Verzeichnisdienste-SAM) im Systemprotokoll der Ereignisanzeige in Windows Server 2012. Dieses Ereignis wird von frühere Versionen von Windows nicht protokollieren.  
  
> [!NOTE]
> Nachdem Sie den RID-Pool ungültig, erhalten Sie einen Fehler beim ersten Erstellen der Sicherheitsprinzipal (Benutzer, Computer oder Gruppe). Der Versuch, ein Objekt zu erstellen, löst eine Anforderung für ein neuer RID-Pool. Wiederholung des Vorgangs ist erfolgreich, da der neue RID-Pool zugeordnet wird.  
  
## <a name="to-invalidate-the-current-rid-pool"></a>Den aktuelle RID-Pool ungültig gemacht werden  
  
- Öffnen Sie eine Windows PowerShell-Sitzung mit erhöhten Rechten, führen Sie den folgenden Befehl aus, und drücken Sie EINGABETASTE:  

   ```powershell
   $Domain = New-Object System.DirectoryServices.DirectoryEntry  
   $DomainSid = $Domain.objectSid  
   $RootDSE = New-Object System.DirectoryServices.DirectoryEntry("LDAP://RootDSE")  
   $RootDSE.UsePropertyCache = $false  
   $RootDSE.Put("invalidateRidPool", $DomainSid.Value)  
   $RootDSE.SetInfo()  
   ```  

## <a name="next-steps"></a>Nächste Schritte

- [Für die Wiederherstellung des AD-Gesamtstruktur](AD-Forest-Recovery-Guide.md)
- [Wiederherstellung der Gesamtstruktur der Active Directory - Prozeduren](AD-Forest-Recovery-Procedures.md)
