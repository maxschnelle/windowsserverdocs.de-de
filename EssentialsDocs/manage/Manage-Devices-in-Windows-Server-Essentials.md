---
title: "Verwalten von Geräten in Windows Server Essentials"
description: Beschreibt, wie Sie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f5fe1088-ebe7-4799-a47d-075b0048dea1
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 288d62a3fe4d9073ba2c0e3fdff385d8317f20d4
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="manage-devices-in-windows-server-essentials"></a>Verwalten von Geräten in Windows Server Essentials

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials
 
 In den folgenden Abschnitten werden die Geräteverwaltungsfunktionen eines Servers, und führen Sie zum Einrichten und Verwenden von Geräten in Ihrem Netzwerk:  
  
-   [Verwalten von Geräten mithilfe des Dashboards](Manage-Devices-in-Windows-Server-Essentials.md#BKMK_1)  
  
-   [Zuweisen von Benutzerkontenberechtigungen auf bestimmten Netzwerkcomputern anmelden](Manage-Devices-in-Windows-Server-Essentials.md#BKMK_2)  
  
-   [Entfernen eines Computers vom server](Manage-Devices-in-Windows-Server-Essentials.md#BKMK_3)  
  
-   [Konfigurieren der gruppenrichtlinieneinstellungen für ordnerumleitung und Sicherheit](Manage-Devices-in-Windows-Server-Essentials.md#BKMK_5)  
  
-   [Verbinden Sie mit einem Computer im Netzwerk mithilfe einer Remotedesktopsitzung](Manage-Devices-in-Windows-Server-Essentials.md#BKMK_7)  
  
-   [Anzeigen von Computereigenschaften](Manage-Devices-in-Windows-Server-Essentials.md#BKMK_8)  
  
##  <a name="BKMK_1"></a>Verwalten von Geräten mithilfe des Dashboards  
 Windows Server Essentials ermöglicht die allgemeine administrative Aufgaben mithilfe von Windows Server Essentials-Dashboard ausführen. Die **Geräte** -Seite des Dashboards bietet Folgendes:  
  
-   Eine Liste von Computern im Netzwerk, das anzeigt:  
  
    -   Der Name des Computers  
  
    -   Der Status des Computers, entweder **Online** oder **Offline**  
  
    -   Die Beschreibung eines Computers  
  
    -   Der Sicherungsstatus des Computers  
  
    -   Der Aktualisierungsstatus des Computers  
  
    -   Der Sicherheitsstatus des Computers  
  
    -   Benachrichtigungsstatus des Computers  
  
    -   Informationen zur Richtlinie für den computer  
  
-   Ein Detailbereich mit zusätzlichen Informationen zu einem ausgewählten computer  
  
-   Ein Aufgabenbereich, der eine Reihe von Gerät administrative Aufgaben wie das Anzeigen von Computereigenschaften und Warnungen, Sicherung einrichten und Wiederherstellen von Dateien und Ordnern aus einer Sicherung enthält  
  
#### <a name="to-view-the-status-of-network-computers"></a>Anzeigen des Status von Computern im Netzwerk  
  
1.  Öffnen Sie das Windows Server Essentials-Dashboard.  
  
2.  Klicken Sie auf der Navigationsleiste auf **Geräte**.  
  
3.  Anzeigen des Status aller Computer im Netzwerk im Listenbereich an.  
  
 Die folgende Tabelle beschreibt die verschiedenen Computer und Sicherungsaufgaben, die in Windows Server Essentials-Dashboard verfügbar sind. Einige Aufgaben sind computerspezifisch, und sie werden nur angezeigt, wenn Sie einen Computer in der Liste auswählen.  
  
### <a name="computer-tasks-in-the-dashboard"></a>Computeraufgaben im Dashboard  
  
|Den Namen der Aufgabe|Beschreibung|  
|---------------|-----------------|  
|Computereigenschaften anzeigen|Zeigt allgemeine Informationen für einen ausgewählten Computer, und ermöglicht Ihnen das Anzeigen von Details zu den computersicherungen.|  
|Sicherung für diesen Computer einrichten|Führt die Sicherung-Assistenten.|  
|Sicherung für den Computer anpassen|Öffnet die sicherungseigenschaften, von denen Sie die sicherungseinstellungen für den ausgewählten Computer ändern können.|  
|Starten Sie eine Sicherung für den computer|Startet eine Sicherung für einen ausgewählten Computer.|  
|Sicherung für den Computer beenden|Beendet die Sicherung für einen ausgewählten Computer.|  
|Wiederherstellen von Dateien oder Ordner für den computer|Führt die Wiederherstellen von Dateien und Ordner-Assistent, der Sie bestimmte Dateien, Ordner oder Laufwerke wiederherstellen können.|  
|Anzeigen von Warnungen für den computer|Zeigt wichtige und andere informative Warnungen an und ermöglicht es Ihnen, korrekturmaßnahmen durchzuführen.|  
|Remotedesktop auf dem computer|Wird der Remotedesktopverbindung zum ausgewählten Computer geöffnet.|  
|Entfernen Sie den computer|Führt die entfernen eine Computer-Assistenten, der den Computer vom Windows Server Essentials-Dashboard trennt.|  
|Anpassen der computersicherung und Dateiversionsverlauf-Einstellungen|Öffnet die Einstellungen für die Seite, von der Sie den Sicherungszeitplan und Einstellungen für Dateiversionsverlauf für Client Computer ändern können.|  
|Wie werden Computer mit dem Server verbunden?|Öffnet ein Hilfethema, das beschreibt die Schritte zum Hinzufügen eines Computers mit dem Netzwerk.|  
|Implementieren von Gruppenrichtlinien|Wendet Richtlinieneinstellungen auf Windows 8 und Windows 7-Computern, die der Domäne angehören.|  
  
##  <a name="BKMK_2"></a>Zuweisen von Benutzerkontenberechtigungen auf bestimmten Netzwerkcomputern anmelden  
 Sie können Benutzerkonten Berechtigungen zuweisen, sodass Benutzer sich nur auf bestimmten Netzwerkcomputern anmelden können beim Windows Server Essentials-Netzwerk von einem Remotestandort aus Zugriff auf.  
  
#### <a name="to-change-the-computer-access-for-a-user-account"></a>So ändern Sie den Computerzugriff für ein Benutzerkonto  
  
1.  Öffnen Sie das Windows Server Essentials-Dashboard.  
  
2.  Klicken Sie auf der Navigationsleiste auf **Benutzer**.  
  
3.  Wählen Sie in der Liste der Benutzerkonten das Benutzerkonto, das Sie ändern möchten.  
  
4.  In der **< Benutzer Zuordnung überprüfen\ > Aufgaben** Bereich, klicken Sie auf **Kontoeigenschaften anzeigen**. Die **Eigenschaften** Seite für das Benutzerkonto, das angezeigt wird.  
  
5.  Auf der **Zugriff auf den Computer** Registerkarte, wählen Sie den Computer, die diese Benutzer remote zugreifen kann, und klicken Sie dann auf **OK**.  
  
##  <a name="BKMK_3"></a>Entfernen eines Computers vom server  
 Wenn Sie einen Computer von einem Server, die Windows Server Essentials ausgeführt wird, mithilfe des Dashboards entfernen, wird er nicht mehr vom Server verwaltet. Daher wird der Server keine Erstellung von computersicherungen oder Überwachung seines Zustands nach dem Entfernen aus dem Netzwerk.  
  
> [!NOTE]
>  Entfernen eines Computers vom Server nicht den Computer vom Netzwerk getrennt. Der Computer kann weiterhin Ressourcen im Netzwerk auf die gleiche Weise zugreifen, die es konnte, bevor Sie mit dem Server verbunden wird. Um zu verhindern, dass den Computer Zugriff auf Serverressourcen und vom Server zu trennen, müssen Sie den Computer aus der Domäne entfernen. Darüber hinaus wird zum Entfernen des Computers vom Server nicht automatisch die Connector-Software oder das Launchpad auf dem Computer deinstalliert, der entfernt wird. Sie müssen die Connector-Software manuell vom Computer entfernen. Weitere Informationen finden Sie im Abschnitt deinstallieren die Connector-Software in [Herstellen einer Verbindung](../use/Get-Connected-in-Windows-Server-Essentials.md).  
  
#### <a name="to-remove-a-computer-from-the-network-by-using-the-dashboard"></a>Zum Entfernen eines Computers aus dem Netzwerk, über das Dashboard  
  
1.  Öffnen Sie das Windows Server Essentials-Dashboard.  
  
2.  Klicken Sie auf der Navigationsleiste auf die **Geräte** Registerkarte.  
  
3.  In der Liste der Computer, mit der Maustaste des Computers, die Sie verwenden möchten, aus dem Netzwerk entfernen, und klicken Sie dann auf **entfernen Sie den Computer**.  
  
##  <a name="BKMK_5"></a>Konfigurieren der gruppenrichtlinieneinstellungen für ordnerumleitung und Sicherheit  
 Sie können eine Gruppenrichtlinie konfigurieren und mithilfe von Windows Server Essentials-Dashboard auf Computern in Windows Server Essentials-Netzwerk bereitstellen. Gruppenrichtlinien in Windows Server Essentials enthält Einstellungen für ordnerumleitung und Sicherheit, die Auswirkungen auf Windows Update, Windows Defender und der Netzwerk-Firewall.  
  
#### <a name="to-configure-group-policy-in-windows-server-essentials"></a>So konfigurieren Sie Gruppenrichtlinien in Windows Server Essentials  
  
1.  Öffnen Sie das Windows Server Essentials-Dashboard.  
  
2.  Klicken Sie auf der Navigationsleiste auf **Geräte**.  
  
3.  Für Windows Server Essentials: Im globalen **Benutzeraufgaben** Bereich, klicken Sie auf **Gruppenrichtlinie implementieren**.  
  
     Für Windows Server Essentials: Im globalen **Geräteaufgaben** Bereich, klicken Sie auf **Gruppenrichtlinie implementieren**.  
  
4.  Der Assistent zum Implementieren von Gruppenrichtlinien wird geöffnet.  
  
5.  Auf der **aktivieren Gruppenrichtlinie zur Ordnerumleitung** Seite des Assistenten können Sie die Benutzerordner, die Sie umleiten möchten.  
  
6.  Auf der **Sicherheitsrichtlinieneinstellungen aktivieren** Seite des Assistenten können Sie gruppenrichtlinieneinstellungen für **Windows Update**, **Windows Defender**, und die **Netzwerkfirewall**.  
  
7.  Klicken Sie auf **Fertig stellen** um die gruppenrichtlinieneinstellungen zu implementieren.  
  
##  <a name="BKMK_7"></a>Verbinden Sie mit einem Computer im Netzwerk mithilfe einer Remotedesktopsitzung  
 Ihre Windows Server Essentials-Netzwerkcomputer Remotezugriff, wenn Sie nicht im Büro sind, mithilfe eines Webbrowsers, melden Sie sich bei Ihrer Organisation s Remote Web Access-Website und auf die **Computer** auf den Namen des Computers.  
  
 Die **Status** Spalte zeigt an, ob Sie auf einem Computer in Ihrem Netzwerk herstellen können und können die folgenden Werte enthalten:  
  
-   **Verfügbar**  
  
     Der Computer eingeschaltet ist und für eine Remoteverbindung verfügbar ist. Auch wenn dieser Status angezeigt wird, können Sie möglicherweise trotzdem nicht auf diesem Computer herstellen, wenn eine Drittanbieterfirewall die Verbindung blockiert.  
  
-   **Offline oder im Ruhezustand**  
  
     Der Computer ist ausgeschaltet oder befindet sich im Energiesparmodus oder Ruhezustand befindet. Wenn ein Computer offline oder im Ruhezustand ist, wird der Status in Echtzeit aktualisiert, damit Sie ermitteln können, wenn der Computer verfügbar ist.  
  
-   **Nicht unterstütztes Betriebssystem**  
  
     Das Betriebssystem auf dem Computer unterstützt Remotedesktop nicht. Es kann für den Status auf dem Server aktualisiert werden, wenn eine Änderung von bis zu sechs Stunden dauern.  
  
-   **Verbindung ist deaktiviert.**  
  
     Die computerverbindung wird entweder durch eine Firewall blockiert, oder der Remotedesktop auf dem Computer oder durch eine Gruppenrichtlinie deaktiviert ist. Es kann für den Status auf dem Server aktualisiert werden, wenn eine Änderung von bis zu sechs Stunden dauern.  
  
##  <a name="BKMK_8"></a>Anzeigen von Computereigenschaften  
 Die **Geräte** Abschnitt des Windows Server Essentials-Dashboards zeigt eine Liste von Computern im Netzwerk. Die Liste enthält auch zusätzliche Informationen zu jedem Computer.  
  
#### <a name="to-view-a-list-of-computers"></a>Zum Anzeigen einer Liste von Computern  
  
1.  Öffnen Sie das Windows Server Essentials-Dashboard.  
  
2.  Klicken Sie auf der Hauptnavigationsleiste auf **Geräte**.  
  
3.  Das Dashboard zeigt eine aktuelle Liste der Computer.  
  
#### <a name="to-view-or-change-properties-for-a-computer"></a>Zum Anzeigen oder Ändern von Eigenschaften für einen computer  
  
1.  Wählen Sie in der Liste der Computer das Konto für das Sie Eigenschaften anzeigen oder ändern möchten.  
  
2.  In der **< Computername\ > Aufgaben** Bereich, klicken Sie auf **Computereigenschaften anzeigen**. Die **Eigenschaften** Seite für die Computer wird angezeigt.  
  
3.  Klicken Sie auf eine Registerkarte, um die Eigenschaften für diesen Computer anzeigen.  
  
4.  Um die Änderungen zu speichern, die Sie den Eigenschaften vornehmen, klicken Sie auf **übernehmen**.  
  
## <a name="see-also"></a>Siehe auch  
  
-   [Verwalten des Remotewebzugriffs](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md)  
  
-   [Verwenden von Web Access](../use/Use-Remote-Web-Access-in-Windows-Server-Essentials.md)  
  
-   [Verwalten von Benutzerkonten, die über das Dashboard](Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Manage8)  
  
-   [Verwalten von Windows Server Essentials](Manage-Windows-Server-Essentials.md)  
  
-   [Verwenden von Windows Server Essentials](../use/Use-Windows-Server-Essentials.md)
