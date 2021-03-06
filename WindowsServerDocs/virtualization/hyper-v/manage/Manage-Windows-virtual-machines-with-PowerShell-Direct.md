---
title: Verwalten von virtuellen Windows-Computern mit PowerShell Direct
description: Hier finden Sie Anweisungen für die Verwendung von PowerShell Direct zum Verwalten virtueller Computer ohne Verwendung eines Netzwerks oder einer Remote Verbindung.
ms.topic: article
ms.assetid: b5715c02-a90f-4de9-a71e-0fc09093ba2d
ms.author: benarm
author: BenjaminArmstrong
ms.date: 10/04/2016
ms.openlocfilehash: fcf9863a90b9d42d1495c0da0267feba18d119a1
ms.sourcegitcommit: dd1fbb5d7e71ba8cd1b5bfaf38e3123bca115572
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/17/2020
ms.locfileid: "90744735"
---
# <a name="manage-windows-virtual-machines-with-powershell-direct"></a>Verwalten von virtuellen Windows-Computern mit PowerShell Direct

>Gilt für: Windows 10, Windows Server 2016, Windows Server 2019

Mit PowerShell Direct können Sie einen virtuellen Computer unter Windows 10, Windows Server 2016 oder Windows Server 2019 über einen Hyper-V-Host unter Windows 10, Windows Server 2016 oder Windows 2019 Server remote verwalten. PowerShell Direct ermöglicht die Windows PowerShell-Verwaltung innerhalb eines virtuellen Computers unabhängig von der Netzwerkkonfiguration oder den Remote Verwaltungs Einstellungen auf dem Hyper-V-Host oder dem virtuellen Computer. Dies erleichtert es Hyper-V-Administratoren zur Automatisierung und Verwaltung virtueller Computer und Konfiguration Skript.

Es gibt zwei Verfahren zum Ausführen von PowerShell direkt:

- Erstellen und Beenden einer PowerShell Direct-Sitzungs mit PSSession-cmdlets

- Ausführen von Skripts oder Befehls mit dem Invoke-Command-cmdlet

Wenn Sie ältere virtuelle Computer verwalten, verwenden Sie die Verbindung mit virtuellen Computern (VMConnect) oder [Konfigurieren Sie ein virtuelles Netzwerk für den virtuellen Computer](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc816585(v=ws.10)).

## <a name="create-and-exit-a-powershell-direct-session-using-pssession-cmdlets"></a>Erstellen und Beenden einer PowerShell Direct-Sitzungs mit PSSession-cmdlets

1. Öffnen Sie Windows PowerShell als Administrator, auf dem Hyper-V-Host.

2. Verwenden [Sie das Enter-PSSession-](/powershell/module/microsoft.powershell.core/enter-pssession?view=powershell-7) Cmdlet, um eine Verbindung mit dem virtuellen Computer herzustellen. Führen Sie einen der folgenden Befehle aus, um eine Sitzung mit dem Namen oder der GUID des virtuellen Computers zu erstellen:

    ```
    Enter-PSSession -VMName <VMName>
    ```

    ```
    Enter-PSSession -VMGUID <VMGUID>
    ```

3. Geben Sie Ihre Anmelde Informationen für den virtuellen Computer ein.
4. Führen Sie beliebige Befehle werden müssen. Diese Befehle führen Sie auf dem virtuellen Computer, dem Sie der Sitzung erstellt.

5.  Wenn Sie fertig sind, verwenden Sie [Exit-PSSession](/powershell/module/microsoft.powershell.core/exit-pssession?view=powershell-7) , um die Sitzung zu schließen.

    ```
    Exit-PSSession
    ```

## <a name="run-script-or-command-with-invoke-command-cmdlet"></a>Ausführen von Skripts oder Befehls mit dem Cmdlet "Invoke-Command"
Sie können mithilfe des Cmdlets [Invoke-Command](/powershell/module/Microsoft.PowerShell.Core/Invoke-Command) einen vordefinierten Satz von Befehlen auf dem virtuellen Computer ausführen. Es folgt ein Beispiel der Nutzung des Cmdlets „Invoke-Command“, wobei „PSTest“ der Name des virtuellen Computers ist und sich das auszuführende Skript (foo.ps1) im Skriptordner auf Laufwerk C:/ befindet:

```
Invoke-Command -VMName PSTest  -FilePath C:\script\foo.ps1
```

Zum Ausführen eines einzelnen Befehls verwenden Sie den Parameter **-ScriptBlock**:

```
Invoke-Command -VMName PSTest  -ScriptBlock { cmdlet }
```

## <a name="whats-required-to-use-powershell-direct"></a>Was ist erforderlich, um PowerShell direkt zu verwenden?
Zum Erstellen einer PowerShell-Direct-Sitzung auf einem virtuellen Computer

-   Die virtuelle Maschine muss lokal auf dem Host ausgeführt werden und gestartet.

-   Sie müssen in dem Hostcomputer als Hyper-V-Administrator angemeldet sein.

-   Sie müssen gültige Anmeldeinformationen für den virtuellen Computer angeben.

-   Auf dem Host Betriebssystem muss mindestens Windows 10 oder Windows Server 2016 ausgeführt werden.

-   Auf dem virtuellen Computer muss mindestens Windows 10 oder Windows Server 2016 ausgeführt werden.

Mithilfe des Cmdlets [Get-VM](/powershell/module/hyper-v/get-vm) können Sie überprüfen, ob die von Ihnen verwendeten Anmelde Informationen die Rolle "Hyper-V-Administrator" aufweisen und eine Liste der virtuellen Computer, die lokal auf dem Host ausgeführt werden, und gestartet wird.

## <a name="see-also"></a>Weitere Informationen
[Enter-PSSession](/powershell/module/Microsoft.PowerShell.Core/Enter-PSSession) 
 [Exit-PSSession](/powershell/module/Microsoft.PowerShell.Core/Exit-PSSession) 
 [Befehl "aufrufen](/powershell/module/Microsoft.PowerShell.Core/Invoke-Command) "