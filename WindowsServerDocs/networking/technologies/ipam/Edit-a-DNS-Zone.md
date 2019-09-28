---
title: Bearbeiten einer DNS-Zone
description: Dieses Thema ist Teil des Verwaltungs Handbuchs für die IP-Adressverwaltung (IPAM) in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ipam
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a35164e1-11ad-47c8-9843-580d30c70d07
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 2175cf9c740d7b727ba017922a77c94d4379c891
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71355276"
---
# <a name="edit-a-dns-zone"></a>Bearbeiten einer DNS-Zone

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Sie können dieses Thema verwenden, um eine DNS-Zone in der IPAM-Client Konsole zu bearbeiten.  
  
Die Mitgliedschaft in **Administratoren** oder einer entsprechenden Gruppe ist die Mindestanforderung für die Durchführung dieses Verfahrens.  
  
### <a name="to-edit-a-dns-zone"></a>So bearbeiten Sie eine DNS-Zone  
  
1.  Klicken Sie in Server-Manager auf **IPAM**. Die IPAM-Client Konsole wird angezeigt.  
  
2.  Klicken Sie im Navigationsbereich unter **überwachen und verwalten**auf **DNS-Zonen**. Der Navigationsbereich gliedert sich in einen oberen Navigationsbereich und einen niedrigeren Navigationsbereich.  
  
3.  Stellen Sie im unteren Navigationsbereich eine der folgenden Optionen zur Auswahl:  
  
    -   Forward-Lookup  
  
    -   IPv4-Reverse-Lookup  
  
    -   IPv6-Reverse-Lookup  
  
4.  Wählen Sie z. b. IPv4-Reverse-Lookup aus.  
  
    ![Zonentyp auswählen](../../media/Edit-a-DNS-Zone/ipam_EditZone_01.jpg)  
  
5.  Klicken Sie im Anzeigebereich mit der rechten Maustaste auf die Zone, die Sie bearbeiten möchten, und klicken Sie dann auf **DNS-Zone bearbeiten**.  
  
    ![DNS-Zone bearbeiten](../../media/Edit-a-DNS-Zone/ipam_EditZone_02.jpg)  
  
6.  Das Dialogfeld **DNS-Zone bearbeiten** wird geöffnet, und die Seite **Allgemein** ist ausgewählt. Bearbeiten Sie bei Bedarf die allgemeinen Zonen Eigenschaften: **DNS-Server**, **Zonen Kategorie**und **Zonentyp**, und klicken Sie dann auf **anwenden** , oder wenn Ihre Bearbeitung **fertig ist**  
  
    ![Zonen Eigenschaften bearbeiten und speichern](../../media/Edit-a-DNS-Zone/ipam_EditZone_03a.jpg)  
  
7.  Klicken Sie im Dialogfeld **DNS-Zone bearbeiten** auf **erweitert**. Die Seite **Erweiterte** Zonen Eigenschaften wird geöffnet. Bearbeiten Sie ggf. die Eigenschaften, die Sie ändern möchten, und klicken Sie dann auf übernehmen. Wenn Ihre Bearbeitung fertig **ist,** klicken Sie auf **anwenden** .  
  
    ![Erweiterte Zonen Eigenschaften bearbeiten](../../media/Edit-a-DNS-Zone/ipam_EditZone_04a.jpg)  
  
8.  Wählen Sie bei Bedarf die Eigenschaften der zusätzlichen Zonen Eigenschaften aus (Namen Server, SOA, Zonenübertragungen), nehmen Sie die Änderungen vor, und klicken **Sie auf über** nehmen oder **OK**. Klicken Sie auf **Zusammenfassung**, und klicken Sie dann auf **OK**, um alle Änderungen an der Zone zu überprüfen.  
  
## <a name="see-also"></a>Siehe auch  
[DNS-Zonenverwaltung](DNS-Zone-Management.md)  
[Verwalten von IPAM](Manage-IPAM.md)  
  


