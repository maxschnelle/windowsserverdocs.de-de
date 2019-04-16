---
title: Umstellung von Windows Server Essentials auf Windows Server2012 R2 Standard
description: Beschreibt, wie Sie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a14689e3-2310-4229-bd3e-dafc0e739e02
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: d371e24b17310c0687666185f56fe07a135ff91f
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="transition-from-windows-server-essentials-to-windows-server-2012-r2-standard"></a>Umstellung von Windows Server Essentials auf Windows Server2012 R2 Standard

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials

Windows Server2016 ist die Cloud bereit, die Ihre aktuellen Arbeitslasten und führt gleichzeitig neue Technologien, die für den Übergang für Cloud computing vereinfachen unterstützt. Windows Server2016-Inhalte können Sie vorzubereiten.

 Windows Server Essentials unterstützt bis zu 25 Benutzer und 50 Geräte. Wenn Ihre geschäftliche Anforderungen diese Begrenzung überschreiten, können Sie eine direkte lizenzumstellung von Windows Server Essentials zu Windows Server2012 R2 Standard, lizenzvorschriften ausführen.  
  
 Nach der Windows Server2012 R2 Standard Umstellung, werden die Benutzerkonten- und gerätebegrenzungen zwar entfernt, aber die Features, die speziell für Windows Server Essentials (z.B. das Dashboard, Remotewebzugriff und clientcomputersicherung) weiterhin verfügbar. Technischer Einschränkungen für diese Features unterstützt jedoch höchstens 100 Benutzerkonten und 200 Geräten. Die Sicherungsfunktion für Clientcomputer wird die Sicherung von bis zu 75 Geräten unterstützen.  
  
> [!IMPORTANT]
>   Windows Server2012 R2 Standard erfordert eine Clientzugriffslizenz (CAL) für jeden Benutzer oder Geräte in Ihrer Umgebung. Dies unterscheidet sich von Windows Server Essentials, die die CAL-Modell nicht verwendet und kommt nicht keine Clientzugriffslizenzen. Bei der Windows Server Essentials auf Windows Server2012 R2 Standard Umstellung, müssen Sie die entsprechende Anzahl und Typ der Clientzugriffslizenzen für Ihre Umgebung (die meisten Kunden erwerben Benutzer-CALs) erwerben.  
  
## <a name="before-the-transition"></a>Vor der Umstellung  
  
-   Vor der Umstellung von Windows Server Essentials auf Windows Server2012 R2 Standard, sollten Sie vollständig die Serverdaten sichern.  
  
    > [!IMPORTANT]
    >  Sie können nicht ohne eine vollständige Sicherung des Servers den Server in den Zustand wiederherstellen, in dem vor der Umstellung.  
  
-   Stellen Sie außerdem sicher, dass Sie lesen und der Endbenutzer-Lizenzvertrag (EULA) für Windows Server2012 R2 Standard verstehen. So zeigen Sie den Endbenutzer-Lizenzvertrag an  
  
    1.  Öffnen Sie ein Eingabeaufforderungsfenster als Administrator.  
  
    2.  Führen Sie den folgenden Befehl ein:  
  
         **DISM /online /set-edition: ServerStandard /geteula:***Eula Path* (wobei *Eula Path* den Speicherort darstellt, dem Sie die EULA-Datei speichern möchten, zum Beispiel: C:\ws8std_eula.rtf). Achten Sie darauf, RTF als die Dateierweiterung zu verwenden.  
  
    3.  Öffnen Sie den Speicherort der Datei, und doppelklicken Sie dann auf die Datei, um es zu öffnen.  
  
## <a name="transition-to--windows-server-2012-r2-standard"></a>Wechsel zu Windows Server2012 R2 Standard  
 Nachdem Sie entschieden haben, für den Übergang Windows Server Essentials zu Windows Server2012 R2 Standard, vollständige diese beiden Schritteaus:  
  
1.  Erwerben einer Lizenz für Windows Server2012 R2 Standard und die entsprechende Anzahl an Benutzer- und/oder Geräte-Clientzugriffslizenzen für Ihre Umgebung.  
  
     Sie können eine Lizenz für Windows Server2012 R2 Standard erwerben, über einen Vertragshändler, einen Distributor oder mithilfe einer [Microsoft-Partner](https://pinpoint.microsoft.com/SelectCulture.aspx).  
  
    > [!NOTE]
    >  Wenn Sie Windows Server2012 R2 Standard ursprünglich erworben und Ihre Herabstufungsrechte für eine Ihrer beiden virtuellen Instanzen als Windows Server Essentials installieren ausgeübt, brauchen Sie keine zusätzlichen Lizenzen erwerben.  
    >   
    >  Wenn Sie Windows Server2012 R2 Standard über den volumenlizenzkanal erwerben, können Sie ein ISO-Abbild und einen Product Key für Windows Server2012 R2 Standard vom Volume Licensing Service Center (VLSC) herunterladen.  
    >   
    >  Wenn Sie Windows Server2012 R2 Standard über einen anderen Kanal erwerben, können Sie herunterladen ein ISO-Abbild und einen evaluierungs-Product Key für Windows Server Essentials aus der [TechNet Evaluation Center](https://technet.microsoft.com/evalcenter/jj659306.aspx). Den Übergang durchführen, wie im nächsten Schrittbeschrieben wird das evaluierungsprodukt in ein vollständig lizenziertes und unterstütztes Produkt umgewandelt.  
  
2.  Öffnen Sie Windows PowerShell als Administrator, und führen Sie den folgenden Befehl:  
  
     **DISM /online /set-edition: ServerStandard /accepteula /productkey:***Product Key* (wobei *Product Key* ist der Product Key für Ihre Kopie von Windows Server2012 R2 Standard).  
  
     Der Server wird neu gestartet, um den Umstellungsprozess fertigzustellen.  
  
 Nach der Umstellung sind die Windows Server Essentials-Funktionen bleiben auf dem Server und werden für bis zu 100 Benutzern und 200 Geräte unterstützt.  
  
## <a name="see-also"></a>Siehe auch  
  

-   [Migrieren von Serverdaten zu Windows Server Essentials](Migrate-Server-Data-to-Windows-Server-Essentials.md)

-   [Migrieren von Serverdaten zu Windows Server Essentials](../migrate/Migrate-Server-Data-to-Windows-Server-Essentials.md)

