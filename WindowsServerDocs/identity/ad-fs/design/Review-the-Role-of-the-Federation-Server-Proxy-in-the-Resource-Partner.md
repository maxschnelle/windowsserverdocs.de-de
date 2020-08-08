---
ms.assetid: 14aa112d-ae31-4181-97e4-92623b5c9270
title: Überprüfen der Rolle des Verbundserverproxys beim Ressourcenpartner
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: b431d14abfa66ceb70e5885b4301648936c4c4ff
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87969687"
---
# <a name="review-the-role-of-the-federation-server-proxy-in-the-resource-partner"></a>Überprüfen der Rolle des Verbundserverproxys beim Ressourcenpartner

Ein Verbund Server Proxy in Active Directory-Verbunddienste (AD FS) \( AD FS \) kann in Abhängigkeit von der Konfiguration des Servers zum erfüllen der Anforderungen der Ressourcen Partnerorganisation eine oder mehrere der folgenden Rollen erfüllen:

-   **Ermittlung von Kontopartnern**: Ein Internetclientcomputer muss bestimmen, welcher Kontopartner ihn authentifiziert. Der Client findet den Konto Partner mithilfe eines Webformulars " \( discoverclientrealm. aspx" der Konto Partner Ermittlung \) , das auf dem Verbund Server Proxy im Ressourcen Partner gespeichert ist. Wenn im Snap-in AD FS Verwaltung mehr als ein Konto Partner konfiguriert ist \- , wird \- dem Client ein Dropdown Menü mit allen verfügbaren Konto Partnern angezeigt, die für Internet Client Computer sichtbar sind, die auf das Webformular zum Ermitteln von Konto Partnern zugreifen. Sie können ändern, wie das Webformular zum Ermitteln von Kontopartnern auf Clientcomputern dargestellt wird, indem Sie die Datei "discoverclientrealm.aspx" bearbeiten.

-   **Umleitung von Sicherheits Token**: der Verbund Server Proxy im Konto Partner sendet die Sicherheits Token an den Ressourcen Partner. Der Ressourcen Verbund Server Proxy akzeptiert diese Token und übergibt sie an den Verbund Server im Ressourcen Partner. Der Ressourcen Verbund Server gibt dann ein Sicherheits Token aus, das an einen bestimmten ressourcenweb Server gebunden ist. Der Ressourcen Verbund Server Proxy leitet das Token dann an den Client um.

Zusammenfassend ermöglicht ein Ressourcen Verbund Server Proxy den Verbund Anmeldevorgang durch Umleitung von Client Computern an einen Verbund Server, der die Clients authentifizieren kann. Ein Ressourcen Verbund Server Proxy fungiert auch als Proxy für Client Sicherheits Token für Ressourcen Verbund Server.

> [!NOTE]
> Wenn es notwendig ist, die Menge an Hardware und die Anzahl der erforderlichen Zertifikate zu verringern, kann sich der Verbund Server Proxy auf demselben Computer wie der Webserver befinden.

## <a name="see-also"></a>Weitere Informationen
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)

