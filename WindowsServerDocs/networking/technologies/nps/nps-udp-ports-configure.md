---
title: Konfigurieren von NPS-UDP-Portinformationen
description: Sie können in diesem Thema verwenden, Konfigurieren der Ports, die Windows-Verwaltungsinstrumentation (Network Policy Server, NPS) für die Remote Authentication Dial-in User Service (RADIUS)-Authentifizierung und Kontoführungsdatenverkehr unter Windows Server 2016 verwendet.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 70569958-d7a7-474e-a817-6b7b5134784a
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 44c20092180c47e97f1505271203f4491606bbcf
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59851971"
---
# <a name="configure-nps-udp-port-information"></a>Konfigurieren von NPS-UDP-Portinformationen

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Sie können das folgende Verfahren zum Konfigurieren der Ports, für die Remote Authentication Dial-in User Service (Network Policy Server, NPS) verwendet \(RADIUS\) Authentifizierung und Kontoführung.

Standardmäßig überwacht NPS RADIUS-Datenverkehr an Ports 1812, 1813, 1645 und 1646 für Internetprotokoll Version 6 \(IPv6\) und IPv4 für alle installierten Netzwerkadapter.

>[!NOTE]
>Wenn Sie auf einem Netzwerkadapter entweder IPv4 oder IPv6 deinstallieren, überwacht NPS RADIUS-Datenverkehr für das-Protokoll nicht.

Die Werte des Ports 1812, für die Authentifizierung und 1813 für die Kontoführung werden RADIUS-Standardports, die von der Internet Engineering Task Force definiert \(IETF\) in den RFCs 2865 und 2866. Allerdings verwenden viele Access-Server standardmäßig Port 1645 für authentifizierungsanforderungen und 1646 für kontoführungsanforderungen. Unabhängig davon, welche Portnummern, die Sie verwenden möchten, sicher, dass NPS und Ihre Access-Server konfiguriert sind, um dieselben diejenigen zu verwenden.

>[WICHTIG] Wenn Sie nicht die Standardportnummern für die RADIUS-verwenden, müssen Sie Ausnahmen in der Firewall für den lokalen Computer zum Zulassen von RADIUS-Datenverkehr auf die neuen Ports konfigurieren. Weitere Informationen finden Sie unter [Konfigurieren von Firewalls für RADIUS-Verkehr](nps-firewalls-configure.md).

Grundvoraussetzung für die Ausführung dieses Vorgangs ist die Mitgliedschaft in **Domänen-Admins** oder einer gleichwertigen Gruppe.

## <a name="to-configure-nps-udp-port-information"></a>Zum Konfigurieren von NPS UDP-Port-Informationen 

1. Öffnen Sie die NPS-Konsole.
2. Klicken Sie mit der rechten Maustaste auf **Netzwerkrichtlinienserver**, und klicken Sie dann auf **Eigenschaften**.
3. Klicken Sie auf die **Ports** Registerkarte, und betrachten Sie die Einstellungen für Ports. Wenn Ihre RADIUS-Authentifizierung und die RADIUS-Kontoführung UDP-Ports von den Standardwerten bereitgestellt (1812 und 1645 für die Authentifizierung und 1813 und 1646 für die Kontoführung) variieren möchten, geben Sie die Porteinstellungen in **Authentifizierung** und  **Accounting**.
4. Um mehrere Porteinstellungen für die Authentifizierung oder kontoführungsanforderungen verwenden möchten, trennen Sie die Portnummern durch Kommas.

Weitere Informationen zum Verwalten von NPS finden Sie unter [Verwalten des Netzwerkrichtlinienservers](nps-manage-top.md).

Weitere Informationen zu NPS finden Sie unter [(Network Policy Server, NPS)](nps-top.md).
