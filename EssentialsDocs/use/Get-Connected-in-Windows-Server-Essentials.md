---
title: Get Connected in Windows Server Essentials
description: Beschreibt, wie Sie Windows Server Essentials
ms.custom: na
ms.date: 05/07/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 149a5d34-43b7-4b9e-99e7-9f2294ab9ddb
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 1d7f3c33f1254c8dbe4af8bdf5baa4144c134248
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="get-connected-in-windows-server-essentials"></a>Get Connected in Windows Server Essentials

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials
  
 Sie können Ihre Computer mit dem Windows Server Essentials-Server verbinden, mithilfe der Connector-Software. Die Connector-Software wird installiert, wenn Sie einen Computer mithilfe das Verbinden eines Computers für den Assistenten für den Server mit dem Server verbinden. Sie können diesen Assistenten starten, indem Sie Folgendes eingeben **http://<servername\>/connect**, wobei **< Servername\ >** ist der Name des Servers.  
  
 In diesem Thema:  
  

-   [Vorbereiten der Computer mit dem Server verbinden](Get-Connected-in-Windows-Server-Essentials.md#BKMK_A)  
  
-   [Verbinden von Computern mit dem Server mithilfe der Connector-software](Get-Connected-in-Windows-Server-Essentials.md#BKMK_B)  
  
-   [Verwenden des LaunchPads](Get-Connected-in-Windows-Server-Essentials.md#BKMK_C)  

-   [Vorbereiten der Computer mit dem Server verbinden](Get-Connected-in-Windows-Server-Essentials.md#BKMK_A)  
  
-   [Verbinden von Computern mit dem Server mithilfe der Connector-software](Get-Connected-in-Windows-Server-Essentials.md#BKMK_B)  
  
-   [Verwenden des LaunchPads](Get-Connected-in-Windows-Server-Essentials.md#BKMK_C)  

  
##  <a name="BKMK_A"></a>Vorbereiten der Computer mit dem Server verbinden  
 Dieser Abschnitt beschreibt die Connector-Software, die Betriebssysteme, die unterstützt werden, indem Sie Windows Server Essentials, die erforderlichen Aufgaben, die vor dem Verbinden der Computer mit dem Server ausgeführt werden müssen und die Änderungen, die der Server auf den Computern vornimmt, wenn Sie die Connector-Software ausführen.  
  

-   [Connector-Software (Übersicht)](Get-Connected-in-Windows-Server-Essentials.md#BKMK_1)  
  
-   [Voraussetzungen zum Verbinden eines Computers mit dem server](Get-Connected-in-Windows-Server-Essentials.md#BKMK_2)  
  
-   [Voraussetzungen für die Verbindung mit einem Macintosh-Computer im Netzwerk](Get-Connected-in-Windows-Server-Essentials.md#BKMK_3)  
  
-   [Unterstützte Betriebssysteme für Clientcomputer](Get-Connected-in-Windows-Server-Essentials.md#BKMK_4)  
  
-   [Ändert der Server auf einem Clientcomputer](Get-Connected-in-Windows-Server-Essentials.md#BKMK_5)  
  
-   [Netzwerk-Informationen zu Benutzername und Kennwort](Get-Connected-in-Windows-Server-Essentials.md#BKMK_6)  
  
-   [Server-Administratorkonto s](Get-Connected-in-Windows-Server-Essentials.md#BKMK_7)  
  
-   [Entfernen eines Computers aus einer Windows-Domäne](Get-Connected-in-Windows-Server-Essentials.md#BKMK_8)  
  
###  <a name="BKMK_1"></a>Connector-Software (Übersicht)  
 Die Connector-Software für das Betriebssystem Windows Server Essentials verbindet die Computer in Ihrem Netzwerk mit dem Windows Server Essentials-Server. Wenn Sie Computer mit dem Server verbinden, kann die Connector-Software automatisch die Computer sichern und ihren Zustand zu überwachen. Die Connector-Software ermöglicht auch das Konfigurieren und die Windows Server Essentials-Server Remote zu verwalten. Die Connector-Software wird installiert, wenn Sie einen Clientcomputer mit dem Server verbinden. Weitere Informationen zum Verbinden von Clientcomputern mit Windows Server Essentials-Server finden Sie unter [Verbinden von Computern mit dem Server](Get-Connected-in-Windows-Server-Essentials.md#BKMK_9) weiter unten in diesem Thema.  

-   [Connector-Software (Übersicht)](Get-Connected-in-Windows-Server-Essentials.md#BKMK_1)  
  
-   [Voraussetzungen zum Verbinden eines Computers mit dem server](../use/Get-Connected-in-Windows-Server-Essentials.md#BKMK_2)  
  
-   [Voraussetzungen für die Verbindung mit einem Macintosh-Computer im Netzwerk](Get-Connected-in-Windows-Server-Essentials.md#BKMK_3)  
  
-   [Unterstützte Betriebssysteme für Clientcomputer](Get-Connected-in-Windows-Server-Essentials.md#BKMK_4)  
  
-   [Ändert der Server auf einem Clientcomputer](Get-Connected-in-Windows-Server-Essentials.md#BKMK_5)  
  
-   [Netzwerk-Informationen zu Benutzername und Kennwort](Get-Connected-in-Windows-Server-Essentials.md#BKMK_6)  
  
-   [Server-Administratorkonto s](Get-Connected-in-Windows-Server-Essentials.md#BKMK_7)  
  
-   [Entfernen eines Computers aus einer Windows-Domäne](Get-Connected-in-Windows-Server-Essentials.md#BKMK_8)  
  
###  <a name="BKMK_1"></a>Connector-Software (Übersicht)  
 Die Connector-Software für das Betriebssystem Windows Server Essentials verbindet die Computer in Ihrem Netzwerk mit dem Windows Server Essentials-Server. Wenn Sie Computer mit dem Server verbinden, kann die Connector-Software automatisch die Computer sichern und ihren Zustand zu überwachen. Die Connector-Software ermöglicht auch das Konfigurieren und die Windows Server Essentials-Server Remote zu verwalten. Die Connector-Software wird installiert, wenn Sie einen Clientcomputer mit dem Server verbinden. Weitere Informationen zum Verbinden von Clientcomputern mit Windows Server Essentials-Server finden Sie unter [Verbinden von Computern mit dem Server](Get-Connected-in-Windows-Server-Essentials.md#BKMK_9) weiter unten in diesem Thema.  

  
###  <a name="BKMK_2"></a>Voraussetzungen zum Verbinden eines Computers mit dem server  
 Bevor Sie einen Computer mit dem Netzwerk verbinden, müssen die folgenden Anforderungen erfüllt sein:  
  
-   Die Installation von Windows Server Essentials abgeschlossen ist, und der Server ausgeführt wird. Die Connector-Software wird die Installation beendet, wenn er nicht mit dem Server kommunizieren kann.  
  

-   Der Clientcomputer wird ein unterstütztes Betriebssystem ausgeführt. Weitere Informationen finden Sie unter [unterstützte Betriebssysteme für Clientcomputer](Get-Connected-in-Windows-Server-Essentials.md#BKMK_4).

  
-   Der Clientcomputer muss eine gültige Verbindung mit dem Internet verfügen.  
  
-   Der Clientcomputer ist im selben IP-Subnetz wie der Server, der Windows Server Essentials ausgeführt wird, wenn der Clientcomputer im selben Netzwerk wie der Server.  
  
-   Der Clientcomputer ist .NET Framework 4.5 installiert. Die Connector-Software installiert automatisch auf dem Computer.  
  
-   Der Clientcomputer erfüllt die folgenden mindestsystemanforderungen:  
  
    -   Prozessor 1,4 GHz oder schneller  
  
    -   1 GB RAM oder mehr  
  
    -   1 GB verfügbarer Festplatten-Speicherplatz (ein Teil davon wird nach der Installation freigegeben)  
  
-   Die Startpartition (d. h. die Datenträgerpartition, auf dem Windows-Betriebssystem installiert ist) wird mit dem NTFS-Dateisystem formatiert.  
  
-   Den Namen des Computers wird nicht mehr als 15 Zeichen umfassen.  
  
-   Der Computername enthält einen Unterstrich (_) keine.  
  
-   Der Computer s Datum und Uhrzeit korrekt ausgerichtet an den Einstellungen auf dem Server.  
  
-   Ein Clientcomputer kann zu einem bestimmten Zeitpunkt mit nur einem Windows Server Essentials-Server verbunden sein.  
  
-   Ein Clientcomputer, der bereits einer anderen Active Directory-Domäne angehört kann eine Windows Server Essentials-Domäne nicht beitreten.  
  
> [!NOTE]

>  In einer lokalen Clientbereitstellung für Windows Server Essentials oder Windows Server Essentials können Sie Computer mit dem Server verbinden, ohne sie zur Windows Server Essentials-Domäne hinzuzufügen. Diese Methode ist nicht für alle unterstützten Clientbetriebssysteme und Features wie Gruppenrichtlinien und virtuelle private Netzwerke (VPNs), auf die erfordern, dass ein Computer mit der Domäne verbunden werden, sind nicht verfügbar. Anforderungen und Anleitungen finden Sie unter [Computer mit einem Windows Server Essentials-Server verbinden, ohne den Domänenbeitritt](Get-Connected-in-Windows-Server-Essentials.md#BKMK_10).  
  
 Eine schrittweise Anleitung zum Verbinden eines Computers mit dem Server mit Windows Server Essentials finden Sie unter [Verbinden von Computern mit dem Server](Get-Connected-in-Windows-Server-Essentials.md#BKMK_9).  

>  In einer lokalen Clientbereitstellung für Windows Server Essentials oder Windows Server Essentials können Sie Computer mit dem Server verbinden, ohne sie zur Windows Server Essentials-Domäne hinzuzufügen. Diese Methode ist nicht für alle unterstützten Clientbetriebssysteme und Features wie Gruppenrichtlinien und virtuelle private Netzwerke (VPNs), auf die erfordern, dass ein Computer mit der Domäne verbunden werden, sind nicht verfügbar. Anforderungen und Anleitungen finden Sie unter [Computer mit einem Windows Server Essentials-Server verbinden, ohne den Domänenbeitritt](Get-Connected-in-Windows-Server-Essentials.md#BKMK_10).  
  
 Eine schrittweise Anleitung zum Verbinden eines Computers mit dem Server mit Windows Server Essentials finden Sie unter [Verbinden von Computern mit dem Server](Get-Connected-in-Windows-Server-Essentials.md#BKMK_9).  

  
###  <a name="BKMK_3"></a>Voraussetzungen für die Verbindung mit einem Macintosh-Computer im Netzwerk  
 Die folgenden Anforderungen müssen erfüllt sein, bevor Sie einen Macintosh-Computer mit dem Netzwerk verbinden:  
  
-   Die Installation des Server-Betriebssystems ist abgeschlossen, und der Server ausgeführt wird. Die Connector-Software wird nicht installiert, wenn er mit dem Server kommunizieren kann.  
  
-   Der Computer wird Mac OS X 10.5 (Leopard) oder höher ausgeführt werden.  
  
-   Der Computer befindet sich in demselben IP-Subnetz wie der Server.  
  
-   Der Computer muss eine gültige Verbindung mit dem Internet verfügen.  
  
-   Stellen Sie sicher, dass der Computer die folgenden Mindestanforderungen erfüllt:  
  
    -   Prozessor 1,4 GHz oder schneller  
  
    -   1 GB RAM oder mehr  
  
    -   1 GB verfügbarer Festplatten-Speicherplatz (ein Teil davon wird nach der Installation freigegeben)  
  
-   Ein Clientcomputer kann zu einem bestimmten Zeitpunkt mit nur einem Server verbunden sein.  
  
###  <a name="BKMK_4"></a>Unterstützte Betriebssysteme für Clientcomputer  
 Windows Server Essentials enthält den gleichen Satz von Features für alle unterstützten Clientcomputer. Dazu gehören Domain Join, Launchpad und clientseitige integritätsbenachrichtigungen.  
  
> [!IMPORTANT]
>  Windows Server Essentials unterstützt nicht die Windows-Versionen Home, Starter oder Media Center-Beitritt zu Computern mit der Domäne. Darüber hinaus können Sie den Remotewebzugriff auf diesen Computern eine Verbindung herstellen.  
  
#### <a name="windows-server-essentials"></a>Windows Server Essentials  
  Dieser Abschnitt gilt für einen Server mit Windows Server Essentials oder auf einem Server mit Windows Server 2012 R2 Standard oder Windows Server 2012 R2 Datacenter mit installierter Windows Server Essentials Experience-Rolle. Die folgenden Betriebssysteme werden unterstützt:  
  
 **Windows 7-Betriebssysteme**  
  
-    Windows 7 Home Basic SP1 (x 86- und X64)  
  
-    Windows 7 Home Premium SP1 (x 86- und X64)  
  
-    Windows 7 Professional SP1 (x 86- und X64)  
  
-    Windows 7 Ultimate SP1 (x 86- und X64)  
  
-    Windows 7 Enterprise SP1 (x 86- und X64)  
  
-    Windows 7 Starter SP1 (x 86)  
  
 **Windows 8-Betriebssysteme**  
  
-   Windows 8  
  
-   Windows 8 Professional  
  
-   Windows 8 Enterprise  
  
 **Windows 8.1-Betriebssysteme**  
  
-   Windows 8.1  
  
-   Windows 8.1 Professional  
  
-   Windows 8.1 Enterprise  
  
 **Windows 10-Betriebssysteme**  
  
-   Windows10  
  
-   Windows 10 Professional  
  
-   Windows 10 Enterprise  
  
-   Windows 10 Education  
  
 **Mac-Clientcomputer**  
  
-   Mac OS X v10. 5 Leopard  
  
-   Mac OS X v10.6 Snow Leopard  
  
-   Mac OS X 10.7 Lion  
  
-   Mac OS X v10.8 Mountain Lion  
  
> [!NOTE]
>  Sie können den Integritäts- und Sicherungsstatus für einen Macintosh-Computer aus dem Windows Server Essentials-Dashboard anzeigen. Allerdings nicht konfigurieren Sie die computersicherung oder starten eine Sicherung über das Dashboard. Darüber hinaus können Sie Remote Web Access um einen Macintosh-Computer zu verbinden.  
  
#### <a name="windows-server-essentials"></a>Windows Server Essentials  
  Dieser Abschnitt gilt für einen Server mit Windows Server Essentials. Die folgenden Betriebssysteme werden unterstützt:  
  
 **Windows 7-Betriebssysteme**  
  
-    Windows 7 Home Basic (X86- und X64)  
  
-    Windows 7 Home Premium (X86- und X64)  
  
-    Windows 7 Professional (X86- und X64)  
  
-    Windows 7 Ultimate (X86- und X64)  
  
-    Windows 7 Enterprise (X86- und X64)  
  
-    Windows 7 Starter (x86)  
  
 **Windows 8-Betriebssysteme**  
  
-   Windows 8  
  
-   Windows 8 Professional  
  
-   Windows 8 Enterprise  
  
 **Windows 10-Betriebssysteme**  
  
-   Windows10  
  
-   Windows 10 Professional  
  
-   Windows 10 Enterprise  
  
-   Windows 10 Education  
  
 **Mac-Clientcomputer**  
  
-   Mac OS X v10. 5 Leopard  
  
-   Mac OS X v10.6 Snow Leopard  
  
-   Mac OS X 10.7 Lion  
  
> [!NOTE]
>  Sie können den Integritäts- und Sicherungsstatus für einen Macintosh-Computer aus dem Windows Server Essentials-Dashboard anzeigen. Allerdings nicht konfigurieren Sie die computersicherung oder starten eine Sicherung über das Dashboard. Darüber hinaus können Sie Remote Web Access um einen Macintosh-Computer zu verbinden.  
  
###  <a name="BKMK_5"></a>Ändert der Server auf einem Clientcomputer  
 Wenn Sie einen Computer mit dem Server verbinden, wird die Windows Server Essentials-Software eine Reihe von Änderungen auf dem Computer, damit der Computer und Server zusammenarbeiten können.  
  
 Die Software führt Folgendes aus:  
  
-   Installiert die Connector-Software auf dem computer  
  
-   Microsoft .NET Framework 4.5 installiert auf dem Computer, wenn es nicht bereits installiert ist  
  
-   Erstellt von Tastenkombinationen auf dem Computer s-Desktop auf das Dashboard und Launchpad  
  
-   Konfiguriert die Windows-Firewall-Ports auf dem Computer, um die folgenden Features arbeiten zu ermöglichen:  
  
    -   Core Networking  
  
    -   Remote Desktop Services  
  
-   Nimmt folgende Änderungen an dem Computer um Sicherungen zu vereinfachen:  
  
    -   Erstellt geplante Aufgaben zum Ausführen automatischer Sicherungen.  
  
    -   Installiert Dienste, die Sicherungsvorgänge mit dem Server verwalten  
  
    -   Installiert einen virtuellen Gerätetreiber, die verwendet wird, während der Wiederherstellungsvorgänge von Dateien und Ordner  
  
-   Installiert den Health Agent, um Probleme zu erkennen und die entsprechenden Benachrichtigungen erstellen  
  
-   Sie erstellt geplante Aufgaben auf dem Computer für wiederkehrende integritätsbewertungen und Definitionen zu synchronisieren.  
  
-   Sie fügt Dienste auf dem Computer, die der Computer verwendet wird, für die Kommunikation mit dem Server sowie mit anderen Windows Server Essentials-features  
  
-   Öffnen TCP-Port 3389 auf Clientcomputern mit Windows-Clients, damit Remote Desktop Services ausführen können  
  
-   Stellt VPN auf dem Clientcomputer und bietet einen einzigen Klick wenn VPN-Funktion auf Windows Server Essentials aktiviert ist, oder einem Klick bietet, wenn die VPN-Funktionalität auf Windows Server Essentials aktiviert ist  
  

 Informationen zum Verbinden Ihres Computers mit dem Server finden Sie unter [Verbinden von Computern mit dem Server](Get-Connected-in-Windows-Server-Essentials.md#BKMK_9).  
  
###  <a name="BKMK_6"></a>Netzwerk-Informationen zu Benutzername und Kennwort  
 Sie erhalten die Netzwerk-Benutzerinformationen an Namen und das Kennwort von der Person, die den Server verwaltet. Diese Anmeldeinformationen können Sie um Ihren Computer auf dem Server und den Zugriff auf Informationen vom Server zu verbinden.  
  
###  <a name="BKMK_6"></a>Netzwerk-Informationen zu Benutzername und Kennwort  
 Sie erhalten die Netzwerk-Benutzerinformationen an Namen und das Kennwort von der Person, die den Server verwaltet. Diese Anmeldeinformationen können Sie um Ihren Computer auf dem Server und den Zugriff auf Informationen vom Server zu verbinden. 

  
 Wenn Sie den Server-Administrator sind, können die Anmeldeinformationen für das Netzwerk durch Hinzufügen eines Benutzerkontos aus der **Benutzer** Dashboard-Registerkarte. Weitere Informationen zu Benutzerkonten finden Sie unter [Verwalten von Benutzerkonten, die über das Dashboard](../manage/Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Manage8).  
  
###  <a name="BKMK_7"></a>Server-Administratorkonto s  
 Sie müssen einen Administratorkontonamen Netzwerk und ein Kennwort zum Installieren der Connector-Software bereitstellen können. Ein netzwerkadministratorkonto ermöglicht es dem Benutzer das lokale Netzwerk für Ihre Organisation zu verwalten und hilft, verwalten und Warten von Netzwerkgeräte wie Switches und Router.  
  
 Die Aufgaben, die mit einem netzwerkadministratorkonto durchgeführt werden können, können umfassen:  
  
-   Installieren von netzwerkanwendungen und anderer software  
  
-   Verwalten von Speicher auf dem server  
  
-   Verteilen von Softwareupdates  
  
-   Durchführen regelmäßiger Sicherungen  
  
-   Überwachen der täglichen Aktivitäten im Netzwerk  
  
 Sie können in Windows Server Essentials, Windows Server Essentials und Windows Server 2012 R2 mit installierter Windows Server Essentials Experience-Rolle kann den Netzwerkadministrator zuweisen Zugriffsebene für jedes Benutzerkonto. Dadurch wird die erforderlichen Berechtigungen zum Ausführen der Aufgaben eines Netzwerkadministrators gewährt. Wenn ein Benutzer den Netzwerkadministrator zugewiesen ist Zugriffsebene, die **Steuerung des Benutzerzugriffs** öffnet sich die Eingabeaufforderung für jede Aufgabe, die Administratorberechtigungen erforderlich sind.  
  
###  <a name="BKMK_8"></a>Entfernen eines Computers aus einer Windows-Domäne  
 Um einen Computer aus der Domäne entfernen, werden Sie für den Benutzernamen und das Kennwort des Domänenkontos aufgefordert werden.  
  
##### <a name="to-remove-a-computer-from-a-windows-domain"></a>Zum Entfernen eines Computers aus einer Windows-Domäne  
  
1.  Klicken Sie auf **starten**, mit der rechten Maustaste **Computer**, und klicken Sie dann auf **Eigenschaften**.  
  
2.  Klicken Sie unter **Einstellungen für Computernamen, Domäne und Arbeitsgruppe**, klicken Sie auf **Einstellungsänderungen**.  
  
    > [!NOTE]
    >  Wenn Sie aufgefordert, ein Administratorkennwort oder eine Bestätigung einzugeben werden, geben Sie das Kennwort bzw. die Bestätigung.  
  
3.  In der **Systemeigenschaften** Dialogfeld, klicken Sie auf die **Computername** Registerkarte, und klicken Sie dann auf **ändern**.  
  
4.  In der **Computer bzw.-domänenänderungen** Dialogfeld unter **Mitglied**, klicken Sie auf **Arbeitsgruppe**, und führen Sie dann eine der folgenden Optionen:  
  
    1.  Um einer bestehenden Arbeitsgruppe beizutreten, geben Sie den Namen der Arbeitsgruppe, die Sie verwenden möchten, verknüpfen, und klicken Sie dann auf **OK**.  
  
    2.  Um einer Arbeitsgruppe zu erstellen, geben Sie den Namen der Arbeitsgruppe, die Sie erstellen möchten, und klicken Sie dann auf **OK**.  
  
        > [!NOTE]
        >  Der Computer aus der Domäne entfernt werden, und Ihr Computerkonto in dieser Domäne wird deaktiviert.  
  
##  <a name="BKMK_B"></a>Verbinden von Computern mit dem Server mithilfe der Connector-software  
 Dieser Abschnitt enthält Informationen, mit denen Sie die Connector-Software installieren, verbinden Ihren Computer mit dem Server und Problembehandlung beim Verbinden von Computern mit dem Server und Verfahren erläutert.  
  

-   [Verbinden von Computern mit dem server](Get-Connected-in-Windows-Server-Essentials.md#BKMK_9)  
  
-   [Verbinden Sie Computer mit einem Windows Server Essentials-Server, ohne der Domäne beitreten kann](Get-Connected-in-Windows-Server-Essentials.md#BKMK_10)  
  
-   [Installieren Sie die Connector-software](Get-Connected-in-Windows-Server-Essentials.md#BKMK_11)  
  
-   [Verschieben von Daten und Einstellungen manuell](Get-Connected-in-Windows-Server-Essentials.md#BKMK_12)  
  
-   [Übertragen Sie mehrerer Benutzerprofile während der Bereitstellung](Get-Connected-in-Windows-Server-Essentials.md#BKMK_Transfer)  
  
-   [Deinstallieren Sie die Connector-software](Get-Connected-in-Windows-Server-Essentials.md#BKMK_13)  
  
-   [Trennen Sie den Computer aus, oder Verbinden Sie Ihren Computer mit dem server](Get-Connected-in-Windows-Server-Essentials.md#BKMK_14)  
  
-   [Wie Sicherung im Energiesparmodus und Ruhezustand](Get-Connected-in-Windows-Server-Essentials.md#BKMK_Sleep)  

-   [Verbinden von Computern mit dem server](Get-Connected-in-Windows-Server-Essentials.md#BKMK_9)  
  
-   [Verbinden Sie Computer mit einem Windows Server Essentials-Server, ohne der Domäne beitreten kann](Get-Connected-in-Windows-Server-Essentials.md#BKMK_10)  
  
-   [Installieren Sie die Connector-software](Get-Connected-in-Windows-Server-Essentials.md#BKMK_11)  
  
-   [Verschieben von Daten und Einstellungen manuell](Get-Connected-in-Windows-Server-Essentials.md#BKMK_12)  
  
-   [Übertragen Sie mehrerer Benutzerprofile während der Bereitstellung](Get-Connected-in-Windows-Server-Essentials.md#BKMK_Transfer)  
  
-   [Deinstallieren Sie die Connector-software](Get-Connected-in-Windows-Server-Essentials.md#BKMK_13)  
  
-   [Trennen Sie den Computer aus, oder Verbinden Sie Ihren Computer mit dem server](Get-Connected-in-Windows-Server-Essentials.md#BKMK_14)  
  
-   [Wie Sicherung im Energiesparmodus und Ruhezustand](Get-Connected-in-Windows-Server-Essentials.md#BKMK_Sleep)  

  
###  <a name="BKMK_9"></a>Verbinden von Computern mit dem server  
 Wenn Sie einen Computer auf einem Server mit Windows Server Essentials oder Windows Server 2012 R2 mit installierter Windows Server Essentials Experience-Rolle verbinden, stellen Sie sicher, dass der Clientcomputer über eine gültige Verbindung mit dem Internet verfügt.  
  
 Führen Sie das folgende Verfahren auf allen Clientcomputern, die sie mit dem Server herstellen.  
  
 Um den Vorgang abzuschließen, benötigen Sie die folgenden Informationen:  
  
-   Den Benutzernamen und das Kennwort der Person, die den Computer im neuen Netzwerk verwendet  
  
-   Die Kombination aus Benutzername und Kennwort für das lokale Administratorkonto des Computers s  
  
> [!NOTE]

>  In einer lokalen Clientbereitstellung für Windows Server Essentials oder Windows Server Essentials können Sie Computer mit dem Server verbinden, ohne sie zur Windows Server Essentials-Domäne hinzuzufügen. Diese Methode ist nicht für alle unterstützten Clientbetriebssysteme und Features wie Gruppenrichtlinien und virtuelle private Netzwerke (VPNs), auf die erfordern, dass ein Computer mit der Domäne verbunden werden, sind nicht verfügbar. Anforderungen und Anleitungen finden Sie unter [Computer mit einem Windows Server Essentials-Server verbinden, ohne den Domänenbeitritt](Get-Connected-in-Windows-Server-Essentials.md#BKMK_10).  

>  In einer lokalen Clientbereitstellung für Windows Server Essentials oder Windows Server Essentials können Sie Computer mit dem Server verbinden, ohne sie zur Windows Server Essentials-Domäne hinzuzufügen. Diese Methode ist nicht für alle unterstützten Clientbetriebssysteme und Features wie Gruppenrichtlinien und virtuelle private Netzwerke (VPNs), auf die erfordern, dass ein Computer mit der Domäne verbunden werden, sind nicht verfügbar. Anforderungen und Anleitungen finden Sie unter [Computer mit einem Windows Server Essentials-Server verbinden, ohne den Domänenbeitritt](Get-Connected-in-Windows-Server-Essentials.md#BKMK_10).  

  
##### <a name="to-connect-a-client-computer-to-the-server"></a>Auf einen Clientcomputer mit dem Server verbinden  
  
1.  Melden Sie sich auf dem Computer, den Sie mit dem Server verbinden möchten.  
  
    > [!NOTE]
    >  Wenn auf diesem Computer mehrere Benutzerkonten vorhanden sind, melden Sie sich mit dem Benutzerkonto an, das dessen Dokumente, Bilder und persönlichen Vorlieben, die Sie beibehalten, nachdem Sie den Computer mit dem Server verbinden möchten.  
  
2.  Öffnen Sie einen Internetbrowser, z. B. Internet Explorer.  
  
3.  Geben Sie in der Adressleiste **http://<servername\>/Connect**, und drücken Sie dann die EINGABETASTE.  
  
    > [!NOTE]
    >  Wenn der Computer an einem Remotestandort außerhalb des Windows Server Essentials-Netzwerks befindet, geben Sie zum Verbinden ein Computers zum Assistenten für den Server ausführen **http://<domainname\>/connect** in der Adressleiste des Browsers ein (< Domäne\ > steht für den Domänennamen Ihrer Organisation). Sie können Ihre Domänennameninformationen von Ihrem Netzwerkadministrator abrufen.  
  
4.  Die **Verbinden des Computers mit dem Server** Seite wird angezeigt. Führen Sie einen der folgenden:  
  
    -   Für einen Computer mit dem Windows-Betriebssystem, klicken Sie auf **Software für Windows herunterladen**.  
  
    -   Damit ein Computer auf dem Mac OS X oder höher, klicken Sie auf **Software für Mac herunterladen**.  
  
5.  Klicken Sie in der Datei Download Warnmeldung zur downloadsicherheit auf **ausführen**.  
  
6.  Wenn die Meldung der Benutzerkontensteuerung angezeigt wird, klicken Sie auf **Ja** , oder geben Sie den lokalen Benutzernamen und das Kennwort, wenn Sie aufgefordert werden.  
  
7.  Verbinden ein Computers für den Assistenten für den Server angezeigt wird. Führen Sie Folgendes ein, um den Assistenten abzuschließen:  
  
    1.  Akzeptieren Sie den Endbenutzer-Lizenzvertrag.  
  
    2.  Auf der **meinen Server suchen** Seite, automatische Erkennung des Servers im lokalen Netzwerk, und wählen Sie den Server, die Verbindung hergestellt werden soll. Oder, wenn Sie die Informationen verfügen, können Sie s Namen oder die Adresse Ihres manuell eingeben.  
  
    3.  Auf der **neue Netzwerk-Benutzernamen und Kennwort** Seite, gehen Sie folgendermaßen vor:  
  
        -   Verwenden Sie ist dies der erste Computer, den Sie mit dem Server verbinden, und ist dies der Computer, den Sie zum Verwalten des Servers verwenden möchten, das Administratorkonto, das Sie während des Setups erstellt.  
  
        -   Für alle anderen Computer zunächst erstellen Sie ein Netzwerkbenutzerkonto auf dem Server mithilfe des Dashboards. Erstellen Sie das Benutzerkonto mit Administrator- oder Standardbenutzerrechten Benutzerrechte, je nach den Aufgaben, die von der Person, die mit dem Computer ausgeführt werden.  
  
    4.  Wenn auf Ihrem Computer Windows 8, Windows 8.1 oder Windows 10 ausgeführt wird, überspringen Sie diesen Schritt. Wenn Ihr Computer Windows 7 ausgeführt wird, und besitzen Sie Dokumente, Bilder oder persönlichen Einstellungen (z. B. Desktophintergrundbilder, Bildschirmschoner oder Internet Explorer-Favoriten), die Sie nach dem behalten möchten, fügen Sie den Computer zum neuen Netzwerk, auf die **auswählen, wenn Sie Ihre vorhandenen Daten und Einstellungen verschieben möchten** Seite des Assistenten die Option der **Verschieben von Daten und Einstellungen auf Mein neues Netzwerkbenutzerkonto**.  
  
    5.  Wählen Sie ggf. automatisch Reaktivieren eines Computers zum Erstellen einer Sicherung auf dem **auswählen, wenn Sie diese Computer zum Erstellen der Sicherung reaktivieren möchten** Seite.  
  
    6.  Führen Sie die verbleibenden Anweisungen im Assistenten, um den Computer mit dem Netzwerk hinzugefügt haben.  
  
8.  Nachdem Sie den Computer mit dem Netzwerk hinzugefügt haben, verwenden Sie die neue Kombination aus Benutzername und Kennwort am Computer anmelden.  
  
    > [!NOTE]
    >  Wenn Sie sich an einem Computer, die Windows 8 ausgeführt wird zum ersten Mal anmelden mit Ihrem Netzwerkkonto an, nach dem er eine Verbindung mit dem Server herstellt, werden Sie Anweisungen zum Migrieren von Dateien und Anwendungen von Ihrem alten Benutzerkonto angezeigt. Folgen Sie den Anweisungen auf dem **wie migriere ich Dateien und Anwendungen von meinem alten Benutzerkonto? ** Seite, um alle Dateien und Anwendungen zu Ihrem Netzwerkbenutzerkonto zu migrieren.  
  
9. Nachdem der Computer erfolgreich mit dem Server verbunden ist, werden Verknüpfungen zur Connector TrayApp und zum Server-Dashboard im Menü "Start", die wie folgt verwendet werden können (bei Ihrem Computer Windows 8, Windows 8.1 ausgeführt wird, oder Windows 10, das Dashboard und Connector TrayApp auf der Startseite der Computer s stehen) angezeigt:  
  
    -   Wenn auf Ihrem Computer Windows 8, Windows 8.1 oder Windows 10 ausgeführt wird, wird das Dashboard und Connector TrayApp als Anwendung sein.  
  
    -   In der Connector TrayApp, können Sie aktivieren oder Deaktivieren der **Remote verbunden bleiben** Feature. Doppelklicken Sie auf die TrayApp, um das Launchpad zu starten. Über das Launchpad können Sie Zugriff auf die freigegebenen Ordner Verknüpfung, computersicherungen konfigurieren, Warnungen, und öffnen Sie die Remotewebzugriff-Website.  
  
    -   Von der **Dashboard** verknüpfen, können Sie den Server verwalten.  
  
###  <a name="BKMK_10"></a>Verbinden Sie Computer mit einem Windows Server Essentials-Server, ohne der Domäne beitreten kann  
 In diesem Thema wird beschrieben, wie Sie einen Windows 7, Windows 8, Windows 8.1 oder Windows 10-Computer mit einem Windows Server Essentials-Netzwerk hinzufügen, ohne dass der Computer mit der Windows Server Essentials-Domäne in einer lokalen Clientbereitstellung Beitritt. Diese Verbindungsmethode wird in Windows Server Essentials und Windows Server Essentials unterstützt.  
  
 Dies ist eine Alternative zu der üblichen-Methode, die erforderlich sind, den Computer mit Windows Server Essentials-Domäne verknüpfen. Mit dieser Methode Wenn der Computer in einer anderen Domäne muss es aus dieser Domäne entfernt werden, bevor sie Windows Server Essentials-Domäne hinzugefügt werden kann.  
  
#### <a name="feature-limits"></a>Feature-Grenzen  
 Einige Funktionen sind eingeschränkt, wenn ein Clientcomputer nicht mit der Windows Server Essentials-Domäne hinzugefügt wird:  
  
-   Alle Features, die erfordern, dass der Computer der Domäne hinzugefügt werden? einschließlich Anmeldeinformationen für die Domäne, Gruppenrichtlinie und virtuelle private Netzwerke (VPNs)? sind nicht verfügbar.  
  
-   Add-ons von Drittanbietern, die erfordern, dass der Computer der Domäne hinzugefügt werden, funktionieren nicht ordnungsgemäß.  
  
-   Diese Methode kann verwendet werden, um einen externen Computer mit dem Server verbinden.  
  
#### <a name="prerequisites"></a>Erforderliche Komponenten  
  
-   Der Computer muss es sich um eine physische Verbindung mit dem lokalen Netzwerk verfügen.  
  
-   Eines der folgenden Betriebssysteme muss auf dem Computer installiert sein:  
  
    -   Windows 10 Pro, Windows 10 Enterprise  
  
    -    Windows 8.1 Pro, Windows 8.1 Enterprise, Windows 8 Pro, Windows 8 Enterprise  
  
    -    Windows 7 Professional (X86- und X64), Windows 7 Enterprise (X86- und X64), Windows 7 Ultimate (X86- und X64)  
  

-   Der Computer muss alle anderen Anforderungen an Clientcomputer in Windows Server Essentials erfüllen. Weitere Informationen finden Sie unter [Voraussetzungen zum Verbinden eines Computers mit dem Server](Get-Connected-in-Windows-Server-Essentials.md#BKMK_2).  

  
-   Um eine Verbindung zu aktivieren, ohne dass Sie die Domäne beitritt, müssen Sie auf den Computer mit einem Konto anmelden auf, die Mitglied der lokalen Administratorgruppe ist.  
  
-   Um den Computer mit dem Windows Server Essentials-Server zu verbinden, benötigen Sie die folgenden Informationen:  
  
    -   Ein Konto mit Administratorrechten auf Windows Server Essentials (Ihr Konto).  
  
    -   Die Kombination aus Benutzername und Kennwort für das Domänenkonto der Person, die den Computer verwendet. Das Domänenkonto muss auch über Administratorrechte auf dem Windows Server Essentials-Server verfügen.  
  
#### <a name="connect-to-a-windows-server-essentials-network"></a>Verbinden Sie mit einem Windows Server Essentials-Netzwerk  
 Vergewissern Sie sich, dass alle Voraussetzungen erfüllt sind, verbinden Sie den Computer mit Windows Server Essentials-Netzwerk.  
  
###### <a name="to-connect-a-computer-in-a-different-domain-to-a-windows-server-essentials-network"></a>Verbinden eines Computers in einer anderen Domäne mit einem Windows Server Essentials-Netzwerk  
  
1.  Melden Sie sich auf dem Clientcomputer mit einem Konto, das Mitglied der lokalen Administratorgruppe ist.  
  
2.  Öffnen Sie eine Eingabeaufforderung mit Administratorrechten an.  
  
    -   In Windows 10, klicken Sie auf die **starten** Schaltfläche **alle Apps** -> **Windows Systemprogramme** -> **Eingabeaufforderung**mit der rechten Maustaste auf Eingabeaufforderung, und klicken Sie dann auf **als Administrator ausführen**.  
  
    -   In Windows 8 auf die **starten** geben **Befehl** und drücken Sie dann die EINGABETASTE. In den Ergebnissen mit der rechten Maustaste **Eingabeaufforderung**, und klicken Sie dann auf **als Administrator ausführen**.  
  
    -   In Windows 7 auf die **starten** Menü geben **Befehl** in das Suchfeld, mit der rechten Maustaste **Eingabeaufforderung**, und klicken Sie dann auf **als Administrator ausführen**.  
  
3.  Geben Sie den folgenden Befehl an der Eingabeaufforderung, und drücken Sie dann die EINGABETASTE:  
  
    ```  
    reg add "HKLM\SOFTWARE\Microsoft\Windows Server\ClientDeployment" /v SkipDomainJoin /t REG_DWORD /d 1  
    ```  
  

4.  Führen Sie die Schritte in [Verbinden von Computern mit dem Server](Get-Connected-in-Windows-Server-Essentials.md#BKMK_9).  

  
####  <a name="BKMK_SecondServer"></a>Verbinden eines zweiten Servers mit dem Netzwerk  
  
###### <a name="to-join-a-second-server-to-the-network"></a>Auf einem zweiten Server mit dem Netzwerk hinzufügen  
  
1.  Melden Sie sich an den Server, den Sie mit dem Windows Server Essentials-Netzwerk herstellen möchten.  
  
2.  Öffnen Sie einen Internetbrowser, und geben Sie in der Adressleiste **http://<servername\>/Connect**, wobei *< Servername\ >* ist der Name des Servers mit Windows Server Essentials, und drücken Sie dann die EINGABETASTE.  
  
3.  Wenn die verstärkte Sicherheitskonfiguration für Internet Explorer auf dem Server aktiviert ist, die Sie versuchen, eine Verbindung mit dem Windows Server Essentials-Netzwerk herstellen, führen Sie Folgendes aus. andernfalls überspringen Sie diesen Schritt.  
  
    1.  Zum Übernehmen der blockierenden Nachricht klicken Sie auf **schließen**.  
  
    2.  Hinzufügen der **http://<servername\>/Connect** Website, um den vertrauenswürdigen Websites wie folgt:  
  
        1.  Klicken Sie im Navigationsbereich Browser **Tools**, und klicken Sie dann auf **Internetoptionen**.  
  
        2.  Klicken Sie auf die **Security** Registerkarte, und klicken Sie dann auf **vertrauenswürdige Sites**.  
  
        3.  Klicken Sie auf **Sites**.  
  
        4.  Die Website angezeigt werden soll, der **diese Website zur Zone hinzufügen** Feld. Klicken Sie auf **hinzufügen**.  
  
        5.  Klicken Sie auf **schließen**, und klicken Sie dann auf **OK**.  
  
    3.  Aktualisieren Sie die Webseite.  
  

    4.  Um den zweiten Server mit einem Server unter Windows Server Essentials zu verbinden, folgen Sie den Anweisungen [Verbinden von Computern mit dem Server](Get-Connected-in-Windows-Server-Essentials.md#BKMK_9).  

  
    > [!NOTE]
    >  Verbinden eines zweiten Servers mit einem Server unter Windows Server Essentials unterscheidet sich von der Verbindung mit einem Client-Computer wie folgt:  
    >   
    >  -   Es ist keine Migration von Benutzerprofilen. aus diesem Grund wird das aktuelle Profil nicht migriert werden.  
    > -   Können nicht den zweiten Server mit Client Computer Backup gesichert, und es gibt keine Option, um den Computer für die Sicherung zu reaktivieren.  
  
 Nachdem Sie den zweiten Server auf einen Server, auf denen Windows Server Essentials ausgeführt wird hinzugefügt, werden die folgenden Features auf dem verbundenen Server bereitgestellt:  
  
-   Updates und Benachrichtigungen funktionieren wie auf anderen Clientcomputern.  
  
-   Online und Offline funktionieren wie auf anderen Clientcomputern.  
  
-   Sie können mit Remote Web Access mit dem zweiten Server verbinden.  
  
-   Der zweite Server wird in die Integritätsberichte enthalten sein, da Windows Server Essentials Warnungen im Zusammenhang mit diesem Server generiert wird.  
  
 Verwaltung des zweiten Servers aus dem Server mit Windows Server Essentials unterscheidet sich von der Verwaltung anderer Clientcomputer wie folgt:  
  
-   Es werden keine Einstiegspunkt für TrayApp, Launchpad und Dashboard Client.  
  
-   Der zweite Server ist aufgeführt, in der **Server** auf die **Geräte** Registerkarte.  
  
-   Da die clientcomputersicherung für den zweiten Server nicht unterstützt wird, wird der Sicherungsstatus als angezeigt **nicht unterstützt**. Darüber hinaus, wenn Sie den zweiten Server und mit der rechten Maustaste auswählen, sind keine Sicherung und Wiederherstellung verwandten Aufgaben für den zweiten Server angezeigt.  
  
-   Wenn Sie den zweiten Server auswählen, und klicken Sie dann auf die **Servereigenschaften anzeigen** Aufgabe ist, gibt es keine **Sicherung** Registerkarte auf der Eigenschaftenseite des Servers angezeigt.  
  
-   Da auf einem Windows Server-Betriebssystem kein Sicherheitscenter vorhanden ist, zeigt den Status des zweite Servers s-Sicherheit als **nicht zutreffend**.  
  
-   Der zweite Server s Gruppenrichtlinien-Status wird angezeigt, als **nicht zutreffend**.  
  
###  <a name="BKMK_11"></a>Installieren Sie die Connector-software  
 Die Connector-Software in Windows Server Essentials wird installiert, wenn Sie Ihren Computer mit den eines Computers für den Assistenten zum Herstellen einer Verbindung mit dem Server verbinden. Starten dieses Assistenten durch Eingabe **http://<ServerName\>/connect** in der Adressleiste des Browsers ein (wobei *< ServerName\ >* ist der Name des Servers).  
  
> [!NOTE]
>  Wenn der Computer an einem Remotestandort befindet, geben Sie zum Verbinden ein Computers zum Assistenten für den Server ausführen **http://<domainname\>/connect** in der Adressleiste des Webbrowsers (, in denen *< Domäne\ >* der Domänennamen Ihrer Organisation ist). Sie können Ihre Domänennameninformationen von Ihrem Netzwerkadministrator abrufen.  
  
 Die Connector-Software führt Folgendes aus:  
  
-   Verbindet den Computer mit Windows Server Essentials  
  
-   Sichert automatisch auf Ihrem Computer über Nacht (Wenn Sie den Server zum Erstellen von Client-Sicherungen konfigurieren)  
  
-   Hilft dem Administrator bei der Überwachung des Computers  
  
-   Ermöglicht es Ihnen, konfigurieren und Verwalten von Windows Server Essentials Remote von Ihrem Computer zu Hause  
  

 Eine schrittweise Anleitung zum Verbinden Ihres Computers mit dem Windows Server Essentials-Server finden Sie unter [Verbinden von Computern mit dem Server](Get-Connected-in-Windows-Server-Essentials.md#BKMK_9).   

  
###  <a name="BKMK_12"></a>Verschieben von Daten und Einstellungen manuell  
  Windows Server Essentials und Windows Server Essentials unterstützen die Migration von Benutzerprofilen nur für Clientcomputer, auf denen das Betriebssystem Windows 7 ausgeführt werden. Wenn Sie einen Windows 7-basierten Computer mit dem Server verbinden, kann das Verbinden des Computers mit dem Assistenten für den Server das Benutzerprofil automatisch migrieren.  
  
 Das Benutzerprofil kann nicht automatisch übertragen werden, wenn ein Windows 8, Windows 8.1 oder Windows 10-Computer mit dem Server verbinden. Allerdings auf einem Computer unter Windows 8 können Windows-EasyTransfer Sie Daten und Einstellungen aus dem ursprünglichen lokalen Benutzer in der Domäne beigetretenen Computer übertragen. Dazu müssen Sie ein Administrator auf dem Quellcomputer Windows 8 und der Windows 8-Zielcomputers sein. Informationen zur Verwendung von Windows Easy Transfer für die Übertragung von Dateien und Einstellungen finden Sie unter [Artikel 2735227](https://support.microsoft.com/kb/2735227) in der Microsoft Knowledge Base.  
  
###  <a name="BKMK_Transfer"></a>Übertragen Sie mehrerer Benutzerprofile während der Bereitstellung  
 Bevor Sie einen Computer mit Windows 7 oder Windows 7 SP1-Betriebssystem auf den Windows Server Essentials-Server herstellen, erstellen, um übertragen mehrere lokale Benutzerprofile müssen Sie zunächst die entsprechenden Netzwerkbenutzerkonten auf dem Server. Weitere Informationen zum Erstellen von Benutzerkonten finden Sie unter [Hinzufügen eines Benutzerkontos](../manage/Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Manage1).  
  
 Migration von Benutzerprofilen wird nur auf einem Computer unter Windows 7 (für Windows Server Essentials) oder Windows 7 SP1 (für Windows Server Essentials) unterstützt. Wenn Sie einen Computer mit dem Verbinden des Computers zum Assistenten für den Server mit Windows Server Essentials-Server verbinden, erhalten Sie eine Option, um die Benutzerdaten und Einstellungen Alter lokaler Benutzerkonten in die neuen Netzwerkbenutzerkonten verschieben. Dazu auf die **Verschieben vorhandener Benutzerdaten und Einstellungen** Seite des Assistenten die Netzwerkbenutzerkonten den lokalen Benutzerkonten zu, auf dem Computer mehrere Benutzerprofile übertragen, die auf dem Clientcomputer befinden zuordnen.  
  
###  <a name="BKMK_13"></a>Deinstallieren Sie die Connector-software  
 Sie können die Connector-Software auf einem Computer mithilfe der Systemsteuerung deinstallieren. Dies ist in der Regel erfolgt, liegt ein Problem mit der Connector-Software oder wenn Sie eine neuere Version der Connector-Software installieren müssen. Sie müssen auf dem Computer als Administrator zum Durchführen dieses Verfahrens angemeldet sein.  
  
> [!IMPORTANT]
>  Wenn Sie das Betriebssystem auf einem Clientcomputer aktualisieren, wird die Connector-Software automatisch deinstalliert. Sie müssen die Connector-Software neu installieren, nachdem das Upgrade abgeschlossen ist. Die bevorzugte Methode ist auf die Connector-Software zu deinstallieren, bevor Sie das Betriebssystem aktualisieren. Deinstallieren der Connector-Software nach dem Abschluss des Upgrades ist zwar akzeptabel. jedoch kann es dazu führen, dass in einem inkonsistenten Status für den Clientcomputer mit dem Server die Connector-Software deinstalliert und neu installiert wird.  
  
##### <a name="to-uninstall-connector-software-from-a-computer"></a>Connector-Software auf einem Computer deinstallieren  
  
1.  Auf einem Computer, auf denen Windows 7, Windows 8, Windows 8.1 oder Windows 10 ausgeführt wird, öffnen **Systemsteuerung**, und klicken Sie dann in der **Programme** auf **installierte Updates anzeigen**.  
  
2.  Wählen Sie aus der Liste der installierten Programme **Windows Server Essentials Connector**, und klicken Sie dann auf **Deinstallieren**.  
  
3.  Klicken Sie auf der Seite mit der Warnung auf **Ja**.  
  
4.  Wenn die **User Account Control** Fenster angezeigt wird, klicken Sie auf **zulassen**.  
  
5.  In Windows Server Essentials, wenn die Windows Server Essentials Connector-Seite gefragt werden, ob Sie Launchpad schließen angezeigt wird, klicken Sie auf **OK**.  
  
6.  Warten Sie, bis das Programm zu deinstallieren. Nach dem Entfernen der Software **Windows Server Essentials Connector** in der Liste der installierten Programme oder Updates nicht mehr angezeigt wird. Darüber hinaus werden die Verknüpfungen mit dem Launchpad und Dashboard nicht mehr auf dem s-Computerdesktop angezeigt.  
  
> [!NOTE]
>  -   Deinstallieren der Connector-Software wird nicht entfernen Sie den Computer aus der Liste der Computer, die Anzeige auf der **Geräte** Dashboard-Registerkarte. Zum Entfernen des Computers über das Dashboard finden Sie unter [Entfernen eines Computers vom Server](../manage/Manage-Devices-in-Windows-Server-Essentials.md#BKMK_3).  
> -   Wenn Sie die Connector-Software deinstallieren, werden die freigegebenen Ordner auf dem Clientcomputer, die dem Server zugeordnet wurden, nicht gelöscht. Sie müssen die freigegebenen Ordner, die mit dem Server zugeordnet sind, manuell löschen.  

> -   Deinstallieren die Connector-Software werden keine den Computer die ursprüngliche Domäne verlässt gestellt. Sie müssen den Computer aus der Domäne manuell entfernen. Anweisungen finden Sie unter [Entfernen eines Computers aus einer Windows-Domäne](Get-Connected-in-Windows-Server-Essentials.md#BKMK_8).  

  
###  <a name="BKMK_14"></a>Trennen Sie den Computer aus, oder Verbinden Sie Ihren Computer mit dem server  
 Wenn einen Computer vom Server trennen möchten, müssen Sie die folgenden Schritte ausführen:  
  

1.  Deinstallieren Sie die Connector-Software auf dem Computer mithilfe der Systemsteuerung. Eine schrittweise Anleitung finden Sie unter [deinstallieren die Connector-Software](Get-Connected-in-Windows-Server-Essentials.md#BKMK_13).   

  
2.  Entfernen Sie den Computer aus der Windows Server Essentials-Domäne, und fügen Sie ihn der Arbeitsgruppe hinzu. Eine ausführliche Anleitung zum Beitreten zu einer Arbeitsgruppe Windows [beitreten zu oder erstellen eine Arbeitsgruppe](https://windows.microsoft.com/windows7/Join-or-create-a-workgroup).  
  
3.  Entfernen Sie den Computer mithilfe des Dashboards vom Server. Eine schrittweise Anleitung finden Sie unter [Entfernen eines Computers vom Server](../manage/Manage-Devices-in-Windows-Server-Essentials.md#BKMK_3).  
  
 Um einen Computer mit dem Server die Verbindung wiederherzustellen, die zuvor aus dem Windows Server Essentials-Server-Netzwerk getrennt wurde, müssen Sie die folgenden Schritte ausführen:  
  

1.  Deinstallieren Sie die Connector-Software auf dem Computer mithilfe der Systemsteuerung. Eine schrittweise Anleitung finden Sie unter [deinstallieren die Connector-Software](Get-Connected-in-Windows-Server-Essentials.md#BKMK_13).  
  
2.  Entfernen Sie den Computer aus der Windows Server Essentials-Domäne, und fügen Sie ihn der Arbeitsgruppe hinzu. Eine ausführliche Anleitung zum Beitreten zu einer Arbeitsgruppe Windows [beitreten zu oder erstellen eine Arbeitsgruppe](https://windows.microsoft.com/windows7/Join-or-create-a-workgroup).  
  
3.  Verbinden Sie den Computer mithilfe des Assistenten zum Verbinden eines Computers mit dem Server. Eine schrittweise Anleitung finden Sie unter [Verbinden von Computern mit dem Server](Get-Connected-in-Windows-Server-Essentials.md#BKMK_9).  
  
###  <a name="BKMK_Sleep"></a>Wie Sicherung im Energiesparmodus und Ruhezustand  
 Bei Auswahl der **Reaktivieren des Computers für die Sicherung** Option, wenn Sie einen Computer mit dem Server, dem Computer verbinden automatisch Reaktivieren aus dem Standbymodus oder Ruhezustand gemäß dem Sicherungszeitplan täglich, damit sie gesichert werden können. Nachdem die Sicherung abgeschlossen ist, wird der Computer in den Energiesparmodus oder Ruhezustand versetzt, basierend auf den energieverwaltungseinstellungen zurück. Wenn Sie diese Option nicht auswählen, wird der Server Einrichten eines Computers nicht sichern, wenn der Computer im Energiesparmodus oder Ruhezustand ist. Weitere Informationen finden Sie unter [Verwalten der Clientsicherung](../manage/Manage-Client-Computer-Backup-in-Windows-Server-Essentials.md).  
  
##  <a name="BKMK_C"></a>Verwenden des LaunchPads  
 Sie können das Launchpad auf freigegebene Ressourcen auf dem Windows Server Essentials-Server zuzugreifen, computersicherungen auszuführen und auf integritätswarnungen zu reagieren.  
  
-   [Übersicht über die Launchpad](../manage/Overview-of-the-Launchpad-in-Windows-Server-Essentials.md)  
  
-   [Verwenden des LaunchPads mit einem Macintosh-computer](../manage/Overview-of-the-Launchpad-in-Windows-Server-Essentials.md#BKMK_Mac)  
  
## <a name="see-also"></a>Siehe auch  
  
-   [Problembehandlung beim Verbinden von Computern mit dem server](../support/Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md)  
  
-   [Verwalten von Benutzerkonten](../manage/Manage-User-Accounts-in-Windows-Server-Essentials.md)  
  

-   [Verwenden von freigegebenen Ordnern](Use-Shared-Folders-in-Windows-Server-Essentials.md)  
  
-   [Remote-Arbeit](Work-Remotely-in-Windows-Server-Essentials.md)  
  
-   [Wiedergeben von digitalen Medien](Play-Digital-Media-in-Windows-Server-Essentials.md)

-   [Verwenden von freigegebenen Ordnern](../use/Use-Shared-Folders-in-Windows-Server-Essentials.md)  
  
-   [Remote-Arbeit](../use/Work-Remotely-in-Windows-Server-Essentials.md)  
  
-   [Wiedergeben von digitalen Medien](../use/Play-Digital-Media-in-Windows-Server-Essentials.md)

