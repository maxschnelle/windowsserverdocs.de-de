---
title: 'AD-Gesamtstruktur Wiederherstellung: Entfernen des globalen Katalogs'
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server
ms.assetid: 60087a62-11e6-4750-a70e-510f35315688
ms.technology: identity-adds
ms.openlocfilehash: 3ba1336828ad6031ce7fb47a659d084494466e4a
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71409098"
---
# <a name="ad-forest-recovery---removing-the-global-catalog"></a>AD-Gesamtstruktur Wiederherstellung: Entfernen des globalen Katalogs  

>Gilt für: Windows Server 2016, Windows Server 2012 und 2012 R2, Windows Server 2008 und 2008 R2

 Verwenden Sie das folgende Verfahren, um den globalen Katalog von einem DC zu entfernen. 
  
 Wenn Sie einen globalen Katalogserver aus einer Sicherung wiederherstellen, kann dies dazu führen, dass der globale Katalog neuere Daten für eines seiner partiellen Replikate enthält als die entsprechende Domäne, die für dieses partielle Replikat In einem solchen Fall werden die neueren Daten nicht aus dem globalen Katalog entfernt und können sogar auf andere globale Katalogserver repliziert werden. Daher sollten Sie den globalen Katalog kurz nach Abschluss des Wiederherstellungs Vorgangs entfernen, auch wenn Sie einen Domänen Controller wieder hergestellt haben, der ein globaler Katalogserver war, entweder versehentlich oder weil es sich dabei um die alleinige vertrauenswürdige Sicherung handelt. Beim Entfernen des globalen Katalogs entfernt der Computer alle Teil Replikate. 
  
## <a name="to-remove-the-global-catalog-using-active-directory-sites-and-services"></a>So entfernen Sie den globalen Katalog mithilfe Active Directory Standorte und Dienste  
 
1. Öffnen Sie Server-Manager, klicken Sie auf Extras **, und klicken Sie auf** **Active Directory Websites und Dienste**. 
2. Erweitern Sie in der Konsolen Struktur den Container **Standorte** , und wählen Sie dann den entsprechenden Standort aus, der den Zielserver enthält. 
3. Erweitern Sie den Container **Server** , und erweitern Sie dann das *Server* Objekt für den Domänen Controller, von dem aus Sie den globalen Katalog entfernen möchten. 
4. Klicken Sie mit der rechten Maustaste auf **NTDS-Einstellungen**, und klicken Sie auf **Eigenschaften**. 
5. Deaktivieren Sie das Kontrollkästchen **globaler Katalog** . 
   ![remove GC @ no__t-1
6. Klicken Sie auf **Übernehmen**.
  
## <a name="to-remove-the-global-catalog-using-repadmin"></a>So entfernen Sie den globalen Katalog mithilfe von "repadmin"  
  
Öffnen Sie eine Eingabeaufforderung mit erhöhten Rechten, geben Sie folgenden Befehl ein, und drücken Sie die EINGABETASTE:  

   ```
   repadmin.exe /options DC_NAME –IS_GC  
   ```  

## <a name="next-steps"></a>Nächste Schritte

- [Wiederherstellung der AD-Gesamtstruktur: Leitfaden](AD-Forest-Recovery-Guide.md)
- [Wiederherstellung der AD-Gesamtstruktur: Verfahren](AD-Forest-Recovery-Procedures.md)
