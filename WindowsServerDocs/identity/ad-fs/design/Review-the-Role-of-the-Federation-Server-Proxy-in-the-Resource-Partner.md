---
ms.assetid: 14aa112d-ae31-4181-97e4-92623b5c9270
title: Überprüfen der Rolle des Verbundserverproxys beim Ressourcenpartner
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: df9e291d85ea8899d7f546956276c60582893fe8
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71359045"
---
# <a name="review-the-role-of-the-federation-server-proxy-in-the-resource-partner"></a>Überprüfen der Rolle des Verbundserverproxys beim Ressourcenpartner

Ein Verbund Server Proxy in Active Directory-Verbunddienste (AD FS) \(ad FS @ no__t-1 kann in einer oder mehreren der folgenden Rollen funktionieren, je nachdem, wie Sie den Server so konfigurieren, dass er die Anforderungen der Ressourcen Partnerorganisation erfüllt:  
  
-   **Konto Partner**Ermittlung: Ein Internet Client Computer muss bestimmen, welcher Konto Partner ihn authentifiziert. Der Client findet den Konto Partner mithilfe eines Webformulars für die Konto Partner Ermittlung @no__t -0discoverclientrealm. aspx @ no__t-1, der auf dem Verbund Server Proxy im Ressourcen Partner gespeichert ist. Wenn mehr als ein Konto Partner im AD FS Management-Snap @ no__t-0in konfiguriert ist, wird dem Client ein Drop @ no__t-1down-Menü mit allen verfügbaren Konto Partnern angezeigt, die für Internet Client Computer sichtbar sind, die auf das Web der Konto Partner Ermittlung zugreifen. gehören. Sie können ändern, wie das Webformular zum Ermitteln von Kontopartnern auf Clientcomputern dargestellt wird, indem Sie die Datei "discoverclientrealm.aspx" bearbeiten.  
  
-   **Umleitung von Sicherheits Token**: Der Verbund Server Proxy im Konto Partner sendet die Sicherheits Token an den Ressourcen Partner. Der Ressourcen Verbund Server Proxy akzeptiert diese Token und übergibt sie an den Verbund Server im Ressourcen Partner. Der Ressourcen Verbund Server gibt dann ein Sicherheits Token aus, das an einen bestimmten ressourcenweb Server gebunden ist. Der Ressourcen Verbund Server Proxy leitet das Token dann an den Client um.  
  
Zusammenfassend ermöglicht ein Ressourcen Verbund Server Proxy den Verbund Anmeldevorgang durch Umleitung von Client Computern an einen Verbund Server, der die Clients authentifizieren kann. Ein Ressourcen Verbund Server Proxy fungiert auch als Proxy für Client Sicherheits Token für Ressourcen Verbund Server.  
  
> [!NOTE]  
> Wenn es notwendig ist, die Menge an Hardware und die Anzahl der erforderlichen Zertifikate zu verringern, kann sich der Verbund Server Proxy auf demselben Computer wie der Webserver befinden.  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)

