---
title: Erstellen eines virtuellen Computers in Hyper-V
description: Enthält Anweisungen zum Erstellen eines virtuellen Computers mit dem Hyper-V-Manager oder Windows PowerShell.
manager: dongill
ms.topic: get-started-article
ms.assetid: 59297022-a898-456c-b299-d79cd5860238
author: kbdazure
ms.author: kathydav
ms.date: 10/04/2016
ms.openlocfilehash: 5f4e07919503f283add8da1c8dd522f3d2b7f222
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87942016"
---
# <a name="create-a-virtual-machine-in-hyper-v"></a>Erstellen eines virtuellen Computers in Hyper-V

>Gilt für: Windows 10, Windows Server 2016, Microsoft Hyper-V Server 2016, Windows Server 2019, Microsoft Hyper-V Server 2019

Erfahren Sie, wie Sie einen virtuellen Computer mit dem Hyper-v-Manager und Windows PowerShell erstellen und welche Optionen beim Erstellen eines virtuellen Computers im Hyper-v-Manager vorhanden sind.

## <a name="create-a-virtual-machine-by-using-hyper-v-manager"></a>Erstellen eines virtuellen Computers mit dem Hyper-V-Manager

1.  Öffnen Sie den **Hyper-V-Manager**.

2.  Klicken Sie im Bereich **Aktion** auf **neu**, und klicken Sie dann auf **virtueller Computer**.

3.  Klicken Sie im **Assistenten für neue virtuelle Computer**auf **weiter**.

4.  Treffen Sie auf jeder Seite die geeigneten Optionen für den virtuellen Computer. Weitere Informationen finden Sie weiter unten in diesem Thema unter [Optionen für neue virtuelle Maschinen und Standardeinstellungen im Hyper-V-Manager](#options-in-hyper-v-manager-new-virtual-machine-wizard) .

5.  Nachdem Sie Ihre Auswahl auf der Seite **Zusammenfassung** überprüft haben, klicken Sie auf **Fertig**stellen.

6.  Klicken Sie im Hyper-V-Manager mit der rechten Maustaste auf den virtuellen Computer, und wählen Sie **verbinden**aus.

7.  Wählen Sie im Fenster Verbindung mit dem virtuellen Computer die Option **Aktion**  >  **starten**aus.

## <a name="create-a-virtual-machine-by-using-windows-powershell"></a>Erstellen eines virtuellen Computers mithilfe von Windows PowerShell

1. Klicken Sie auf dem Windows-Desktop auf die Schaltfläche „Start“, und geben Sie einen beliebigen Teil des Namens **Windows PowerShell** ein.

2. Klicken Sie mit der rechten Maustaste auf **Windows PowerShell**, und wählen Sie **Als Administrator ausführen** aus.

3. Holen Sie sich den Namen des virtuellen Switches, den der virtuelle Computer verwenden soll, mithilfe von [Get-VMSwitch](https://technet.microsoft.com/library/hh848499.aspx).  Ein auf ein Objekt angewendeter

   ```
   Get-VMSwitch  * | Format-Table Name
   ```

4. Verwenden Sie das Cmdlet [New-VM](https://technet.microsoft.com/library/hh848537.aspx) , um den virtuellen Computer zu erstellen.  Weitere Informationen finden Sie in den folgenden Beispielen.

   > [!NOTE]
   > Wenn Sie diese virtuelle Maschine auf einen Hyper-V-Host mit Windows Server 2012 R2 verschieben können, verwenden Sie den Parameter-Version mit [New-VM](https://technet.microsoft.com/library/hh848537.aspx) , um die Konfigurations Version der virtuellen Maschine auf 5 festzulegen. Die standardmäßige VM-Konfigurations Version für Windows Server 2016 wird von Windows Server 2012 R2 oder früheren Versionen nicht unterstützt. Nachdem der virtuelle Computer erstellt wurde, können Sie die Konfigurations Version des virtuellen Computers nicht mehr ändern. Weitere Informationen finden Sie [unter Unterstützte Konfigurations Versionen für virtuelle Computer](../deploy/Upgrade-virtual-machine-version-in-Hyper-V-on-Windows-or-Windows-Server.md#supported-virtual-machine-configuration-versions).

   - **Vorhandene virtuelle Festplatte** : um einen virtuellen Computer mit einer vorhandenen virtuellen Festplatte zu erstellen, können Sie den folgenden Befehl verwenden:
     - **-Name** ist der Name, den Sie für den erstellten virtuellen Computer angeben.
     - **-MemoryStartupBytes** ist die Menge an Arbeitsspeicher, die für den virtuellen Computer beim Starten verfügbar ist.
     - **-BootDevice** ist das Gerät, mit dem der virtuelle Computer gestartet wird, wenn er mit dem Netzwerkadapter (Network Adapter) oder der virtuellen Festplatte (VHD) gestartet wird.
     - **-VHDPath** ist der Pfad zum VM-Datenträger, der verwendet werden soll.
     - **-Path** ist der Pfad, unter dem die VM-Konfigurationsdateien gespeichert werden sollen.
     - **-Generation** ist die VM-Generation. Verwenden Sie Generation 1 für VHD und Generation 2 für VHDX. Weitere Informationen finden Sie [unter sollte ich einen virtuellen Computer der Generation 1 oder 2 in Hyper-V erstellen?.](../plan/Should-I-create-a-generation-1-or-2-virtual-machine-in-Hyper-V.md)
     - **-Switch** ist der Name des virtuellen Switches, über den der virtuelle Computer eine Verbindung mit anderen virtuellen Computern oder dem Netzwerk herstellen soll. Weitere Informationen finden Sie unter [Erstellen eines virtuellen Switches für virtuelle Hyper-V-](Create-a-virtual-switch-for-Hyper-V-virtual-machines.md)Computer.

       ```
       New-VM -Name <Name> -MemoryStartupBytes <Memory> -BootDevice <BootDevice> -VHDPath <VHDPath> -Path <Path> -Generation <Generation> -Switch <SwitchName>
       ```

       Zum Beispiel:

       ```
       New-VM -Name Win10VM -MemoryStartupBytes 4GB -BootDevice VHD -VHDPath .\VMs\Win10.vhdx -Path .\VMData -Generation 2 -Switch ExternalSwitch
       ```

       Dadurch wird ein virtueller Computer der Generation 2 mit dem Namen Win10VM und 4 GB Arbeitsspeicher erstellt. Er startet aus dem Ordner „VMs\Win10.vhdx“ im aktuellen Verzeichnis und verwendet den virtuellen Switch „ExternalSwitch“. Die VM-Konfigurationsdateien werden im Ordner „VMData“ gespeichert.

   - **Neue virtuelle Festplatte** : um einen virtuellen Computer mit einer neuen virtuellen Festplatte zu erstellen, ersetzen Sie den Parameter " **-vhdpath** " aus dem obigen Beispiel durch " **-newvhdpath** ", und fügen Sie den Parameter " **-newvhdsizebytes** " hinzu. Ein auf ein Objekt angewendeter

     ```
     New-VM -Name Win10VM -MemoryStartupBytes 4GB -BootDevice VHD -NewVHDPath .\VMs\Win10.vhdx -Path .\VMData -NewVHDSizeBytes 20GB -Generation 2 -Switch ExternalSwitch
     ```

   - **Neue virtuelle Festplatte, die mit dem Betriebssystem Abbild** gestartet wird: um einen virtuellen Computer mit einem neuen virtuellen Datenträger zu erstellen, der zu einem Betriebssystem Abbild gestartet wird, finden Sie weitere Informationen im PowerShell-Beispiel unter Exemplarische Vorgehensweise: Erstellen eines virtuellen Computers unter [Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_create_vm).

5. Starten Sie den virtuellen Computer mithilfe des Cmdlets [Start-VM](https://technet.microsoft.com/library/hh848589.aspx) . Führen Sie das folgende Cmdlet aus, wobei Name der Name des virtuellen Computers ist, den Sie erstellt haben.

   ```
   Start-VM -Name <Name>
   ```

   Zum Beispiel:

   ```
   Start-VM -Name Win10VM
   ```

6. Stellen Sie mithilfe der Verbindung mit virtuellen Computern (VMConnect) eine Verbindung mit dem virtuellen Computer her.

   ```
   VMConnect.exe
   ```

## <a name="options-in-hyper-v-manager-new-virtual-machine-wizard"></a>Optionen im Assistenten für neue virtuelle Computer im Hyper-V-Manager
In der folgenden Tabelle sind die Optionen aufgeführt, die Sie auswählen können, wenn Sie einen virtuellen Computer im Hyper-V-Manager erstellen, und die Standardeinstellungen.

|Seite|Standard für Windows Server 2016 und Windows 10|Weitere Optionen|
|--------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------|
|**Name und Pfad angeben**|Name: neuer virtueller Computer.<p>Speicherort: **c:\ProgramData\Microsoft\Windows\Hyper-v \\ **.|Sie können auch einen eigenen Namen eingeben und einen anderen Speicherort für den virtuellen Computer auswählen.<p>Hier werden die Konfigurationsdateien für den virtuellen Computer gespeichert.|
|**Generation angeben**|Generation 1|Sie können auch einen virtuellen Computer der Generation 2 erstellen. Weitere Informationen finden Sie unter [sollte ich einen virtuellen Computer der Generation 1 oder 2 in Hyper-V erstellen?.](../plan/Should-I-create-a-generation-1-or-2-virtual-machine-in-Hyper-V.md)|
|**Speicher zuweisen**|Start Speicher: 1024 MB<p>Dynamischer Arbeitsspeicher: **nicht ausgewählt**|Sie können den Start Speicher von 32 MB auf 5902mb festlegen.<p>Sie können auch dynamischer Arbeitsspeicher verwenden. Weitere Informationen finden Sie unter [Übersicht über Hyper-V-dynamischer Arbeitsspeicher](https://technet.microsoft.com/library/hh831766.aspx).|
|**Netzwerk konfigurieren**|Not connected|Sie können eine Netzwerkverbindung für die virtuelle Maschine aus einer Liste vorhandener virtueller Switches auswählen. Weitere Informationen finden Sie unter [Erstellen eines virtuellen Switches für virtuelle Hyper-V-](Create-a-virtual-switch-for-Hyper-V-virtual-machines.md)Computer.|
|**Virtuelle Festplatte verbinden**|Erstellen einer virtuellen Festplatte<p>Name: <*VMName*>. vhdx<p>**Speicherort**: **c:\Users\Public\Documents\Hyper-v\virtuelle fest \\ Platten**<p>**Größe**: 127 GB|Sie können auch eine vorhandene virtuelle Festplatte verwenden oder warten und eine virtuelle Festplatte später anfügen.|
|**Installationsoptionen**|Betriebssystem später installieren|Mit diesen Optionen wird die Start Reihenfolge des virtuellen Computers geändert, sodass Sie die Installation über eine ISO-Datei, eine startbare Diskette oder einen netzwerkinstallationsdienst wie die Windows-Bereitstellungs Dienste (WDS) Durchführung können.|
|**Zusammenfassung**|Zeigt die Optionen an, die Sie ausgewählt haben, damit Sie sicherstellen können, dass Sie korrekt sind.<p>- Name<br />-Generierung<br />- Arbeitsspeicher<br />-Netzwerk<br />-Festplatte<br />-Betriebs System|**Tipp:** Sie können die Zusammenfassung von der Seite kopieren und in e-Mail oder an einer anderen Stelle einfügen, um die Nachverfolgung der virtuellen Computer zu unterstützen.|

## <a name="additional-references"></a>Weitere Verweise

- [New-VM](https://technet.microsoft.com/library/hh848537.aspx)

- [Unterstützte Konfigurations Versionen für virtuelle Computer](../deploy/Upgrade-virtual-machine-version-in-Hyper-V-on-Windows-or-Windows-Server.md#supported-virtual-machine-configuration-versions)

-   [Soll ich in Hyper-V einen virtuellen Computer der 1. oder der 2. Generation erstellen?](../plan/Should-I-create-a-generation-1-or-2-virtual-machine-in-Hyper-V.md)

-   [Erstellen eines virtuellen Switches für Hyper-V-VMs](Create-a-virtual-switch-for-Hyper-V-virtual-machines.md)
