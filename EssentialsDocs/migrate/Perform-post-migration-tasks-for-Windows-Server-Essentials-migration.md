---
title: "Ausführen von Aufgaben nach der Migration zu Windows Server Essentials-migration1"
description: Beschreibt, wie Sie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f2d236a4-0d62-4961-9d1f-332054e06f6d
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 535a547ded55cb4afc0942259eadf5222a815274
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="perform-post-migration-tasks-for-windows-server-essentials-migration1"></a>Ausführen von Aufgaben nach der Migration zu Windows Server Essentials-migration1

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials

Die folgenden Aufgaben können Sie das Abschließen der Einrichtung der Zielserver mit einigen gleichen Einstellungen, die auf dem Quellserver waren. Ist möglicherweise deaktiviert, einige dieser Einstellungen auf dem Quellserver während der Migration, damit sie nicht auf den Zielserver migriert wurden. Oder sie sind optionale Konfigurationsschritte, die Sie ausführen möchten.  
  

-   [Löschen von DNS-Einträgen des Quellservers](Perform-post-migration-tasks-for-Windows-Server-Essentials-migration.md#BKMK_DeleteDNSEntries)  
  
-   [Freigeben Sie Line-of-Business und anderen Anwendungsordnern für Daten](Perform-post-migration-tasks-for-Windows-Server-Essentials-migration.md#BKMK_ShareLineOfBusinessAndOtherApplications)  
  
-   [Beheben von clientcomputerproblemen nach der Migration](Perform-post-migration-tasks-for-Windows-Server-Essentials-migration.md#BKMK_FixClientComputerIssuesAfterMigrating)  
  
-   [Erteilen Sie der integrierten Administratorengruppe das Recht zum Anmelden als Batchauftrag.](Perform-post-migration-tasks-for-Windows-Server-Essentials-migration.md#BKMK_AdminGroup)  

-   [Löschen von DNS-Einträgen des Quellservers](../migrate/Perform-post-migration-tasks-for-Windows-Server-Essentials-migration.md#BKMK_DeleteDNSEntries)  
  
-   [Freigeben Sie Line-of-Business und anderen Anwendungsordnern für Daten](../migrate/Perform-post-migration-tasks-for-Windows-Server-Essentials-migration.md#BKMK_ShareLineOfBusinessAndOtherApplications)  
  
-   [Beheben von clientcomputerproblemen nach der Migration](../migrate/Perform-post-migration-tasks-for-Windows-Server-Essentials-migration.md#BKMK_FixClientComputerIssuesAfterMigrating)  
  
-   [Erteilen Sie der integrierten Administratorengruppe das Recht zum Anmelden als Batchauftrag.](../migrate/Perform-post-migration-tasks-for-Windows-Server-Essentials-migration.md#BKMK_AdminGroup)  

  
##  <a name="BKMK_DeleteDNSEntries"></a>Löschen von DNS-Einträgen des Quellservers  
 Nachdem Sie den Quellserver außer Betrieb nehmen, kann der Domain Name Service (DNS)-Server weiterhin Einträge enthalten, die auf den Quellserver verweisen. Löschen Sie die DNS-Einträge.  
  
#### <a name="to-delete-dns-entries-that-point-to-the-source-server"></a>So löschen Sie DNS-Einträge, die auf den Quellserver verweisen  
  
1.  Öffnen Sie auf dem Zielserver **DNS-Manager**.  
  
2.  Im DNS-Manager mit der rechten Maustaste des Servernamens, klicken Sie auf **Eigenschaften**, und klicken Sie dann auf die **Weiterleitungen** Registerkarte.  
  
3.  Bestimmen Sie, ob ein Eintrag vorhanden ist, in der Weiterleitungsliste, die auf dem Quellserver verweist. Wenn vorhanden ist, klicken Sie auf **bearbeiten**, und löschen Sie diesen Eintrag in der **Weiterleitungen bearbeiten** Fenster.  
  
4.  In **DNS-Manager**, erweitern Sie den Namen des Servers, und klicken Sie dann **Forward-Lookupzonen**.  
  
5.  Für jede Forward-Lookupzone Maustaste auf die Zone, und klicken Sie auf **Eigenschaften**, und klicken Sie dann auf die **Namenserver** Registerkarte.  
  
6.  Klicken Sie auf einen Eintrag in der **Namenserver** Feld, klicken Sie auf dem Quellserver verweist auf, das **entfernen**, und klicken Sie dann auf **OK**.  
  
7.  Wiederholen Sie die Schritte5 und 6, bis alle Verweise auf dem Quellserver entfernt werden.  
  
8.  Klicken Sie auf **OK** zum Schließen der **Eigenschaften** Fenster.  
  
9. In der **DNS-Manager** -Konsole, erweitern Sie **Reverse-Lookupzonen**.  
  
10. Wiederholen Sie die Schritte6 bis 9, um alle Reverse-Lookupzonen zu entfernen, die auf den Quellserver verweisen.  
  
##  <a name="BKMK_ShareLineOfBusinessAndOtherApplications"></a>Freigeben Sie Line-of-Business und anderen Anwendungsordnern für Daten  
 Sie müssen festlegen, die Berechtigungen für freigegebene Ordner und NTFS-Berechtigungen für die Line-of-Business und anderen Anwendungsordnern für Daten, die Sie auf den Zielserver kopiert. Nachdem Sie die Berechtigungen festgelegt haben, werden die freigegebenen Ordner angezeigt, in der Windows Server Essentials-Dashboard in der **Speicher** Abschnitt.  
  
 Wenn Sie ein Anmeldeskript zum Zuordnen von Laufwerken für die freigegebenen Ordner verwenden, müssen Sie das Skript zum Zuordnen der Laufwerke auf dem Zielserver aktualisieren.  
  
##  <a name="BKMK_FixClientComputerIssuesAfterMigrating"></a>Beheben von clientcomputerproblemen nach der Migration  
 Migrieren zu Windows Server Essentials von Windows Small Business Server2003 Premium Edition mit Microsoft Internet Security und Acceleration (ISA) Server installiert Clientcomputer im Netzwerk weiterhin Microsoft Firewall Client und Internet Explorer zur Verwendung eines Proxyservers konfiguriert.  
  
 Dies verursacht Konnektivitätsprobleme auf dem Client Computer, da der Proxyserver nicht mehr vorhanden ist. Wenn ein anderer Proxyserver konfiguriert ist, weiterhin die Clientcomputer den Server mit Windows SBS 2003 für den Proxyserver verwenden. Um dieses Problem zu beheben, müssen Sie Internet Explorer nicht verwenden, einen Proxyserver oder die neuen Proxyserver neu konfigurieren.  
  
#### <a name="to-reconfigure-internet-explorer"></a>So konfigurieren Sie Internet Explorer neu  
  
1.  In Internet Explorer, klicken Sie auf **Tools**, und klicken Sie dann auf **Internetoptionen**.  
  
2.  Klicken Sie auf die **Verbindungen** auf **LAN-Einstellungen**, und führen Sie dann eine der folgenden Optionen:  
  
    -   Wenn Sie nicht in Ihrem Netzwerk einen Proxyserver verwenden, deaktivieren Sie alle Kontrollkästchen in der **Einstellungen des lokalen Netzwerks (LAN)** Dialogfeld.  
  
    -   Wenn Sie einen neuen Proxyserver im Netzwerk verwenden möchten:  
  
        1.  In der **Einstellungen des lokalen Netzwerks (LAN)** Dialogfeld, deaktivieren Sie die Kontrollkästchen in der **automatische Konfiguration** Abschnitt.  
  
        2.  In der **Proxyserver** Abschnitt, stellen Sie sicher, dass beide Kontrollkästchen aktiviert sind.  
  
        3.  In der **Adresse** Geben Sie den vollständig qualifizierten Domänennamen (FQDN) des Proxyservers.  
  
        4.  In der **Port** geben **80**.  
  
3.  Klicken Sie auf **OK** zweimal.  
  
4.  Navigieren Sie zu einer Website, um sicherzustellen, dass die Verbindungseinstellungen richtig sind.  
  
##  <a name="BKMK_AdminGroup"></a>Erteilen Sie der integrierten Administratorengruppe das Recht zum Anmelden als Batchauftrag.  
 Nach der Migration einer vorhandenen Windows Small Business Server2003-Domäne mit Windows Server Essentials sollten Sie der integrierten Administratorengruppe das Recht zum Anmelden als Stapelverarbeitungsauftrag verfügen. Stellen Sie sicher, dass die integrierte Administratorengruppe das Recht zum Anmelden als Stapelverarbeitungsauftrag auf dem Zielserver noch hat. Administratoren benötigen dieses Recht eine Warnung auf dem Zielserver ausgeführt wird, ohne sich anzumelden.  
  
#### <a name="to-give-the-built-in-administrators-group-the-right-to-log-on-as-a-batch-job"></a>So erteilen Sie der integrierten Administratorengruppe das Recht zum Anmelden als Stapelverarbeitungsauftrag  
  
1.  Öffnen Sie auf dem Zielserver die **Gruppenrichtlinienverwaltung** Verwaltungstool.  
  
2.  In der **Gruppenrichtlinienverwaltung** Konsolenstruktur, erweitern Sie **Gesamtstruktur:***< ServerName\ >*, erweitern Sie Domänen und erweitern Sie dann den Server.  
  
3.  Erweitern Sie **Domänencontroller**, mit der rechten Maustaste **Standarddomänencontroller-Richtlinie**, und klicken Sie dann auf **bearbeiten**.  
  
4.  In **Gruppenrichtlinienverwaltungs-Editor**, klicken Sie auf **Standarddomänencontroller-Richtlinie***< ServerName\ >***Richtlinie**, und erweitern Sie dann **Computerkonfiguration**.  
  
5.  Erweitern Sie **Richtlinien**, erweitern Sie **Windows-Einstellungen**, und erweitern Sie dann **Sicherheitseinstellungen**.  
  
6.  In der **Sicherheitseinstellungen** Konsolenstruktur, erweitern Sie **lokale Richtlinien**, und klicken Sie dann auf **Zuweisen von Benutzerrechten**.  
  
7.  Klicken Sie im Ergebnisbereich mit der rechten Maustaste **Anmelden als Stapelverarbeitungsauftrag**, und klicken Sie dann auf Eigenschaften.  
  
8.  In der **Anmelden als Stapelverarbeitungsauftrag** auf **Benutzer oder Gruppe hinzufügen**.  
  
9. In der **Benutzer oder Gruppe hinzufügen** Dialogfeld, klicken Sie auf **Durchsuchen**.  
  
10. In der **Auswahl von Benutzern, Computern oder Gruppen**, geben Sie im Dialogfeld **Administratoren**.  
  
11. Klicken Sie auf **Namen überprüfen** zu überprüfen, ob die integrierte Administratorengruppe angezeigt wird, und klicken Sie dann auf **OK** dreimal, um die Einstellung zu speichern.  
  
## <a name="see-also"></a>Siehe auch  
  

-   [Migration von Windows SBS 2003](Migrate-Windows-Small-Business-Server-2003-to-Windows-Server-Essentials.md)  
  
-   [Migrieren von Serverdaten zu Windows Server Essentials](Migrate-Server-Data-to-Windows-Server-Essentials.md)

-   [Migration von Windows SBS 2003](../migrate/Migrate-Windows-Small-Business-Server-2003-to-Windows-Server-Essentials.md)  
  
-   [Migrieren von Serverdaten zu Windows Server Essentials](../migrate/Migrate-Server-Data-to-Windows-Server-Essentials.md)

