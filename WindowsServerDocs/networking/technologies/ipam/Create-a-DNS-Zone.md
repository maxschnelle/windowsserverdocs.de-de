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
ms.author: lizross
author: eross-msft
ms.openlocfilehash: a9762d15d0b95954623bbefdec38696885676975
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80312637"
---
# <a name="create-a-dns-zone"></a>Erstellen einer DNS-Zone

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

Sie können dieses Thema verwenden, um eine DNS-Zone mit der IPAM-Client Konsole zu erstellen.  
  
Die Mitgliedschaft in **Administratoren** oder einer entsprechenden Gruppe ist die Mindestanforderung für die Durchführung dieses Verfahrens.  
  
### <a name="to-create-a-dns-zone"></a>So erstellen Sie eine DNS-Zone  
  
1.  Klicken Sie in Server-Manager auf **IPAM**. Die IPAM-Client Konsole wird angezeigt.  
  
2.  Klicken Sie im Navigationsbereich unter **überwachen und verwalten**auf **DNS-und DHCP-Server**. Klicken Sie im Anzeigebereich auf **Servertyp**, und klicken Sie dann auf **DNS**. Alle DNS-Server, die von IPAM verwaltet werden, werden in den Suchergebnissen aufgeführt.  
  
3.  Suchen Sie den Server, auf dem Sie eine Zone hinzufügen möchten, und klicken Sie mit der rechten Maustaste auf den Server.  Klicken Sie auf **DNS-Zone erstellen**.  
  
    ![DNS-Zone erstellen](../../media/Create-a-DNS-Zone/ipam_CreateDNSZone_01a.jpg)  
  
4.  Das Dialogfeld **DNS-Zone erstellen** wird geöffnet. Wählen Sie unter **Allgemeine Eigenschaften**eine Zonen Kategorie, einen Zonentyp aus, und geben Sie in **Zonenname**einen Namen ein. Wählen Sie in **Erweiterte Eigenschaften**auch Werte für Ihre Bereitstellung aus, und klicken Sie dann auf **OK**.  
  
    ![Erweiterte Eigenschaften](../../media/Create-a-DNS-Zone/ipam_CreateDNSZone_02a.jpg)  
  
## <a name="see-also"></a>Weitere Informationen  
[DNS-Zonenverwaltung](DNS-Zone-Management.md)  
[Verwalten von IPAM](Manage-IPAM.md)  
  


