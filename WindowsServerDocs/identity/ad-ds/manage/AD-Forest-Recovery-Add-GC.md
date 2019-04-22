---
title: 'AD-Gesamtstruktur-Wiederherstellung: Hinzufügen von der Garbage Collector'
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 5a291f65-794e-4fc3-996e-094c5845a383
ms.technology: identity-adds
ms.openlocfilehash: 156a4a64d9c3bb8261bd603b72ae11b81ff1d152
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59825631"
---
# <a name="ad-forest-recovery---adding-the-gc"></a>AD-Gesamtstruktur-Wiederherstellung: Hinzufügen von der Garbage Collector

>Gilt für: Windows Server 2016, Windows Server 2012 und 2012 R2, Windows Server 2008 und 2008 R2

Verwenden Sie das folgende Verfahren, um an einem Domänencontroller der globale Katalog hinzugefügt.  
  
## <a name="to-add-the-global-catalog"></a>Den globalen Katalog hinzufügen  
  
1. Klicken Sie auf **starten**, zeigen Sie auf **Programme**, zeigen Sie auf **Verwaltung**, und klicken Sie dann auf **Active Directory-Standorte und-Dienste**.  
2. Erweitern Sie in der Konsolenstruktur der **Websites** Container, und wählen Sie dann den entsprechenden Standort an, die den Zielserver enthält.  
3. Erweitern Sie die **Server** Container, und erweitern Sie dann das Serverobjekt für den DC, der in der globale Katalog hinzugefügt werden soll.  
4. Mit der rechten Maustaste **NTDS-Einstellungen**, und klicken Sie dann auf **Eigenschaften**.  
5. Wählen Sie die **globalen Katalog** Kontrollkästchen.  
![Hinzufügen von GC](media/AD-Forest-Recovery-Add-GC/addgc1.png)

## <a name="to-add-the-global-catalog-using-repadmin"></a>Den globalen Katalog mithilfe von Repadmin hinzufügen  

- Öffnen Sie eine Eingabeaufforderung mit erhöhten Rechten, geben Sie den folgenden Befehl, und drücken Sie die EINGABETASTE:  

   ```  
   repadmin.exe /options DC_NAME +IS_GC  
   ```  

Im folgenden finden Möglichkeiten, um den Prozess des Hinzufügens des globalen Katalogs auf den DC in der Stammdomäne zu beschleunigen:  

- Im Idealfall sollte der Domänencontroller in der Stammdomäne einen Replikationspartner der wiederhergestellten Domänencontroller in der nicht-Root-Domäne sein. Wenn dies der Fall ist, vergewissern Sie sich, dass die Konsistenzprüfung (KCC) die entsprechende erstellt hat **RepsFrom** Objekt für die Quell-DC und die Partition im Stammverzeichnis DC. Sie können dies nachprüfen, indem Sie Ausführung der **Repadmin/showreps/v** Befehl. 

- Es ist keine **RepsFrom** Objekt erstellt haben, erstellen Sie dieses Objekt für die Konfigurationspartition. Auf diese Weise kann der Domänencontroller in der Stammdomäne bestimmen, welche DCs in der nicht-Root-Domäne gelöscht wurden. Dies können Sie die folgenden Befehle verwenden:  

   ```
   repadmin /add ConfigurationNamingContext DestinationDomainController SourceDomainControllerCNAME  
   ```

   ```
   repadmin /options DSA -Disable_NTDSCONN_XLATE  
   ```

   Das Format für die *SourceDomainControllerCNAME* ist:  

   ```
  
   sourceDCGuid._msdcs.root domain  
   ```

   Z. B. das Repadmin / Befehl hinzufügen, für die Konfigurationspartition der Domäne "contoso.com" sein kann:  

   ```
   repadmin /add cn=configuration,DC=contoso,DC=com DC01 937ef930-7356-43c8-88dc-8baaaa781cf6._msdcs.dDSP17A22.contoso.com  
   ```

- Wenn die **RepsFrom** Objekt vorhanden ist, wird versuchen, den DC in der Stammdomäne mit dem Domänencontroller in der nicht-Root-Domäne zu synchronisieren, wie folgt:  

   ```
   Repadmin /sync DomainNamingContext DestinationDomainController SourceDomainControllerGUID  
   ```

   Wo *DestinationDomainController* ist der Domänencontroller in der Stammdomäne und *SourceDomainController* wird der wiederhergestellte DC in der nicht-Root-Domäne. 

- Der Root-Domain-DNS-Server müssen die Aliasressourceneintrags (CNAME)-Ressourceneinträge für die Quell-DC an. Stellen Sie sicher, dass die übergeordneten DNS-Zone Delegation-Ressourceneinträgen (Namenserver (NS) und Hostressourceneinträge (A)) für die richtigen Domänencontroller (DCs, die aus einer Sicherung wiederhergestellt wurden) enthält, in der untergeordneten Zone. 
- Stellen Sie sicher, dass der Domänencontroller in der Stammdomäne der richtige Schlüssel Verteilung Schlüsselverteilungscenter (KDC) in der Stammdomäne Kontakt aufnimmt. Um dies an der Eingabeaufforderung zu testen, geben Sie den folgenden Befehl, und drücken Sie dann die EINGABETASTE:  

   ```
   nltest /dsgetdc:nonroot domain name /KDC /Force  
   ```

## <a name="next-steps"></a>Nächste Schritte

- [Für die Wiederherstellung des AD-Gesamtstruktur](AD-Forest-Recovery-Guide.md)
- [Wiederherstellung der Gesamtstruktur der Active Directory - Prozeduren](AD-Forest-Recovery-Procedures.md)  
