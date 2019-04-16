---
title: "Wiederherstellung des AD-Gesamtstruktur - hinzufügen des globalen Katalogs"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 5a291f65-794e-4fc3-996e-094c5845a383
ms.technology: identity-adfs
ms.openlocfilehash: 3749fd99737f61c55871f613b9feaa21090d3bae
ms.sourcegitcommit: 84a2bdcb92ba6af45781fab9727617e50fa5e911
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/07/2017
---
# <a name="ad-forest-recovery---adding-the-gc"></a>Wiederherstellung des AD-Gesamtstruktur - hinzufügen des globalen Katalogs 

>Gilt für: Windows Server2016, Windows Server2012 und 2012 R2, Windows Server2008 und 2008 R2

 Verwenden Sie das folgende Verfahren auf einem Domänencontroller den globalen Katalog hinzugefügt.  
  
## <a name="to-add-the-global-catalog"></a>Hinzufügen des globalen Katalogs  
  
1.  Klicken Sie auf **starten**, zeigen Sie auf **alle Programme**, zeigen Sie auf **Verwaltung**, und klicken Sie dann auf **Active Directory-Standorte und -Dienste**.  
2.  Erweitern Sie in der Konsolenstruktur der **Sites** Container, und wählen Sie dann den entsprechenden Standort mit dem Zielserver.  
3.  Erweitern Sie die **Server** Container, und erweitern Sie dann das Serverobjekt für den Domänencontroller den globalen Katalog hinzugefügt werden soll.  
4.  Mit der rechten Maustaste **NTDS-Einstellungsobjekt**, und klicken Sie dann auf **Eigenschaften**.  
5.  Wählen Sie die **globalen Katalog** Kontrollkästchen.  
![Hinzufügen des globalen Katalogs](media/AD-Forest-Recovery-Add-GC/addgc1.png)
  
## <a name="to-add-the-global-catalog-using-repadmin"></a>Hinzufügen des globalen Katalogs mithilfe von Repadmin  
  
1.  Öffnen Sie ein Eingabeaufforderungsfenster mit erhöhten Rechten, geben Sie den folgenden Befehl, und drücken Sie die EINGABETASTE:  
  
    ```  
    repadmin.exe /options DC_NAME +IS_GC  
    ```  
  
 Im folgenden sind Möglichkeiten zum Beschleunigen der Domänencontroller in der Stammdomäne den globalen Katalog hinzugefügt:  
  
-   Im Idealfall sollte der Domänencontroller in der Stammdomäne Replikationspartner für die wiederhergestellten Domänencontroller in der Nicht-Stamm-Domänen. Wenn dies der Fall ist, stellen Sie sicher, dass die Konsistenzprüfung (KCC) die entsprechende erstellt hat **RepsFrom** -Objekt für den Quelldomänencontroller und im Stammverzeichnis DC-Partition. Sie können dies überprüfen, indem Sie mit der **Repadmin /showreps /v** Befehl.  
  
-   Es ist keine **RepsFrom** Objekt erstellt, dieses Objekt der Konfigurationspartition. Auf diese Weise kann der Domänencontroller in der Stammdomäne bestimmen, welche Domänencontroller in der Stammdomäne gelöscht wurden. Sie erreichen dies mit den folgenden Befehlen:  
  
    ```  
    repadmin /add ConfigurationNamingContext DestinationDomainController SourceDomainControllerCNAME  
    ```  
  
    ```  
    repadmin /options DSA -Disable_NTDSCONN_XLATE  
    ```  
  
     Das Format für die *SourceDomainControllerCNAME* ist:  
  
    ```  
  
    sourceDCGuid._msdcs.root domain  
    ```  
  
     Beispielsweise kann der Befehl Repadmin /add der Konfigurationspartition von der Domäne contoso.com sein:  
  
    ```  
    repadmin /add cn=configuration,DC=contoso,DC=com DC01 937ef930-7356-43c8-88dc-8baaaa781cf6._msdcs.dDSP17A22.contoso.com  
    ```  
  
-   Wenn die **RepsFrom** Objekt vorhanden ist, wird der Domänencontroller in der Stammdomäne mit dem Domänencontroller in der Stammdomäne wie folgt synchronisieren:  
  
    ```  
    Repadmin /sync DomainNamingContext DestinationDomainController SourceDomainControllerGUID  
    ```  
  
     Wo *DestinationDomainController* ist der Domänencontroller in der Stammdomäne und *SourceDomainController* ist der wiederhergestellten Domänencontroller in der Stammdomäne.  
  
-   Der Stamm-Domäne-DNS-Server müssen die Alias (CNAME)-Ressourceneinträge für die Quell-DC. Stellen Sie sicher, dass die übergeordneten DNS-Zone enthält Delegierung-Ressourceneinträgen (Namenserver (NS) und Hostressourceneinträge (A)) für die richtige Domänencontroller (DCs, die aus einer Sicherung wiederhergestellt wurden) in die untergeordnete Zone.  
  
-   Stellen Sie sicher, dass der Domänencontroller in der Stammdomäne Kontakt mit den richtigen Key Distribution Center (KDC) in der Stammdomäne. Um, an der Eingabeaufforderung zu testen, geben Sie den folgenden Befehl, und drücken Sie dann die EINGABETASTE:  
  
    ```  
    nltest /dsgetdc:nonroot domain name /KDC /Force  
    ```  
## <a name="next-steps"></a>Nächste Schritte

- [AD-Gesamtstruktur für die Wiederherstellung](AD-Forest-Recovery-Guide.md)
- [Wiederherstellung der Active Directory-Gesamtstruktur - Verfahren](AD-Forest-Recovery-Procedures.md)  
