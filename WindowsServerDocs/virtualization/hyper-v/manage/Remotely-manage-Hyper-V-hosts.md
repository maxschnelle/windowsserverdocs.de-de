---
title: Remoteverwaltung von Hyper-V-hosts
description: Beschreibt die Versionskompatibilität zwischen Hyper-V-Hosts und Hyper-V-Manager und Herstellen einer Verbindung mit remote-Hosts in unterschiedlichen Umgebungen, einschließlich Domänen- und eigenständigen.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2d34e98c-6134-479b-8000-3eb360b8b8a3
author: KBDAzure
ms.author: kathydav
ms.date: 12/06/2016
ms.openlocfilehash: df66f308ee7999f97fe7e57a8b52256f2561faa2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59870231"
---
# <a name="remotely-manage-hyper-v-hosts-with-hyper-v-manager"></a>Remoteverwaltung von Hyper-V-Hosts mit Hyper-V-Manager

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows 10, Windows 8.1

Dieser Artikel listet die unterstützten Kombinationen von Hyper-V-Hosts und Hyper-V-Manager-Versionen und beschreibt, wie Sie Remote- und lokale Hyper-V-Hosts herstellen, damit Sie diese verwalten können. 

Hyper-V-Manager können Sie eine kleine Anzahl von lokalen und remote Hyper-V-Hosts zu verwalten. Es wird installiert, wenn Sie die Hyper-V-Verwaltungstools installieren, können entweder über eine vollständige Hyper-V-Installation oder einer Installation nur die Tools. Dies bedeutet, dass eine nur-Tools-Installation können Sie die Tools auf Computern verwenden, die die hardwareanforderungen für Hyper-V-Host nicht erfüllen. Weitere Informationen zu den hardwareanforderungen für Hyper-V-Hosts finden Sie unter [Systemanforderungen](..\System-requirements-for-Hyper-V-on-Windows.md).

Wenn Hyper-V-Manager nicht installiert ist, finden Sie unter den [Anweisungen](#install-hyper-v-manager) unten.

## <a name="supported-combinations-of-hyper-v-manager-and-hyper-v-host-versions"></a>Unterstützte Kombinationen von Hyper-V-Manager und Hyper-V-Host-Versionen

In einigen Fällen können Sie eine andere Version von Hyper-V-Manager als die Hyper-V-Version auf dem Host verwenden, wie in der Tabelle dargestellt. Wenn Sie dies tun, bietet Hyper-V-Manager für die Version von Hyper-V verfügbaren Funktionen auf dem Host, den Sie verwalten. Z. B. Wenn Sie die Version von Hyper-V-Manager in Windows Server 2012 R2 zur Remoteverwaltung von eines Hosts mit Hyper-V unter Windows Server 2012 verwenden, Sie verwenden, in Windows Server 2012 R2 verfügbaren Funktionen auf dem Hyper-V-Host nicht.

Die folgende Tabelle zeigt, welche Versionen von Hyper-V-Host Sie über eine bestimmte Version von Hyper-V-Manager verwalten können. Nur unterstützt, Betriebssystem, die angegeben sind. Weitere Informationen über den Supportstatus von einer bestimmten Betriebssystemversion verwenden die **Suche Product Lifecycle** Schaltfläche der [Microsoft Lifecycle Policy](https://support.microsoft.com/lifecycle) Seite. Im Allgemeinen können ältere Versionen von Hyper-V-Manager nur einen Hyper-V-Host, die unter die gleiche Version oder vergleichbare Windows Server-Version verwalten.

|Hyper-V-Manager-version | Hyper-V-Host-version|
|---|---|
|Windows 2016, Windows 10|– Windows Server 2016 – alle Editionen und Installationsoptionen "Optionen", einschließlich Nano Server-Instanz, und die entsprechende Version von Hyper-V-Server <br>– Windows Server 2012 R2 – alle Editionen und Installationsoptionen und entsprechende Version von Hyper-V-Server <br>– Windows Server 2012 – alle Editionen und Installationsoptionen und entsprechende Version von Hyper-V-Server <br> - Windows 10 <br> - Windows 8.1  |
| Windows Server 2012 R2, Windows 8.1 | – Windows Server 2012 R2 – alle Editionen und Installationsoptionen und entsprechende Version von Hyper-V-Server <br>– Windows Server 2012 – alle Editionen und Installationsoptionen und entsprechende Version von Hyper-V-Server <br>- Windows 8.1
| Windows Server 2012 | – Windows Server 2012 – alle Editionen und Installationsoptionen und entsprechende Version von Hyper-V-Server
| Windows Server 2008 R2 Servicepack 1, Windows 7 Servicepack 1 | – Windows Server 2008 R2 – alle Editionen und Installationsoptionen und entsprechende Version von Hyper-V-Server
| WindowsServer 2008, Windows Vista Servicepack 2 | – Windows Server 2008 – alle Editionen und Installationsoptionen und entsprechende Version von Hyper-V-Server

>[!NOTE]
>Service Pack-Unterstützung endete am 12. Januar 2016 für Windows 8. Weitere Informationen finden Sie unter den [Windows 8.1 – häufig gestellte Fragen](https://support.microsoft.com/help/18581).

## <a name="connect-to-a-hyper-v-host"></a>Verbindung zu einem Hyper-V-host

Zum Verbinden mit einem Hyper-V-Host von Hyper-V-Manager Maustaste **Hyper-V-Manager** im linken Bereich, und klicken Sie dann auf **Herstellen einer Verbindung mit Server**.

## <a name="manage-hyper-v-on-a-local-computer"></a>Verwalten von Hyper-V auf einem lokalen computer

Hyper-V-Manager keine Computer aufgeführt, die Hyper-V-host erst, wenn Sie den Computer, einschließlich von einem lokalen Computer hinzufügen. Gehen Sie dazu wie folgt vor:

1. Klicken Sie im linken Bereich mit der Maustaste **Hyper-V-Manager**.
2. Klicken Sie auf **eine Verbindung mit Server herstellen**.
3. Von **Computer auswählen**, klicken Sie auf **lokalen Computer** , und klicken Sie dann auf **OK**.

Wenn Sie keine Verbindung herstellen können:

* Es ist möglich, dass nur die Hyper-V-Verwaltungstools installiert sind. Suchen Sie nach dem Virtual Machine Management-Dienst, um zu überprüfen, dass Hyper-V-Plattform installiert ist. \(Öffnen Sie die Dienste-desktop-app: Klicken Sie auf **starten**, klicken Sie auf die **Suche starten** geben **"Services.msc"**, und drücken Sie dann die **EINGABETASTE**. Wenn der Virtual Machine Management-Dienst nicht aufgeführt ist, installieren Sie das Hyper-V-Plattform mithilfe der Anweisungen in [Installieren von Hyper-V](..\get-started\Install-the-Hyper-V-role-on-Windows-Server.md).\)
* Überprüfen Sie, dass die Hardware die Anforderungen erfüllt. Finden Sie unter [Systemanforderungen](..\System-requirements-for-Hyper-V-on-Windows.md).
* Überprüfen Sie, dass Ihr Benutzerkonto der Gruppe "Administratoren" oder die Gruppe "Hyper-V-Administratoren" angehört.

## <a name="manage-hyper-v-hosts-remotely"></a>Remoteverwaltung von Hyper-V-hosts  

Aktivieren Sie Remoteverwaltung auf dem lokalen Computer und die remote-Host, um remote Hyper-V-Hosts zu verwalten.

Öffnen Sie in Windows Server, Server-Manager \> **lokalen Server** \> **Remoteverwaltung** , und klicken Sie dann auf **zulassen von Remoteverbindungen auf diesem Computer**. 

Oder über eines der Betriebssysteme Windows PowerShell als Administrator, und führen Sie: 

```
Enable-PSRemoting
```

### <a name="connect-to-hosts-in-the-same-domain"></a>Herstellen einer Verbindung von Hosts in der gleichen Domäne mit

Für Windows 8.1 und früher, funktioniert die Remoteverwaltung nur, wenn der Host befindet sich in derselben Domäne und Ihrem lokalen Benutzerkonto auch auf dem Remotehost ist.

Wählen Sie zum Hinzufügen von einem Hyper-V-Remotehost zu Hyper-V-Manager **einem anderen Computer** in die **Computer auswählen** im Dialogfeld, und geben Sie des Hostnamen des Remotehosts Hostname, NetBIOS-Namen oder den vollqualifizierten Domänennamen \(FQDN\).

Hyper-V-Manager in Windows Server 2016 und Windows 10 bietet mehrere Typen von remote-Verbindung als vorherige Versionen, die in den folgenden Abschnitten beschrieben.  

### <a name="connect-to-a-windows-2016-or-windows-10-remote-host-as-a-different-user"></a>Mit einem Windows 2016 oder Windows 10-Remotehost als anderer Benutzer verbinden

Dadurch können Sie die Hyper-V-Host herstellen, wenn Sie nicht auf dem lokalen Computer als Benutzer ausführen, die ein Mitglied der Gruppe der Hyper-V-Administratoren oder der Gruppe "Administratoren" auf dem Hyper-V-Host ist. Gehen Sie dazu wie folgt vor:

1. Klicken Sie im linken Bereich mit der Maustaste **Hyper-V-Manager**.
1. Klicken Sie auf **eine Verbindung mit Server herstellen**.
1. Wählen Sie **als anderer Benutzer verbinden** in die **Computer auswählen** Dialogfeld.
1. Wählen Sie **Benutzer festlegen**.

>[!NOTE]
> Dies funktioniert nur für Windows Server 2016 oder Windows 10 **remote** Hosts.

### <a name="connect-to-a-windows-2016-or-windows-10-remote-host-using-ip-address"></a>Verbinden Sie mit einem Windows 2016 oder Windows 10 Remotehost über IP-Adresse

Gehen Sie dazu wie folgt vor:

1. Klicken Sie im linken Bereich mit der Maustaste **Hyper-V-Manager**.
1. Klicken Sie auf **eine Verbindung mit Server herstellen**.
1. Geben Sie die IP-Adresse in der **einem anderen Computer** Textfeld ein.

>[!NOTE]
> Dies funktioniert nur für Windows Server 2016 oder Windows 10 **remote** Hosts.

### <a name="connect-to-a-windows-2016-or-windows-10-remote-host-outside-your-domain-or-with-no-domain"></a>Verbinden Sie mit einem Windows 2016 oder Windows 10-Remotehost außerhalb der Domäne oder ohne Domäne

Gehen Sie dazu wie folgt vor:

1. Öffnen Sie auf dem Hyper-V-Host verwaltet werden eine Windows PowerShell-Sitzung als Administrator an.

1. Erstellen Sie die erforderlichen Firewallregeln für private Netzwerkzonen:   
   
   ```
   Enable-PSRemoting
   ```

2. Um remote-Zugriff auf Öffentliche Zonen zu ermöglichen, aktivieren Sie Firewallregeln für CredSSP und WinRM:
  
   ```
   Enable-WSManCredSSP -Role server
   ```

    Weitere Informationen finden Sie unter [Enable-PSRemoting](https://technet.microsoft.com/library/hh849694.aspx) und [Enable-WSManCredSSP](https://technet.microsoft.com/library/hh849872.aspx).

Konfigurieren Sie anschließend den Computer, den Sie zum Verwalten von Hyper-V-Hosts verwenden.

1. Öffnen Sie eine Windows PowerShell-Sitzung als Administrator an.
1. Führen Sie die folgenden Befehle:

     ```
     Set-Item WSMan:\localhost\Client\TrustedHosts -Value "fqdn-of-hyper-v-host"
     ```
     ```
     Enable-WSManCredSSP -Role client -DelegateComputer "fqdn-of-hyper-v-host"
     ```
1. Sie müssen möglicherweise auch die folgenden Gruppenrichtlinien konfigurieren: 
    * **Computerkonfiguration** \> **Administrative Vorlagen** \> **System** \> **Anmeldeinformationen Delegierung** \> **Delegierung von aktuellen Anmeldeinformationen mit reiner NTLM-Serverauthentifizierung zulassen**
    * Klicken Sie auf **aktivieren** und fügen *Wsman/Fqdn-von-hyper-V-Host*.
1. Open **Hyper-V-Manager**.
1. Klicken Sie im linken Bereich mit der Maustaste **Hyper-V-Manager**.
1. Klicken Sie auf **eine Verbindung mit Server herstellen**.

>[!NOTE]
> Dies funktioniert nur für Windows Server 2016 oder Windows 10 **remote** Hosts.

Cmdlet-Details, finden Sie unter [Set-Item](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.management/set-item) und [Enable-WSManCredSSP](https://technet.microsoft.com/library/hh849872.aspx).

## <a name="install-hyper-v-manager"></a>Installieren von Hyper-V-Manager

Um ein UI-Tool verwenden, wählen Sie das entsprechende für das Betriebssystem auf dem Computer, auf dem Hyper-V-Manager ausgeführt werden:

Öffnen Sie in Windows Server, Server-Manager \> **verwalten** \> **Rollen und Features hinzufügen**. Verschieben Sie in der **Features** Seite, und erweitern Sie **Remoteserver-Verwaltungstools** \> **Rollenverwaltungstools** \>  **Hyper-V-Verwaltungstools**. 

Auf Windows, Hyper-V-Manager steht auf [alle Windows-Betriebssystem, das Hyper-V umfasst](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_compatibility).

1. Klicken Sie auf dem Windows-Desktop, klicken Sie auf die Schaltfläche "Start", und beginnen mit der Eingabe **Programme und Funktionen**. 
1. Klicken Sie in den Suchergebnissen auf **Programme und Funktionen**.
1. Klicken Sie im linken Bereich auf **Aktivieren von Windows-Funktionen ein- oder ausschalten**.
1. Erweitern Sie den Hyper-V-Ordner und **klicken Sie auf Hyper-V-Verwaltungstools**.
1. Klicken Sie zum Installieren von Hyper-V-Manager **Hyper-V-Verwaltungstools**. Wenn Sie auch Hyper-V-Modul installieren möchten, klicken Sie auf diese Option.

Um Windows PowerShell zu verwenden, führen Sie den folgenden Befehl als Administrator aus:

```
add-windowsfeature rsat-hyper-v-tools
```

## <a name="see-also"></a>Siehe auch  
 
[Installieren von Hyper-V](..\get-started\Install-the-Hyper-V-role-on-Windows-Server.md) 

