---
ms.assetid: 14aa112d-ae31-4181-97e4-92623b5c9270
title: Überprüfen der Rolle des Verbundserverproxys beim Ressourcenpartner
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 377baa8f282f3886284a53b686944fe145b1b15e
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66190887"
---
# <a name="review-the-role-of-the-federation-server-proxy-in-the-resource-partner"></a>Überprüfen der Rolle des Verbundserverproxys beim Ressourcenpartner

Eines Verbundserverproxys in Active Directory-Verbunddienste \(AD FS\) -Funktion in eine oder mehrere der folgenden Rollen, je nachdem, wie Sie den Server, um die Anforderungen der Ressourcenpartnerorganisation konfigurieren können:  
  
-   **Ermittlung von Kontopartnern**: Ein internetclientcomputer muss bestimmen, welcher Kontopartner ihn authentifiziert wird. Der Client findet den Kontopartner mithilfe eines Discovery-Webformular \(discoverclientrealm.aspx\), die auf des Verbundserverproxys beim Ressourcenpartner gespeichert ist. Wenn mehr als ein Kontopartner konfiguriert ist im AD FS-Verwaltungs-Snap-\-in einem Dropdown\--Menü angezeigt wird, an den Client mit allen verfügbaren Kontopartnern, die für internetclientcomputer sichtbar sind, die den Kontopartner zugreifen Webformular zum ermitteln. Sie können ändern, wie das Webformular zum Ermitteln von Kontopartnern auf Clientcomputern dargestellt wird, indem Sie die Datei "discoverclientrealm.aspx" bearbeiten.  
  
-   **Umleitung von Sicherheitstoken**: Des Verbundserverproxys beim Kontopartner sendet die Sicherheitstoken an den Ressourcenpartner. Der Verbundserverproxy für die Ressource akzeptiert diese Token und übergibt sie an der Verbundserver in der Ressourcenpartnerorganisation. Der Ressourcenverbundserver klicken Sie dann Sicherheitstoken ein, das für einen bestimmten Webserver gebunden ist. Der Verbundserverproxy für die Ressource leitet dann das Token wird an den Client.  
  
Zusammenfassend lässt sich sagen, erleichtert ein Ressourcen-Verbundserverproxys den verbundanmeldevorgang durch das Umleiten von Clientcomputern bei einem Verbundserver, der die Clients authentifizieren können. Verbundserverproxys für eine Ressource fungiert außerdem als Proxy für Client-Sicherheitstoken für Ressourcenverbundserver.  
  
> [!NOTE]  
> Wenn es erforderlich, um die Menge an Hardware und die Anzahl der erforderlichen Zertifikate zu reduzieren, kann der Verbundserverproxy auf dem gleichen Computer wie der Webserver befinden.  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)

