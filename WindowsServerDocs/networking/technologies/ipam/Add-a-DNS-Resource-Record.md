---
title: Hinzufügen eines DNS-Ressourceneintrags
description: Dieses Thema ist Teil des Verwaltungs Handbuchs für die IP-Adressverwaltung (IPAM) in Windows Server 2016.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-ipam
ms.topic: article
ms.assetid: 5379373f-a3d9-4f51-b6fc-bf0f6df1d244
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 67238c1546e8833298ec061cf6e05a038b9d474c
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80814843"
---
# <a name="add-a-dns-resource-record"></a>Hinzufügen eines DNS-Ressourceneintrags

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

In diesem Thema können Sie mithilfe der IPAM-Client Konsole einen oder mehrere neue DNS-Ressourcen Einträge hinzufügen.  
  
Die Mitgliedschaft in **Administratoren** oder einer entsprechenden Gruppe ist die Mindestanforderung für die Durchführung dieses Verfahrens.  
  
### <a name="to-add-a-dns-resource-record"></a>So fügen Sie einen DNS-Ressourcen Daten Satz hinzu  
  
1.  Klicken Sie in Server-Manager auf **IPAM**. Die IPAM-Client Konsole wird angezeigt.  
  
2.  Klicken Sie im Navigationsbereich unter **überwachen und verwalten**auf **DNS-Zonen**.  Der Navigationsbereich gliedert sich in einen oberen Navigationsbereich und einen niedrigeren Navigationsbereich.  
  
3.  Klicken Sie im unteren Navigationsbereich auf **Forward-Lookup**. Alle von IPAM verwalteten DNS-Forward-Lookupzonen werden in den Suchergebnissen des Anzeige Bereichs angezeigt. Klicken Sie mit der rechten Maustaste auf die Zone, der Sie einen Ressourcen Daten Satz hinzufügen möchten, und klicken Sie dann auf **DNS-Ressourcen Daten Satz**  
  
    ![DNS-Ressourcen Daten Satz hinzufügen](../../media/Add-a-DNS-Resource-Record/ipam_DNSrr_01.jpg)
  
4.  Das Dialogfeld **DNS-Ressourcen Einträge hinzufügen** wird geöffnet. Klicken Sie unter **Ressourcen Daten Satz Eigenschaften**auf **DNS-Server** , und wählen Sie den DNS-Server aus, auf dem Sie einen oder mehrere neue Ressourcen Einträge hinzufügen möchten. Klicken Sie unter **DNS-Ressourcen Einträge konfigurieren**auf **neu**.  
  
    ![Konfigurieren von DNS-Ressourcen Einträgen](../../media/Add-a-DNS-Resource-Record/ipam_DNSrr_02.jpg)  
  
5.  Das Dialogfeld wird erweitert, um einen **neuen Ressourcen Daten Satz**anzuzeigen. Klicken Sie auf **Ressourcen Daten Satz**.  
  
    ![Typ des Ressourcendatensatzes](../../media/Add-a-DNS-Resource-Record/ipam_DNSrr_03.jpg)  
  
6.  Die Liste der Ressourcen Daten Satz Typen wird angezeigt. Klicken Sie auf den Ressourcen Daten Satz, den Sie hinzufügen möchten.  
  
    ![Auswählen des hinzu zufügenden Datensatzes](../../media/Add-a-DNS-Resource-Record/ipam_DNSrr_04.jpg)  
  
7.  Geben Sie im **neuen Ressourcen Daten Satz** unter **Name**einen Namen für den Ressourcen Daten Satz ein. Geben Sie unter **IP-Adresse**eine IP-Adresse ein, und wählen Sie dann die Ressourcen Daten Satz Eigenschaften aus, die für Ihre Bereitstellung geeignet sind. Klicken Sie auf **Ressourcen Datensatz hinzufügen**.  
  
    ![Ressourcen Daten Satz hinzufügen](../../media/Add-a-DNS-Resource-Record/ipam_DNSrr_06.jpg)  
  
8.  Wenn Sie keine weiteren neuen Ressourcen Einträge erstellen möchten, klicken Sie auf **OK**. Wenn Sie zusätzliche neue Ressourcen Einträge erstellen möchten, klicken Sie auf **neu**.  
  
    ![Klicken Sie auf OK oder neu.](../../media/Add-a-DNS-Resource-Record/ipam_DNSrr_r2_01.jpg)
  
9. Das Dialogfeld wird erweitert, um einen **neuen Ressourcen Daten Satz**anzuzeigen. Klicken Sie auf **Ressourcen Daten Satz**. Die Liste der Ressourcen Daten Satz Typen wird angezeigt. Klicken Sie auf den Ressourcen Daten Satz, den Sie hinzufügen möchten.  
  
10. Geben Sie im **neuen Ressourcen Daten Satz** unter **Name**einen Namen für den Ressourcen Daten Satz ein. Geben Sie unter **IP-Adresse**eine IP-Adresse ein, und wählen Sie dann die Ressourcen Daten Satz Eigenschaften aus, die für Ihre Bereitstellung geeignet sind. Klicken Sie auf **Ressourcen Datensatz hinzufügen**.  
  
    ![Ressourcen Daten Satz hinzufügen](../../media/Add-a-DNS-Resource-Record/ipam_DNSrr_r2_02.jpg)  
  
11. Wenn Sie weitere Ressourcen Einträge hinzufügen möchten, wiederholen Sie den Vorgang zum Erstellen von Datensätzen. Wenn Sie mit dem Erstellen neuer Ressourcen Einträge abgeschlossen haben **, klicken Sie**auf übernehmen.  
  
    ![Erstellung des Ressourcen Datensatzes vervollständigen](../../media/Add-a-DNS-Resource-Record/ipam_DNSrr_r2_03.jpg)  
  
12. Im Dialogfeld **Ressourcen Eintrag hinzufügen** wird eine Zusammenfassung der Ressourcen Einträge angezeigt, während von IPAM die Ressourcen Einträge auf dem angegebenen DNS-Server erstellt werden. Wenn die Datensätze erfolgreich erstellt wurden, lautet der **Status** des Datensatzes " **erfolgreich**".  
  
    ![Additions Status aufzeichnen](../../media/Add-a-DNS-Resource-Record/ipam_DNSrr_r2_04.jpg)  
  
13. Klicken Sie auf **OK**.  
  
## <a name="see-also"></a>Weitere Informationen  
[Verwaltung von DNS-Ressourcen Einträgen](DNS-Resource-Record-Management.md)  
[Verwalten von IPAM](Manage-IPAM.md)  
  


