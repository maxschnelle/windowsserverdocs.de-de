---
title: Installieren Sie die Netzwerk-Controller-Serverrolle mit Server-Manager
description: Dieses Thema enthält Anweisungen zum Installieren Sie der Netzwerk-Controller-Serverrolle mithilfe des Server-Managers in Windows Server 2016.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 3a6e4352-ff62-4290-b8a4-5c83740070fc
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 15cb1ef3bad7038cc97784504807b44b4920def6
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="install-the-network-controller-server-role-using-server-manager"></a>Installieren Sie die Netzwerk-Controller-Serverrolle mit Server-Manager

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Dieses Thema enthält Anweisungen für die Netzwerk-Controller-Serverrolle mithilfe von Server-Manager installieren.

>[!IMPORTANT]
>Stellen Sie die Serverrolle "Netzwerkcontroller" auf physischen Hosts nicht. Sie müssen die Netzwerk-Controller-Serverrolle auf einem virtuellen Hyper-V-Computer installieren, zum Bereitstellen von Netzwerkcontroller \(VM\), die auf einem Hyper-V-Host installiert ist. Nachdem Sie Netzwerkcontroller auf virtuellen Computern auf drei verschiedenen Hyper\-V-Hosts installiert haben, müssen Sie die Hyper\-V-Hosts für die Software Defined Networking \(SDN\) durch Hinzufügen von Hosts des Netzwerkcontrollers mithilfe von Windows PowerShell-Befehl aktivieren **neu NetworkControllerServer**. Auf diese Weise aktivieren Sie das Lastenausgleichsmodul für SDN-Software funktioniert. Weitere Informationen finden Sie unter [neu NetworkControllerServer](https://technet.microsoft.com/itpro/powershell/windows/network-controller/new-networkcontrollerserver).
  
Nach der Installation von Netzwerkcontroller müssen Sie Windows PowerShell-Befehle für die weitere Netzwerk-Controller-Konfiguration verwenden. Weitere Informationen finden Sie unter [Bereitstellen des Netzwerkcontrollers mithilfe von Windows PowerShell](../../deploy/Deploy-Network-Controller-using-Windows-PowerShell.md).  
  
### <a name="to-install-network-controller"></a>So installieren Sie Netzwerkcontroller  
  
1.  Klicken Sie im Server-Manager auf **verwalten**, und klicken Sie dann auf **Hinzufügen von Rollen und Features**. Der Assistent zum Hinzufügen von Rollen und Features wird geöffnet. Klicken Sie auf **Weiter**.  
  
2.  In **Select Installation Type**, halten Sie die Standardeinstellung, und klicken Sie auf **Weiter**.  
  
3.  In **Zielserver auswählen**, wählen Sie den Server, in dem Sie installieren möchten Netzwerkcontroller, und klicken Sie dann auf **Weiter**.  
  
4.  In **Serverrollen auswählen**im **Rollen**, klicken Sie auf **Netzwerkcontroller**.  
  
    ![Netzwerk-Controller-Serverrolle](../../../media/Install-the-Network-Controller-server-role-using-Server-Manager/netc_install_07.jpg)  
  
5.  Die **Hinzufügen von Features, die für den Netzwerkcontroller erforderlich sind** Dialogfeld wird geöffnet. Klicken Sie auf **Hinzufügen von Features**.  
  
    ![Hinzufügen von Features für den Netzwerkcontroller](../../../media/Install-the-Network-Controller-server-role-using-Server-Manager/netc_install_06.jpg)  
  
6.  In **Serverrollen auswählen**, klicken Sie auf **Weiter**.  
  
    ![Klicken Sie auf Weiter](../../../media/Install-the-Network-Controller-server-role-using-Server-Manager/netc_install_07.jpg)  
  
7.  In **Features auswählen**, klicken Sie auf **Weiter**.  
  
8.  In **Netzwerkcontroller** klicken Sie auf **Weiter**.  
  
9. In **Installationsauswahl bestätigen**, überprüfen Sie Ihre Auswahl. Installation des Netzwerkcontroller erfordert, dass Sie den Computer neu starten, nachdem der Assistent ausgeführt wird. Aus diesem Grund klicken Sie auf **Zielserver bei Bedarf automatisch neu**. Die **Hinzufügen von Rollen und Features Assistenten** Dialogfeld wird geöffnet. Klicken Sie auf **Ja**.  
  
    ![Hinzufügen von Rollen und Features-Assistenten](../../../media/Install-the-Network-Controller-server-role-using-Server-Manager/netc_install_11.jpg)  
  
10. In **Installationsauswahl bestätigen**, klicken Sie auf **installieren**.  
  
11. Die Netzwerk-Controller-Serverrolle installiert, auf dem Zielserver, und klicken Sie dann den Server neu gestartet wird.  
  
12. Nach dem Neustart des Computers, melden Sie sich bei dem Computer, und überprüfen Sie Netzwerkcontroller Installation von Server-Manager anzeigen.  
  
    ![Server-Manager](../../../media/Install-the-Network-Controller-server-role-using-Server-Manager/nc_013.jpg)  
  
## <a name="see-also"></a>Siehe auch  
[Netzwerkcontroller](Network-Controller.md)  
  


