---
title: Wiederherstellung der AD-Gesamtstruktur – Entfernen des globalen Katalogs
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 60087a62-11e6-4750-a70e-510f35315688
ms.technology: identity-adds
ms.openlocfilehash: d730ce65fc179aee6a98f7cfc1a5b693bfcd6c93
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59817071"
---
# <a name="ad-forest-recovery---removing-the-global-catalog"></a>AD-Gesamtstruktur-Wiederherstellung: Entfernen des globalen Katalogs  

>Gilt für: Windows Server 2016, Windows Server 2012 und 2012 R2, Windows Server 2008 und 2008 R2

 Verwenden Sie das folgende Verfahren, um den globalen Katalog von einem Domänencontroller zu entfernen. 
  
 Wiederherstellen von einem globalen Katalogserver aus einer Sicherung kann im globalen Katalog enthält neuere Daten für eine ihrer partiellen Replikate nicht mit der entsprechenden Domäne, die für dieses Replikat autorisierend ist führen. In diesem Fall wird die neuere Daten nicht aus dem globalen Katalog entfernt und möglicherweise sogar auf anderen globalen Katalogserver repliziert. Daher sollten auch, wenn Sie einen Domänencontroller, der entweder ein globaler Katalogserver, versehentlich wurde wiederhergestellt wurde oder das einzelne Sicherung war Sie als vertrauenswürdig eingestuft, Sie den globalen Katalog entfernen sobald der Wiederherstellungsvorgang abgeschlossen ist. Wenn der globale Katalog entfernt wird, entfernt der Computer seine Teilreplikate. 
  
## <a name="to-remove-the-global-catalog-using-active-directory-sites-and-services"></a>So entfernen Sie den globalen Katalog mithilfe der Active Directory-Standorte und-Dienste  
 
1. Öffnen Sie Server-Manager, klicken Sie auf **Tools** , und klicken Sie auf **Active Directory-Standorte und-Dienste**. 
2. Erweitern Sie in der Konsolenstruktur der **Websites** Container, und wählen Sie dann den entsprechenden Standort an, die den Zielserver enthält. 
3. Erweitern Sie die **Server** Container, und erweitern Sie dann die *Server* Objekt für den DC, der von dem der globale Katalog entfernt werden sollen. 
4. Mit der rechten Maustaste **NTDS-Einstellungen**, und klicken Sie dann auf **Eigenschaften**. 
5. Deaktivieren der **globalen Katalog** Kontrollkästchen. 
   ![Entfernen von GC](media/AD-Forest-Recovery-Remove-GC/removegc1.png)
6. Klicken Sie auf **Übernehmen**.
  
## <a name="to-remove-the-global-catalog-using-repadmin"></a>So entfernen Sie den globalen Katalog mit Repadmin  
  
Öffnen Sie eine Eingabeaufforderung mit erhöhten Rechten, geben Sie den folgenden Befehl, und drücken Sie die EINGABETASTE:  

   ```
   repadmin.exe /options DC_NAME –IS_GC  
   ```  

## <a name="next-steps"></a>Nächste Schritte

- [Für die Wiederherstellung des AD-Gesamtstruktur](AD-Forest-Recovery-Guide.md)
- [Wiederherstellung der Gesamtstruktur der Active Directory - Prozeduren](AD-Forest-Recovery-Procedures.md)
