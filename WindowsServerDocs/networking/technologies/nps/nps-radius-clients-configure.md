---
title: Konfigurieren von RADIUS-Clients
description: Dieses Thema enthält Informationen zum Konfigurieren von RADIUS-Clients für den Netzwerk Richtlinien Server unter Windows Server 2016.
manager: brianlic
ms.topic: article
ms.assetid: cde37849-ce79-4c26-aa14-cd0ef31cae18
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 1992470a643a1633479940c1a0f98f8e7e67f5c1
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87951961"
---
# <a name="configure-radius-clients"></a>Konfigurieren von RADIUS-Clients

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Sie können dieses Thema verwenden, um Netzwerk Zugriffs Server als RADIUS-Clients in NPS zu konfigurieren.

Wenn Sie einen neuen Netzwerk Zugriffs Server- \( VPN-Server, drahtlosen Zugriffspunkt, authentifizier enden Switch oder DFÜ-Server in \) Ihrem Netzwerk hinzufügen, müssen Sie den Server in NPS als RADIUS-Client hinzufügen und dann den RADIUS-Client für die Kommunikation mit dem NPS konfigurieren.

>[!IMPORTANT]
>Client Computer und-Geräte, z. b. Laptops, Tablets, Smartphones und andere Computer, auf denen Client Betriebssysteme ausgeführt werden, sind keine RADIUS-Clients. RADIUS-Clients sind Netzwerk Zugriffs Server, z. b. drahtlos Zugriffspunkte, 802.1 x-fähige Switches, VPN-Server (virtuelles privates Netzwerk) und DFÜ-Server, da Sie das RADIUS-Protokoll für die Kommunikation mit RADIUS-Servern verwenden, z. b. Netzwerk Richtlinien Server- \( NPS- \) Server.

Dieser Schritt ist auch erforderlich, wenn Ihr NPS Mitglied einer RADIUS-Remote Server Gruppe ist, die auf einem NPS-Proxy konfiguriert ist. In dieser Situation müssen Sie nicht nur die Schritte in dieser Aufgabe auf dem NPS-Proxy ausführen, sondern auch die folgenden Schritte ausführen:

- Konfigurieren Sie auf dem NPS-Proxy eine Remote-RADIUS-Server Gruppe, die den NPS enthält.
- Konfigurieren Sie den NPS-Proxy auf dem Remote-NPS als RADIUS-Client.

Um die in diesem Thema beschriebenen Verfahren auszuführen, benötigen Sie mindestens einen Netzwerk Zugriffs Server- \( VPN-Server, drahtlosen Zugriffspunkt, authentifizier enden Switch oder DFÜ-Server \) oder NPS-Proxy, der physisch im Netzwerk installiert ist.

## <a name="configure-the-network-access-server"></a>Konfigurieren des Netzwerk Zugriffs Servers

Verwenden Sie dieses Verfahren, um Netzwerk Zugriffs Server für die Verwendung mit NPS zu konfigurieren. Wenn Sie Netzwerk Zugriffs Server (Network Access Server, nass) als RADIUS-Clients bereitstellen, müssen Sie die Clients für die Kommunikation mit dem NPSS konfigurieren, bei dem der nass als Clients konfiguriert ist.

Diese Vorgehensweise bietet allgemeine Richtlinien für die Einstellungen, die Sie zum Konfigurieren von "nass" verwenden sollten. spezifische Anweisungen zum Konfigurieren des Geräts, das Sie in Ihrem Netzwerk bereitstellen, finden Sie in der NAS-Produktdokumentation.

### <a name="to-configure-the-network-access-server"></a>So konfigurieren Sie den Netzwerk Zugriffs Server

1. Wählen Sie auf dem NAS **in RADIUS**-Einstellungen **RADIUS-Authentifizierung** auf UDP-Port **1812** (User Datagram Protocol) und RADIUS-Konto **Führung** über UDP-Port **1813**aus.
2. Geben Sie unter **Authentifizierungsserver** oder **RADIUS-Server**je nach den Anforderungen des NAS ihren NPS nach IP-Adresse oder vollständig qualifizierter Domänen Name (Fully Qualified Domain Name, FQDN) an.
3. Geben Sie unter **geheimer** Schlüssel oder **gemeinsamer geheimer**Schlüssel ein sicheres Kennwort ein. Wenn Sie NAS als RADIUS-Client in NPS konfigurieren, verwenden Sie das gleiche Kennwort, und vergessen Sie es nicht.
4. Wenn Sie PEAP oder EAP als Authentifizierungsmethode verwenden, konfigurieren Sie das NAS für die Verwendung der EAP-Authentifizierung.
5. Wenn Sie einen drahtlosen Zugriffspunkt konfigurieren, geben Sie in **SSID**einen Service Set Identifier \( -SSID an \) . Hierbei handelt es sich um eine alphanumerische Zeichenfolge, die als Netzwerkname fungiert. Dieser Name wird von Zugriffs Punkten an drahtlose Clients übertragen und ist für Benutzer mit WLAN \( - \) Hotspots sichtbar.
6. Wenn Sie einen drahtlosen Zugriffspunkt konfigurieren, aktivieren Sie in **802.1 x und WPA**die **IEEE 802.1 x-Authentifizierung** , wenn Sie PEAP-MS-CHAP v2, PEAP-TLS oder EAP-TLS bereitstellen möchten.

## <a name="add-the-network-access-server-as-a-radius-client-in-nps"></a>Hinzufügen des Netzwerk Zugriffs Servers als RADIUS-Client in NPS

Verwenden Sie dieses Verfahren, um einen Netzwerk Zugriffs Server als RADIUS-Client in NPS hinzuzufügen. Mit diesem Verfahren können Sie ein NAS-Element als RADIUS-Client mithilfe der NPS-Konsole konfigurieren.

Sie müssen Mitglied der Gruppe **Administratoren** sein, um diesen Vorgang auszuführen.

### <a name="to-add-a-network-access-server-as-a-radius-client-in-nps"></a>So fügen Sie einen Netzwerk Zugriffs Server als RADIUS-Client in NPS hinzu

1. Klicken Sie auf dem NPS in Server-Manager auf **Extras, und klicken Sie dann**auf **Netzwerk Richtlinien Server**. Die NPS-Konsole wird geöffnet.
2. Doppelklicken Sie in der NPS-Konsole auf **RADIUS-Clients und-Server**. Klicken Sie mit der rechten Maustaste auf **RADIUS-Clients**und dann auf **Neuer RADIUS-Client**.
3. Vergewissern Sie sich, dass im **neuen RADIUS-Client**das Kontrollkästchen **diesen RADIUS-Client aktivieren aktiviert** ist.
4. Geben Sie im **neuen RADIUS-Client**unter Anzeige **Name**einen anzeigen Amen für das NAS ein. Geben Sie unter **Adresse (IP oder DNS)** die NAS-IP-Adresse oder den voll qualifizierten Domänen Namen (FQDN) ein. Wenn Sie den FQDN eingeben, klicken Sie auf **überprüfen** , wenn Sie überprüfen möchten, ob der Name richtig ist und einer gültigen IP-Adresse zugeordnet ist.
5. Geben Sie im **neuen RADIUS-Client**unter **Hersteller**den Namen des NAS-Herstellers an. Wenn Sie sich nicht sicher sind, ob der NAS-Hersteller den Namen hat, wählen Sie **RADIUS Standard**aus.
6. Führen Sie unter " **gemeinsamer geheimer**Schlüssel" unter " **Neuer RADIUS-Client**" einen der folgenden Schritte aus:
    - Stellen Sie sicher, dass **manuell** ausgewählt ist, und geben Sie dann unter **gemeinsames Geheimnis**das sichere Kennwort ein, das auch im NAS eingegeben wird. Geben Sie den gemeinsamen geheimen Schlüssel in **Confirm Shared Secret**erneut ein.
    - Wählen Sie **generieren**aus, und klicken Sie dann auf **generieren** , um automatisch ein gemeinsames Geheimnis zu generieren. Speichern Sie den generierten gemeinsamen geheimen Schlüssel für die Konfiguration auf dem NAS, damit er mit dem NPS kommunizieren kann.
7. Wenn Sie in **neuem RADIUS-Client**unter **zusätzliche Optionen**andere Authentifizierungsmethoden als EAP und PEAP verwenden und Ihr NAS die Verwendung des Message Authenticator-Attributs unterstützt, wählen Sie **Zugriffs Anforderungs Nachrichten müssen das Message Authenticator-Attribut enthalten**.
8. Klicken Sie auf **OK**. Ihr NAS wird in der Liste der auf dem NPS konfigurierten RADIUS-Clients angezeigt.

## <a name="configure-radius-clients-by-ip-address-range-in-windows-server-2016-datacenter"></a>Konfigurieren von RADIUS-Clients nach IP-Adressbereich in Windows Server 2016 Datacenter

Wenn Sie Windows Server 2016 Datacenter ausführen, können Sie RADIUS-Clients in NPS nach IP-Adressbereich konfigurieren. Dadurch können Sie der NPS-Konsole eine große Anzahl von RADIUS-Clients (z. b. drahtlos Zugriffspunkte) gleichzeitig hinzufügen, anstatt jeden RADIUS-Client einzeln hinzuzufügen.

Sie können RADIUS-Clients nicht durch den IP-Adressbereich konfigurieren, wenn Sie NPS unter Windows Server 2016 Standard ausführen.

Verwenden Sie dieses Verfahren, um eine Gruppe von Netzwerk Zugriffs Servern (nass) als RADIUS-Clients hinzuzufügen, die alle mit IP-Adressen desselben IP-Adress Bereichs konfiguriert sind.

Alle RADIUS-Clients im Bereich müssen dieselbe Konfiguration und denselben gemeinsamen geheimen Schlüssel verwenden.

Sie müssen Mitglied der Gruppe **Administratoren** sein, um diesen Vorgang auszuführen.

### <a name="to-set-up-radius-clients-by-ip-address-range"></a>So richten Sie RADIUS-Clients anhand des IP-Adress Bereichs ein

1. Klicken Sie auf dem NPS in Server-Manager auf **Extras, und klicken Sie dann**auf **Netzwerk Richtlinien Server**. Die NPS-Konsole wird geöffnet.
2. Doppelklicken Sie in der NPS-Konsole auf **RADIUS-Clients und-Server**. Klicken Sie mit der rechten Maustaste auf **RADIUS-Clients**und dann auf **Neuer RADIUS-Client**.
3. Geben Sie im **neuen RADIUS-Client**unter Anzeige **Name**einen anzeigen Amen für die Auflistung von nass ein.
4. Geben Sie unter **Adress \( - \) IP oder DNS**den IP-Adressbereich für die RADIUS-Clients ein, indem Sie die \( CIDR-Notation für das Domänen übergreifende Routing von Domänen \) Wenn beispielsweise der IP-Adressbereich für "nass" 10.10.0.0 lautet, geben Sie **10.10.0.0/16**ein.
5. Geben Sie im **neuen RADIUS-Client**unter **Hersteller**den Namen des NAS-Herstellers an. Wenn Sie sich nicht sicher sind, ob der NAS-Hersteller den Namen hat, wählen Sie **RADIUS Standard**aus.
6. Führen Sie unter " **gemeinsamer geheimer**Schlüssel" unter " **Neuer RADIUS-Client**" einen der folgenden Schritte aus:
    - Stellen Sie sicher, dass **manuell** ausgewählt ist, und geben Sie dann unter **gemeinsames Geheimnis**das sichere Kennwort ein, das auch im NAS eingegeben wird. Geben Sie den gemeinsamen geheimen Schlüssel in **Confirm Shared Secret**erneut ein.
    - Wählen Sie **generieren**aus, und klicken Sie dann auf **generieren** , um automatisch ein gemeinsames Geheimnis zu generieren. Speichern Sie den generierten gemeinsamen geheimen Schlüssel für die Konfiguration auf dem NAS, damit er mit dem NPS kommunizieren kann.
7. Wenn Sie in **neuem RADIUS-Client**unter " **zusätzliche Optionen**" andere andere Authentifizierungsmethoden als EAP und PEAP verwenden und all Ihre Unterstützung für das Message Authenticator-Attribut verwenden, **müssen Sie die Option Zugriffs Anforderungs Nachrichten müssen das Message Authenticator-Attribut enthalten**.
8. Klicken Sie auf **OK**. Ihr nass wird in der Liste der auf dem NPS konfigurierten RADIUS-Clients angezeigt.

Weitere Informationen finden Sie unter [RADIUS-Clients](nps-radius-clients.md).

Weitere Informationen zu NPS finden Sie unter [Netzwerk Richtlinien Server (Network Policy Server, NPS)](nps-top.md).