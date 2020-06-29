---
title: Übersicht über das Launchpad in Windows Server Essentials
description: Beschreibt die Verwendung von Windows Server Essentials
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: 198d16cb-3d07-4706-be89-ad14a5f7dc47
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: e3a25a574e932d9a6a66ca706472dfed5a67a6ee
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/27/2020
ms.locfileid: "85470415"
---
# <a name="overview-of-the-launchpad-in-windows-server-essentials"></a>Übersicht über das Launchpad in Windows Server Essentials

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Beim Windows Server Essentials-Launchpad handelt es sich um eine kleine Anwendung, die auf einem Computer installiert wird, wenn der Computer zum ersten Mal eine Verbindung mit dem Server herstellt. Das Launchpad bietet authentifizierten Benutzern Zugriff auf die wichtigsten Features von Windows Server Essentials, dazu zählen u. a. Computersicherungen, freigegebene Dateien und Medien und die Website für Remotewebzugriff. Benutzer können über Computer, die Mitglied der Domäne sind, oder über Computer, die nicht Mitglied der Domäne sind, auf diese Funktionen zugreifen. Das Launchpad bietet auch Echtzeitinformationen und Benachrichtigungen über den Zustand des Computers. Mit dem Launchpad können Administratoren auf das Serverdashboard zugreifen, selbst wenn der Computer nicht mit dem Netzwerk verbunden ist.

 OEMs und unabhängige Softwarehersteller, die Add-Ins für Windows Server Essentials entwickeln, können mit dem Launchpad die Add-In-Funktionalität auf Computern im Netzwerk erweitern.

 Die folgenden Windows-Betriebssysteme unterstützen die Verwendung des Windows Server Essentials-Launchpads:

- **Windows 8**: alle Editionen.

- **Windows 7**: alle Editionen.
- **Windows 10**: alle Editionen.

  Die folgenden Betriebssysteme unterstützen die Verwendung des Windows Server Essentials-Launchpads nicht:

- **Zusätzliche Server**: Das Windows Server Essentials-Launchpad kann nicht auf zusätzlichen Computern ausgeführt werden, auf denen das Windows Server-Betriebssystem läuft.

  Inhalte dieses Themas:

- [Verwenden des Launchpads](Overview-of-the-Launchpad-in-Windows-Server-Essentials.md#BKMK_Launchpad)

- [Verwenden des Launchpads mit einem Macintosh-Computer](Overview-of-the-Launchpad-in-Windows-Server-Essentials.md#BKMK_Mac)

##  <a name="use-the-launchpad"></a><a name="BKMK_Launchpad"></a>Verwenden des Launchpad
 Die folgenden Links und Informationen sind auf dem Windows Server Essentials-Launchpad verfügbar.

### <a name="backup"></a>Backup
 Klicken Sie auf **Sicherung**, um die **Eigenschaften der Sicherung** für den Computer aufzurufen. Auf der Seite **Eigenschaften der Sicherung** können Sie Folgendes durchführen:

- Starten oder Beenden einer Sicherung

- Anzeigen des Status und der Details für die aktuelle Sicherung

- Festlegen, wie die Rechenleistung verwaltet wird, wenn die Sicherung ausgeführt wird

  Informationen dazu, wie Sie Launchpad zum Sichern des Computers verwenden, finden Sie unter [Verwalten der Client Sicherung](Manage-Client-Computer-Backup-in-Windows-Server-Essentials.md).

### <a name="remote-web-access"></a>Remotewebzugriff
 Klicken Sie auf **Remotewebzugriff**, um den Webbrowser für die Remotewebzugriffssite zu öffnen. Mithilfe der Website für den Remotewebzugriff können Sie eine Verbindung mit anderen Computern herstellen und auf einige der Netzwerkressourcen innerhalb des Büros oder von einem beliebigen Remotestandort aus mit einem internetfähigen Computer zugreifen. Weitere Informationen zu Remote Webzugriff finden Sie unter [Manage Remote Webzugriff](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md).

### <a name="shared-folders"></a>Freigegebene Ordner
 Klicken Sie auf **Freigegebene Ordner**, um Windows-Explorer am Speicherort der freigegebenen Ordner auf dem Server zu öffnen. Informationen zum Freigeben von Dateien und Ordnern finden Sie im Thema [Verwalten von Server Ordnern](Manage-Server-Folders-in-Windows-Server-Essentials.md).

### <a name="dashboard"></a>Dashboard
 Klicken Sie auf  **Dashboard** , um die Seite **Anmelden** zu öffnen, sodass auf das Windows Server Essentials-Dashboard zugegriffen werden kann. Nachdem Sie sich angemeldet haben, wird eine Remotedesktopverbindung mit dem Serverdashboard hergestellt. Weitere Informationen zum Dashboard finden Sie unter [Übersicht](Overview-of-the-Dashboard-in-Windows-Server-Essentials.md)über das Dashboard.

> [!NOTE]
>  Um dieses Feature verwenden zu können, müssen Sie über die entsprechenden Berechtigungen verfügen, um sich auf dem Server anmelden zu können.

### <a name="microsoft-office-365"></a>Microsoft Office 365
 Der **Microsoft Office 365** -Link wird nur auf dem Launchpad angezeigt, wenn der Benutzer über ein Office 365-Konto verfügt. Klicken Sie auf  **Microsoft Office 365** , um auf weitere Links zu Office 365-Ressourcen zuzugreifen. Weitere Informationen finden Sie unter [Schnellstarthandbuch to using Microsoft Office 365](../use/Quick-Start-Guide-to-Using-Microsoft-Office-365-with-Windows-Server-Essentials.md).

### <a name="computer-health-alerts"></a>Computer-Integritätswarnungen
 Warnungen, die auf dem Launchpad angezeigt werden, bieten einen schnellen Überblick hinsichtlich der aktuellen Integrität des Computers. Klicken Sie zum Anzeigen von Informationen zu einer Integritätswarnung auf ein Warnsymbol, um die Meldungsanzeige zu öffnen. Integritätswarnungen erscheinen basierend auf dem Schweregrad in der Anzeige. Die schwerwiegendsten Warnungen werden zuerst in der Liste angezeigt. Weniger schwerwiegende Warnungen werden weiter unten in der Liste angezeigt. Weitere Informationen zu Integritäts Warnungen für Computer finden Sie unter [Verwalten der System](Manage-System-Health-in-Windows-Server-Essentials.md)Integrität.

##  <a name="use-the-launchpad-with-a-mac-computer"></a><a name="BKMK_Mac"></a>Verwenden des LaunchPads mit einem Macintosh-Computer
 Sie können einen Macintosh- &reg; Computer &reg; , auf dem Mac OS X 10,5 oder höher ausgeführt wird, mit Windows Server Essentials, Windows Server Essentials oder Windows Server 2012 R2 verbinden oder die Connector-Software herunterladen und installieren. Wenn Sie die Installation der Connector-Software beendet haben, können Sie auswählen, dass das Launchpad beim Systemstart automatisch gestartet wird.

 Beim Launchpad handelt es sich um eine kleine Anwendung, die authentifizierten Benutzern Zugriff auf die wichtigsten Features des Servers bietet, dazu zählen u. a. freigegebene Dateien und Medien, Add-Ins und der Remotewebzugriff. Das Launchpad bietet auch Echtzeitinformationen und Benachrichtigungen über den Zustand des Computers.

> [!NOTE]
>  Serveradministratoren können das Launchpad oder den Remotewebzugriff auf einem Macintosh-Computer nicht nutzen, um das Serverdashboard zu öffnen und den Server zu verwalten.

### <a name="backup"></a>Backup
 Klicken Sie auf **Sicherung**, um Time Machine einzurichten, sodass Sie Ihren Computer sichern und die Time Machine-Einstellungen ändern können. Weitere Informationen zu Time Machine finden Sie in der Dokumentation Ihres Computerherstellers.

### <a name="remote-web-access"></a>Remotewebzugriff
 Klicken Sie auf **Remote Webzugriff** , um den Webbrowser für die Remote Webzugriff Website zu öffnen. Der Remote Webzugriff ermöglicht Ihnen den Zugriff auf die freigegebenen Dateien und Ordner auf dem Server von einem beliebigen Remote Standort aus mit einem Internet fähigen Computer. Sie können Dateien hochladen, Musik und Videos über webbasierte Medien wiedergeben sowie Bilder anzeigen und Bildschirmpräsentationen wiedergegeben. Weitere Informationen finden Sie unter [Verwenden von Remote Webzugriff](../use/Use-Remote-Web-Access-in-Windows-Server-Essentials.md).

### <a name="shared-folders"></a>Freigegebene Ordner
 Klicken Sie auf **Freigegebene Ordner**, um Finder am Speicherort der freigegebenen Ordner auf dem Server zu öffnen. Weitere Informationen zum Freigeben von Dateien und Ordnern finden Sie unter Verwenden von frei [gegebenen Ordnern](../use/Use-Shared-Folders-in-Windows-Server-Essentials.md).

### <a name="computer-health-alerts"></a>Computer-Integritätswarnungen
 Warnungen, die auf dem Launchpad angezeigt werden, bieten einen schnellen Überblick hinsichtlich der aktuellen Integrität des Computers. Klicken Sie zum Anzeigen von Informationen zu einer Integritätswarnung auf ein Warnsymbol, um die Meldungsanzeige zu öffnen. Integritätswarnungen erscheinen basierend auf dem Schweregrad in der Anzeige. Die schwerwiegendsten Warnungen werden zuerst in der Liste angezeigt. Weniger schwerwiegende Warnungen werden weiter unten in der Liste angezeigt.

## <a name="additional-references"></a>Zusätzliche Referenzen

-   [Verbindung herstellen](../use/Get-Connected-in-Windows-Server-Essentials.md)

-   [Verwenden von Windows Server Essentials](../use/Use-Windows-Server-Essentials.md)

-   [Verwalten von Windows Server Essentials](Manage-Windows-Server-Essentials.md)
