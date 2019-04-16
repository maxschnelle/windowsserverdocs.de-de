---
title: Konfigurieren einer Server Core-Installation von Windows Server mit „Sconfig.cmd“
description: Erläutert die Verwendung von „Sconfig.cmd“
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.date: 10/17/2017
ms.technology: server-general
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e6cac074-c6fc-46dd-9664-fa0342c0a5e8
author: jaimeo
ms.author: jaimeo
manager: dongill
ms.localizationpriority: high
ms.openlocfilehash: 2473b4ffae79c29ec7505616c139c03b21a4427b
ms.sourcegitcommit: e0479b0114eac7f232e8b1e45eeede96ccd72b26
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/22/2018
ms.locfileid: "1284348"
---
# <a name="configure-a-server-core-installation-of-windows-server-2016-or-windows-server-version-1709-with-sconfigcmd"></a>Konfigurieren einer Server Core-Installation von Windows Server mit „Sconfig.cmd“
> Gilt für: Windows Server (Semi-Annual Channel) and Windows Server 2016

In der Version 1709 von Windows Server2016 können Sie das Server-Konfigurationstool (Sconfig.cmd) zum Konfigurieren und Verwalten verschiedener allgemeiner Aspekte von Server Core-Installationen verwenden. Sie müssen Mitglied der Gruppe %%amp;quot;Administratoren%%amp;quot; sein, um das Tool verwenden zu können.  
  
Sie können „Sconfig.cmd“ in Installationen von Server Core und Server mit Desktopdarstellung (nur Windows Server 2016) verwenden. 
  
## <a name="start-the-server-configuration-tool"></a>Starten Sie das Serverkonfigurationstool  
  
1.  Wechseln Sie zum Systemlaufwerk.  
  
2.  Geben Sie `Sconfig.cmd` ein, und drücken Sie die EINGABETASTE. Die Benutzeroberfläche des Server-Konfigurationstools wird geöffnet:  
  
 <img src="mainsconfigpage.png" style='float:left; padding:.5em;' alt="Screenshot of Sconfig.cmd user interface">  
Screenshot der Benutzeroberfläche von „Sconfig.cmd“  
  
##  <a name="BKMK_Domainworkgroup"></a> Domänen-/Arbeitsgruppeneinstellungen  
 Die aktuellen Einstellungen für die Domäne/Arbeitsgruppe werden auf dem Standardbildschirm des Server-Konfigurationstools angezeigt. Sie können einer Domäne oder Arbeitsgruppe beitreten, indem Sie über das Hauptmenü auf die Seite **Domäne/Arbeitsgruppe** zugreifen, die Anweisungen auf den folgenden Seiten ausführen und dabei alle erforderlichen Informationen angeben.  
  
 Wenn ein Domänenbenutzer nicht der lokalen Administratorgruppe hinzugefügt wurde, können Sie mithilfe des Domänenbenutzers keine Systemänderungen wie das Ändern des Computernamens vornehmen. Lassen Sie einen Neustart des Computers zu, um einen Domänenbenutzer der lokalen Administratorgruppe hinzuzufügen. Melden Sie sich dann als lokaler Administrator auf dem Computer an, und führen Sie die Schritteim Abschnitt [Einstellungen für lokale Administratoren](assetId:///3c2f8ca4-6adc-4ebd-8daf-eb0de16c2c7d#BKMK_Localadministratorsettings) weiter unten in diesem Dokument durch.  
  
> [!NOTE]
>  Sie müssen den Server neu starten, damit Änderungen an der Domänen- oder Arbeitsgruppenmitgliedschaft wirksam werden. Sie können jedoch weitere Änderungen vornehmen und erst danach den Server neu starten, damit er nicht mehrmals neu gestartet werden muss. Ausgeführte virtuelle Computer werden vor dem Neustart des Hyper-V-Servers standardmäßig automatisch gesichert.  
  
## <a name="computer-name-settings"></a>Einstellungen für Computernamen  
 Der aktuelle Computername wird auf dem Standardbildschirm des Server-Konfigurationstools angezeigt. Sie können den Computernamen ändern, indem Sie über das Hauptmenü die Einstellungsseite „Computername“ öffnen und den Anweisungen folgen.  
  
> [!NOTE]
>  Sie müssen den Server neu starten, damit Änderungen an der Domänen- oder Arbeitsgruppenmitgliedschaft wirksam werden. Sie können jedoch weitere Änderungen vornehmen und erst danach den Server neu starten, damit er nicht mehrmals neu gestartet werden muss. Ausgeführte virtuelle Computer werden vor dem Neustart des Hyper-V-Servers standardmäßig automatisch gesichert.  
  
##  <a name="BKMK_Localadministratorsettings"></a> Lokale Administratoreinstellungen  
 Verwenden Sie die Option **Lokalen Administrator hinzufügen** im Hauptmenü, um der lokalen Administratorgruppe weitere Benutzer hinzuzufügen. Auf einem Computer, der einer Domäne beigetreten ist, geben Sie den Benutzer im folgenden Format ein: Domäne\Benutzername. Auf einem Computer, der keiner Domäne angehört Arbeitsgruppencomputer), geben Sie nur den Benutzernamen ein. Die Änderungen werden sofort wirksam.  
  
## <a name="network-settings"></a>Netzwerkeinstellungen  
 Sie können die IP-Adresse so konfigurieren, dass sie automatisch von einem DHCP-Server zugewiesen wird, oder Sie können manuell eine statische IP-Adresse zuweisen. Mit dieser Option können Sie auch DNS-Servereinstellungen für den Server konfigurieren.  
  
> [!NOTE]
>  Diese und viele weitere Optionen sind jetzt über die Windows PowerShell-Netzwerk-Cmdlets verfügbar. Weitere Informationen finden Sie unter [Netzwerkadapter-Cmdlets](https://technet.microsoft.com/library/jj134956.aspx) in der Windows Server-Bibliothek.  
  
## <a name="windows-update-settings"></a>Windows Update-Einstellungen  
 Die aktuellen WindowsUpdate-Einstellungen werden auf dem Standardbildschirm des Server-Konfigurationstools angezeigt. Im Hauptmenü können Sie in der Konfigurationsoption **Windows Update-Einstellungen** automatische oder manuelle Updates für den Server konfigurieren.  
  
 Wenn **automatische Updates** aktiviert sind, führt das System täglich um 3:00 Uhr eine Überprüfung auf Updates durch und installiert diese ggf. Die Einstellungen werden sofort wirksam. Wenn **manuelle** Updates ausgewählt sind, sucht das System nicht automatisch nach Updates.  
  
 Im Hauptmenü können Sie über die Option **Updates herunterladen und installieren** verfügbare Updates jederzeit herunterladen und installieren.

 Mit der Option **Nur herunterladen** werden verfügbare Updates gesucht und herunterladen, und Sie werden im Info-Center benachrichtigt, dass sie bereit für die Installation sind. Dies ist die Standardoption.  
  
## <a name="remote-desktop-settings"></a>Remotedesktop-Einstellungen  
 Der aktuelle Status von Remotedesktop-Einstellungen wird auf dem Standardbildschirm des Server-Konfigurationstools angezeigt. Sie können die folgenden Remotedesktop-Einstellungen konfigurieren, indem Sie die Hauptmenüoption **Remotedesktop** aufrufen und den Anweisungen auf dem Bildschirm folgen.  
  
-   Remotedesktop für Clients aktivieren, auf denen Remotedesktop mit Authentifizierung auf Netzwerkebene ausgeführt wird  
  
-   Remotedesktop für Clients mit einer beliebigen Remotedesktopversion aktivieren  
  
-   Remotedesktop deaktivieren  
  
## <a name="date-and-time-settings"></a>Datums- und Uhrzeiteinstellungen  
 Sie können über die Hauptmenüoption **Datum und Uhrzeit** auf die Datums- und Uhrzeiteinstellungen zugreifen und sie ändern. 

## <a name="telemetry-settings"></a>Telemetrieeinstellungen
Sie können mit dieser Option konfigurieren, welche Daten an Microsoft gesendet werden.

## <a name="windows-activation-settings"></a>Einstellungen für die Aktivierung von Windows
Sie können mit dieser Option die Aktivierung von Windows konfigurieren.
  
## <a name="to-enable-remote-management"></a>So aktivieren Sie die Remoteverwaltung  
Über die Hauptmenüoption **Remoteverwaltung konfigurieren** können Sie verschiedene Remoteverwaltungsszenarien konfigurieren.  
  
-   Remoteverwaltung der Microsoft Management Console  
-   Windows PowerShell  
-   Server-Manager  
  
## <a name="to-log-off-restart-or-shut-down-the-server"></a>Abmelden, Neustarten oder Herunterfahren des Servers  
 Zum Abmelden, Neustarten oder Herunterfahren des Servers rufen Sie im Hauptmenü das entsprechende Menüelement auf. Diese Optionen sind auch im Windows-Sicherheitsmenü verfügbar, das in jeder Anwendung jederzeit mit der Tastenkombination STRG+ALT+ENTF aufgerufen werden kann.  
  
## <a name="to-exit-to-the-command-line"></a>So beenden Sie die Befehlszeile  
 Wählen Sie die Option ** Zur Befehlszeile wechseln**, und drücken Sie die EINGABETASTE, um die Befehlszeile zu beenden. Wenn Sie zum Server-Konfigurationstool zurückkehren möchten, geben Sie **Sconfig.cmd** ein und drücken dann die EINGABETASTE.