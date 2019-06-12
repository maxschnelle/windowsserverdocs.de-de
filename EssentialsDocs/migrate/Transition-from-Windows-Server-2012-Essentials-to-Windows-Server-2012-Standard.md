---
title: Umstellung von Windows Server Essentials auf Windows Server 2012 Standard
description: Beschreibt, wie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 51bcf124-c215-4e9d-9fa8-a90fa2c2fa22
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 445472822de09263b84821e552c931ca19f14b2b
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66432534"
---
# <a name="transition-from-windows-server-essentials-to-windows-server-2012-standard"></a>Umstellung von Windows Server Essentials auf Windows Server 2012 Standard

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

 Windows Server® 2012 Essentials unterstützt bis zu 25 Benutzern und 50 Geräten. Wenn Sie Ihre geschäftliche Anforderungen diese Begrenzung überschreiten, können Sie eine direkte lizenzumstellung von Windows Server Essentials auf Windows Server 2012 Standard, um die lizenzvorschriften weiterhin zu erfüllen ausführen.  
  
## <a name="how-the-transition-affects-user-and-device-limits"></a>So wirkt sich die Umstellung auf Benutzer- und Gerätebegrenzungen aus  
 Nach dem Wechsel zu Windows Server 2012 Standard, werden die Benutzerkonten- und gerätebegrenzungen zwar entfernt, aber die Funktionen, die in Windows Server Essentials (z. B. das Dashboard, Remotewebzugriff und clientcomputersicherung), sind weiterhin verfügbar. Aufgrund technischer Einschränkungen für diese Funktionen werden jedoch höchstens 75 Benutzerkonten und 75 Geräte unterstützt. Wenn es mehr als 75 Benutzerkonten oder Geräte hinzugefügt wird, sollten Sie die Windows Server Essentials-Funktionen deaktivieren und verwenden Sie die Windows Server 2012 Standard systemeigene Tools zum Verwalten von Benutzerkonten und Geräten.  
  
> [!IMPORTANT]
>   Windows Server 2012 Standard erfordert eine Clientzugriffslizenz (CAL) für jeden Benutzer und Gerät in Ihrer Umgebung. Dies unterscheidet sich von Windows Server Essentials, die das CAL-Modell nicht verwendet und keine Clientzugriffslizenzen enthalten sind.  Wenn von Windows Server Essentials in Windows Server 2012 Standard zu übergeht, müssen Sie die entsprechende Anzahl und Typ der Clientzugriffslizenzen für Ihre Umgebung (die meisten Kunden erwerben Benutzer-CALs) zu erwerben.  
  
## <a name="before-the-transition"></a>Vor der Umstellung  
  
-   Vor der Umstellung von Windows Server Essentials auf Windows Server 2012 Standard, sollten Sie vollständige Serverdaten Sicherung.  
  
    > [!IMPORTANT]
    >  Ohne eine vollständige Sicherung des Servers kann der Zustand des Servers vor der Umstellung nicht wiederhergestellt werden.  
  
-   Stellen Sie außerdem sicher, dass Sie lesen und der Endbenutzer-Lizenzvertrag (EULA) für Windows Server 2012 Standard verstehen. So zeigen Sie die EULA an:  
  
    1.  Öffnen Sie ein Befehlsfenster als Administrator.  
  
    2.  Führen Sie den folgenden Befehl aus:  
  
         **dism /online /set-edition:ServerStandard /geteula: eula path**  
  
         Dabei steht **eula path** für den Speicherort, an dem die EULA-Datei gespeichert werden soll. Beispiel: C:\ws8std_eula.rtf.  Achten Sie darauf, RTF als Dateierweiterung zu verwenden.  
  
    3.  Navigieren Sie zum Speicherort der Datei, und doppelklicken Sie darauf, um sie zu öffnen.  
  
## <a name="transition-to--windows-server-2012-standard"></a>Übergang zu Windows Server 2012 Standard  
 Nachdem Sie entschieden haben, die von Windows Server Essentials auf Windows Server 2012 Standard, vollständig durch diese beiden Schritte übergehen:  
  
1. Erwerben einer Lizenz für Windows Server 2012 Standard und die entsprechende Anzahl an Benutzer- und/oder Geräte-Clientzugriffslizenzen für Ihre Umgebung an.  
  
    Sie können eine Lizenz für Windows Server 2012 Standard erwerben, über einen Vertragshändler, einen Verteiler oder mit Hilfe von einem [Microsoft-Partner](https://pinpoint.microsoft.com/SelectCulture.aspx).  
  
   > [!NOTE]
   >  Wenn Sie Windows Server 2012 Standard ursprünglich erworben und Ihre Herabstufungsrechte eine Ihrer beiden virtuellen Instanzen als Windows Server Essentials installieren, müssen Sie nicht keine zusätzlichen Lizenzen erwerben.  
   >   
   >  Wenn Sie Windows Server 2012 Standard über den volumenlizenzkanal erwerben, können Sie ein ISO-Abbild und einen Product Key für Windows Server 2012 Standard vom Volume Licensing Service Center (VLSC) herunterladen.  
   >   
   >  Wenn Sie Windows Server 2012 Standard über einen anderen Kanal erwerben können ein ISO-Abbild und einen evaluierungs-Product Key für Windows Server Essential aus dem [TechNet Evaluation Center](https://technet.microsoft.com/evalcenter/jj659306.aspx). Durch das Ausführen der Umstellung gemäß der Beschreibung im folgenden Schritt wird das Evaluierungsprodukt in ein vollständig lizenziertes und unterstütztes Produkt umgewandelt.  
  
2. Öffnen Sie Windows PowerShell als Administrator, und führen Sie dann den folgenden Befehl aus.  
  
    **dism /online /set-edition:ServerStandard /accepteula /productkey:** *Product Key*  
  
    Wo *Product Key* ist der Product Key für Ihre Kopie von Windows Server 2012 Standard.  
  
    Der Server wird neu gestartet, um den Umstellungsprozess fertigzustellen.  
  
   Nach der Umstellung sind die Windows Server Essentials-Funktionen weiterhin auf dem Server und werden für bis zu 75 Benutzer und 75 Geräte unterstützt. Wenn Sie eine dieser Begrenzungen überschreiten, sollten Sie die Windows Server 2012 Standard systemeigenen Tools zum Verwalten von Benutzerkonten und Geräten verwenden.  
  
   Nach dem Wechsel zu Windows Server 2012 Standard sind der Medienfunktionen von Windows Server Essentials darüber hinaus nicht mehr verfügbar. Dazu zählen die Medienfunktionen des Remotewebzugriffs sowie die Medieneinstellungen auf dem Dashboard.  
  
## <a name="turn-off--windows-server-essentials-features"></a>Deaktivieren Sie Windows Server Essentials-Funktionen  
 Wenn Sie Windows Server Essentials-Dashboard oder andere Zusatzfunktionen zum Verwalten des Servers nicht mehr benötigen, können Sie die Funktionen deaktivieren und entfernen sie von Ihrem Server.  
  
 Die **Assistent für Windows Server Essentials-Funktionen deaktivieren** hilft Ihnen, die Funktionen zu deinstallieren. Er bereinigt auch den Server von Dateien, die von der Windows Server Essentials-Server-Software erstellt wurden.  Einige Bereinigungsoptionen werden sofort ausgeführt, während andere nach einem Neustart des Servers initiiert werden.  
  
 Die **Assistent für Windows Server Essentials-Funktionen deaktivieren** erfordert, dass Sie alle add-ins manuell deinstallieren, bevor der Assistent fertiggestellt werden kann. Zum Anzeigen einer Liste der installierten Add-Ins öffnen Sie im Dashboard die Anwendungsseite. Wenn der Assistent installierte Add-Ins ermittelt werden Sie benachrichtigt und aufgefordert, diese zu deinstallieren.  
  
 Die **Assistent für Windows Server Essentials-Funktionen deaktivieren** ermöglicht es Ihnen zu entscheiden, ob Sicherungsdateien für den Client Computer, die nach dem Deaktivieren der Windows Server Essentials-Funktionen zu halten.  
  
 Es gibt zwei Möglichkeiten zum Ausführen der **Assistent für Windows Server Essentials-Funktionen deaktivieren** über das Dashboard:  
  
#### <a name="from-the-alert"></a>In der Warnmeldung  
  
1.  Öffnen Sie im Dashboard die Meldungsanzeige.  
  
2.  Wählen Sie in der Liste die Warnung, die Informationen zum Deaktivieren von Windows Server Essentials-Funktionen nach der Umstellung von Berichten ein.  
  
3.  Klicken Sie in der Warnung auf **Deaktivieren von Windows Server Essentials-Funktionen**.  
  
#### <a name="from-the-get-help-and-support-pane"></a>Im Bereich %%amp;quot;Hilfe und Support%%amp;quot;  
  
1. Klicken Sie auf der Startseite auf %%amp;quot;Hilfe und Support%%amp;quot;.  
  
2. Klicken Sie auf **Assistent für Windows Server Essentials-Funktionen deaktivieren**.  
  
   Es ist möglich, dass einige Aufgaben, indem ausgeführt die **Assistent für Windows Server Essentials-Funktionen deaktivieren** nicht erfolgreich abgeschlossen. In einigen Fällen wird dadurch die Ausführung des Dashboards verhindert. In diesem Fall können Sie den Assistenten manuell starten, indem Sie folgende Datei ausführen:  
  
   **%SystemDrive%\Programme\Microsoft c:\Programme\Windows Server\Bin\TurnOffFeaturesWizard.exe**  
  
## <a name="see-also"></a>Siehe auch  
  

-   [Umstellung auf Windows Server 2012 R2 Standard](Transition-from-Windows-Server-2012-R2-Essentials-to-Windows-Server-2012-R2-Standard.md)  
  
-   [Migrieren von Serverdaten zu Windows Server Essentials](Migrate-Server-Data-to-Windows-Server-Essentials.md)

-   [Umstellung auf Windows Server 2012 R2 Standard](../migrate/Transition-from-Windows-Server-2012-R2-Essentials-to-Windows-Server-2012-R2-Standard.md)  
  
-   [Migrieren von Serverdaten zu Windows Server Essentials](../migrate/Migrate-Server-Data-to-Windows-Server-Essentials.md)

