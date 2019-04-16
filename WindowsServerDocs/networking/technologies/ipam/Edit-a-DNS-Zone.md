---
title: Bearbeiten einer DNS-Zone
description: Dieses Thema ist Teil des Handbuchs Verwaltung von IP-Adressverwaltung (IPAM) in Windows Server2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-ipam
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a35164e1-11ad-47c8-9843-580d30c70d07
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 3e7cc75017c2b59293a042d4af0a677d3eda46c0
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="edit-a-dns-zone"></a>Bearbeiten einer DNS-Zone

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

In diesem Thema können Sie eine DNS-Zone in der IPAM-Clientkonsole bearbeiten.  
  
Mitgliedschaft in **Administratoren**, oder einer gleichwertigen Gruppe ist mindestens erforderlich, um dieses Verfahren auszuführen.  
  
### <a name="to-edit-a-dns-zone"></a>So bearbeiten Sie eine DNS-Zone  
  
1.  Klicken Sie im Server-Manager auf **IPAM**. Die IPAM-Clientkonsole angezeigt wird.  
  
2.  Klicken Sie im Navigationsbereich in **ÜBERWACHEN und verwalten**, klicken Sie auf **DNS-Zonen**. Der Navigationsbereich unterteilt in ein im oberen Navigationsbereich und einen unteren Navigationsbereich.  
  
3.  Klicken Sie im unteren Navigationsbereich stellen Sie eine der folgenden Optionen:  
  
    -   Forward-Lookupzone  
  
    -   IPv4 Reverse-Lookup  
  
    -   IPv6-Reverse-Lookup  
  
4.  Wählen Sie z.B. IPv4 Reverse-Lookup.  
  
    ![Wählen Sie eine Zone](../../media/Edit-a-DNS-Zone/ipam_EditZone_01.jpg)  
  
5.  Klicken Sie im Anzeigebereich mit der Maustaste der Zone, die Sie bearbeiten möchten, und klicken Sie dann auf **bearbeiten DNS-Zone**.  
  
    ![Bearbeiten von DNS-Zone](../../media/Edit-a-DNS-Zone/ipam_EditZone_02.jpg)  
  
6.  Die **bearbeiten DNS-Zone** Dialogfeld wird geöffnet, mit der **allgemeine** Seite ausgewählt. Bei Bedarf bearbeiten Sie die allgemeinen Eigenschaften: **DNS-Server**, **Zone Kategorie**, und **Zonentyp**, und klicken Sie dann auf **übernehmen** oder, wenn die Bearbeitung abgeschlossen ist, sind **OK**.  
  
    ![Zoneneigenschaften bearbeiten und speichern](../../media/Edit-a-DNS-Zone/ipam_EditZone_03a.jpg)  
  
7.  In der **bearbeiten DNS-Zone** Dialogfeld, klicken Sie auf **erweitert**. Die **erweitert** Zone Eigenschaftenseite wird geöffnet. Bei Bedarf die Eigenschaften, die Sie ändern möchten, und klicken Sie dann auf Bearbeiten **übernehmen** oder, wenn die Bearbeitung abgeschlossen ist, sind **OK**.  
  
    ![Bearbeiten der Zoneneigenschaften für erweiterte](../../media/Edit-a-DNS-Zone/ipam_EditZone_04a.jpg)  
  
8.  Bei Bedarf, wählen Sie die zusätzlichen Eigenschaften Seite Zonennamen (Zonenübertragungen Namenserver, SOA), nehmen Sie die Bearbeitung, und klicken Sie auf **übernehmen** oder **OK**. Um alle Ihre Bearbeitungen Zone zu überprüfen, klicken Sie auf **Zusammenfassung**, und klicken Sie dann auf **OK**.  
  
## <a name="see-also"></a>Siehe auch  
[DNS-Zonenverwaltung](DNS-Zone-Management.md)  
[Verwalten von IPAM](Manage-IPAM.md)  
  


