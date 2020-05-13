---
title: Verwalten von Hyper-V-Integration Services
description: Beschreibt, wie Integrationsdienste ein-und ausgeschaltet werden und bei Bedarf installiert werden.
ms.technology: compute-hyper-v
author: kbdazure
ms.author: kathydav
manager: dongill
ms.date: 12/20/2016
ms.topic: article
ms.prod: windows-server
ms.assetid: 9cafd6cb-dbbe-4b91-b26c-dee1c18fd8c2
ms.openlocfilehash: 4237da8ee393953a8eb2a2b577c2df201f96a7be
ms.sourcegitcommit: aed942d11f1a361fc1d17553a4cf190a864d1268
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/12/2020
ms.locfileid: "83235064"
---
# <a name="manage-hyper-v-integration-services"></a>Verwalten von Hyper-V-Integration Services

> Gilt für: Windows 10, Windows Server 2012, Windows Server 2012r2, Windows Server 2016, Windows Server 2019

Mithilfe der bidirektionalen Kommunikation mit dem Hyper-v-Host können Sie Hyper-V Integration Services die Leistung virtueller Computer verbessern und bequeme Features bereitstellen. Viele dieser Dienste sind Bequemlichkeiten, wie z. b. das Kopieren von Gast Dateien, während andere für die Funktionalität des virtuellen Computers, z. b. synthetische Gerätetreiber, wichtig sind. Diese Dienste und Treiber werden manchmal als "Integrations Komponenten" bezeichnet. Sie können steuern, ob einzelne bequeme Dienste für einen bestimmten virtuellen Computer ausgeführt werden. Die Treiber Komponenten sind nicht für die manuelle Wartung vorgesehen.

Ausführliche Informationen zu den einzelnen Integrationsdiensten finden Sie unter [Hyper-V-Integration Services](https://docs.microsoft.com/virtualization/hyper-v-on-windows/reference/integration-services).

> [!IMPORTANT]
> Jeder Dienst, den Sie verwenden möchten, muss sowohl auf dem Host als auch auf dem Gast aktiviert sein, damit er funktioniert. Alle Integrationsdienste mit Ausnahme von "Hyper-V-Gastschnittstellendienst" sind unter Windows-Gastbetriebssystemen standardmäßig aktiviert. Die Dienste können einzeln aktiviert und deaktiviert werden. In den nächsten Abschnitten wird erläutert, wie Sie.

## <a name="turn-an-integration-service-on-or-off-using-hyper-v-manager"></a>Aktivieren oder Deaktivieren eines Integrations Dienstanbieter mit dem Hyper-V-Manager

1. Klicken Sie im mittleren Bereich mit der rechten Maustaste auf den virtuellen Computer, und klicken Sie dann auf **Einstellungen**.

2. Klicken Sie im linken Bereich des Fensters **Einstellungen** unter **Verwaltung**auf **Integration Services**.

Im Integration Services Bereich werden alle Integrationsdienste aufgelistet, die auf dem Hyper-V-Host verfügbar sind, und ob der Host die virtuelle Maschine für die Verwendung aktiviert hat.

### <a name="turn-an-integration-service-on-or-off-using-powershell"></a>Aktivieren oder Deaktivieren eines Integrations Dienstanbieter mithilfe von PowerShell

Verwenden Sie hierzu " [enable-vmintegrationservice](https://technet.microsoft.com/library/hh848500.aspx) " und "Enable [-vmintegrationservice](https://technet.microsoft.com/library/hh848488.aspx)", um dies in PowerShell zu tun.

In den folgenden Beispielen wird veranschaulicht, wie Sie den Integrations Dienst für Gast Dateien kopieren für einen virtuellen Computer namens "demovm" aktivieren und deaktivieren.

1. Hier erhalten Sie eine Liste der laufenden Integrationsdienste:

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

1. Gast Dienst Schnittstelle aktivieren:

   ``` PowerShell
   Enable-VMIntegrationService -VMName "DemoVM" -Name "Guest Service Interface"
   ```

1. Überprüfen Sie, ob die Gast Dienst Schnittstelle aktiviert ist:

   ```
   Get-VMIntegrationService -VMName "DemoVM"
   ```

1. Gast Dienst Schnittstelle ausschalten:

    ```
    Disable-VMIntegrationService -VMName "DemoVM" -Name "Guest Service Interface"
    ```

## <a name="checking-the-guests-integration-services-version"></a>Überprüfen der Integration Services-Version des Gasts
Einige Features funktionieren möglicherweise nicht ordnungsgemäß oder überhaupt nicht, wenn die Integrationsdienste des Gasts nicht aktuell sind. Um die Versionsinformationen für ein Fenster zu erhalten, melden Sie sich beim Gast Betriebssystem an, öffnen Sie eine Eingabeaufforderung, und führen Sie den folgenden Befehl aus:

```
REG QUERY "HKLM\Software\Microsoft\Virtual Machine\Auto" /v IntegrationServicesVersion
```

Ältere Gast Betriebssysteme haben nicht alle verfügbaren Dienste. Beispielsweise können Windows Server 2008 R2-Gäste nicht über das "Hyper-V-Gastschnittstellendienst" verfügen.

## <a name="start-and-stop-an-integration-service-from-a-windows-guest"></a>Starten und Beenden eines Integrations Diensts von einem Windows-Gast
Damit ein Integrations Dienst voll funktionsfähig ist, muss der zugehörige Dienst innerhalb des Gast Betriebssystems zusätzlich zur Aktivierung auf dem Host ausgeführt werden. In Windows-Gastbetriebssystemen wird jeder Integrations Dienst als standardmäßiger Windows-Dienst aufgeführt. Sie können das Applet "Dienste" in der Systemsteuerung oder PowerShell verwenden, um diese Dienste zu starten und zu starten.

> [!IMPORTANT]
> Das Beenden eines Integrations Diensts kann die Fähigkeit des Hosts, den virtuellen Computer zu verwalten, stark beeinträchtigen. Um ordnungsgemäß zu funktionieren, muss jeder Integrations Dienst, den Sie verwenden möchten, sowohl auf dem Host als auch auf dem Gast aktiviert sein.
> Als bewährte Vorgehensweise sollten Sie die Integrationsdienste von Hyper-V nur mithilfe der oben aufgeführten Anweisungen steuern. Der übereinstimmende Dienst im Gast Betriebssystem wird automatisch beendet oder gestartet, wenn Sie seinen Status in Hyper-V ändern.
> Wenn Sie einen Dienst im Gast Betriebssystem starten, aber in Hyper-V deaktiviert ist, wird der Dienst angehalten. Wenn Sie einen Dienst im Gast Betriebssystem, der in Hyper-v aktiviert ist, beendet haben, startet Hyper-v ihn schließlich erneut. Wenn Sie den Dienst im Gast deaktivieren, kann er von Hyper-V nicht gestartet werden.

### <a name="use-windows-services-to-start-or-stop-an-integration-service-within-a-windows-guest"></a>Verwenden von Windows-Diensten zum Starten oder Beenden eines Integrations Diensts innerhalb eines Windows-Gast Diensts

1. Öffnen Sie den Dienst-Manager, indem Sie ```services.msc``` als Administrator ausführen oder indem Sie in der Systemsteuerung auf das Symbol "Dienste" doppelklicken.

    ![Screenshot mit dem Bereich "Windows-Dienste"](media/HVServices.png)

1. Suchen Sie die Dienste, die mit "Hyper-V" beginnen.

1. Klicken Sie mit der rechten Maustaste auf den Dienst, der gestartet oder beendet werden soll Klicken Sie auf die gewünschte Aktion.

### <a name="use-windows-powershell-to-start-or-stop-an-integration-service-within-a-windows-guest"></a>Verwenden von Windows PowerShell zum Starten oder Beenden eines Integrations Diensts innerhalb eines Windows-Gast Betriebssystems

1. Führen Sie Folgendes aus, um eine Liste der Integrationsdienste zu erhalten:

    ```
    Get-Service -Name vm*
    ```

1.  Die Ausgabe sollte etwa so aussehen:

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

1. Ausführen von " [Start-Service](https://technet.microsoft.com/library/hh849825.aspx) " oder "Start [-Service](https://technet.microsoft.com/library/hh849790.aspx)". Um beispielsweise Windows PowerShell Direct zu deaktivieren, führen Sie Folgendes aus:

    ```
    Stop-Service -Name vmicvmsession
    ```

## <a name="start-and-stop-an-integration-service-from-a-linux-guest"></a>Starten und Beenden eines Integrations Diensts von einem Linux-Gast

Linux-Integrationsdienste werden in der Regel über den Linux-Kernel bereitgestellt. Der Treiber für Linux-Integrationsdienste hat den Namen **hv_utils**.

1. Um herauszufinden, ob **hv_utils** geladen ist, verwenden Sie den folgenden Befehl:

   ``` BASH
   lsmod | grep hv_utils
   ```

2. Die Ausgabe sollte etwa so aussehen:

    ``` BASH
    Module                  Size   Used by
    hv_utils               20480   0
    hv_vmbus               61440   8 hv_balloon,hyperv_keyboard,hv_netvsc,hid_hyperv,hv_utils,hyperv_fb,hv_storvsc
    ```

3. Wenn Sie herausfinden möchten, ob die erforderlichen Daemons ausgeführt werden, verwenden Sie diesen Befehl.

    ``` BASH
    ps -ef | grep hv
    ```

4. Die Ausgabe sollte etwa so aussehen:

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

5. Führen Sie Folgendes aus, um festzustellen, welche Daemons verfügbar sind:

    ``` BASH
    compgen -c hv_
    ```

6. Die Ausgabe sollte etwa so aussehen:

    ``` BASH
    hv_vss_daemon
    hv_get_dhcp_info
    hv_get_dns_info
    hv_set_ifconfig
    hv_kvp_daemon
    hv_fcopy_daemon
    ```

   Zu den unter Umständen aufgelisteten Integrations Dienst-Daemons zählen die folgenden. Wenn fehlende vorhanden sind, werden Sie möglicherweise auf Ihrem System nicht unterstützt, oder Sie sind möglicherweise nicht installiert. Weitere Informationen finden Sie [unter Unterstützte virtuelle Linux-und FreeBSD-Computer für Hyper-V unter Windows](https://technet.microsoft.com/library/dn531030.aspx).
   - **hv_vss_daemon**: Dieser Daemon ist zum Erstellen von Sicherungen virtueller Linux-Computer erforderlich.
   - **hv_kvp_daemon**: Dieser Daemon ermöglicht das Festlegen und Abfragen von systeminternen und extrinsischen Schlüssel-Wert-Paaren.
   - **hv_fcopy_daemon**: Dieser Daemon implementiert einen Datei Kopier Dienst zwischen Host und Gast.

### <a name="examples"></a>Beispiele

Diese Beispiele veranschaulichen das Beenden und Starten des KVP-Daemons mit dem Namen `hv_kvp_daemon` .

1. Verwenden Sie die Prozess-ID \( \) -PID, um den Prozess des Daemons zu verhindern. Um die PID zu finden, sehen Sie sich die zweite Spalte der Ausgabe an, oder verwenden Sie `pidof` . Hyper-V-Daemons werden als root-Vorgänge ausgeführt, sodass Sie Root-Berechtigungen benötigen.

    ``` BASH
    sudo kill -15 `pidof hv_kvp_daemon`
    ```

1. Führen Sie folgende Schritte aus, um zu überprüfen, ob der gesamte `hv_kvp_daemon` Prozess

    ```
    ps -ef | hv
    ```

1. Um den Daemon erneut zu starten, führen Sie den Daemon als root-Vorgang aus:

    ``` BASH
    sudo hv_kvp_daemon
    ```

1. Führen Sie Folgendes aus, um zu überprüfen, ob der `hv_kvp_daemon` Prozess mit einer neuen Prozess-ID aufgelistet ist:

    ```
    ps -ef | hv
    ```

## <a name="keep-integration-services-up-to-date"></a>Integration Services auf dem neuesten standhalten

Es wird empfohlen, Integration Services auf dem neuesten Stand zu halten, um die bestmögliche Leistung und die neuesten Features für Ihre virtuellen Computer zu erhalten. Dies ist für die meisten Windows-Gäste standardmäßig der Fall, wenn Sie so eingerichtet sind, dass wichtige Updates von Windows Update erhalten werden. Linux-Gäste, die aktuelle Kernel verwenden, erhalten beim Aktualisieren des Kernels die neuesten Integrations Komponenten.

**Für virtuelle Maschinen, die auf Windows 10-/Windows Server 2016/2019-Hosts ausgeführt werden:**

> [!NOTE]
> Die Image Datei "vmguest. ISO" ist nicht in Hyper-V unter Windows 10/Windows Server 2016/2019 enthalten, da Sie nicht mehr benötigt wird.

| Gast  | Updatemechanismus | Notizen |
|:---------|:---------|:---------|
| Windows 10 | Windows Update | |
| Windows 8.1 | Windows Update | |
| Windows 8 | Windows Update | Benötigt den Integrationsdienst „Datenaustausch“.* |
| Windows 7 | Windows Update | Benötigt den Integrationsdienst „Datenaustausch“.* |
| Windows Vista (SP 2) | Windows Update | Benötigt den Integrationsdienst „Datenaustausch“.* |
| - | | |
| Windows Server 2016 | Windows Update | |
| Windows Server (halbjährlicher Kanal) | Windows Update | |
| Windows Server 2012 R2 | Windows Update | |
| Windows Server 2012 | Windows Update | Benötigt den Integrationsdienst „Datenaustausch“.* |
| Windows Server 2008 R2 (SP 1) | Windows Update | Benötigt den Integrationsdienst „Datenaustausch“.* |
| Windows Server 2008 (SP 2) | Windows Update | Erweiterte Unterstützung nur in Windows Server 2016 ([Weitere Informationen](https://support.microsoft.com/lifecycle?p1=12925)). |
| Windows Home Server 2011 | Windows Update | Wird in Windows Server 2016 ([Weitere Informationen](https://support.microsoft.com/lifecycle?p1=15820)) nicht unterstützt. |
| Windows Small Business Server 2011 | Windows Update | Nicht im grundlegenden Support enthalten ([Weitere Informationen](https://support.microsoft.com/lifecycle?p1=15817)). |
| - | | |
| Linux-Gastbetriebssysteme | Paket-Manager | Integration Services für Linux sind in die Distribution integriert, es können jedoch optionale Updates verfügbar sein. ******** |

\*Wenn der Datenaustausch-Integrations Dienst nicht aktiviert werden kann, stehen die Integrationsdienste für diese Gäste im [Download Center](https://support.microsoft.com/kb/3071740) als CAB-Datei (CAB-Datei) zur Verfügung. Anweisungen zum Anwenden eines CAB finden Sie in diesem [Blogbeitrag](https://techcommunity.microsoft.com/t5/virtualization/integration-components-available-for-virtual-machines-not/ba-p/382247).

**Für virtuelle Maschinen, die auf Windows 8.1/Windows Server 2012r2-Hosts ausgeführt werden:**

| Gast  | Updatemechanismus | Notizen |
|:---------|:---------|:---------|
| Windows 10 | Windows Update | |
| Windows 8.1 | Integrationsdienste-Datenträger | Weitere [Informationen](#install-or-update-integration-services)finden Sie unten unter. |
| Windows 8 | Integrationsdienste-Datenträger | Weitere [Informationen](#install-or-update-integration-services)finden Sie unten unter. |
| Windows 7 | Integrationsdienste-Datenträger | Weitere [Informationen](#install-or-update-integration-services)finden Sie unten unter. |
| Windows Vista (SP 2) | Integrationsdienste-Datenträger | Weitere [Informationen](#install-or-update-integration-services)finden Sie unten unter. |
| Windows XP (SP 2, SP 3) | Integrationsdienste-Datenträger | Weitere [Informationen](#install-or-update-integration-services)finden Sie unten unter. |
| - | | |
| Windows Server 2016 | Windows Update | |
| Windows Server (halbjährlicher Kanal) | Windows Update | |
| Windows Server 2012 R2 | Integrationsdienste-Datenträger | Weitere [Informationen](#install-or-update-integration-services)finden Sie unten unter. |
| Windows Server 2012 | Integrationsdienste-Datenträger | Weitere [Informationen](#install-or-update-integration-services)finden Sie unten unter. |
| Windows Server 2008 R2 | Integrationsdienste-Datenträger | Weitere [Informationen](#install-or-update-integration-services)finden Sie unten unter. |
| Windows Server 2008 (SP 2) | Integrationsdienste-Datenträger | Weitere [Informationen](#install-or-update-integration-services)finden Sie unten unter. |
| Windows Home Server 2011 | Integrationsdienste-Datenträger | Weitere [Informationen](#install-or-update-integration-services)finden Sie unten unter. |
| Windows Small Business Server 2011 | Integrationsdienste-Datenträger | Weitere [Informationen](#install-or-update-integration-services)finden Sie unten unter. |
| Windows Server 2003 R2 (SP 2) | Integrationsdienste-Datenträger | Weitere [Informationen](#install-or-update-integration-services)finden Sie unten unter. |
| Windows Server 2003 (SP 2) | Integrationsdienste-Datenträger | Weitere [Informationen](#install-or-update-integration-services)finden Sie unten unter. |
| - | | |
| Linux-Gastbetriebssysteme | Paket-Manager | Integration Services für Linux sind in die Distribution integriert, es können jedoch optionale Updates verfügbar sein. ** |


**Für virtuelle Computer, die auf Windows 8/Windows Server 2012-Hosts ausgeführt werden:**

| Gast  | Updatemechanismus | Notizen |
|:---------|:---------|:---------|
| Windows 8.1 | Integrationsdienste-Datenträger | Weitere [Informationen](#install-or-update-integration-services)finden Sie unten unter. |
| Windows 8 | Integrationsdienste-Datenträger | Weitere [Informationen](#install-or-update-integration-services)finden Sie unten unter. |
| Windows 7 | Integrationsdienste-Datenträger | Weitere [Informationen](#install-or-update-integration-services)finden Sie unten unter. |
| Windows Vista (SP 2) | Integrationsdienste-Datenträger | Weitere [Informationen](#install-or-update-integration-services)finden Sie unten unter. |
| Windows XP (SP 2, SP 3) | Integrationsdienste-Datenträger | Weitere [Informationen](#install-or-update-integration-services)finden Sie unten unter. |
| - | | |
| Windows Server 2012 R2 | Integrationsdienste-Datenträger | Weitere [Informationen](#install-or-update-integration-services)finden Sie unten unter. |
| Windows Server 2012 | Integrationsdienste-Datenträger | Weitere [Informationen](#install-or-update-integration-services)finden Sie unten unter. |
| Windows Server 2008 R2 | Integrationsdienste-Datenträger | Weitere [Informationen](#install-or-update-integration-services)finden Sie unten unter.|
| Windows Server 2008 (SP 2) | Integrationsdienste-Datenträger | Weitere [Informationen](#install-or-update-integration-services)finden Sie unten unter. |
| Windows Home Server 2011 | Integrationsdienste-Datenträger | Weitere [Informationen](#install-or-update-integration-services)finden Sie unten unter. |
| Windows Small Business Server 2011 | Integrationsdienste-Datenträger | Weitere [Informationen](#install-or-update-integration-services)finden Sie unten unter. |
| Windows Server 2003 R2 (SP 2) | Integrationsdienste-Datenträger | Weitere [Informationen](#install-or-update-integration-services)finden Sie unten unter. |
| Windows Server 2003 (SP 2) | Integrationsdienste-Datenträger | Weitere [Informationen](#install-or-update-integration-services)finden Sie unten unter. |
| - | | |
| Linux-Gastbetriebssysteme | Paket-Manager | Integration Services für Linux sind in die Distribution integriert, es können jedoch optionale Updates verfügbar sein. ** |

Weitere Informationen zu Linux-Gastbetriebssystemen finden Sie [unter Unterstützte virtuelle Linux-und FreeBSD-Computer für Hyper-V unter Windows](https://technet.microsoft.com/windows-server-docs/virtualization/hyper-v/supported-linux-and-freebsd-virtual-machines-for-hyper-v-on-windows).

## <a name="install-or-update-integration-services"></a>Installieren oder Aktualisieren von Integrationsdiensten

> [!NOTE]
> Bei Hosts, die älter als Windows Server 2016 und Windows 10 sind, müssen Sie die Integrationsdienste in den Gastbetriebssystemen **manuell installieren oder aktualisieren** .

Verfahren zum manuellen Installieren oder Aktualisieren der Integrationsdienste:

1.  Öffnen Sie den Hyper-V-Manager. Klicken Sie im Menü Extras von Server-Manager auf **Hyper-V-Manager**.

2.  Stellen Sie eine Verbindung mit dem virtuellen Computer her. Klicken Sie mit der rechten Maustaste auf den virtuellen Computer und dann auf **verbinden**.

3.  Klicken Sie im Menü %%amp;quot;Aktion%%amp;quot; von %%amp;quot;Verbindung mit virtuellen Computern%%amp;quot; auf **Installationsdatenträger für Integrationsdienste einlegen**. Dadurch wird der Installationsdatenträger im virtuellen DVD-Laufwerk geladen. Abhängig vom Gast Betriebssystem müssen Sie die Installation möglicherweise manuell starten.

4.  Nach Abschluss der Installation sind alle Integrationsdienste verfügbar.

> [!NOTE]
> Diese Schritte **können nicht automatisiert** oder innerhalb einer Windows PowerShell-Sitzung für virtuelle **Online** Computer ausgeführt werden.
> Sie können Sie auf vhdx- **Offline** Images anwenden. Weitere Informationen finden [Sie unter Installieren von Integration Services, wenn der virtuelle Computer nicht ausgeführt wird](https://docs.microsoft.com/virtualization/community/team-blog/2013/20130418-how-to-install-integration-services-when-the-virtual-machine-is-not-running).
> Sie können die Bereitstellung der Integrationsdienste auch über **Configuration Manager** mit den VMS **Online**automatisieren, aber Sie müssen die VMs am Ende der Installation neu starten. Weitere Informationen finden [Sie unter Bereitstellen von Hyper-V-Integration Services auf VMS mithilfe von config Manager](https://docs.microsoft.com/archive/blogs/manageabilityguys/deploying-hyper-v-integration-services-to-vms-using-config-manager-and-dism)
