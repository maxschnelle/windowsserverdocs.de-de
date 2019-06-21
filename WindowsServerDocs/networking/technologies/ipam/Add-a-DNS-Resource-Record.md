---
title: Hinzufügen eines DNS-Ressourceneintrags
description: Dieses Thema ist Teil des Leitfadens Verwaltung von IP-Adressverwaltung (IPAM) in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-ipam
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5379373f-a3d9-4f51-b6fc-bf0f6df1d244
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 36773525187229e498b9addf4b1e6532fd413701
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/20/2019
ms.locfileid: "67282314"
---
# <a name="add-a-dns-resource-record"></a>Hinzufügen eines DNS-Ressourceneintrags

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Sie können in diesem Thema verwenden, um eine oder mehrere neue DNS-Ressourceneinträge mithilfe der IPAM-Clientkonsole hinzufügen.  
  
Die Mitgliedschaft in **Administratoren** oder einer entsprechenden Gruppe ist die Mindestanforderung für die Durchführung dieses Verfahrens.  
  
### <a name="to-add-a-dns-resource-record"></a>Hinzufügen ein DNS-Ressourceneintrags  
  
1.  Klicken Sie im Server-Manager **IPAM**. Die IPAM-Clientkonsole angezeigt wird.  
  
2.  Klicken Sie im Navigationsbereich in **ÜBERWACHEN und verwalten**, klicken Sie auf **DNS-Zonen**.  Im Navigationsbereich, die in einer oberen Navigationsbereich und einer unteren Navigationsbereich unterteilt werden.  
  
3.  Klicken Sie im unteren Navigationsbereich auf **Forward-Lookup**. Alle IPAM verwalteten DNS-Forward-Lookup-Zonen werden in den Suchergebnissen der Anzeige im Bereich angezeigt. Mit der rechten Maustaste in der Zone, in denen Sie möchten zum Hinzufügen eines Ressourceneintrags, und klicken Sie dann auf **Hinzufügen von DNS-Ressourceneintrag**.  
  
    ![Hinzufügen von DNS-Ressourceneintrag](../../media/Add-a-DNS-Resource-Record/ipam_DNSrr_01.jpg)
  
4.  Die **Hinzufügen von DNS-Ressourceneinträge** Dialogfeld wird geöffnet. In **Datensatz Ressourceneigenschaften**, klicken Sie auf **DNS-Server** , und wählen Sie den DNS-Server, in dem Sie eine oder mehrere neue Ressourceneinträge hinzufügen möchten. In **Konfigurieren von DNS-Ressourceneinträge**, klicken Sie auf **neu**.  
  
    ![Konfigurieren von DNS-Ressourceneinträgen](../../media/Add-a-DNS-Resource-Record/ipam_DNSrr_02.jpg)  
  
5.  Das Dialogfeld wird erweitert, um Sie anzuzeigen **neuer Ressourcendatensatz**. Klicken Sie auf **Ressourceneintragstyp**.  
  
    ![Typ des Ressourcendatensatzes](../../media/Add-a-DNS-Resource-Record/ipam_DNSrr_03.jpg)  
  
6.  Die Liste der Ressourcendatensatztypen wird angezeigt. Klicken Sie auf den Ressourcentyp für den Datensatz, den Sie hinzufügen möchten.  
  
    ![Wählen Sie Datensatztyp hinzufügen aus](../../media/Add-a-DNS-Resource-Record/ipam_DNSrr_04.jpg)  
  
7.  In **neuer Ressourcendatensatz,** in **Namen**, geben Sie einen Datensatz. In **IP-Adresse**, geben Sie eine IP-Adresse ein, und wählen Sie dann die Datensatz-Ressourceneigenschaften, die für Ihre Bereitstellung geeignet sind. Klicken Sie auf **hinzufügen**.  
  
    ![Hinzufügen](../../media/Add-a-DNS-Resource-Record/ipam_DNSrr_06.jpg)  
  
8.  Wenn Sie keine weiteren neuen Ressourceneinträge erstellen möchten, klicken Sie auf **OK**. Wenn Sie zusätzliche neue Ressourceneinträge erstellen möchten, klicken Sie auf **neu**.  
  
    ![Klicken Sie auf OK oder neuer](../../media/Add-a-DNS-Resource-Record/ipam_DNSrr_r2_01.jpg)
  
9. Das Dialogfeld wird erweitert, um Sie anzuzeigen **neuer Ressourcendatensatz**. Klicken Sie auf **Ressourceneintragstyp**. Die Liste der Ressourcendatensatztypen wird angezeigt. Klicken Sie auf den Ressourcentyp für den Datensatz, den Sie hinzufügen möchten.  
  
10. In **neuer Ressourcendatensatz,** in **Namen**, geben Sie einen Datensatz. In **IP-Adresse**, geben Sie eine IP-Adresse ein, und wählen Sie dann die Datensatz-Ressourceneigenschaften, die für Ihre Bereitstellung geeignet sind. Klicken Sie auf **hinzufügen**.  
  
    ![Hinzufügen](../../media/Add-a-DNS-Resource-Record/ipam_DNSrr_r2_02.jpg)  
  
11. Wenn Sie mehrere Ressourceneinträge hinzufügen möchten, wiederholen Sie den Vorgang zum Erstellen von Datensätzen. Wenn Sie erstellen neue Ressourceneinträge fertig sind, klicken Sie auf **übernehmen**.  
  
    ![Erstellen des Datensatzes umfangreiche Ressource](../../media/Add-a-DNS-Resource-Record/ipam_DNSrr_r2_03.jpg)  
  
12. Die **hinzufügen-Ressourceneintrag** im Dialogfeld zeigt eine Zusammenfassung der Ressourcen-Datensätze an, während die Ressourceneinträge in IPAM auf dem DNS-Server erstellt wird, die Sie angegeben. Wenn die Datensätze erfolgreich erstellt werden, die **Status** des Datensatzes ist **Erfolg**.  
  
    ![Hinzufügen von Datensatzstatus](../../media/Add-a-DNS-Resource-Record/ipam_DNSrr_r2_04.jpg)  
  
13. Klicken Sie auf **OK**.  
  
## <a name="see-also"></a>Siehe auch  
[DNS-Datensatz Ressourcenverwaltung](DNS-Resource-Record-Management.md)  
[Verwalten von IPAM](Manage-IPAM.md)  
  


