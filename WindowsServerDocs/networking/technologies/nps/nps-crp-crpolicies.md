---
title: Verbindungsanforderungsrichtlinien
description: Dieses Thema enthält eine Übersicht über Netzwerkrichtlinienserver Verbindungsanforderungsrichtlinien in Windows Server 2016.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 4ec45e0c-6b37-4dfb-8158-5f40677b0157
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 496ba87597b0be6cad1109269d2f72f52de017f1
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="connection-request-policies"></a>Verbindungsanforderungsrichtlinien

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

In diesem Thema können Sie Informationen zum NPS-Verbindungsanforderungsrichtlinien so konfigurieren Sie den NPS-Server als RADIUS-Server, RADIUS-Proxy oder beides verwenden.

>[!NOTE]
>Zusätzlich zu diesem Thema ist die folgende Dokumentation zum Verbindungs-Anforderung Richtlinie verfügbar.
> - [Konfigurieren von Verbindungsanforderungsrichtlinien](nps-crp-configure.md)
> - [Konfigurieren von RADIUS-Remoteservergruppen](nps-crp-rrsg-configure.md)

Verbindungsanforderungsrichtlinien sind Bedingungen und Einstellungen, mit denen Netzwerkadministratoren festlegen, welche Server Remote Authentication Dial-in User Service (RADIUS) führen Sie die Authentifizierung und Autorisierung von verbindungsanforderungen an, denen den Netzwerkrichtlinienserver (Network Policy Server, NPS) von RADIUS-Clients empfängt. Verbindungsanforderungsrichtlinien können konfiguriert werden, um festzulegen, welche RADIUS-Server für RADIUS-Kontoführung verwendet werden.

Sie können Verbindung erstellen Verbindungsanforderungsrichtlinien so, dass einige RADIUS-Anforderungsnachrichten von RADIUS-Clients lokal verarbeitet werden (NPS als RADIUS-Server verwendet wird) und andere Typen von Nachrichten an einen anderen RADIUS-Server (NPS als RADIUS-Proxy verwendet wird) weitergeleitet werden.

Mit Verbindungsanforderungsrichtlinien können Sie NPS als RADIUS-Server oder als RADIUS-Proxy, anhand verschiedener Faktoren wie den folgenden verwenden: 

- Die Uhrzeit und Tag der Woche
- Den Bereichsnamen in der Anfrage
- Die Art der Verbindung angefordert wird
- Die IP-Adresse des RADIUS-Clients

RADIUS-Zugriffsanforderung Nachrichten werden nur dann, wenn die Einstellungen der eingehenden Nachricht mindestens eines der Verbindungsanforderungsrichtlinien auf dem NPS-Server konfigurierten übereinstimmen NPS übermittelt oder verarbeitet. 

Wenn die Einstellungen übereinstimmen, und die Richtlinie erfordert, dass der NPS-Server die Nachricht nicht verarbeiten, fungiert als RADIUS-Server, NPS, Authentifizierung und Autorisierung der Anforderung der Verbindung. Wenn die Einstellungen übereinstimmen, und die Richtlinie erfordert, dass der NPS-Server die Nachricht weiterleitet, wird NPS als RADIUS-Proxy fungiert und leitet die Anforderung der Verbindung an einen RADIUS-Remoteserver für die Verarbeitung.

Wenn die Einstellungen einer eingehenden Nachricht von RADIUS-Zugriffsanforderung nicht mindestens eines der Verbindungsanforderungsrichtlinien übereinstimmen, wird eine Access-Reject-Nachricht an den RADIUS-Client gesendet und der Benutzer oder Computer mit dem Netzwerk herzustellen versuchen, Zugriff verweigert wird.

## <a name="configuration-examples"></a>Beispiele für die Anwendungskonfiguration

Die folgenden Konfigurationsbeispiele veranschaulichen, wie Sie Verbindungsanforderungsrichtlinien verwenden können.

### <a name="nps-as-a-radius-server"></a>NPS als RADIUS-server

Die standardmäßige Verbindungsanforderungsrichtlinie ist die einzige konfigurierte Richtlinie. In diesem Beispiel NPS als RADIUS-Server konfiguriert ist, und alle verbindungsanforderungen von den lokalen Netzwerkrichtlinienserver verarbeitet werden. Der NPS-Server kann authentifizieren und Autorisieren von Benutzern, deren Konten in der Domäne des Netzwerkrichtlinienservers und in vertrauenswürdigen Domänen befinden.


### <a name="nps-as-a-radius-proxy"></a>NPS als RADIUS-proxy

Die standardmäßige Verbindungsanforderungsrichtlinie wird gelöscht, und zwei neue Verbindungsanforderungsrichtlinien werden erstellt, um Anfragen an zwei verschiedene Domänen weiterleiten. In diesem Beispiel wird NPS als RADIUS-Proxy konfiguriert. NPS werden alle Verbindungsanfragen auf dem lokalen Server nicht verarbeitet. Stattdessen werden die verbindungsanforderungen weitergeleitet, NPS oder andere RADIUS-Server, die als Mitglieder von RADIUS-Remoteservergruppen konfiguriert sind.


### <a name="nps-as-both-radius-server-and-radius-proxy"></a>NPS als RADIUS-Server und RADIUS-proxy

Zusätzlich zu den Standard-Verbindungsanforderungsrichtlinie wird eine neue Verbindungsanforderungsrichtlinie erstellt, die verbindungsanforderungen an einen Netzwerkrichtlinienserver oder einen anderen RADIUS-Server in einer nicht vertrauenswürdigen Domäne weiterleitet. In diesem Beispiel wird die Proxy-Richtlinie in der sortierte Liste der Richtlinien zuerst angezeigt. Wenn die verbindungsanforderung die Proxy-Richtlinie übereinstimmt, wird die verbindungsanforderung an den Radius-Server die RADIUS-Remoteservergruppe weitergeleitet. Wenn die verbindungsanforderung nicht die Proxy-Richtlinie entspricht aber der standardmäßige Verbindungsanforderungsrichtlinie entspricht, verarbeitet NPS die verbindungsanforderung auf dem lokalen Server. Wenn die verbindungsanforderung entweder Richtlinie nicht übereinstimmt, wird sie verworfen.

### <a name="nps-as-radius-server-with-remote-accounting-servers"></a>NPS als RADIUS-Server mit Remoteservern Buchhaltung

In diesem Beispiel der lokale NPS-Server ist nicht für die Kontoführung ausführen konfiguriert, und die standardmäßige Verbindungsanforderungsrichtlinie wird überarbeitet, sodass RADIUS-Kontoführungsnachrichten an einen Netzwerkrichtlinienserver oder einen anderen RADIUS-Server in einer RADIUS-Remoteservergruppe weitergeleitet werden. Zwar Kontoführungsnachrichten weitergeleitet werden, Authentifizierung und Autorisierung Nachrichten nicht weitergeleitet werden, und der lokale NPS-Server führt diese Funktionen für die lokale Domäne, und alle vertrauenswürdigen Domänen.


### <a name="nps-with-remote-radius-to-windows-user-mapping"></a>NPS mit RADIUS für die Zuordnung der Windows-Benutzer

In diesem Beispiel fungiert NPS als einen RADIUS-Server und RADIUS-Proxy für jede einzelne verbindungsanforderung durch die Authentifizierungsanforderung an einen RADIUS-Remoteserver bei der Verwendung von einem lokalen Windows-Benutzerkonto für die Autorisierung weiterleiten. Diese Konfiguration wird durch die Konfiguration der Remote-RADIUS-Attribut Windows Benutzerzuordnung als Bedingung für die Verbindungsanforderungsrichtlinie implementiert. (Darüber hinaus muss ein Benutzerkonto lokal erstellt werden, die den gleichen Namen wie das Remotebenutzerkonto hat für die Authentifizierung vom RADIUS-Remoteserver ausgeführt wird.)

## <a name="connection-request-policy-conditions"></a>Verbindung Anforderung richtlinienbedingungen

Richtlinienbedingungen für die Anforderung Verbindung werden eine oder mehrere RADIUS-Attribute, die mit den Attributen der eingehenden Nachricht RADIUS-Zugriffsanforderung verglichen werden. Wenn mehrere Bedingungen vorhanden sind, klicken Sie dann alle Bedingungen in der Verbindung die Anforderungsnachricht wurde und in der Anfrage Richtlinie in der Reihenfolge für die Richtlinie vom NPS erzwungen werden entsprechen.

Im folgenden werden die verfügbaren Bedingungsattribute, die Sie in der Verbindungsanforderungsrichtlinien konfigurieren können.

### <a name="connection-properties-attribute-group"></a>Verbindung Eigenschaften Attributgruppe

Attributgruppe Verbindungseigenschaften enthält die folgenden Attribute.

- **Farbigen Rahmen Protokoll**. Um festzulegen, die den Typ der Datenblöcke für eingehende Pakete verwendet. Beispiele sind (PPP-Protokoll), serielle Zeile SLIP (Internet Protocol), Frame Relay- und x. 25.
- **Diensttyp**. Wird verwendet, um den Typ des angeforderten Diensts festzulegen. Beispiele: farbigen Rahmen (z. B. PPP-Verbindungen) und die Anmeldeinformationen (z. B. Telnet-Verbindungen). Weitere Informationen zu RADIUS-Diensttypen finden Sie unter RFC 2865, "Remote Authentication Dial-in User Service (RADIUS)".
- **Getunnelt Typ**. Mit einer der Typ des Tunnels, der vom anfordernden Client erstellt wird. Tunneltypen gehören Point to Point Tunneling-Protokoll (PPTP) und die Layer-Two-Tunneling-Protokoll (L2TP).

### <a name="day-and-time-restrictions-attribute-group"></a>Tages- und Uhrzeitbegrenzungen Attributgruppe 

Attributgruppe Tages- und Uhrzeitbegrenzungen enthält das Tages- und Uhrzeitbegrenzungen-Attribut. Mit diesem Attribut können Sie den Wochentag und die Uhrzeit der Verbindung festlegen. Das Tag und die Uhrzeit ist relativ zum Datum und Uhrzeit des NPS-Servers.

### <a name="gateway-attribute-group"></a>Gateway-Attributgruppe

Die Gruppe der Gateway-Attribut enthält die folgenden Attribute.

- **Empfangs-ID**. Wird verwendet, um die Telefonnummer des Netzwerkzugriffsservers festzulegen. Dieses Attribut ist eine Zeichenfolge. Mustervergleichssyntax können Vorwahlen angeben.
- **NAS-Bezeichner**. Wird verwendet, um den Namen des Servers mit Network Access festzulegen. Dieses Attribut ist eine Zeichenfolge. Mustervergleichssyntax können NAS-IDs angeben.
- **NAS-IPv4-Adresse**. Mit einer Internetprotokoll Version 4 (IPv4)-Adresse des Netzwerkzugriffsservers (der RADIUS-Client). Dieses Attribut ist eine Zeichenfolge. Mustervergleichssyntax können IP-Netzwerke.
- **NAS-IPv6-Adresse**. Mit einer Internetprotokoll, Version 6 (IPv6)-Adresse des Netzwerkzugriffsservers (der RADIUS-Client). Dieses Attribut ist eine Zeichenfolge. Mustervergleichssyntax können IP-Netzwerke.
- **NAS-Porttyp**. Wird verwendet, um den Typ des Mediums verwendet der Client Zugriff festzulegen. Beispiele sind analoge Telefonleitungen (asynchron), digitale Netzwerk ISDN (Integrated Services), Tunnel oder virtuelle private Netzwerke (VPNs), IEEE 802.11 Drahtlos und Ethernet-switches.

### <a name="machine-identity-attribute-group"></a>Computer-Identität Attributgruppe

Die Computeridentität Attributgruppe enthält die Computeridentität-Attribut. Mit diesem Attribut können Sie die Methode, mit der Clients identifiziert werden, in der Richtlinie angeben.

### <a name="radius-client-properties-attribute-group"></a>RADIUS-Clienteigenschaften Attributgruppe

Die Eigenschaften des RADIUS-Client-Attributgruppe enthält die folgenden Attribute.

- **Anrufer-ID**. Wird verwendet, um die Telefonnummer des Anrufers (Client Access) festzulegen. Dieses Attribut ist eine Zeichenfolge. Mustervergleichssyntax können Vorwahlen angeben.
- **Clientanzeigenamen**. Verwendet, um den Namen des RADIUS-Client-Computers festlegen, die Authentifizierung anfordert. Dieses Attribut ist eine Zeichenfolge. Mustervergleichssyntax können Clientnamen angeben.
- **Die IPv4-Adresse des Clients**. Verwendet, um die IPv4-Adresse des Netzwerkzugriffsservers (der RADIUS-Client) festgelegt. Dieses Attribut ist eine Zeichenfolge. Mustervergleichssyntax können IP-Netzwerke.
- **Client-IPv6-Adresse**. Verwendet, um die IPv6-Adresse des Netzwerkzugriffsservers (der RADIUS-Client) festgelegt. Dieses Attribut ist eine Zeichenfolge. Mustervergleichssyntax können IP-Netzwerke.
- **Client-Anbieter**. Verwendet, um den Hersteller des Servers mit Network Access festlegen, die Authentifizierung anfordert. Ein Computer mit der Routing- und RAS-Dienst ist der Microsoft NAS-Hersteller. Dieses Attribut können Sie verschiedene Richtlinien für unterschiedliche NAS-Hersteller konfigurieren. Dieses Attribut ist eine Zeichenfolge. Sie können mustervergleichssyntax verwenden.

### <a name="user-name-attribute-group"></a>Benutzergruppe Name-Attribut

Attributgruppe Benutzernamen enthält das User Name-Attribut. Mit diesem Attribut können Sie festlegen, den Benutzernamen oder einen Teil des Benutzernamens, die den Benutzernamen, die vom Client in der RADIUS-Meldung Access bereitgestellte übereinstimmen müssen. Dieses Attribut ist eine Zeichenfolge, die in der Regel einen Bereichsnamen und einen Benutzerkontonamen enthält. Mustervergleichssyntax können Benutzernamen an.

## <a name="connection-request-policy-settings"></a>Verbindung anforderungsrichtlinieneinstellungen

Anforderungsrichtlinieneinstellungen Verbindung werden eine Reihe von Eigenschaften, die auf eine eingehende RADIUS-Nachricht angewendet werden. Einstellungen umfassen die folgenden Gruppen von Eigenschaften.

- Authentifizierung
- Kontoführung
- Attribut bearbeiten
- Weiterleitung-Anforderung
- Erweiterte

Die folgenden Abschnitte enthalten weiteren Details zu diesen Einstellungen.

### <a name="authentication"></a>Authentifizierung

Mit dieser Einstellung können Sie die Einstellungen, die in allen Netzwerkrichtlinien konfiguriert sind und überschreiben Sie Authentifizierungsmethoden und Typen, die erforderlich sind, für die Verbindung mit dem Netzwerk festlegen können.

>[!IMPORTANT]
>Wenn Sie eine Authentifizierungsmethode in der Verbindungsanforderungsrichtlinie, die weniger sicher als die Authentifizierungsmethode, die Sie in der Netzwerkrichtlinie zu konfigurieren konfigurieren, ist die sichere Authentifizierungsmethode, die Sie in der Netzwerkrichtlinie konfigurieren außer Kraft gesetzt. Z. B. Wenn Sie eine Netzwerkrichtlinie haben, erfordert die Verwendung von Protected Extensible Authentication Protocol – Microsoft Challenge Handshake Authentication Protocol Version 2 \ (PEAP-MS-CHAP v2\), ist eine kennwortbasierte Authentifizierungsmethode für sichere Wireless, konfigurieren und außerdem eine Verbindungsanforderungsrichtlinie zum Zulassen von nicht authentifizierten Zugriffs, das Ergebnis ist, dass keine Clients zur Authentifizierung mithilfe von PEAP-MS-CHAP v2 erforderlich sind. In diesem Beispiel werden alle Clients, die eine Verbindung mit Ihrem Netzwerk gewährt nicht authentifizierten Zugriff.

### <a name="accounting"></a>Kontoführung

Mit dieser Einstellung können Sie konfigurieren, Verbindungsanforderungsrichtlinie zum Weiterleiten von Daten an einen Netzwerkrichtlinienserver oder einen anderen RADIUS-Server in einer RADIUS-Remoteservergruppe, so, dass die RADIUS-Remoteservergruppe die Kontoführung ausführt.

>[!NOTE]
>Wenn Sie mehrere RADIUS-Server und Daten für alle Server in einer zentralen RADIUS-Kontoführung-Datenbank gespeichert werden sollen, können Sie die Verbindung Anforderung Buchhaltung Einstellung in einer Richtlinie auf jedem RADIUS-Server Kontoführungsdaten weitergeleitet aus allen von den Servern an einen Netzwerkrichtlinienserver oder anderen RADIUS-Server, der als Kontoführungsserver bestimmt ist.

Verbindung Buchhaltung anforderungsrichtlinieneinstellungen funktionieren unabhängig von der Buchhaltung Konfiguration des lokalen NPS-Servers. Anders ausgedrückt, wenn Sie der lokalen NPS RADIUS-Kontoführungsinformationen in einer lokalen Datei oder in einer Microsoft SQL Server-Datenbank protokollieren konfigurieren, wird er dazu unabhängig davon, ob Sie eine Verbindungsanforderungsrichtlinie zum Weiterleiten von Kontoführungsnachrichten an einen RADIUS-Remoteservergruppe konfigurieren.

Wenn Kontoführungsinformationen Remote, aber nicht lokal protokolliert werden sollen, müssen Sie den lokalen NPS-Server so, dass keine Kontoführung, gleichzeitig die Kontoführung in einer Verbindungsanforderungsrichtlinie, dass Kontoführungsdaten weitergeleitet, eine RADIUS-Remoteservergruppe konfigurieren.

### <a name="attribute-manipulation"></a>Attribut bearbeiten

Sie können eine Reihe von Suchen und Ersetzen Regeln konfigurieren, die die Textzeichenfolgen eines der folgenden Attribute bearbeiten.

- Benutzername
- Empfangs-ID
- Anrufer-ID

Suchen und Ersetzen Regel Verarbeitung tritt für eine der genannten Attribute, bevor die RADIUS-Meldung-Authentifizierung und-Kontoführung Einstellungen ist. Attribut Manipulation Regeln gelten nur für ein Attribut. Sie können keine Attribut Manipulation Regeln für jedes Attribut konfigurieren. Darüber hinaus ist die Liste der Attribute, die Sie bearbeiten können eine statische Liste. die Liste der Attribute, die für die Manipulation kann nicht hinzugefügt werden.

>[!NOTE]
>Wenn Sie das MS-CHAP v2-Authentifizierungsprotokoll verwenden, können Sie das Attribut Benutzernamen ändern, wenn die Verbindungsanforderungsrichtlinie zum Weiterleiten der RADIUS-Meldung verwendet wird. Die einzige Ausnahme tritt auf, wenn ein Schrägstrich (\) verwendet wird und die Manipulation wirkt sich nur auf die Informationen auf der linken Seite der. Ein umgekehrter Schrägstrich ist in der Regel verwendet, um einen Domänennamen (die Informationen auf der linken Seite des umgekehrten) und den Namen eines Benutzerkontos in der Domäne (die Informationen rechts neben den umgekehrten Schrägstrich) angeben. In diesem Fall dürfen nur Attribut Manipulation-Regeln, die ändern oder ersetzen den Domänennamen ein.

Beispiele für den Bereichsnamen im User Name-Attribut bearbeiten finden Sie im Abschnitt "Beispiele für die Manipulation von den Bereichsnamen im User Name-Attribut" im Thema [reguläre Ausdrücke in NPS](nps-crp-reg-expressions.md).

### <a name="forwarding-request"></a>Weiterleitung-Anforderung

Sie können festlegen, dass die folgenden Weiterleiten der Anforderung-Optionen, die für die RADIUS-Zugriffsanforderung Nachrichten verwendet werden:

- **Authentifizieren von Anforderungen auf diesem Server**. Mithilfe dieser Einstellung verwendet NPS zum Authentifizieren der verbindungsanforderung einer Windows NT 4.0-Domäne, Active Directory oder die lokale Sicherheitskontenverwaltung (Security Accounts Manager, SAM)-Benutzerkontendatenbank. Diese Einstellung gibt auch, dass die übereinstimmende Netzwerkrichtlinie auf dem Netzwerkrichtlinienserver, zusammen mit der DFÜ-Eigenschaften des Benutzerkontos, konfiguriert werden von NPS zur Autorisierung der verbindungsanforderung verwendet. In diesem Fall wird der NPS-Server konfiguriert, als RADIUS-Server ausführen.

- **Anforderungen an die folgenden RADIUS-Remoteservergruppe weiterleiten**. Mithilfe dieser Einstellung leitet NPS verbindungsanforderungen an den RADIUS-Remoteservergruppe, die Sie angeben. Wenn der NPS-Server eine gültige Access-Accept-Nachricht erhält, die die Zugriffsanforderung Nachricht entspricht, wird der Verbindungsversuch als authentifiziert und autorisiert. In diesem Fall fungiert der NPS als RADIUS-Proxy.

- **Benutzer ohne Bestätigung der Anmeldeinformationen akzeptieren**. Mit dieser Einstellung NPS überprüft nicht die Identität des Benutzers eine Verbindung mit dem Netzwerk herstellen und NPS versucht nicht, stellen Sie sicher, dass der Benutzer oder Computer das Recht hat, mit dem Netzwerk verbinden. Wenn NPS so konfiguriert ist, dass nicht authentifizierten Zugriff zulassen und eine Anforderung der Verbindung empfängt, sendet NPS sofort eine Access-Accept-Nachricht an den RADIUS-Client und den Benutzer oder Computer Zugriff auf das Netzwerk gewährt wird. Diese Einstellung wird verwendet, für einige Arten von erzwungenen Tunneln, in dem Zugriffsclient getunnelt wird, bevor Benutzeranmeldeinformationen authentifiziert werden.

>[!NOTE]
>Diese Authentifizierungsoption kann nicht verwendet werden, wenn das Authentifizierungsprotokoll des Zugriffsclients für den MS-CHAP v2 oder Extensible Authentication Protocol-Transport Layer Security (EAP-TLS) beide die gegenseitigen Authentifizierung unterstützen. Bei der gegenseitigen Authentifizierung beweist der, dass es ein gültiger Zugriffsclient der authentifizierende Server (Netzwerkrichtlinienserver ist), und der Authentifizierungsserver beweist, dass er ein gültiger Authentifizierungsserver, den der Client ist. Wenn diese Authentifizierungsoption verwendet wird, wird die Access-Accept-Meldung zurückgegeben. Allerdings der authentifizierende Server bietet keine Überprüfung auf dem Zugriffsclient und gegenseitige Authentifizierung ein Fehler auftritt.

Beispiele für die Verwendung von regulären Ausdrücken Routingregeln zu erstellen, die Weiterleiten von RADIUS-Nachrichten mit einem angegebenen Bereichsnamen an einer RADIUS-Remoteservergruppe finden Sie im Abschnitt "Beispiel für die Weiterleitung von RADIUS-Nachricht über einen Proxyserver" im Thema [reguläre Ausdrücke verwenden, auf dem Netzwerkrichtlinienserver](nps-crp-reg-expressions.md).

### <a name="advanced"></a>Erweiterte

Sie können die Reihe von RADIUS-Attribute angeben, werden erweiterte Eigenschaften festlegen:

- Der Nachricht hinzugefügt, RADIUS-Antwort Wenn der Netzwerkrichtlinienserver als RADIUS-Authentifizierung oder Kontoführungsserver verwendet wird. Wenn auf eine Netzwerkrichtlinie und der Verbindungsanforderungsrichtlinie angegebenen Attribute vorhanden sind, sind die Attribute, die in der RADIUS-Antwortnachricht gesendet werden die Kombination von zwei Sätze von Attributen.
- Bei der NPS-Server als RADIUS-Authentifizierung oder Kontoführung Proxyserver verwendet wird, ist hinzugefügt der RADIUS-Meldung. Wenn das Attribut bereits in der Meldung vorhanden, die weitergeleitet wird ist, wird es mit dem Wert des Attributs in der Verbindungsanforderungsrichtlinie angegebenen ersetzt. 

Darüber hinaus einige Attribute, die für die Konfiguration für die Verbindung verfügbar sind, fordern die Richtlinien **Einstellungen** Registerkarte die **erweitert** Kategorie spezielle Funktionen bereitstellen. Sie können z. B. Konfigurieren der **Remote-RADIUS-auf Windows-Benutzerzuordnung** Attribut, wenn Sie die Authentifizierung teilen möchten, und Autorisierung, der eine Anforderung der Verbindung zwischen zwei Benutzer Datenbanken Konten.

Die **Remote-RADIUS-auf Windows-Benutzerzuordnung** Attribut gibt an, dass Windows-Authentifizierung für Benutzer ausgeführt wird, die von einem remote-RADIUS-Server authentifiziert werden. Anders ausgedrückt, ein RADIUS-Remoteserver führt die Authentifizierung bei einem Benutzerkonto in ein remote Benutzerkonten-Datenbank, aber der lokalen NPS-Server autorisiert, die Anforderung der Verbindung mit einem Benutzerkonto in einer lokalen Benutzerkonten-Datenbank. Dies ist hilfreich, wenn Sie, dass Besucher Zugriff auf das Netzwerk möchten.

Z. B. Besucher von Partnerorganisationen können durch ihre eigenen Partner Organisation RADIUS-Server authentifiziert werden, und klicken Sie dann in Ihrer Organisation ein Windows-Benutzerkonto verwenden, auf einem Gast lokalen Netzwerks (LAN) in Ihrem Netzwerk zugreifen.

Andere Attribute, die spezielle Funktionen bereit sind:

- **MS-Quarantine-IPFilter und MS-Quarantine-Session-Timeout**. Diese Attribute werden verwendet, wenn Sie mit der Routing- und RAS VPN-Bereitstellung Network Access Quarantine Steuerelement (NAQC) bereitstellen.
- **Passport-Benutzer-Mapping-UPN-Suffix**. Dieses Attribut können Sie verbindungsanforderungen mit Windows Live™ ID-Anmeldeinformationen zu authentifizieren.
- **Tunnel-Tag**. Dieses Attribut gibt die VLAN-ID-Nummer, die Verbindung vom NAS zugewiesen wird, wenn Sie virtuelle lokale Netzwerke (VLANs) bereitstellen.

## <a name="default-connection-request-policy"></a>Standardmäßige Verbindungsanforderungsrichtlinie

Eine standardmäßige Verbindungsanforderungsrichtlinie wird erstellt, bei der Installation von NPS. Diese Richtlinie hat die folgende Konfiguration.

- Authentifizierung ist nicht konfiguriert.
- Kontoführung ist nicht für forward Kontoführungsinformationen an einen RADIUS-Remoteservergruppe konfiguriert.
- Attribut ist nicht mit dem Attribut Manipulation Regeln konfiguriert, die auf RADIUS-Remoteservergruppen verbindungsanforderungen weitergeleitet.
- Anforderung ist so konfiguriert, dass Verbindungsanfragen werden authentifiziert und, auf dem lokalen NPS-Server autorisiert.
- Erweiterte Attribute sind nicht konfiguriert.

Die standardmäßige Verbindungsanforderungsrichtlinie verwendet NPS als RADIUS-Server. Um einen Server mit NPS als RADIUS-Proxy fungieren zu konfigurieren, müssen Sie auch eine RADIUS-Remoteservergruppe konfigurieren. Sie können eine neue RADIUS-Remoteservergruppe erstellen, während Sie eine neue Verbindungsanforderungsrichtlinie mit dem Assistenten für neue Verbindung erstellen. Sie können die Standard-Verbindungsanforderungsrichtlinie löschen, oder stellen Sie sicher, dass der standardmäßige Verbindungsanforderungsrichtlinie die letzte Richtlinie vom letzten versehen, um die sortierte Liste der Richtlinien durch NPS verarbeiteten ist.

>[!NOTE]
>NPS und RAS-Dienst installiert, auf dem gleichen Computer und der RAS-Dienst für Windows-Authentifizierung konfiguriert ist, und Buchhaltung, es ist möglich, für die RAS-Authentifizierung und kontoführungsanforderungen an einen RADIUS-Server weitergeleitet wird. Dies kann vorkommen, wenn die RAS-Authentifizierung und kontoführungsanforderungen eine Verbindungsanforderungsrichtlinie übereinstimmen, die sie an einen RADIUS-Remoteservergruppe Weiterleiten konfiguriert ist.