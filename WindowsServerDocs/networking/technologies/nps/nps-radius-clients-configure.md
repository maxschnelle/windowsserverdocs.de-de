---
title: Konfigurieren von RADIUS-Clients
description: Dieses Thema enthält Informationen zum Konfigurieren von RADIUS-Clients für Netzwerkrichtlinienserver unter Windows Server 2016.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: cde37849-ce79-4c26-aa14-cd0ef31cae18
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 851bdb0677a17567f81a2c331baad595fe40436a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59839491"
---
# <a name="configure-radius-clients"></a>Konfigurieren von RADIUS-Clients

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Sie können in diesem Thema verwenden, um Netzwerkzugriffsserver als RADIUS-Clients in NPS konfigurieren.

Beim Hinzufügen einer neuen Netzwerkzugriffsservers \(VPN-Server, drahtlosen Zugriffspunkt, Authentifizierung, Switch oder DFÜ-Server\) zum Netzwerk müssen Sie fügen Sie den Server als RADIUS-Client auf dem Netzwerkrichtlinienserver, und konfigurieren Sie dann auf den RADIUS-Client für die Kommunikation mit dem NPS.

>[!IMPORTANT]
>Client-Computern und Geräten, z. B. Laptops, Tablets, Smartphones und andere Computer mit Clientbetriebssystemen, sind keine RADIUS-Clients. RADIUS-Clients sind Netzwerkzugriffsserver – z. B. Drahtloszugriffspunkte, 802.1X-fähige X-fähigen switches, virtuelle Private Netzwerk (VPN)-Server und DFÜ-Server –, da sie das RADIUS-Protokoll verwenden, für die Kommunikation mit RADIUS-Server, z. B. Network Policy Server \(NPS\) Server.

Dieser Schritt ist auch erforderlich, wenn Sie den NPS RADIUS-Remoteservergruppe angehört, die auf einem NPS-Proxy konfiguriert ist. In diesem Fall, zusätzlich zu den Schritten in dieser Aufgabe auf dem NPS-Proxy gehen Sie folgendermaßen vor:

- Konfigurieren Sie eine remote-RADIUS-Servergruppe, die den NPS enthält, auf dem NPS-Proxy.
- Konfigurieren Sie die NPS-Proxy für den remote-NPS als RADIUS-Client.

Um die Verfahren in diesem Thema ausführen zu können, benötigen Sie mindestens eine Netzwerkzugriffsservers \(VPN-Server, drahtlosen Zugriffspunkt, Authentifizierung, Switch oder DFÜ-Server\) oder NPS-Proxy, die physisch in Ihrem Netzwerk installiert.

## <a name="configure-the-network-access-server"></a>Network Access Server konfigurieren

Verwenden Sie dieses Verfahren, um Netzwerkzugriffsserver, die für die Verwendung mit NPS konfigurieren. Wenn Sie Netzwerkzugriffsserver (NAS) als RADIUS-Clients bereitstellen, müssen Sie konfigurieren die Clients die Kommunikation mit dem NPSs, in die NAS-Servern als Clients konfiguriert sind.

Dieses Verfahren umfasst allgemeine Richtlinien über die Einstellungen, die Sie verwenden sollten, um Ihre Netzwerkzugriffsserver konfigurieren; spezifische Anweisungen zum Konfigurieren des Geräts, auf denen Sie in Ihrem Netzwerk bereitstellen, finden Sie unter der NAS-Produktdokumentation.

### <a name="to-configure-the-network-access-server"></a>Network Access Server konfigurieren

1. Auf dem NAS in **RADIUS-Clienteinstellungen**Option **RADIUS-Authentifizierung** User Datagram Protocol (UDP) Port **1812** und **RADIUS-Kontoführung**an UDP-Port **1813**.
2. In **Authentifizierungsserver** oder **RADIUS-Server**, geben Sie Ihre IP-Adresse oder den vollqualifizierten Domänennamen (FQDN), je nach den Anforderungen des NAS von NPS. 
3. In **Geheimnis** oder **gemeinsamer geheimer Schlüssel**, geben Sie ein sicheres Kennwort ein. Wenn Sie das NAS als RADIUS-Client in NPS konfigurieren, verwenden Sie das gleiche Kennwort, damit sie nicht vergessen.
4. Wenn Sie PEAP oder EAP als Authentifizierungsmethode verwenden, konfigurieren Sie das NAS um EAP-Authentifizierung verwenden.
5. Wenn Sie in einem drahtlosen Zugriffspunkt, konfigurieren **SSID**, geben Sie einen Service Set Identifier \(SSID\), dies ist eine alphanumerische Zeichenfolge, die als Name des Netzwerks dient. Dieser Name wird übertragen, indem Sie Zugriffspunkten, drahtlosen Clients und ist sichtbar für Benutzer in Ihrer drahtlosen Qualität \(Wi-Fi\) Hotspots.
6. Wenn Sie in einem drahtlosen Zugriffspunkt, konfigurieren **802.1 X und WPA**, aktivieren Sie **IEEE 802.1X-Authentifizierung** , wenn Sie PEAP-MS-CHAP v2, PEAP-TLS oder EAP-TLS bereitstellen möchten.

## <a name="add-the-network-access-server-as-a-radius-client-in-nps"></a>Network Access Server als RADIUS-Client auf dem Netzwerkrichtlinienserver hinzufügen

Verwenden Sie dieses Verfahren zum Hinzufügen eines Netzwerk-Servers als RADIUS-Client auf dem Netzwerkrichtlinienserver. Sie können dieses Verfahren verwenden, NAS als RADIUS-Client zu konfigurieren, mit der NPS-Konsole.

Sie müssen Mitglied der Gruppe **Administratoren** sein, um diesen Vorgang auszuführen.

### <a name="to-add-a-network-access-server-as-a-radius-client-in-nps"></a>Hinzufügen ein Netzwerk-Servers als RADIUS-Client auf dem Netzwerkrichtlinienserver

1. Klicken Sie auf den NPS, im Server-Manager auf **Tools**, und klicken Sie dann auf **Netzwerkrichtlinienserver**. Die NPS-Konsole wird geöffnet.
2. Doppelklicken Sie in der NPS-Konsole auf **RADIUS-Clients und Servern**. Mit der rechten Maustaste **RADIUS-Clients**, und klicken Sie dann auf **Neuer RADIUS-Client**. 
3. In **Neuer RADIUS-Client**, überprüfen Sie, ob die **aktivieren Sie dieses RADIUS-Clients** das Kontrollkästchen aktiviert ist.
4. In **Neuer RADIUS-Client**im **Anzeigenamen**, geben Sie einen Anzeigenamen für das NAS. In **Adresse (IP oder DNS)**, geben Sie den NAS IP-Adresse oder den vollständig qualifizierten Domänennamen (FQDN). Wenn Sie den FQDN eingegeben haben, klicken Sie auf **überprüfen** sollten Sie überprüfen, ob der Name richtig ist und eine gültige IP-Adresse zugeordnet. 
5. In **Neuer RADIUS-Client**im **Hersteller**, geben Sie den Namen der NAS-Hersteller. Wenn Sie nicht über den Herstellernamen NAS sicher sind, wählen Sie **RADIUS-Standards**.
6. In **Neuer RADIUS-Client**im **gemeinsamer geheimer Schlüssel**, führen Sie einen der folgenden:
    - Sicherstellen, dass **manuelle** ausgewählt ist, und klicken Sie dann im **gemeinsamer geheimer Schlüssel**, geben Sie das starke Kennwort, die auch auf dem NAS eingegeben werden. Geben Sie den gemeinsamen geheimen Schlüssel im **gemeinsamen geheimen Schlüssel bestätigen**.
    - Wählen Sie **generieren**, und klicken Sie dann auf **generieren** einen gemeinsamen geheimen Schlüssel automatisch generieren. Speichern Sie den generierten gemeinsamen geheimen Schlüssel für die Konfiguration auf dem NAS, sodass er mit der NPS kommunizieren kann.
7. In **Neuer RADIUS-Client**im **zusätzliche Optionen**, sofern Sie andere Authentifizierungsmethoden als EAP und PEAP verwenden, und wenn Ihre NAS Verwendung des Attributs Authenticator Nachricht unterstützt, wählen **Access-Request-Nachrichten darf das Attribut für die Nachrichtenauthentifizierung**.
8. Klicken Sie auf **OK**. Ihre NAS wird angezeigt, in der Liste der RADIUS-Clients, die für den NPS konfiguriert.

## <a name="configure-radius-clients-by-ip-address-range-in-windows-server-2016-datacenter"></a>Konfigurieren Sie RADIUS-Clients von IP-Adressbereich in Windows Server 2016 Datacenter

Wenn Sie Windows Server 2016 Datacenter ausgeführt werden, können Sie durch die IP-Adressbereich RADIUS-Clients in NPS konfigurieren. Dadurch können Sie die NPS-Konsole gleichzeitig ausführen möchten, eine große Anzahl von RADIUS-Clients (z. B. drahtlose Zugriffspunkte) hinzufügen, anstatt jeden RADIUS-Client einzeln hinzuzufügen.

Sie können nicht von IP-Adressbereich RADIUS-Clients konfigurieren, wenn Sie NPS unter Windows Server 2016 Standard ausführen.

Verwenden Sie dieses Verfahren, um eine Gruppe von Netzwerkzugriffsservern (NAS) als RADIUS-Clients hinzuzufügen, die alle mit der IP-Adressen aus der gleichen IP-Adressbereich konfiguriert sind.

Alle im Bereich RADIUS-Clients müssen die gleiche Konfiguration und den gemeinsamen geheimen Schlüssel verwenden.

Sie müssen Mitglied der Gruppe **Administratoren** sein, um diesen Vorgang auszuführen.

### <a name="to-set-up-radius-clients-by-ip-address-range"></a>Einrichten von RADIUS-Clients von IP-Adressbereich

1. Klicken Sie auf den NPS, im Server-Manager auf **Tools**, und klicken Sie dann auf **Netzwerkrichtlinienserver**. Die NPS-Konsole wird geöffnet.
2. Doppelklicken Sie in der NPS-Konsole auf **RADIUS-Clients und Servern**. Mit der rechten Maustaste **RADIUS-Clients**, und klicken Sie dann auf **Neuer RADIUS-Client**.
3. In **Neuer RADIUS-Client**im **Anzeigenamen**, geben Sie einen Anzeigenamen für die Auflistung von NAS-Servern.
4. In **Adresse \(IP-Adresse oder DNS-\)**, geben Sie den IP-Adressbereich für den RADIUS-Clients mithilfe von klassenloses domänenübergreifendes Routing \(CIDR\) Notation. Geben Sie beispielsweise, wenn die IP-Adressbereich für den NAS-Servern 10.10.0.0 ist, **10.10.0.0/16**.
5. In **Neuer RADIUS-Client**im **Hersteller**, geben Sie den Namen der NAS-Hersteller. Wenn Sie nicht über den Herstellernamen NAS sicher sind, wählen Sie **RADIUS-Standards**.
6. In **Neuer RADIUS-Client**im **gemeinsamer geheimer Schlüssel**, führen Sie einen der folgenden:
    - Sicherstellen, dass **manuelle** ausgewählt ist, und klicken Sie dann im **gemeinsamer geheimer Schlüssel**, geben Sie das starke Kennwort, die auch auf dem NAS eingegeben werden. Geben Sie den gemeinsamen geheimen Schlüssel im **gemeinsamen geheimen Schlüssel bestätigen**.
    - Wählen Sie **generieren**, und klicken Sie dann auf **generieren** einen gemeinsamen geheimen Schlüssel automatisch generieren. Speichern Sie den generierten gemeinsamen geheimen Schlüssel für die Konfiguration auf dem NAS, sodass er mit der NPS kommunizieren kann.
7. In **Neuer RADIUS-Client**im **zusätzliche Optionen**, sofern andere Authentifizierungsmethoden als EAP und PEAP verwenden, und wenn die Unterstützung aller Ihrer NAS-Servern mithilfe des Attributs Authenticator Nachricht, wählen Sie  **Access-Request-Meldungen darf das Attribut für die Nachrichtenauthentifizierung**.
8. Klicken Sie auf **OK**. Ihre Netzwerkzugriffsserver angezeigt, in der Liste der RADIUS-Clients, die für den NPS konfiguriert.

Weitere Informationen finden Sie unter [RADIUS-Clients](nps-radius-clients.md).

Weitere Informationen zu NPS finden Sie unter [(Network Policy Server, NPS)](nps-top.md).