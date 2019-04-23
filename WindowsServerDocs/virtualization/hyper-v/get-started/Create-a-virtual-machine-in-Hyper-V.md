---
title: Erstellen eines virtuellen Computers in Hyper-V
description: Bietet eine Anleitung zum Erstellen eines virtuellen Computers mit Hyper-V-Manager oder Windows PowerShell
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 59297022-a898-456c-b299-d79cd5860238
author: KBDAzure
ms.author: kathydav
ms.date: 10/04/2016
ms.openlocfilehash: 8bc0aba906066f1c2fdc4d906ebbc78b08e871f0
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59852141"
---
# <a name="create-a-virtual-machine-in-hyper-v"></a>Erstellen eines virtuellen Computers in Hyper-V

>Gilt für: Windows 10, WindowsServer 2016, Microsoft Hyper-V Server 2016, WindowsServer 2019, Microsoft Hyper-V-Server 2019

Erfahren Sie, wie Sie einen virtuellen Computer zu erstellen, mit dem Hyper-V-Manager und Windows PowerShell und welche Optionen haben, wenn Sie einen virtuellen Computer in Hyper-V-Manager erstellen.  

## <a name="BKMK_HyperVManager"></a>Erstellen eines virtuellen Computers mit Hyper-V-Manager  

1.  Open **Hyper-V-Manager**.  

2.  Von der **Aktion** Bereich, klicken Sie auf **neu**, und klicken Sie dann auf **VM**.  

3.  Von der **Assistenten für neue virtuelle Maschine**, klicken Sie auf **Weiter**.  

4.  Stellen Sie der entsprechenden Optionen für den virtuellen Computer, auf den einzelnen Seiten. Weitere Informationen finden Sie unter [neuer virtueller Computer – Optionen und Standardwerte in Hyper-V-Manager](#BKMK_Options) weiter unten in diesem Thema.  

5.  Nach dem Überprüfen Ihrer Auswahl in der **Zusammenfassung** auf **Fertig stellen**.  

6.  Klicken Sie im Hyper-V-Manager mit der rechten Maustaste den virtuellen Computer, und wählen **verbinden**.  

7.  Wählen Sie die Verbindung mit virtuellen Computern im **Aktion** > **starten**.  

## <a name="BKMK_PowerShell"></a>Erstellen eines virtuellen Computers mithilfe von Windows PowerShell  

1.  Klicken Sie auf dem Windows-Desktop auf die Schaltfläche „Start“, und geben Sie einen beliebigen Teil des Namens **Windows PowerShell** ein.  

2.  Mit der rechten Maustaste **Windows PowerShell** , und wählen Sie **als Administrator ausführen**.  

3.  Rufen Sie den Namen des virtuellen Switches an, die Sie den virtuellen Computer mit möchten [Get-VMSwitch](https://technet.microsoft.com/library/hh848499.aspx).  Beispiel:  

    ```  
    Get-VMSwitch  * | Format-Table Name  
    ```  

4.  Verwenden der [New-VM](https://technet.microsoft.com/library/hh848537.aspx) -Cmdlet zum Erstellen des virtuellen Computers.  Weitere Informationen finden Sie in den folgenden Beispielen.  

    > [!NOTE]  
    > Wenn Sie diese virtuelle Maschine auf einem Hyper-V-Host, die Windows Server 2012 R2 ausgeführt wird verschieben können, verwenden Sie den - Version-Parameter mit [New-VM](https://technet.microsoft.com/library/hh848537.aspx) für die VM-Konfigurationsversion auf 5 festzulegen. Die Standardversion für die Konfiguration von virtuellen Computer für Windows Server 2016 wird von Windows Server 2012 R2 oder früheren Versionen nicht unterstützt. Sie können die Konfigurationsversion des virtuellen Computers nicht ändern, nachdem der virtuelle Computer erstellt wurde. Weitere Informationen finden Sie unter [unterstützte Versionen von VM-Konfiguration](../deploy/Upgrade-virtual-machine-version-in-Hyper-V-on-Windows-or-Windows-Server.md#BKMK_SupportedConfigVersions).  

    - **Vorhandene virtuelle Festplatte** – zum Erstellen eines virtuellen Computers mit einer vorhandenen virtuellen Festplatte können Sie den folgenden Befehl aus,  
        -   **--Name** ist der Name, den Sie für den virtuellen Computer bereitstellen, die Sie erstellen.  
        -   **-MemoryStartupBytes** ist die Menge an Arbeitsspeicher, die mit dem virtuellen Computer beim Start verfügbar ist.  
        -   **-%BootDevice** ist das Gerät, das mit dem virtuellen Computer gestartet, beim Start wie Netzwerkadapter (Netzwerkadapter) oder virtuelle Festplatte (VHD wird).  
        -   **-%Vhdpath** ist der Pfad auf dem Datenträger des virtuellen Computers, die Sie verwenden möchten.  
        -   **-Path** ist der Pfad zum Speichern von Konfigurationsdateien des virtuellen Computers.  
        -   **-Generation** Generation des virtuellen Computers ist. Verwenden Sie für die virtuelle Festplatte und der Generation 2 für VHDX Generation 1. Finden Sie unter [sollten virtuelle Maschine der Generation 1 oder 2 in Hyper-V erstellen?](../plan/Should-I-create-a-generation-1-or-2-virtual-machine-in-Hyper-V.md)  
        -   **-Wechseln Sie** ist der Name des virtuellen Switches an, die Sie den virtuellen Computer zu verwenden, um mit anderen virtuellen Computern oder dem Netzwerk verbinden möchten. Finden Sie unter [erstellen Sie einen virtuellen Switch für Hyper-V-Maschinen](Create-a-virtual-switch-for-Hyper-V-virtual-machines.md).  

        ```  
        New-VM -Name <Name> -MemoryStartupBytes <Memory> -BootDevice <BootDevice> -VHDPath <VHDPath> -Path <Path> -Generation <Generation> -Switch <SwitchName>  
        ```  

        Zum Beispiel:  

        ```  
        New-VM -Name Win10VM -MemoryStartupBytes 4GB -BootDevice VHD -VHDPath .\VMs\Win10.vhdx -Path .\VMData -Generation 2 -Switch ExternalSwitch  
        ```  

        Dadurch wird einen virtueller Computer der Generation 2 mit dem Namen Win10VM mit 4GB RAM erstellt. Es gestartet wird, aus dem Ordner VMs\Win10.vhdx im aktuellen Verzeichnis und den virtuellen Switch mit dem Namen ExternalSwitch verwendet. Die Konfigurationsdateien der virtuellen Computer werden im Ordner "VMData" gespeichert.  

    -   **Neue virtuelle Festplatte** : Informationen zum Erstellen eines virtuellen Computers mit einer neuen virtuellen Festplatte, ersetzen Sie die **- %vhdpath** Parameter aus dem Beispiel oben mit **- NewVHDPath** und Hinzufügen der **- NewVHDSizeBytes** Parameter. Beispiel:  

        ```  
        New-VM -Name Win10VM -MemoryStartupBytes 4GB -BootDevice VHD -NewVHDPath .\VMs\Win10.vhdx -Path .\VMData -NewVHDSizeBytes 20GB -Generation 2 -Switch ExternalSwitch  
        ```  

    -   **Neue virtuelle Festplatte, die mit dem Betriebssystemabbild, das gestartet wird** – zum Erstellen eines virtuellen Computers mit einer neuen virtuellen Festplatte, die startet, um ein Betriebssystemabbild, finden Sie im PowerShell-Beispiel in [VM Exemplarische Vorgehensweise für Hyper-V auf erstellen. Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_create_vm).  

5.  Starten Sie den virtuellen Computer mithilfe der [Start-VM](https://technet.microsoft.com/library/hh848589.aspx) Cmdlet. Führen Sie das folgende Cmdlet aus, wobei der Name der Name des erstellten virtuellen Computers ist.  

    ```  
    Start-VM -Name <Name>  
    ```  

    Zum Beispiel:  

    ```  
    Start-VM -Name Win10VM  
    ```  

6.  Verbinden Sie mit dem virtuellen Computer mithilfe der Verbindung mit virtuellen Computern (VMConnect).  

    ```  
    VMConnect.exe  
    ```  

## <a name="BKMK_Options"></a>Optionen im Assistenten für neue Hyper-V-Manager-VM  
Die folgende Tabelle enthält die Optionen, die Sie beim Erstellen von eines virtuellen Computers in Hyper-V-Manager und die Standardwerte für die einzelnen auswählen können.  

|Page|Standardeinstellung für WindowsServer 2016 und Windows 10|Weitere Optionen|  
|--------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------|  
|**Name und Pfad angeben**|Name:  Neue virtuelle Maschine.<br /><br />Speicherort:  **C:\ProgramData\Microsoft\Windows\Hyper-V\\**.|Sie können außerdem Geben Sie einen eigenen Namen und wählen Sie einen anderen Speicherort für den virtuellen Computer.<br /><br />Dies ist das, wo die Konfigurationsdateien der virtuellen Maschine gespeichert werden sollen.|  
|**Generation angeben**|Erste Generation|Sie können auch auswählen, um einen virtuellen Computer der Generation 2 zu erstellen. Weitere Informationen finden Sie unter [sollten virtuelle Maschine der Generation 1 oder 2 in Hyper-V erstellen?](../plan/Should-I-create-a-generation-1-or-2-virtual-machine-in-Hyper-V.md)|  
|**Speicher zuweisen**|Arbeitsspeicher beim Start: 1024 MB<br /><br />Dynamischer Arbeitsspeicher: **nicht ausgewählt**|Sie können den startspeicher zwischen 32 MB und 5902 MB festlegen.<br /><br />Sie können auch auswählen, um die Verwendung von dynamischem Arbeitsspeicher. Weitere Informationen finden Sie unter [Hyper-V dynamischer Arbeitsspeicher – Übersicht](https://technet.microsoft.com/library/hh831766.aspx).|  
|**Netzwerk konfigurieren**|Nicht verbunden|Sie können eine Netzwerkverbindung für den virtuellen Computer aus einer Liste von vorhandenen virtuellen Switches verwenden auswählen. Finden Sie unter [erstellen Sie einen virtuellen Switch für Hyper-V-Maschinen](Create-a-virtual-switch-for-Hyper-V-virtual-machines.md).|  
|**Virtuelle Festplatte verbinden**|Erstellen einer virtuellen Festplatte<br /><br />Name: <*Vmname*> vhdx<br /><br />**Speicherort**: **C:\Users\Public\Documents\Hyper-V\Virtual Festplatten\\**<br /><br />**Größe**: 127GB|Sie können auch auswählen, um eine vorhandene virtuelle Festplatte verwenden, oder warten Sie, und eine virtuelle Festplatte später zuordnen.|  
|**Installationsoptionen**|Installieren Sie später ein Betriebssystem installiert ist|Diese Optionen ändern die Startreihenfolge des virtuellen Computers, damit Sie von einer ISO-Datei, die Startdiskette oder ein Dienst zur Installation, wie der Windows-Verwaltungsinstrumentation (Windows Deployment Services, WDS) installieren können.|  
|**Zusammenfassung**|Die Optionen, die Sie ausgewählt haben, zeigt an, damit Sie überprüfen können, dass diese richtig sind.<br /><br />-Name<br />-Generierung<br />-Arbeitsspeicher<br />-Netzwerk<br />-Festplatte<br />-Betriebssystem|**Tipp:** Sie können die Zusammenfassung auf der Seite kopieren und fügen Sie ihn in der E-mail oder an anderer Stelle Ihnen das Nachverfolgen Ihrer virtuellen Computer helfen.|  

## <a name="see-also"></a>Siehe auch  

- [New-VM](https://technet.microsoft.com/library/hh848537.aspx)  

- [Versionen von unterstützten VM-Konfiguration](../deploy/Upgrade-virtual-machine-version-in-Hyper-V-on-Windows-or-Windows-Server.md#BKMK_SupportedConfigVersions)  

-   [Sollte ich virtuelle Computer der Generation 1 oder 2 in Hyper-V erstellen?](../plan/Should-I-create-a-generation-1-or-2-virtual-machine-in-Hyper-V.md)  

-   [Erstellen Sie einen virtuellen Switch für Hyper-V-Computer](Create-a-virtual-switch-for-Hyper-V-virtual-machines.md)  
