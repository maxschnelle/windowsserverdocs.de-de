---
title: Installieren der Serverrolle der Netzwerk-Controller mit dem Server-Manager
description: Dieses Thema enthält Anweisungen zum Installieren Sie der Netzwerkcontroller-Serverrolle mithilfe von Server-Manager in Windows Server 2016.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 3a6e4352-ff62-4290-b8a4-5c83740070fc
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 699e2ca5c4ec33099d0ad948523b6f587ad118e4
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59859061"
---
# <a name="install-the-network-controller-server-role-using-server-manager"></a>Installieren der Serverrolle der Netzwerk-Controller mit dem Server-Manager

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Dieses Thema enthält Anweisungen zum Installieren Sie der Netzwerkcontroller-Serverrolle mithilfe des Server-Manager.

>[!IMPORTANT]
>Stellen Sie keine der Serverrolle "Netzwerkcontroller" auf physischen Hosts ausgeführt werden. Sie müssen die Netzwerkcontroller-Serverrolle auf einem virtuellen Hyper-V-Computer installieren, zum Bereitstellen des Netzwerkcontrollers \(VM\) , die auf einem Hyper-V-Host installiert ist. Nach der Installation des Netzwerkcontrollers auf virtuellen Computern für drei verschiedene Hyper\-V-Hosts müssen Sie die Hyper aktivieren\-V-Hosts für die Software Defined Networking \(SDN\) durch Hinzufügen von Hosts mit dem Netzwerkcontroller der Windows PowerShell-Befehl **New-NetworkControllerServer**. Auf diese Weise aktivieren Sie den SDN-Softwarelastenausgleich-Funktion. Weitere Informationen finden Sie unter [New-NetworkControllerServer](https://technet.microsoft.com/itpro/powershell/windows/network-controller/new-networkcontrollerserver).
  
Nach der Installation des Netzwerkcontrollers müssen Sie Windows PowerShell-Befehle für die weitere Konfiguration für den Netzwerkcontroller verwenden. Weitere Informationen finden Sie unter [Bereitstellen des Netzwerkcontrollers mithilfe von Windows PowerShell](../../deploy/Deploy-Network-Controller-using-Windows-PowerShell.md).  
  
### <a name="to-install-network-controller"></a>So installieren Sie den Netzwerkcontroller  
  
1.  Klicken Sie im Server-Manager auf **Verwalten**und dann auf **Rollen und Features hinzufügen**. Des Assistenten zum Hinzufügen von Rollen und Features wird geöffnet. Klicken Sie auf **Weiter**.  
  
2.  In **Select Installation Type**, die Standardeinstellung, und klicken Sie auf **Weiter**.  
  
3.  In **Zielserver auswählen**, wählen Sie den Server, in dem Sie installieren möchten Netzwerkcontroller, und klicken Sie dann auf **Weiter**.  
  
4.  In **Serverrollen auswählen**im **Rollen**, klicken Sie auf **Netzwerkcontroller**.  
  
    ![Netzwerk-Controller-Server-Rolle](../../../media/Install-the-Network-Controller-server-role-using-Server-Manager/netc_install_07.jpg)  
  
5.  Die **Hinzufügen von Funktionen, die für den Netzwerkcontroller erforderlich sind** Dialogfeld wird geöffnet. Klicken Sie auf **Hinzufügen von Funktionen**.  
  
    ![Hinzufügen von Funktionen für den Netzwerkcontroller](../../../media/Install-the-Network-Controller-server-role-using-Server-Manager/netc_install_06.jpg)  
  
6.  In **Serverrollen auswählen**, klicken Sie auf **Weiter**.  
  
    ![Klicken Sie auf Weiter](../../../media/Install-the-Network-Controller-server-role-using-Server-Manager/netc_install_07.jpg)  
  
7.  In **Features auswählen**, klicken Sie auf **Weiter**.  
  
8.  In **Netzwerkcontroller** klicken Sie auf **Weiter**.  
  
9. In **Installationsauswahl bestätigen**, überprüfen Sie Ihre Auswahl. Installation des Netzwerkcontrollers erfordert, dass Sie den Computer neu starten, nachdem der Assistent ausgeführt wird. Aus diesem Grund klicken Sie auf **automatisch neu starten die Zielserver bei Bedarf**. Die **Hinzufügen von Rollen und Features Assistenten** Dialogfeld wird geöffnet. Klicken Sie auf **Ja**.  
  
    ![Assistent zum Hinzufügen von Rollen und Features](../../../media/Install-the-Network-Controller-server-role-using-Server-Manager/netc_install_11.jpg)  
  
10. Klicken Sie unter **Installationsauswahl bestätigen** auf **Installieren**.  
  
11. Die Netzwerkcontroller-Serverrolle installiert wird, auf dem Zielserver, und klicken Sie dann den Server neu gestartet wurde.  
  
12. Nach dem Neustart des Computers melden Sie sich bei dem Computer, und überprüfen Sie den Netzwerkcontroller-Installation durch Anzeigen von Server-Manager.  
  
    ![Server-Manager](../../../media/Install-the-Network-Controller-server-role-using-Server-Manager/nc_013.jpg)  
  
## <a name="see-also"></a>Siehe auch  
[Netzwerkcontroller](Network-Controller.md)  
  


