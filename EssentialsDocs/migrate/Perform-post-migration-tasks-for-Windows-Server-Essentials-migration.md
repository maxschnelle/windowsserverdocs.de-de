---
title: Ausführen von Aufgaben nach der Migration für Windows Server Essentials Migration1
description: Beschreibt die Verwendung von Windows Server Essentials
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: f2d236a4-0d62-4961-9d1f-332054e06f6d
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: b421ab7b234c9ae2ffb7d0765fe0937c4376996a
ms.sourcegitcommit: 6d6a0225b1f83b71fcb494b94d666cd5e54c7566
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/23/2020
ms.locfileid: "85267521"
---
# <a name="perform-post-migration-tasks-for-windows-server-essentials-migration1"></a>Ausführen von Aufgaben nach der Migration für Windows Server Essentials Migration1

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Die folgenden Aufgaben helfen Ihnen bei der Einrichtung der Zielserver mit einigen gleichen Einstellungen, die sich auf dem Quellserver befinden. Möglicherweise haben Sie einige dieser Einstellungen auf Ihrem Quellserver beim Migrieren deaktiviert, damit sie nicht auf den Zielserver migriert wurden. Oder es sind optionale Konfigurationsschritte, die Sie ausführen sollten.  
  

-   [Löschen von DNS-Einträgen des Quellservers](Perform-post-migration-tasks-for-Windows-Server-Essentials-migration.md#BKMK_DeleteDNSEntries)  
  
-   [Freigeben von Branchen- und anderen Anwendungsordnern für Daten](Perform-post-migration-tasks-for-Windows-Server-Essentials-migration.md#BKMK_ShareLineOfBusinessAndOtherApplications)  
  
-   [Beheben von Clientcomputerproblemen nach der Migration](Perform-post-migration-tasks-for-Windows-Server-Essentials-migration.md#BKMK_FixClientComputerIssuesAfterMigrating)  
  
-   [Erteilen des Rechts zum Anmelden als Stapelverarbeitungsauftrag für die integrierte Administratorengruppe](Perform-post-migration-tasks-for-Windows-Server-Essentials-migration.md#BKMK_AdminGroup)  

  
##  <a name="delete-dns-entries-of-the-source-server"></a><a name="BKMK_DeleteDNSEntries"></a>Löschen von DNS-Einträgen des Quell Servers  
 Nachdem Sie den Quellserver außer Betrieb nehmen, kann der Domain Name Service (DNS)-Server weiterhin Einträge enthalten, die auf den Quellserver verweisen. Löschen Sie diese DNS-Einträge.  
  
#### <a name="to-delete-dns-entries-that-point-to-the-source-server"></a>So löschen Sie DNS-Einträge, die auf den Quellserver verweisen  
  
1.  Öffnen Sie auf dem Zielserver **DNS-Manager**.  
  
2.  Klicken Sie im DNS-Manager mit der rechten Maustaste auf den Namen des Servers, klicken Sie auf **Eigenschaften**, und klicken Sie dann auf die Registerkarte **Weiterleitungen**.  
  
3.  Ermitteln Sie, ob es einen Eintrag in der Weiterleitungsliste gibt, der auf den Quellserver verweist. Wenn einer vorhanden ist, klicken Sie auf **Bearbeiten**, und löschen Sie diesen Eintrag im Fenster **Weiterleitungen bearbeiten**.  
  
4.  Erweitern Sie im **DNS-Manager** den Namen des Servers, und klicken Sie dann auf **Forward-Lookupzonen**.  
  
5.  Klicken Sie mit der rechten Maustaste für jede Forward-Lookupzone auf die Zone, klicken Sie dann auf **Eigenschaften**, und klicken Sie dann auf die Registerkarte **Server benennen**.  
  
6.  Klicken Sie auf einen Eintrag im Feld **Server benennen**, der auf de Quellserver verweist, klicken Sie auf **Entfernen**,und klicken Sie dann auf **OK**.  
  
7.  Wiederholen Sie die Schritte 5 und 6, bis sämtliche, auf den Quellserver zeigenden Elemente entfernt sind.  
  
8.  Klicken Sie auf **OK**, um das Dialogfeld **Eigenschaften** zu schließen.  
  
9. Erweitern Sie in der **DNS-Manager**-Konsole **Forward-Lookupzonen**.  
  
10. Wiederholen Sie die Schritte 6 bis 9, um alle Reverse-Lookupzonen zu entfernen, die auf den Quellserver verweisen.  
  
##  <a name="share-line-of-business-and-other-application-data-folders"></a><a name="BKMK_ShareLineOfBusinessAndOtherApplications"></a>Freigeben von Branchen-und anderen Anwendungsdaten Ordnern  
 Sie müssen die Berechtigungen für freigegebene Ordner und NTFS-Berechtigungen für die Branchen- und andere Anwendungsordner für Daten, die Sie auf den Zielserver kopiert haben, festlegen. Nachdem Sie die Berechtigungen festgelegt haben, werden die freigegebenen Ordner im Windows Server Essentials-Dashboard im Abschnitt " **Storage** " angezeigt.  
  
 Wenn Sie ein Anmeldeskript zum Zuordnen von Laufwerken für die freigegebenen Ordner verwenden, müssen Sie das Skript zum Zuordnen der Laufwerke auf dem Zielserver aktualisieren.  
  
##  <a name="fix-client-computer-issues-after-migrating"></a><a name="BKMK_FixClientComputerIssuesAfterMigrating"></a>Beheben von Problemen mit Client Computern nach der Migration  
 Bei der Migration zu Windows Server Essentials von Windows Small Business Server 2003 Premium Edition mit installiertem Microsoft Internet Security and Acceleration (ISA) Server haben Client Computer im Netzwerk weiterhin den Microsoft Firewall-Client und Internet Explorer für die Verwendung eines Proxy Servers konfiguriert.  
  
 Dies verursacht Konnektivitätsprobleme auf den Clientcomputern, da der Proxyserver nicht mehr vorhanden ist. Ist ein anderer Proxyserver konfiguriert, verwenden die Clientcomputer weiterhin den Server mit Windows SBS 2003 für den Proxyserver. Um dieses Problem zu beheben, müssen Sie den Internet Explorer neu konfigurieren, so dass er weder den Proxyserver noch den neuen Proxyserver verwendet.  
  
#### <a name="to-reconfigure-internet-explorer"></a>So konfigurieren Sie den Internet Explorer neu  
  
1.  Klicken Sie in Internet Explorer auf **Extras**, und klicken Sie dann auf **Internetoptionen**.  
  
2.  Klicken Sie auf der Registerkarte **Verbindungen** auf **LAN-Einstellungen**, und führen Sie eine der folgenden Optionen aus:  
  
    -   Wenn Sie keinen Proxyserver im Netzwerk verwenden, deaktivieren Sie alle Kontrollkästchen im Dialogfeld **Einstellungen für lokales Netzwerk (LAN)**.  
  
    -   Wenn Sie einen neuen Proxyserver im Netzwerk verwenden möchten:  
  
        1.  Deaktivieren Sie im Dialogfeld **Einstellungen für lokales Netzwerk (LAN)** die Kontrollkästchen im Abschnitt **Automatische Konfiguration**.  
  
        2.  Stellen Sie im Abschnitt **Proxyserver** sicher, dass beide Kontrollkästchen aktiviert sind.  
  
        3.  Geben Sie im Feld **Adresse** den vollqualifizierten Domänennamen (FQDN) des Proxyservers ein.  
  
        4.  Geben Sie im Feld **Port****80** ein.  
  
3.  Klicken Sie zweimal auf **OK**.  
  
4.  Navigieren Sie zu einer Website, um sicherzustellen, dass die Verbindungseinstellungen richtig sind.  
  
##  <a name="give-the-built-in-administrators-group-the-right-to-log-on-as-a-batch-job"></a><a name="BKMK_AdminGroup"></a>Der integrierten Gruppe "Administratoren" das Recht zum Anmelden als Batch Auftrag einräumen  
 Nach der Migration einer vorhandenen Windows Small Business Server 2003-Domäne zu Windows Server Essentials sollten Sie der integrierten Gruppe "Administratoren" das Recht zum Anmelden als Batch Auftrag einräumen. Stellen Sie sicher, dass die integrierte Administratorengruppe immer noch über die Berechtigung zum Anmelden als Stapelverarbeitungsauftrag auf dem Zielserver verfügt. Administratoren benötigen dieses Recht, um eine Warnung auf dem Zielserver auszuführen, ohne sich anzumelden.  
  
#### <a name="to-give-the-built-in-administrators-group-the-right-to-log-on-as-a-batch-job"></a>So erteilen Sie der integrierten Administratorengruppe das Recht zum Anmelden als Stapelverarbeitungsauftrag  
  
1. Öffnen Sie auf dem Zielserver das Verwaltungstool **Gruppenrichtlinienverwaltung**.  
  
2. Erweitern Sie in der Konsolen Struktur der **Gruppenrichtlinie Verwaltung** den Eintrag Gesamtstruktur **:** *<Servername \> *, erweitern Sie Domänen, und erweitern Sie dann den Server.  
  
3. Erweitern Sie **Domänencontroller**, klicken Sie mit der rechten Maustaste auf **Standard-Domänencontrollerrichtlinie**, und klicken Sie dann auf **Bearbeiten**.  
  
4. Klicken Sie in **Gruppenrichtlinienverwaltungs-Editor**auf **Standard Domänen Controller-Richtlinie** <em><Servername \> </em>**Richtlinie**, und erweitern Sie dann **Computer Konfiguration**.  
  
5. Erweitern Sie **Richtlinien**, erweitern Sie **Windows-Einstellungen** und erweitern Sie dann **Sicherheitseinstellungen**.  
  
6. Erweitern Sie in der Konsolenstruktur **Sicherheitseinstellungen**, **lokale Richtlinien**, und klicken Sie dann auf **Zuweisen von Benutzerrechten**.  
  
7. Klicken Sie im Ergebnisbereich mit der rechten Maustaste auf **Anmelden als Stapelverarbeitungsauftrag**, und klicken Sie dann auf Eigenschaften.  
  
8. Klicken Sie auf der Seite **Anmelden als Stapelverarbeitungsauftrag** auf **Benutzer oder Gruppe hinzufügen**.  
  
9. Klicken Sie im Dialogfeld auf **Benutzer oder Gruppe hinzufügen** auf **Durchsuchen**.  
  
10. Geben Sie im Dialogfeld **Benutzer, Computer oder Gruppen auswählen****Administrators** ein.  
  
11. Klicken Sie auf **Namen überprüfen**, um zu überprüfen, ob die integrierten Administratorengruppe angezeigt wird, und klicken Sie dann dreimal auf **OK**, um die Einstellung zu speichern.  
  
## <a name="see-also"></a>Weitere Informationen  
  

-   [Migration von Windows SBS 2003](Migrate-Windows-Small-Business-Server-2003-to-Windows-Server-Essentials.md)  
  
-   [Migrieren von Serverdaten zu Windows Server Essentials](Migrate-Server-Data-to-Windows-Server-Essentials.md)

