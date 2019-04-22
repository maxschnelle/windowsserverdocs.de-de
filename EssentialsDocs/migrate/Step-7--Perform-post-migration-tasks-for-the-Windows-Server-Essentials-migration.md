---
title: 'Schritt 7: Ausführen von Aufgaben nach der Migration für die Windows Server Essentials-migration'
description: Beschreibt, wie Windows Server Essentials
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
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59819161"
---
# <a name="step-7-perform-post-migration-tasks-for-the-windows-server-essentials-migration"></a>Schritt 7: Ausführen von Aufgaben nach der Migration für die Windows Server Essentials-migration

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Die folgenden Aufgaben helfen Ihnen bei der Einrichtung der Zielserver mit einigen gleichen Einstellungen, die sich auf dem Quellserver befinden. Möglicherweise haben Sie einige dieser Einstellungen auf Ihrem Quellserver beim Migrieren deaktiviert, damit sie nicht auf den Zielserver migriert wurden.  
  
1.  [Löschen von DNS-Einträge für den Quellserver](Step-7--Perform-post-migration-tasks-for-the-Windows-Server-Essentials-migration.md#BKMK_DeleteDNSEntries)  
  
2.  [Freigeben von Line-of-Business- und anderen Anwendungsordnern für Daten](Step-7--Perform-post-migration-tasks-for-the-Windows-Server-Essentials-migration.md#BKMK_ShareLineOfBusinessAndOtherApplications)  
  
##  <a name="BKMK_DeleteDNSEntries"></a> Löschen von DNS-Einträge für den Quellserver  
 Nachdem Sie den Quellserver außer Betrieb nehmen, kann der Domain Name Service (DNS)-Server weiterhin Einträge enthalten, die auf den Quellserver verweisen. Löschen Sie diese DNS-Einträge.  
  
#### <a name="to-delete-dns-entries-that-point-to-the-source-server"></a>So löschen Sie DNS-Einträge, die auf den Quellserver verweisen  
  
1.  Öffnen Sie auf dem Zielserver **DNS-Manager**.  
  
2.  Klicken Sie im DNS-Manager mit der rechten Maustaste auf den Namen des Servers, klicken Sie auf **Eigenschaften**, und klicken Sie dann auf die Registerkarte **Weiterleitungen** .  
  
3.  Ermitteln Sie, ob es einen Eintrag in der Weiterleitungsliste gibt, der auf den Quellserver verweist. Wenn einer vorhanden ist, klicken Sie auf **Bearbeiten**, und löschen Sie diesen Eintrag im Fenster **Weiterleitungen bearbeiten**.  
  
4.  Erweitern Sie im **DNS-Manager**den Namen des Servers, und klicken Sie dann auf **Forward-Lookupzonen**.  
  
5.  Klicken Sie mit der rechten Maustaste für jede Forward-Lookupzone auf die Zone, klicken Sie dann auf **Eigenschaften**, und klicken Sie dann auf die Registerkarte **Server benennen**.  
  
6.  Wählen Sie einen Eintrag im Textfeld **Server benennen**, der auf de Quellserver verweist, klicken Sie auf **Entfernen** und klicken Sie dann auf **OK**.  
  
7.  Wiederholen Sie die Schritte 5 und 6, bis alle Verweise auf den Quellserver entfernt sind.  
  
8.  Klicken Sie auf **OK**, um das Dialogfeld **Eigenschaften** zu schließen.  
  
9. Erweitern Sie im **DNS-Manager****Reverse-Lookupzonen**.  
  
10. Wiederholen Sie die Schritte 6 bis 9, um alle Reverse-Lookupzonen zu entfernen, die auf den Quellserver verweisen.  
  
##  <a name="BKMK_ShareLineOfBusinessAndOtherApplications"></a> Freigeben von Line-of-Business- und anderen Anwendungsordnern für Daten  
 Sie müssen die Berechtigungen für freigegebene Ordner und NTFS-Berechtigungen für die Branchen- und andere Anwendungsordner für Daten, die Sie auf den Zielserver kopiert haben, festlegen. Nachdem Sie die Berechtigungen festgelegt haben, werden die freigegebenen Ordner auf dem Dashboard in der Registerkarte **Speicher** angezeigt.  
  
 Wenn Sie ein Anmeldeskript zum Zuordnen von Laufwerken für die freigegebenen Ordner verwenden, müssen Sie das Skript zum Zuordnen der Laufwerke auf dem Zielserver aktualisieren.  
  
## <a name="next-steps"></a>Nächste Schritte  
 Sie haben die Aufgaben nach der Migration zu Windows Server Essentials ausgeführt. Wechseln Sie nun zur [Schritt 8: Ausführen von Windows Server Essentials Best Practices Analyzer](Step-8--Run-the-Windows-Server-Essentials-Best-Practices-Analyzer.md).  
  

Alle Schritte finden Sie unter [Migrieren zu Windows Server Essentials](Migrate-from-Previous-Versions-to-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md).

