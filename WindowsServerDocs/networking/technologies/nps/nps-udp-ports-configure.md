---
title: Konfigurieren von NPS-UDP-Portinformationen
description: In diesem Thema können Sie die Ports konfigurieren, die für die Remote Authentication Dial-in User Service (RADIUS)-Authentifizierung und -Kontoführung Datenverkehr in Windows Server2016 (Network Policy Server, NPS) verwendet.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 70569958-d7a7-474e-a817-6b7b5134784a
ms.author: pashort
author: shortpatti
ms.openlocfilehash: f0e703dc6f9083f1e79091a6cee6d1ac58753d12
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="configure-nps-udp-port-information"></a>Konfigurieren von NPS-UDP-Portinformationen

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Das folgende Verfahren können zum Konfigurieren der Ports, die für die Remote Authentication Dial-in User Service \(RADIUS\) Authentifizierung und -Kontoführung Datenverkehr (Network Policy Server, NPS) verwendet.

Standardmäßig überwacht NPS RADIUS-Datenverkehr auf den Ports 1812, 1813, 1645 und 1646 für sowohl IPv4 als auch Internet Protocol Version 6 \(IPv6\) für alle installierten Netzwerkadapter.

>[!NOTE]
>Wenn Sie auf einem Netzwerkadapter entweder IPv4 oder IPv6 deinstallieren, überwacht NPS RADIUS-Datenverkehr für das deinstallierte Protokoll nicht.

Die Werte Ports 1812 für die Authentifizierung und 1813 für die Kontoführung handelt es sich um RADIUS-Standardports, die von der Internet Engineering Task Force \(IETF\) in RFC 2865 und 2866 definiert. Standardmäßig verwenden viele Server Ports für Authentifizierungsanfragen 1645 und 1646 zur Kontoführung. Unabhängig davon, welche Portnummern, die Sie verwenden möchten, stellen Sie sicher, dass NPS und RAS-Servers für die gleichen Ports konfiguriert sind.

>[WICHTIGE] Wenn Sie nicht die Standardportnummern RADIUS verwenden, müssen Sie Ausnahmen in der Firewall für den lokalen Computer zum Zulassen von RADIUS-Datenverkehr über die neuen Ports konfigurieren. Weitere Informationen finden Sie unter [Konfigurieren von Firewalls für RADIUS-Datenverkehr](nps-firewalls-configure.md).

Mitgliedschaft in **Domänen-Admins**, oder einer gleichwertigen Gruppe ist mindestens erforderlich, um dieses Verfahren ausführen.

## <a name="to-configure-nps-udp-port-information"></a>So konfigurieren Sie NPS UDP-Portinformationen 

1. Öffnen Sie die NPS-Konsole.
2. Mit der rechten Maustaste **Netzwerkrichtlinienserver**, und klicken Sie dann auf **Eigenschaften**.
3. Klicken Sie auf die **Ports** Registerkarte, und überprüfen Sie die Einstellungen für Ports. Wenn Ihre RADIUS-Authentifizierung und RADIUS-Kontoführung UDP-Ports von bereitgestellten Standardwerte (1812 und 1645 für die Authentifizierung und 1813 und 1646 für die Kontoführung) variieren, geben Sie die Porteinstellungen in **Authentifizierung** und **Accounting**.
4. Um mehrere Porteinstellungen für die Authentifizierung oder Kontoführung verwenden möchten, trennen Sie die Portnummern durch Kommas.

Weitere Informationen zum Verwalten von NPS finden Sie unter [Netzwerkrichtlinienserver verwalten](nps-manage-top.md).

Weitere Informationen zu NPS finden Sie unter [(Network Policy Server, NPS)](nps-top.md).
