---
ms.assetid: 14aa112d-ae31-4181-97e4-92623b5c9270
title: Review the Role of the Federation Serverproxy in the Resource Partner
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 31e285e863e4316a8e0a65f9b68c27442290927d
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="review-the-role-of-the-federation-server-proxy-in-the-resource-partner"></a>Review the Role of the Federation Serverproxy in the Resource Partner

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Ein Verbundserverproxy in Active Directory Federation Services \(AD FS\) kann eine oder mehrere der folgenden Rollen, je nach des Servers Konfiguration, damit die Bedürfnisse der Ressourcenpartnerorganisation fungieren:  
  
-   **Ermittlung von Kontopartnern**: ein internetclientcomputer muss ermitteln, welcher Kontopartner ihn authentifiziert wird. Der Client findet den Kontopartner mithilfe einer Konto Partner Discovery Web Form \(discoverclientrealm.aspx\), die auf des Verbundserverproxys beim Ressourcenpartner gespeichert ist. Wenn mehrere ist ein Kontopartner konfiguriert, in der AD FS-Snap-In, ein Drop\-Down-Menü an den Client mit allen verfügbaren Kontopartnern angezeigt wird, die für internetclientcomputer sichtbar sind, die die Ermittlung von Kontopartnern Webformular zugreifen. Sie können ändern, wie die Ermittlung von Kontopartnern Webformular auf Clientcomputern dargestellt wird, indem Sie die Datei discoverclientrealm.aspx anpassen.  
  
-   **Umleitung von Sicherheitstoken**: des Verbundserverproxys beim Kontopartner sendet die Sicherheitstoken an den Ressourcenpartner. Der Verbundserverproxy Ressource akzeptiert diese Token und übergibt sie an der Verbundserver in der Ressourcenpartnerorganisation. Der Ressourcenverbundserver dann Sicherheitstoken ein, die für eine bestimmte Ressource Webserver gebunden ist. Der Ressourcenverbundserver-Proxy leitet dann das Token an den Client.  
  
Zusammenfassend lässt sich sagen, erleichtert ein Verbundserverproxys Ressource federated Anmeldeprozess durch die Umleitung von Clientcomputern an einem Verbundserver, der die Clients authentifizieren kann. Verbundserverproxys für eine Ressource fungiert außerdem als Proxy für clientsicherheitstoken für Ressourcenverbundserver.  
  
> [!NOTE]  
> Wenn es zum Verringern der Menge an Hardware und die Anzahl der erforderlichen Zertifikate erforderlich ist, kann der Verbundserverproxy auf demselben Computer wie der Webserver befinden.  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)

