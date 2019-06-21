---
title: Bearbeiten einer DNS-Zone
description: Dieses Thema ist Teil des Leitfadens Verwaltung von IP-Adressverwaltung (IPAM) in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-ipam
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a35164e1-11ad-47c8-9843-580d30c70d07
ms.author: pashort
author: shortpatti
ms.openlocfilehash: d688790828cb58b9fca2a17c95212c064532bb22
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/20/2019
ms.locfileid: "67282171"
---
# <a name="edit-a-dns-zone"></a>Bearbeiten einer DNS-Zone

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Sie können in diesem Thema verwenden, um eine DNS-Zone in der IPAM-Clientkonsole zu bearbeiten.  
  
Die Mitgliedschaft in **Administratoren** oder einer entsprechenden Gruppe ist die Mindestanforderung für die Durchführung dieses Verfahrens.  
  
### <a name="to-edit-a-dns-zone"></a>So bearbeiten Sie eine DNS-zone  
  
1.  Klicken Sie im Server-Manager **IPAM**. Die IPAM-Clientkonsole angezeigt wird.  
  
2.  Klicken Sie im Navigationsbereich in **ÜBERWACHEN und verwalten**, klicken Sie auf **DNS-Zonen**. Im Navigationsbereich, die in einer oberen Navigationsbereich und einer unteren Navigationsbereich unterteilt werden.  
  
3.  Stellen Sie im unteren Navigationsbereich wird eine der folgenden Optionen aus:  
  
    -   Forward-Lookupzone  
  
    -   IPv4 Reverse-Lookup  
  
    -   IPv6-Reverse-Lookup  
  
4.  Wählen Sie z. B. die IPv4-Reverse-Lookup.  
  
    ![Wählen Sie eine zone](../../media/Edit-a-DNS-Zone/ipam_EditZone_01.jpg)  
  
5.  Klicken Sie im Anzeigebereich mit der Maustaste der Zone, die Sie bearbeiten möchten, und klicken Sie dann auf **bearbeiten DNS-Zone**.  
  
    ![Bearbeiten von DNS-Zone](../../media/Edit-a-DNS-Zone/ipam_EditZone_02.jpg)  
  
6.  Die **bearbeiten DNS-Zone** Dialogfeld wird geöffnet, und die **allgemeine** ausgewählten Seite. Wenn erforderlich, bearbeiten Sie die allgemeine Zoneneigenschaften: **DNS-Server**, **Zone Kategorie**, und **Zonentyp**, und klicken Sie dann auf **übernehmen** oder, wenn die Bearbeitung abgeschlossen ist, sind **OK**.  
  
    ![Zoneneigenschaften bearbeiten und speichern](../../media/Edit-a-DNS-Zone/ipam_EditZone_03a.jpg)  
  
7.  In der **bearbeiten DNS-Zone** Dialogfeld klicken Sie auf **erweitert**. Die **erweitert** Zoneneigenschaften-Seite wird geöffnet. Wenn erforderlich, bearbeiten Sie die Eigenschaften, die Sie ändern möchten, und klicken Sie dann auf **übernehmen** oder, wenn die Bearbeitung abgeschlossen ist, sind **OK**.  
  
    ![Erweiterte Zoneneigenschaften bearbeiten](../../media/Edit-a-DNS-Zone/ipam_EditZone_04a.jpg)  
  
8.  Bei Bedarf wählen Sie die zusätzlichen Eigenschaften Seite Zonennamen (Namenserver, d. h. einer SOA-Zonenübertragungen), nehmen Ihre Bearbeitungen vor, und klicken Sie auf **übernehmen** oder **OK**. Um alle Änderungen Zone zu überprüfen, klicken Sie auf **Zusammenfassung**, und klicken Sie dann auf **OK**.  
  
## <a name="see-also"></a>Siehe auch  
[DNS-Zonenverwaltung](DNS-Zone-Management.md)  
[Verwalten von IPAM](Manage-IPAM.md)  
  


