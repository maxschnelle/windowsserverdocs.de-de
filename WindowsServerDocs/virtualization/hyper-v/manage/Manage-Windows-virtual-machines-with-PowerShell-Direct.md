---
title: Verwalten von Windows-VMs mit PowerShell Direct
description: Enthält Anweisungen für die Verwendung von PowerShell Direct zum Verwalten der virtuellen Computer ohne Rückgriff auf ein Netzwerk oder eine Remoteverbindung mit ihnen.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b5715c02-a90f-4de9-a71e-0fc09093ba2d
author: KBDAzure
ms.author: kathydav
ms.date: 10/04/2016
ms.openlocfilehash: 4081a9737825d2f50f0d3b19b3bada3b9bbc76f1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59814701"
---
# <a name="manage-windows-virtual-machines-with-powershell-direct"></a>Verwalten von Windows-VMs mit PowerShell Direct

>Gilt für: Windows 10, WindowsServer 2016, WindowsServer 2019
  
Sie können PowerShell Direct verwenden, um ein Windows 10, Windows Server 2016 oder Windows Server-2019 virtuellen Computer von einem Windows 10, Windows Server 2016 oder Windows Server 2019 Hyper-V-Host Remote zu verwalten. PowerShell Direct ermöglicht die Verwaltung von Windows PowerShell innerhalb eines virtuellen Computers unabhängig von der Netzwerkkonfiguration oder remoteverwaltungseinstellungen auf dem Hyper-V-Host oder dem virtuellen Computer. Dies erleichtert Hyper-V-Administratoren die Automatisierung und Erstellung von Skripts zur Verwaltung und Konfiguration virtueller Computer.  
  
Es gibt zwei Möglichkeiten, PowerShell Direct auszuführen:  
  
- Erstellen und Beenden einer PowerShell Direct-Sitzungs mit PSSession-cmdlets
  
- Ausführen von Skripts oder Befehls mit dem Invoke-Command-cmdlet
  
Wenn Sie ältere virtuelle Computer verwalten, verwenden Sie die Verbindung mit virtuellen Computern (VMConnect) oder [Konfigurieren Sie ein virtuelles Netzwerk für den virtuellen Computer](https://technet.microsoft.com/library/cc816585.aspx).  
  
## <a name="create-and-exit-a-powershell-direct-session-using-pssession-cmdlets"></a>Erstellen und Beenden einer PowerShell Direct-Sitzungs mit PSSession-cmdlets  
  
1. Öffnen Sie Windows PowerShell auf dem Hyper-V-Host als Administrator.  
  
2. Verwenden der [Enter-PSSession](https://technet.microsoft.com/library/hh849707.aspx) Cmdlet, um eine Verbindung mit dem virtuellen Computer herstellen. Führen Sie einen der folgenden Befehle zum Erstellen einer Sitzung mit dem Namen des virtuellen Computers oder GUID:  
  
    ```  
    Enter-PSSession -VMName <VMName>  
    ```  
  
    ```  
    Enter-PSSession -VMGUID <VMGUID>  
    ```  
  
3. Geben Sie Ihre Anmeldeinformationen für den virtuellen Computer.   
4. Führen Sie alle erforderlichen Befehle aus. Diese Befehle werden auf dem virtuellen Computer ausgeführt, auf dem Sie die Sitzung erstellt haben.  
  
5.  Wenn Sie fertig sind, verwenden Sie die [Exit-PSSession](https://technet.microsoft.com/library/hh849743.aspx) zum Schließen der Sitzung.   
  
    ```  
    Exit-PSSession  
    ```  
  
## <a name="run-script-or-command-with-invoke-command-cmdlet"></a>Ausführen von Skripts oder Befehls mit dem Cmdlet "Invoke-Command"  
Sie können mithilfe des Cmdlets [Invoke-Command](https://docs.microsoft.com/powershell/module/Microsoft.PowerShell.Core/Invoke-Command) einen vordefinierten Satz von Befehlen auf dem virtuellen Computer ausführen. Es folgt ein Beispiel der Nutzung des Cmdlets „Invoke-Command“, wobei „PSTest“ der Name des virtuellen Computers ist und sich das auszuführende Skript (foo.ps1) im Skriptordner auf Laufwerk C:/ befindet:   
  
```  
Invoke-Command -VMName PSTest  -FilePath C:\script\foo.ps1  
```  
  
Zum Ausführen eines einzelnen Befehls verwenden Sie den Parameter **-ScriptBlock**:  
  
```  
Invoke-Command -VMName PSTest  -ScriptBlock { cmdlet }  
```  
  
## <a name="whats-required-to-use-powershell-direct"></a>Was ist erforderlich, um PowerShell direkt zu verwenden?  
So richten Sie eine PowerShell Direct-Sitzung auf einem virtuellen Computer ein  
  
-   Der virtuelle Computer muss lokal auf dem Host ausgeführt und gestartet werden.  
  
-   Sie müssen am Hostcomputer als Hyper-V-Administrator angemeldet sein.  
  
-   Sie müssen gültige Anmeldeinformationen für den virtuellen Computer angeben.  
  
-   Betriebssystem des Hosts mindestens ausführen muss Windows 10 oder Windows Server 2016.
  
-   Ausführen des virtuellen Computers muss mindestens Windows 10 oder Windows Server 2016.  
  
Sie können die [Get-VM](https://docs.microsoft.com/powershell/module/hyper-v/get-vm) Cmdlet überprüfen Sie, ob die Anmeldeinformationen, Sie verwenden, die Hyper-V-Administratorrolle sowie eine Liste der virtuellen Computer lokal auf dem Host ausgeführt werden und gestartet wurden.  
  
## <a name="see-also"></a>Siehe auch  
[Enter-PSSession](https://docs.microsoft.com/powershell/module/Microsoft.PowerShell.Core/Enter-PSSession)  
[Exit-PSSession](https://docs.microsoft.com/powershell/module/Microsoft.PowerShell.Core/Exit-PSSession)  
[Invoke-Command](https://docs.microsoft.com/powershell/module/Microsoft.PowerShell.Core/Invoke-Command)  
  


