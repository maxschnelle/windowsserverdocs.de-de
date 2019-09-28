---
title: Remote Verwaltung von Hyper-V-Hosts
description: Beschreibt die Versions Kompatibilität zwischen Hyper-v-Hosts und Hyper-v-Manager sowie das Herstellen einer Verbindung mit Remote Hosts in verschiedenen Umgebungen, einschließlich Domänen übergreifender und eigenständiger Umgebungen.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2d34e98c-6134-479b-8000-3eb360b8b8a3
author: KBDAzure
ms.author: kathydav
ms.date: 12/06/2016
ms.openlocfilehash: 677e054fe42978697ef786b73daac75069f0408f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71392689"
---
# <a name="remotely-manage-hyper-v-hosts-with-hyper-v-manager"></a>Remote Verwaltung von Hyper-v-Hosts mit dem Hyper-v-Manager

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows 10, Windows 8.1

In diesem Artikel werden die unterstützten Kombinationen von Hyper-v-Hosts und Hyper-v-Manager-Versionen aufgelistet, und es wird beschrieben, wie Sie eine Verbindung mit Remote-und lokalen Hyper-v-Hosts herstellen, um 

Mit dem Hyper-v-Manager können Sie eine kleine Anzahl von Hyper-v-Hosts sowohl Remote als auch lokal verwalten. Die Installation wird bei der Installation der Hyper-v-Verwaltungs Tools installiert, die Sie entweder über eine vollständige Hyper-v-Installation oder eine reine Tools-Installation durchführen können. Wenn Sie eine nur-Tools-Installation durchführen, können Sie die Tools auf Computern verwenden, die die Hardwareanforderungen zum Hosten von Hyper-V nicht erfüllen. Weitere Informationen zu Hardware für Hyper-V-Hosts finden Sie unter [System Anforderungen](../System-requirements-for-Hyper-V-on-Windows.md).

Wenn Hyper-V-Manager nicht installiert ist, lesen Sie die [Anweisungen](#install-hyper-v-manager) unten.

## <a name="supported-combinations-of-hyper-v-manager-and-hyper-v-host-versions"></a>Unterstützte Kombinationen aus Hyper-v-Manager und Hyper-v-Host Versionen

In einigen Fällen können Sie eine andere Version von Hyper-v-Manager verwenden als die Hyper-v-Version auf dem Host, wie in der Tabelle dargestellt. Wenn Sie dies tun, stellt der Hyper-v-Manager die verfügbaren Funktionen für die Hyper-v-Version auf dem Host bereit, den Sie verwalten. Wenn Sie z. b. die Version von Hyper-v-Manager in Windows Server 2012 R2 verwenden, um einen Host, auf dem Hyper-v unter Windows Server 2012 ausgeführt wird, Remote zu verwalten, können Sie in Windows Server 2012 R2 auf diesem Hyper-v-Host verfügbare Funktionen nicht verwenden.

In der folgenden Tabelle ist aufgeführt, welche Versionen eines Hyper-v-Hosts von einer bestimmten Version von Hyper-v-Manager verwaltet werden können. Es werden nur unterstützte Betriebssystemversionen aufgelistet. Ausführliche Informationen zum Support Status einer bestimmten Betriebssystemversion finden Sie auf der Seite [Microsoft Lifecycle Policy](https://support.microsoft.com/lifecycle) auf der Schaltfläche **Product Lebenszyklus suchen** . Im Allgemeinen können ältere Versionen von Hyper-v-Manager nur einen Hyper-v-Host verwalten, auf dem dieselbe Version oder die vergleichbare Version von Windows Server ausgeführt wird.

|Hyper-V-Manager-Version | Hyper-V-Host Version|
|---|---|
|Windows 2016, Windows 10|-Windows Server 2016 – alle Editionen und Installationsoptionen, einschließlich nano Server, und die entsprechende Version von Hyper-V Server <br>-Windows Server 2012 R2 – alle Editionen und Installationsoptionen sowie die entsprechende Version von Hyper-V Server <br>-Windows Server 2012 – alle Editionen und Installationsoptionen und die entsprechende Version von Hyper-V Server <br> -Windows 10 <br> -Windows 8.1  |
| Windows Server 2012 R2, Windows 8.1 | -Windows Server 2012 R2 – alle Editionen und Installationsoptionen sowie die entsprechende Version von Hyper-V Server <br>-Windows Server 2012 – alle Editionen und Installationsoptionen und die entsprechende Version von Hyper-V Server <br>-Windows 8.1
| Windows Server 2012 | -Windows Server 2012 – alle Editionen und Installationsoptionen und die entsprechende Version von Hyper-V Server
| Windows Server 2008 R2 Service Pack 1, Windows 7 Service Pack 1 | -Windows Server 2008 R2 – alle Editionen und Installationsoptionen sowie die entsprechende Version von Hyper-V Server
| Windows Server 2008, Windows Vista Service Pack 2 | -Windows Server 2008 – alle Editionen und Installationsoptionen und die entsprechende Version von Hyper-V Server

>[!NOTE]
>Die Service Pack-Unterstützung wurde für Windows 8 am 12. Januar 2016 beendet. Weitere Informationen finden Sie in den [Windows 8.1 FAQ](https://support.microsoft.com/help/18581).

## <a name="connect-to-a-hyper-v-host"></a>Herstellen einer Verbindung mit einem Hyper-V-Host

Zum Herstellen einer Verbindung mit einem Hyper-v-Host über den Hyper-v-Manager klicken Sie im linken Bereich mit der rechten Maustaste auf **Hyper-v-Manager** , und klicken Sie dann auf **Verbindung mit Server herstellen**.

## <a name="manage-hyper-v-on-a-local-computer"></a>Verwalten von Hyper-V auf einem lokalen Computer

Mit dem Hyper-v-Manager werden keine Computer aufgelistet, auf denen Hyper-v gehostet wird, bis Sie den Computer einschließlich eines lokalen Computers hinzufügen. Gehen Sie dazu wie folgt vor:

1. Klicken Sie im linken Bereich mit der rechten Maustaste auf **Hyper-V-Manager**.
2. Klicken Sie auf **Verbindung mit Server herstellen**.
3. Klicken Sie unter **Computer auswählen**auf **lokaler Computer** , und klicken Sie dann auf **OK**.

Wenn keine Verbindung hergestellt werden kann:

* Es ist möglich, dass nur die Hyper-V-Tools installiert werden. Suchen Sie nach dem Verwaltungsdienst für virtuelle Computer, um zu überprüfen, ob die Hyper-V-Plattform installiert ist. /(Öffnen Sie die Desktop-App für Dienste: Klicken Sie auf **Start**, klicken Sie **auf Start,** geben Sie **Services. msc**ein, und drücken Sie dann die **Eingabe**Taste. Wenn der Verwaltungsdienst für virtuelle Computer nicht aufgeführt ist, installieren Sie die Hyper-v-Plattform, indem Sie die Anweisungen unter [Installieren von Hyper-v](../get-started/Install-the-Hyper-V-role-on-Windows-Server.md)befolgen.
* Überprüfen Sie, ob Ihre Hardware die Anforderungen erfüllt. Siehe [System Anforderungen](../System-requirements-for-Hyper-V-on-Windows.md).
* Überprüfen Sie, ob Ihr Benutzerkonto der Gruppe "Administratoren" oder der Gruppe "Hyper-V-Administratoren" angehört.

## <a name="manage-hyper-v-hosts-remotely"></a>Remote Verwaltung von Hyper-V-Hosts  

Zum Verwalten von Hyper-V-Remote Hosts aktivieren Sie die Remote Verwaltung auf dem lokalen Computer und Remote Host.

Öffnen Sie unter Windows Server Server-Manager \>**lokaler Server** \>**Remote Verwaltung** , und klicken Sie dann auf **Remote Verbindungen mit diesem Computer zulassen**. 

Oder öffnen Sie Windows PowerShell von einem der beiden Betriebssysteme als Administrator, und führen Sie Folgendes aus: 

```
Enable-PSRemoting
```

### <a name="connect-to-hosts-in-the-same-domain"></a>Herstellen einer Verbindung mit Hosts in derselben Domäne

Bei Windows 8.1 und früheren Versionen funktioniert die Remote Verwaltung nur, wenn sich der Host in derselben Domäne befindet und das lokale Benutzerkonto auch auf dem Remote Host ausgeführt wird.

Wählen Sie zum Hinzufügen eines Hyper-v-Remote Hosts zu Hyper-v-Manager **einen anderen Computer** im Dialogfeld **Computer auswählen** aus, und geben Sie den Hostnamen des Remote Hosts, den NetBIOS-Namen oder den voll qualifizierten Domänen Namen \(fqdn @ no__t-3 ein.

Der Hyper-V-Manager in Windows Server 2016 und Windows 10 bietet mehr Typen von Remote Verbindungen als vorherige Versionen, die in den folgenden Abschnitten beschrieben werden.  

### <a name="connect-to-a-windows-2016-or-windows-10-remote-host-as-a-different-user"></a>Herstellen einer Verbindung mit einem Windows 2016-oder Windows 10-Remote Host als anderer Benutzer

Auf diese Weise können Sie eine Verbindung mit dem Hyper-v-Host herstellen, wenn Sie nicht auf dem lokalen Computer als Benutzer ausgeführt werden, der Mitglied der Gruppe "Hyper-v-Administratoren" oder der Gruppe "Administratoren" auf dem Hyper-v-Host ist. Gehen Sie dazu wie folgt vor:

1. Klicken Sie im linken Bereich mit der rechten Maustaste auf **Hyper-V-Manager**.
1. Klicken Sie auf **Verbindung mit Server herstellen**.
1. Wählen Sie im Dialogfeld **Computer auswählen** die Option **als anderer Benutzer verbinden** aus.
1. Wählen Sie **Benutzer festlegen**aus.

>[!NOTE]
> Dies funktioniert nur für Windows Server 2016-oder Windows 10- **Remote** Hosts.

### <a name="connect-to-a-windows-2016-or-windows-10-remote-host-using-ip-address"></a>Herstellen einer Verbindung mit einem Windows 2016-oder Windows 10-Remote Host über die IP-Adresse

Gehen Sie dazu wie folgt vor:

1. Klicken Sie im linken Bereich mit der rechten Maustaste auf **Hyper-V-Manager**.
1. Klicken Sie auf **Verbindung mit Server herstellen**.
1. Geben Sie die IP-Adresse in das Textfeld **anderer Computer ein** .

>[!NOTE]
> Dies funktioniert nur für Windows Server 2016-oder Windows 10- **Remote** Hosts.

### <a name="connect-to-a-windows-2016-or-windows-10-remote-host-outside-your-domain-or-with-no-domain"></a>Herstellen einer Verbindung mit einem Windows 2016-oder Windows 10-Remote Host außerhalb Ihrer Domäne oder ohne Domäne

Gehen Sie dazu wie folgt vor:

1. Öffnen Sie auf dem zu verwaltenden Hyper-V-Host eine Windows PowerShell-Sitzung als Administrator.

1. Erstellen Sie die erforderlichen Firewallregeln für private Netzwerk Zonen:   
   
   ```
   Enable-PSRemoting
   ```

2. Um den Remote Zugriff auf Öffentliche Zonen zuzulassen, aktivieren Sie Firewallregeln für "kredssp" und "WinRM":
  
   ```
   Enable-WSManCredSSP -Role server
   ```

    Weitere Informationen finden Sie unter [enable-psremoting](https://technet.microsoft.com/library/hh849694.aspx) und [enable-wsmankredssp](https://technet.microsoft.com/library/hh849872.aspx).

Konfigurieren Sie als nächstes den Computer, den Sie zum Verwalten des Hyper-V-Hosts verwenden.

1. Öffnen Sie eine Windows PowerShell-Sitzung als Administrator.
1. Führen Sie die folgenden Befehle aus:

     ```
     Set-Item WSMan:\localhost\Client\TrustedHosts -Value "fqdn-of-hyper-v-host"
     ```
     ```
     Enable-WSManCredSSP -Role client -DelegateComputer "fqdn-of-hyper-v-host"
     ```
1. Möglicherweise müssen Sie auch die folgende Gruppenrichtlinie konfigurieren: 
    * **Computer Konfiguration** \> **Administrative Vorlagen** \> **System** \> **Delegierung von Anmelde** Informationen \> **zulassen, dass neue Anmelde Informationen mit nur NTLM-Server Authentifizierung delegiert** werden
    * Klicken Sie auf **aktivieren** , und fügen Sie *WSMAN/sqdn-of-Hyper-v-Host*hinzu.
1. Öffnen Sie den **Hyper-V-Manager**.
1. Klicken Sie im linken Bereich mit der rechten Maustaste auf **Hyper-V-Manager**.
1. Klicken Sie auf **Verbindung mit Server herstellen**.

>[!NOTE]
> Dies funktioniert nur für Windows Server 2016-oder Windows 10- **Remote** Hosts.

Informationen zu Cmdlets finden Sie unter [Set-Item](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.management/set-item) und [enable-wsmankredssp](https://technet.microsoft.com/library/hh849872.aspx).

## <a name="install-hyper-v-manager"></a>Installieren von Hyper-V-Manager

Wenn Sie ein UI-Tool verwenden möchten, wählen Sie das geeignete für das Betriebssystem auf dem Computer aus, auf dem Sie Hyper-V-Manager ausführen möchten:

Öffnen Sie unter Windows Server Server-Manager \> **Verwalten** \> **Rollen und Features hinzufügen**. Wechseln Sie zur Seite " **Features** ", und erweitern Sie **Remote Server-Verwaltungs Tools** \> **Rollen Verwaltungs Tools** \> **Hyper-V-Verwaltungs Tools**. 

Unter Windows ist Hyper-v-Manager auf [jedem Windows-Betriebssystem verfügbar, das Hyper-v umfasst](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_compatibility).

1. Klicken Sie auf dem Windows-Desktop auf die Schaltfläche Start, und geben Sie **Programme und Funktionen**ein. 
1. Klicken Sie in den Suchergebnissen auf **Programme und Funktionen**.
1. Klicken Sie im linken **Bereich auf Windows-Funktionen ein-oder ausschalten**.
1. Erweitern Sie den Hyper-v-Ordner, und **Klicken Sie auf Hyper-v-Verwaltungs Tools**.
1. Klicken Sie zum Installieren von Hyper-v-Manager auf **Hyper-v-Verwaltungs Tools**. Wenn Sie auch das Hyper-V-Modul installieren möchten, klicken Sie auf diese Option.

Um Windows PowerShell zu verwenden, führen Sie den folgenden Befehl als Administrator aus:

```
add-windowsfeature rsat-hyper-v-tools
```

## <a name="see-also"></a>Siehe auch  
 
[Installieren von Hyper-V](../get-started/Install-the-Hyper-V-role-on-Windows-Server.md) 

