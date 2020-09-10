---
title: Remote-Arbeit in Windows Server Essentials
description: Beschreibt die Verwendung von Windows Server Essentials
ms.date: 10/03/2016
ms.topic: article
ms.assetid: 8b183f8f-1279-4fdf-a495-c7c801563cb0
author: nnamuhcs
ms.author: geschuma
manager: mtillman
ms.openlocfilehash: 955b7e028b774699bc5170bda1fac29b88a35483
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89624854"
---
# <a name="work-remotely-in-windows-server-essentials"></a>Remote-Arbeit in Windows Server Essentials

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

 Wenn Sie sich nicht in Reichweite Ihres Netzwerks befinden, haben Sie mehrere Möglichkeiten, auf die auf dem Server gespeicherten Ressourcen zuzugreifen. Voraussetzung dafür ist, dass "Zugriff überall"-Funktionen (wie Remotewebzugriff, virtuelles privates Netzwerk und DirectAccess) auf dem Server konfiguriert sind

 In den folgenden Themen wird der Remotezugriff auf Serverressourcen erläutert:


-   [Verwenden des Remotewebzugriffs in Windows Server 2012 Essentials](Work-Remotely-in-Windows-Server-Essentials.md#BKMA_RWA)

-   [Verwenden von VPN für die Verbindung mit Windows Server Essentials](Work-Remotely-in-Windows-Server-Essentials.md#BKMK_3)

-   [Verwenden der My Server-App zum Herstellen einer Verbindung mit Windows Server Essentials](Work-Remotely-in-Windows-Server-Essentials.md#BKMK_App)

-   [Verwenden der My Server-App für Windows Phone](Work-Remotely-in-Windows-Server-Essentials.md#BKMK_2)

-   [Verwenden von Microsoft 365 mit Windows Server Essentials](Work-Remotely-in-Windows-Server-Essentials.md#BKMK_O365)

> [!NOTE]
>  Weitere Informationen zum Konfigurieren von "Zugriff überall" auf dem Server finden Sie unter Verwalten von " [Zugriff überall](../manage/Manage-Anywhere-Access-in-Windows-Server-Essentials.md)".

##  <a name="use-remote-web-access-in-windows-server-essentials"></a><a name="BKMA_RWA"></a> Verwenden von Remote Webzugriff in Windows Server Essentials

 Remotewebzugriff bietet die Möglichkeit, auch unterwegs mit dem Windows Server Essentials-Netzwerk in Verbindung zu bleiben. Weitere Informationen finden Sie im Thema [Verwenden von Remote Webzugriff](Use-Remote-Web-Access-in-Windows-Server-Essentials.md).


##  <a name="use-vpn-to-connect-to-windows-server-essentials"></a><a name="BKMK_3"></a> Herstellen einer Verbindung mit Windows Server Essentials mithilfe von VPN
 Angenommen, Sie verfügen über einen Clientcomputer, der mit Netzwerkkonten eingerichtet wurde, über die mithilfe eines VPNs eine Verbindung mit einem gehosteten Server unter Windows Server Essentials hergestellt werden kann. In diesem Fall müssen alle neu erstellten Benutzerkonten auf dem gehosteten Server ein VPN verwenden, wenn sie sich erstmalig beim Clientcomputer anmelden. Führen Sie das folgende Verfahren auf dem Clientcomputer aus, der mit dem Server verbunden ist.

#### <a name="to-use-vpn-to-remotely-access-server-resources"></a>So verwenden Sie ein VPN für den Remotezugriff auf Serverressourcen

1.  Drücken Sie auf dem Clientcomputer STRG+ALT+ENTF.

2.  Klicken Sie auf dem Anmeldebildschirm auf **Benutzer wechseln**.

3.  Klicken Sie unten rechts auf dem Bildschirm auf das Symbol für die Netzwerkanmeldung.

4.  Melden Sie sich mit Ihrem Netzwerk-Benutzernamen und -Kennwort beim Windows Server Essentials-Netzwerk an.

##  <a name="use-the-my-server-app-to-connect-to-windows-server-essentials"></a><a name="BKMK_App"></a> Verwenden der My Server-App zum Herstellen einer Verbindung mit Windows Server Essentials
 Mithilfe der My Server-App können Sie von Ihrem Windows-basierten PC, Laptop oder Surface-Gerät eine Verbindung mit Ressourcen herstellen und einfache administrative Aufgaben auf Ihrem Windows Server Essentials-Server ausführen. Wenn auf Ihrem Server Windows Server 2012 ausgeführt wird, laden Sie die My Server-Original-APP von [Apps für Windows](https://windows.microsoft.com/windows-8/apps)herunter. Wenn auf Ihrem Server Windows Server Essentials ausgeführt wird, müssen Sie stattdessen die My Server 2012 R2-app herunterladen.

 Sie können die erweiterte My Server 2012 R2-App nutzen, um mithilfe von Remotedesktop eine Verbindung mit Server- oder Clientcomputern herzustellen. Wenn Ihr Windows Server Essentials-Server in Microsoft 365 integriert ist und Ihr Abonnement SharePoint Online umfasst, können Sie auch mit Dokumenten in Ihren SharePoint Online-Bibliotheken arbeiten und die SharePoint-Team Websites über My Server 2012 R2 öffnen.


 Weitere Informationen zum Installieren und Verwenden dieser apps finden Sie unter [Verwenden der My Server-App](Use-the-My-Server-App-to-Connect-to-Windows-Server-Essentials.md).

 Weitere Informationen zum Installieren und Verwenden dieser apps finden Sie unter [Verwenden der My Server-App](../use/Use-the-My-Server-App-to-Connect-to-Windows-Server-Essentials.md).


##  <a name="use-the-my-server-app-for-windows-phone"></a><a name="BKMK_2"></a> Verwenden der My Server-App für Windows Phone
 Die Windows-App My Server für Windows Phone (für Windows Server 2012) und die My Server 2012 R2-App für Windows Phone (für Windows Server Essentials) sind so konzipiert, dass Sie bei der Arbeit an Remote Standorten nahtlos mit ihren Servern in Verbindung bleiben können. Dies ist eine der verschiedenen Möglichkeiten, auf Windows Server Essentials zuzugreifen, nachdem Sie den Server für den Remote Zugriff konfiguriert haben.

 Sie können beide Apps aus dem Windows Phone Store herunterladen:

- [Installieren von My Server für Windows Phone](http://www.windowsphone.com/store/app/my-server/6c2f98d5-6fcf-4e1d-b8b1-cde62ea1a94a)

- [Installieren von My Server 2012 R2 für Windows Phone](http://www.windowsphone.com/store/app/my-server-2012-r2/44f596b5-0477-4096-b96e-ddd6ef64ad6b)

  Weitere Informationen zur My Server-Phone-App finden Sie im Blogbeitrag [My Server Phone App for Windows Server Essentials](/archive/blogs/sbs/my-server-phone-app-for-windows-server-2012-essentials). Informationen zur Windows Phone-App "My Server 2012 R2" finden Sie im Blogbeitrag [My Server 2012 R2 Windows and Windows Phone apps](/archive/blogs/sbs/my-server-2012-r2-windows-and-windows-phone-apps).

##  <a name="use-microsoft-365-with-windows-server-essentials"></a><a name="BKMK_O365"></a> Verwenden von Microsoft 365 mit Windows Server Essentials

 Microsoft 365 ist ein benutzerfreundliches webfähiges Toolset, mit dem Sie von nahezu überall und von jedem Gerät aus auf e-Mails, wichtige Dokumente, Kontakte und Kalender zugreifen können. Weitere Informationen finden [Sie unter Schnellstarthandbuch to using Microsoft 365](Quick-Start-Guide-to-Using-Microsoft-Office-365-with-Windows-Server-Essentials.md).


## <a name="see-also"></a>Weitere Informationen

-   [Verwalten von %%amp;quot;Zugriff überall%%amp;quot;](../manage/Manage-Anywhere-Access-in-Windows-Server-Essentials.md)

-   [Verbindung herstellen](Get-Connected-in-Windows-Server-Essentials.md)

-   [Verwenden von freigegebenen Ordnern](Use-Shared-Folders-in-Windows-Server-Essentials.md)

-   [Wiedergeben von digitalen Medien](Play-Digital-Media-in-Windows-Server-Essentials.md)