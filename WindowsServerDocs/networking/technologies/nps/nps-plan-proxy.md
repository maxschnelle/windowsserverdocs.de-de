---
title: Planen eines NPS als RADIUS-Proxy
description: Dieses Thema enthält Informationen zur Planung der Bereitstellung in Windows Server 2016 Network Policy Server RADIUS-Proxy-Bereitstellung.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: ca77d64a-065b-4bf2-8252-3e75f71b7734
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 83fbe57ee62480439190dcc53428e02a4f8e6897
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59829561"
---
# <a name="plan-nps-as-a-radius-proxy"></a>Planen eines NPS als RADIUS-Proxy

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Bei der Bereitstellung (Network Policy Server, NPS) als ein Remote Authentication Dial-in User Service \(RADIUS\) NPS-Proxy empfangen verbindungsanforderungen von RADIUS-Clients, z. B. Netzwerkzugriffsserver oder anderen RADIUS-Proxys, und klicken Sie dann leitet diese Weiterleitung von verbindungsanforderungen an den Server mit NPS oder andere RADIUS-Server weiter. Sie können diese Richtlinien für die projektplanung verwenden, um Ihre RADIUS-serverbereitstellung zu vereinfachen.

Diese Richtlinien für die projektplanung enthalten keine Situationen, in denen Sie NPS als RADIUS-Server bereitstellen möchten. Wenn Sie NPS als RADIUS-Server bereitstellen, führt NPS-Authentifizierung, Autorisierung und Kontoführung für die Weiterleitung von verbindungsanforderungen für die lokale Domäne sowie für Domänen, die die lokale Domäne vertrauen.

Bevor Sie NPS als RADIUS-Proxy in Ihrem Netzwerk bereitstellen, verwenden Sie die folgenden Richtlinien, um die Planung Ihrer Bereitstellung.

- Planen Sie die NPS-Konfiguration.

- Planen Sie die RADIUS-Clients.

- Planen Sie die RADIUS-Remoteservergruppen.

- Planen Sie die Manipulation-Regeln für die nachrichtenweiterleitung Attribut.

- Planen Sie Verbindungsanforderungsrichtlinien.

- Planen Sie die NPS-Kontoführung.

## <a name="plan-nps-configuration"></a>Planen der NPS-Konfiguration

Wenn Sie NPS als RADIUS-Proxy verwenden, leitet NPS verbindungsanforderungen an einen Netzwerkrichtlinienserver oder andere RADIUS-Server zur Verarbeitung weiter. Aus diesem Grund ist die Domänenmitgliedschaft des NPS-Proxy nicht relevant. Der Proxy muss nicht in Active Directory-Domänendiensten registriert sein \(AD DS\) , da kein Zugriff auf die DFÜ-Eigenschaften von Benutzerkonten erforderlich ist. Darüber hinaus müssen Sie keine Netzwerkrichtlinien auf einem NPS-Proxy zu konfigurieren, da der Proxy keine Autorisierung für verbindungsanforderungen durchführt. Der NPS-Proxy kann Mitglied einer Domäne oder einem eigenständigen Server mit ohne Domänenmitgliedschaft sind möglich.

NPS muss für die Kommunikation mit RADIUS-Clients, die so genannte Netzwerkzugriffsserver, mit dem RADIUS-Protokoll konfiguriert werden. Darüber hinaus können Sie den Typen von Ereignissen von aufgezeichneten NPS konfigurieren den Fall, und Sie eine Beschreibung für den Server eingeben können.

### <a name="key-steps"></a>Wichtige Schritte

Bei der Planung für die NPS-Proxykonfiguration, können Sie die folgenden Schritte aus.

- Bestimmen Sie die RADIUS-Ports, die der NPS-Proxy zum Empfangen von RADIUS-Nachrichten von RADIUS-Clients und zum Senden von RADIUS-Nachrichten an die Mitglieder von RADIUS-Remoteservergruppen verwendet. Die Standardports für die User Datagram Protocol (UDP) sind 1812 und 1645 für RADIUS-Authentifizierungsnachrichten und UDP-Ports 1813 und 1646 für RADIUS-Kontoführungsnachrichten.

- Wenn der NPS-Proxy mit mehreren Netzwerkadaptern konfiguriert ist, ermitteln Sie die Adapter, die über denen RADIUS-Datenverkehr zugelassen werden soll.

- Geben Sie die Typen von Ereignissen, die auf die im Ereignisprotokoll aufgezeichnet werden sollen. Sie können abgelehnte verbindungsanforderungen, erfolgreichen Weiterleitung von verbindungsanforderungen oder beides protokollieren.

- Bestimmen Sie, ob Sie mehr als ein NPS-Proxy bereitstellen. Um Fehlertoleranz bereitzustellen, müssen verwenden Sie mindestens zwei NPS-Proxys. NPS Proxy als des primären RADIUS-Proxys verwendet wird, und der andere als Sicherung verwendet wird. Jeden RADIUS-Client ist für beide Proxys NPS konfiguriert. Wenn der primäre NPS-Proxy nicht verfügbar ist, senden RADIUS-Clients dann Access-Request-Nachrichten an den alternativen NPS-Proxy.

- Planen Sie das Skript verwendet, um eine Konfiguration der NPS-Proxy gegenüber anderen Proxys NPS, um auf den administrativen Aufwand zu speichern und zu verhindern, dass die falsche Konfiguration eines Servers zu kopieren. NPS enthält die Netsh-Befehle, die Sie kopieren oder einen Teil einer NPS-Proxykonfiguration für den Import in einer anderen NPS-Proxy zu ermöglichen. Sie können die Befehle an der Eingabeaufforderung Netsh manuell ausführen. Aber wenn Sie Ihre Befehlssequenz als Skript speichern, können Sie das Skript ausführen zu einem späteren Zeitpunkt, wenn Sie die Proxykonfigurationen ändern möchten.

## <a name="plan-radius-clients"></a>Planen der RADIUS-clients

RADIUS-Clients sind Netzwerkzugriffsserver, z. B. Drahtloszugriffspunkte, virtuelles privates Netzwerk \(VPN\) Servern, 802.1 X-fähigen Switches und DFÜ-Server. RADIUS-Proxys, die Verbindung Anforderungsnachrichten an den RADIUS-Server weiterleiten, sind auch die RADIUS-Clients. NPS unterstützt alle Netzwerkzugriffsserver und RADIUS-Proxys, die mit dem RADIUS-Protokoll zu erfüllen, wie beschrieben in RFC 2865, "Remote Authentication Dial-in User Service \(RADIUS\)," und die RFC 2866 unter "RADIUS-Kontoführung."

Darüber hinaus müssen sowohl der drahtlose Zugriffspunkte als auch der Schalter der 802.1X-Authentifizierung können. Wenn Sie Extensible Authentication Protocol (EAP) oder PEAP Protected Extensible Authentication Protocol () bereitstellen möchten, müssen die Verwendung von EAP Zugriffspunkten und Switches unterstützt werden.

Konfigurieren Sie den Zugriffspunkt und dem Zugriffsclient Password Authentication Protocol (PAP) verwenden, um grundlegende Interoperabilität für PPP-Verbindungen für drahtlose Zugriffspunkte zu testen. Verwenden Sie zusätzliche PPP-basierte Authentifizierungsprotokolle wie z. B. PEAP, bis Sie diejenigen getestet haben, die Sie für den Zugriff auf das Netzwerk verwenden möchten.

### <a name="key-steps"></a>Wichtige Schritte

Bei der Planung für RADIUS-Clients, können Sie die folgenden Schritte aus.

- Dokumentieren Sie die anbieterspezifische-Attribute (VSA), die Sie in NPS konfigurieren müssen. Wenn Ihre Netzwerkzugriffsserver VSAs benötigen, melden Sie die VSA-Informationen für die spätere Verwendung, wenn Sie Ihren Netzwerkrichtlinien in NPS konfigurieren.

- Dokumentieren Sie die IP-Adressen der RADIUS-Clients und der NPS-Proxy, um die Konfiguration aller Geräte zu vereinfachen. Wenn Sie Ihre RADIUS-Clients bereitstellen, müssen Sie sie an, um das RADIUS-Protokoll mit der NPS-Proxy IP-Adresse eingegeben haben, als authentifizierendem Server verwenden, konfigurieren. Und wenn Sie NPS für die Kommunikation mit Ihrem RADIUS-Clients konfigurieren, müssen Sie die RADIUS-Client-IP-Adressen eingeben, in der NPS-Snap-in.

- Erstellen Sie gemeinsame geheime Schlüssel für die Konfiguration aus, auf den RADIUS-Clients und der NPS-Snap-in. Sie müssen den RADIUS-Clients konfigurieren, mit einem gemeinsamen geheimen Schlüssel oder Kennwort mit der Sie auch in der NPS-Snap-in beim Konfigurieren der RADIUS-Clients in NPS eingeben.

## <a name="plan-remote-radius-server-groups"></a>Planen der RADIUS-Remoteservergruppen

Wenn Sie eine remote-RADIUS-Servergruppe auf NPS-Proxy konfigurieren, sagen Sie dem NPS-Proxy, wo Sie einige oder alle Verbindung Anforderungsnachrichten zu senden, die von Netzwerkzugriffsservern und NPS-Proxys oder anderen RADIUS-Proxys empfangen.

Sie können NPS als RADIUS-Proxy zum Weiterleiten von Verbindung, auf eine anfordert oder mehr RADIUS-Remoteservergruppen und jede Gruppe kann eine oder mehrere RADIUS-Server enthalten. Wenn Sie möchten, dass den NPS-Proxy zum Weiterleiten von Nachrichten an mehrere Gruppen, konfigurieren Sie eine Verbindungsanforderungsrichtlinie pro Gruppe. Die Verbindungsanforderungsrichtlinie enthält zusätzliche Informationen, z. B. Attribut Manipulation Regeln, die dem NPS-Proxy, welche Nachrichten mitzuteilen an die remote-RADIUS-Servergruppe in der Richtlinie angegeben.

Sie können mithilfe von Netsh-Befehle für den NPS, indem Sie Gruppen direkt in der NPS-Snap-in unter RADIUS-Remoteservergruppen konfigurieren oder durch Ausführen des Assistenten für neue Verbindungsanforderungsrichtlinie RADIUS-Remoteservergruppen konfigurieren.

### <a name="key-steps"></a>Wichtige Schritte

Bei der Planung für die RADIUS-Remoteservergruppen, können Sie die folgenden Schritte aus.

- Bestimmen Sie die Domänen, die die RADIUS-Server enthalten, an denen den NPS-Proxy zum Weiterleiten von verbindungsanforderungen werden sollen. Diese Domänen enthalten die Benutzerkonten für Benutzer, die über den RADIUS-Clients mit dem Netzwerk verbunden sind, die Sie bereitstellen.

- Bestimmen Sie, ob Sie müssen neue RADIUS-Server in Domänen hinzufügen, in denen RADIUS nicht bereits bereitgestellt wurde.

- Dokumentieren Sie die IP-Adressen der RADIUS-Server, die Sie remote-RADIUS-Servergruppen hinzufügen möchten.

- Bestimmen Sie, wie viele RADIUS-Remoteservergruppen Sie erstellen müssen. In einigen Fällen empfiehlt es sich um eine remote-RADIUS-Servergruppe pro Domäne zu erstellen, und klicken Sie dann die RADIUS-Server für die Domäne zur Gruppe hinzufügen. Aber es gibt möglicherweise Fälle, in denen Sie eine große Menge an Ressourcen in einer Domäne, einschließlich eine große Anzahl von Benutzern mit den Benutzerkonten in der Domäne, eine große Anzahl von Domänencontrollern und eine große Anzahl von RADIUS-Server haben. Oder Ihrer Domäne möglicherweise einen großen geografischen Bereich, verursacht Sie Netzwerkzugriffsserver und RADIUS-Server an Speicherorten, die voneinander entfernten behandelt. In dieser und möglicherweise anderen Fällen können Sie mehrere RADIUS-Remoteservergruppen pro Domäne erstellen.

- Erstellen Sie gemeinsame geheime Schlüssel für die Konfiguration aus, auf dem NPS-Proxy, und klicken Sie auf den remote-RADIUS-Servern.

## <a name="plan-attribute-manipulation-rules-for-message-forwarding"></a>Planen der Attribut-Manipulation-Regeln für die nachrichtenweiterleitung

Attribut-Manipulation-Regeln, die in den Verbindungsanforderungsrichtlinien konfiguriert sind, können Sie die Access-Request-Nachrichten zu identifizieren, die an einer bestimmten RADIUS-Remoteservergruppe weitergeleitet werden sollen.

Sie können NPS, um alle verbindungsanforderungen an einen RADIUS-Remoteservergruppe weitergeleitet werden, ohne Attribut Manipulation Regeln konfigurieren.

Wenn Sie mehr als einem Speicherort verfügen, um die verbindungsanforderungen weitergeleitet werden soll, Sie jedoch müssen für jeden Standort eine Verbindungsanforderungsrichtlinie zu erstellen, und konfigurieren Sie die Richtlinie mit dem remote-RADIUS-Servergruppe, Nachrichten weitergeleitet werden soll, sowie mit den Regeln der Attribut-Bearbeitung, die NPS, welche Nachrichten mitzuteilen weiterleiten.

Sie können Regeln für die folgenden Attribute erstellen.

- Wird aufgerufen,-Station-ID Die Telefonnummer des den Netzwerkzugriffsserver (NAS). Der Wert dieses Attributs ist eine Zeichenfolge. Sie können die mustervergleichssyntax verwenden, Ortskennzahlen angeben.

- Aufruf-Station-ID Die Telefonnummer des Anrufers. Der Wert dieses Attributs ist eine Zeichenfolge. Sie können die mustervergleichssyntax verwenden, Ortskennzahlen angeben.

- Benutzername. Der Benutzername, der von der Access-Client bereitgestellt wird und, die vom NAS in der RADIUS-Access-Request-Nachricht enthalten ist. Der Wert dieses Attributs ist eine Zeichenfolge, die einen Bereichsnamen und einen Benutzerkontonamen in der Regel enthält.

Um ordnungsgemäß zu ersetzen, oder konvertieren Bereichsnamen in den Namen des eine verbindungsanforderung, müssen Sie auf der entsprechenden Verbindungsanforderungsrichtlinie Attribut Manipulation-Regeln für das User-Name-Attribut konfigurieren.

### <a name="key-steps"></a>Wichtige Schritte

Bei der Planung für die Bearbeitung Attributmanipulationsregeln, können Sie die folgenden Schritte aus.

- Planen Sie das routing von Nachrichten aus der NAS über den Proxy auf die RADIUS-Remoteserver, um sicherzustellen, dass Sie einen logischen Pfad mit dem Weiterleiten von Nachrichten an den RADIUS-Servern verfügen.

- Bestimmen Sie eine oder mehrere Attribute, die Sie für jede Verbindungsanforderungsrichtlinie verwenden möchten.

- Dokumentieren Sie die Attribut-Manipulation-Regeln, die Sie für jede Verbindungsanforderungsrichtlinie verwenden möchten, und entsprechen Sie die Regeln für die remote-RADIUS-Servergruppe an der Nachrichten weitergeleitet werden.

## <a name="plan-connection-request-policies"></a>Planen der Verbindungsanforderungsrichtlinien

Die Standard-Verbindungsanforderungsrichtlinie ist für den NPS konfiguriert, wenn er als RADIUS-Server verwendet wird. Zusätzliche Verbindungsanforderungsrichtlinien können verwendet werden, spezifischere Bedingungen definieren, Attribut bearbeiten Regeln erstellen, die NPS mitzuteilen, welche Nachrichten, die zum Weiterleiten an den RADIUS-Remoteservergruppen und erweiterter Attribute angeben. Verwenden Sie den Assistenten für neue Verbindungen, um allgemeine oder benutzerdefinierte Verbindungs-Request-Richtlinien zu erstellen.

### <a name="key-steps"></a>Wichtige Schritte

Bei der Planung für Verbindungsanforderungsrichtlinien, können Sie die folgenden Schritte aus.

- Löschen Sie die Standard-Verbindungsanforderungsrichtlinie auf jedem Server mit NPS, Funktionen ausschließlich als RADIUS-Proxy.

- Planen Sie zusätzliche Bedingungen und Einstellungen, die für jede Richtlinie erforderlich sind, kombinieren diese Informationen, mit der remote-RADIUS-Servergruppe und die Attribut-Manipulation-Regeln für die Richtlinie geplant.

- Entwerfen Sie den Plan aus, um allgemeine Verbindungsanforderungsrichtlinien auf alle NPS-Proxys zu verteilen. Erstellen von Richtlinien für einen Netzwerkrichtlinienserver üblich, mehrere NPS-Proxys, und klicken Sie dann die Netsh-Befehle für den NPS verwenden, um die Verbindung Anforderung Richtlinien und die Serverkonfiguration für alle anderen Proxys zu importieren.

## <a name="plan-nps-accounting"></a>Planen Sie die NPS-Kontoführung

Wenn Sie NPS als RADIUS-Proxy konfigurieren, können Sie es zum Ausführen von RADIUS-Kontoführung mithilfe der NPS-Datenbankformat-Protokolldateien, datenbankkompatibles-Datenbankformat-Protokolldateien und NPS SQL Server-Protokollierung konfigurieren.

Sie können auch Kontoführungsnachrichten an einen RADIUS-Remoteservergruppe weiterleiten, die Buchhaltung ausführt, mithilfe eines der folgenden Protokollierungsformate.

### <a name="key-steps"></a>Wichtige Schritte

Bei der Planung für die NPS-Kontoführung, können Sie die folgenden Schritte aus.

- Bestimmen Sie, ob den NPS-Proxy, Buchhaltung Dienste ausführen oder Kontoführungsnachrichten an einen RADIUS-Remoteservergruppe für die Kontoführung weiterzuleiten.

- Deaktivieren die lokalen NPS-Proxy, accounting, wenn Sie planen, Kontoführungsnachrichten an andere Server weiterleiten möchten.

- Planen Sie verbindungsschritte für die Anforderung Richtlinienkonfiguration, wenn Sie planen, Kontoführungsnachrichten an andere Server weiterleiten. Wenn Sie die lokalen Kontoführung für den NPS-Proxy deaktivieren, müssen jedes Verbindungsanforderungsrichtlinie, die Sie auf diesen Proxy konfigurieren berücksichtigt die nachrichtenweiterleitung aktiviert und ordnungsgemäß konfiguriert.

- Bestimmen Sie die Protokollierungsformat, das Sie verwenden möchten: IAS-Datenbankformat-Protokolldateien, datenbankkompatibles Format Protokolldateien oder NPS SQL Server-Protokollierung.

Um einen Lastenausgleich für NPS als RADIUS-Proxy konfigurieren zu können, finden Sie unter [NPS Proxy Server Load Balancing](nps-manage-proxy-lb.md).

