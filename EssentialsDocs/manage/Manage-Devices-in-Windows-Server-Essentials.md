---
title: Verwalten von Geräten in Windows Server Essentials
description: Beschreibt, wie Windows Server Essentials
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
ms.openlocfilehash: d740b71a2c3b9ed8ddb0ecfae6da2cf7d4f689a5
ms.sourcegitcommit: 2977c707a299929c6ab0d1e0adab2e1c644b8306
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/24/2019
ms.locfileid: "63720415"
---
# <a name="manage-devices-in-windows-server-essentials"></a>Verwalten von Geräten in Windows Server Essentials

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials
 
 In den folgenden Abschnitten werden die Geräteverwaltungsfunktionen eines Servers beschrieben und erläutert, sowie wie Sie Geräte im Netzwerk einrichten und verwenden:  
  
-   [Verwalten von Geräten mithilfe des Dashboards](Manage-Devices-in-Windows-Server-Essentials.md#BKMK_1)  
  
-   [Zuweisen von Benutzerkontenberechtigungen zum auf bestimmten Netzwerkcomputern anmelden](Manage-Devices-in-Windows-Server-Essentials.md#BKMK_2)  
  
-   [Entfernen eines Computers vom server](Manage-Devices-in-Windows-Server-Essentials.md#BKMK_3)  
  
-   [Konfigurieren der gruppenrichtlinieneinstellungen für ordnerumleitung und Sicherheit](Manage-Devices-in-Windows-Server-Essentials.md#BKMK_5)  
  
-   [Verbindung mit einem Netzwerkcomputer mithilfe einer Remotedesktopsitzung](Manage-Devices-in-Windows-Server-Essentials.md#BKMK_7)  
  
-   [Anzeigen von Computereigenschaften](Manage-Devices-in-Windows-Server-Essentials.md#BKMK_8)  
  
##  <a name="BKMK_1"></a> Verwalten von Geräten mithilfe des Dashboards  
 Windows Server Essentials ermöglicht es, die allgemeinen administrativen Aufgaben mithilfe des Windows Server Essentials-Dashboard auszuführen. Die Seite **Geräte** des Dashboards enthält Folgendes:  
  
-   Liste der Netzwerkcomputer mit folgenden Angaben:  
  
    -   Name des Computers  
  
    -   Status des Computers (**Online** oder **Offline**)  
  
    -   Beschreibung des Computers  
  
    -   Sicherungsstatus des Computers  
  
    -   Updatestatus des Computers  
  
    -   Sicherheitsstatus des Computers  
  
    -   Benachrichtigungsstatus des Computers  
  
    -   Gruppenrichtlinieninformationen zum Computer  
  
-   Einen Detailbereich mit zusätzlichen Informationen zu einem ausgewählten Computer  
  
-   Einen Aufgabenbereich, der eine Reihe von Aufgaben zur Geräteverwaltung wie etwa das Anzeigen von Computereigenschaften und Warnungen, das Einrichten einer Computersicherung und das Wiederherstellen von Dateien und Ordnern aus einer Sicherung enthält  
  
#### <a name="to-view-the-status-of-network-computers"></a>So zeigen Sie den Status von Netzwerkcomputern an  
  
1.  Öffnen Sie das Windows Server Essentials-Dashboard.  
  
2.  Klicken Sie auf der Navigationsleiste auf **Geräte**.  
  
3.  Zeigen Sie den Status aller Computer im Netzwerk im Listenbereich an.  
  
 Die folgende Tabelle beschreibt die verschiedenen Computer und Sicherungsaufgaben, die im Windows Server Essentials-Dashboard verfügbar sind. Einige Aufgaben sind computerspezifisch und nur sichtbar, wenn Sie einen Computer in der Liste auswählen.  
  
### <a name="computer-tasks-in-the-dashboard"></a>Computeraufgaben im Dashboard  
  
|Aufgabenname|Beschreibung|  
|---------------|-----------------|  
|Computereigenschaften anzeigen|Zeigt allgemeine Informationen zu einem ausgewählten Computer an, und ermöglicht Ihnen das Anzeigen der Details zu den Computersicherungen.|  
|Sicherung für diesen Computer einrichten|Führt den Assistenten zum Einrichten der Sicherung aus.|  
|Sicherung für den Computer anpassen|Öffnet die Sicherungseigenschaften, in denen Sie die Sicherungseinstellungen für den ausgewählten Computer ändern können.|  
|Sicherung für den Computer starten|Startet eine Sicherung für den ausgewählten Computer.|  
|Sicherung für den Computer beenden|Beendet die Sicherung für einen ausgewählten Computer.|  
|Dateien oder Ordner für den Computer wiederherstellen|Führt den Assistenten zum Wiederherstellen von Dateien und Ordnern aus, mit dem Sie bestimmte Dateien, Ordner oder Laufwerke wiederherstellen können.|  
|Warnungen für den Computer anzeigen|Zeigt wichtige und andere informative Warnungen an, und ermöglicht es Ihnen, gegebenenfalls Korrekturmaßnahmen durchzuführen.|  
|Remotedesktop auf dem Computer|Öffnet eine Remotedesktopverbindung zum ausgewählten Computer.|  
|Computer entfernen|Führt den Assistenten zum Entfernen eines Computers aus, der den Computer vom Windows Server Essentials-Dashboard trennt.|  
|Einstellungen für Computersicherung und Dateiversionsverlauf anpassen|Öffnet die Seite mit den Sicherungseinstellungen, über die Sie den Sicherungszeitplan und Einstellungen für den Dateiversionsverlauf für Clientcomputer ändern können.|  
|Wie werden Computer mit dem Server verbunden?|Öffnet ein Hilfethema, das die Schritte zum Hinzufügen eines Computers zum Netzwerk beschreibt.|  
|Gruppenrichtlinie implementieren|Wendet Richtlinieneinstellungen auf Windows 8- und Windows 7-Computer an, die der Domäne beigetreten sind.|  
  
##  <a name="BKMK_2"></a> Zuweisen von Benutzerkontenberechtigungen zum auf bestimmten Netzwerkcomputern anmelden  
 Sie können Benutzerkonten Berechtigungen zuweisen, sodass Benutzer sich nur auf bestimmten Netzwerkcomputern anmelden können, wenn von einem Remotestandort aus auf das Windows Server Essentials-Netzwerk zugegriffen wird.  
  
#### <a name="to-change-the-computer-access-for-a-user-account"></a>So ändern Sie den Computerzugriff für ein Benutzerkonto  
  
1.  Öffnen Sie das Windows Server Essentials-Dashboard.  
  
2.  Klicken Sie auf der Navigationsleiste auf **Benutzer**.  
  
3.  Wählen Sie in der Liste von Benutzerkonten das Benutzerkonto aus, das Sie ändern möchten.  
  
4.  In der **< Benutzerkonto\> Aufgaben** Bereich, klicken Sie auf **Kontoeigenschaften anzeigen**. Die Seite **Eigenschaften** für das Benutzerkonto wird angezeigt.  
  
5.  Wählen Sie auf der Registerkarte **Computerzugriff** den Computer aus, auf den dieser Benutzer remote zugreifen kann, und klicken Sie dann auf **OK**.  
  
##  <a name="BKMK_3"></a> Entfernen eines Computers vom server  
 Wenn Sie einen Computer von einem Server, auf dem Windows Server Essentials ausgeführt wird, mithilfe des Dashboards entfernen, wird er nicht mehr vom Server verwaltet. Daher wird der Server das Erstellen von Computersicherungen oder die Überwachung seines Zustands nach dem Entfernen aus dem Netzwerk beenden.  
  
> [!NOTE]
>  Entfernen eines Computers vom Server trennt den Computer nicht vom Netzwerk. Der Computer kann weiterhin so auf Ressourcen im Netzwerk zugreifen, wie er es konnte, bevor er mit dem Server verbunden wurde. Um zu verhindern, dass der Computer Zugriff auf Serverressourcen hat, und um ihn vom Server zu trennen, müssen Sie den Computer aus der Domäne entfernen. Darüber hinaus wird beim Entfernen des Computers vom Server nicht automatisch die Connector-Software oder das Launchpad auf dem Computer, der entfernt wird, deinstalliert. Sie müssen die Connector-Software manuell vom Computer entfernen. Weitere Informationen finden Sie im Abschnitt zu deinstallieren die Connector-Software in [Verbindungsherstellung](../use/Get-Connected-in-Windows-Server-Essentials.md).  
  
#### <a name="to-remove-a-computer-from-the-network-by-using-the-dashboard"></a>So entfernen Sie mithilfe des Dashboards einen Computer aus dem Netzwerk  
  
1.  Öffnen Sie das Windows Server Essentials-Dashboard.  
  
2.  Klicken Sie auf der Navigationsleiste auf die Registerkarte **Geräte** .  
  
3.  Rechtsklicken Sie in der Liste der Computer auf den Computer, den Sie aus dem Netzwerk entfernen möchten, und klicken Sie dann auf **Computer entfernen**.  
  
##  <a name="BKMK_5"></a> Konfigurieren der gruppenrichtlinieneinstellungen für ordnerumleitung und Sicherheit  
 Sie können eine Gruppenrichtlinie konfigurieren und mithilfe von Windows Server Essentials-Dashboard auf Computern im Windows Server Essentials-Netzwerk bereitstellen. Gruppenrichtlinien in Windows Server Essentials enthalten Einstellungen für Ordnerumleitung und Sicherheit, die Auswirkungen auf Windows Update, Windows Defender und die Netzwerkfirewall haben.  
  
#### <a name="to-configure-group-policy-in-windows-server-essentials"></a>So konfigurieren Sie Gruppenrichtlinien in Windows Server Essentials  
  
1.  Öffnen Sie das Windows Server Essentials-Dashboard.  
  
2.  Klicken Sie auf der Navigationsleiste auf **GERÄTE**.  
  
3.  Für Windows Server Essentials: Klicken Sie im globalen Bereich**Benutzeraufgaben** auf **Gruppenrichtlinie implementieren**.  
  
     Für Windows Server Essentials: Klicken Sie im globalen Bereich**Geräteaufgaben** auf **Gruppenrichtlinie implementieren**.  
  
4.  Der Assistent zur Implementierung von Gruppenrichtlinien wird geöffnet.  
  
5.  Auf der Seite **Gruppenrichtlinie für Ordnerumleitung aktivieren** des Assistenten können Sie die Benutzerordner auswählen, auf die Sie umleiten möchten.  
  
6.  Auf der Seite **Sicherheitsrichtlinieneinstellungen aktivieren** des Assistenten können Sie Gruppenrichtlinieneinstellungen für **Windows Update**, **Windows Defender**und die **Netzwerkfirewall**auswählen.  
  
7.  Klicken Sie auf **Fertig stellen** , um die Gruppenrichtlinieneinstellungen zu implementieren.  
  
##  <a name="BKMK_7"></a> Verbindung mit einem Netzwerkcomputer mithilfe einer Remotedesktopsitzung  
 Um Remote Ihren Windows Server Essentials-Netzwerkcomputer zuzugreifen, wenn Sie nicht im Büro sind, mithilfe Ihres Webbrowsers, um für Remotewebzugriff Ihrer Organisation s Remote Web Access-Website anzumelden, und auf die **Computer** Registerkarte, klicken Sie auf den Namen des der Computer, auf.  
  
 Die Spalte **Status** zeigt an, ob Sie eine Verbindung zu einem Computer in Ihrem Netzwerk herstellen können, und kann die folgenden Werte enthalten:  
  
-   **Verfügbar**  
  
     Der Computer ist eingeschaltet ist und für eine Remoteverbindung verfügbar. Auch wenn dieser Status angezeigt wird, können Sie möglicherweise trotzdem keine Verbindung mit diesem Computer herstellen, wenn eine Drittanbieterfirewall die Verbindung blockiert.  
  
-   **Offline oder im Ruhezustand**  
  
     Der Computer ist ausgeschaltet oder befindet sich im Standbymodus oder im Ruhezustandmodus. Wenn ein Computer offline oder im Ruhezustand ist, wird der Status in Echtzeit aktualisiert, damit Sie wissen, wenn der Computer verfügbar ist.  
  
-   **Nicht unterstütztes Betriebssystem**  
  
     Das Betriebssystem auf dem Computer unterstützt keinen Remotedesktop. Es kann bis zu sechs Stunden dauern, bis der Status auf dem Server aktualisiert wird, wenn eine Änderung durchgeführt wird.  
  
-   **Verbindung ist deaktiviert.**  
  
     Die Computerverbindung wird entweder durch eine Firewall blockiert, oder der Remotedesktop ist auf dem Computer oder durch eine Gruppenrichtlinie deaktiviert. Es kann bis zu sechs Stunden dauern, bis der Status auf dem Server aktualisiert wird, wenn eine Änderung durchgeführt wird.  
  
##  <a name="BKMK_8"></a> Anzeigen von Computereigenschaften  
 Der Abschnitt **Geräte** des Windows Server Essentials-Dashboards zeigt eine Liste mit Netzwerkcomputern an. Die Liste enthält auch zusätzliche Informationen zu jedem Computer.  
  
#### <a name="to-view-a-list-of-computers"></a>So zeigen Sie eine Liste von Computern an  
  
1.  Öffnen Sie das Windows Server Essentials-Dashboard.  
  
2.  Klicken Sie auf der Hauptnavigationsleiste auf **Geräte**.  
  
3.  Das Dashboard zeigt eine aktuelle Liste der Computer an.  
  
#### <a name="to-view-or-change-properties-for-a-computer"></a>So zeigen Sie an oder ändern Eigenschaften für einen Computer  
  
1.  Wählen Sie in der Liste der Computer das Konto aus, für das Sie Eigenschaften anzeigen oder ändern möchten.  
  
2.  In der **< Computername\> Aufgaben** Bereich, klicken Sie auf **Computereigenschaften anzeigen**. Die Seite **Eigenschaften** für die Computer wird angezeigt.  
  
3.  Klicken Sie auf eine Registerkarte, um die Eigenschaften für diesen Computer anzuzeigen.  
  
4.  Klicken Sie zum Speichern von Änderungen an den Computereigenschaften auf **Übernehmen**.  
  
## <a name="see-also"></a>Siehe auch  
  
-   [Verwalten des Remotewebzugriffs](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md)  
  
-   [Verwenden des Remotewebzugriffs](../use/Use-Remote-Web-Access-in-Windows-Server-Essentials.md)  
  
-   [Verwalten von Benutzerkonten, die mithilfe des Dashboards](Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Manage8)  
  
-   [Verwalten von Windows Server Essentials](Manage-Windows-Server-Essentials.md)  
  
-   [Verwenden von Windows Server Essentials](../use/Use-Windows-Server-Essentials.md)
