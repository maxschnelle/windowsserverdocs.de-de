---
title: Konfigurieren von NPS auf einem mehrfach vernetzten Computer
description: Dieses Thema enthält Anweisungen zum Konfigurieren eines Servers mit mehreren Netzwerkadaptern, auf denen der Netzwerk Richtlinien Server unter Windows Server 2016 ausgeführt wird.
manager: brianlic
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: d9d9e9ac-4859-4522-89ed-a23092c9e12a
ms.author: lizross
author: eross-msft
ms.openlocfilehash: a937e151954629f7e8775ec68ba8ab5f2b63ee1a
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80315809"
---
# <a name="configure-nps-on-a-multihomed-computer"></a>Konfigurieren von NPS auf einem mehrfach vernetzten Computer

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

Sie können dieses Thema verwenden, um ein NPS mit mehreren Netzwerkadaptern zu konfigurieren.

Wenn Sie mehrere Netzwerkadapter auf einem Server verwenden, auf dem der Netzwerk Richtlinien Server (Network Policy Server, NPS) ausgeführt wird, können Sie Folgendes konfigurieren:

- Die Netzwerkadapter, von denen Remote Authentication Dial-in User Service \(RADIUS nicht gesendet und empfangen werden,\)-Datenverkehr.
- Auf Netzwerkadapter Basis, ob NPS RADIUS-Datenverkehr auf Internet Protokollversion 4 \(IPv4-\), IPv6 oder sowohl IPv4 als auch IPv6 überwacht.
- Die UDP-Portnummern, über die der RADIUS-Datenverkehr pro Protokoll \(IPv4-oder IPv6-\), pro Netzwerkadapter gesendet und empfangen wird.

Standardmäßig überwacht NPS RADIUS-Datenverkehr über die Ports 1812, 1813, 1645 und 1646 sowohl für IPv6 als auch für IPv4 für alle installierten Netzwerkadapter. Da NPS automatisch alle Netzwerkadapter für RADIUS-Datenverkehr verwendet, müssen Sie nur die Netzwerkadapter angeben, die NPS für den RADIUS-Verkehr verwenden soll, wenn Sie verhindern möchten, dass NPS einen bestimmten Netzwerkadapter verwenden.

>[!NOTE]
>Wenn Sie IPv4 oder IPv6 auf einem Netzwerkadapter deinstallieren, überwacht NPS nicht den RADIUS-Datenverkehr für das nicht installierte Protokoll.

Auf einem NPS, auf dem mehrere Netzwerkadapter installiert sind, empfiehlt es sich, NPS so zu konfigurieren, dass RADIUS-Datenverkehr nur an die von Ihnen angegebenen Adapter gesendet und empfangen wird.

Beispielsweise kann ein Netzwerkadapter, der im NPS installiert ist, zu einem Netzwerksegment führen, das keine RADIUS-Clients enthält, während ein zweiter Netzwerkadapter NPS mit einem Netzwerkpfad zu den konfigurierten RADIUS-Clients bereitstellt. In diesem Szenario ist es wichtig, dass NPS den zweiten Netzwerkadapter für den gesamten RADIUS-Datenverkehr verwendet.

Wenn für Ihr NPS beispielsweise drei Netzwerkadapter installiert sind, Sie aber nur zwei der Adapter für RADIUS-Datenverkehr verwenden möchten, können Sie nur Port Informationen für die beiden Adapter konfigurieren. Wenn Sie die Port Konfiguration für den dritten Adapter ausschließen, verhindern Sie, dass NPS den Adapter für RADIUS-Datenverkehr verwenden.

## <a name="using-a-network-adapter"></a>Verwenden eines Netzwerkadapters

Verwenden Sie die folgende Syntax im Dialogfeld Eigenschaften von Netzwerk Richtlinien Server in der NPS-Konsole, um NPS zum lauschen auf und Senden von RADIUS-Datenverkehr auf einem Netzwerkadapter zu konfigurieren:

- Syntax des IPv4-Datenverkehrs: IPAddress: UDPPort, wobei IPAddress die IPv4-Adresse ist, die auf dem Netzwerkadapter konfiguriert ist, über den Sie RADIUS-Datenverkehr senden möchten, und UDPPort ist die Nummer des RADIUS-Ports, den Sie für die RADIUS-Authentifizierung oder die Kontoführung verwenden möchten. verkehrssicher.
- IPv6-Datenverkehrs Syntax: [IPv6Address]: UDPPort, bei dem die Klammern um IPv6Address erforderlich sind, IPv6Address ist die IPv6-Adresse, die auf dem Netzwerkadapter konfiguriert ist, über den RADIUS-Datenverkehr gesendet werden soll, und UDPPort ist die gewünschte RADIUS-Portnummer. zur Verwendung für RADIUS-Authentifizierung oder Daten Buchhaltungs Datenverkehr.

Die folgenden Zeichen können als Trennzeichen für die Konfiguration von IP-Adresse und UDP-Port Informationen verwendet werden:

- Adress-/portdelimiter: Doppelpunkt (:)
- Port Trennzeichen: Komma (,)
- Schnittstellen Trennzeichen: Semikolon (;)

## <a name="configuring-network-access-servers"></a>Konfigurieren von Netzwerk Zugriffs Servern

Stellen Sie sicher, dass Ihre Netzwerk Zugriffs Server mit den gleichen RADIUS-UDP-Portnummern konfiguriert sind, die Sie für den NPSS konfigurieren. Die in den RFCs 2865 und 2866 definierten RADIUS-Standard-UDP-Ports lauten 1812 für die Authentifizierung und 1813 für die Kontoführung. Allerdings sind einige Zugriffs Server standardmäßig so konfiguriert, dass Sie den UDP-Port 1645 für Authentifizierungsanforderungen und den UDP-Port 1646 für Buchhaltungs Anforderungen verwenden.

>[!IMPORTANT]
>Wenn Sie die RADIUS-Standard Portnummern nicht verwenden, müssen Sie Ausnahmen in der Firewall für den lokalen Computer konfigurieren, um RADIUS-Datenverkehr für die neuen Ports zuzulassen. Weitere Informationen finden Sie unter [Konfigurieren von Firewalls für RADIUS-Datenverkehr](nps-firewalls-configure.md).

## <a name="configure-the-multihomed-nps"></a>Konfigurieren der mehrfach vernetzten NPS

Sie können das folgende Verfahren verwenden, um die mehrfach vernetzten NPS zu konfigurieren.

Zum Durchführen dieses Verfahrens ist mindestens die Mitgliedschaft in **Domänen-Admins** oder eine entsprechende Berechtigung erforderlich.

### <a name="to-specify-the-network-adapter-and-udp-ports-that-nps-uses-for-radius-traffic"></a>So geben Sie den Netzwerkadapter und die UDP-Ports an, die NPS für RADIUS-Datenverkehr verwendet

1. Klicken Sie im Server-Manager auf **Extras, und**klicken Sie dann auf **Netzwerk Richtlinien Server** , um die NPS-Konsole zu öffnen.

2. Klicken Sie mit der rechten Maustaste auf **Netzwerkrichtlinienserver**, und klicken Sie dann auf **Eigenschaften**.

3. Klicken Sie auf die Registerkarte **Ports** , und fügen Sie die IP-Adresse für den Netzwerkadapter, den Sie für den RADIUS-Datenverkehr verwenden möchten, den vorhandenen Portnummern hinzu. Wenn Sie z. b. die IP-Adresse 192.168.1.2 und die RADIUS-Ports 1812 und 1645 für Authentifizierungsanforderungen verwenden möchten, ändern Sie die Port Einstellung von **1812, 1645** in **192.168.1.2:1812, 1645**. Wenn sich die UDP-Ports der RADIUS-Authentifizierung und der RADIUS-Buchhaltung von den Standardwerten unterscheiden, ändern Sie die Port Einstellungen entsprechend.

4. Wenn Sie mehrere Port Einstellungen für Authentifizierungs-oder Buchhaltungs Anforderungen verwenden möchten, trennen Sie die Portnummern durch Kommas.

Weitere Informationen zu NPS-UDP-Ports finden Sie unter [Konfigurieren von NPS-UDP-Port Informationen](nps-udp-ports-configure.md) .


Weitere Informationen zu NPS finden Sie unter [Netzwerk Richtlinien Server](nps-top.md) .

