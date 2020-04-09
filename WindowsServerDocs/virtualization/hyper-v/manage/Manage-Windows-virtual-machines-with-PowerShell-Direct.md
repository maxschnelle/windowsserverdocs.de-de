---
title: Verwalten von virtuellen Windows-Computern mit PowerShell Direct
description: Hier finden Sie Anweisungen für die Verwendung von PowerShell Direct zum Verwalten virtueller Computer ohne Verwendung eines Netzwerks oder einer Remote Verbindung.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.topic: article
ms.assetid: b5715c02-a90f-4de9-a71e-0fc09093ba2d
author: kbdazure
ms.author: kathydav
ms.date: 10/04/2016
ms.openlocfilehash: c4a051de2d8f62c38ae0c44b1a62d5bf9df339e8
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80859433"
---
# <a name="manage-windows-virtual-machines-with-powershell-direct"></a>Verwalten von virtuellen Windows-Computern mit PowerShell Direct

>Gilt für: Windows 10, Windows Server 2016, Windows Server 2019
  
Mit PowerShell Direct können Sie einen virtuellen Computer unter Windows 10, Windows Server 2016 oder Windows Server 2019 über einen Hyper-V-Host unter Windows 10, Windows Server 2016 oder Windows 2019 Server remote verwalten. PowerShell Direct ermöglicht die Windows PowerShell-Verwaltung innerhalb eines virtuellen Computers unabhängig von der Netzwerkkonfiguration oder den Remote Verwaltungs Einstellungen auf dem Hyper-V-Host oder dem virtuellen Computer. Dies erleichtert Hyper-V-Administratoren die Automatisierung und Erstellung von Skripts zur Verwaltung und Konfiguration virtueller Computer.  
  
Es gibt zwei Möglichkeiten, PowerShell Direct auszuführen:  
  
- Erstellen und Beenden einer PowerShell Direct-Sitzungs mit PSSession-cmdlets
  
- Ausführen von Skripts oder Befehls mit dem Invoke-Command-cmdlet
  
Wenn Sie ältere virtuelle Computer verwalten, verwenden Sie die Verbindung mit virtuellen Computern (VMConnect) oder [Konfigurieren Sie ein virtuelles Netzwerk für den virtuellen Computer](https://technet.microsoft.com/library/cc816585.aspx).  
  
## <a name="create-and-exit-a-powershell-direct-session-using-pssession-cmdlets"></a>Erstellen und Beenden einer PowerShell Direct-Sitzungs mit PSSession-cmdlets  
  
1. Öffnen Sie Windows PowerShell auf dem Hyper-V-Host als Administrator.  
  
2. Verwenden [Sie das Enter-PSSession-](https://technet.microsoft.com/library/hh849707.aspx) Cmdlet, um eine Verbindung mit dem virtuellen Computer herzustellen. Führen Sie einen der folgenden Befehle aus, um eine Sitzung mit dem Namen oder der GUID des virtuellen Computers zu erstellen:  
  
    ```  
    Enter-PSSession -VMName <VMName>  
    ```  
  
    ```  
    Enter-PSSession -VMGUID <VMGUID>  
    ```  
  
3. Geben Sie Ihre Anmelde Informationen für den virtuellen Computer ein.   
4. Führen Sie alle erforderlichen Befehle aus. Diese Befehle werden auf dem virtuellen Computer ausgeführt, auf dem Sie die Sitzung erstellt haben.  
  
5.  Wenn Sie fertig sind, verwenden Sie [Exit-PSSession](https://technet.microsoft.com/library/hh849743.aspx) , um die Sitzung zu schließen.   
  
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
  
-   Auf dem Host Betriebssystem muss mindestens Windows 10 oder Windows Server 2016 ausgeführt werden.
  
-   Auf dem virtuellen Computer muss mindestens Windows 10 oder Windows Server 2016 ausgeführt werden.  
  
Mithilfe des Cmdlets [Get-VM](https://docs.microsoft.com/powershell/module/hyper-v/get-vm) können Sie überprüfen, ob die von Ihnen verwendeten Anmelde Informationen die Rolle "Hyper-V-Administrator" aufweisen und eine Liste der virtuellen Computer, die lokal auf dem Host ausgeführt werden, und gestartet wird.  
  
## <a name="see-also"></a>Weitere Informationen  
[Enter-PSSession](https://docs.microsoft.com/powershell/module/Microsoft.PowerShell.Core/Enter-PSSession)  
[Exit-PSSession](https://docs.microsoft.com/powershell/module/Microsoft.PowerShell.Core/Exit-PSSession)  
[Befehl "aufrufen"](https://docs.microsoft.com/powershell/module/Microsoft.PowerShell.Core/Invoke-Command)  
  


