---
title: Planen Sie NPS als RADIUS-proxy
description: Dieses Thema enthält Informationen zur Bereitstellung von Network Policy Server RADIUS-Proxy in Windows Server 2016 planen.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: ca77d64a-065b-4bf2-8252-3e75f71b7734
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 966e555ebcac6c7daf4a26b322f0d29f023f8539
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="plan-nps-as-a-radius-proxy"></a>Planen Sie NPS als RADIUS-proxy

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Bei der Bereitstellung (Network Policy Server, NPS) als Proxy Remote Authentication Dial-in User Service \(RADIUS\) NPS empfängt verbindungsanforderungen von RADIUS-Clients, z. B. Netzwerkzugriffsserver oder andere RADIUS-Proxys und leitet diese Verbindungsanfragen zum Server mit NPS oder andere RADIUS-Server weiter. Diese Richtlinien, Planung können Sie um die RADIUS-Bereitstellung zu vereinfachen.

Diese planungsempfehlungen enthalten nicht Situationen, in denen Sie NPS als RADIUS-Server bereitstellen möchten. Wenn Sie NPS als RADIUS-Server bereitstellen, führt NPS-Authentifizierung, Autorisierung und Kontoführung für verbindungsanforderungen für die lokale Domäne und Domänen, die die lokale Domäne vertrauen.

Bevor Sie NPS als RADIUS-Proxy in Ihrem Netzwerk bereitstellen, verwenden Sie die folgenden Richtlinien zum Planen der Bereitstellung.

- Planen der NPS-Serverkonfiguration.

- Planen der RADIUS-Clients.

- Planen der RADIUS-Remoteservergruppen.

- Planen Sie Attribut Manipulation Regeln zum Weiterleiten der Nachricht.

- Planen Sie Verbindungsanforderungsrichtlinien.

- Planen Sie die NPS-Kontoführung.

## <a name="plan-nps-server-configuration"></a>Planen der NPS-Serverkonfiguration

Wenn Sie NPS als RADIUS-Proxy verwenden, werden NPS verbindungsanforderungen an einem NPS-Server oder andere RADIUS-Server für die Verarbeitung weitergeleitet. Aus diesem Grund ist die Domänenmitgliedschaft des NPS-Proxys nicht relevant. Der Proxy muss nicht in Active Directory Domain Services \(AD DS\) registriert werden, weil kein Zugriff auf die DFÜ-Eigenschaften von Benutzerkonten ist. Darüber hinaus müssen Sie nicht Netzwerkrichtlinien auf einem NPS-Proxy zu konfigurieren, da der Proxy nicht Autorisierung für verbindungsanforderungen durchgeführt wird. Der NPS-Proxy kann Mitglied einer Domäne oder einem eigenständigen Server mit kein Mitglied der Domäne sein.

NPS muss konfiguriert werden, um die Kommunikation mit RADIUS-Clients, die auch als Netzwerkzugriffsserver, mit dem RADIUS-Protokoll bezeichnet. Darüber hinaus können Sie den Typen von Ereignissen, die von NPS aufgezeichnet konfigurieren im Ereignisprotokoll und eine Beschreibung für den Server eingeben können.

### <a name="key-steps"></a>Wichtige Schritte

Bei der Planung für NPS-Proxy-Konfiguration, können Sie die folgenden Schritteaus.

- Bestimmen Sie die RADIUS-Ports, die NPS-Proxy RADIUS-Nachrichten von RADIUS-Clients empfangen und Senden von RADIUS-Nachrichten an Mitglieder der RADIUS-Remoteservergruppen verwendet. Die Standardports für das User Datagram-Protokoll (UDP) sind 1812 und 1645 für RADIUS-Authentifizierungsnachrichten und UDP-Ports 1813 und 1646 für RADIUS-Kontoführungsnachrichten.

- Wenn der NPS-Proxy mit mehreren Netzwerkadaptern konfiguriert ist, bestimmen Sie die Adapter, über denen RADIUS-Datenverkehr zugelassen werden soll.

- Bestimmen der Typen von Ereignissen, die NPS im Ereignisprotokoll aufgezeichnet werden sollen. Sie können abgelehnten Verbindungsanfragen und/oder Anforderungen erfolgreich eine Verbindung protokollieren.

- Bestimmen Sie, ob Sie mehrere NPS-Proxy bereitstellen. Um Fehlertoleranz bereitzustellen, verwenden Sie mindestens zwei NPS-Proxys. Ein NPS-Proxy als des primären RADIUS-Proxys verwendet wird und das andere als Sicherung verwendet wird. Jeden RADIUS-Client wird dann auf beide NPS-Proxys konfiguriert. Wenn der primäre NPS-Proxy nicht verfügbar ist, Nachrichten RADIUS-Clients klicken Sie dann Access-Anforderung an den alternativen NPS-Proxy.

- Planen Sie das Skript verwendet, um einen NPS-Proxykonfiguration an andere NPS-Proxys, speichern Sie den Verwaltungsaufwand und falsche Konfiguration von einem Server zu kopieren. NPS enthält die Netsh-Befehle, die Ihnen ermöglichen, kopieren Sie alle oder einen Teil einer NPS-Proxy-Konfiguration auf einem anderen NPS-Proxy zu importieren. Sie können die Befehle an der Eingabeaufforderung Netsh manuell ausführen. Jedoch, wenn Sie die Befehlsfolge als Skript speichern, können Sie das Skript ausführen zu einem späteren Zeitpunkt, wenn Sie die Proxy-Konfiguration ändern möchten.

## <a name="plan-radius-clients"></a>Planen der RADIUS-clients

RADIUS-Clients sind Netzwerkzugriffsserver, z. B. Drahtloszugriffspunkte, virtuelles privates Netzwerk \(VPN\) Servern, 802.1 X-fähigen Switches und DFÜ-Server. RADIUS-Proxys, die Verbindung Anforderungsnachrichten RADIUS-Server weitergeleitet werden, sind auch RADIUS-Clients. NPS unterstützt alle Netzwerkzugriffsserver und RADIUS-Proxys, die mit dem RADIUS-Protokoll erfüllen, wie beschrieben in RFC 2865, "Remote Authentication Dial-in User Service \(RADIUS\)," und RFC 2866, "RADIUS-Kontoführung."

Drahtlose Zugriffspunkte und Switches muss außerdem der 802. 1 X-Authentifizierung. Wenn Sie die Extensible Authentication Protocol (EAP) oder Protected Extensible Authentication-Protokoll (PEAP) bereitstellen möchten, müssen Zugriffspunkte und Switches die Verwendung von EAP unterstützen.

Konfigurieren Sie zum Testen der grundlegenden Interoperabilität für PPP-Verbindungen für drahtlose Zugriffspunkte Zugriffspunkt und der Zugriffsclient (PAP = Password Authentication Protocol) verwenden. Verwenden Sie zusätzliche PPP-basierte Authentifizierungsprotokolle, wie z. B. PEAP, bis Sie diejenigen getestet haben, die Sie für den Zugriff auf das Netzwerk verwenden möchten.

### <a name="key-steps"></a>Wichtige Schritte

Bei der Planung für RADIUS-Clients können Sie die folgenden Schritte aus.

- Dokumentieren Sie die anbieterspezifische herstellerspezifische Attribute, die müssen Sie in NPS konfigurieren. Wenn Ihre Netzwerkzugriffsserver herstellerspezifische benötigen, protokollieren Sie herstellerspezifisches Attribut Informationen zur späteren Verwendung, wenn Sie auf dem Netzwerkrichtlinienserver Netzwerkrichtlinien konfigurieren.

- Dokumentieren Sie die IP-Adressen von RADIUS-Clients und der NPS-Proxy, um die Konfiguration aller Geräte zu vereinfachen. Wenn Sie Ihre RADIUS-Clients bereitstellen, müssen Sie, um die RADIUS-Protokoll, mit der NPS-Proxy IP-Adresse als der authentifizierende Server eingegeben verwenden konfigurieren. Und wenn Sie NPS zur Kommunikation mit RADIUS-Clients konfigurieren, müssen Sie die RADIUS-Client-IP-Adressen eingeben, in der NPS-Snap-in.

- Erstellen Sie gemeinsame geheime Schlüssel für die Konfiguration auf den RADIUS-Clients und dem NPS-Snap-in. Sie müssen RADIUS-Clients konfigurieren, mit einem gemeinsamen geheimen Schlüssel oder ein Kennwort, die Sie in der NPS-Snap-in beim Konfigurieren von RADIUS-Clients in NPS auch eingeben werden.

## <a name="plan-remote-radius-server-groups"></a>Planen der RADIUS-Remoteservergruppen

Wenn Sie eine RADIUS-Remoteservergruppe auf einen NPS-Proxy zu konfigurieren, werden Sie dem NPS-Proxy darüber informiert, wo Sie einige oder alle Verbindung Anforderungsnachrichten senden, die sie vom Netzwerkzugriffsserver und NPS-Proxys oder andere RADIUS-Proxys erhält.

Sie können NPS als RADIUS-Proxy zur Verbindung Weiterleiten einer anfordert oder mehr RADIUS-Remoteservergruppen und jede Gruppe kann einen oder mehrere RADIUS-Server enthalten. Wenn den NPS-Proxy Nachrichten zu mehreren Gruppen weitergeleitet werden sollen, konfigurieren Sie eine Verbindungsanforderungsrichtlinie pro Gruppe. Die Verbindungsanforderungsrichtlinie enthält zusätzliche Informationen, z. B. Attribut Manipulation Regeln, die dem NPS-Proxy, welche Nachrichten mitzuteilen an den RADIUS-Remoteservergruppe in der Richtlinie angegeben.

Sie können die RADIUS-Remoteservergruppen mithilfe von Netsh-Befehle für den NPS, indem Sie Gruppen direkt in der NPS-Snap-in unter RADIUS-Remoteservergruppen konfigurieren oder durch Ausführen des Assistenten für neue Verbindungsanforderungsrichtlinie konfigurieren.

### <a name="key-steps"></a>Wichtige Schritte

Bei der Planung für RADIUS-Remoteservergruppen, können Sie die folgenden Schritte aus.

- Bestimmen Sie die Domänen, die die RADIUS-Server enthalten, mit denen den NPS-Proxy verbindungsanforderungen weitergeleitet werden soll. Diese Domänen enthalten, die die Benutzerkonten für Benutzer, die über den RADIUS-Clients mit dem Netzwerk verbinden, die Sie bereitstellen.

- Zu ermitteln, ob Sie neue RADIUS-Server in Domänen hinzufügen, in denen RADIUS nicht bereits bereitgestellt ist.

- Dokumentieren Sie die IP-Adressen der RADIUS-Server, die Sie RADIUS-Remoteservergruppen hinzufügen möchten.

- Bestimmen Sie, wie viele RADIUS-Remoteservergruppen erstellt werden müssen. In einigen Fällen empfiehlt es sich, erstellen einen RADIUS-Remoteservergruppe pro Domäne, und klicken Sie dann die RADIUS-Server für die Domäne zur Gruppe hinzufügen. Jedoch gibt es möglicherweise Fälle, in denen Sie eine große Menge von Ressourcen in einer Domäne, z. B. eine große Anzahl von Benutzern mit Benutzerkonten in der Domäne, eine große Anzahl von Domänencontrollern und eine große Anzahl von RADIUS-Server haben. Oder Ihre Domäne möglicherweise einen großen geografischen Bereich, verursachen Sie RAS-Servern und RADIUS-Server an, die weit voneinander entfernt sind. In diesen und möglicherweise anderen Fällen können Sie mehrere RADIUS-Remoteservergruppen pro Domäne erstellen.

- Erstellen Sie gemeinsame geheime Schlüssel für die Konfiguration auf dem NPS-Proxy und den RADIUS-Servern.

## <a name="plan-attribute-manipulation-rules-for-message-forwarding"></a>Planen der Attribut Manipulation Regeln zum Weiterleiten der Nachricht

Attribut Manipulation Regeln, die im Verbindungsanforderungsrichtlinien konfiguriert sind, können Sie die Zugriffsanforderung Nachrichten zu identifizieren, die Sie an einer bestimmten RADIUS-Remoteservergruppe weiterleiten möchten.

Sie können NPS zum Weiterleiten von allen verbindungsanforderungen an einen RADIUS-Remoteservergruppe ohne Attribut Manipulation Regeln konfigurieren.

Wenn Sie mehrere Standorte verfügen, verbindungsanforderungen weitergeleitet werden soll, jedoch müssen eine Verbindungsanforderungsrichtlinie für jeden Standort erstellen Sie die Richtlinie konfigurieren, mit dem RADIUS-Remoteservergruppe, Nachrichten weitergeleitet werden sollen, sowie mit Attribut Manipulation Regeln, die NPS, welche Nachrichten mitzuteilen weiterleiten.

Sie können Regeln für die folgenden Attribute erstellen.

- Namens-Station-ID Die Telefonnummer des Netzwerkzugriffsservers (NAS). Der Wert dieses Attributs ist eine Zeichenfolge. Mustervergleichssyntax können Vorwahlen angeben.

- Aufrufen von-Station-ID Die Telefonnummer des Anrufers. Der Wert dieses Attributs ist eine Zeichenfolge. Mustervergleichssyntax können Vorwahlen angeben.

- Benutzername. Der Benutzername, der vom Zugriffsclient bereitgestellt wird und, die vom NAS in der RADIUS-Zugriffsanforderung-Nachricht enthalten ist. Der Wert dieses Attributs ist eine Zeichenfolge, die in der Regel einen Bereichsnamen und einen Benutzerkontonamen enthält.

Um ordnungsgemäß zu ersetzen oder Bereichsnamen in den Namen der Anfrage für eine Verbindung zu konvertieren, müssen Sie auf die entsprechende Verbindungsanforderungsrichtlinie Attribut Manipulation Regeln für die Benutzer-Name-Attribut konfigurieren.

### <a name="key-steps"></a>Wichtige Schritte

Bei der Planung für die Bearbeitung Attributmanipulationsregeln können Sie die folgenden Schritte aus.

- Planen Sie Nachrichtenrouting vom NAS über den Proxy an den RADIUS-Servern sicher, dass Sie einen logischen Pfad zum Weiterleiten von Nachrichten an den RADIUS-Server.

- Bestimmen Sie einen oder mehrere Attribute, die Sie für jede Verbindungsanforderungsrichtlinie verwenden möchten.

- Dokumentieren Sie das Attribut Manipulation Regeln, die Sie für jede Verbindungsanforderungsrichtlinie verwenden möchten, und entsprechen Sie die Regeln, die RADIUS-Remoteservergruppe an der Nachrichten weitergeleitet werden.

## <a name="plan-connection-request-policies"></a>Planen der Verbindungsanforderungsrichtlinien

Die standardmäßige Verbindungsanforderungsrichtlinie ist für den NPS konfiguriert, wenn es als RADIUS-Server verwendet wird. Zusätzliche Verbindungsanforderungsrichtlinien können verwendet werden, definieren spezifische Bedingungen, Attribut Manipulation Regeln erstellen, die NPS mitzuteilen, welche Nachrichten an den RADIUS-Remoteservergruppen weiterleiten und erweiterter Attribute angeben. Verwenden Sie den Assistenten für neue Verbindungen, um allgemeine oder benutzerdefinierte Verbindung Verbindungsanforderungsrichtlinien zu erstellen.

### <a name="key-steps"></a>Wichtige Schritte

Bei der Planung für Verbindungsanforderungsrichtlinien, können Sie die folgenden Schritte aus.

- Löschen Sie die Standard-Verbindungsanforderungsrichtlinie auf jedem Server mit NPS dieser Funktionen ausschließlich als RADIUS-Proxy.

- Planen Sie zusätzliche Bedingungen und Einstellungen, die für jede Richtlinie erforderlich sind, kombinieren diese Informationen mit dem RADIUS-Remoteservergruppe und das Attribut Manipulation Regeln für die Richtlinie geplant.

- Entwerfen des Plans zum allgemeinen Verbindungsanforderungsrichtlinien auf alle NPS-Proxys zu verteilen. Erstellen von Richtlinien auf einem NPS-Server für mehrere NPS-Proxys, und klicken Sie dann die Netsh-Befehle für den NPS verwenden, um die Verbindung Anforderung Richtlinien und die Serverkonfiguration auf alle anderen Proxys zu importieren.

## <a name="plan-nps-accounting"></a>Planen der NPS-Kontoführung

Wenn Sie NPS als RADIUS-Proxy konfigurieren, können Sie es zum Ausführen von RADIUS-Kontoführung mit NPS-Protokolldateien im Format, datenbankkompatiblen Format Protokolldateien oder NPS-SQL Server-Protokollierung konfigurieren.

Sie können auch Kontoführungsnachrichten an einen RADIUS-Remoteservergruppe weiterleiten, die mit einem dieser Protokollierungsformate die Kontoführung ausführt.

### <a name="key-steps"></a>Wichtige Schritte

Bei der Planung für die NPS-Kontoführung, können Sie die folgenden Schritte aus.

- Bestimmen Sie, ob den NPS-Proxy Kontoführungsdienste ausführen oder Kontoführungsnachrichten an einen RADIUS-Remoteservergruppe für die Kontoführung weitergeleitet werden soll.

- Planen von lokalen NPS-Proxy accounting, wenn Sie planen, Buchhaltung Nachrichten an andere Server weiterleiten zu deaktivieren.

- Planen Sie Verbindung Anforderung Richtlinie Konfigurationsschritte Kontoführungsnachrichten an andere Server weitergeleitet werden soll. Wenn Sie die lokalen Kontoführung für den NPS-Proxy deaktivieren, muss jeder Verbindungsanforderungsrichtlinie, die Sie auf diesen Proxy konfigurieren Kontoführung meldungsweiterleitung aktiviert und richtig konfiguriert verfügen.

- Bestimmen Sie das Protokollformat, die Sie verwenden möchten: Protokolldateien der IAS-Format, datenbankkompatiblen Format Protokolldateien oder NPS SQL Server-Protokollierung.

Konfigurieren des Netzwerklastenausgleichs für NPS als RADIUS-Proxy finden Sie in [NPS-Proxy Server Load Balancing](nps-manage-proxy-lb.md).

