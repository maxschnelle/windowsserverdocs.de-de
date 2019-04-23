---
title: Verwalten des VPN in Windows Server Essentials
description: Beschreibt, wie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cc2b264a-b9a8-4114-9f7b-8604f77096e5
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: ec367337318d12161a250572745d8f303d098ffe
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59849201"
---
# <a name="manage-vpn-in-windows-server-essentials"></a>Verwalten des VPN in Windows Server Essentials

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials 
  
 Virtuelle private Netzwerkverbindungen (VPN) ermöglichen es Benutzern, zuhause oder unterwegs zu arbeiten, um auf einen Server in einem privaten Netzwerk zuzugreifen, indem sie die von einem öffentlichen Netzwerk wie z. B. dem Internet bereitgestellte Infrastruktur nutzen. Zur Verwendung von VPN für den Zugriff auf Serverressourcen müssen Sie folgende Schritte ausführen:  
  
-   [VPN für den Remotezugriff auf dem Server aktivieren](Manage-VPN-in-Windows-Server-Essentials.md#BKMK_1)  
  
-   [Festlegen von VPN-Berechtigungen für Netzwerkbenutzer](Manage-VPN-in-Windows-Server-Essentials.md#BKMK_2)  
  
-   [Verbinden Sie Clientcomputer mit dem server](Manage-VPN-in-Windows-Server-Essentials.md#BKMK_Connect)  
  
-   [Verwenden Sie-VPN-Verbindung mit Windows Server Essentials](Manage-VPN-in-Windows-Server-Essentials.md#BKMK_3)  
  
##  <a name="BKMK_1"></a> VPN für den Remotezugriff auf dem Server aktivieren  
 Führen Sie das folgende Verfahren aus, um das VPN in Windows Server Essentials für das Aktivieren des Remotezugriffs zu konfigurieren.  
  
#### <a name="to-enable-vpn-in-windows-server-essentials"></a>So aktivieren Sie das VPN in Windows Server Essentials  
  
1.  Öffnen Sie das Dashboard.  
  
2.  Klicken Sie auf **Einstellungen** und dann auf die Registerkarte **Zugriff überall**.  
  
3.  Klicken Sie auf **Konfigurieren**. Der Assistent zum Einrichten von %%amp;quot;Zugriff überall%%amp;quot; wird gestartet.  
  
4.  Aktivieren Sie auf der Seite **Folgende Funktionen für Zugriff überall aktivieren** das Kontrollkästchen **Virtuelles privates Netzwerk**.  
  
5.  Folgen Sie den Anweisungen, um den Assistenten fertigzustellen.  
  
##  <a name="BKMK_2"></a> Festlegen von VPN-Berechtigungen für Netzwerkbenutzer  
 Sie können eine Verbindung mit Windows Server Essentials über VPN herstellen und auf alle Ressourcen zugreifen, die auf dem Server gespeichert sind. Dies ist besonders dann nützlich, wenn auf Ihrem Clientcomputer Netzwerkkonten eingerichtet sind, die verwendet werden können, um eine Verbindung mit einem gehosteten Windows Server Essentials-Server über eine VPN-Verbindung herzustellen. Alle auf dem dem gehosteten Windows Server Essentials-Server neu erstellten Benutzerkonten müssen bei der ersten Anmeldung am Clientcomputer VPN verwenden.  
  
#### <a name="to-set-vpn-permissions-for-network-users"></a>So legen Sie die VPN-Berechtigungen für Netzwerkbenutzer fest  
  
1.  Öffnen Sie das Dashboard.  
  
2.  Klicken Sie auf der Navigationsleiste auf **BENUTZER**.  
  
3.  Wählen Sie in der Liste von Benutzerkonten das Benutzerkonto aus, für das Sie die Berechtigung zum Remotezugriff auf den Desktop gewähren möchten.  
  
4.  In der **< Benutzerkonto\> Aufgaben** Bereich, klicken Sie auf **Eigenschaften**.  
  
5.  In der **< Benutzerkonto\> Eigenschaften**, klicken Sie auf die **Zugriff überall** Registerkarte.  
  
6.  Aktivieren Sie auf der Registerkarte **Zugriff überall** das Kontrollkästchen **Virtuelles privates Netzwerk (VPN) zulassen**  , um es Benutzern zu gestatten, die Verbindung zum Server über ein VPN herzustellen.  
  
7.  Klicken Sie auf **Übernehmen**, und klicken Sie anschließend auf **OK**.  
  
##  <a name="BKMK_Connect"></a> Verbinden Sie Clientcomputer mit dem server  
 Sobald VPN auf einem Server mit ausgeführten Windows Server Essentials für den Remotezugriff aktiviert ist, können Sie eine VPN-Verbindung verwenden, um eine Verbindung mit allen auf dem Server gespeicherten Ressourcen herzustellen und darauf zuzugreifen. Zuvor müssen Sie jedoch den Computer mit dem Server verbinden. Wenn Sie den Computer mithilfe des entsprechenden Assistenten mit dem Server verbinden, wird auf dem Clientcomputer automatisch eine VPN-Netzwerkverbindung erstellt, die zuhause oder unterwegs für den Zugriff auf Serverressourcen verwendet werden kann. Schrittweise Anweisungen zum Verbinden Ihres Computers mit dem Server finden Sie unter [Connect computers to the server](../use/Get-Connected-in-Windows-Server-Essentials.md#BKMK_9).  
  
##  <a name="BKMK_3"></a> Verwenden Sie-VPN-Verbindung mit Windows Server Essentials  
 Angenommen, Sie verfügen über einen Clientcomputer, der mit Netzwerkkonten eingerichtet wurde, über die mithilfe eines VPNs eine Verbindung mit einem gehosteten Server unter Windows Server Essentials hergestellt werden kann. In diesem Fall müssen alle neu erstellten Benutzerkonten auf dem gehosteten Server ein VPN verwenden, wenn sie sich erstmalig beim Clientcomputer anmelden. Führen Sie das folgende Verfahren auf dem Clientcomputer aus, der mit dem Server verbunden ist.  
  
#### <a name="to-use-vpn-to-remotely-access-server-resources"></a>So verwenden Sie ein VPN für den Remotezugriff auf Serverressourcen  
  
1.  Drücken Sie auf dem Clientcomputer STRG+ALT+ENTF.  
  
2.  Klicken Sie auf dem Anmeldebildschirm auf **Benutzer wechseln**.  
  
3.  Klicken Sie unten rechts auf dem Bildschirm auf das Symbol für die Netzwerkanmeldung.  
  
4.  Melden Sie sich mit Ihrem Netzwerk-Benutzernamen und -Kennwort beim Windows Server Essentials-Netzwerk an.  
  
## <a name="see-also"></a>Siehe auch  
  
-   [Arbeiten im Remotemodus](../use/Work-Remotely-in-Windows-Server-Essentials.md)  
  
-   [Verwalten von Zugriff überall](Manage-Anywhere-Access-in-Windows-Server-Essentials.md)  
  
-   [Verwalten von Windows Server Essentials](Manage-Windows-Server-Essentials.md)
