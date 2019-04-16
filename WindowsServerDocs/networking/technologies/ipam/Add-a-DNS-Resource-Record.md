---
title: Hinzufügen eines DNS-Ressourceneintrags
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
ms.assetid: 5379373f-a3d9-4f51-b6fc-bf0f6df1d244
ms.author: pashort
author: shortpatti
ms.openlocfilehash: e14a59e9f172b20e85a34d2299e3733a796adafc
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="add-a-dns-resource-record"></a>Hinzufügen eines DNS-Ressourceneintrags

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

In diesem Thema können Sie eine oder mehrere neue DNS-Ressourceneinträge mit IPAM-Clientkonsole hinzufügen.  
  
Mitgliedschaft in **Administratoren**, oder einer gleichwertigen Gruppe ist mindestens erforderlich, um dieses Verfahren auszuführen.  
  
### <a name="to-add-a-dns-resource-record"></a>So fügen Sie einen DNS-Ressourceneintrag hinzu  
  
1.  Klicken Sie im Server-Manager auf **IPAM**. Die IPAM-Clientkonsole angezeigt wird.  
  
2.  Klicken Sie im Navigationsbereich in **ÜBERWACHEN und verwalten**, klicken Sie auf **DNS-Zonen**.  Der Navigationsbereich unterteilt in ein im oberen Navigationsbereich und einen unteren Navigationsbereich.  
  
3.  Klicken Sie im unteren Navigationsbereich, klicken Sie auf **Forward-Lookup**. Alle IPAM verwalteten DNS-Forward-Lookupzonen werden im Bereich der Suchergebnisse angezeigt. Die Zone soll Hinzufügen eines Ressourceneintrags ein, und klicken Sie dann auf **Hinzufügen von DNS-Ressourceneintrag**.  
  
    ![Hinzufügen von DNS-Ressourceneintrag](../../media/Add-a-DNS-Resource-Record/ipam_DNSrr_01.jpg)
  
4.  Die **DNS-Ressourceneinträge hinzufügen** Dialogfeld wird geöffnet. In **Datensatz Ressourceneigenschaften**, klicken Sie auf **DNS-Server**, und wählen Sie den DNS-Server, in dem Sie eine oder mehrere neue Ressourceneinträge hinzufügen möchten. In **konfigurieren Sie DNS-Ressourceneinträge**, klicken Sie auf **neu**.  
  
    ![Konfigurieren von DNS-Ressourceneinträgen](../../media/Add-a-DNS-Resource-Record/ipam_DNSrr_02.jpg)  
  
5.  Das Dialogfeld wird erweitert, um Sie einzublenden **neuer Ressourcendatensatz**. Klicken Sie auf **Ressourceneintragstyp**.  
  
    ![Typ des Ressourcendatensatzes](../../media/Add-a-DNS-Resource-Record/ipam_DNSrr_03.jpg)  
  
6.  Die Liste der Ressourcendatensatztypen wird angezeigt. Klicken Sie auf den Ressourceneintragstyp, den Sie hinzufügen möchten.  
  
    ![Wählen Sie Datensatztyp hinzu](../../media/Add-a-DNS-Resource-Record/ipam_DNSrr_04.jpg)  
  
7.  In **neuer Ressourcendatensatz** in **Namen**, geben Sie einen Datensatz. In **IP-Adresse**, geben Sie eine IP-Adresse, und wählen Sie dann die Eigenschaften von Ressourcen, die für Ihre Bereitstellung geeignet sind. Klicken Sie auf **hinzufügen**.  
  
    ![Hinzufügen](../../media/Add-a-DNS-Resource-Record/ipam_DNSrr_06.jpg)  
  
8.  Wenn Sie keine weiteren neuen Ressourceneinträge erstellen möchten, klicken Sie auf **OK**. Wenn Sie weitere neue Ressourceneinträge erstellen möchten, klicken Sie auf **neu**.  
  
    ![Klicken Sie auf OK oder neu](../../media/Add-a-DNS-Resource-Record/ipam_DNSrr_r2_01.jpg)
  
9. Das Dialogfeld wird erweitert, um Sie einzublenden **neuer Ressourcendatensatz**. Klicken Sie auf **Ressourceneintragstyp**. Die Liste der Ressourcendatensatztypen wird angezeigt. Klicken Sie auf den Ressourceneintragstyp, den Sie hinzufügen möchten.  
  
10. In **neuer Ressourcendatensatz** in **Namen**, geben Sie einen Datensatz. In **IP-Adresse**, geben Sie eine IP-Adresse, und wählen Sie dann die Eigenschaften von Ressourcen, die für Ihre Bereitstellung geeignet sind. Klicken Sie auf **hinzufügen**.  
  
    ![Hinzufügen](../../media/Add-a-DNS-Resource-Record/ipam_DNSrr_r2_02.jpg)  
  
11. Wenn Sie weitere Ressourceneinträge hinzufügen möchten, wiederholen Sie den Vorgang zum Erstellen von Datensätzen. Wenn Sie das Erstellen von neuen Ressourceneinträge fertig sind, klicken Sie auf **übernehmen**.  
  
    ![Vollständige ressourcenerstellung](../../media/Add-a-DNS-Resource-Record/ipam_DNSrr_r2_03.jpg)  
  
12. Die **Ressourceneintrag hinzufügen** Dialogfeld zeigt eine Zusammenfassung der Ressource Datensätze während IPAM auf dem DNS-Server die Ressourceneinträge erstellt, die Sie angegeben haben. Wenn die Einträge erfolgreich erstellt werden, die **Status** des Eintrags wird **Erfolg**.  
  
    ![Status des Datensatzes hinzufügen](../../media/Add-a-DNS-Resource-Record/ipam_DNSrr_r2_04.jpg)  
  
13. Klicken Sie auf **OK**.  
  
## <a name="see-also"></a>Siehe auch  
[DNS-Datensatz Ressourcenverwaltung](DNS-Resource-Record-Management.md)  
[Verwalten von IPAM](Manage-IPAM.md)  
  


