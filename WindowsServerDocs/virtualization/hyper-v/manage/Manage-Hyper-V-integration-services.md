---
title: Verwalten von Hyper-V-Integrationsdiensten
description: Beschreibt das Aktivieren bzw. Deaktivieren von Integrationsdiensten und installieren Sie sie bei Bedarf
ms.technology: compute-hyper-v
author: KBDAzure
ms.author: kathydav
manager: dongill
ms.date: 12/20/2016
ms.topic: article
ms.prod: windows-server-threshold
ms.service: na
ms.assetid: 9cafd6cb-dbbe-4b91-b26c-dee1c18fd8c2
ms.openlocfilehash: b049efc61d5060791574f20fcdd8b369a26f0507
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59890251"
---
>Gilt für: Windows 10, WindowsServer 2016, WindowsServer 2019

# <a name="manage-hyper-v-integration-services"></a>Verwalten von Hyper-V-Integrationsdiensten

Hyper-V-Integrationsdienste Verbessern der Leistung der virtuellen Computer, und geben praktischer Features zur Verfügung, durch die Nutzung der bidirektionalen Kommunikation mit dem Hyper-V-Host. Viele dieser Dienste sind Vorteile, z. B. Kopieren von gastdateien, während andere Funktionen des virtuellen Computers wie synthetische Treiber am wichtigsten sind. Diese Gruppe von Diensten und Treiber werden manchmal als "Integrationskomponenten" bezeichnet. Sie können steuern, ob der Einfachheit halber einzelne Dienste für einen bestimmten virtuellen Computer ausgeführt werden. Die Treiberkomponenten sollen nicht manuell bearbeitet werden.

Weitere Informationen zu einzelnen Integrationsdienst, finden Sie unter [Hyper-V-Integrationsdienste](https://docs.microsoft.com/virtualization/hyper-v-on-windows/reference/integration-services).

>[!IMPORTANT]
>Jeder Dienst, die Sie verwenden möchten, muss in den Host- und Gastbetriebssysteme aktiviert sein, um zu funktionieren. Alle Integrationsdienste mit Ausnahme von "Hyper-V-Gastdienstschnittstelle" sind standardmäßig auf Windows-Gastbetriebssysteme. Die Dienste aktiviert werden können, ein- und ausschalten einzeln. Die nächsten Abschnitte zeigen Ihnen, wie.

## <a name="turn-an-integration-service-on-or-off-using-hyper-v-manager"></a>Aktivieren Sie oder deaktivieren Sie mit dem Hyper-V-Manager von eines Integration-Diensts

1. Klicken Sie im mittleren Bereich, mit der rechten Maustaste den virtuellen Computer, und klicken Sie auf **Einstellungen**.
  
2. Im linken Bereich, der die **Einstellungen** Fenster unter **Management**, klicken Sie auf **Integrationsdienste**.
  
Die Integration Services-Bereich listet alle Integrationsdienste verfügbar sind, auf dem Hyper-V-Host und gibt an, ob der Host für den virtuellen Computer, deren Verwendung aktiviert hat.

### <a name="turn-an-integration-service-on-or-off-using-powershell"></a>Aktivieren Sie einen Integration-Dienst aus, oder deaktivieren Sie mithilfe von PowerShell

Verwenden Sie hierzu in PowerShell [Enable-VMIntegrationService](https://technet.microsoft.com/library/hh848500.aspx) und [Disable-VMIntegrationService](https://technet.microsoft.com/library/hh848488.aspx).

Die folgenden Beispiele veranschaulichen das Aktivieren des Gast-Datei kopieren Integrationsdienst ein- und ausschalten für eine virtuelle Maschine mit dem Namen "Demovm".

1. Abrufen einer Liste von Integrationsdiensten ausführen:
  
    ``` PowerShell
    Get-VMIntegrationService -VMName "DemoVM"
    ```
1. Die Ausgabe sollte wie folgt aussehen:

    ``` PowerShell
   VMName      Name                    Enabled PrimaryStatusDescription SecondaryStatusDescription
   ------      ----                    ------- ------------------------ --------------------------
   DemoVM      Guest Service Interface False   OK
   DemoVM      Heartbeat               True    OK                       OK
   DemoVM      Key-Value Pair Exchange True    OK
   DemoVM      Shutdown                True    OK
   DemoVM      Time Synchronization    True    OK
   DemoVM      VSS                     True    OK
   ```

1. Aktivieren Sie Guest Service Interface:

   ``` PowerShell
   Enable-VMIntegrationService -VMName "DemoVM" -Name "Guest Service Interface"
   ```

1. Stellen Sie sicher, dass Guest Service Interface aktiviert ist:

   ```
   Get-VMIntegrationService -VMName "DemoVM" 
   ``` 

1. Deaktivieren Sie Guest Service Interface:

    ```
    Disable-VMIntegrationService -VMName "DemoVM" -Name "Guest Service Interface"
    ```
   
## <a name="checking-the-guests-integration-services-version"></a>Überprüfen das Gastbetriebssystem Integrationsdienste-version
Einige Features funktionieren nicht ordnungsgemäß oder überhaupt, wenn das Gastbetriebssystem Integrationsdienste nicht aktuell sind. Rufen Sie die Versionsinformationen für eine Windows, melden Sie sich bei dem Gastbetriebssystem, öffnen Sie eine Eingabeaufforderung, und führen Sie diesen Befehl:

```
REG QUERY "HKLM\Software\Microsoft\Virtual Machine\Auto" /v IntegrationServicesVersion
```
Frühere Gastbetriebssysteme müssen nicht alle verfügbaren Dienste. Sind keine Windows Server 2008 R2-Gäste z. B. die "Hyper-V-Gastdienstschnittstelle".

## <a name="start-and-stop-an-integration-service-from-a-windows-guest"></a>Starten Sie und beenden Sie einen Integration-Dienst von einem Windows-Gast
In der Reihenfolge für einen Integrationsdienst voll funktionsfähig ist muss der entsprechende Dienst auf dem Gast zusätzlich zur Aktivierung auf dem Host ausgeführt werden. In Windows-Gäste ist jede Integration-Dienst als standard Windows-Dienst aufgeführt. Sie können das Applet "Dienste" in der Systemsteuerung oder PowerShell verwenden, beenden und starten Sie diese Dienste.

>[!IMPORTANT]
> Beenden des Diensts Integration kann die Fähigkeit des Hosts zum Verwalten Ihres virtuellen Computers gravierend. Ordnungsgemäß funktioniert, muss jeder Integrationsdienst, die Sie verwenden möchten, auf dem Host und Gast aktiviert sein.
> Als bewährte Methode sollten Sie nur Integrationsdiensten vom Hyper-V mithilfe der oben genannten Anweisungen steuern. Der entsprechende Dienst im Gastbetriebssystem, das wird beenden oder automatisch gestartet, wenn Sie seinen Status in Hyper-V geändert.
> Wenn Sie einen Dienst in das Gastbetriebssystem starten, aber er die in Hyper-V deaktiviert ist, wird der Dienst beendet. Wenn Sie einen Dienst in der Gast-Betriebssystems, die in Hyper-V aktiviert ist beenden, wird Hyper-V schließlich erneut gestartet. Wenn Sie den Dienst auf dem Gast zu deaktivieren, werden Hyper-V kann nicht gestartet werden.

### <a name="use-windows-services-to-start-or-stop-an-integration-service-within-a-windows-guest"></a>Verwenden von Windows-Dienste starten oder Beenden einen Integrationsdienst auf einem Windows-Gast

1. Öffnen Sie Dienste-Manager mit ```services.msc``` als Administrator oder durch Doppelklicken auf das Symbol "Dienste" in der Systemsteuerung.

    ![Screenshot, der im Windows-Dienste angezeigt wird](media/HVServices.png) 

1. Suchen Sie die Dienste, die mit "Hyper-V" beginnen. 

1. Mit der rechten Maustaste in der Sie des Diensts starten oder beenden. Klicken Sie auf die gewünschte Aktion.


### <a name="use-windows-powershell-to-start-or-stop-an-integration-service-within-a-windows-guest"></a>Mithilfe von Windows PowerShell starten oder Beenden einen Integrationsdienst auf einem Windows-Gast

1. Um eine Liste von Integrationsservices zu erhalten, führen Sie Folgendes aus:

    ```
    Get-Service -Name vm*
    ```
1.  Die Ausgabe sollte etwa wie folgt aussehen:

    ```PowerShell
    Status   Name               DisplayName
    ------   ----               -----------
    Running  vmicguestinterface Hyper-V Guest Service Interface
    Running  vmicheartbeat      Hyper-V Heartbeat Service
    Running  vmickvpexchange    Hyper-V Data Exchange Service
    Running  vmicrdv            Hyper-V Remote Desktop Virtualizati...
    Running  vmicshutdown       Hyper-V Guest Shutdown Service
    Running  vmictimesync       Hyper-V Time Synchronization Service
    Stopped  vmicvmsession      Hyper-V VM Session Service
    Running  vmicvss            Hyper-V Volume Shadow Copy Requestor
    ```

1. Führen Sie einen [Start-Service-](https://technet.microsoft.com/library/hh849825.aspx) oder [Stop-Service-](https://technet.microsoft.com/library/hh849790.aspx). Z. B. um die Windows PowerShell Direct zu deaktivieren, führen Sie aus:

    ```
    Stop-Service -Name vmicvmsession
    ```

## <a name="start-and-stop-an-integration-service-from-a-linux-guest"></a>Starten und Beenden eines Integration-Diensts mit einer Linux-Gastbetriebssysteme 

Linux-Integrationsdienste werden in der Regel über den Linux-Kernel bereitgestellt. Der Linux Integration Services-Treiber ist mit dem Namen **Hv_utils**.

1.  Um zu ermitteln, ob **Hv_utils** geladen wurde, verwenden Sie diesen Befehl:

    ``` BASH
    lsmod | grep hv_utils
    ``` 
  
1. Die Ausgabe sollte etwa wie folgt aussehen:  
  
    ``` BASH
    Module                  Size   Used by
    hv_utils               20480   0
    hv_vmbus               61440   8 hv_balloon,hyperv_keyboard,hv_netvsc,hid_hyperv,hv_utils,hyperv_fb,hv_storvsc
    ```

1. Um herauszufinden, ob die erforderlichen Daemons ausgeführt werden, verwenden Sie diesen Befehl aus.
  
    ``` BASH
    ps -ef | grep hv
    ```
  
1. Die Ausgabe sollte etwa wie folgt aussehen: 
  
    ```BASH
    root       236     2  0 Jul11 ?        00:00:00 [hv_vmbus_con]
    root       237     2  0 Jul11 ?        00:00:00 [hv_vmbus_ctl]
    ...
    root       252     2  0 Jul11 ?        00:00:00 [hv_vmbus_ctl]
    root      1286     1  0 Jul11 ?        00:01:11 /usr/lib/linux-tools/3.13.0-32-generic/hv_kvp_daemon
    root      9333     1  0 Oct12 ?        00:00:00 /usr/lib/linux-tools/3.13.0-32-generic/hv_kvp_daemon
    root      9365     1  0 Oct12 ?        00:00:00 /usr/lib/linux-tools/3.13.0-32-generic/hv_vss_daemon
    scooley  43774 43755  0 21:20 pts/0    00:00:00 grep --color=auto hv          
    ```

1. Führen Sie Folgendes aus, um festzustellen, welche Daemons verfügbar sind:

    ``` BASH
    compgen -c hv_
    ```
  
1. Die Ausgabe sollte etwa wie folgt aussehen:
  
    ``` BASH
    hv_vss_daemon
    hv_get_dhcp_info
    hv_get_dns_info
    hv_set_ifconfig
    hv_kvp_daemon
    hv_fcopy_daemon     
    ```
  
 Daemons für Integrationsdienste, die aufgelistet werden können, gehören die folgenden. Fehlen, sie möglicherweise nicht auf Ihrem System unterstützt werden, oder sie können nicht installiert werden. Details finden, finden Sie unter [unterstützt Linux und FreeBSD-VMs für Hyper-V unter Windows](https://technet.microsoft.com/library/dn531030.aspx).  
  - **hv_vss_daemon**: Dieser Daemon ist erforderlich, um live Linux-VM-Sicherungen zu erstellen.
  - **hv_kvp_daemon**: Dieser Daemon ermöglicht das Festlegen und Abfragen interner und externer Schlüsselwertpaare Schlüssel-/Wertpaaren.
  - **hv_fcopy_daemon**: Dieser Daemon implementiert einen dateikopierdienst zwischen Host und Gast.  

### <a name="examples"></a>Beispiele

Diese Beispiele zeigen, beenden und starten den KVP-Daemon, mit dem Namen `hv_kvp_daemon`.

1. Verwenden Sie die Prozess-ID \(PID\) Daemon Prozess zu beenden. Um die PID zu suchen, sehen Sie sich die zweite Spalte der Ausgabe, oder verwenden Sie `pidof`. Hyper-V-Daemons als Root-Benutzer, ausgeführt, sodass Sie mit Root-Berechtigungen benötigen.

    ``` BASH
    sudo kill -15 `pidof hv_kvp_daemon`
    ```

1. Zum Überprüfen, ob alle `hv_kvp_daemon` Prozess nicht mehr vorhanden ist, werden ausgeführt:

    ```
    ps -ef | hv
    ```

1. Um den Daemon erneut zu starten, führen Sie den Daemon als Root-Benutzer:

    ``` BASH
    sudo hv_kvp_daemon
    ``` 

1. Zum Überprüfen, ob die `hv_kvp_daemon` Prozess wird mit einer neuen Prozess-ID, und führen Sie aufgeführt:

    ```
    ps -ef | hv
    ```

## <a name="keep-integration-services-up-to-date"></a>Halten Sie Integrationsdienste auf dem neuesten Stand

Es wird empfohlen, dass Sie Integrationsdienste auf dem neuesten Stand, erhalten die beste Leistung und die neuesten Funktionen für Ihre virtuellen Computer beibehalten. Dies geschieht für die meisten Windows-Gäste in der Standardeinstellung, wenn sie eingerichtet werden, um wichtige Updates von Windows Update erhalten werden. Linux-Gäste, die mit der aktuellen Kernel erhalten die neuesten Integrationskomponenten, bei der Aktualisierung des Kernels.

**Für auf Windows 10-Hosts ausgeführte virtuelle Computer:**

> [!NOTE]
> Die Imagedatei "vmguest.iso" ist in Hyper-V unter Windows 10 enthalten, da es nicht mehr benötigt wird.

| Gast  | Updatemechanismus | Hinweise |
|:---------|:---------|:---------|
| Windows 10 | Windows Update | |
| Windows 8.1 | Windows Update | |
| Windows 8 | Windows Update | Benötigt den Integrationsdienst „Datenaustausch“.* |
| Windows 7 | Windows Update | Benötigt den Integrationsdienst „Datenaustausch“.* |
| Windows Vista (SP 2) | Windows Update | Benötigt den Integrationsdienst „Datenaustausch“.* |
| - | | |
| Windows Server 2016 | Windows Update | |
| WindowsServer Halbjährlicher Kanal | Windows Update | |
| Windows Server 2012 R2 | Windows Update | |
| Windows Server 2012 | Windows Update | Benötigt den Integrationsdienst „Datenaustausch“.* |
| Windows Server 2008 R2 (SP 1) | Windows Update | Benötigt den Integrationsdienst „Datenaustausch“.* |
| Windows Server 2008 (SP 2) | Windows Update | Erweiterte Unterstützung nur in Windows Server 2016 ([erfahren Sie mehr](https://support.microsoft.com/lifecycle?p1=12925)). |
| Windows Home Server 2011 | Windows Update | Wird in Windows Server 2016 nicht mehr unterstützt ([erfahren Sie mehr](https://support.microsoft.com/lifecycle?p1=15820)). |
| Windows Small Business Server 2011 | Windows Update | Nicht im grundlegenden Support enthalten ([Weitere Informationen](https://support.microsoft.com/lifecycle?p1=15817)). |
| - | | |
| Linux-Gastbetriebssysteme | Paket-Manager | Für Linux-Integrationsdienste werden in die Distribution integriert, aber möglicherweise optionale Updates verfügbar. ******** |

\* Wenn der Integrationsdienst für den Datenaustausch kann nicht aktiviert werden, stehen die Integrationsdienste für diese Gastbetriebssysteme über die [Downloadcenter](https://support.microsoft.com/kb/3071740) als CAB-Datei (Cab)-Datei. Anweisungen zum Ausführen einer CAB-Datei finden Sie in diesem [Blogbeitrag](https://blogs.technet.com/b/virtualization/archive/2015/07/24/integration-components-available-for-virtual-machines-not-connected-to-windows-update.aspx).

**Für auf Windows 8.1-Hosts ausgeführte virtuelle Computer:**

| Gast  | Updatemechanismus | Hinweise |
|:---------|:---------|:---------|
| Windows 10 | Windows Update | |
| Windows 8.1 | Windows Update | |
| Windows 8 | Integrationsdienste-Datenträger | Finden Sie unter [Anweisungen](#install-or-update-integration-services)weiter unten. |
| Windows 7 | Integrationsdienste-Datenträger | Finden Sie unter [Anweisungen](#install-or-update-integration-services)weiter unten. |
| Windows Vista (SP 2) | Integrationsdienste-Datenträger | Finden Sie unter [Anweisungen](#install-or-update-integration-services)weiter unten. |
| Windows XP (SP 2, SP 3) | Integrationsdienste-Datenträger | Finden Sie unter [Anweisungen](#install-or-update-integration-services)weiter unten. |
| - | | |
| Windows Server 2016 | Windows Update | |
| WindowsServer Halbjährlicher Kanal | Windows Update | |
| Windows Server 2012 R2 | Windows Update | |
| Windows Server 2012 | Integrationsdienste-Datenträger | Finden Sie unter [Anweisungen](#install-or-update-integration-services)weiter unten. |
| Windows Server 2008 R2 | Integrationsdienste-Datenträger | Finden Sie unter [Anweisungen](#install-or-update-integration-services)weiter unten. |
| Windows Server 2008 (SP 2) | Integrationsdienste-Datenträger | Finden Sie unter [Anweisungen](#install-or-update-integration-services)weiter unten. |
| Windows Home Server 2011 | Integrationsdienste-Datenträger | Finden Sie unter [Anweisungen](#install-or-update-integration-services)weiter unten. |
| Windows Small Business Server 2011 | Integrationsdienste-Datenträger | Finden Sie unter [Anweisungen](#install-or-update-integration-services)weiter unten. |
| Windows Server 2003 R2 (SP 2) | Integrationsdienste-Datenträger | Finden Sie unter [Anweisungen](#install-or-update-integration-services)weiter unten. |
| Windows Server 2003 (SP 2) | Integrationsdienste-Datenträger | Finden Sie unter [Anweisungen](#install-or-update-integration-services)weiter unten. |
| - | | |
| Linux-Gastbetriebssysteme | Paket-Manager | Für Linux-Integrationsdienste werden in die Distribution integriert, aber möglicherweise optionale Updates verfügbar. ** |


**Für auf Windows 8-Hosts ausgeführte virtuelle Computer:**

| Gast  | Updatemechanismus | Hinweise |
|:---------|:---------|:---------|
| Windows 8.1 | Windows Update | |
| Windows 8 | Integrationsdienste-Datenträger | Finden Sie unter [Anweisungen](#install-or-update-integration-services)weiter unten. |
| Windows 7 | Integrationsdienste-Datenträger | Finden Sie unter [Anweisungen](#install-or-update-integration-services)weiter unten. |
| Windows Vista (SP 2) | Integrationsdienste-Datenträger | Finden Sie unter [Anweisungen](#install-or-update-integration-services)weiter unten. |
| Windows XP (SP 2, SP 3) | Integrationsdienste-Datenträger | Finden Sie unter [Anweisungen](#install-or-update-integration-services)weiter unten. |
| - | | |
| Windows Server 2012 R2 | Windows Update | |
| Windows Server 2012 | Integrationsdienste-Datenträger | Finden Sie unter [Anweisungen](#install-or-update-integration-services)weiter unten. |
| Windows Server 2008 R2 | Integrationsdienste-Datenträger | Finden Sie unter [Anweisungen](#install-or-update-integration-services)weiter unten.|
| Windows Server 2008 (SP 2) | Integrationsdienste-Datenträger | Finden Sie unter [Anweisungen](#install-or-update-integration-services)weiter unten. |
| Windows Home Server 2011 | Integrationsdienste-Datenträger | Finden Sie unter [Anweisungen](#install-or-update-integration-services)weiter unten. |
| Windows Small Business Server 2011 | Integrationsdienste-Datenträger | Finden Sie unter [Anweisungen](#install-or-update-integration-services)weiter unten. |
| Windows Server 2003 R2 (SP 2) | Integrationsdienste-Datenträger | Finden Sie unter [Anweisungen](#install-or-update-integration-services)weiter unten. |
| Windows Server 2003 (SP 2) | Integrationsdienste-Datenträger | Finden Sie unter [Anweisungen](#install-or-update-integration-services)weiter unten. |
| - | | |
| Linux-Gastbetriebssysteme | Paket-Manager | Für Linux-Integrationsdienste werden in die Distribution integriert, aber möglicherweise optionale Updates verfügbar. ** |

Weitere Informationen zu Linux-Gastbetriebssystemen finden Sie unter [unterstützt Linux und FreeBSD-VMs für Hyper-V unter Windows](https://technet.microsoft.com/windows-server-docs/virtualization/hyper-v/supported-linux-and-freebsd-virtual-machines-for-hyper-v-on-windows).

## <a name="install-or-update-integration-services"></a>Installieren oder Aktualisieren von Integrationsservices

Für Hosts müssen älter als Windows Server 2016 und Windows 10, Sie manuell installieren oder Aktualisieren von Integration Services in die Gastbetriebssysteme. 
  
1.  Öffnen Sie den Hyper-V-Manager. Klicken Sie in Server-Manager im Menü Extras auf **Hyper-V-Manager**.  
  
2.  Stellen Sie eine Verbindung mit dem virtuellen Computer her. Mit der rechten Maustaste den virtuellen Computer aus, und klicken Sie auf **Connect**.  
  
3.  Klicken Sie im Menü %%amp;quot;Aktion%%amp;quot; von %%amp;quot;Verbindung mit virtuellen Computern%%amp;quot; auf **Installationsdatenträger für Integrationsdienste einlegen**. Dadurch wird der Installationsdatenträger im virtuellen DVD-Laufwerk geladen. Je nach Gastbetriebssystem müssen Sie die Installation manuell zu starten.  
  
4.  Nach Abschluss der Installation sind alle Integrationsdienste verfügbar.

Diese Schritte nicht automatisiert oder innerhalb einer Windows PowerShell-Sitzung für online-VMs. Sie können diese VHDX-Offlineabbildern zuweisen; [finden Sie in diesem Blogbeitrag](https://blogs.technet.microsoft.com/virtualization/2013/04/18/how-to-install-integration-services-when-the-virtual-machine-is-not-running/).
