---
title: Wiederherstellung des AD-Gesamtstruktur - Bereinigen von Metadaten entfernter dcs
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: e7543381-4081-407f-adad-a9de792c6616
ms.technology: identity-adfs
ms.openlocfilehash: 3027c59b58801b44d20127e6bcf62dd7319708bd
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="ad-forest-recovery---cleaning-metadata-of-removed-writable-domain-controllers"></a>Wiederherstellung des AD-Gesamtstruktur - Bereinigen von Metadaten entfernter beschreibbarer Domänencontroller 

>Gilt für: Windows Server2016, Windows Server2012 und 2012 R2, Windows Server2008 und 2008 R2
 
 Metadatencleanup entfernt Active Directory-Daten, die einen Domänencontroller im Replikationssystem identifiziert.  
  
 Verwenden Sie das folgende Verfahren, um die DC-Objekte für Domänencontroller zu löschen, die Sie durch erneutes Installieren von AD DS und dem Netzwerk wieder zu hinzufügen möchten.  
  
 Wenn Sie die Version des Active Directory-Benutzer und -Computer oder Active Directory-Standorte und Dienste, die Remoteserver-Verwaltungstools (RSAT) enthalten, wird Metadatenbereinigung automatisch ausgeführt, wenn Sie ein DC-Objekt löschen.  
  

## <a name="deleting-a-domain-controller-using-active-directory-users-and-computers"></a>Löschen einen Domänencontroller mithilfe von Active Directory-Benutzer und -Computer  
 Wenn Sie die Version des Active Directory-Benutzer und -Computer oder Active Directory-Verwaltungscenter in Remoteserver-Verwaltungstools (RSAT) verwenden, wird Metadatenbereinigung automatisch ausgeführt, wenn Sie das Domänencontrollerobjekt löschen. Das Serverobjekt und das Computerobjekt werden auch automatisch gelöscht.  
  
 Als Alternative können auch können Active Directory-Standorte und -Dienste in Remoteserver-Verwaltungstools Sie ein DC-Objekt löschen. Wenn Sie Active Directory-Standorte und -Dienste verwenden, müssen Sie die zugehörigen Serverobjekts und NTDS-Einstellungsobjekt löschen, bevor Sie das Domänencontrollerobjekt löschen können.  
  
 Remoteserver-Verwaltungstools herunterladen:  

-   [Remoteserver-Verwaltungstools für Windows10](https://www.microsoft.com/download/details.aspx?id=45520)
  
-   [Remoteserver-Verwaltungstools für Windows8](https://www.microsoft.com/download/details.aspx?id=28972)  

-   [Remoteserver-Verwaltungstools für Windows7 mit Servicepack 1 (SP1)](https://www.microsoft.com/download/details.aspx?id=7887)  
  
-   [Microsoft Remoteserver-Verwaltungstools für windowsvista](https://www.microsoft.com/download/details.aspx?id=21090)  
  
 Das folgende Verfahren gilt für Domänencontroller, auf denen entweder Windows Server2016, 2012, 2008 R2 oder 2008 ausgeführt. Der Zieldomänencontroller die Bereinigung Metadaten kann eine beliebige Version von Windows Server ausführen.  
  
### <a name="to-delete-a-domain-controller-object-using-active-directory-users-and-computers-in-rsat"></a>So löschen Sie einen Domänencontroller-Objekts mithilfe von Active Directory-Benutzer und -Computer in Remoteserver-Verwaltungstools  
  
1.  Klicken Sie auf **starten**, klicken Sie auf **Verwaltung**, und klicken Sie dann auf **Active Directory-Benutzer und -Computer**.  
2.  Klicken Sie in der Konsolenstruktur, doppelklicken Sie auf den Domänencontainer, und doppelklicken Sie dann auf die **Domänencontroller** Organisationseinheit (OU).  
3.  Klicken Sie im Detailbereich mit der Maustaste im Domänencontrollers, die Sie löschen möchten, und klicken Sie dann auf **löschen**. 
![Löschen](media/AD-Forest-Recovery-Cleaning-Metadata/delete1.png) 
4.  Klicken Sie auf **Ja** zu bestätigen. Wählen Sie die **dieser Domänencontroller ist dauerhaft offline und kann nicht mehr mit dem Active Directory Domain Services Installation Assistenten (DCPROMO) herabgestuft werden** Kontrollkästchen und klicken Sie dann auf **löschen**.  
5.  Wenn der Domänencontroller ein globaler Katalogserver war, klicken Sie auf **Ja** bestätigen Sie, dass das Löschen.  
  
## <a name="next-steps"></a>Nächste Schritte

- [AD-Gesamtstruktur für die Wiederherstellung](AD-Forest-Recovery-Guide.md)
- [Wiederherstellung der Active Directory-Gesamtstruktur - Verfahren](AD-Forest-Recovery-Procedures.md)
  
