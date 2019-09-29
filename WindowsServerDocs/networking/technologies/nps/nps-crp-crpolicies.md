---
title: Verbindungsanforderungsrichtlinien
description: Dieses Thema enthält eine Übersicht über die Verbindungs Anforderungs Richtlinien für Netzwerk Richtlinien Server in Windows Server 2016.
manager: brianlic
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 4ec45e0c-6b37-4dfb-8158-5f40677b0157
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 0b373e496567f414657b380bad952baefcbe4b18
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71396367"
---
# <a name="connection-request-policies"></a>Verbindungsanforderungsrichtlinien

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In diesem Thema erfahren Sie, wie Sie NPS-Verbindungs Anforderungs Richtlinien verwenden, um den NPS als RADIUS-Server, RADIUS-Proxy oder beides zu konfigurieren.

>[!NOTE]
>Zusätzlich zu diesem Thema ist die folgende Dokumentation zur Verbindungs Anforderungs Richtlinie verfügbar.
> - [Konfigurieren von Verbindungs Anforderungs Richtlinien](nps-crp-configure.md)
> - [Konfigurieren von Remote-RADIUS-Server Gruppen](nps-crp-rrsg-configure.md)

Verbindungs Anforderungs Richtlinien sind Sätze von Bedingungen und Einstellungen, mit denen Netzwerkadministratoren festlegen können, welche Remote Authentication Dial-in User Service (RADIUS)-Server die Authentifizierung und Autorisierung von Verbindungsanforderungen durchführen, die von der der Server, auf dem der Netzwerk Richtlinien Server (Network Policy Server, NPS) ausgeführt wird, Verbindungs Anforderungs Richtlinien können konfiguriert werden, um anzugeben, welche RADIUS-Server für die RADIUS-Kontoführung verwendet werden.

Sie können Verbindungs Anforderungs Richtlinien erstellen, damit einige RADIUS-Anforderungs Nachrichten, die von RADIUS-Clients gesendet werden, lokal verarbeitet werden (NPS wird als RADIUS-Server verwendet) und andere Nachrichten Typen an einen anderen RADIUS-Server weitergeleitet werden (NPS wird als RADIUS-Proxy verwendet).

Mit Verbindungs Anforderungs Richtlinien können Sie NPS als RADIUS-Server oder als RADIUS-Proxy verwenden, basierend auf Faktoren wie den folgenden: 

- Uhrzeit und Tag der Woche
- Der Bereichs Name in der Verbindungsanforderung.
- Der angeforderte Verbindungstyp.
- Die IP-Adresse des RADIUS-Clients

RADIUS-Zugriffs Anforderungs Nachrichten werden nur von NPS verarbeitet oder weitergeleitet, wenn die Einstellungen der eingehenden Nachricht mindestens einer der Verbindungs Anforderungs Richtlinien entsprechen, die auf dem NPS konfiguriert sind. 

Wenn die Richtlinien Einstellungen stimmen und die Richtlinie erfordert, dass der NPS die Nachricht verarbeitet, fungiert NPS als RADIUS-Server, der die Verbindungsanforderung authentifiziert und autorisiert. Wenn die Richtlinien Einstellungen stimmen und die Richtlinie erfordert, dass der NPS die Nachricht weiterleitet, fungiert NPS als RADIUS-Proxy und leitet die Verbindungsanforderung zur Verarbeitung an einen Remote-RADIUS-Server weiter.

Wenn die Einstellungen einer eingehenden RADIUS-Access-Request-Nachricht nicht mindestens einer der Verbindungs Anforderungs Richtlinien entsprechen, wird eine Zugriffs Ablehnungs Nachricht an den RADIUS-Client gesendet, und der Benutzer bzw. Computer, der versucht, eine Verbindung mit dem Netzwerk herzustellen, wird der Zugriff verweigert.

## <a name="configuration-examples"></a>Konfigurationsbeispiele

Die folgenden Konfigurationsbeispiele veranschaulichen, wie Sie Verbindungs Anforderungs Richtlinien verwenden können.

### <a name="nps-as-a-radius-server"></a>NPS als RADIUS-Server

Die standardmäßige Verbindungs Anforderungs Richtlinie ist die einzige konfigurierte Richtlinie. In diesem Beispiel ist NPS als RADIUS-Server konfiguriert, und alle Verbindungsanforderungen werden vom lokalen NPS verarbeitet. Der NPS kann Benutzer authentifizieren und autorisieren, deren Konten sich in der Domäne der NPS-Domäne und in vertrauenswürdigen Domänen befinden.


### <a name="nps-as-a-radius-proxy"></a>NPS als RADIUS-Proxy

Die Standard-Verbindungs Anforderungs Richtlinie wird gelöscht, und es werden zwei neue Verbindungs Anforderungs Richtlinien erstellt, um Anforderungen an zwei verschiedene Domänen weiterzuleiten. In diesem Beispiel ist NPS als RADIUS-Proxy konfiguriert. NPS verarbeitet keine Verbindungsanforderungen auf dem lokalen Server. Stattdessen werden Verbindungsanforderungen an NPS oder andere RADIUS-Server weitergeleitet, die als Mitglieder von RADIUS-Remote Server Gruppen konfiguriert sind.


### <a name="nps-as-both-radius-server-and-radius-proxy"></a>NPS als RADIUS-Server und RADIUS-Proxy

Zusätzlich zur Standard Verbindungs Anforderungs Richtlinie wird eine neue Verbindungs Anforderungs Richtlinie erstellt, die Verbindungsanforderungen an einen NPS oder einen anderen RADIUS-Server in einer nicht vertrauenswürdigen Domäne weiterleitet. In diesem Beispiel wird die Proxy Richtlinie zuerst in der geordneten Liste der Richtlinien angezeigt. Wenn die Verbindungsanforderung mit der Proxy Richtlinie übereinstimmt, wird die Verbindungsanforderung an den RADIUS-Server in der Remote-RADIUS-Server Gruppe weitergeleitet. Wenn die Verbindungsanforderung nicht mit der Proxy Richtlinie, aber mit der standardmäßigen Verbindungs Anforderungs Richtlinie identisch ist, verarbeitet NPS die Verbindungsanforderung auf dem lokalen Server. Wenn die Verbindungsanforderung keiner Richtlinie entspricht, wird sie verworfen.

### <a name="nps-as-radius-server-with-remote-accounting-servers"></a>NPS als RADIUS-Server mit Remote Buchhaltungs Servern

In diesem Beispiel ist der lokale NPS nicht für die Kontoführung konfiguriert, und die standardmäßige Verbindungs Anforderungs Richtlinie wird so überarbeitet, dass RADIUS-Buchhaltungs Nachrichten an einen NPS oder einen anderen RADIUS-Server in einer RADIUS-Remote Server Gruppe weitergeleitet werden. Obwohl Buchhaltungs Nachrichten weitergeleitet werden, werden Authentifizierungs-und Autorisierungs Nachrichten nicht weitergeleitet, und der lokale NPS führt diese Funktionen für die lokale Domäne und alle vertrauenswürdigen Domänen aus.


### <a name="nps-with-remote-radius-to-windows-user-mapping"></a>NPS mit Remote RADIUS-zu-Windows-Benutzer Zuordnung

In diesem Beispiel fungiert NPS sowohl als RADIUS-Server als auch als RADIUS-Proxy für jede einzelne Verbindungsanforderung, indem die Authentifizierungsanforderung an einen RADIUS-Remote Server weitergeleitet wird, während ein lokales Windows-Benutzerkonto für die Autorisierung verwendet wird. Diese Konfiguration wird implementiert, indem das Attribut Remote RADIUS für Windows-Benutzer Zuordnung als Bedingung der Verbindungs Anforderungs Richtlinie konfiguriert wird. (Zusätzlich muss ein Benutzerkonto lokal erstellt werden, das denselben Namen hat wie das Remote Benutzerkonto, mit dem die Authentifizierung durch den RADIUS-Remote Server erfolgt.)

## <a name="connection-request-policy-conditions"></a>Bedingungen der Verbindungs Anforderungs Richtlinie

Bedingungen für Verbindungs Anforderungs Richtlinien sind mindestens ein RADIUS-Attribut, das mit den Attributen der eingehenden RADIUS-Zugriffs Anforderungs Nachricht verglichen wird. Wenn mehrere Bedingungen vorliegen, müssen alle Bedingungen in der Verbindungs Anforderungs Nachricht und in der Verbindungs Anforderungs Richtlinie entsprechen, damit die Richtlinie von NPS erzwungen wird.


Im folgenden finden Sie die verfügbaren Bedingungs Attribute, die Sie in Verbindungs Anforderungs Richtlinien konfigurieren können.

### <a name="connection-properties-attribute-group"></a>Attribut Gruppe "Verbindungs Eigenschaften"

Die Attribut Gruppe "Verbindungs Eigenschaften" enthält die folgenden Attribute.

- **Gerahmte Protokoll**. Wird verwendet, um den Typ des Frames für eingehende Pakete festzulegen. Beispiele hierfür sind Point-to-Point-Protokoll (PPP), Serial Line Internet Protocol (Slip), Frame Relay und X. 25.
- **Diensttyp**. Dient zum Festlegen des angeforderten Dienst Typs. Beispiele hierfür sind z. b. zusammengefasst (z. b. PPP-Verbindungen) und die Anmeldung (z.b. Telnet-Verbindungen). Weitere Informationen zu RADIUS-Dienst Typen finden Sie unter RFC 2865, "Remote Authentication Dial-in User Service (RADIUS)".
- **Tunneltyp**. Dient zum Festlegen des Tunnel Typs, der vom anfordernden Client erstellt wird. Zu den Tunnel Typen zählen das Point-to-Point-Tunneling-Protokoll (PPTP) und das Layer-Two-Tunneling-Protokoll (L2TP).

### <a name="day-and-time-restrictions-attribute-group"></a>Attribut Gruppe für Tages-und Uhrzeit Einschränkungen 

Die Attribut Gruppe für die Tages-und Uhrzeit Einschränkungen enthält das Tag-und Uhrzeit-Einschränkungs Attribut. Mit diesem Attribut können Sie den Wochentag und die Uhrzeit des Verbindungsversuchs angeben. Der Tag und die Uhrzeit sind relativ zum Tag und zur Uhrzeit des NPS.

### <a name="gateway-attribute-group"></a>Gateway-Attribut Gruppe

Die Gruppe "Gateway-Attribut" enthält die folgenden Attribute.

- Wird **als Stations-ID bezeichnet**. Dient zum Festlegen der Telefonnummer des Netzwerk Zugriffs Servers. Dieses Attribut ist eine Zeichenfolge. Sie können die Muster Vergleichs Syntax zum Angeben von Bereichs Codes verwenden.
- **NAS-Bezeichner**. Wird verwendet, um den Namen des Netzwerk Zugriffs Servers festzulegen. Dieses Attribut ist eine Zeichenfolge. Sie können die Muster Vergleichs Syntax zum Angeben von NAS-Bezeichnerzeichen verwenden.
- **NAS-IPv4-Adresse**. Wird verwendet, um die IPv4-Adresse (Internet Protocol Version 4) des Netzwerk Zugriffs Servers (RADIUS-Client) festzulegen. Dieses Attribut ist eine Zeichenfolge. Zum Angeben von IP-Netzwerken können Sie die Syntax für Muster Übereinstimmungen verwenden.
- **NAS-IPv6-Adresse**. Dient zum Festlegen der IPv6-Adresse (Internet Protokollversion 6) des Netzwerk Zugriffs Servers (RADIUS-Client). Dieses Attribut ist eine Zeichenfolge. Zum Angeben von IP-Netzwerken können Sie die Syntax für Muster Übereinstimmungen verwenden.
- **NAS-Porttyp**. Wird verwendet, um den Medientyp festzulegen, der vom Zugriffs Client verwendet wird. Beispiele sind analoge Telefonleitungen (Async), integrierte Dienste Digital Network (ISDN), Tunnel oder virtuelle private Netzwerke (Virtual Private Networks, VPNs), IEEE 802,11 Wireless-und Ethernet-Switches.

### <a name="machine-identity-attribute-group"></a>Computer Identitäts Attribut Gruppe

Die Attribut Gruppe für die Computer Identität enthält das Attribut "Computer Identität". Mithilfe dieses Attributs können Sie die Methode angeben, mit der Clients in der Richtlinie identifiziert werden.

### <a name="radius-client-properties-attribute-group"></a>Attribut Gruppe der RADIUS-Client Eigenschaften

Die Attribut Gruppe "RADIUS-Client Eigenschaften" enthält die folgenden Attribute.

- **Aufruf Station-ID**. Dient zum Festlegen der Telefonnummer, die vom Aufrufer (dem Zugriffs Client) verwendet wird. Dieses Attribut ist eine Zeichenfolge. Sie können die Muster Vergleichs Syntax zum Angeben von Bereichs Codes verwenden.  In 802.1 x-Authentifizierungen wird die Mac-Adresse in der Regel aufgefüllt und kann vom Client abgeglichen werden.  Dieses Feld wird in der Regel für Mac-Adress Umgehungs Szenarien verwendet, wenn die Verbindungs Anforderungs Richtlinie für "Benutzer ohne Überprüfung von Anmelde Informationen akzeptieren" konfiguriert ist.  
- Anzeige **Name des Clients**. Wird verwendet, um den Namen des RADIUS-Client Computers anzugeben, der die Authentifizierung anfordert. Dieses Attribut ist eine Zeichenfolge. Sie können die Muster Vergleichs Syntax verwenden, um Client Namen anzugeben.
- **Client-IPv4-Adresse**. Dient zum Festlegen der IPv4-Adresse des Netzwerk Zugriffs Servers (RADIUS-Client). Dieses Attribut ist eine Zeichenfolge. Zum Angeben von IP-Netzwerken können Sie die Syntax für Muster Übereinstimmungen verwenden.
- **IPv6-Client Adresse**. Dient zum Festlegen der IPv6-Adresse des Netzwerk Zugriffs Servers (RADIUS-Client). Dieses Attribut ist eine Zeichenfolge. Zum Angeben von IP-Netzwerken können Sie die Syntax für Muster Übereinstimmungen verwenden.
- **Client Hersteller**. Dient zum Festlegen des Anbieters des Netzwerk Zugriffs Servers, der die Authentifizierung anfordert. Ein Computer, auf dem der Routing-und RAS-Dienst ausgeführt wird, ist der Microsoft NAS-Hersteller. Sie können dieses Attribut verwenden, um separate Richtlinien für verschiedene NAS-Hersteller zu konfigurieren. Dieses Attribut ist eine Zeichenfolge. Sie können die Syntax für die Muster Übereinstimmung verwenden.

### <a name="user-name-attribute-group"></a>Benutzer Name-Attribut Gruppe

Die Benutzernamen-Attribut Gruppe enthält das User Name-Attribut. Mithilfe dieses Attributs können Sie den Benutzernamen oder einen Teil des Benutzernamens angeben, der mit dem Benutzernamen, der vom Zugriffs Client in der RADIUS-Nachricht angegeben wird, entsprechen muss. Dieses Attribut ist eine Zeichenfolge, die in der Regel einen Bereichs Namen und einen Benutzerkonto Namen enthält. Sie können die Muster Vergleichs Syntax verwenden, um Benutzernamen anzugeben.

## <a name="connection-request-policy-settings"></a>Richtlinien Einstellungen für Verbindungsanforderungen

Verbindungs Anforderungs Richtlinien-Einstellungen sind ein Satz von Eigenschaften, die auf eine eingehende RADIUS-Nachricht angewendet werden. Die Einstellungen bestehen aus den folgenden Eigenschaften Gruppen.

- Authentifizierung
- Kontoführung
- Attribut Bearbeitung
- Weiterleitungs Anforderung
- Erweitert

In den folgenden Abschnitten finden Sie weitere Details zu diesen Einstellungen.

### <a name="authentication"></a>Authentifizierung

Mit dieser Einstellung können Sie die Authentifizierungs Einstellungen außer Kraft setzen, die in allen Netzwerk Richtlinien konfiguriert sind, und Sie können die Authentifizierungsmethoden und-Typen festlegen, die für die Verbindung mit dem Netzwerk erforderlich sind.

>[!IMPORTANT]
>Wenn Sie eine Authentifizierungsmethode in einer Verbindungs Anforderungs Richtlinie konfigurieren, die weniger sicher ist als die Authentifizierungsmethode, die Sie in der Netzwerk Richtlinie konfigurieren, wird die sicherere Authentifizierungsmethode, die Sie in der Netzwerk Richtlinie konfigurieren, überschrieben. Angenommen, Sie verfügen über eine Netzwerk Richtlinie, die die Verwendung von Protected Extensible Authentication Protocol-Microsoft Challenge Handshake Authentication Protocol Version 2 \(peer-MS-CHAP v2 @ no__t-1 erfordert, bei dem es sich um eine Kenn Wort basierte Authentifizierung handelt. Methode für sicheres Drahtlos Netzwerk, und Sie konfigurieren auch eine Verbindungs Anforderungs Richtlinie, um nicht authentifizierten Zugriff zuzulassen. Dies hat zur Folge, dass keine Clients für die Authentifizierung mithilfe von "Peer-MS-CHAP v2" erforderlich sind. In diesem Beispiel erhalten alle Clients, die eine Verbindung mit Ihrem Netzwerk herstellen, nicht authentifizierten Zugriff.

### <a name="accounting"></a>Kontoführung

Mit dieser Einstellung können Sie die Verbindungs Anforderungs Richtlinie so konfigurieren, dass Buchhaltungsinformationen an einen NPS oder einen anderen RADIUS-Server in einer RADIUS-Remote Server Gruppe weiterleiten werden, damit die Remote-RADIUS-Server Gruppe eine Buchhaltung ausführt.

>[!NOTE]
>Wenn Sie über mehrere RADIUS-Server verfügen und Buchhaltungsinformationen für alle Server benötigen, die in einer zentralen RADIUS-Buchhaltungs Datenbank gespeichert sind, können Sie die Einstellungen für die Verbindungs Anforderungs Richtlinie in einer Richtlinie auf jedem RADIUS-Server verwenden, um Buchhaltungsdaten weiterzuleiten. alle Server auf einem NPS oder einem anderen RADIUS-Server, der als Buchhaltungsserver festgelegt ist.

Die Verbindungs Anforderungs Richtlinien-Buchhaltungs Einstellungen funktionieren unabhängig von der Kontoführungs Konfiguration des lokalen NPS. Anders ausgedrückt: Wenn Sie das lokale NPS so konfigurieren, dass RADIUS-Buchhaltungsinformationen in einer lokalen Datei oder einer Microsoft SQL Server Datenbank protokolliert werden, erfolgt dies unabhängig davon, ob Sie eine Verbindungs Anforderungs Richtlinie zum Weiterleiten von Buchhaltungs Nachrichten an einen Remote RADIUS konfigurieren. Server Gruppe.

Wenn Buchhaltungsinformationen Remote, aber nicht lokal protokolliert werden sollen, müssen Sie den lokalen NPS so konfigurieren, dass er keine Buchhaltung ausführt, und gleichzeitig die Kontoführung in einer Verbindungs Anforderungs Richtlinie konfigurieren, um Buchhaltungsdaten an eine Remote-RADIUS-Server Gruppe weiterzuleiten.

### <a name="attribute-manipulation"></a>Attribut Bearbeitung

Sie können eine Reihe von Such-und Ersetzungs Regeln konfigurieren, mit denen die Text Zeichenfolgen eines der folgenden Attribute geändert werden.

- Benutzername
- Aufgerufene Stations-ID
- Aufruf Stations-ID

Die Verarbeitung von "suchen und ersetzen"-Regeln tritt für eines der vorangehenden Attribute ein, bevor die RADIUS-Nachricht den Authentifizierungs-und Kontoführungs Einstellungen unterliegt. Attribut Bearbeitungs Regeln gelten nur für ein einzelnes Attribut. Sie können für jedes Attribut keine Regeln für die Attribut Bearbeitung konfigurieren. Außerdem ist die Liste der Attribute, die Sie bearbeiten können, eine statische Liste. der Liste der zur Bearbeitung verfügbaren Attribute kann nicht hinzugefügt werden.

>[!NOTE]
>Wenn Sie das MS-CHAP v2-Authentifizierungsprotokoll verwenden, können Sie das User Name-Attribut nicht bearbeiten, wenn die Verbindungs Anforderungs Richtlinie zum Weiterleiten der RADIUS-Nachricht verwendet wird. Die einzige Ausnahme tritt auf, wenn ein umgekehrter Schrägstrich (\)-Zeichen verwendet wird, und die Bearbeitung wirkt sich nur auf die Informationen auf der linken Seite aus. Ein umgekehrter Schrägstrich wird normalerweise verwendet, um einen Domänen Namen (die Informationen auf der linken Seite des umgekehrten Schrägstrichs) und einen Benutzerkonto Namen innerhalb der Domäne (die Informationen auf der rechten Seite des umgekehrten Schrägstrichs) anzugeben. In diesem Fall sind nur Attribut Bearbeitungs Regeln zulässig, die den Domänen Namen ändern oder ersetzen.

Beispiele zum Bearbeiten des Bereichs namens im User Name-Attribut finden Sie im Abschnitt "Beispiele für die Bearbeitung des Bereichs namens im User Name-Attribut" im Thema [Verwenden von regulären Ausdrücken in NPS](nps-crp-reg-expressions.md).

### <a name="forwarding-request"></a>Weiterleitungs Anforderung

Sie können die folgenden Weiterleitungs Anforderungs Optionen festlegen, die für RADIUS-Zugriffs Anforderungs Nachrichten verwendet werden:

- **Authentifizieren Sie Anforderungen auf diesem Server**. Wenn Sie diese Einstellung verwenden, verwendet NPS eine Windows NT 4,0-Domäne, Active Directory oder die SAM-Benutzerkonten Datenbank (Local Security Accounts Manager), um die Verbindungsanforderung zu authentifizieren. Diese Einstellung gibt auch an, dass die entsprechende Netzwerk Richtlinie, die in NPS konfiguriert ist, zusammen mit den Einwähleigenschaften des Benutzerkontos von NPS verwendet wird, um die Verbindungsanforderung zu autorisieren. In diesem Fall ist der NPS für die Ausführung als RADIUS-Server konfiguriert.

- **Leiten Sie Anforderungen an die folgende Remote-RADIUS-Server Gruppe weiter**. Mit dieser Einstellung leitet NPS Verbindungsanforderungen an die von Ihnen angegebene Remote-RADIUS-Server Gruppe weiter. Wenn der NPS eine gültige Access-Accept-Nachricht empfängt, die der Access-Request-Nachricht entspricht, wird der Verbindungsversuch als authentifiziert und autorisiert betrachtet. In diesem Fall fungiert das NPS als RADIUS-Proxy.

- **Akzeptieren Sie Benutzer, ohne die Anmelde**Informationen zu überprüfen. Mit dieser Einstellung überprüft NPS nicht die Identität des Benutzers, der versucht, eine Verbindung mit dem Netzwerk herzustellen, und NPS versucht nicht, zu überprüfen, ob der Benutzer oder Computer über das Recht zum Herstellen einer Verbindung mit dem Netzwerk verfügt. Wenn NPS so konfiguriert ist, dass er nicht authentifizierten Zugriff zulässt und eine Verbindungsanforderung empfängt, sendet NPS sofort eine Access-Accept-Nachricht an den RADIUS-Client, und der Benutzer bzw. Computer erhält Netzwerk Zugriff. Diese Einstellung wird für einige Arten von obligatorischen Tunneln verwendet, bei denen der Zugriffs Client getunngt wird, bevor Benutzer Anmelde Informationen authentifiziert werden.

>[!NOTE]
>Diese Authentifizierungs Option kann nicht verwendet werden, wenn das Authentifizierungsprotokoll des Zugriffs Clients MS-CHAP v2 oder Extensible Authentication Protocol-Transport Layer Security (EAP-TLS) ist, die beide gegenseitige Authentifizierung bereitstellen. Bei gegenseitiger Authentifizierung stellt der Zugriffs Client fest, dass es sich um einen gültigen Zugriffs Client für den authentifizier enden Server (NPS) handelt und der authentifizier Ende Server bestätigt, dass es sich um einen gültigen authentifizier enden Server beim Zugriffs Client handelt. Wenn diese Authentifizierungs Option verwendet wird, wird die Access-Accept-Nachricht zurückgegeben. Der authentifizier Ende Server stellt jedoch keine Validierung für den Zugriffs Client bereit, und die gegenseitige Authentifizierung schlägt fehl.

Beispiele für die Verwendung von regulären Ausdrücken zum Erstellen von Routing Regeln, die RADIUS-Nachrichten mit einem bestimmten Bereichs Namen an eine Remote-RADIUS-Server Gruppe weiterleiten, finden Sie im Abschnitt "Beispiel für die RADIUS-Nachrichten Weiterleitung durch einen Proxy Server" im Thema [use Regular Ausdrücke in NPS](nps-crp-reg-expressions.md).

### <a name="advanced"></a>Erweitert

Sie können erweiterte Eigenschaften festlegen, um die Reihe von RADIUS-Attributen anzugeben, die Folgendes sind:

- Wird der RADIUS-Antwortnachricht hinzugefügt, wenn der NPS als RADIUS-Authentifizierung oder Buchhaltungsserver verwendet wird. Wenn in einer Netzwerk Richtlinie und in der Verbindungs Anforderungs Richtlinie Attribute angegeben sind, sind die in der RADIUS-Antwortnachricht gesendeten Attribute die Kombination der beiden Attribut Sätze.
- Wird der RADIUS-Nachricht hinzugefügt, wenn der NPS als RADIUS-Authentifizierung oder als Buchhaltungs Proxy verwendet wird. Wenn das Attribut bereits in der weitergeleiteten Nachricht vorhanden ist, wird es durch den Wert des in der Verbindungs Anforderungs Richtlinie angegebenen Attributs ersetzt. 

Außerdem stellen bestimmte Attribute, die für die Konfiguration auf der Registerkarte Verbindungs Anforderungs Richtlinien **Einstellungen** in der Kategorie **erweitert** verfügbar sind, spezielle Funktionen bereit. Beispielsweise können Sie das Attribut **Remote RADIUS für Windows-Benutzer Zuordnung** konfigurieren, wenn Sie die Authentifizierung und Autorisierung einer Verbindungsanforderung zwischen zwei Benutzerkonten Datenbanken aufteilen möchten.

Das Attribut " **RADIUS-zu-Windows-Benutzer Zuordnung** " gibt an, dass die Windows-Autorisierung für Benutzer erfolgt, die von einem RADIUS-Remote Server authentifiziert Mit anderen Worten: ein RADIUS-Remote Server führt die Authentifizierung für ein Benutzerkonto in einer Remote-Benutzerkonten Datenbank aus, aber der lokale NPS autorisiert die Verbindungsanforderung für ein Benutzerkonto in einer lokalen Benutzerkonten Datenbank. Dies ist hilfreich, wenn Sie Besuchern den Zugriff auf Ihr Netzwerk gestatten möchten.

Beispielsweise können Besucher von Partnerorganisationen von einem eigenen RADIUS-Server der Partnerorganisation authentifiziert werden und dann ein Windows-Benutzerkonto in Ihrer Organisation verwenden, um auf ein LAN (Local Area Network) im Netzwerk zuzugreifen.

Weitere Attribute, die spezialisierte Funktionen bereitstellen, sind:

- **MS-Quarantäne-IPFilter und MS-Quarantäne-Session-Timeout**. Diese Attribute werden verwendet, wenn Sie die Netzwerk Zugriffs Quarantäne-Steuerung (NAQC) mit der Routing-und RAS-VPN-Bereitstellung bereitstellen.
- **Passport-User-Mapping-UPN-Suffix**. Mit diesem Attribut können Sie Verbindungsanforderungen mit Anmelde Informationen für das Windows Live™ ID-Benutzerkonto authentifizieren.
- **Tunneltag**. Dieses Attribut kennzeichnet die VLAN-ID-Nummer, der die Verbindung vom NAS beim Bereitstellen von virtuellen lokalen Netzwerken (VLANs) zugewiesen werden soll.

## <a name="default-connection-request-policy"></a>Standard-Verbindungs Anforderungs Richtlinie

Bei der Installation von NPS wird eine standardmäßige Verbindungs Anforderungs Richtlinie erstellt. Diese Richtlinie weist die folgende Konfiguration auf.

- Die Authentifizierung ist nicht konfiguriert.
- Die Kontoführung ist nicht für das Weiterleiten von Buchhaltungsinformationen an eine Remote-RADIUS-Server Gruppe konfiguriert.
- Das Attribut ist nicht mit Regeln zur Attribut Bearbeitung konfiguriert, die Verbindungsanforderungen an Remote-RADIUS-Server Gruppen weiterleiten.
- Die Weiterleitungs Anforderung ist so konfiguriert, dass Verbindungsanforderungen authentifiziert und auf dem lokalen NPS autorisiert werden.
- Erweiterte Attribute sind nicht konfiguriert.

Die Standard-Verbindungs Anforderungs Richtlinie verwendet NPS als RADIUS-Server. Zum Konfigurieren eines Servers, auf dem NPS ausgeführt wird, der als RADIUS-Proxy fungiert, müssen Sie auch eine Remote-RADIUS-Server Gruppe konfigurieren. Sie können eine neue Remote-RADIUS-Server Gruppe erstellen, während Sie eine neue Verbindungs Anforderungs Richtlinie mithilfe des Assistenten für neue Verbindungs Anforderungs Richtlinien erstellen. Sie können entweder die Standard-Verbindungs Anforderungs Richtlinie löschen oder überprüfen, ob die standardmäßige Verbindungs Anforderungs Richtlinie die letzte Richtlinie ist, die von NPS verarbeitet wurde, indem Sie Sie zuletzt in der geordneten Liste der Richtlinien platzieren.

>[!NOTE]
>Wenn NPS und der RAS-Dienst auf demselben Computer installiert sind und der RAS-Dienst für die Windows-Authentifizierung und-Kontoführung konfiguriert ist, ist es möglich, dass die Remote Zugriffs Authentifizierung und die Buchhaltungs Anforderungen an einen RADIUS-Server weitergeleitet werden. . Dies kann vorkommen, wenn die RAS-Authentifizierung und die Buchhaltungs Anforderungen einer Verbindungs Anforderungs Richtlinie entsprechen, die so konfiguriert ist, dass Sie an eine Remote-RADIUS-Server Gruppe weiterleiten werden.
