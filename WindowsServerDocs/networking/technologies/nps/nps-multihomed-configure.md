---
title: Konfigurieren von NPS auf einem mehrfach vernetzten Computer
description: Dieses Thema enthält Anweisungen zum Konfigurieren eines Servers mit mehreren Netzwerkadaptern, die in Windows Server2016 Network Policy Server ausgeführt wird.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: d9d9e9ac-4859-4522-89ed-a23092c9e12a
ms.author: pashort
author: shortpatti
ms.openlocfilehash: f80e83a4d79036729b6b442e6362d52fbda12edd
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="configure-nps-on-a-multihomed-computer"></a>Konfigurieren von NPS auf einem mehrfach vernetzten Computer

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

In diesem Thema können Sie einen NPS-Server mit mehreren Netzwerkadaptern konfigurieren.

Wenn Sie mehrere Netzwerkadapter auf einem Server mit Netzwerkrichtlinienserver (Network Policy Server, NPS) verwenden, können Sie Folgendes konfigurieren:

- Die Netzwerkadapter, die keine und führen Sie senden und Empfangen von Remote Authentication Dial-in User Service \(RADIUS\) Datenverkehr.
- Pro-Adapter pro Netzwerk überwacht, ob NPS RADIUS-Datenverkehr auf Internetprotokoll Version 4 \(IPv4\), IPv6, oder IPv4 und IPv6.
- Die UDP-Portnummern, über welche RADIUS Datenverkehr gesendet und empfangen wird auf einer pro-Protokoll \ (IPv4 oder IPv6\) pro Adapter einzeln.

Standardmäßig überwacht NPS RADIUS-Datenverkehr auf den Ports 1812, 1813, 1645 und 1646 für IPv6 und IPv4 für alle installierten Netzwerkadapter. Da NPS automatisch alle Netzwerkadapter für RADIUS-Datenverkehr verwendet wird, müssen Sie nur angeben, dass der Netzwerkadapter, die NPS für RADIUS verwendet werden sollen Datenverkehr, wenn Sie verhindern, dass NPS einen bestimmten Netzwerkadapter verwenden möchten.

>[!NOTE]
>Wenn Sie auf einem Netzwerkadapter entweder IPv4 oder IPv6 deinstallieren, überwacht NPS RADIUS-Datenverkehr für das deinstallierte Protokoll nicht.

Auf einem Netzwerkrichtlinienserver, die mehrere Netzwerkadapter installiert sind, möchten möglicherweise Konfigurieren von NPS zum Senden und Empfangen von RADIUS-Datenverkehr nur auf den Adaptern ab.

Z.B. ein Netzwerkadapter installiert, in der NPS-Server kann dazu führen, dass ein Netzwerksegment, die keine RADIUS-Clients enthält, während eine zweite Netzwerkkarte bereitstellt wurde NPS mit einem Netzwerkpfad zu RADIUS-Clients konfiguriert. In diesem Szenario ist es wichtig, dass Sie direkt auf den zweiten Netzwerkadapter für RADIUS-Datenverkehr verwenden.

In einem weiteren Beispiel können der NPS-Server verfügt über drei Netzwerkadapter installiert, aber Sie möchten nur NPS, zwei Adapter für RADIUS-Datenverkehr, müssen Sie Portinformationen für nur zwei Adapter konfigurieren. Durch Ausschließen der Portkonfiguration für den dritten Netzwerkadapter, verhindern Sie NPS unter Verwendung des Adapters für RADIUS-Datenverkehr.

## <a name="using-a-network-adapter"></a>Mithilfe eines Netzwerkadapters

Verwenden Sie die folgende Syntax auf das Dialogfeld "Eigenschaften" des Netzwerkrichtlinienservers in der NPS-Konsole, um NPS zum Überwachen und Senden von RADIUS-Datenverkehr auf einem Netzwerkadapter zu konfigurieren:

- Syntax für IPv4-Datenverkehr: IPAddress:UDPport, wobei IP-Adresse die IPv4-Adresse, die auf dem Netzwerkadapter konfiguriert ist, über die Sie RADIUS-Datenverkehr senden möchten, und UDPport ist die RADIUS-Portnummer, die Sie für die RADIUS-Authentifizierung oder Kontoführungsdatenverkehr verwenden möchten.
- Syntax für IPv6-Datenverkehr: [IPv6Address]: UDPport, in denen die Klammern IPv6Address erforderlich sind, IPv6Address ist die IPv6-Adresse, die auf dem Netzwerkadapter konfiguriert ist, über den RADIUS-Datenverkehr gesendet werden sollen, und UDPport ist die RADIUS-Portnummer, die Sie für die RADIUS-Authentifizierung oder Kontoführungsdatenverkehr verwenden möchten.

Die folgenden Zeichen können zum Konfigurieren von IP-Adresse und UDP-Portinformationen als Trennzeichen verwendet werden:

- Adresse/Port als Trennzeichen: Doppelpunkt (:))
- Port als Trennzeichen: durch Kommas (,)
- Trennzeichen für Schnittstelle: Semikolon (;)

## <a name="configuring-network-access-servers"></a>Konfigurieren Netzwerkzugriffsserver

Stellen Sie sicher, dass Ihre Netzwerkzugriffsserver mit den gleichen RADIUS-UDP-Portnummern konfiguriert sind, die Sie auf den NPS-Servern konfigurieren. In den RFCs 2865 und 2866 definierten standardmäßigen RADIUS-UDP-Ports sind 1812 für die Authentifizierung und 1813 für die Kontoführung. Allerdings sind einige Server standardmäßig mithilfe von UDP-Port 1645 zur Authentifizierung und UDP-Port 1646 zur Kontoführung konfiguriert.

>[!IMPORTANT]
>Wenn Sie nicht die Standardportnummern RADIUS verwenden, müssen Sie Ausnahmen in der Firewall für den lokalen Computer zum Zulassen von RADIUS-Datenverkehr über die neuen Ports konfigurieren. Weitere Informationen finden Sie unter [Konfigurieren von Firewalls für RADIUS-Datenverkehr](nps-firewalls-configure.md).

## <a name="configure-the-multihomed-nps-server"></a>Konfigurieren Sie den mehrfach vernetzten NPS-Server

Das folgende Verfahren können Ihren mehrfach vernetzten NPS-Server konfigurieren.

Mitgliedschaft in **Domänen-Admins**, oder einer gleichwertigen Gruppe ist mindestens erforderlich, um dieses Verfahren ausführen.

### <a name="to-specify-the-network-adapter-and-udp-ports-that-nps-uses-for-radius-traffic"></a>Die Netzwerkadapter und UDP-Ports, mit denen NPS RADIUS-Datenverkehr

1. Klicken Sie im Server-Manager auf **Tools**, und klicken Sie dann auf **Netzwerkrichtlinienserver** die NPS-Konsole zu öffnen.

2. Mit der rechten Maustaste **Netzwerkrichtlinienserver**, und klicken Sie dann auf **Eigenschaften**.

3. Klicken Sie auf die **Ports** Registerkarte, und stellen Sie die IP-Adresse für den Netzwerkadapter, die Sie für den RADIUS-Datenverkehr zu den vorhandenen Portnummern verwenden möchten. Wenn beispielsweise Sie die IP-Adresse 192.168.1.2 und RADIUS-Ports 1812 und 1645 zur Authentifizierung verwenden möchten, ändern Sie die porteinstellung von **1812,1645** auf **192.168.1.2:1812,1645**. Wenn Ihre RADIUS-Authentifizierung und RADIUS-Kontoführung UDP-Ports von den Standardwerten unterscheiden, ändern Sie die Porteinstellungen entsprechend.

4. Um mehrere Porteinstellungen für die Authentifizierung oder Kontoführung verwenden möchten, trennen Sie die Portnummern durch Kommas.

Weitere Informationen zu NPS-UDP-Ports, finden Sie unter [NPS-UDP-Portinformationen konfigurieren](nps-udp-ports-configure.md)


Weitere Informationen zu NPS finden Sie unter [Netzwerkrichtlinienserver](nps-top.md)

