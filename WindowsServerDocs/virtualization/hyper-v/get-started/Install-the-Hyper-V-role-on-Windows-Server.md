---
title: Installieren der Hyper-V-Rolle unter Windows Server
description: Enthält Anweisungen zum Installieren von Hyper-V mithilfe von Server-Manager oder Windows PowerShell.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 8e871317-09d2-4314-a6ec-ced12b7aee89
author: KBDAzure
ms.author: kathydav
ms.date: 12/02/2016
ms.openlocfilehash: 2687a907852e2a81f03b147df1425cd01b34fb76
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71392809"
---
# <a name="install-the-hyper-v-role-on-windows-server"></a>Installieren der Hyper-V-Rolle unter Windows Server

>Gilt für: Windows Server 2016, Windows Server 2019
  
Um virtuelle Computer zu erstellen und auszuführen, installieren Sie die Hyper-V-Rolle unter Windows Server, indem Sie Server-Manager oder das Cmdlet **install-Windows Feature** in Windows PowerShell verwenden. Informationen zu Windows 10 finden Sie unter [Installieren von Hyper-V unter Windows 10](https://docs.microsoft.com/virtualization/hyper-v-on-windows/quick-start/enable-hyper-v).

Weitere Informationen zu Hyper-v finden Sie in der [Übersicht über die Hyper-v-Technologie](../Hyper-V-Technology-Overview.md). Zum Ausprobieren von Windows Server 2019 können Sie eine Evaluierungsversion herunterladen und installieren. Weitere Informationen finden Sie im [Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-windows-server-2019).

Stellen Sie vor dem Installieren von Windows Server oder dem Hinzufügen der Hyper-V-Rolle Folgendes sicher:
- Die Computer Hardware ist kompatibel. Weitere Informationen finden Sie unter [Systemanforderungen für Windows Server](../../../get-started/System-Requirements.md) und [Systemanforderungen für Hyper-V unter Windows Server](../System-requirements-for-Hyper-V-on-Windows.md).
- Sie beabsichtigen nicht, Virtualisierungsanwendungen von Drittanbietern zu verwenden, die auf den gleichen Prozessor Features basieren, die von Hyper-V benötigt werden. Beispiele hierfür sind VMware-Arbeitsstation und VirtualBox. Sie können Hyper-V installieren, ohne diese anderen apps zu deinstallieren. Wenn Sie jedoch versuchen, Sie zum Verwalten virtueller Maschinen zu verwenden, wenn der Hyper-V-Hypervisor ausgeführt wird, werden die virtuellen Computer möglicherweise nicht zuverlässig gestartet oder nicht zuverlässig ausgeführt. Ausführliche Informationen und Anweisungen zum Ausschalten des Hyper-v-Hypervisors, wenn Sie eine dieser Apps verwenden müssen, finden Sie unter [Virtualisierungsanwendungen funktionieren nicht zusammen mit Hyper-v, Device Guard und Credential Guard](https://support.microsoft.com/help/3204980/virtualization-applications-do-not-work-together-with-hyper-v-device-g).

Wenn Sie nur die Verwaltungs Tools (z. b. Hyper-v-Manager) installieren möchten, finden Sie weitere Informationen unter [Remote Verwaltung von Hyper-v-Hosts mit Hyper-v-Manager](../Manage/Remotely-manage-Hyper-V-hosts.md).
  
## <a name="install-hyper-v-by-using-server-manager"></a>Installieren von Hyper-V mit Server-Manager  
  
1. Klicken Sie im **Server-Manager** im Menü **Verwalten** auf **Rollen und Funktionen hinzufügen**.  
  
2. Überprüfen Sie auf der Seite **Vorbemerkungen**, ob der Zielserver und die Netzwerkumgebung für die Installation der Rolle und des Features vorbereitet sind. Klicken Sie auf **Weiter**.  
  
3. Wählen Sie auf der Seite **Installationstyp auswählen** die Option **Rollenbasierte oder featurebasierte Installation**, und klicken Sie anschließend auf **Weiter**.  
  
4. Wählen Sie auf der Seite **Zielserver auswählen** einen Server aus dem Serverpool aus, und klicken Sie auf **Weiter**.  
  
5. Wählen Sie auf der Seite **Serverrollen auswählen** die Option **Hyper-V**.  
  
6. Klicken Sie auf **Features hinzufügen**, um die Tools hinzuzufügen, die Sie zum Erstellen und Verwalten von virtuellen Computern verwenden. Klicken Sie auf der Seite mit den Features auf **Weiter**.  
  
7. Wählen Sie auf der Seite **Virtuelle Switches erstellen**, **Migration eines virtuellen Computers** und **Standardspeicher** die gewünschten Optionen.  
  
8. Wählen Sie auf der Seite **Installationsauswahl bestätigen** die Option **Zielserver bei Bedarf automatisch neu starten**, und klicken Sie dann auf **Installieren**.  
  
9. Vergewissern Sie sich nach Abschluss der Installation, dass Hyper-V ordnungsgemäß installiert ist. Öffnen Sie in Server-Manager die Seite **alle Server** , und wählen Sie einen Server aus, auf dem Hyper-V installiert ist. Überprüfen Sie die Kachel **Rollen und Features** auf der Seite für den ausgewählten Server.  
  
## <a name="install-hyper-v-by-using-the-install-windowsfeature-cmdlet"></a>Installieren von Hyper-V mithilfe des Cmdlets "Install-Windows Feature"  
  
1. Klicken Sie auf dem Windows-Desktop auf die Schaltfläche „Start“, und geben Sie einen beliebigen Teil des Namens **Windows PowerShell** ein.  
  
2. Klicken Sie mit der rechten Maustaste auf Windows PowerShell, und wählen Sie **als Administrator ausführen**.  
  
3. Wenn Sie Hyper-V auf einem Server installieren möchten, mit dem Sie eine Remote Verbindung hergestellt haben, führen Sie den folgenden Befehl aus, und ersetzen Sie `<computer_name>` durch den Namen des Servers.  
  
    ```powershell
    Install-WindowsFeature -Name Hyper-V -ComputerName <computer_name> -IncludeManagementTools -Restart  
    ```  
  
    Wenn Sie lokal mit dem Server verbunden sind, führen Sie den Befehl ohne `-ComputerName <computer_name>` aus.  
  
4. Nachdem der Server neu gestartet wurde, können Sie sehen, dass die Hyper-V-Rolle installiert ist, und sehen, welche anderen Rollen und Features installiert werden, indem Sie den folgenden Befehl ausführen:  
  
    ```powershell
    Get-WindowsFeature -ComputerName <computer_name>  
    ```  
  
    Wenn Sie lokal mit dem Server verbunden sind, führen Sie den Befehl ohne `-ComputerName <computer_name>` aus.  
  
> [!NOTE]  
> Wenn Sie diese Rolle auf einem Server installieren, auf dem die Server Core-Installationsoption von Windows Server 2016 ausgeführt wird, und den Parameter `-IncludeManagementTools` verwenden, wird nur das Hyper-V-Modul für Windows PowerShell installiert. Sie können das GUI-Verwaltungs Tool Hyper-v-Manager auf einem anderen Computer verwenden, um einen Hyper-v-Host, der auf einer Server Core-Installation ausgeführt wird, Remote zu verwalten. Anweisungen zum Herstellen einer Remote Verbindung finden Sie unter [Remote Verwaltung von Hyper-v-Hosts mit dem Hyper-v-Manager](../Manage/Remotely-manage-Hyper-V-hosts.md).  
  
## <a name="see-also"></a>Siehe auch  
  
- [Install-Windows Feature](https://docs.microsoft.com/powershell/module/Microsoft.Windows.ServerManager.Migration/Install-WindowsFeature)  
