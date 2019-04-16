---
title: "Wiederherstellung des AD-Gesamtstruktur - den RID-Pool ungültig"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 2f5f84df-bd85-4ca4-bdd3-835bd1d45c11
ms.technology: identity-adfs
ms.openlocfilehash: cb024356ae5f872e93448d73ea54b271fe3fae4d
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="ad-forest-recovery---invalidating-the-current-rid-pool"></a>Wiederherstellung des AD-Gesamtstruktur - den aktuellen RID-Pool ungültig  

>Gilt für: Windows Server2016, Windows Server2012 und 2012 R2, Windows Server2008 und 2008 R2

 Verwenden Sie das folgende Verfahren an uns Windows PowerShell den aktuellen RID-Pool auf einem Domänencontroller für ungültig erklärt. Windows PowerShell ist standardmäßig aktiviert, auf Windows Server2012 und Windows Server2008 R2, jedoch nicht Windows Server2008, auf dem mithilfe von installiert werden müssen **Features hinzufügen**. Es kann sein [heruntergeladen](https://www.microsoft.com/download/details.aspx?id=20020) unter Windows Server2003 ausführen.  
  
 Den Befehl erfolgreich abgeschlossen wurde, prüfen für Ereignis-ID 16654 (Quelle ist Verzeichnisdienste-SAM) im Systemprotokoll in der Ereignisanzeige in Windows Server2012. Dieses Ereignis wird von frühere Versionen von Windows nicht protokollieren.  
  
> [!NOTE]
>  Nachdem Sie den RID-Pool ungültig, erhalten Sie einen Fehler beim ersten Versuch, Sicherheitsprinzipal (Benutzer, Computer oder Gruppe) zu erstellen. Der Versuch, ein Objekt zu erstellen, wird eine Anforderung für eine neue RID-Pool ausgelöst. Wiederholung des Vorgangs erfolgreich ist, da der neue RID-Pool zugeordnet werden kann.  
  
## <a name="to-invalidate-the-current-rid-pool"></a>Um den aktuellen RID-Pool ungültig  
  
1.  Öffnen Sie eine Windows PowerShell-Sitzung mit erhöhten Rechten, führen Sie den folgenden Befehl aus, und drücken Sie die EINGABETASTE:  
  
    ```  
    $Domain = New-Object System.DirectoryServices.DirectoryEntry  
    $DomainSid = $Domain.objectSid  
    $RootDSE = New-Object System.DirectoryServices.DirectoryEntry("LDAP://RootDSE")  
    $RootDSE.UsePropertyCache = $false  
    $RootDSE.Put("invalidateRidPool", $DomainSid.Value)  
    $RootDSE.SetInfo()  
    ```  
  
## <a name="next-steps"></a>Nächste Schritte

- [AD-Gesamtstruktur für die Wiederherstellung](AD-Forest-Recovery-Guide.md)
- [Wiederherstellung der Active Directory-Gesamtstruktur - Verfahren](AD-Forest-Recovery-Procedures.md)
