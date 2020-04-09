---
ms.assetid: 14aa112d-ae31-4181-97e4-92623b5c9270
title: Überprüfen der Rolle des Verbundserverproxys beim Ressourcenpartner
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 6f49677df16cb1b44d08449a3983ae29fed3cb27
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80858543"
---
# <a name="review-the-role-of-the-federation-server-proxy-in-the-resource-partner"></a>Überprüfen der Rolle des Verbundserverproxys beim Ressourcenpartner

Ein Verbund Server Proxy in Active Directory-Verbunddienste (AD FS) \(AD FS\) kann in einer oder mehreren der folgenden Rollen funktionieren, je nachdem, wie Sie den Server zum erfüllen der Anforderungen der Ressourcen Partnerorganisation konfigurieren:  
  
-   **Ermittlung von Kontopartnern**: Ein Internetclientcomputer muss bestimmen, welcher Kontopartner ihn authentifiziert. Der Client findet den Konto Partner mithilfe eines Webformulars für die Konto Partner Ermittlung \(discoverclientrealm. aspx\), das auf dem Verbund Server Proxy im Ressourcen Partner gespeichert ist. Wenn mehr als ein Konto Partner im AD FS Verwaltungs-Snap\-in konfiguriert ist, wird dem Client ein Dropdown\-Dropdown Menü mit allen verfügbaren Konto Partnern angezeigt, die für Internet Client Computer sichtbar sind, die auf das Webformular zum Ermitteln von Konto Partnern zugreifen. Sie können ändern, wie das Webformular zum Ermitteln von Kontopartnern auf Clientcomputern dargestellt wird, indem Sie die Datei "discoverclientrealm.aspx" bearbeiten.  
  
-   **Umleitung von Sicherheits Token**: der Verbund Server Proxy im Konto Partner sendet die Sicherheits Token an den Ressourcen Partner. Der Ressourcen Verbund Server Proxy akzeptiert diese Token und übergibt sie an den Verbund Server im Ressourcen Partner. Der Ressourcen Verbund Server gibt dann ein Sicherheits Token aus, das an einen bestimmten ressourcenweb Server gebunden ist. Der Ressourcen Verbund Server Proxy leitet das Token dann an den Client um.  
  
Zusammenfassend ermöglicht ein Ressourcen Verbund Server Proxy den Verbund Anmeldevorgang durch Umleitung von Client Computern an einen Verbund Server, der die Clients authentifizieren kann. Ein Ressourcen Verbund Server Proxy fungiert auch als Proxy für Client Sicherheits Token für Ressourcen Verbund Server.  
  
> [!NOTE]  
> Wenn es notwendig ist, die Menge an Hardware und die Anzahl der erforderlichen Zertifikate zu verringern, kann sich der Verbund Server Proxy auf demselben Computer wie der Webserver befinden.  
  
## <a name="see-also"></a>Weitere Informationen
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)

