---
title: "Schritt7: Ausführen von Aufgaben nach der Migration für die Windows Server Essentials-Migration"
description: Beschreibt, wie Sie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d382e3fd-d393-4bd0-883f-db50104a969f
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 6a61d28f29097bcb6993a471587f4cc1ae0bcc3f
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="step-7-perform-post-migration-tasks-for-the-windows-server-essentials-migration"></a>Schritt7: Ausführen von Aufgaben nach der Migration für die Windows Server Essentials-Migration

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials

Die folgenden Aufgaben können Sie das Abschließen der Einrichtung der Zielserver mit einigen gleichen Einstellungen, die auf dem Quellserver waren. Ist möglicherweise deaktiviert, einige dieser Einstellungen auf dem Quellserver während der Migration, damit sie nicht auf den Zielserver migriert wurden.  
  
1.  [Löschen von DNS-Einträge für den Quellserver](Step-7--Perform-post-migration-tasks-for-the-Windows-Server-Essentials-migration.md#BKMK_DeleteDNSEntries)  
  
2.  [Freigeben Sie Line-of-Business und anderen Anwendungsordnern für Daten](Step-7--Perform-post-migration-tasks-for-the-Windows-Server-Essentials-migration.md#BKMK_ShareLineOfBusinessAndOtherApplications)  
  
##  <a name="BKMK_DeleteDNSEntries"></a>Löschen von DNS-Einträge für den Quellserver  
 Nachdem Sie den Quellserver außer Betrieb nehmen, kann der Domain Name Service (DNS)-Server weiterhin Einträge enthalten, die auf den Quellserver verweisen. Löschen Sie die DNS-Einträge.  
  
#### <a name="to-delete-dns-entries-that-point-to-the-source-server"></a>So löschen Sie DNS-Einträge, die auf den Quellserver verweisen  
  
1.  Öffnen Sie auf dem Zielserver **DNS-Manager**.  
  
2.  Im DNS-Manager mit der rechten Maustaste des Servernamens, klicken Sie auf **Eigenschaften**, und klicken Sie dann auf die **Weiterleitungen** Registerkarte.  
  
3.  Bestimmen Sie, ob ein Eintrag vorhanden ist, in der Weiterleitungsliste, die auf dem Quellserver verweist. Wenn vorhanden ist, klicken Sie auf **bearbeiten**, und löschen Sie diesen Eintrag in der **Weiterleitungen bearbeiten** Fenster.  
  
4.  In **DNS-Manager**, erweitern Sie den Namen des Servers, und klicken Sie dann **Forward-Lookupzonen**.  
  
5.  Für jede Forward-Lookupzone Maustaste auf die Zone, und klicken Sie auf **Eigenschaften**, und klicken Sie dann auf die **Namenserver** Registerkarte.  
  
6.  Wählen Sie einen Eintrag in der **Namenserver** Textfeld, klicken Sie auf dem Quellserver verweist auf, das **entfernen**, und klicken Sie dann auf **OK**.  
  
7.  Wiederholen Sie die Schritte5 und 6, bis alle Verweise auf dem Quellserver entfernt werden.  
  
8.  Klicken Sie auf **OK** zum Schließen der **Eigenschaften** Fenster.  
  
9. In **DNS-Manager**, erweitern Sie **Reverse-Lookupzonen**.  
  
10. Wiederholen Sie die Schritte6 bis 9, um alle Reverse-Lookupzonen zu entfernen, die auf den Quellserver verweisen.  
  
##  <a name="BKMK_ShareLineOfBusinessAndOtherApplications"></a>Freigeben Sie Line-of-Business und anderen Anwendungsordnern für Daten  
 Sie müssen festlegen, die Berechtigungen für freigegebene Ordner und NTFS-Berechtigungen für die Line-of-Business und anderen Anwendungsordnern für Daten, die Sie auf den Zielserver kopiert. Nachdem Sie die Berechtigungen festgelegt haben, werden die freigegebenen Ordner auf dem Dashboard auf angezeigt der **Speicher** Registerkarte.  
  
 Wenn Sie ein Anmeldeskript zum Zuordnen von Laufwerken für die freigegebenen Ordner verwenden, müssen Sie das Skript zum Zuordnen der Laufwerke auf dem Zielserver aktualisieren.  
  
## <a name="next-steps"></a>Nächste Schritte  
 Sie haben die Aufgaben nach der Migration für die Windows Server Essentials-Migration durchgeführt. Lesen Sie jetzt [Schritt8: Ausführen der Windows Server Essentials Best Practices Analyzer](Step-8--Run-the-Windows-Server-Essentials-Best-Practices-Analyzer.md).  
  

Alle Schrittefinden Sie unter [Migrieren zu Windows Server Essentials](Migrate-from-Previous-Versions-to-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md).

