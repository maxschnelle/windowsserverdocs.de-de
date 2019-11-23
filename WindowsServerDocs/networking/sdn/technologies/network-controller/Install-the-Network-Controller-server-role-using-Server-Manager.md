---
title: Installieren der Server Rolle "Netzwerk Controller" mithilfe von Server-Manager
description: Dieses Thema enthält Anweisungen zum Installieren der Server Rolle "Netzwerk Controller" mithilfe von Server-Manager in Windows Server 2016.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 3a6e4352-ff62-4290-b8a4-5c83740070fc
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 8b656bbd823a10f1e36d1757bb53c4565d4e828c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405833"
---
# <a name="install-the-network-controller-server-role-using-server-manager"></a>Installieren der Server Rolle "Netzwerk Controller" mithilfe von Server-Manager

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

Dieses Thema enthält Anweisungen zum Installieren der Netzwerk Controller-Server Rolle mit Server-Manager.

>[!IMPORTANT]
>Stellen Sie die Netzwerk Controller-Server Rolle nicht auf physischen Hosts bereit. Zum Bereitstellen des Netzwerk Controllers müssen Sie die Netzwerk Controller-Server Rolle auf einem virtuellen Hyper-v-Computer \(VM-\) installieren, der auf einem Hyper-v-Host installiert ist. Nachdem Sie den Netzwerk Controller auf virtuellen Computern auf drei verschiedenen Hyper\-V-Hosts installiert haben, müssen Sie die Hyper\-V-Hosts für Software-Defined Networking \(Sdn\) aktivieren, indem Sie die Hosts mithilfe des Windows PowerShell-Befehls **New-networkcontrollerserver**dem Netzwerk Controller hinzufügen. Auf diese Weise aktivieren Sie die Load Balancer der Sdn-Software. Weitere Informationen finden Sie unter [New-networkcontrollerserver](https://technet.microsoft.com/itpro/powershell/windows/network-controller/new-networkcontrollerserver).
  
Nachdem Sie den Netzwerk Controller installiert haben, müssen Sie Windows PowerShell-Befehle für die zusätzliche Netzwerk Controller Konfiguration verwenden. Weitere Informationen finden Sie unter Bereitstellen eines [Netzwerk Controllers mithilfe von Windows PowerShell](../../deploy/Deploy-Network-Controller-using-Windows-PowerShell.md).  
  
### <a name="to-install-network-controller"></a>So installieren Sie den Netzwerk Controller  
  
1.  Klicken Sie im Server-Manager auf **Verwalten**und dann auf **Rollen und Features hinzufügen**. Der Assistent zum Hinzufügen von Rollen und Features wird geöffnet. Klicken Sie auf **Weiter**.  
  
2.  Behalten Sie in **Installationstyp auswählen**die Standardeinstellung bei, und klicken Sie auf **weiter**.  
  
3.  Wählen Sie unter **Ziel Server auswählen**den Server aus, auf dem Sie den Netzwerk Controller installieren möchten, und klicken Sie dann auf **weiter**.  
  
4.  Klicken Sie unter **Server Rollen auswählen**unter **Rollen**auf **Netzwerk Controller**.  
  
    ![Netzwerk Controller-Server Rolle](../../../media/Install-the-Network-Controller-server-role-using-Server-Manager/netc_install_07.jpg)  
  
5.  Das Dialogfeld **für den Netzwerk Controller erforderliche Features hinzufügen wird** geöffnet. Klicken Sie auf **Features hinzufügen**.  
  
    ![Features für Netzwerk Controller hinzufügen](../../../media/Install-the-Network-Controller-server-role-using-Server-Manager/netc_install_06.jpg)  
  
6.  Klicken Sie unter **Server Rollen auswählen**auf **weiter**.  
  
    ![Klicken Sie auf weiter](../../../media/Install-the-Network-Controller-server-role-using-Server-Manager/netc_install_07.jpg)  
  
7.  Klicken Sie unter **Features auswählen**auf **weiter**.  
  
8.  Klicken Sie im **Netzwerk Controller** auf **weiter**.  
  
9. Überprüfen Sie unter **Installations Auswahl bestätigen**Ihre Auswahl. Die Installation des Netzwerk Controllers erfordert, dass Sie den Computer nach dem Ausführen des Assistenten neu starten. Klicken Sie daher auf **den Zielserver bei Bedarf automatisch neu starten**. Das Dialogfeld **Assistent zum Hinzufügen von Rollen und Features** wird geöffnet. Klicken Sie auf **Ja**.  
  
    ![Assistent zum Hinzufügen von Rollen und Features](../../../media/Install-the-Network-Controller-server-role-using-Server-Manager/netc_install_11.jpg)  
  
10. Klicken Sie unter **Installationsauswahl bestätigen** auf **Installieren**.  
  
11. Die Server Rolle "Netzwerk Controller" wird auf dem Zielserver installiert, und der Server wird neu gestartet.  
  
12. Melden Sie sich nach dem Neustart des Computers am Computer an, und überprüfen Sie die Installation des Netzwerk Controllers, indem Sie Server-Manager anzeigen.  
  
    ![Server-Manager](../../../media/Install-the-Network-Controller-server-role-using-Server-Manager/nc_013.jpg)  
  
## <a name="see-also"></a>Weitere Informationen  
[Netzwerkcontroller](Network-Controller.md)  
  


