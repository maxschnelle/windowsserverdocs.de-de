---
title: Wiederherstellung der Active Directory-Gesamtstruktur - Entfernen des globalen Katalogs
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 60087a62-11e6-4750-a70e-510f35315688
ms.technology: identity-adfs
ms.openlocfilehash: b7da7c03cbae4691e8f902f1be0cb33c0c912248
ms.sourcegitcommit: 84a2bdcb92ba6af45781fab9727617e50fa5e911
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/07/2017
---
# <a name="ad-forest-recovery---removing-the-global-catalog"></a>Wiederherstellung des AD-Gesamtstruktur - Entfernen des globalen Katalogs  

>Gilt für: Windows Server2016, Windows Server2012 und 2012 R2, Windows Server2008 und 2008 R2

 Verwenden Sie das folgende Verfahren auf um den globalen Katalog von einem Domänencontroller zu entfernen.  
  
 Einen globaler Katalogserver aus einer Sicherung wiederherstellen kann dazu führen, dass im globalen Katalog neuere Daten für eines seiner teilweise Replikate als der entsprechenden Domäne, die für die Teilreplikat autorisierend ist. In diesem Fall die neueren Daten werden nicht aus dem globalen Katalog entfernt und möglicherweise auch auf anderen globalen Katalogserver repliziert werden. Daher sollten auch, wenn Sie einen Domänencontroller, der ein globaler Katalogserver, entweder versehentlich wurde wiederhergestellt wurde, oder da, die die einsame Sicherung wurde Sie als vertrauenswürdig eingestuft, Sie den globalen Katalog entfernen unmittelbar nach der Wiederherstellungsvorgang abgeschlossen ist. Wenn der globale Katalog entfernt wird, entfernt der Computer seine Teilreplikate.  
  
## <a name="to-remove-the-global-catalog-using-active-directory-sites-and-services"></a>So entfernen Sie den globalen Katalog mithilfe von Active Directory-Standorte und -Dienste  
 
1.  Öffnen Sie Server-Manager, klicken Sie auf **Tools**, und klicken Sie auf **Active Directory-Standorte und -Dienste**.  
2.  Erweitern Sie in der Konsolenstruktur der **Sites** Container, und wählen Sie dann den entsprechenden Standort mit dem Zielserver.  
3.  Erweitern Sie die **Server** Container, und erweitern Sie dann die *Server* -Objekt für den Domänencontroller, von dem der globale Katalog entfernt werden soll.  
4.  Mit der rechten Maustaste **NTDS-Einstellungsobjekt**, und klicken Sie dann auf **Eigenschaften**.  
5.  Deaktivieren der **globalen Katalog** Kontrollkästchen.  
![Entfernen des globalen Katalogs](media/AD-Forest-Recovery-Remove-GC/removegc1.png)
6.  Klicken Sie auf **gelten**.
  
## <a name="to-remove-the-global-catalog-using-repadmin"></a>So entfernen Sie den globalen Katalog mithilfe von Repadmin  
  
1.  Öffnen Sie ein Eingabeaufforderungsfenster mit erhöhten Rechten, geben Sie den folgenden Befehl, und drücken Sie die EINGABETASTE:  
  
    ```  
    repadmin.exe /options DC_NAME –IS_GC  
    ```  
  
 ## <a name="next-steps"></a>Nächste Schritte

- [AD-Gesamtstruktur für die Wiederherstellung](AD-Forest-Recovery-Guide.md)
- [Wiederherstellung der Active Directory-Gesamtstruktur - Verfahren](AD-Forest-Recovery-Procedures.md)
