---
title: "Übergang von Windows Server Essentials zu Windows Server2012 Standard"
description: Beschreibt, wie Sie Windows Server Essentials
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
ms.openlocfilehash: d2005b72adede72b718fa5b49b93435f5fbac1bd
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="transition-from-windows-server-essentials-to-windows-server-2012-standard"></a>Übergang von Windows Server Essentials zu Windows Server2012 Standard

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials

 Windows Server® 2012 Essentials unterstützt bis zu 25 Benutzer und 50 Geräte. Wenn Ihre geschäftliche Anforderungen diese Begrenzung überschreiten, können Sie eine direkte lizenzumstellung von Windows Server Essentials auf Windows Server2012 Standard, um die Lizenz ausführen.  
  
## <a name="how-the-transition-affects-user-and-device-limits"></a>Beschränkt die Auswirkungen der Übergang auf Benutzer und Gerät  
 Nach der Windows Server2012 Standard Umstellung, werden die Benutzerkonten- und gerätebegrenzungen zwar entfernt, aber die Features, die speziell für Windows Server Essentials (z.B. das Dashboard, Remotewebzugriff und clientcomputersicherung), weiterhin verfügbar. Technische Einschränkungen für diese Funktionen jedoch unterstützt höchstens 75 Benutzerkonten und 75 Geräte. Wenn es mehr als 75 Benutzerkonten oder Geräte hinzugefügt wird, sollten Sie die Windows Server Essentials-Funktionen deaktivieren und der Windows Server2012 Standard systemeigenen Tools zum Verwalten von Benutzerkonten und Geräten verwenden.  
  
> [!IMPORTANT]
>   Windows Server2012 Standard ist (Client Access License, CAL) für jeden Benutzer oder Geräte in Ihrer Umgebung erforderlich. Dies unterscheidet sich von Windows Server Essentials, die die CAL-Modell nicht verwendet und kommt nicht keine Clientzugriffslizenzen.  Bei der Windows Server Essentials auf Windows Server2012 Standard Umstellung, müssen Sie die entsprechende Anzahl und Typ der Clientzugriffslizenzen für Ihre Umgebung (die meisten Kunden erwerben Benutzer-CALs) erwerben.  
  
## <a name="before-the-transition"></a>Vor der Umstellung  
  
-   Vor der Umstellung von Windows Server Essentials auf Windows Server2012 Standard, sollten Sie vollständig die Serverdaten sichern.  
  
    > [!IMPORTANT]
    >  Sie können nicht ohne eine vollständige Sicherung des Servers den Server in den Zustand wiederherstellen, in dem vor der Umstellung.  
  
-   Stellen Sie außerdem sicher, dass Sie lesen und der Endbenutzer-Lizenzvertrag (EULA) für Windows Server2012 Standard verstehen. So zeigen Sie den Endbenutzer-Lizenzvertrag an  
  
    1.  Öffnen Sie ein Eingabeaufforderungsfenster als Administrator.  
  
    2.  Führen Sie den folgenden Befehl ein:  
  
         **DISM /online /set-edition: ServerStandard /geteula: Eula Path**  
  
         Wo **Eula Path** den Speicherort darstellt, dem Sie die EULA-Datei speichern möchten. Beispiel: C:\ws8std_eula.RTF.  Achten Sie darauf, RTF als die Dateierweiterung zu verwenden.  
  
    3.  Öffnen Sie den Speicherort der Datei, und doppelklicken Sie dann auf die Datei, um es zu öffnen.  
  
## <a name="transition-to--windows-server-2012-standard"></a>Umstellung auf Windows Server2012 Standard  
 Nachdem Sie entschieden haben, für den Übergang Windows Server Essentials auf Windows Server2012 Standard, vollständige diese beiden Schritteaus:  
  
1.  Erwerben einer Lizenz für Windows Server2012 Standard und die erforderlichen Anzahl an Benutzer- und/oder Geräte-Clientzugriffslizenzen für Ihre Umgebung.  
  
     Sie können eine Lizenz für Windows Server2012 Standard erwerben, über einen Vertragshändler, einen Distributor oder mithilfe einer [Microsoft-Partner](https://pinpoint.microsoft.com/SelectCulture.aspx).  
  
    > [!NOTE]
    >  Wenn Sie Windows Server2012 Standard ursprünglich erworben und Ihre Herabstufungsrechte für eine Ihrer beiden virtuellen Instanzen als Windows Server Essentials installieren ausgeübt, brauchen Sie keine zusätzlichen Lizenzen erwerben.  
    >   
    >  Wenn Sie Windows Server2012 Standard über den volumenlizenzkanal erwerben, können Sie ein ISO-Abbild und einen Product Key für Windows Server2012 Standard vom Volume Licensing Service Center (VLSC) herunterladen.  
    >   
    >  Wenn Sie Windows Server2012 Standard über einen anderen Kanal erwerben können herunterladen ein ISO-Abbild und einen evaluierungs-Product Key für Windows Server Essentials aus der [TechNet Evaluation Center](https://technet.microsoft.com/evalcenter/jj659306.aspx). Den Übergang durchführen, wie im nächsten Schrittbeschrieben wird das evaluierungsprodukt in ein vollständig lizenziertes und unterstütztes Produkt umgewandelt.  
  
2.  Öffnen Sie Windows PowerShell als Administrator, und führen Sie den folgenden Befehl aus.  
  
     **DISM /online /set-edition: ServerStandard /accepteula /productkey:***Product Key*  
  
     Wo *Product Key* ist der Product Key für Ihre Kopie von Windows Server2012 Standard.  
  
     Der Server wird neu gestartet, um den Umstellungsprozess fertigzustellen.  
  
 Nach der Umstellung sind die Windows Server Essentials-Funktionen bleiben auf dem Server und werden für bis zu 75 Benutzer und 75 Geräte unterstützt. Wenn Sie einen dieser Grenzwerte überschreiten, sollten Sie die Windows Server2012 Standard systemeigenen Tools zum Verwalten von Benutzerkonten und Geräten verwenden.  
  
 Nach der Windows Server2012 Standard Umstellung, sind die Medienfunktionen von Windows Server Essentials darüber hinaus nicht mehr verfügbar. Dazu gehören die Medienfunktionen des Remotewebzugriffs sowie die Medieneinstellungen auf dem Dashboard.  
  
## <a name="turn-off--windows-server-essentials-features"></a>Windows Server Essentials-Funktionen deaktivieren  
 Wenn Sie Windows Server Essentials-Dashboard oder andere Zusatzfunktionen zum Verwalten des Servers nicht mehr benötigen, können Sie die Funktionen deaktivieren und von Ihrem Server entfernen.  
  
 Die **Assistent für Windows Server Essentials-Funktionen deaktivieren** können Sie die Features deinstallieren. Er bereinigt auch den Server von Dateien, die von der Windows Server Essentials-Server-Software erstellt wurden.  Einige Bereinigungsoptionen werden sofort ausgeführt, während andere nach dem Neustart des Servers initiiert werden.  
  
 Die **Assistent für Windows Server Essentials-Funktionen deaktivieren** erfordert, dass alle Add-Ins manuell deinstallieren, bevor Sie den Assistenten abschließen können. Um eine Liste der installierten Add-Ins anzuzeigen, öffnen Sie die Seite "Anwendungstyp" im Dashboard. Der Assistent wird Sie gewarnt, wenn es erkennt der installierten Add-Ins und werden aufgefordert, diese zu deinstallieren.  
  
 Die **Assistent für Windows Server Essentials-Funktionen deaktivieren** können Sie wählen, ob Sie Sicherungsdateien für Client Computer, die nach dem Deaktivieren der Windows Server Essentials-Funktionen zu halten.  
  
 Es gibt zwei Möglichkeiten zum Ausführen der **Assistent für Windows Server Essentials-Funktionen deaktivieren** über das Dashboard:  
  
#### <a name="from-the-alert"></a>In der Warnmeldung  
  
1.  Öffnen Sie die Meldungsanzeige über das Dashboard.  
  
2.  Wählen Sie in der Liste die Warnung, die Informationen zum Deaktivieren von Windows Server Essentials-Funktionen nach der Umstellung meldet.  
  
3.  Klicken Sie in der Warnung auf **Windows Server Essentials-Funktionen deaktivieren**.  
  
#### <a name="from-the-get-help-and-support-pane"></a>Klicken Sie im Hilfe und Support  
  
1.  Auf der Startseite, klicken Sie dann auf Hilfe und Support.  
  
2.  Klicken Sie auf **Assistent für Windows Server Essentials-Funktionen deaktivieren**.  
  
 Es ist möglich, dass einige Aufgaben durch die **Assistent für Windows Server Essentials-Funktionen deaktivieren** nicht erfolgreich abgeschlossen. In einigen Fällen kann dies im Dashboard deaktivieren. In diesem Fall können Sie den Assistenten manuell starten, durch Ausführen der Datei:  
  
 **%SystemDrive%\Program c:\Programme\Windows Server\Bin\TurnOffFeaturesWizard.exe**  
  
## <a name="see-also"></a>Siehe auch  
  

-   [Wechsel zu Windows Server 2012 R2 Standard](Transition-from-Windows-Server-2012-R2-Essentials-to-Windows-Server-2012-R2-Standard.md)  
  
-   [Migrieren von Serverdaten zu Windows Server Essentials](Migrate-Server-Data-to-Windows-Server-Essentials.md)

-   [Wechsel zu Windows Server 2012 R2 Standard](../migrate/Transition-from-Windows-Server-2012-R2-Essentials-to-Windows-Server-2012-R2-Standard.md)  
  
-   [Migrieren von Serverdaten zu Windows Server Essentials](../migrate/Migrate-Server-Data-to-Windows-Server-Essentials.md)

