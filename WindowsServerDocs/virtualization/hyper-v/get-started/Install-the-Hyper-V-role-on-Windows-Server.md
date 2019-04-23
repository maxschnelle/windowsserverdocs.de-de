---
title: Installieren der Hyper-V-Serverrolle unter Windows Server
description: Enthält Anweisungen zum Installieren von Hyper-V über Server-Manager oder Windows PowerShell
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 8e871317-09d2-4314-a6ec-ced12b7aee89
author: KBDAzure
ms.author: kathydav
ms.date: 12/02/2016
ms.openlocfilehash: a4167065c11cf87ba761ed65884b88c5413dfdf8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59870431"
---
# <a name="install-the-hyper-v-role-on-windows-server"></a>Installieren der Hyper-V-Serverrolle unter Windows Server

>Gilt für: WindowsServer 2016, WindowsServer 2019
  
Installieren Sie zum Erstellen und Ausführen von virtuellen Computern, die Hyper-V-Rolle unter Windows Server mithilfe von Server-Manager oder das **Install-WindowsFeature** Windows PowerShell-Cmdlet. Windows 10, finden Sie unter [Installieren von Hyper-V unter Windows 10](https://docs.microsoft.com/virtualization/hyper-v-on-windows/quick-start/enable-hyper-v).

Weitere Informationen zu Hyper-V finden Sie unter den [Übersicht über die Hyper-V-Technologie](..\Hyper-V-Technology-Overview.md). Um Windows Server-2019 auszuprobieren, können Sie herunterladen und installieren eine Evaluierungsversion. Finden Sie unter den [Evaluierungscenter](https://www.microsoft.com/evalcenter/evaluate-windows-server-2019).

Vor der Installation von Windows Server und Hyper-V-Rolle hinzufügen, stellen Sie sicher, dass:
- Die Computerhardware ist kompatibel. Weitere Informationen finden Sie unter [System Requirements for Windows Server](../../../get-started/System-Requirements.md) und [Systemanforderungen für Hyper-V unter Windows Server](../System-requirements-for-Hyper-V-on-Windows.md).
- Sie möchten keine apps von Drittanbietern verwenden, die die gleichen Prozessorfunktionen verwenden, die Hyper-V erfordert. Beispiele: VMWare Workstation und VirtualBox. Sie können Hyper-V installieren, ohne diese anderen apps zu deinstallieren. Aber wenn Sie versuchen, diese verwenden, um virtuelle Computer verwalten, wenn der Hyper-V-Hypervisor ausgeführt wird, wird die virtuellen Computer möglicherweise nicht gestartet oder unberechenbar Verhalten führen kann. Details und Anweisungen zum Deaktivieren des Hyper-V-Hypervisors, wenn Sie eine dieser apps verwenden müssen, finden Sie unter [Virtualization-Anwendungen funktionieren nicht zusammen mit Hyper-V, Device Guard und Credential Guard](https://support.microsoft.com/help/3204980/virtualization-applications-do-not-work-together-with-hyper-v-device-g).

Wenn Sie nur die Verwaltungstools, wie z. B. Hyper-V-Manager installieren möchten, finden Sie unter [Remoteverwaltung von Hyper-V-Hosts mit Hyper-V-Manager](..\Manage\Remotely-manage-Hyper-V-hosts.md).
  
## <a name="BKMK_SERV"></a>Installieren von Hyper-V mithilfe von Server-Manager  
  
1. Klicken Sie im **Server-Manager** im Menü **Verwalten** auf **Rollen und Funktionen hinzufügen**.  
  
2. Überprüfen Sie auf der Seite **Vorbemerkungen**, ob der Zielserver und die Netzwerkumgebung für die Installation der Rolle und des Features vorbereitet sind. Klicken Sie auf **Weiter**.  
  
3. Wählen Sie auf der Seite **Installationstyp auswählen** die Option **Rollenbasierte oder featurebasierte Installation**, und klicken Sie anschließend auf **Weiter**.  
  
4. Wählen Sie auf der Seite **Zielserver auswählen** einen Server aus dem Serverpool aus, und klicken Sie auf **Weiter**.  
  
5. Wählen Sie auf der Seite **Serverrollen auswählen** die Option **Hyper-V**.  
  
6. Klicken Sie auf **Features hinzufügen**, um die Tools hinzuzufügen, die Sie zum Erstellen und Verwalten von virtuellen Computern verwenden. Klicken Sie auf der Seite mit den Features auf **Weiter**.  
  
7. Wählen Sie auf der Seite **Virtuelle Switches erstellen**, **Migration eines virtuellen Computers** und **Standardspeicher** die gewünschten Optionen.  
  
8. Wählen Sie auf der Seite **Installationsauswahl bestätigen** die Option **Zielserver bei Bedarf automatisch neu starten**, und klicken Sie dann auf **Installieren**.  
  
9. Wenn die Installation abgeschlossen ist, stellen Sie sicher, dass Hyper-V ordnungsgemäß installiert. Öffnen der **alle Server** Seite im Server-Manager, und wählen Sie einen Server, auf dem Sie Hyper-V installiert. Überprüfen Sie die **Rollen und Features** Kachel auf der Seite für den ausgewählten Server.  
  
## <a name="BKMK_PWRSH"></a>Installieren von Hyper-V mithilfe des Install-WindowsFeature-Cmdlets  
  
1. Klicken Sie auf dem Windows-Desktop auf die Schaltfläche „Start“, und geben Sie einen beliebigen Teil des Namens **Windows PowerShell** ein.  
  
2. Mit der rechten Maustaste in Windows PowerShell, und wählen Sie **als Administrator ausführen**.  
  
3. Um Hyper-V auf einem Server installieren Sie Remote verbunden sind, führen Sie den folgenden Befehl aus, und Ersetzen Sie `<computer_name>` mit den Namen des Servers.  
  
    ```powershell
    Install-WindowsFeature -Name Hyper-V -ComputerName <computer_name> -IncludeManagementTools -Restart  
    ```  
  
    Wenn Sie lokal auf dem Server verbunden sind, führen Sie den Befehl ohne `-ComputerName <computer_name>`.  
  
4. Nach dem Neustart des Servers werden Sie sehen, dass die Hyper-V-Rolle installiert ist, und informieren Sie andere Rollen und Features installiert, indem Sie den folgenden Befehl ausführen:  
  
    ```powershell
    Get-WindowsFeature -ComputerName <computer_name>  
    ```  
  
    Wenn Sie lokal auf dem Server verbunden sind, führen Sie den Befehl ohne `-ComputerName <computer_name>`.  
  
> [!NOTE]  
> Wenn Sie diese Rolle auf einem Server installiert, die die Server Core-Installationsoption von Windows Server 2016 ausgeführt wird, und verwenden Sie den Parameter `-IncludeManagementTools`, nur die Hyper-V-Modul für Windows PowerShell installiert ist. Sie können die GUI-Verwaltungstool, Hyper-V-Manager verwenden, auf einem anderen Computer zur Remoteverwaltung von Hyper-V-Host, der auf einer Server Core-Installation ausgeführt wird. Anweisungen dazu, eine Remoteverbindung herstellen, finden Sie unter [Remoteverwaltung von Hyper-V-Hosts mit Hyper-V-Manager](..\Manage\Remotely-manage-Hyper-V-hosts.md).  
  
## <a name="see-also"></a>Siehe auch  
  
- [Install-WindowsFeature](https://docs.microsoft.com/powershell/module/Microsoft.Windows.ServerManager.Migration/Install-WindowsFeature)  
