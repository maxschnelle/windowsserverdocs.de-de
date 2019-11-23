---
title: 'AD-Gesamtstruktur Wiederherstellung: Hinzufügen der GC'
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server
ms.assetid: 5a291f65-794e-4fc3-996e-094c5845a383
ms.technology: identity-adds
ms.openlocfilehash: f82033dd042847c7c735423c25756b936b137230
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71369337"
---
# <a name="ad-forest-recovery---adding-the-gc"></a>AD-Gesamtstruktur Wiederherstellung: Hinzufügen der GC

>Gilt für: Windows Server 2016, Windows Server 2012 und 2012 R2, Windows Server 2008 und 2008 R2

Gehen Sie wie folgt vor, um den globalen Katalog einem DC hinzuzufügen.  
  
## <a name="to-add-the-global-catalog"></a>So fügen Sie den globalen Katalog hinzu  
  
1. Klicken Sie auf **Start**, zeigen Sie auf **Alle Programme**und auf **Verwaltung**, und klicken Sie dann auf **Active Directory Websites und Dienste**.  
2. Erweitern Sie in der Konsolen Struktur den Container **Standorte** , und wählen Sie dann den entsprechenden Standort aus, der den Zielserver enthält.  
3. Erweitern Sie den Container **Server** , und erweitern Sie dann das Server Objekt für den Domänen Controller, dem Sie den globalen Katalog hinzufügen möchten.  
4. Klicken Sie mit der rechten Maustaste auf **NTDS-Einstellungen**, und klicken Sie auf **Eigenschaften**.  
5. Aktivieren Sie das Kontrollkästchen **globaler Katalog** .  
![Hinzufügen von GC-](media/AD-Forest-Recovery-Add-GC/addgc1.png)

## <a name="to-add-the-global-catalog-using-repadmin"></a>So fügen Sie den globalen Katalog mithilfe von Repadmin hinzu  

- Öffnen Sie eine Eingabeaufforderung mit erhöhten Rechten, geben Sie folgenden Befehl ein, und drücken Sie die EINGABETASTE:  

   ```  
   repadmin.exe /options DC_NAME +IS_GC  
   ```  

Im folgenden finden Sie Möglichkeiten, den Prozess des Hinzufügens des globalen Katalogs zum DC in der Stamm Domäne zu beschleunigen:  

- Im Idealfall sollte der DC in der Stamm Domäne ein Replikations Partner der wiederhergestellten DCS in den nicht Stamm Domänen sein. Wenn dies der Fall ist, vergewissern Sie sich, dass die Konsistenzprüfung (KCC) das entsprechende **repsfrom** -Objekt für den Quell Domänen Controller und die Partition im Stamm-DC erstellt hat. Sie können dies überprüfen, indem Sie den Befehl **repadmin/showreps/v** ausführen. 

- Wenn kein **repsfrom** -Objekt erstellt wurde, erstellen Sie dieses Objekt für die Konfigurations Partition. Auf diese Weise kann der Domänen Controller in der Stamm Domäne ermitteln, welche DCS in der nicht Stamm Domäne gelöscht wurden. Dies können Sie mit den folgenden Befehlen erreichen:  

   ```
   repadmin /add ConfigurationNamingContext DestinationDomainController SourceDomainControllerCNAME  
   ```

   ```
   repadmin /options DSA -Disable_NTDSCONN_XLATE  
   ```

   Das Format für den *sourcedomaincontrollercname* lautet wie folgt:  

   ```
  
   sourceDCGuid._msdcs.root domain  
   ```

   Der Befehl repadmin/Add für die Konfigurations Partition der contoso.com-Domäne könnte beispielsweise wie folgt lauten:  

   ```
   repadmin /add cn=configuration,DC=contoso,DC=com DC01 937ef930-7356-43c8-88dc-8baaaa781cf6._msdcs.dDSP17A22.contoso.com  
   ```

- Wenn das **repsfrom** -Objekt vorhanden ist, versuchen Sie, den Domänen Controller in der Stamm Domäne mit dem DC in der nicht-Stamm Domäne wie folgt zu synchronisieren:  

   ```
   Repadmin /sync DomainNamingContext DestinationDomainController SourceDomainControllerGUID  
   ```

   Dabei ist *destinationdomaincontroller* der DC in der Stamm Domäne, und *sourcedomaincontroller* ist der wiederhergestellte Domänen Controller in der nicht-Stamm Domäne. 

- Der Stamm Domänen-DNS-Server sollte über die Alias Ressourcen Einträge (CNAME) für den Quell Domänen Controller verfügen. Stellen Sie sicher, dass die übergeordnete DNS-Zone Delegat-Ressourcen Einträge (Nameserver (NS) und Host (A)-Ressourcen Einträge) für die korrekten DCS (die DCS, die aus der Sicherung wieder hergestellt wurden) in der untergeordneten Zone enthält. 
- Stellen Sie sicher, dass der Domänen Controller in der Stamm Domäne die richtige Schlüsselverteilungscenter (KDC) in der nicht-Stamm Domäne kontaktiert. Um dies zu testen, geben Sie an der Eingabeaufforderung den folgenden Befehl ein, und drücken Sie dann die EINGABETASTE:  

   ```
   nltest /dsgetdc:nonroot domain name /KDC /Force  
   ```

## <a name="next-steps"></a>Nächste Schritte

- [Wiederherstellung der AD-Gesamtstruktur: Leitfaden](AD-Forest-Recovery-Guide.md)
- [Wiederherstellung der AD-Gesamtstruktur: Verfahren](AD-Forest-Recovery-Procedures.md)  
