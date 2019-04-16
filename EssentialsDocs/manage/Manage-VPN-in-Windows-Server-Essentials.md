---
title: Verwalten des VPN in Windows Server Essentials
description: Beschreibt, wie Sie Windows Server Essentials
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
ms.openlocfilehash: 08a08a13d696371420bdfdf89f54320c787636b0
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="manage-vpn-in-windows-server-essentials"></a>Verwalten des VPN in Windows Server Essentials

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials 
  
 Verbindungen virtuelles privates Netzwerk (VPN) ermöglichen es Benutzern zu Hause oder unterwegs auf einem Server in einem privaten Netzwerk mithilfe von einem öffentlichen Netzwerk, z. B. dem Internet bereitgestellte Infrastruktur nutzen. Zur Verwendung von VPN für den Zugriff auf Serverressourcen müssen Sie folgende Schritte ausführen:  
  
-   [Aktivieren von VPN für den Remotezugriff auf dem server](Manage-VPN-in-Windows-Server-Essentials.md#BKMK_1)  
  
-   [Festlegen von VPN-Berechtigungen für Netzwerkbenutzer](Manage-VPN-in-Windows-Server-Essentials.md#BKMK_2)  
  
-   [Verbinden Sie Clientcomputer mit dem server](Manage-VPN-in-Windows-Server-Essentials.md#BKMK_Connect)  
  
-   [Verwenden Sie-VPN-Verbindung mit Windows Server Essentials](Manage-VPN-in-Windows-Server-Essentials.md#BKMK_3)  
  
##  <a name="BKMK_1"></a>Aktivieren von VPN für den Remotezugriff auf dem server  
 Führen Sie das folgende Verfahren zum Konfigurieren von VPN in Windows Server Essentials zu aktivieren.  
  
#### <a name="to-enable-vpn-in-windows-server-essentials"></a>So aktivieren Sie VPN in Windows Server Essentials  
  
1.  Öffnen Sie das Dashboard.  
  
2.  Klicken Sie auf **Einstellungen**, und klicken Sie dann auf die **"Zugriff überall"** Registerkarte.  
  
3.  Klicken Sie auf **konfigurieren**. Der überall Zugriff-Assistent wird angezeigt.  
  
4.  Auf der **Funktionen für Zugriff überall aktivieren** Seite auf die **virtuelles privates Netzwerk** Kontrollkästchen.  
  
5.  Führen Sie die Anweisungen, um den Assistenten abzuschließen.  
  
##  <a name="BKMK_2"></a>Festlegen von VPN-Berechtigungen für Netzwerkbenutzer  
 Sie können VPN zum Verbinden mit Windows Server Essentials und Zugriff auf alle Ressourcen, die auf dem Server gespeichert sind. Dies ist besonders hilfreich, wenn Sie einen Clientcomputer verfügen, der mit Netzwerkkonten eingerichtet ist, die für die Verbindung mit einem gehosteten Windows Server Essentials-Server über eine VPN-Verbindung verwendet werden können. Alle neu erstellten Benutzerkonten auf dem gehosteten Windows Server Essentials-Server müssen auf dem Client-Computer zum ersten Mal anmelden VPN verwenden.  
  
#### <a name="to-set-vpn-permissions-for-network-users"></a>VPN-Berechtigungen für Netzwerkbenutzer fest  
  
1.  Öffnen Sie das Dashboard.  
  
2.  Klicken Sie auf der Navigationsleiste auf **Benutzer**.  
  
3.  Wählen Sie in der Liste der Benutzerkonten das Benutzerkonto, dem Sie Berechtigungen für Remotezugriff auf den Desktop gewähren möchten.  
  
4.  In der **< Benutzer Zuordnung überprüfen\ > Aufgaben** Bereich, klicken Sie auf **Eigenschaften**.  
  
5.  In der **< Benutzer Zuordnung überprüfen\ > Eigenschaften**, klicken Sie auf die **"Zugriff überall"** Registerkarte.  
  
6.  Auf der **"Zugriff überall"** Tab, um einem Benutzer ermöglichen, mit dem Server verbinden, über ein VPN, wählen Sie die **virtuellen privaten Netzwerk (VPN) zulassen** Kontrollkästchen.  
  
7.  Klicken Sie auf **übernehmen**, und klicken Sie dann auf **OK**.  
  
##  <a name="BKMK_Connect"></a>Verbinden Sie Clientcomputer mit dem server  
 Nachdem Sie auf einem Server unter Windows Server Essentials für den Remotezugriff auf VPN aktiviert ist, können Sie eine VPN-Verbindung herstellen und Zugriff auf alle Ressourcen, die auf dem Server gespeichert sind. Allerdings müssen Sie zunächst den Computer mit dem Server verbinden. Wenn Sie einen Computer mit dem Server verbinden, über den Arbeitsplatz verbinden Assistenten, wird eine VPN-Netzwerkverbindung wird auf dem Clientcomputer automatisch generiert und kann verwendet werden, auf Serverressourcen zugreifen, während der Arbeit von zuhause oder unterwegs. Eine schrittweise Anleitung zum Verbinden Ihres Computers mit dem Server finden Sie unter [Verbinden von Computern mit dem Server](../use/Get-Connected-in-Windows-Server-Essentials.md#BKMK_9).  
  
##  <a name="BKMK_3"></a>Verwenden Sie-VPN-Verbindung mit Windows Server Essentials  
 Besitzen Sie einen Clientcomputer, der mit Netzwerkkonten eingerichtet ist, die verwendet werden können, für die Verbindung mit einem gehosteten Server unter Windows Server Essentials über eine VPN-Verbindung, die neu erstellten Benutzerkonten muss der gehostete Server VPN verwenden, für den Client zum ersten Mal anmelden. Führen Sie das folgende Verfahren auf dem Clientcomputer, der mit dem Server verbunden ist.  
  
#### <a name="to-use-vpn-to-remotely-access-server-resources"></a>Mit diesen-VPN-Remotezugriff auf Serverressourcen  
  
1.  Drücken Sie Strg + Alt + ENTF auf dem Clientcomputer.  
  
2.  Klicken Sie auf **Benutzer wechseln** auf dem Anmeldebildschirm.  
  
3.  Klicken Sie auf das Netzwerksymbol für die Anmeldung auf der unteren rechten Ecke des Bildschirms.  
  
4.  Melden Sie sich mit dem Windows Server Essentials-Netzwerk mit Ihrem Netzwerk-Benutzernamen und Kennwort.  
  
## <a name="see-also"></a>Siehe auch  
  
-   [Remote-Arbeit](../use/Work-Remotely-in-Windows-Server-Essentials.md)  
  
-   [Verwalten von Zugriff überall](Manage-Anywhere-Access-in-Windows-Server-Essentials.md)  
  
-   [Verwalten von Windows Server Essentials](Manage-Windows-Server-Essentials.md)
