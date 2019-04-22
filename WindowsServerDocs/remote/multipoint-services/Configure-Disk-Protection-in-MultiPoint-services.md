---
title: Konfigurieren von Datenträgerschutz in MultiPoint Services
description: Erfahren Sie, wie von Datenträgerschutz für MultiPoint Services einrichten
ms.custom: na
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bd9bf5b9-e481-499b-9c15-7ee5a4f470c4
author: evaseydl
manager: scottman
ms.author: evas
ms.date: 08/04/2016
ms.openlocfilehash: dc0a46b57753f08cc7d79fd05de7a9e81469cc86
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59820171"
---
# <a name="configure-disk-protection"></a>Konfigurieren von Datenträgerschutz
Sie können die Datenträgerschutz in Multipoint Services verwenden, schützen Sie Ihre Systemvolume von unbeabsichtigten Updates, zum Planen von Windows-Updates beibehalten werden sollen, während des Datenträgerschutzes Datenträgerschutz vorübergehend zu deaktivieren und deinstallieren Sie den Datenträgerschutz aktiv ist.  
  
Durch das Aktivieren von Datenträgerschutz in MultiPoint Services, können Sie das Systemvolume (das Laufwerk, auf dem Windows installiert ist, in der Regel "c:") schützen. vor unerwünschten Änderungen. Wenn Disk Protection aktiviert ist, werden Änderungen an das Systemvolume, damit sie verwirft einfach einen Neustart des Computers, und wird automatisch das System wieder in den vorherigen als funktionierend bekannten Zustand in einen temporären Speicherort gespeichert.  
  
Der Administrator kann leicht Software installieren oder nehmen Sie konfigurationsänderungen durch vorübergehendes Deaktivieren des datenträgerschutzes. Um das System den aktuellen Windows-Updates und Antimalwaredefinitionen zu halten, plant Datenträgerschutz ein Wartungsfensters herunterladen und Installieren von Updates. Der Administrator bieten auch ein benutzerdefiniertes Skript zum Ausführen im Rahmen des Wartungsfensters, um alle Wartungsbedarf über Windows Update zu berücksichtigen.  
  
## <a name="enable-disk-protection"></a>Aktivieren Sie den Datenträgerschutz  
Bevor Sie den Datenträgerschutz aktivieren, stellen Sie sicher, dass alle Anwendungen und Treiber installiert und auf dem neuesten Stand sind, und verschieben Sie Ihre Benutzerprofile auf ein Volume aus, die nicht geschützt werden. Wenn Sie manuelle Updates vornehmen, nachdem Sie den Datenträgerschutz aktivieren möchten, können Sie vorübergehend Datenträgerschutz deaktivieren. Allerdings ist es am einfachsten, die als idealer Status des Systems kommen, bevor Disk Protection aktiviert ist.  
  
 
1.  Melden Sie sich an den Server mit MultiPoint Services als Administrator an.  
  
2.  Bevor Sie den Datenträgerschutz aktivieren:  
  
    -   Vergewissern Sie sich das MultiPoint Services-System in genau den Zustand ist in der Sie verbleiben soll. Beispielsweise stellen Sie sicher, dass installierte Software, Updates und Systemeinstellungen richtig sind.  
  
    -   Verschieben von Benutzerprofilen auf ein Volume aus, die nicht geschützt ist, oder richten Sie einen freigegebenen Dateispeicherort aus dem System, wie in beschrieben [aktivieren-Dateifreigabe in MultiPoint Services](Enable-file-sharing-in-MultiPoint-services.md).  
  
3.  Von der **starten** öffnen **MultiPoint-Manager**.  
  
4.  Klicken Sie auf die **Startseite** auf **Datenträgerschutz aktivieren**, und klicken Sie dann auf **OK**.  
  
Wenn zum ersten Mal Disk Protection aktiviert ist, wird das System einen Treiber zu installieren und erstellen eine Cachedatei auf dem Systemvolume vorbereitet. Die Cachedatei speichert vorübergehend alle Änderungen an das Systemvolume, während des Datenträgerschutzes aktiv ist. Da System-Updates in der Cachedatei gespeichert werden, ändern sie nicht den geschützten Inhalt des Volumes außerhalb der Cachedatei. Jedes Mal, die das System gestartet wird, ist die Cachedatei Zurücksetzen der verwirft alle Änderungen seit dem Systemstart der vorherigen dort gespeichert. Daher startet das System immer in den gleichen Zustand wie beim Disk Protection aktiviert wurde.  
  
Windows muss einige Systemdateien – wie z.B. die Systemauslagerungsdatei Speicherortes Absturz und Ereignisprotokolle zu aktualisieren. Diese Dateien werden nicht verworfen, wenn der Datenträger-Schutz aktiviert ist. Um dies zu erreichen, wird ein neues Volume mit dem Namen DpReserved erstellt, wenn Datenträgerschutz zum ersten Mal aktiviert ist, und diese Dateien in diesem Volume verschoben werden. DpReserved Partition ist nicht geschützt, sodass Schreibvorgänge für diese Dateien bei neu gestartet wird, behalten, auch wenn die Disk Protection aktiviert ist.  
  
## <a name="schedule-software-updates"></a>Planen von Softwareupdates  
Wenn es sich bei Windows für die automatische Installation von Windows-Updates konfiguriert ist, des Datenträgerschutzes können diese Updates in die konfigurierte Zeit und verwirft keine Updates. Windows-Updates für 3:00 Uhr geplant, beispielweise Datenträgerschutz für Updates täglich um 3:00 Uhr Wenn keine Updates gefunden werden, MultiPoint Services vorübergehend deaktiviert Datenträgerschutz, wendet die Updates, und klicken Sie dann erneut Disk Protection aktiviert.  
   
1.  Im MultiPoint-Manager zeigt die **Startseite** Registerkarte, und klicken Sie dann auf **Planen von Softwareupdates**.  
  
2.  Klicken Sie in das Dialogfeld Zeitplan von Softwareupdates auf **aktualisieren zur**, und wählen Sie eine Zeit für Updates – z. B. **3:00 Uhr**.  
  
3.  Wählen Sie die **führen Sie Windows Update** Kontrollkästchen.  
  
4.  Wenn Ihre Organisation ein eigenes Updateskript ausgeführt wird, wählen Sie die **führen Sie das folgende Programm** , und geben Sie den Speicherort des Updateskripts Ihrer Organisation.  
  
5.  Wählen Sie eine maximale Zeit, die Updates ausführen zu können.  
  
6.  Klicken Sie unter **Abschluss**, auswählen, ob die Anwendung zurück zu den vorherigen Zustand der Stromversorgung oder fahren Sie nach dem Anwenden von Updates herunter.  
  
7.  Klicken Sie auf **OK**.  
  
## <a name="temporarily-disable-disk-protection"></a>Vorübergehend deaktivieren des Datenträgerschutzes  
Wenn der Administrator muss die Software installieren, Systemeinstellungen ändern oder andere Wartungsaufgaben, bei denen Systemupdates ausführen, können sie vorübergehend Datenträgerschutz deaktivieren. Nachdem die Änderungen vorgenommen wurden, sollten Sie die aktivieren Sie Datenträgerschutz wieder. Bei System neu gestartet wird wird das System den Zustand beibehalten, wenn der Datenträger-Schutz aktiviert wurde.  
    
1.  MultiPoint-Manager, klicken Sie auf die **Startseite** Registerkarte.  
  
2.  Klicken Sie auf der Registerkarte Home auf **Deaktivieren des datenträgerschutzes**, und klicken Sie dann auf **OK**.  
  
> [!NOTE]  
> Denken Sie daran, um Disk Protection erneut zu aktivieren, nachdem die Wartung abgeschlossen ist. Das System wird nicht erneut geschützt werden, bis der Administrator explizit wieder Disk Protection aktiviert.  
  
## <a name="uninstall-disk-protection"></a>Deinstallieren des Datenträgerschutzes  
Der Treiber und der Cache-Datei des Datenträgerschutzes Deinstallieren entfernt werden, sodass nur hierzu sollten Sie mithilfe des Datenträgerschutzes langfristig zu beenden. Wenn Sie einfach Wartungsarbeiten durchführen oder den Schutz vorübergehend beenden möchten, verwenden Sie stattdessen die Aufgabe des Datenträger Schutzes deaktivieren.  
  
Sie können Datenträgerschutz deinstallieren, ob er aktiviert oder deaktiviert ist.  
   
1.  MultiPoint-Manager, klicken Sie auf die **Startseite** Registerkarte.  
  
2.  Auf der Registerkarte "Home", und klicken Sie auf auf **deinstallieren Datenträgerschutz**, und klicken Sie dann auf **OK**.  
  
    Nachdem Sie auf **OK**, den Computer neu gestartet wird. Der Deinstallationsvorgang erfordert mehrere neu gestartet wird, in denen der Treiber und die Cache-Datei entfernt werden. Die DpReserved Partition verbleiben, und die Auslagerungsdatei, Absturz Speicherortes und Ereignisprotokoll Dateien bleiben so konfiguriert, dass die Partition DpReserved verwenden.