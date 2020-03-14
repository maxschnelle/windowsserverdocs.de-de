---
title: Herstellen einer Verbindung in Windows Server Essentials
description: Beschreibt die Verwendung von Windows Server Essentials
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
ms.openlocfilehash: 04d09574046474da5bee4437628ade9646cf58ca
ms.sourcegitcommit: 0a0a45bec6583162ba5e4b17979f0b5a0c179ab2
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79322122"
---
# <a name="get-connected-in-windows-server-essentials"></a>Herstellen einer Verbindung in Windows Server Essentials

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

 Verwenden Sie die Connector-Software, um Ihre Computer mit dem Windows Server Essentials-Server zu verbinden. Die Connector-Software wird installiert, wenn Sie einen Computer mithilfe des Assistenten "Computer mit dem Server verbinden" mit dem Server verbinden. Sie können diesen Assistenten starten, indem Sie **http://< Servername\>/Connect**eingeben, wobei **< Servername\>** der Name des Servers ist.  

 In diesem Abschnitt:  


-   [Vorbereiten der Verbindung von Computern mit dem Server](Get-Connected-in-Windows-Server-Essentials.md#BKMK_A)  

-   [Verbinden von Computern mit dem Server mithilfe der Connector-Software](Get-Connected-in-Windows-Server-Essentials.md#BKMK_B)  

-   [Verwenden des Launchpad](Get-Connected-in-Windows-Server-Essentials.md#BKMK_C)  

-   [Vorbereiten der Verbindung von Computern mit dem Server](Get-Connected-in-Windows-Server-Essentials.md#BKMK_A)  

-   [Verbinden von Computern mit dem Server mithilfe der Connector-Software](Get-Connected-in-Windows-Server-Essentials.md#BKMK_B)  

-   [Verwenden des Launchpad](Get-Connected-in-Windows-Server-Essentials.md#BKMK_C)  


##  <a name="BKMK_A"></a>Vorbereiten der Verbindung von Computern mit dem Server  
 In diesem Abschnitt wird Folgendes erläutert: die Connector-Software, die von Windows Server Essentials unterstützten Betriebssysteme, die Aufgaben, die vor dem Verbinden der Computer mit dem Server ausgeführt werden müssen, und die Änderungen, die der Server auf den Computern vornimmt, wenn Sie die Connector-Software ausführen.  


-   [Connector-Software Übersicht](Get-Connected-in-Windows-Server-Essentials.md#BKMK_1)  

-   [Voraussetzungen zum Verbinden eines Computers mit dem Server](Get-Connected-in-Windows-Server-Essentials.md#BKMK_2)  

-   [Voraussetzungen zum Verbinden eines Mac-Computers mit dem Netzwerk](Get-Connected-in-Windows-Server-Essentials.md#BKMK_3)  

-   [Unterstützte Betriebssysteme für Client Computer](Get-Connected-in-Windows-Server-Essentials.md#BKMK_4)  

-   [Änderungen, die der Server auf einem Client Computer vornimmt](Get-Connected-in-Windows-Server-Essentials.md#BKMK_5)  

-   [Informationen zum Netzwerk Benutzernamen und-Kennwort](Get-Connected-in-Windows-Server-Essentials.md#BKMK_6)  

-   [Konto des Server Administrators](Get-Connected-in-Windows-Server-Essentials.md#BKMK_7)  

-   [Entfernen eines Computers aus einer Windows-Domäne](Get-Connected-in-Windows-Server-Essentials.md#BKMK_8)  

###  <a name="BKMK_1"></a>Connector-Software Übersicht  
 Die Connector-Software für das Betriebssystem Windows Server Essentials verbindet die Computer in Ihrem Netzwerk mit dem Windows Server Essentials-Server. Wenn Sie die Computer mit dem Server verbinden, ermöglicht es Ihnen die Connector-Software, die Computer automatisch zu sichern und ihren Zustand zu überwachen. Mithilfe der Connector-Software ist es auch möglich, den Windows Server Essentials-Server zu konfigurieren und remote zu verwalten. Die Connector-Software wird installiert, wenn Sie einen Clientcomputer mit dem Server verbinden. Ausführliche Anweisungen zum Verbinden von Clientcomputern mit dem Windows Server Essentials-Server finden Sie unter [Verbinden von Computern mit dem Server](Get-Connected-in-Windows-Server-Essentials.md#BKMK_9) weiter unten in diesem Thema.  

-   [Connector-Software Übersicht](Get-Connected-in-Windows-Server-Essentials.md#BKMK_1)  

-   [Voraussetzungen zum Verbinden eines Computers mit dem Server](../use/Get-Connected-in-Windows-Server-Essentials.md#BKMK_2)  

-   [Voraussetzungen zum Verbinden eines Mac-Computers mit dem Netzwerk](Get-Connected-in-Windows-Server-Essentials.md#BKMK_3)  

-   [Unterstützte Betriebssysteme für Client Computer](Get-Connected-in-Windows-Server-Essentials.md#BKMK_4)  

-   [Änderungen, die der Server auf einem Client Computer vornimmt](Get-Connected-in-Windows-Server-Essentials.md#BKMK_5)  

-   [Informationen zum Netzwerk Benutzernamen und-Kennwort](Get-Connected-in-Windows-Server-Essentials.md#BKMK_6)  

-   [Konto des Server Administrators](Get-Connected-in-Windows-Server-Essentials.md#BKMK_7)  

-   [Entfernen eines Computers aus einer Windows-Domäne](Get-Connected-in-Windows-Server-Essentials.md#BKMK_8)  

###  <a name="BKMK_1"></a>Connector-Software Übersicht  
 Die Connector-Software für das Betriebssystem Windows Server Essentials verbindet die Computer in Ihrem Netzwerk mit dem Windows Server Essentials-Server. Wenn Sie die Computer mit dem Server verbinden, ermöglicht es Ihnen die Connector-Software, die Computer automatisch zu sichern und ihren Zustand zu überwachen. Mithilfe der Connector-Software ist es auch möglich, den Windows Server Essentials-Server zu konfigurieren und remote zu verwalten. Die Connector-Software wird installiert, wenn Sie einen Clientcomputer mit dem Server verbinden. Ausführliche Anweisungen zum Verbinden von Clientcomputern mit dem Windows Server Essentials-Server finden Sie unter [Verbinden von Computern mit dem Server](Get-Connected-in-Windows-Server-Essentials.md#BKMK_9) weiter unten in diesem Thema.  


###  <a name="BKMK_2"></a>Voraussetzungen zum Verbinden eines Computers mit dem Server  
 Bevor Sie einen Computer mit dem Netzwerk verbinden, müssen die folgenden Anforderungen erfüllt sein:  

-   Die Installation von Windows Server Essentials muss abgeschlossen sein und der Server ausgeführt werden. Die Connector-Software beendet die Installation, wenn sie nicht mit dem Server kommunizieren kann.  


-   Auf dem Clientcomputer wird ein unterstütztes Betriebssystem ausgeführt. Weitere Informationen finden Sie unter [Unterstützte Betriebssysteme für Clientcomputer](Get-Connected-in-Windows-Server-Essentials.md#BKMK_4).


-   Der Clientcomputer hat eine gültige Verbindung mit dem Internet.  

-   Wenn der Clientcomputer sich im selben Netzwerk befindet wie der Server, auf dem Windows Server Essentials ausgeführt wird, muss sich der Clientcomputer in demselben IP-Subnetz wie der Server befinden.  

-   Auf dem Clientcomputer ist .NET Framework 4.5 installiert. Die Connector-Software installiert .NET Framework 4.5 automatisch.  

-   Der Clientcomputer erfüllt die folgenden Mindestsystemanforderungen:  

    -   1,4-GHz-Prozessor oder schneller  

    -   1 GB RAM oder mehr  

    -   1 GB verfügbarer Festplatten-Speicherplatz (ein Teil davon wird nach der Installation freigegeben)  

-   Die Boot-Partition (d. h. die Datenträgerpartition, auf der das Windows-Betriebssystem installiert ist), wird mit dem NTFS-Dateisystem formatiert.  

-   Der Computername enthält nicht mehr als 15 Zeichen.  

-   Der Computername enthält keine Unterstriche (_).  

-   Die Datums-und Uhrzeit Einstellungen des Computers richten sich an den Einstellungen auf dem Server.  

-   Ein Clientcomputer kann stets nur mit einem Windows Server Essentials-Server verbunden sein.  

-   Ein Clientcomputer, der bereits einer anderen Active Directory-Domäne angehört, kann keiner Windows Server Essentials-Domäne mehr beitreten.  

> [!NOTE]
> 
>  In einer lokalen Client Bereitstellung für Windows Server Essentials oder Windows Server Essentials können Sie Computer mit dem Server verbinden, ohne Sie zur Windows Server Essentials-Domäne hinzuzufügen. Diese Methode ist nicht für alle unterstützten Clientbetriebssysteme verfügbar und Features wie Gruppenrichtlinien und virtuelle private Netzwerke (VPN), die erfordern, dass ein Computer mit der Domäne verbunden ist, sind in diesem Fall ebenfalls nicht verfügbar. Anforderungen und Anleitungen finden Sie unter [Verbinden von Computern mit einem Windows Server Essentials-Server, ohne der Domäne beizutreten](Get-Connected-in-Windows-Server-Essentials.md#BKMK_10).  

 Schrittweise Anleitungen zum Verbinden eines Computers mit einem Server mit Windows Server Essentials finden Sie unter [Verbinden von Computern mit dem Server](Get-Connected-in-Windows-Server-Essentials.md#BKMK_9).  

>  In einer lokalen Client Bereitstellung für Windows Server Essentials oder Windows Server Essentials können Sie Computer mit dem Server verbinden, ohne Sie zur Windows Server Essentials-Domäne hinzuzufügen. Diese Methode ist nicht für alle unterstützten Clientbetriebssysteme verfügbar und Features wie Gruppenrichtlinien und virtuelle private Netzwerke (VPN), die erfordern, dass ein Computer mit der Domäne verbunden ist, sind in diesem Fall ebenfalls nicht verfügbar. Anforderungen und Anleitungen finden Sie unter [Verbinden von Computern mit einem Windows Server Essentials-Server, ohne der Domäne beizutreten](Get-Connected-in-Windows-Server-Essentials.md#BKMK_10).  

 Schrittweise Anleitungen zum Verbinden eines Computers mit einem Server mit Windows Server Essentials finden Sie unter [Verbinden von Computern mit dem Server](Get-Connected-in-Windows-Server-Essentials.md#BKMK_9).  


###  <a name="BKMK_3"></a>Voraussetzungen zum Verbinden eines Mac-Computers mit dem Netzwerk  
 Bevor Sie einen Mac mit dem Netzwerk verbinden, müssen die folgenden Anforderungen erfüllt sein:  

-   Die Installation des Server-Betriebssystems muss abgeschlossen sein und der Server ausgeführt werden. Die Connector-Software wird nicht installiert, wenn sie nicht mit dem Server kommunizieren kann.  

-   Auf dem Computer wird Mac OS X 10.5 (Leopard) oder höher ausgeführt.  

-   Der Computer befindet sich im gleichen IP-Subnetz wie der Server.  

-   Der Computer hat eine gültige Verbindung mit dem Internet.  

-   Stellen Sie sicher, dass der Computer die folgenden Mindestsystemanforderungen erfüllt:  

    -   1,4-GHz-Prozessor oder schneller  

    -   1 GB RAM oder mehr  

    -   1 GB verfügbarer Festplatten-Speicherplatz (ein Teil davon wird nach der Installation freigegeben)  

-   Ein Clientcomputer kann zu einem bestimmten Zeitpunkt nur mit einem Server verbunden sein.  

###  <a name="BKMK_4"></a>Unterstützte Betriebssysteme für Client Computer  
 Windows Server Essentials enthält für alle unterstützten Clientcomputer die gleichen Features. Dazu gehören Domain Join, Launchpad und clientseitige Integritätsbenachrichtigungen.  

> [!IMPORTANT]
>  Computer mit den Windows-Versionen Home, Starter oder Media Center können der Domäne nicht beitreten. Es ist außerdem nicht möglich, den Remotewebzugriff zu verwenden, um eine Verbindung mit diesen Computern herzustellen.  

#### <a name="windows-server-essentials"></a>Windows Server Essentials  
  Dieser Abschnitt gilt für einen Server, auf dem Windows Server Essentials ausgeführt wird, oder für einen Server, auf dem Windows Server 2012 R2 Standard oder Windows Server 2012 R2 Datacenter mit installierter Windows Server Essentials-Rolle ausgeführt wird. Die folgenden Betriebssysteme werden unterstützt:  

 **Windows 7-Betriebssysteme**  

- Windows 7 Home Basic SP1 (x86 und x64)  

- Windows 7 Home Premium SP1 (x86 und x64)  

- Windows 7 Professional SP1 (x86 und x64)  

- Windows 7 Ultimate SP1 (x86 und x64)  

- Windows 7 Enterprise SP1 (x86 und x64)  

- Windows 7 Starter SP1 (x86)  

  **Windows 8-Betriebssysteme**  

- Windows 8  

- Windows 8 Pro  

- Windows 8 Enterprise  

  **Betriebssysteme Windows 8.1**  

- Windows 8.1  

- Windows 8.1 Pro  

- Windows 8.1 Enterprise  

  **Windows 10-Betriebssysteme**  

- Windows 10  

- Windows 10 Pro  

- Windows 10 Enterprise  

- Windows 10 Education  

  **Macintosh-Client Computer**  

- Mac OS X v10.5 Leopard  

- Mac OS X v10.6 Snow Leopard  

- Mac OS X v10.7 Lion  

- Mac OS X v10.8 Mountain Lion  

> [!NOTE]
>  Sie können den Integritäts-und Sicherungs Status eines Macintosh-Computers über das Windows Server Essentials-Dashboard anzeigen. Allerdings ist es nicht möglich, Sicherungen vom Dashboard aus zu konfigurieren oder zu starten. Außerdem ist es nicht möglich, den Remotewebzugriff zu verwenden, um eine Verbindung mit einem Mac-Computer herzustellen.  

#### <a name="windows-server-essentials"></a>Windows Server Essentials  
  Dieser Abschnitt gilt für einen Server, auf dem Windows Server Essentials ausgeführt wird. Die folgenden Betriebssysteme werden unterstützt:  

 **Windows 7-Betriebssysteme**  

- Windows 7 Home Basic (x86 und x64)  

- Windows 7 Home Premium (x86 und x64)  

- Windows 7 Professional (x86 und x64)  

- Windows 7 Ultimate (x86 und x64)  

- Windows 7 Enterprise (x86 und x64)  

- Windows 7 Starter (x86)  

  **Windows 8-Betriebssysteme**  

- Windows 8  

- Windows 8 Pro  

- Windows 8 Enterprise  

  **Windows 10-Betriebssysteme**  

- Windows 10  

- Windows 10 Pro  

- Windows 10 Enterprise  

- Windows 10 Education  

  **Macintosh-Client Computer**  

- Mac OS X v10.5 Leopard  

- Mac OS X v10.6 Snow Leopard  

- Mac OS X v10.7 Lion  

> [!NOTE]
>  Sie können den Integritäts- und Sicherungsstatus eines Mac-Computers vom Windows Server Essentials-Dashboard aus anzeigen. Allerdings ist es nicht möglich, Sicherungen vom Dashboard aus zu konfigurieren oder zu starten. Außerdem ist es nicht möglich, den Remotewebzugriff zu verwenden, um eine Verbindung mit einem Mac-Computer herzustellen.  

###  <a name="BKMK_5"></a>Änderungen, die der Server auf einem Client Computer vornimmt  
 Wenn Sie einen Computer mit dem Server verbinden, nimmt Windows Server Essentials eine Reihe von Änderungen am Computer vor, damit Computer und Server zusammenarbeiten können.  

 Die Software führt Folgendes durch:  

-   Sie installiert die Connector-Software auf dem Computer.  

-   Sie installiert Microsoft .NET Framework 4.5 auf dem Computer, wenn es nicht bereits installiert ist.  

-   Erstellt Verknüpfungen auf dem Desktop des Computers mit dem Dashboard und dem launchpad.  

-   Sie konfiguriert die Windows Firewall-Ports auf dem Computer, damit die folgenden Funktionen ausgeführt werden können:  

    -   Kernnetzwerk  

    -   Remotedesktopdienste  

-   Sie nimmt die folgenden Änderungen am Computer vor, um Sicherungen zu vereinfachen:  

    -   Sie erstellt geplante Aufgaben zum Ausführen automatischer Sicherungen.  

    -   Sie installiert Dienste, die Sicherungsvorgänge mit dem Server verwalten.  

    -   Sie installiert einen virtuellen Gerätetreiber, der während der Wiederherstellungsvorgänge von Dateien und Ordnern verwendet wird.  

-   Sie installiert den Health Agent, um Integritätsprobleme zu erkennen und die entsprechenden Warnmeldungen zu erstellen.  

-   Sie erstellt auf dem Computer geplante Tasks für wiederkehrende Integritätsbewertungen und zur Synchronisierung der Definitionen von Integritätswarnungen.  

-   Sie fügt Dienste hinzu, die der Computer für die Kommunikation mit dem Server sowie mit anderen Windows Server Essentials-Funktionen verwendet.  

-   Sie öffnet den TCP-Port 3389 auf Clientcomputern mit Windows Clients, damit Remote Desktop Services ausgeführt werden können.  

-   Stellt VPN auf dem Client Computer bereit und bietet einen einfachen Mausklick, wenn die VPN-Funktionalität unter Windows Server Essentials aktiviert ist, oder bietet eine automatische Verbindung, wenn die VPN-Funktionalität unter Windows Server Essentials aktiviert ist.  


 Weitere Informationen zum Verbinden Ihres Computers mit dem Server finden Sie unter [Verbinden von Computern mit dem Server](Get-Connected-in-Windows-Server-Essentials.md#BKMK_9).  

###  <a name="BKMK_6"></a>Informationen zum Netzwerk Benutzernamen und-Kennwort  
 Sie erhalten Ihren Netzwerk-Benutzernamen und das Kennwort von der Person, die den Server verwaltet. Diese Anmeldeinformationen können Sie verwenden, um den Computer mit dem Server zu verbinden und auf Informationen vom Server zuzugreifen.  

###  <a name="BKMK_6"></a>Informationen zum Netzwerk Benutzernamen und-Kennwort  
 Sie erhalten Ihren Netzwerk-Benutzernamen und das Kennwort von der Person, die den Server verwaltet. Diese Anmeldeinformationen können Sie verwenden, um den Computer mit dem Server zu verbinden und auf Informationen vom Server zuzugreifen. 


 Wenn Sie der Serveradministrator sind, können Sie die Anmeldeinformationen für das Netzwerk durch Hinzufügen eines Benutzerkontos aus der Dashboard-Registerkarte **Benutzer** erstellen. Weitere Informationen über Benutzerkonten finden Sie unter [Verwalten von Benutzerkonten mithilfe des Dashboards](../manage/Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Manage8).  

###  <a name="BKMK_7"></a>Konto des Server Administrators  
 Sie müssen den Namen und das Kennwort des Netzwerkadministratorkontos angeben, um die Connector-Software installieren zu können. Ein Netzwerkadministratorkonto ermöglicht es dem Benutzer, das lokale Netzwerk der Organisation zu verwalten, und hilft, Netzwerkgeräte wie Switches und Router zu verwalten und zu warten.  

 Zu den Aufgaben, die mit einem Netzwerkadministratorkonto durchgeführt werden können, zählen:  

- Installieren von Netzwerkanwendungen und anderer Software  

- Verwalten von Speicher auf dem Server  

- Verteilen von Softwareupdates  

- Durchführen regelmäßiger Sicherungen  

- Überwachen der täglichen Aktivitäten im Netzwerk  

  In Windows Server Essentials, Windows Server Essentials und Windows Server 2012 R2 mit installierter Windows Server Essentials-Rolle können Sie jedem Benutzerkonto die Zugriffsebene für den Netzwerkadministrator zuweisen. Dadurch werden dem Benutzer die erforderlichen Berechtigungen zum Ausführen der Aufgaben eines Netzwerkadministrators gewährt. Wenn einem Benutzer die Zugriffsebene "Netzwerkadministrator" zugewiesen wird, öffnet sich die Eingabeaufforderung **Steuerung des Benutzerzugriffs** für jede Aufgabe, die Administratorberechtigungen erfordert.  

###  <a name="BKMK_8"></a>Entfernen eines Computers aus einer Windows-Domäne  
 Um einen Computer aus der Domäne zu entfernen, werden Sie aufgefordert, den Benutzernamen und das Kennwort für das Domänenkonto anzugeben.  

##### <a name="to-remove-a-computer-from-a-windows-domain"></a>So entfernen Sie einen Computers aus einer Windows-Domäne  

1.  Klicken Sie auf **Start**und mit der rechten Maustaste auf **Computer**und klicken Sie dann auf **Eigenschaften**.  

2.  Klicken Sie unter **Einstellungen für Computernamen, Domäne und Arbeitsgruppe** auf **Einstellungen ändern**.  

    > [!NOTE]
    >  Wenn Sie aufgefordert werden, ein Administratorkennwort oder eine Bestätigung anzugeben, geben Sie das Domänenkennwort ein oder erteilen Sie die Bestätigung.  

3.  Klicken Sie im Dialogfeld **Systemeigenschaften** auf die Registerkarte **Computername** und klicken Sie dann auf **Ändern**.  

4.  Klicken Sie im Dialogfeld **Änderungen an Computernamen/Domäne** unter **Mitglied** auf **Arbeitsgruppe** und führen Sie eine der folgenden Optionen aus:  

    1.  Um einer bestehenden Arbeitsgruppe beizutreten, geben Sie den Namen der Arbeitsgruppe ein und klicken Sie dann auf **OK**.  

    2.  Um eine Arbeitsgruppe zu erstellen, geben Sie den Namen der Arbeitsgruppe ein und klicken Sie dann auf **OK**.  

        > [!NOTE]
        >  Der Computer wird aus der Domäne entfernt und das Konto in dieser Domäne deaktiviert.  

##  <a name="BKMK_B"></a>Verbinden von Computern mit dem Server mithilfe der Connector-Software  
 In diesem Abschnitt werden Informationen und Verfahren erläutert, die Ihnen bei der Installation der Connector-Software, beim Verbinden des Computers mit dem Server und der damit verbundenen Problembehandlung helfen.  


-   [Verbinden von Computern mit dem Server](Get-Connected-in-Windows-Server-Essentials.md#BKMK_9)  

-   [Verbinden von Computern mit einem Windows Server Essentials-Server ohne Beitritt zur Domäne](Get-Connected-in-Windows-Server-Essentials.md#BKMK_10)  

-   [Installieren der Connector-Software](Get-Connected-in-Windows-Server-Essentials.md#BKMK_11)  

-   [Manuelles Verschieben von Computer Daten und-Einstellungen](Get-Connected-in-Windows-Server-Essentials.md#BKMK_12)  

-   [Übertragen mehrerer Benutzerprofile während der Bereitstellung des Computers](Get-Connected-in-Windows-Server-Essentials.md#BKMK_Transfer)  

-   [Deinstallieren der Connector-Software](Get-Connected-in-Windows-Server-Essentials.md#BKMK_13)  

-   [Trennen Sie den Computer, oder verbinden Sie den Computer erneut mit dem Server.](Get-Connected-in-Windows-Server-Essentials.md#BKMK_14)  

-   [Funktionsweise der Sicherung mit dem Modus "Standby" und "Ruhezustand"](Get-Connected-in-Windows-Server-Essentials.md#BKMK_Sleep)  

-   [Verbinden von Computern mit dem Server](Get-Connected-in-Windows-Server-Essentials.md#BKMK_9)  

-   [Verbinden von Computern mit einem Windows Server Essentials-Server ohne Beitritt zur Domäne](Get-Connected-in-Windows-Server-Essentials.md#BKMK_10)  

-   [Installieren der Connector-Software](Get-Connected-in-Windows-Server-Essentials.md#BKMK_11)  

-   [Manuelles Verschieben von Computer Daten und-Einstellungen](Get-Connected-in-Windows-Server-Essentials.md#BKMK_12)  

-   [Übertragen mehrerer Benutzerprofile während der Bereitstellung des Computers](Get-Connected-in-Windows-Server-Essentials.md#BKMK_Transfer)  

-   [Deinstallieren der Connector-Software](Get-Connected-in-Windows-Server-Essentials.md#BKMK_13)  

-   [Trennen Sie den Computer, oder verbinden Sie den Computer erneut mit dem Server.](Get-Connected-in-Windows-Server-Essentials.md#BKMK_14)  

-   [Funktionsweise der Sicherung mit dem Modus "Standby" und "Ruhezustand"](Get-Connected-in-Windows-Server-Essentials.md#BKMK_Sleep)  


###  <a name="BKMK_9"></a>Verbinden von Computern mit dem Server  
 Wenn Sie einen Computer mit einem Server verbinden, auf dem Windows Server Essentials oder Windows Server 2012 R2 mit installierter Windows Server Essentials-Rolle ausgeführt wird, müssen Sie sicherstellen, dass der Client Computer über eine gültige Verbindung mit dem Internet verfügt.  

 Führen Sie das folgende Verfahren auf allen Clientcomputern aus, um sie mit dem Server zu verbinden.  

 Um den Vorgang abzuschließen, benötigen Sie folgende Informationen:  

-   Den Benutzernamen und das Kennwort der Person, die den Computer im neuen Netzwerk verwendet  

-   Der Benutzername und das Kennwort des lokalen Administrator Kontos des Computers  

> [!NOTE]
> 
>  In einer lokalen Client Bereitstellung für Windows Server Essentials oder Windows Server Essentials können Sie Computer mit dem Server verbinden, ohne Sie zur Windows Server Essentials-Domäne hinzuzufügen. Diese Methode ist nicht für alle unterstützten Clientbetriebssysteme verfügbar und Features wie Gruppenrichtlinien und virtuelle private Netzwerke (VPN), die erfordern, dass ein Computer mit der Domäne verbunden ist, sind in diesem Fall ebenfalls nicht verfügbar. Anforderungen und Anleitungen finden Sie unter [Verbinden von Computern mit einem Windows Server Essentials-Server, ohne der Domäne beizutreten](Get-Connected-in-Windows-Server-Essentials.md#BKMK_10).  
> 
>  In einer lokalen Client Bereitstellung für Windows Server Essentials oder Windows Server Essentials können Sie Computer mit dem Server verbinden, ohne Sie zur Windows Server Essentials-Domäne hinzuzufügen. Diese Methode ist nicht für alle unterstützten Clientbetriebssysteme verfügbar und Features wie Gruppenrichtlinien und virtuelle private Netzwerke (VPN), die erfordern, dass ein Computer mit der Domäne verbunden ist, sind in diesem Fall ebenfalls nicht verfügbar. Anforderungen und Anleitungen finden Sie unter [Verbinden von Computern mit einem Windows Server Essentials-Server, ohne der Domäne beizutreten](Get-Connected-in-Windows-Server-Essentials.md#BKMK_10).  


##### <a name="to-connect-a-client-computer-to-the-server"></a>So verbinden Sie einen Clientcomputer mit dem Server  

1.  Melden Sie sich an dem Computer an, den Sie mit dem Server verbinden möchten.  

    > [!NOTE]
    >  Wenn auf diesem Computer mehrere Benutzerkonten vorhanden sind, melden Sie sich mit dem Benutzerkonto an, dessen Dokumente, Bilder und persönliche Einstellungen Sie nach dem Verbinden mit dem Server beibehalten möchten.  

2.  Öffnen Sie einen Internetbrowser, z. B. Internet Explorer.  

3.  Geben Sie in der Adressleiste **http://< Servername\>/Connect**ein, und drücken Sie dann die EINGABETASTE.  

    > [!NOTE]
    >  Wenn sich Ihr Computer an einem Remote Standort außerhalb des Windows Server Essentials-Netzwerks befindet, geben Sie zum Ausführen des Assistenten zum Verbinden eines Computers mit dem Server in der Adressleiste des Webbrowsers **http://< Domainname\>/Connect** ein. dabei ist < Domänen\> der Domänen Name Ihrer Organisation). Ihre Domänennamensinformationen können Sie von Ihrem Netzwerkadministrator abrufen.  

4.  Die Seite **Computer mit dem Server verbinden** wird angezeigt. Führen Sie eine der folgenden Aktionen aus:  

    -   Wenn auf dem Computer das Windows-Betriebssystem ausgeführt wird, klicken Sie auf **Software für Windows herunterladen**.  

    -   Klicken Sie auf **Software für Mac herunterladen**, wenn auf dem Computer Mac OS X oder höher ausgeführt wird.  

5.  Klicken Sie in der Warnmeldung zur Downloadsicherheit auf **Ausführen**.  

6.  Wenn die Meldung zur Benutzerkontensteuerung angezeigt wird, klicken Sie auf **Ja** , oder geben Sie den lokalen Benutzernamen und das zugehörige Kennwort ein, wenn Sie dazu aufgefordert werden.  

7.  Der Assistent zum Verbinden eines Computers mit dem Server wird angezeigt. Führen Sie die folgenden Schritte aus, um den Assistenten zu beenden:  

    1.  Akzeptieren Sie den Endbenutzer-Lizenzvertrag.  

    2.  Führen Sie auf der Seite **Meinen Server suchen** die automatische Erkennung des Servers in den lokalen Netzwerken durch und wählen Sie den Server, mit dem Sie die Verbindung herstellen möchten. Wenn Sie über die Informationen verfügen, können Sie den Namen oder die Domänen Adresse des Servers manuell eingeben.  

    3.  Geben Sie auf der Seite **Neuen Netzwerkbenutzernamen und Kennwort eingeben** Folgendes ein:  

        -   Wenn dies der erste Computer ist, den Sie mit dem Server verbinden, und dieser Computer für die Verwaltung des Servers verwendet wird, dann melden Sie sich mit dem Administratorkonto an, das während des Setups erstellt wurde.  

        -   Richten Sie für alle anderen Computer zunächst mithilfe des Dashboards ein Netzwerkbenutzerkonto auf dem Server ein. Erstellen Sie das Benutzerkonto mit Administrator- oder Standardbenutzerrechten, je nach den Aufgaben, die von der Person ausgeführt werden, die den Computer verwendet.  

    4.  Wenn auf Ihrem Computer Windows 8, Windows 8.1 oder Windows 10 ausgeführt wird, überspringen Sie diesen Schritt. Wenn auf dem Computer Windows 7 ausgeführt wird und Ihre Dokumente, Bilder oder persönlichen Einstellungen (z. B. Desktophintergrundbilder, Bildschirmschoner oder Internet Explorer-Favoriten) noch verfügbar sein sollen, nachdem Sie diesen Computer dem neuen Netzwerk hinzugefügt haben, können Sie auf der Seite **Vorhandene Daten und Einstellungen verschieben** des Assistenten die Option **Daten und Einstellungen in neues Netzwerkbenutzerkonto verschieben**auswählen.  

    5.  Auf der Seite **Wählen Sie aus, ob der Ruhezustand des Computers zum Erstellen der Sicherung deaktiviert werden soll** können Sie auswählen, ob der Ruhezustand des Computers zum Erstellen der Sicherung automatisch deaktiviert werden soll.  

    6.  Befolgen Sie die verbleibenden Anweisungen des Assistenten, um den Computer dem Netzwerk hinzuzufügen.  

8.  Nachdem Sie den Computer dem Netzwerk hinzugefügt haben, können Sie sich mit Ihrem neuen Benutzernamen und dem zugehörigen Kennwort am Computer anmelden.  

    > [!NOTE]
    >  Wenn Sie sich das erste Mal mit Ihrem Netzwerkkonto an einem Computer anmelden, auf dem Windows 8 ausgeführt wird, nachdem er mit Ihrem Server verbunden wurde, erhalten Sie Anweisungen zur Migration von Dateien und Anwendungen von Ihrem alten Benutzerkonto. Befolgen Sie die Anweisungen auf der Seite **Wie kann ich Dateien und Anwendungen von meinem alten Benutzerkonto migrieren?** , um alle Dateien und Anwendungen zu Ihrem Netzwerkbenutzerkonto zu migrieren.  

9. Nachdem der Computer erfolgreich mit dem Server verbunden wurde, werden im Startmenü Verknüpfungen mit der Connector trayapp und dem Server Dashboard angezeigt. Diese können wie folgt verwendet werden (wenn auf dem Computer Windows 8, Windows 8.1 oder Windows 10, das Dashboard und der Connector ausgeführt wird. Trayapp wird auf dem Start Bildschirm des Computers verfügbar sein):  

    -   Wenn auf Ihrem Computer Windows 8, Windows 8.1 oder Windows 10 ausgeführt wird, können das Dashboard und die Connector trayapp als App durchsucht werden.  

    -   In der Connector TrayApp können Sie die Funktion **Remote verbunden bleiben** aktivieren und deaktivieren. Sie können die TrayApp auch doppelklicken, um das Launchpad zu starten. Über das Launchpad erhalten Sie Zugriff auf die Verknüpfung "Freigegebene Ordner", können Computersicherungen konfigurieren, Warnungen bearbeiten und die Website für den Remotezugriff öffnen.  

    -   Über die Verknüpfung **Dashboard** können Sie den Server verwalten.  

###  <a name="BKMK_10"></a>Verbinden von Computern mit einem Windows Server Essentials-Server ohne Beitritt zur Domäne  
 In diesem Thema wird beschrieben, wie ein Windows 7-, Windows 8-, Windows 8.1-oder Windows 10-Computer zu einem Windows Server Essentials-Netzwerk hinzugefügt wird, ohne dass der Computer der Windows Server Essentials-Domäne in einer lokalen Client Bereitstellung hinzugefügt wird. Diese Verbindungsmethode wird in Windows Server Essentials und Windows Server Essentials unterstützt.  

 Dies ist eine Alternative zu der üblichen-Methode, bei der es erforderlich ist, den Computer zur Windows Server Essentials-Domäne hinzuzufügen. Bei dieser Methode muss der Computer, wenn er sich in einer anderen Domäne befindet, aus dieser entfernt werden, bevor er zur Windows Server Essentials-Domäne hinzugefügt werden kann.  

#### <a name="feature-limits"></a>Einschränkungen  
 Einige Funktionen sind eingeschränkt verfügbar, wenn der Clientcomputer nicht zur Windows Server Essentials-Domäne hinzugefügt wird:  

-   Alle Features, die erfordern, dass der Computer der Domäne hinzugefügt wird? einschließlich Domänen Anmelde Informationen, Gruppenrichtlinie und VPNs (virtuelle private Netzwerke)? sind nicht verfügbar.  

-   Add-Ons von Drittanbietern, die es erfordern, dass der Computer der Domäne beitritt, werden nicht ordnungsgemäß funktionieren.  

-   Diese Methode kann nicht verwendet werden, um einen externen Computer mit dem Server zu verbinden.  

#### <a name="prerequisites"></a>Erforderliche Komponenten  

-   Der Computer muss über eine physische Verbindung mit dem lokalen Netzwerk verfügen.  

-   Eines der folgenden Betriebssysteme muss auf dem Computer installiert sein:  

    -   Windows 10 Pro, Windows 10 Enterprise  

    -    Windows 8.1 pro, Windows 8.1 Enterprise, Windows 8 pro, Windows 8 Enterprise  

    -    Windows 7 Professional (x86 und x64), Windows 7 Enterprise (x86 und x64), Windows 7 Ultimate (x86 und x64)  


-   Der Computer muss alle anderen Anforderungen an Clientcomputer in Windows Server Essentials erfüllen. Weitere Informationen finden Sie unter [Voraussetzungen zum Verbinden eines Computers mit dem Server](Get-Connected-in-Windows-Server-Essentials.md#BKMK_2).  


-   Um eine Verbindung herzustellen, ohne einer Domäne beizutreten, müssen Sie sich auf dem Computer mit einem Konto anmelden, das Mitglied der lokalen Administratorengruppe ist.  

-   Um den Computer mit dem Windows Server Essentials-Server zu verbinden, benötigen Sie die folgenden Informationen:  

    -   Ein Konto mit Administratorrechten auf Windows Server Essentials (Ihr Konto).  

    -   Den Benutzernamen und das Kennwort für das Domänenkonto der Person, die den Computer verwendet. Das Domänenkonto muss auch über Administratorrechte auf dem Windows Server Essentials-Server verfügen.  

#### <a name="connect-to-a-windows-server-essentials-network"></a>Herstellen einer Verbindung mit einem Windows Server Essentials-Netzwerk  
 Nachdem Sie sich vergewissert haben, dass alle Voraussetzungen erfüllt sind, verbinden Sie den Computer mit dem Windows Server Essentials-Netzwerk.  

###### <a name="to-connect-a-computer-in-a-different-domain-to-a-windows-server-essentials-network"></a>Verbinden eines Computers in einer anderen Domäne mit einem Windows Server Essentials-Netzwerk  

1.  Melden Sie sich auf dem Clientcomputer mit einem Konto an, das Mitglied der lokalen Administratorengruppe ist.  

2.  Öffnen Sie eine Eingabeaufforderung mit Administratorrechten.  

    -   Klicken Sie unter Windows 10 auf die Schaltfläche **Start** , wählen Sie **alle apps** -> **Windows-System Tools** -> **Eingabeaufforderung**aus, klicken Sie mit der rechten Maustaste auf Eingabeaufforderung, und klicken Sie dann auf **als Administrator ausführen**.  

    -   Geben Sie in Windows 8 auf der **Start** Seite **Command** ein, und drücken Sie dann die EINGABETASTE. Klicken Sie in den Ergebnissen mit der rechten Maustaste auf **Eingabeaufforderung**und dann auf **Als Administrator ausführen**.  

    -   Geben Sie in Windows 7 im **Startmenü** den **Befehl Befehl** in das Suchfeld ein, klicken Sie mit der rechten Maustaste auf **Eingabeaufforderung**, und klicken Sie dann auf **als Administrator ausführen**.  

3.  Geben Sie an der Eingabeaufforderung den folgenden Befehl ein und drücken Sie dann die EINGABETASTE:  

    ```  
    reg add "HKLM\SOFTWARE\Microsoft\Windows Server\ClientDeployment" /v SkipDomainJoin /t REG_DWORD /d 1  
    ```  


4.  Führen Sie die Schritte in [Verbinden von Computern mit dem Server](Get-Connected-in-Windows-Server-Essentials.md#BKMK_9) aus.  


####  <a name="BKMK_SecondServer"></a>Verbinden eines zweiten Servers mit dem Netzwerk  

###### <a name="to-join-a-second-server-to-the-network"></a>So verbinden Sie einen zweiten Server mit dem Netzwerk  

1.  Melden Sie sich bei dem Server an, den Sie mit dem Windows Server Essentials-Netzwerk verbinden möchten.  

2.  Öffnen Sie einen Internet Browser, und geben Sie in der Adressleiste **http://< Servername\>/Connect**ein, wobei *< Servername\>* der Name des Servers ist, auf dem Windows Server Essentials ausgeführt wird, und drücken Sie dann die EINGABETASTE.  

3.  Wenn die verstärkte Sicherheitskonfiguration für Internet Explorer auf dem Server aktiviert ist, den Sie mit dem Windows Server Essentials-Netzwerk verbinden möchten, führen Sie die folgenden Schritte aus; andernfalls überspringen Sie diesen Schritt.  

    1.  Zum Übernehmen der blockierenden Nachricht klicken Sie auf **Schließen**.  

    2.  Fügen Sie die Website " **http://< Servername\>/Connect** " wie folgt den vertrauenswürdigen Websites hinzu:  

        1.  Klicken Sie im Navigationsbereich des Browsers auf **Extras**und dann auf **Internetoptionen**.  

        2.  Klicken Sie auf die Registerkarte **Sicherheit** und dann auf **Vertrauenswürdige Sites**.  

        3.  Klicken Sie auf **Sites**.  

        4.  Die Website sollte im Feld **Diese Website zur Zone hinzufügen** angezeigt werden. Klicken Sie auf **Hinzufügen**.  

        5.  Klicken Sie auf **Schließen**und dann auf **OK**.  

    3.  Aktualisieren Sie die Webseite.  


    4.  Um den zweiten Server mit einem Server unter Windows Server Essentials zu verbinden, folgen Sie den Anweisungen unter [Verbinden von Computern mit dem Server](Get-Connected-in-Windows-Server-Essentials.md#BKMK_9).  


~~~
> [!NOTE]
>  Connecting a second server to a server running Windows Server Essentials differs from connecting to a client computer as follows:  
>   
>  -   There is no user profile migration; therefore, the current profile will not be migrated.  
> -   You cannot back up the second server by using client computer backup, and there is no option to wake up the computer for backup.  
~~~

 Nachdem Sie den zweiten Server mit einem Server mit Windows Server Essentials verbunden haben, werden die folgenden Features auf dem verbundenen Server bereitgestellt:  

- Updates und Benachrichtigungen funktionieren wie auf anderen Clientcomputern.  

- Online und Offline funktionieren wie auf anderen Clientcomputern.  

- Sie können sich über den Remotewebzugriff mit dem zweiten Server verbinden.  

- Der zweite Server wird in die Integritätsberichte aufgenommen, da Windows Server Essentials Warnungen im Zusammenhang mit diesem Server generiert.  

  Die Verwaltung des zweiten Servers über den Server mit Windows Server Essentials unterscheidet sich folgendermaßen von der Verwaltung anderer Clientcomputer:  

- Es gibt keinen Einstiegspunkt für TrayApp, Launchpad und Dashboard Client.  

- Der zweite Server ist in der Gruppe der **Server** auf der Registerkarte **Geräte** aufgeführt.  

- Da die Sicherung des Clientcomputers für den zweiten Server nicht unterstützt wird, wird der Sicherungsstatus als **Nicht unterstützt** angezeigt. Wenn Sie den zweiten Server auswählen und mit der rechten Maustaste anklicken, werden darüber hinaus keine mit Sicherung und Wiederherstellung verwandten Aufgaben für den zweiten Server angezeigt.  

- Wenn Sie den zweiten Server auswählen und dann auf die Aufgabe **Server Eigenschaften anzeigen** klicken, wird auf der Seite Eigenschaften des Servers keine Registerkarte **Sicherung** angezeigt.  

- Da in einem Windows Server-Betriebssystem keine Security Center vorhanden ist, wird der Sicherheitsstatus des zweiten Servers als **nicht zutreffend**angezeigt.  

- Der Gruppenrichtlinie Status des zweiten Servers wird als **nicht zutreffend**angezeigt.  

###  <a name="BKMK_11"></a>Installieren der Connector-Software  
 Die Connector-Software in Windows Server Essentials wird installiert, wenn Sie einen Computer mithilfe des Assistenten "Computer mit dem Server verbinden" mit dem Server verbinden. Sie können diesen Assistenten starten, indem Sie in der Adressleiste des Webbrowsers **http://< Servername\>/Connect** eingeben (wobei *< Servername\>* der Name Ihres Servers ist).  

> [!NOTE]
>  Wenn sich Ihr Computer an einem Remote Standort befindet, geben Sie zum Ausführen des Assistenten zum Verbinden eines Computers mit dem Server in der Adressleiste des Webbrowsers **http://< Domainname\>/Connect** ein (wobei *< Domänen\>* der Domänen Name Ihrer Organisation ist). Ihre Domänennamensinformationen können Sie von Ihrem Netzwerkadministrator abrufen.  

 Die Connector-Software führt Folgendes durch:  

-   Sie verbindet den Computer mit Windows Server Essentials.  

-   Sie sichert den Computer automatisch über Nacht, wenn Sie den Server zum Erstellen von Client-Sicherungen konfigurieren.  

-   Sie hilft dem Administrator bei der Überwachung des Zustands des Computers.  

-   Sie ermöglicht es Ihnen, Windows Server Essentials remote von Ihrem Computer zu Hause zu konfigurieren und zu verwalten.  


 Schrittweise Anweisungen zum Verbinden Ihres Computers mit dem Windows Server Essentials-Server finden Sie unter [Verbinden von Computern mit dem Server](Get-Connected-in-Windows-Server-Essentials.md#BKMK_9).   


###  <a name="BKMK_12"></a>Manuelles Verschieben von Computer Daten und-Einstellungen  
  Windows Server Essentials und Windows Server Essentials unterstützen die Migration von Benutzerprofilen nur für Client Computer, auf denen das Betriebssystem Windows 7 ausgeführt wird. Wenn Sie einen Windows 7-Computer mit dem Server verbinden, kann der Assistent zum Verbinden des Computers mit dem Server das Benutzerprofil automatisch migrieren.  

 Das Benutzerprofil kann nicht automatisch übertragen werden, wenn ein Windows 8-, Windows 8.1-oder Windows 10-Computer mit dem Server verbunden wird. Allerdings können Sie auf einem Windows 8-Computer Windows Easy Transfer verwenden, um Daten und Einstellungen von dem ursprünglichen lokalen Benutzer auf den Computer in der Domäne zu übertragen. Dazu müssen Sie Administrator des Windows 8-Quellcomputers wie auch des Windows 8-Zielcomputers sein. Informationen zur Verwendung von Windows Easy Transfer für das Übertragen von Dateien und Einstellungen finden Sie unter [Artikel 2735227](https://support.microsoft.com/kb/2735227) in der Microsoft Knowledge Base.  

###  <a name="BKMK_Transfer"></a>Übertragen mehrerer Benutzerprofile während der Bereitstellung des Computers  
 Vor dem Verbinden eines Computers unter Windows 7 oder Windows 7 SP1 mit dem Windows Server Essentials-Server müssen Sie zunächst die entsprechenden Netzwerkbenutzerkonten auf dem Server erstellen, um mehrere lokale Benutzerprofile zu übertragen. Weitere Informationen zum Erstellen von Netzwerk-Benutzerkonten finden Sie unter [Hinzufügen eines Benutzerkontos](../manage/Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Manage1).  

 Die Migration von Benutzerprofilen wird nur auf einem Computer unter Windows 7 (für Windows Server Essentials) oder Windows 7 SP1 (für Windows Server Essentials) unterstützt. Wenn Sie einen Computer mithilfe des Assistenten zum Verbinden des Computers mit dem Server mit dem Windows Server Essentials-Server verbinden, wird Ihnen eine Option angezeigt, mit der Sie die Benutzerdaten und Einstellungen alter lokaler Benutzerkonten in die neuen Netzwerkbenutzerkonten verschieben können. Dazu ordnen Sie auf der Seite **Verschieben vorhandener Benutzerdaten und Einstellungen** des Assistenten die Netzwerkbenutzerkonten den lokalen Benutzerkonten zu, um mehrere Benutzerprofile übertragen zu können.  

###  <a name="BKMK_13"></a>Deinstallieren der Connector-Software  
 Sie können die Connector-Software mithilfe der Systemsteuerung von einem Computer deinstallieren. Dies erfolgt in der Regel dann, wenn Probleme mit der Connector-Software auftreten oder Sie eine neuere Version der Connector-Software installieren müssen. Sie müssen dazu auf dem Computer als Administrator angemeldet sein.  

> [!IMPORTANT]
>  Wenn Sie auf einem Clientcomputer das Betriebssystem aktualisieren, wird die Connector-Software automatisch deinstalliert. Sie müssen die Connector-Software nach dem Upgrade neu installieren. Die bevorzugte Methode ist es, die Connector-Software zu deinstallieren, bevor Sie das Betriebssystem aktualisieren. Das Deinstallieren der Connector-Software nach Abschluss des Upgrades ist zwar akzeptabel, kann allerdings zu Statusunterschieden zwischen Clientcomputer und Server führen, solange die Connector-Software nicht deinstalliert und neu installiert wird.  

##### <a name="to-uninstall-connector-software-from-a-computer"></a>So deinstallieren Sie die Connector-Software von einem Computer  

1.  Öffnen Sie auf einem Computer unter Windows 7, Windows 8, Windows 8.1 oder Windows 10 die **Systemsteuerung**, und klicken Sie dann im Abschnitt **Programme** auf **installierte Updates anzeigen**.  

2.  Wählen Sie in der Liste der installierten Programme **Windows Server Essentials Connector**und klicken Sie dann auf **Deinstallieren**.  

3.  Klicken Sie auf der Seite "Warnung" auf **Ja**.  

4.  Wenn das Fenster zur **Benutzerkontensteuerung** angezeigt wird, klicken Sie auf **Zulassen**.  

5.  Wenn in Windows Server Essentials die Seite Windows Server Essentials-Connector mit dem Hinweis angezeigt wird, das Launchpad zu schließen, klicken Sie auf **OK**.  

6.  Warten Sie, bis das Programm deinstalliert ist. Nach dem Entfernen der Software wird **Windows Server Essentials Connector** nicht mehr in der Liste der installierten Programme oder Updates angezeigt. Außerdem werden die Verknüpfungen mit dem Launchpad und dem Dashboard nicht mehr auf dem Desktop des Computers angezeigt.  

> [!NOTE]
> - Das Deinstallieren der Connector-Software entfernt den Computer jedoch nicht aus der Liste der Computer, die auf der Registerkarte **GERÄTE** des Dashboard angezeigt sind. Um den Computer aus dem Dashboard zu entfernen, nutzen Sie die Anleitungen unter [Einen Computer vom Server entfernen](../manage/Manage-Devices-in-Windows-Server-Essentials.md#BKMK_3).  
>   -   Wenn Sie die Connector-Software deinstallieren, werden die freigegebenen Ordner auf dem Clientcomputer, die dem Server zugeordnet wurden, nicht gelöscht. Sie müssen sie manuell löschen.  
> 
> -   Das Deinstallieren der Connector-Software führt nicht dazu, dass der Computer die ursprüngliche Domäne verlässt. Sie müssen den Computer manuell aus der Domäne entfernen. Eine Anleitung dazu finden Sie unter [Entfernen eines Computers aus einer Windows-Domäne](Get-Connected-in-Windows-Server-Essentials.md#BKMK_8).  


###  <a name="BKMK_14"></a>Trennen Sie den Computer, oder verbinden Sie den Computer erneut mit dem Server.  
 Wenn Sie einen Computer vom Server trennen möchten, müssen Sie die folgenden Schritte ausführen:  


1. Deinstallieren Sie die Connector-Software mithilfe der Systemsteuerung von dem Computer. Schrittweise Anleitungen finden Sie unter [Deinstallieren der Connector-Software](Get-Connected-in-Windows-Server-Essentials.md#BKMK_13).   


2. Entfernen Sie den Computer aus der Windows Server Essentials-Domäne und fügen Sie ihn der Arbeitsgruppe hinzu. Schrittweise Anleitungen zum Beitreten zu einer Windows-Arbeitsgruppe finden Sie unter [Beitreten zu oder Erstellen von Arbeitsgruppen](https://windows.microsoft.com/windows7/Join-or-create-a-workgroup).  

3. Entfernen Sie den Computer mithilfe des Dashboards vom Server. Schrittweise Anleitungen finden Sie unter [Entfernen eines Computers vom Server](../manage/Manage-Devices-in-Windows-Server-Essentials.md#BKMK_3).  

   Um einen Computer, der aus dem Windows Server Essentials-Servernetzwerk entfernt wurde, wieder mit dem Server zu verbinden, müssen Sie die folgenden Schritte ausführen:  


4. Deinstallieren Sie die Connector-Software mithilfe der Systemsteuerung von dem Computer. Schrittweise Anleitungen finden Sie unter [Deinstallieren der Connector-Software](Get-Connected-in-Windows-Server-Essentials.md#BKMK_13).  

5. Entfernen Sie den Computer aus der Windows Server Essentials-Domäne und fügen Sie ihn der Arbeitsgruppe hinzu. Schrittweise Anleitungen zum Beitreten zu einer Windows-Arbeitsgruppe finden Sie unter [Beitreten zu oder Erstellen von Arbeitsgruppen](https://windows.microsoft.com/windows7/Join-or-create-a-workgroup).  

6. Verbinden Sie den Computer mithilfe des Assistenten zum Verbinden eines Computers mit dem Server erneut mit dem Server. Schrittweise Anleitungen finden Sie unter [Verbinden von Computern mit dem Server](Get-Connected-in-Windows-Server-Essentials.md#BKMK_9).  

###  <a name="BKMK_Sleep"></a>Funktionsweise der Sicherung mit dem Modus "Standby" und "Ruhezustand"  
 Wenn Sie beim Verbinden des Computers mit dem Server die Option **Diesen Computer für die Sicherung aus dem Ruhezustand aktivieren** wählen, wird der Computer gemäß dem Sicherungszeitplan täglich automatisch aus dem Energiesparmodus oder Ruhezustand aktiviert, damit die Sicherung durchgeführt werden kann. Nachdem die Sicherung abgeschlossen ist, wird der Computer basierend auf den Energieverwaltungseinstellungen wieder in den Energiesparmodus oder Ruhezustand versetzt. Wenn Sie diese Option nicht aktivieren, sichert der Server den Computer nicht, wenn dieser im Energiesparmodus oder Ruhezustand ist. Weitere Informationen finden Sie unter [Verwalten der Client Sicherung](../manage/Manage-Client-Computer-Backup-in-Windows-Server-Essentials.md).  

##  <a name="BKMK_C"></a>Verwenden des Launchpad  
 Sie können das Launchpad verwenden, um auf freigegebene Ressourcen auf dem Windows Server Essentials-Server zuzugreifen, Computersicherungen auszuführen und auf Integritätswarnungen zu reagieren.  

-   [Launchpad (Übersicht)](../manage/Overview-of-the-Launchpad-in-Windows-Server-Essentials.md)  

-   [Verwenden des LaunchPads mit einem Macintosh-Computer](../manage/Overview-of-the-Launchpad-in-Windows-Server-Essentials.md#BKMK_Mac)  

## <a name="see-also"></a>Siehe auch  

-   [Problembehandlung beim Verbinden von Computern mit dem Server](../support/Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md)  

-   [Verwalten von Benutzerkonten](../manage/Manage-User-Accounts-in-Windows-Server-Essentials.md)  


-   [Verwenden von freigegebenen Ordnern](Use-Shared-Folders-in-Windows-Server-Essentials.md)  

-   [Remote arbeiten](Work-Remotely-in-Windows-Server-Essentials.md)  

-   [Wiedergeben digitaler Medien](Play-Digital-Media-in-Windows-Server-Essentials.md)

-   [Verwenden von freigegebenen Ordnern](../use/Use-Shared-Folders-in-Windows-Server-Essentials.md)  

-   [Remote arbeiten](../use/Work-Remotely-in-Windows-Server-Essentials.md)  

-   [Wiedergeben digitaler Medien](../use/Play-Digital-Media-in-Windows-Server-Essentials.md)

