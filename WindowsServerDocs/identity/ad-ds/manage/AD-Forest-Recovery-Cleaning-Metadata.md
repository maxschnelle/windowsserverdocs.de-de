---
title: 'AD-Gesamtstruktur-Wiederherstellung: Bereinigen von Metadaten der entfernten Domänencontroller'
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: e7543381-4081-407f-adad-a9de792c6616
ms.technology: identity-adds
ms.openlocfilehash: b71cab51a362a96ab6071e5eed3cf31c4421041c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59843041"
---
# <a name="ad-forest-recovery---cleaning-metadata-of-removed-writable-domain-controllers"></a>AD-Gesamtstruktur-Wiederherstellung: Bereinigen von Metadaten entfernter beschreibbarer Domänencontroller

>Gilt für: Windows Server 2016, Windows Server 2012 und 2012 R2, Windows Server 2008 und 2008 R2

Metadatencleanup entfernt die Active Directory-Daten, die einen Domänencontroller im Replikationssystem zu identifizieren.  

Verwenden Sie das folgende Verfahren, um die DC-Objekte für Domänencontroller zu löschen, die Sie planen, wieder mit dem Netzwerk hinzuzufügen, installieren Sie AD DS neu.  
  
Wenn Sie die Version des Active Directory-Benutzer und Computer verwenden, oder Active Directory-Standorte und Dienste, die enthalten Remote Server Administration Tools (RSAT), wird Metadatencleanup automatisch ausgeführt, wenn Sie ein DC-Objekt löschen.  

## <a name="deleting-a-domain-controller-using-active-directory-users-and-computers"></a>Löschen einen Domänencontroller mithilfe von Active Directory-Benutzer und-Computer

Wenn Sie die Version des Active Directory-Benutzer und-Computer oder Active Directory Administrative Center in Remote Server Administration Tools (RSAT) verwenden, wird Metadatencleanup automatisch ausgeführt, wenn Sie das Domänencontrollerobjekt löschen. Das Server-Objekt und dem Computerobjekt werden auch automatisch gelöscht.  

Als Alternative können auch können Active Directory-Standorte und-Dienste in Remoteserver-Verwaltungstools Sie um einen DC-Objekt zu löschen. Wenn Sie Active Directory-Standorte und-Dienste verwenden, müssen Sie den zugeordneten Server-Objekt und das NTDS-Einstellungsobjekt löschen, bevor Sie das Domänencontrollerobjekt löschen können.  

Informationen zum Installieren der Remoteserver-Verwaltungstools, finden Sie im Artikel [Remoteserver-Verwaltungstools](https://docs.microsoft.com/windows-server/remote/remote-server-administration-tools).
  
Das folgende Verfahren gilt für Domänencontroller mit entweder Windows Server 2016, 2012, 2008 R2 oder 2008. Das Ziel-DC von der Bereinigungsvorgang Metadaten kann eine beliebige Version von Windows Server ausführen.  
  
### <a name="to-delete-a-domain-controller-object-using-active-directory-users-and-computers-in-rsat"></a>So löschen Sie einen Domänencontroller-Objekts mithilfe von Active Directory-Benutzer und-Computer in Remoteserver-Verwaltungstools  
  
1. Klicken Sie auf **Start**, zeigen Sie auf **Verwaltung**, und klicken Sie dann auf **Active Directory-Benutzer und -Computer**.  
2. Doppelklicken Sie in der Konsolenstruktur den Domänencontainer und doppelklicken Sie dann auf die **Domänencontroller** Organisationseinheit (OU).  
3. Im Detailbereich mit der Maustaste der Domänencontroller, die Sie löschen möchten, und klicken Sie dann auf **löschen**.
   ![Löschen](media/AD-Forest-Recovery-Cleaning-Metadata/delete1.png) 
4. Klicken Sie zum Bestätigen des Löschvorgangs auf **Ja**. Wählen Sie die **dieser Domänencontroller ist dauerhaft offline und kann nicht mehr mit der Active Directory Domain Services Installation Assistenten (DCPROMO) herabgestuft werden** Kontrollkästchen und klicken Sie auf **löschen**.  
5. Wenn der Domänencontroller einen globalen Katalogserver gestellt wurde, klicken Sie auf **Ja** überprüfen Sie, ob die Löschung.  

## <a name="next-steps"></a>Nächste Schritte

- [Für die Wiederherstellung des AD-Gesamtstruktur](AD-Forest-Recovery-Guide.md)
- [Wiederherstellung der Gesamtstruktur der Active Directory - Prozeduren](AD-Forest-Recovery-Procedures.md)
