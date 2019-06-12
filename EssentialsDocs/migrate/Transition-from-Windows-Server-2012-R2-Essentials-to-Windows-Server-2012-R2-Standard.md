---
title: Umstellung von Windows Server Essentials auf Windows Server 2012 R2 Standard
description: Beschreibt, wie Windows Server Essentials
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
ms.openlocfilehash: ca36533af169c899865789f153960bf5f0dda684
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66432552"
---
# <a name="transition-from-windows-server-essentials-to-windows-server-2012-r2-standard"></a>Umstellung von Windows Server Essentials auf Windows Server 2012 R2 Standard

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Windows Server 2016 ist das bereit für Cloud-Betriebssystem, das Ihre aktuellen Workloads unterstützt, bei der Einführung neuer Technologies, die für den Übergang zum Cloudcomputing zu erleichtern. Windows Server 2016-Inhalts hilft Ihnen beim bereit.

 Windows Server Essentials unterstützt bis zu 25 Benutzern und 50 Geräten. Wenn Sie Ihre geschäftliche Anforderungen diese Begrenzung überschreiten, können Sie eine direkte lizenzumstellung von Windows Server Essentials auf Windows Server 2012 R2 Standard um die lizenzvorschriften weiterhin zu erfüllen ausführen.  
  
 Nach dem Wechsel zu Windows Server 2012 R2 Standard, werden die Benutzerkonten- und gerätebegrenzungen zwar entfernt, aber die Funktionen, die in Windows Server Essentials (z. B. das Dashboard, Remotewebzugriff und clientcomputersicherung) sind weiterhin verfügbar. Aufgrund technischer Einschränkungen für diese Funktionen werden jedoch höchstens 100 Benutzerkonten und 200 Geräte unterstützt. Die Sicherungsfunktion für Clientcomputer wird die Sicherung von bis zu 75 Geräten unterstützen.  
  
> [!IMPORTANT]
>   Windows Server 2012 R2 Standard erfordert eine Clientzugriffslizenz (CAL) für jeden Benutzer und Gerät in Ihrer Umgebung. Dies unterscheidet sich von Windows Server Essentials, die das CAL-Modell nicht verwendet und keine Clientzugriffslizenzen enthalten sind. Wenn von Windows Server Essentials in Windows Server 2012 R2 Standard zu übergeht, müssen Sie die entsprechende Anzahl und Typ der Clientzugriffslizenzen für Ihre Umgebung (die meisten Kunden erwerben Benutzer-CALs) zu erwerben.  
  
## <a name="before-the-transition"></a>Vor der Umstellung  
  
-   Vor der Umstellung von Windows Server Essentials auf Windows Server 2012 R2 Standard, sollten Sie vollständige Serverdaten Sicherung.  
  
    > [!IMPORTANT]
    >  Ohne eine vollständige Sicherung des Servers kann der Zustand des Servers vor der Umstellung nicht wiederhergestellt werden.  
  
-   Stellen Sie außerdem sicher, dass Sie lesen und der Endbenutzer-Lizenzvertrag (EULA) für Windows Server 2012 R2 Standard verstehen. So zeigen Sie die EULA an:  
  
    1.  Öffnen Sie ein Befehlsfenster als Administrator.  
  
    2.  Führen Sie den folgenden Befehl aus:  
  
         **DISM / online/Set-Edition: Serverstandard / geteula:** *Eula Path* (wobei *Eula Path* stellt den Speicherort, zu dem Sie die EULA-Datei speichern möchten z. B.: C:\ws8std_eula.rtf). Achten Sie darauf, RTF als Dateierweiterung zu verwenden.  
  
    3.  Navigieren Sie zum Speicherort der Datei, und doppelklicken Sie darauf, um sie zu öffnen.  
  
## <a name="transition-to--windows-server-2012-r2-standard"></a>Umstellung auf Windows Server 2012 R2 Standard  
 Nachdem Sie entschieden haben, die von Windows Server Essentials auf Windows Server 2012 R2 Standard, vollständig durch diese beiden Schritte übergehen:  
  
1. Erwerben einer Lizenz für Windows Server 2012 R2 Standard und die entsprechende Anzahl an Benutzer- und/oder Geräte-Clientzugriffslizenzen für Ihre Umgebung an.  
  
    Sie können eine Lizenz für Windows Server 2012 R2 Standard erwerben, über einen Vertragshändler, einen Verteiler oder mit Hilfe von einem [Microsoft-Partner](https://pinpoint.microsoft.com/SelectCulture.aspx).  
  
   > [!NOTE]
   >  Wenn Sie Windows Server 2012 R2 Standard ursprünglich erworben und Ihre Herabstufungsrechte eine Ihrer beiden virtuellen Instanzen als Windows Server Essentials installieren, müssen Sie nicht keine zusätzlichen Lizenzen erwerben.  
   >   
   >  Wenn Sie Windows Server 2012 R2 Standard über den volumenlizenzkanal erwerben, können Sie ein ISO-Abbild und einen Product Key für Windows Server 2012 R2 Standard vom Volume Licensing Service Center (VLSC) herunterladen.  
   >   
   >  Wenn Sie Windows Server 2012 R2 Standard über einen anderen Kanal erwerben, Sie können ein ISO-Abbild und einen evaluierungs-Product Key für Windows Server Essential aus dem [TechNet Evaluation Center](https://technet.microsoft.com/evalcenter/jj659306.aspx). Durch das Ausführen der Umstellung gemäß der Beschreibung im folgenden Schritt wird das Evaluierungsprodukt in ein vollständig lizenziertes und unterstütztes Produkt umgewandelt.  
  
2. Öffnen Sie Windows PowerShell als Administrator, und führen Sie dann den folgenden Befehl aus:  
  
    **dism /online /set-edition:ServerStandard /accepteula /productkey:** *Produktschlüssel* (wobei *Product Key* ist der Product Key für Ihre Kopie von Windows Server 2012 R2 Standard).  
  
    Der Server wird neu gestartet, um den Umstellungsprozess fertigzustellen.  
  
   Nach der Umstellung sind die Windows Server Essentials-Funktionen weiterhin auf dem Server und werden für bis zu 100 Benutzern und 200 Geräte unterstützt.  
  
## <a name="see-also"></a>Siehe auch  
  

-   [Migrieren von Serverdaten zu Windows Server Essentials](Migrate-Server-Data-to-Windows-Server-Essentials.md)

-   [Migrieren von Serverdaten zu Windows Server Essentials](../migrate/Migrate-Server-Data-to-Windows-Server-Essentials.md)

