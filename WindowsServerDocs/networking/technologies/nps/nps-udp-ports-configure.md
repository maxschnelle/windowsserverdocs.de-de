---
title: Konfigurieren von NPS-UDP-Portinformationen
description: Sie können dieses Thema verwenden, um die Ports zu konfigurieren, die vom Netzwerk Richtlinien Server (Network Policy Server, NPS) für die Remote Authentication Dial-in User Service-und Buchhaltungsdaten Verkehr in Windows Server 2016 verwendet werden.
manager: brianlic
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 70569958-d7a7-474e-a817-6b7b5134784a
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 1ba6c059639b9ae7e77a9e103e7ed84f6a2032df
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405310"
---
# <a name="configure-nps-udp-port-information"></a>Konfigurieren von NPS-UDP-Portinformationen

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Mithilfe des folgenden Verfahrens können Sie die Ports konfigurieren, die vom Netzwerk Richtlinien Server (Network Policy Server, NPS) für Remote Authentication Dial-in User Service @no__t-Authentifizierungs-und Kontoführungs Datenverkehr verwendet werden.

Standardmäßig überwacht NPS den RADIUS-Datenverkehr über die Ports 1812, 1813, 1645 und 1646 sowohl für die Internet Protokollversion 6 \(ipv6 @ no__t-1 als auch für IPv4 für alle installierten Netzwerkadapter.

>[!NOTE]
>Wenn Sie IPv4 oder IPv6 auf einem Netzwerkadapter deinstallieren, überwacht NPS nicht den RADIUS-Datenverkehr für das nicht installierte Protokoll.

Die Port Werte 1812 für die Authentifizierung und 1813 für die Abrechnung sind RADIUS-Standardports, die durch die Internet Engineering Task Force \(ietf @ no__t-1 in RFCs 2865 und 2866 definiert werden. Allerdings verwenden viele Zugriffs Server standardmäßig die Ports 1645 für Authentifizierungsanforderungen und 1646 für Buchhaltungs Anforderungen. Unabhängig davon, welche Portnummern Sie verwenden möchten, müssen Sie sicherstellen, dass NPS und Ihr Zugriffs Server für die Verwendung derselben konfiguriert sind.

>Wichtig Wenn Sie die RADIUS-Standard Portnummern nicht verwenden, müssen Sie Ausnahmen in der Firewall für den lokalen Computer konfigurieren, um RADIUS-Datenverkehr für die neuen Ports zuzulassen. Weitere Informationen finden Sie unter [Konfigurieren von Firewalls für RADIUS-Datenverkehr](nps-firewalls-configure.md).

Grundvoraussetzung für die Ausführung dieses Vorgangs ist die Mitgliedschaft in **Domänen-Admins** oder einer gleichwertigen Gruppe.

## <a name="to-configure-nps-udp-port-information"></a>So konfigurieren Sie die NPS-UDP-Port Informationen 

1. Öffnen Sie die NPS-Konsole.
2. Klicken Sie mit der rechten Maustaste auf **Netzwerkrichtlinienserver**, und klicken Sie dann auf **Eigenschaften**.
3. Klicken Sie auf die Registerkarte **Ports** , und überprüfen Sie dann die Einstellungen für Ports. Wenn die UDP-Ports der RADIUS-Authentifizierung und der RADIUS-Buchhaltung von den bereitgestellten Standardwerten abweichen (1812 und 1645 für die Authentifizierung und 1813 und 1646 für die Kontoführung), geben Sie Ihre Port Einstellungen in **Authentifizierung** und Konto **Führung**ein.
4. Wenn Sie mehrere Port Einstellungen für Authentifizierungs-oder Buchhaltungs Anforderungen verwenden möchten, trennen Sie die Portnummern durch Kommas.

Weitere Informationen zum Verwalten von NPS finden Sie unter [Verwalten des Netzwerk Richtlinien Servers](nps-manage-top.md).

Weitere Informationen zu NPS finden Sie unter [Netzwerk Richtlinien Server (Network Policy Server, NPS)](nps-top.md).
