---
title: Konfigurieren von RADIUS-Clients
description: Dieses Thema enthält Informationen zum Konfigurieren von RADIUS-Clients für Netzwerkrichtlinienserver in Windows Server2016.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: cde37849-ce79-4c26-aa14-cd0ef31cae18
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 9af3189199c8282394ca34f181a90b4290c55044
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="configure-radius-clients"></a>Konfigurieren von RADIUS-Clients

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

In diesem Thema können Sie Netzwerkzugriffsserver als RADIUS-Clients in NPS konfigurieren.

Wenn Sie einen neuen Netzwerkzugriffsserver hinzufügen \ (VPN-Server, drahtlosen Zugriffspunkt, Authentifizierung, Switch oder DFÜ-Server\) mit dem Netzwerk müssen Sie fügen Sie den Server als RADIUS-Client auf dem Netzwerkrichtlinienserver, und klicken Sie dann den RADIUS-Client zur Kommunikation mit dem NPS-Server konfigurieren.

>[!IMPORTANT]
>Clientcomputern und Geräten, z.B. Laptops, Tablets, Smartphones und andere Computer mit Clientbetriebssystemen, sind keine RADIUS-Clients. RADIUS-Clients sind Netzwerkzugriffsserver – z.B. Drahtloszugriffspunkte, 802.1X-fähige X-fähigen Switches, virtuelle Private Netzwerk (VPN)-Servern und DFÜ-Server -, da sie das RADIUS-Protokoll zur Kommunikation mit RADIUS-Servern, z.B. Netzwerkrichtlinienserver \(NPS\) verwenden.

Dieser Schrittist auch erforderlich, wenn der NPS-Server ein Mitglied einer RADIUS-Remoteservergruppe ist, die auf einen NPS-Proxy konfiguriert ist. In diesem Fall zusätzlich zu den Schrittenin dieser Aufgabe auf dem NPS-Proxy müssen Sie Folgendes tun:

- Konfigurieren Sie eine RADIUS-Remoteservergruppe mit dem NPS Server, auf dem NPS-Proxy.
- Konfigurieren Sie die NPS-Proxy als RADIUS-Client, auf dem NPS-Remoteserver.

Zum Ausführen der Verfahren in diesem Thema benötigen Sie mindestens einen Netzwerkzugriffsserver \ (VPN-Server, drahtlosen Zugriffspunkt, Authentifizierung, Switch oder DFÜ-Server\) oder NPS-Proxy in Ihrem Netzwerk physisch installiert.

## <a name="configure-the-network-access-server"></a>Konfigurieren Sie Netzwerkzugriffsserver

Verwenden Sie dieses Verfahren, um Netzwerkzugriffsserver für die Verwendung mit NPS zu konfigurieren. Wenn Sie Netzwerkzugriffsservern (NAS) als RADIUS-Clients bereitstellen, müssen Sie die Clients mit der NPS-Server kommunizieren, auf dem die Netzwerkzugriffsserver als Clients konfiguriert werden, konfigurieren.

Dieses Verfahren umfasst allgemeine Richtlinien zu den Einstellungen, die Sie verwenden sollten, so konfigurieren Sie Ihre Netzwerkzugriffsserver; spezifische Informationen zur Konfiguration des Geräts, das Sie in Ihrem Netzwerk bereitstellen, finden Sie unter Ihrem NAS-Produktdokumentation.

### <a name="to-configure-the-network-access-server"></a>So konfigurieren Sie Netzwerkzugriffsserver

1. Auf dem NAS in **RADIUS-Einstellungen**Option **RADIUS-Authentifizierung** User Datagram-Protokoll (UDP) Port **1812** und **RADIUS-Kontoführung** UDP-Port **1813**.
2. In **Authentifizierungsserver** oder **RADIUS-Server**, den NPS-Server IP-Adresse oder den vollqualifizierten Domänennamen (FQDN), abhängig von den Anforderungen des Netzwerkzugriffsservers angeben. 
3. In **geheimen Schlüssel** oder **gemeinsamer geheimer Schlüssel**, geben Sie ein sicheres Kennwort ein. Wenn Sie den NAS als RADIUS-Client in NPS konfigurieren, verwenden Sie dasselbe Kennwort, damit Sie nicht vergessen.
4. Wenn Sie PEAP- oder EAP als Authentifizierungsmethode verwenden, konfigurieren Sie die NAS um EAP-Authentifizierung verwenden.
5. Wenn Sie einen drahtlosen Zugriffspunkt in konfigurieren **SSID**, geben Sie einen \(SSID\) Service Set Identifier, sich um eine alphanumerische Zeichenfolge, die als den Namen des Netzwerks dient. Dieser Name von Zugangspunkten für drahtlose Clients übertragen wird und Benutzer an Ihre Wireless Fidelity \(Wi-Fi\) Hotspots sichtbar ist.
6. Wenn Sie einen drahtlosen Zugriffspunkt in konfigurieren **802.1 X und WPA**, aktivieren Sie **IEEE 802.1X-Authentifizierung** Wenn Sie PEAP-MS-CHAP v2, PEAP-TLS oder EAP-TLS bereitstellen möchten.

## <a name="add-the-network-access-server-as-a-radius-client-in-nps"></a>Hinzufügen von Network Access Server als RADIUS-Client auf dem Netzwerkrichtlinienserver

Verwenden Sie dieses Verfahren, um einen Netzwerkzugriffsserver als RADIUS-Client auf dem Netzwerkrichtlinienserver hinzuzufügen. Dieses Verfahrens können Sie um ein NAS als RADIUS-Client zu konfigurieren, mit der NPS-Konsole.

Um dieses Verfahren auszuführen, müssen Sie Mitglied der werden die **Administratoren** Gruppe.

### <a name="to-add-a-network-access-server-as-a-radius-client-in-nps"></a>Hinzufügen ein Netzwerk-Servers als RADIUS-Client auf dem Netzwerkrichtlinienserver

1. Klicken Sie auf dem NPS-Server im Server-Manager auf **Tools**, und klicken Sie dann auf **Netzwerkrichtlinienserver**. Die NPS-Konsole wird geöffnet.
2. Doppelklicken Sie in der NPS-Konsole auf **RADIUS-Clients und Servern**. Mit der rechten Maustaste **RADIUS-Clients**, und klicken Sie dann auf **Neuer RADIUS-Client**. 
3. In **Neuer RADIUS-Client**, überprüfen Sie, ob die **Aktivieren dieser RADIUS-Client** das Kontrollkästchen aktiviert ist.
4. In **Neuer RADIUS-Client**im **Anzeigenamen**, geben Sie einen Anzeigenamen für den NAS. In **Adresse (IP oder DNS)**, geben Sie den NAS-IP-Adresse oder den vollqualifizierten Domänennamen (FQDN). Wenn Sie den FQDN eingegeben haben, klicken Sie auf **überprüfen, ob** stellen Sie sicher, dass der Name richtig ist und eine gültige IP-Adresse zugeordnet werden sollen. 
5. In **Neuer RADIUS-Client**im **Anbieter**, geben Sie den Namen des NAS-Herstellers. Wenn Sie nicht sicher, dass der Name des NAS-Herstellers sind, wählen Sie **RADIUS-Standards**.
6. In **Neuer RADIUS-Client**im **gemeinsamer geheimer Schlüssel**, führen Sie eine der folgenden Optionen:
    - Sicherstellen, dass **manuell** ausgewählt ist, und klicken Sie dann im **gemeinsamer geheimer Schlüssel**, geben Sie das sichere Kennwort, die auch auf dem NAS eingegeben werden. Geben Sie den gemeinsamen geheimen Schlüssel in **gemeinsamen geheimen Schlüssel bestätigen**.
    - Wählen Sie **generieren**, und klicken Sie dann auf **generieren** automatisch einen gemeinsamen geheimen Schlüssel zu generieren. Speichern Sie den generierten gemeinsamen geheimen Schlüssel für die Konfiguration auf dem NAS, damit sie mit dem NPS-Server kommunizieren kann.
7. In **Neuer RADIUS-Client**im **zusätzliche Optionen**, wenn Sie Authentifizierungsmethoden EAP und PEAP verwenden, und wählen Sie, wenn Ihre NAS Verwendung des Attributs Authentifikator Nachricht unterstützt **Nachrichten Zugriff anfordern müssen das Attribut Nachrichtenauthentifizierung enthalten**.
8. Klicken Sie auf **OK**. NAS wird angezeigt, in der Liste der RADIUS-Clients, die auf dem NPS-Server konfiguriert.

## <a name="configure-radius-clients-by-ip-address-range-in-windows-server-2016-datacenter"></a>Konfigurieren von RADIUS-Clients nach IP-Adressbereich in Windows Server2016 Datacenter

Wenn Sie Windows Server2016 Datacenter ausgeführt werden, können Sie über den IP-Adressbereich RADIUS-Clients in NPS konfigurieren. Dadurch können Sie die NPS-Konsole gleichzeitig ausführen möchten, eine große Anzahl von RADIUS-Clients (z.B. drahtlose Zugriffspunkte) hinzufügen, anstatt jeden RADIUS-Client einzeln hinzufügen.

Sie können keine RADIUS-Clients nach IP-Adressbereich konfigurieren, wenn Sie NPS auf Windows Server2016 Standard ausgeführt werden.

Verwenden Sie dieses Verfahren, um eine Gruppe von Netzwerkzugriffsservern (NAS) als RADIUS-Clients hinzufügen, die alle mit IP-Adressen aus dem IP-Adressbereich konfiguriert sind.

Alle im Bereich RADIUS-Clients müssen die gleiche Konfiguration und den gemeinsamen geheimen Schlüssel verwenden.

Um dieses Verfahren auszuführen, müssen Sie Mitglied der werden die **Administratoren** Gruppe.

### <a name="to-set-up-radius-clients-by-ip-address-range"></a>Zum Einrichten von RADIUS-Clients nach IP-Adressbereich

1. Klicken Sie auf dem NPS-Server im Server-Manager auf **Tools**, und klicken Sie dann auf **Netzwerkrichtlinienserver**. Die NPS-Konsole wird geöffnet.
2. Doppelklicken Sie in der NPS-Konsole auf **RADIUS-Clients und Servern**. Mit der rechten Maustaste **RADIUS-Clients**, und klicken Sie dann auf **Neuer RADIUS-Client**.
3. In **Neuer RADIUS-Client**im **Anzeigenamen**, geben Sie einen Anzeigenamen für die Sammlung von NASs.
4. In **Adresse \(IP or DNS\)**, geben Sie den IP-Adressbereich für den RADIUS-Clients mit \(CIDR\) Classless Inter-Domain Routing. Geben Sie z.B. ist der IP-Adressbereich für die Netzwerkzugriffsserver 10.10.0.0, **10.10.0.0/16**.
5. In **Neuer RADIUS-Client**im **Anbieter**, geben Sie den Namen des NAS-Herstellers. Wenn Sie nicht sicher, dass der Name des NAS-Herstellers sind, wählen Sie **RADIUS-Standards**.
6. In **Neuer RADIUS-Client**im **gemeinsamer geheimer Schlüssel**, führen Sie eine der folgenden Optionen:
    - Sicherstellen, dass **manuell** ausgewählt ist, und klicken Sie dann im **gemeinsamer geheimer Schlüssel**, geben Sie das sichere Kennwort, die auch auf dem NAS eingegeben werden. Geben Sie den gemeinsamen geheimen Schlüssel in **gemeinsamen geheimen Schlüssel bestätigen**.
    - Wählen Sie **generieren**, und klicken Sie dann auf **generieren** automatisch einen gemeinsamen geheimen Schlüssel zu generieren. Speichern Sie den generierten gemeinsamen geheimen Schlüssel für die Konfiguration auf dem NAS, damit sie mit dem NPS-Server kommunizieren kann.
7. In **Neuer RADIUS-Client**im **zusätzliche Optionen**, wenn Sie Authentifizierungsmethoden EAP und PEAP verwenden, und wählen Sie alle Ihre Netzwerkzugriffsserver Verwendung des Attributs Authentifikator Nachricht unterstützt **Nachrichten Zugriff anfordern müssen das Attribut Nachrichtenauthentifizierung enthalten**.
8. Klicken Sie auf **OK**. Ihre Netzwerkzugriffsserver angezeigt in der Liste der RADIUS-Clients, die auf dem NPS-Server konfiguriert werden.

Weitere Informationen finden Sie unter [RADIUS-Clients](nps-radius-clients.md).

Weitere Informationen zu NPS finden Sie unter [(Network Policy Server, NPS)](nps-top.md).