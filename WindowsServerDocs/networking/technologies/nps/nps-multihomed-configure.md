---
title: Konfigurieren von NPS auf einem mehrfach vernetzten Computer
description: Dieses Thema enthält Anweisungen zum Konfigurieren eines Servers mit mehreren Netzwerkadaptern, auf dem Network Policy Server unter Windows Server 2016 ausgeführt wird.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: d9d9e9ac-4859-4522-89ed-a23092c9e12a
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 55eccf3afc649e84c5b6f5ce7932ed97617ddca9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59856801"
---
# <a name="configure-nps-on-a-multihomed-computer"></a>Konfigurieren von NPS auf einem mehrfach vernetzten Computer

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Sie können in diesem Thema verwenden, um ein NPS mit mehreren Netzwerkkarten zu konfigurieren.

Wenn Sie mehrere Netzwerkadapter auf einem Server mit Windows-Verwaltungsinstrumentation (Network Policy Server, NPS) verwenden, können Sie Folgendes konfigurieren:

- Die Netzwerkadapter, die und nicht zu senden und Remote Authentication Dial-in User Service empfangen \(RADIUS\) Datenverkehr.
- Einzelne Adapter pro Netzwerk überwacht NPS, ob RADIUS-Datenverkehr auf Internetprotokoll Version 4 \(IPv4\), IPv6 oder IPv4 und IPv6.
- Die UDP-Portnummern, über welche RADIUS Datenverkehr gesendet und empfangen auf einer pro-Protokoll \(IPv4 oder IPv6\), pro-Network Adapter-Basis.

Standardmäßig überwacht NPS RADIUS-Datenverkehr an Ports 1812, 1813, 1645 und 1646 für IPv6 und IPv4 für alle installierten Netzwerkadapter. Da NPS RADIUS-Datenverkehr automatisch alle Netzwerkadapter verwendet, müssen Sie nur angeben, dass Datenverkehr die Netzwerkadaptern, die Sie NPS für RADIUS verwenden möchten, wenn Sie, um zu verhindern, dass NPS mit einem bestimmten Netzwerkadapter möchten.

>[!NOTE]
>Wenn Sie auf einem Netzwerkadapter entweder IPv4 oder IPv6 deinstallieren, überwacht NPS RADIUS-Datenverkehr für das-Protokoll nicht.

Für einen NPS, die mehrere Netzwerkadapter installiert ist, empfiehlt es sich zum Konfigurieren von NPS zum Senden und Empfangen von RADIUS-Verkehr nur auf den Adaptern, die Sie angeben.

Beispielsweise kann ein Netzwerkadapter installiert, die in der NPS auf einem Netzwerksegment führen, die zwar ein zweiter Netzwerkadapter mit einem Netzwerkpfad NPS konfigurierten RADIUS-Clients bietet keine RADIUS-Clients enthält. In diesem Szenario ist es wichtig, um NPS zu verwenden, die zweite Netzwerkkarte für den gesamten RADIUS-Datenverkehr weiterzuleiten.

Ein weiteres Beispiel können den NPS verfügt über drei Netzwerkadapter installiert, aber nur auf zwei Adapter für RADIUS-Datenverkehr verwenden soll Sie Portinformationen für nur die beiden Adapter konfigurieren. Durch Ausschließen Portkonfiguration für die dritte Karte, verhindern Sie NPS Verwenden des Adapters für RADIUS-Verkehr.

## <a name="using-a-network-adapter"></a>Mithilfe eines Netzwerkadapters

Verwenden Sie die folgende Syntax auf das Dialogfeld "Eigenschaften" des Network Policy Server in der NPS-Konsole, um NPS zum Lauschen auf und Senden von RADIUS-Datenverkehr auf einem Netzwerkadapter zu konfigurieren:

- Syntax von IPv4-Datenverkehr: IPAddress:UDPport, in dem IP-Adresse ist die IPv4-Adresse, die auf dem Netzwerkadapter konfiguriert ist, über die Sie die RADIUS-Verkehr senden möchten, und UDPport ist die RADIUS-Portnummer, die Sie für die RADIUS-Authentifizierung oder die Buchhaltung-Datenverkehr verwenden möchten.
- Syntax von IPv6-Datenverkehr: [IPv6Address]: UDPport, in denen die Klammern um IPv6Address sind erforderlich, IPv6Address ist die IPv6-Adresse, die auf dem Netzwerkadapter konfiguriert ist, über die Sie die RADIUS-Verkehr senden möchten, und UDPport ist die RADIUS-Portnummer, die Sie für die RADIUS-Authentifizierung verwenden möchten oder Accounting-Datenverkehr.

Die folgenden Zeichen als Trennzeichen dienen zum Konfigurieren von IP-Adresse und Portinformationen für UDP:

- Adresse und Anschluss, Trennzeichen: Doppelpunkt (:)
- Port-Trennzeichen: Komma (,)
- Schnittstelle Trennzeichen: Semikolon (;)

## <a name="configuring-network-access-servers"></a>Konfigurieren Netzwerkzugriffsserver

Stellen Sie sicher, dass Ihre Netzwerkzugriffsserver mit den gleichen RADIUS-UDP-Portnummern konfiguriert sind, die Sie für Ihre NPSs konfigurieren. Die RADIUS-standard UDP-Ports in den RFCs 2865 und 2866 definiert sind, 1812 für die Authentifizierung und 1813 für die Kontoführung. Allerdings werden manche Zugriffsserver UDP-Port 1645 für authentifizierungsanforderungen und UDP-Port 1646 für kontoführungsanforderungen verwenden standardmäßig konfiguriert.

>[!IMPORTANT]
>Wenn Sie nicht die Standardportnummern für die RADIUS-verwenden, müssen Sie Ausnahmen in der Firewall für den lokalen Computer zum Zulassen von RADIUS-Datenverkehr auf die neuen Ports konfigurieren. Weitere Informationen finden Sie unter [Konfigurieren von Firewalls für RADIUS-Verkehr](nps-firewalls-configure.md).

## <a name="configure-the-multihomed-nps"></a>Konfigurieren der mehrfach vernetzte NPS

Sie können das folgende Verfahren verwenden, Ihre mehrfach vernetzten NPS konfigurieren.

Grundvoraussetzung für die Ausführung dieses Vorgangs ist die Mitgliedschaft in **Domänen-Admins** oder einer gleichwertigen Gruppe.

### <a name="to-specify-the-network-adapter-and-udp-ports-that-nps-uses-for-radius-traffic"></a>Zum Angeben der Netzwerkadapter und der UDP-Ports, mit denen NPS RADIUS-Datenverkehr

1. Klicken Sie im Server-Manager auf **Tools**, und klicken Sie dann auf **Netzwerkrichtlinienserver** die NPS-Konsole zu öffnen.

2. Klicken Sie mit der rechten Maustaste auf **Netzwerkrichtlinienserver**, und klicken Sie dann auf **Eigenschaften**.

3. Klicken Sie auf die **Ports** Registerkarte, und stellen Sie die IP-Adresse für den Netzwerkadapter, die Sie für den RADIUS-Datenverkehr auf die vorhandenen Portnummern verwenden möchten. Beispielsweise sollten Sie die IP-Adresse 192.168.1.2 und RADIUS-Ports 1812 und 1645 für authentifizierungsanforderungen zu verwenden, ändern Sie die Einstellung für den Port aus **1812,1645** zu **192.168.1.2:1812,1645**. Wenn Ihre RADIUS-Authentifizierung und die RADIUS-Kontoführung UDP-Ports von den Standardwerten unterscheiden, ändern Sie die Porteinstellungen entsprechend.

4. Um mehrere Porteinstellungen für die Authentifizierung oder kontoführungsanforderungen verwenden möchten, trennen Sie die Portnummern durch Kommas.

Weitere Informationen zu NPS-UDP-Ports, finden Sie unter [NPS UDP-Port-Informationen konfigurieren](nps-udp-ports-configure.md)


Weitere Informationen zu NPS finden Sie unter [des Netzwerkrichtlinienservers](nps-top.md)

