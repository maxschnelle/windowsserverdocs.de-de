---
title: 'Schritt 7: Ausführen von Aufgaben nach der Migration zu Windows Server Essentials'
description: Beschreibt die Verwendung von Windows Server Essentials
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: d382e3fd-d393-4bd0-883f-db50104a969f
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 579be2c36ca01a4b8ab2a34157e13e298e34c48c
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80852323"
---
# <a name="step-7-perform-post-migration-tasks-for-the-windows-server-essentials-migration"></a>Schritt 7: Ausführen von Aufgaben nach der Migration zu Windows Server Essentials

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Die folgenden Aufgaben helfen Ihnen bei der Einrichtung der Zielserver mit einigen gleichen Einstellungen, die sich auf dem Quellserver befinden. Möglicherweise haben Sie einige dieser Einstellungen auf Ihrem Quellserver beim Migrieren deaktiviert, damit sie nicht auf den Zielserver migriert wurden.  
  
1.  [Löschen von DNS-Einträgen für den Quell Server](Step-7--Perform-post-migration-tasks-for-the-Windows-Server-Essentials-migration.md#BKMK_DeleteDNSEntries)  
  
2.  [Freigeben von Branchen-und anderen Anwendungsdaten Ordnern](Step-7--Perform-post-migration-tasks-for-the-Windows-Server-Essentials-migration.md#BKMK_ShareLineOfBusinessAndOtherApplications)  
  
##  <a name="delete-dns-entries-for-the-source-server"></a><a name="BKMK_DeleteDNSEntries"></a>Löschen von DNS-Einträgen für den Quell Server  
 Nachdem Sie den Quellserver außer Betrieb nehmen, kann der Domain Name Service (DNS)-Server weiterhin Einträge enthalten, die auf den Quellserver verweisen. Löschen Sie diese DNS-Einträge.  
  
#### <a name="to-delete-dns-entries-that-point-to-the-source-server"></a>So löschen Sie DNS-Einträge, die auf den Quellserver verweisen  
  
1.  Öffnen Sie auf dem Zielserver **DNS-Manager**.  
  
2.  Klicken Sie im DNS-Manager mit der rechten Maustaste auf den Namen des Servers, klicken Sie auf **Eigenschaften**, und klicken Sie dann auf die Registerkarte **Weiterleitungen**.  
  
3.  Ermitteln Sie, ob es einen Eintrag in der Weiterleitungsliste gibt, der auf den Quellserver verweist. Wenn einer vorhanden ist, klicken Sie auf **Bearbeiten**, und löschen Sie diesen Eintrag im Fenster **Weiterleitungen bearbeiten**.  
  
4.  Erweitern Sie im **DNS-Manager** den Namen des Servers, und klicken Sie dann auf **Forward-Lookupzonen**.  
  
5.  Klicken Sie mit der rechten Maustaste für jede Forward-Lookupzone auf die Zone, klicken Sie dann auf **Eigenschaften**, und klicken Sie dann auf die Registerkarte **Server benennen**.  
  
6.  Wählen Sie einen Eintrag im Textfeld **Server benennen**, der auf de Quellserver verweist, klicken Sie auf **Entfernen** und klicken Sie dann auf **OK**.  
  
7.  Wiederholen Sie die Schritte 5 und 6, bis alle Verweise auf den Quellserver entfernt sind.  
  
8.  Klicken Sie auf **OK**, um das Dialogfeld **Eigenschaften** zu schließen.  
  
9. Erweitern Sie im **DNS-Manager** **Reverse-Lookupzonen**.  
  
10. Wiederholen Sie die Schritte 6 bis 9, um alle Reverse-Lookupzonen zu entfernen, die auf den Quellserver verweisen.  
  
##  <a name="share-line-of-business-and-other-application-data-folders"></a><a name="BKMK_ShareLineOfBusinessAndOtherApplications"></a>Freigeben von Branchen-und anderen Anwendungsdaten Ordnern  
 Sie müssen die Berechtigungen für freigegebene Ordner und NTFS-Berechtigungen für die Branchen- und andere Anwendungsordner für Daten, die Sie auf den Zielserver kopiert haben, festlegen. Nachdem Sie die Berechtigungen festgelegt haben, werden die freigegebenen Ordner auf dem Dashboard in der Registerkarte**Speicher** angezeigt.  
  
 Wenn Sie ein Anmeldeskript zum Zuordnen von Laufwerken für die freigegebenen Ordner verwenden, müssen Sie das Skript zum Zuordnen der Laufwerke auf dem Zielserver aktualisieren.  
  
## <a name="next-steps"></a>Nächste Schritte  
 Sie haben die Aufgaben nach der Migration für die Windows Server Essentials-Migration durchgeführt. Gehen Sie jetzt zu [Schritt 8: Ausführen des Windows Server Essentials-Best Practices Analyzer](Step-8--Run-the-Windows-Server-Essentials-Best-Practices-Analyzer.md).  
  

Alle Schritte finden Sie unter [Migrieren zu Windows Server Essentials](Migrate-from-Previous-Versions-to-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md).

