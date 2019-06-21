---
title: Erstellen einer DNS-Zone
description: Dieses Thema ist Teil des Leitfadens Verwaltung von IP-Adressverwaltung (IPAM) in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-ipam
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a030ff51-a815-4fc4-b26d-aae41c3e4ce5
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 83e3865308fd45e88b800753b20ab298f9a14c96
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/20/2019
ms.locfileid: "67282253"
---
# <a name="create-a-dns-zone"></a>Erstellen einer DNS-Zone

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Sie können in diesem Thema verwenden, um eine DNS-Zone mithilfe der IPAM-Clientkonsole zu erstellen.  
  
Die Mitgliedschaft in **Administratoren** oder einer entsprechenden Gruppe ist die Mindestanforderung für die Durchführung dieses Verfahrens.  
  
### <a name="to-create-a-dns-zone"></a>Zum Erstellen einer DNS-zone  
  
1.  Klicken Sie im Server-Manager **IPAM**. Die IPAM-Clientkonsole angezeigt wird.  
  
2.  Klicken Sie im Navigationsbereich in **ÜBERWACHEN und verwalten**, klicken Sie auf **DNS- und DHCP-Server**. Klicken Sie im Anzeigebereich auf **Servertyp**, und klicken Sie dann auf **DNS**. Alle DNS-Server, die von IPAM verwaltet werden, werden in den Suchergebnissen aufgeführt.  
  
3.  Suchen Sie den Server, in dem Sie eine Zone hinzufügen möchten, und mit der rechten Maustaste in des Servers.  Klicken Sie auf **DNS-Zone erstellen**.  
  
    ![DNS-Zone erstellen](../../media/Create-a-DNS-Zone/ipam_CreateDNSZone_01a.jpg)  
  
4.  Die **die DNS-Zone erstellen** Dialogfeld wird geöffnet. In **allgemeine Eigenschaften**, wählen Sie eine Zone-Kategorie, einen Typ, und geben Sie einen Namen in **Zonenname**. Wählen Sie auch Werte, die für Ihre Bereitstellung in **erweiterte Eigenschaften**, und klicken Sie dann auf **OK**.  
  
    ![Erweiterte Eigenschaften](../../media/Create-a-DNS-Zone/ipam_CreateDNSZone_02a.jpg)  
  
## <a name="see-also"></a>Siehe auch  
[DNS-Zonenverwaltung](DNS-Zone-Management.md)  
[Verwalten von IPAM](Manage-IPAM.md)  
  


