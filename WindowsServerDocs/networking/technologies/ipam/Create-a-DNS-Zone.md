---
title: Erstellen einer DNS-Zone
description: Dieses Thema ist Teil des Verwaltungs Handbuchs für die IP-Adressverwaltung (IPAM) in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ipam
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a030ff51-a815-4fc4-b26d-aae41c3e4ce5
ms.author: pashort
author: shortpatti
ms.openlocfilehash: dbd46ad129a4b3e5bbbe55f584f1bae43bd077c3
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71355414"
---
# <a name="create-a-dns-zone"></a>Erstellen einer DNS-Zone

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Sie können dieses Thema verwenden, um eine DNS-Zone mit der IPAM-Client Konsole zu erstellen.  
  
Die Mitgliedschaft in **Administratoren** oder einer entsprechenden Gruppe ist die Mindestanforderung für die Durchführung dieses Verfahrens.  
  
### <a name="to-create-a-dns-zone"></a>So erstellen Sie eine DNS-Zone  
  
1.  Klicken Sie in Server-Manager auf **IPAM**. Die IPAM-Client Konsole wird angezeigt.  
  
2.  Klicken Sie im Navigationsbereich unter **überwachen und verwalten**auf **DNS-und DHCP-Server**. Klicken Sie im Anzeigebereich auf **Servertyp**, und klicken Sie dann auf **DNS**. Alle DNS-Server, die von IPAM verwaltet werden, werden in den Suchergebnissen aufgeführt.  
  
3.  Suchen Sie den Server, auf dem Sie eine Zone hinzufügen möchten, und klicken Sie mit der rechten Maustaste auf den Server.  Klicken Sie auf **DNS-Zone erstellen**.  
  
    ![Erstellen einer DNS-Zone](../../media/Create-a-DNS-Zone/ipam_CreateDNSZone_01a.jpg)  
  
4.  Das Dialogfeld **DNS-Zone erstellen** wird geöffnet. Wählen Sie unter **Allgemeine Eigenschaften**eine Zonen Kategorie, einen Zonentyp aus, und geben Sie in **Zonenname**einen Namen ein. Wählen Sie in **Erweiterte Eigenschaften**auch Werte für Ihre Bereitstellung aus, und klicken Sie dann auf **OK**.  
  
    ![Erweiterte Eigenschaften](../../media/Create-a-DNS-Zone/ipam_CreateDNSZone_02a.jpg)  
  
## <a name="see-also"></a>Siehe auch  
[DNS-Zonenverwaltung](DNS-Zone-Management.md)  
[Verwalten von IPAM](Manage-IPAM.md)  
  


