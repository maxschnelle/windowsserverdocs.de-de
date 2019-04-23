---
title: Verbindungsanforderungsrichtlinien
description: Dieses Thema enthält eine Übersicht über Network Policy Server Verbindungsanforderungsrichtlinien in Windows Server 2016.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 4ec45e0c-6b37-4dfb-8158-5f40677b0157
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 21330b3838064c7b31e78ef70bdc04f0db0f50db
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59872941"
---
# <a name="connection-request-policies"></a>Verbindungsanforderungsrichtlinien

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Sie können in diesem Thema erfahren, wie Verbindungsanforderungsrichtlinien NPS verwenden, so konfigurieren Sie den NPS als RADIUS-Server, RADIUS-Proxy oder beides verwenden.

>[!NOTE]
>Zusätzlich zu diesem Thema ist die folgende richtliniendokumentation für die Verbindung Anforderung verfügbar.
> - [Konfigurieren von Verbindungsanforderungsrichtlinien](nps-crp-configure.md)
> - [Konfigurieren von Remote-RADIUS-Servergruppen](nps-crp-rrsg-configure.md)

Verbindungsanforderungsrichtlinien bestehen Sätze von Bedingungen, mit denen Netzwerkadministratoren die Remote Authentication Dial-in User Service (RADIUS)-Server festlegen können. Führen Sie der Authentifizierungs und Autorisierung der Verbindung anfordert, die die Netzwerkrichtlinienserver (Network Policy Server, NPS), Empfangen von RADIUS-Clients. Verbindungsanforderungsrichtlinien können konfiguriert werden, um festzulegen, welche RADIUS-Server für RADIUS-Kontoführung verwendet werden.

Sie können Verbindungs Anforderung Richtlinien erstellen, damit einige vom RADIUS-Clients gesendeten RADIUS-Anforderungsnachrichten lokal verarbeitet werden (NPS als RADIUS-Server verwendet wird) und andere Typen von Nachrichten an einen anderen RADIUS-Server (NPS als RADIUS-Proxy verwendet wird) weitergeleitet werden.

Mit Verbindungsanforderungsrichtlinien können Sie NPS als RADIUS-Server oder als RADIUS-Proxy, basierend auf Faktoren wie den folgenden verwenden: 

- Die Uhrzeit und Wochentag
- Der Bereichsname in der verbindungsanforderung
- Der Typ der angeforderten Verbindung
- Die IP-Adresse des RADIUS-Clients

RADIUS-Access-Request-Nachrichten werden nur dann, wenn die Einstellungen der eingehenden Nachricht mindestens eines der Verbindungsanforderungsrichtlinien, die auf dem NPS konfigurierten übereinstimmen NPS übermittelt oder verarbeitet. 

Wenn die Richtlinieneinstellungen übereinstimmen, und die Richtlinie erfordert, dass der NPS die Nachricht zu verarbeiten, fungiert NPS als RADIUS-Server, authentifizieren und autorisieren die verbindungsanforderung. Wenn mit den Richtlinieneinstellungen übereinstimmen, und die Richtlinie erfordert, dass der NPS die Nachricht weiterleitet, NPS als RADIUS-Proxy fungiert, und leitet die verbindungsanforderung an einen RADIUS-Remoteserver für die Verarbeitung.

Wenn die Einstellungen einer eingehenden RADIUS-Access-Request-Nachricht nicht mindestens eines der Verbindungsanforderungsrichtlinien übereinstimmen, eine Access-Reject-Nachricht wird an den RADIUS-Client gesendet, und der Benutzer oder Computer, die versuchen, die eine Verbindung mit dem Netzwerk herstellen, wird der Zugriff verweigert.

## <a name="configuration-examples"></a>Beispiele für

Die folgende Konfigurationsbeispiele veranschaulichen, wie Sie Verbindungsanforderungsrichtlinien verwenden können.

### <a name="nps-as-a-radius-server"></a>NPS als RADIUS-Server

Die Standard-Verbindungsanforderungsrichtlinie ist die einzige konfigurierte Richtlinie. In diesem Beispiel NPS als RADIUS-Server konfiguriert ist, und alle verbindungsanforderungen werden verarbeitet, indem Sie den lokalen NPS aus. Der NPS kann authentifizieren und Autorisieren von Benutzern, deren Konten in der Domäne der NPS-Domäne und in vertrauenswürdigen Domänen befinden.


### <a name="nps-as-a-radius-proxy"></a>NPS als RADIUS-Proxy

Die Standard-Verbindungsanforderungsrichtlinie wird gelöscht, und zwei neue Verbindungsanforderungsrichtlinien zum Weiterleiten von Anforderungen auf zwei verschiedene Domänen erstellt werden. In diesem Beispiel wird die NPS als RADIUS-Proxy konfiguriert. NPS verarbeitet keine Verbindungsanfragen auf dem lokalen Server. Stattdessen werden verbindungsanforderungen weitergeleitet NPS oder andere RADIUS-Server, die als Mitglieder von RADIUS-Remoteservergruppen konfiguriert sind.


### <a name="nps-as-both-radius-server-and-radius-proxy"></a>NPS als RADIUS-Server und RADIUS-proxy

Zusätzlich zu der Standard-Verbindungsanforderungsrichtlinie wird eine neue Verbindungsanforderungsrichtlinie erstellt, die Weiterleitung von verbindungsanforderungen an ein NPS oder anderen RADIUS-Server in einer nicht vertrauenswürdigen Domäne weiterleitet. In diesem Beispiel wird die Proxyrichtlinie in der sortierten Liste der Richtlinien zuerst angezeigt. Wenn die verbindungsanforderung die Proxyrichtlinie übereinstimmt, wird die verbindungsanforderung an den Radius-Server in der remote-RADIUS-Servergruppe weitergeleitet. Wenn die verbindungsanforderung der Proxyrichtlinie stimmt nicht überein, aber es die Standard-Verbindungsanforderungsrichtlinie entspricht, verarbeitet der NPS die verbindungsanforderung auf dem lokalen Server. Wenn die verbindungsanforderung nicht mit beiden Richtlinien übereinstimmt, wird sie verworfen.

### <a name="nps-as-radius-server-with-remote-accounting-servers"></a>NPS als RADIUS-Server, mit Remoteservern Kontoführung

In diesem Beispiel den lokalen NPS ist nicht für die Kontoführung konfiguriert, und die Standard-Verbindungsanforderungsrichtlinie wird so überarbeitet, dass eine NPS oder anderen RADIUS-Server in einer remote-RADIUS-Servergruppe RADIUS-Kontoführungsnachrichten weitergeleitet werden. Obwohl Kontoführungsnachrichten weitergeleitet werden, Authentifizierung und Autorisierung Nachrichten werden nicht weitergeleitet, und den lokalen NPS führt diese Funktionen für die lokale Domäne, und alle vertrauenswürdigen Domänen.


### <a name="nps-with-remote-radius-to-windows-user-mapping"></a>NPS mit Remote-RADIUS-Windows-benutzerzuordnung

In diesem Beispiel fungiert NPS als ein RADIUS-Server und RADIUS-Proxy für jede einzelne verbindungsanforderung durch Weiterleiten der Authentifizierungsanforderung an einen RADIUS-Remoteserver bei der Verwendung von eines lokalen Windows-Benutzerkontos für die Autorisierung an. Diese Konfiguration wird durch Konfigurieren der Remote-RADIUS-Attribut Windows Benutzerzuordnung als Bedingung für die Verbindungsanforderungsrichtlinie implementiert. (Darüber hinaus muss ein Benutzerkonto lokal erstellt werden, die den gleichen Namen wie das Remotebenutzerkonto verfügt für die Authentifizierung vom RADIUS-Remoteserver ausgeführt wird.)

## <a name="connection-request-policy-conditions"></a>Verbindung Anforderung von Bedingungen für Richtlinien

Verbindung Anforderung von Bedingungen für Richtlinien sind ein oder mehrere RADIUS-Attribute, die den Attributen der eingehenden RADIUS-Access-Request-Nachricht verglichen werden. Wenn es mehrere Bedingungen sind, alle Bedingungen in der Verbindung die Anforderungsnachricht wurde, und in der verbindungsanforderung Richtlinie übereinstimmen muss, in der Reihenfolge für die Richtlinie von NPS erzwungen werden.


Es folgen die verfügbaren Bedingungsattribute, die Sie in den Verbindungsanforderungsrichtlinien konfigurieren können.

### <a name="connection-properties-attribute-group"></a>Verbindungsgruppe Eigenschaften-Attribut

Die Attributgruppe Verbindungseigenschaften enthält die folgenden Attribute.

- **Protokoll mit einem Frame versehen**. Verwendet, um den Typ der Datenblöcke für eingehende Pakete festlegen. Beispiele sind das Point-Protokoll (PPP), (SLIP, Serial Line Internet Protocol), Frame Relay- und x. 25.
- **Diensttyp**. Verwendet, um den Typ des angeforderten Diensts festlegen. Beispiele hierfür sind (z. B. PPP-Verbindungen) mit einem Frame versehen und melden Sie sich (z. B. Telnet-Verbindungen). Weitere Informationen zu RADIUS-Diensttypen finden Sie in RFC 2865, "Remote Authentication Dial-in User Service (RADIUS)".
- **Tunneltyp**. Verwendet, um den Typ der Tunnel zu bestimmen, die vom anfordernden Client erstellt wird. Beispiele für Tunnel enthalten die Point-Tunneling-Protokoll (PPTP) und das Layer-Two-Tunneling-Protokoll (L2TP).

### <a name="day-and-time-restrictions-attribute-group"></a>Tages- und Uhrzeitbegrenzungen Attributgruppe 

Die Attributgruppe Tages- und Uhrzeitbegrenzungen enthält das Tages- und Uhrzeitbegrenzungen-Attribut. Mit diesem Attribut können Sie den Tag der Woche und die Uhrzeit des Verbindungsversuchs festlegen. Das Tag und die Uhrzeit ist relativ zu das Tag und die Uhrzeit für den NPS.

### <a name="gateway-attribute-group"></a>Gateway-Attributgruppe

Die Attributgruppe Gateway enthält die folgenden Attribute.

- **Empfangs-ID**. Verwendet, um die Telefonnummer des Network Access Server festlegen. Dieses Attribut ist eine Zeichenfolge. Sie können die mustervergleichssyntax verwenden, Ortskennzahlen angeben.
- **NAS-Bezeichner**. Verwendet, um den Namen des Network Access Server festlegen. Dieses Attribut ist eine Zeichenfolge. Sie können mustervergleichssyntax verwenden, um NAS-Bezeichner angeben.
- **NAS-IPv4-Adresse**. Verwendet, um das Festlegen von Internet Protocol, Version 4 (IPv4) Adresse der Netzwerk-Zugriffsserver (RADIUS-Client). Dieses Attribut ist eine Zeichenfolge. Sie können die mustervergleichssyntax verwenden, an die IP-Netzwerke.
- **NAS-IPv6-Adresse**. Verwendet, um die Internet Protocol Version 6 (IPv6) Festlegen der Netzwerk-Zugriffsserver (RADIUS-Client)-Adresse. Dieses Attribut ist eine Zeichenfolge. Sie können die mustervergleichssyntax verwenden, an die IP-Netzwerke.
- **NAS-Porttyp**. Verwendet, um den Typ des Mediums verwendet wird, von dem Zugriffsclient festlegen. Beispiele sind analoge Telefonleitungen (auch bekannt als asynchron) "," ISDN Integrated Services Digital Network () "," Tunnel "oder" virtuelle private Netzwerke (VPNs), IEEE 802.11 Drahtlos und Ethernet-switches.

### <a name="machine-identity-attribute-group"></a>Computergruppe der Identity-Attribut

Die Attributgruppe Computeridentität enthält das Computer-Identity-Attribut. Durch dieses Attribut verwenden, können Sie die Methode, die mit der Clients identifiziert werden in der Richtlinie angeben.

### <a name="radius-client-properties-attribute-group"></a>RADIUS-Client-Eigenschaften-Attributgruppe

Die Attributgruppe für die Eigenschaften von RADIUS-Client enthält die folgenden Attribute.

- **Anrufer-ID**. Verwendet, um die Rufnummer des Anrufers (Client Access) festlegen. Dieses Attribut ist eine Zeichenfolge. Sie können die mustervergleichssyntax verwenden, Ortskennzahlen angeben.  In der 802.1X-Authentifizierungen wird die MAC-Adresse in der Regel und auf dem Client verglichen werden kann.  Dieses Feld wird in der Regel für Szenarien der Umgehung der Mac-Adresse verwendet, wenn die Verbindungsanforderungsrichtlinie für "Accept-Benutzer ohne Überprüfung der Anmeldeinformationen" konfiguriert ist.  
- **Client-Anzeigename**. Verwendet, um den Namen des RADIUS-Clients zu bestimmen, die Authentifizierung anfordert. Dieses Attribut ist eine Zeichenfolge. Sie können mustervergleichssyntax verwenden, auf die um clientseitigen Namen zu geben.
- **Die IPv4-Adresse des Clients**. Verwendet, um der IPv4-Adresse der Netzwerk-Zugriffsserver (RADIUS-Client) festlegen. Dieses Attribut ist eine Zeichenfolge. Sie können die mustervergleichssyntax verwenden, an die IP-Netzwerke.
- **Die IPv6-Adresse des Clients**. Verwendet, um die IPv6-Adresse der Netzwerk-Zugriffsserver (RADIUS-Client) festlegen. Dieses Attribut ist eine Zeichenfolge. Sie können die mustervergleichssyntax verwenden, an die IP-Netzwerke.
- **Client-Anbieter**. Verwendet, um den Anbieter der Network Access Server zu bestimmen, die Authentifizierung anfordert. Ein Computer unter den Routing- und RAS-Dienst ist der Microsoft-NAS-Hersteller. Sie können dieses Attribut verwenden, so konfigurieren Sie separate Richtlinien für unterschiedliche NAS-Hersteller. Dieses Attribut ist eine Zeichenfolge. Sie können die Mustervergleichs-Syntax verwenden.

### <a name="user-name-attribute-group"></a>Benutzergruppe von Name-Attribut

Die Attributgruppe Benutzernamen enthält das Benutzernamen-Attribut. Durch dieses Attribut verwenden, können Sie festlegen, den Benutzernamen oder einen Teil des Benutzernamens, die den Benutzernamen ein, die vom Client Access in der RADIUS-Nachricht bereitgestellte entsprechen muss. Dieses Attribut ist eine Zeichenfolge, die einen Bereichsnamen und einen Benutzerkontonamen in der Regel enthält. Sie können mustervergleichssyntax verwenden, um Benutzernamen anzugeben.

## <a name="connection-request-policy-settings"></a>Verbindungseinstellungen für Anforderung-Richtlinie

Verbindung anforderungsrichtlinieneinstellungen sind eine Reihe von Eigenschaften, die auf eine eingehende RADIUS-Nachricht angewendet werden. Einstellungen bestehen die folgenden Gruppen von Eigenschaften ab.

- Authentifizierung
- Kontoführung
- Attribut bearbeiten
- Weiterleitungsanforderung
- Erweitert

Die folgenden Abschnitte enthalten zusätzlichen Details zu diesen Einstellungen.

### <a name="authentication"></a>Authentifizierung

Mit dieser Einstellung können Sie festlegen, überschreiben die Einstellungen für die Authentifizierung, die in alle Netzwerkrichtlinien konfiguriert sind, und können Sie die Authentifizierungsmethoden und Typen, die erforderlich sind, für die Verbindung mit Ihrem Netzwerk festlegen.

>[!IMPORTANT]
>Wenn Sie eine Authentifizierungsmethode in der Verbindungsanforderungsrichtlinie, die weniger sicher als die Authentifizierungsmethode, die Sie in der Netzwerkrichtlinie konfigurieren konfigurieren, wird die sicherere Authentifizierungsmethode, die Sie in der Netzwerkrichtlinie konfigurieren überschrieben. Z. B. Wenn Sie eine Netzwerkrichtlinie haben, erfordert die Verwendung von Protected Extensible Authentication Protocol – Microsoft Challenge Handshake Authentication Protocol Version 2 \(PEAP-MS-CHAP v2\), dies ist eine Kennwort-basierte Authentifizierungsmethode für sichere Drahtlosnetzwerke, und Sie auch konfigurieren, können Sie eine Verbindungsanforderungsrichtlinie zum nicht authentifizierten Zugriff zulassen, die das Ergebnis ist, dass keine-Clients die Authentifizierung mithilfe von PEAP-MS-CHAP v2 erforderlich sind. In diesem Beispiel werden alle Clients, die eine Verbindung mit Ihrem Netzwerk gewährt Zugriff ohne Authentifizierung.

### <a name="accounting"></a>Kontoführung

Mithilfe dieser Einstellung können Sie konfigurieren, Verbindungsanforderungsrichtlinie zum Weiterleiten von Informationen zur Kontoführung an einen Netzwerkrichtlinienserver oder einen anderen RADIUS-Server in einer remote-RADIUS-Servergruppe, damit die RADIUS-Remoteservergruppe Buchhaltung ausführt.

>[!NOTE]
>Wenn Sie mehrere RADIUS-Server und Kontoführungsinformationen für alle Server in einer zentralen RADIUS-Kontoführung-Datenbank gespeichert werden sollen, können die Verbindung Anforderung buchhaltungs-richtlinieneinstellung in einer Richtlinie für jeden RADIUS-Server, dass Kontoführungsdaten aus Sie alle an einem NPS-Server oder anderen RADIUS-Server, der als Kontoführungsserver festgelegt ist.

Die verbindungsanforderung buchhaltungs-Richtlinieneinstellungen unabhängig von der Buchhaltung-Konfiguration, der den lokalen NPS-Funktion. Das heißt, wenn Sie den lokalen NPS zum Protokollieren von Informationen zur RADIUS-Kontoführung in eine lokale Datei oder in einer Microsoft SQL Server-Datenbank konfigurieren, führt es dies unabhängig davon, ob Sie eine Verbindungsanforderungsrichtlinie zum Weiterleiten von Kontoführungsnachrichten an eine remote-RADIUS-konfigurieren Server-Gruppe.

Wenn Sie Informationen zur Kontoführung protokolliert wird, Remote, aber nicht lokal möchten, müssen Sie den lokalen NPS aus, um buchhaltungs-, gleichzeitig die Kontoführung in einer Verbindungsanforderungsrichtlinie zum Weiterleiten von Ressourcenerfassungsdaten an einen RADIUS-Remoteservergruppe nicht ausgeführt werden, konfigurieren.

### <a name="attribute-manipulation"></a>Attribut bearbeiten

Sie können eine Reihe von Such- und Ersetzungsvorgänge Regeln konfigurieren, die die Textzeichenfolgen, die von einem der folgenden Attribute zu bearbeiten.

- Benutzername
- Empfangs-ID
- Anrufer-ID

Suchen und Ersetzen-regelverarbeitung tritt auf, für eine der oben genannten Attribute vor die RADIUS-Nachricht gemäß den Einstellungen für Authentifizierung und-Kontoführung. Attribut bearbeiten Regeln gelten nur für ein einzelnes Attribut. Sie können keine Attribut Manipulation-Regeln für jedes Attribut konfigurieren. Darüber hinaus ist die Liste der Attribute, die Sie bearbeiten können, eine statische Liste; die Liste der Attribute, die zur Bearbeitung kann nicht hinzugefügt werden.

>[!NOTE]
>Wenn Sie das MS-CHAP v2-Authentifizierungsprotokoll verwenden, kann nicht das Benutzernamen-Attribut bearbeiten, wenn die Verbindungsanforderungsrichtlinie zum Weiterleiten der RADIUS-Nachricht verwendet wird. Die einzige Ausnahme tritt auf, wenn ein umgekehrter Schrägstrich (\) Schrägstrich verwendet wird und die Bearbeitung wirkt sich nur auf die Informationen auf der linken Seite des Zertifikats. Ein umgekehrter Schrägstrich wird normalerweise verwendet, um einen Domänennamen an (die Informationen auf der linken Seite des umgekehrten Schrägstrichs) und einen Benutzerkontonamen in der Domäne (die Informationen, die rechts neben den umgekehrten Schrägstrich) anzugeben. In diesem Fall dürfen nur Attribut Manipulation-Regeln, die ändern oder Ersetzen Sie den Domänennamen.

Beispiele für den Bereichsnamen im Benutzernamen-Attribut, Ändern von finden Sie im Abschnitt "Beispiele für die Bearbeitung von den Bereichsnamen im Benutzernamen-Attribut" im Thema [Verwenden von regulären Ausdrücken in NPS](nps-crp-reg-expressions.md).

### <a name="forwarding-request"></a>Weiterleitungsanforderung

Sie können festlegen, dass die folgenden Weiterleitung von Optionen für die Anforderung, die für die RADIUS-Access-Request-Nachrichten verwendet werden:

- **Authentifizieren von Anforderungen auf diesem Server**. Mit dieser Einstellung verwendet NPS zum Authentifizieren der verbindungsanforderung einer Windows NT 4.0-Domäne, Active Directory oder der lokalen Sicherheitskontenverwaltung (Security Accounts Manager, SAM) Benutzerkontendatenbank. Diese Einstellung gibt auch an, dass die übereinstimmende Netzwerkrichtlinie in NPS konfiguriert werden, sowie die Einwähleigenschaften des Benutzerkontos, wird von NPS die verbindungsanforderung autorisiert. In diesem Fall sieht der NPS als RADIUS-Server ausführen.

- **Weiterleiten von Anforderungen an die folgenden RADIUS-Remoteservergruppe**. Verwenden Sie diese Einstellung, leitet NPS verbindungsanforderungen, an die remote-RADIUS-Servergruppe, die Sie angeben. Wenn der NPS eine gültige Access-Accept-Nachricht empfängt, die die Access-Request-Nachricht entspricht, wird der Verbindungsversuch als authentifiziert und autorisiert. In diesem Fall fungiert der NPS als RADIUS-Proxy ein.

- **Benutzer ohne Überprüfung der Anmeldeinformationen akzeptieren**. Mit dieser Einstellung können NPS überprüft nicht die Identität des Benutzers mit dem Netzwerk verbinden möchten, und NPS versucht nicht, stellen Sie sicher, dass der Benutzer oder Computer das Recht vor, mit dem Netzwerk verbunden ist. Wenn NPS so konfiguriert ist, dass nicht authentifizierte Zugriffe zulässig, und es eine verbindungsanforderung empfängt, sendet NPS sofort, dass eine Access-Accept-Nachricht an den RADIUS-Client und der Benutzer oder Computer mit Netzwerkzugriff gewährt wird. Diese Einstellung wird verwendet, für einige Typen von erzwungenem Tunneln, in der Zugriffsclient getunnelt wird, bevor die Anmeldeinformationen des Benutzers authentifiziert werden.

>[!NOTE]
>Diese Authentifizierungsoption kann nicht verwendet werden, wenn das Authentifizierungsprotokoll des Zugriffsclients MS-CHAP v2 oder Extensible Authentication Protocol-Transport Layer Security (EAP-TLS), beide die gegenseitigen Authentifizierung unterstützen. Bei der gegenseitigen Authentifizierung weist der, dass er ein gültiger-Client auf dem Authentifizierungsserver (der NPS), und der Authentifizierungsserver beweist, dass es sich um einen gültigen authentifizierenden Server an den Zugriffsclient ist. Wenn diese Authentifizierungsoption verwendet wird, wird die Access-Accept-Nachricht zurückgegeben. Allerdings wird der authentifizierende Server bietet keine Validierung an den Zugriffsclient, und gegenseitige Authentifizierung ein Fehler auftritt.

Beispiele für reguläre Ausdrücke verwenden, um Routingregeln zu erstellen, das Weiterleiten von RADIUS-Nachrichten mit einem angegebenen Bereichsnamen an eine remote-RADIUS-Servergruppe finden Sie im Abschnitt "Beispiel für die Weiterleitung von RADIUS-Nachricht von einem Proxyserver" im Thema [verwenden Reguläre Ausdrücke in NPS](nps-crp-reg-expressions.md).

### <a name="advanced"></a>Erweitert

Sie können erweiterte Eigenschaften an, die die Reihe der RADIUS-Attribute festlegen:

- Der RADIUS-Antwortnachricht hinzugefügt, wenn NPS als RADIUS-Authentifizierung oder Kontoführungsserver verwendet wird. Wenn Attribute, die für eine Netzwerkrichtlinie und der Verbindungsanforderungsrichtlinie festgelegt sind, werden die Attribute, die in der RADIUS-Antwortnachricht gesendet werden die Kombination der beiden Sätze von Attributen.
- Der RADIUS-Nachricht hinzugefügt, wenn NPS als RADIUS-Authentifizierung oder buchhaltungs-Proxy verwendet wird. Wenn das Attribut bereits in der Nachricht vorhanden, die weitergeleitet werden ist, wird es mit dem Wert des Attributs angegeben in der Verbindungsanforderungsrichtlinie ersetzt. 

Darüber hinaus einige Attribute, die für die Konfiguration für die Verbindung verfügbar sind, fordern Richtlinien **Einstellungen** Registerkarte die **erweitert** Kategorie bieten spezielle Funktionen. Beispielsweise können Sie konfigurieren die **Remote-RADIUS auf Windows-Benutzerzuordnung** Attribut, wenn Sie teilen die Authentifizierung und Autorisierung, der eine Anforderung für die Verbindung zwischen zwei Benutzer, Datenbanken Konten.

Die **Remote-RADIUS auf Windows-Benutzerzuordnung** Attribut gibt an, dass Windows-Autorisierung für Benutzer erfolgt, die von einem remote-RADIUS-Server authentifiziert werden. Das heißt, ein remote-RADIUS-Server führt die Authentifizierung für ein Benutzerkonto in einer Kontodatenbank Remotebenutzer, aber den lokalen NPS autorisiert die verbindungsanforderung für ein Benutzerkonto in einer lokalen Benutzerdatenbank für die Konten. Dies ist nützlich, wenn Sie Besucher Zugriff auf Ihr Netzwerk zulassen möchten.

Z. B. Besucher von Partnerorganisationen können von ihren eigenen Partner Organisation RADIUS-Server authentifiziert werden, und klicken Sie dann ein Windows-Benutzerkonto in Ihrer Organisation auf einem Gast-lokale Netzwerk (LAN) in Ihrem Netzwerk verwenden.

Andere Attribute, die speziellen Funktionen bereitstellen sind:

- **MS-Quarantäne-IPFilter und MS-Quarantäne-Sitzung-Timeout**. Diese Attribute werden verwendet, wenn Sie Network Access Quarantine Control (NAQC) mit der Routing- und RAS VPN-Bereitstellung bereitstellen.
- **Passport-Benutzer-Mapping-UPN-Suffix**. Dieses Attribut ermöglicht Ihnen die Authentifizierung von Anforderungen von Verbindungen mit Windows Live™ ID-Anmeldeinformationen des Benutzerkontos.
- **Tunnel-Tag**. Dieses Attribut legt fest, die VLAN-ID-Nummer, die zu der die Verbindung vom NAS zugewiesen wird, wenn Sie virtuelle lokale Netzwerke (VLANs) bereitstellen.

## <a name="default-connection-request-policy"></a>Standard-Verbindungsanforderungsrichtlinie

Eine Standard-Verbindungsanforderungsrichtlinie wird erstellt, bei der Installation von NPS. Diese Richtlinie hat die folgende Konfiguration an.

- Authentifizierung ist nicht konfiguriert.
- Kontoführung wird nicht für forward Kontoführungsinformationen an einen RADIUS-Remoteservergruppe konfiguriert.
- Attribut wird nicht mit Attribut-Manipulation-Regeln konfiguriert, der verbindungsanforderungen an RADIUS-Remoteservergruppen weiterleiten.
- Weiterleitung der Anforderung ist so konfiguriert, dass verbindungsanforderungen werden authentifiziert und werden, auf den lokalen NPS autorisiert.
- Erweiterte Attribute sind nicht konfiguriert.

Die Standard-Verbindungsanforderungsrichtlinie verwendet NPS als RADIUS-Server. Um einen Server mit NPS als RADIUS-Proxy fungieren konfigurieren zu können, müssen Sie auch eine remote-RADIUS-Servergruppe konfigurieren. Sie können eine neue RADIUS-Remoteservergruppe erstellen, während Sie eine neue Verbindungsanforderungsrichtlinie mit dem Assistenten für neue Verbindung erstellen. Sie können die Standard-Verbindungsanforderungsrichtlinie löschen, oder stellen Sie sicher, dass die Standard-Verbindungsanforderungsrichtlinie, die letzte Richtlinie, die vom NPS verarbeitet werden, indem Sie diesen letzten in der sortierten Liste der Richtlinien ist.

>[!NOTE]
>NPS und RAS-Dienst installiert, auf dem gleichen Computer, und der RAS-Dienst ist für die Windows-Authentifizierung konfiguriert und Buchhaltung, es ist möglich, für die RAS-Authentifizierung und kontoführungsanforderungen an einen RADIUS-Server weitergeleitet werden . Dies kann auftreten, wenn der RAS-Authentifizierung und kontoführungsanforderungen eine Verbindungsanforderungsrichtlinie, die konfiguriert wird entsprechen, um diese an einen RADIUS-Remoteservergruppe weiterleitet.
