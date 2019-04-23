---
title: Planen eines NPS als RADIUS-Server
description: Dieses Thema enthält Informationen zu Network Policy Server RADIUS-serverbereitstellung, die Planung der Bereitstellung in Windows Server 2016.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 2900dd2c-0f70-4f8d-9650-ed83d51d509a
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 5fd89ef8d95735b8cbe1334ba51ed0059595dbc3
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59839171"
---
# <a name="plan-nps-as-a-radius-server"></a>Planen eines NPS als RADIUS-Server

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Bei der Bereitstellung des Netzwerkrichtlinienservers \(NPS\) als Server Remote Authentication Dial-in User Service (RADIUS), führt NPS-Authentifizierung, Autorisierung und Kontoführung für verbindungsanforderungen für die lokale Domäne und Domänen die die lokale Domäne vertrauen. Sie können diese Richtlinien für die projektplanung verwenden, um Ihre RADIUS-serverbereitstellung zu vereinfachen.

Diese Richtlinien für die projektplanung enthalten keine Situationen, in denen Sie NPS als RADIUS-Proxy bereitstellen möchten. Wenn Sie NPS als RADIUS-Proxy bereitstellen, leitet NPS verbindungsanforderungen an einen Server, NPS oder andere RADIUS-Server in Remotedomänen, nicht vertrauenswürdigen Domänen oder beides. 

Bevor Sie NPS als RADIUS-Server in Ihrem Netzwerk bereitstellen, verwenden Sie die folgenden Richtlinien, um die Planung Ihrer Bereitstellung.

- Planen Sie die NPS-Konfiguration.

- Planen Sie die RADIUS-Clients.

- Planen Sie die Verwendung von Authentifizierungsmethoden.

- Planen Sie die Netzwerkrichtlinien.

- Planen Sie die NPS-Kontoführung.

## <a name="plan-nps-configuration"></a>Planen der NPS-Konfiguration

Sie müssen entscheiden, in denen NPS Mitglied ist. Für Umgebungen mit mehreren Domänen kann ein NPS authentifizieren, Anmeldeinformationen für Benutzer in der Domäne, von denen er Mitglied ist und für alle Domänen, die die lokale Domäne, der den NPS zu vertrauen. Damit können den NPS, der DFÜ-Eigenschaften von Benutzerkonten während des Autorisierungsprozesses zu lesen, müssen Sie das Computerkonto des NPS auf dem RAS- und die NPSs für jede Domäne hinzufügen.

Nachdem Sie die Domänenmitgliedschaft des NPS festgelegt haben, muss der Server für die Kommunikation mit RADIUS-Clients, die so genannte Netzwerkzugriffsserver, mit dem RADIUS-Protokoll konfiguriert werden. Darüber hinaus können Sie den Typen von Ereignissen von aufgezeichneten NPS konfigurieren den Fall, und Sie eine Beschreibung für den Server eingeben können.

### <a name="key-steps"></a>Wichtige Schritte

Bei der Planung für die NPS-Konfiguration können Sie die folgenden Schritte aus.

- Bestimmen Sie die RADIUS-Ports, die den NPS zum Empfangen von RADIUS-Nachrichten von RADIUS-Clients verwendet. Die Standardports sind UDP-Ports 1812 und 1645 für RADIUS-Authentifizierungsnachrichten und Port 1813 und 1646 für RADIUS-Kontoführungsnachrichten.

- Wenn Sie den NPS mit mehreren Netzwerkadaptern konfiguriert ist, bestimmen Sie die Adapter, die über denen RADIUS-Datenverkehr zugelassen werden soll.

- Geben Sie die Typen von Ereignissen, die auf die im Ereignisprotokoll aufgezeichnet werden sollen. Sie können abgelehnte authentifizierungsanforderungen, Anforderungen für eine erfolgreiche Authentifizierung oder beide Arten von Anforderungen protokollieren.

- Bestimmen Sie, ob Sie mehrere NPS bereitstellen. Um Fehlertoleranz für RADIUS-basierte Authentifizierung und Kontoführung bereitzustellen, verwenden Sie mindestens zwei NPSs. Einen Netzwerkrichtlinienserver als der primäre RADIUS-Server verwendet wird, und der andere als Sicherung verwendet wird. Jeden RADIUS-Client ist auf beiden NPSs konfiguriert. Wenn der primäre NPS nicht verfügbar ist, senden RADIUS-Clients dann Access-Request-Nachrichten an den alternativen NPS.

- Planen Sie das Skript zum Kopieren von einem NPS-Konfiguration auf anderen NPSs Verwaltungsaufwand sparen und um zu verhindern, dass die falsche Konfiguration eines Servers verwendet. NPS enthält die Netsh-Befehle, mit die Sie ganz oder teilweise ein NPS-Konfiguration für den Import in einer anderen NPS kopieren können. Sie können die Befehle an der Eingabeaufforderung Netsh manuell ausführen. Aber wenn Sie Ihre Befehlssequenz als Skript speichern, können Sie das Skript ausführen zu einem späteren Zeitpunkt, wenn Sie die Serverkonfiguration ändern möchten.

## <a name="plan-radius-clients"></a>Planen der RADIUS-clients

RADIUS-Clients sind Netzwerkzugriffsserver, z. B. Drahtloszugriffspunkte, virtuelles privates Netzwerk (VPN)-Servern, 802.1 X-fähigen Switches und DFÜ-Server. RADIUS-Proxys, die Verbindung Anforderungsnachrichten an den RADIUS-Server weiterleiten, sind auch die RADIUS-Clients. NPS unterstützt alle Netzwerkzugriffsserver und RADIUS-Proxys, die Einhaltung der RADIUS-Protokoll wie in RFC 2865, "Remote Authentication Dial-in User Service (RADIUS)," beschrieben und RFC 2866 unter "RADIUS-Kontoführung."

>[!IMPORTANT]
>Access-Clients, z. B. den Clientcomputern sind keine RADIUS-Clients. Sind RADIUS-Clients nur Netzwerkzugriffsserver und Proxyserver, die das RADIUS-Protokoll unterstützen.

Darüber hinaus müssen sowohl der drahtlose Zugriffspunkte als auch der Schalter der 802.1X-Authentifizierung können. Wenn Sie Extensible Authentication-Protokoll bereitstellen möchten \(EAP\) oder Protected Extensible Authentication Protocol \(PEAP\), Zugriffspunkten und Switches, müssen die Verwendung von EAP unterstützen.

Konfigurieren Sie den Zugriffspunkt und dem Zugriffsclient Password Authentication Protocol (PAP) verwenden, um grundlegende Interoperabilität für PPP-Verbindungen für drahtlose Zugriffspunkte zu testen. Verwenden Sie zusätzliche PPP-basierte Authentifizierungsprotokolle wie z. B. PEAP, bis Sie diejenigen getestet haben, die Sie für den Zugriff auf das Netzwerk verwenden möchten.

### <a name="key-steps"></a>Wichtige Schritte

Bei der Planung für RADIUS-Clients, können Sie die folgenden Schritte aus.

- Dokumentieren Sie die anbieterspezifische-Attribute (VSA), die Sie in NPS konfigurieren müssen. Wenn Ihre Netzwerkzugriffsserver VSAs benötigen, melden Sie die VSA-Informationen für die spätere Verwendung, wenn Sie Ihren Netzwerkrichtlinien in NPS konfigurieren. 

- Dokumentieren Sie die IP-Adressen der RADIUS-Clients und den NPS, um die Konfiguration aller Geräte zu vereinfachen. Wenn Sie Ihre RADIUS-Clients bereitstellen, müssen Sie sie an, um das RADIUS-Protokoll mit der NPS IP-Adresse eingegeben haben, als authentifizierendem Server verwenden, konfigurieren. Und wenn Sie NPS für die Kommunikation mit Ihrem RADIUS-Clients konfigurieren, müssen Sie die RADIUS-Client-IP-Adressen eingeben, in der NPS-Snap-in.

- Erstellen Sie gemeinsame geheime Schlüssel für die Konfiguration aus, auf den RADIUS-Clients und der NPS-Snap-in. Sie müssen den RADIUS-Clients konfigurieren, mit einem gemeinsamen geheimen Schlüssel oder Kennwort mit der Sie auch in der NPS-Snap-in beim Konfigurieren der RADIUS-Clients in NPS eingeben.

## <a name="plan-the-use-of-authentication-methods"></a>Planen der Verwendung von Authentifizierungsmethoden

NPS unterstützt beide Authentifizierungsmethoden für Kennwort-basierte und zertifikatbasierte Authentifizierung. Allerdings unterstützen nicht alle Netzwerkzugriffsserver, die gleichen Authentifizierungsmethoden. In einigen Fällen empfiehlt es sich um eine andere Authentifizierungsmethode, die basierend auf dem Zugriff auf das Netzwerk bereitzustellen.

Sie möchten z. B. sowohl drahtlosen und VPN-Zugriff für Ihre Organisation bereitstellen, aber verwenden eine andere Authentifizierungsmethode für jede Art von Zugriff: EAP-TLS für VPN-Verbindungen kann aufgrund der starken Sicherheit die EAP mit Transport Layer Security (EAP-TLS) zur Verfügung und PEAP-MS-CHAP v2 für 802.1X-authentifizierte drahtlose Verbindungen.

PEAP mit Microsoft Challenge Handshake Authentication Protocol Version 2 (PEAP-MS-CHAP v2) ein Feature, mit dem Namen schnell bietet-Wiederherstellung, die speziell für tragbare Computer und andere drahtlose Geräte konzipiert ist. Schnelle Wiederherstellung der Verbindung können Sie drahtlose Clients Verschieben zwischen Drahtloszugriffspunkten in einem Netzwerk ohne jedes Mal erneut die authentifiziert werden, dass sie mit einem neuen Zugriffspunkt zugeordnet. Dies bietet ein besseres Benutzererlebnis für Mobiltelefone und ermöglicht es ihnen, zwischen Zugriffspunkte ohne ihre Anmeldeinformationen erneut eingeben zu verschieben.
Aufgrund der schnellen verbinden, und die Sicherheit, die PEAP-MS-CHAP v2 bereitstellt, PEAP-MS-CHAP v2 ist eine logische Wahl, als Authentifizierungsmethode für drahtlose Verbindungen.

Für VPN-Verbindungen ist EAP-TLS eine zertifikatbasierte Authentifizierung-Methode, die hohe Sicherheit bietet, die Netzwerkdatenverkehr geschützt, auch wenn sie über das Internet von Heim- oder mobilen Computern an Ihrer Organisation VPN-Server übertragen werden.

### <a name="certificate-based-authentication-methods"></a>Zertifikatbasierte Authentifizierungsmethoden

Zertifikatbasierte Authentifizierungsmethoden haben eine hohe Sicherheit; und sie müssen den Nachteil, dass wird schwieriger, als kennwortbasierte Authentifizierungsmethoden bereitstellen.

Sowohl PEAP-MS-CHAP v2 und EAP-TLS sind zertifikatbasierte Authentifizierungsmethoden, aber es gibt viele Unterschiede zwischen ihnen und die Möglichkeit, in der sie bereitgestellt werden.

### <a name="eap-tls"></a>EAP-TLS

EAP-TLS verwendet Zertifikate für Client- und Serverauthentifizierung und erfordert, dass Sie eine public Key-Infrastruktur (PKI) in Ihrer Organisation bereitstellen. Bereitstellung einer PKI kann komplex sein und erfordert eine Planungsphase, die der Planung für die Verwendung von NPS als RADIUS-Server unabhängig ist.

Mit EAP-TLS, registriert den NPS ein Serverzertifikat von einer Zertifizierungsstelle \(Zertifizierungsstelle\), und das Zertifikat auf dem lokalen Computer im Zertifikatspeicher gespeichert ist. Tritt auf, Server-Authentifizierung, während der Authentifizierung Wenn der NPS das Serverzertifikat an den Zugriffsclient als Beleg für dessen Identität an den Zugriffsclient sendet. Der Access-Client überprüft verschiedene Zertifikateigenschaften, um zu bestimmen, ob das Zertifikat gültig ist und eignet sich für die Verwendung während der Server-Authentifizierung. Wenn das Server-Zertifikat die Mindestanforderungen für Serverzertifikate erfüllt und wird von einer Zertifizierungsstelle ausgegeben, die der Zugriffsclient vertraut, wird der NPS vom Client erfolgreich authentifiziert.

Auf ähnliche Weise erfolgt die Clientauthentifizierung während des Authentifizierungsprozesses sendet der Client das Clientzertifikat an den NPS, um seine Identität an den NPS zu bestätigen. Der NPS untersucht das Zertifikat, und wenn das Clientzertifikat die minimale Client-Zertifikat erfüllt und wird von einer Zertifizierungsstelle ausgegeben, der den NPS vertraut, wird der Access-Client erfolgreich durch den NPS authentifiziert.

Zwar es ist erforderlich, dass das Serverzertifikat im Zertifikatspeicher für den NPS gespeichert wird, das Zertifikat für Client oder Benutzer kann gespeichert werden in den Zertifikatspeicher auf dem Client oder auf einer Smartcard.

Für diesen Authentifizierungsprozess erfolgreich ist, ist es erforderlich, dass auf allen Computern Ihres Unternehmens-ZS-Zertifikat im Zertifikatspeicher vertrauenswürdige Stammzertifizierungsstellen für den lokalen Computer und der aktuelle Benutzer sein.

### <a name="peap-ms-chap-v2"></a>PEAP-MS-CHAP v2

PEAP-MS-CHAP v2 verwendet ein Zertifikat für Server-Authentifizierung und Kennwörtern basierende Anmeldeinformationen für die Benutzerauthentifizierung. Da Zertifikate nur für Server-Authentifizierung verwendet werden, sind Sie nicht erforderlich, um eine PKI bereitstellen, um die PEAP-MS-CHAP v2 verwenden. Wenn Sie PEAP-MS-CHAP v2 bereitstellen, können Sie ein Serverzertifikat für den NPS in einem der beiden folgenden Methoden abrufen:

- Sie können Active Directory-Zertifikatdienste (AD CS), und klicken Sie dann auf Zertifikate automatisch registrieren, NPSs installieren. Wenn Sie diese Methode verwenden, müssen Sie auch das CA-Zertifikat auf Clientcomputern Herstellen einer Verbindung mit Ihrem Netzwerk, damit sie das Zertifikat ausgestellt an den NPS vertrauen registrieren.

- Sie können ein Serverzertifikat von einer öffentlichen Zertifizierungsstelle wie VeriSign erwerben. Wenn Sie diese Methode verwenden, stellen Sie sicher, dass Sie eine ZS auswählen, die bereits von den Clientcomputern als vertrauenswürdig eingestuft wird. Um zu bestimmen, ob Clientcomputer über eine Zertifizierungsstelle vertrauen, öffnen Sie das Zertifikate Microsoft Management Console (MMC)-Snap-in auf einem Clientcomputer, und zeigen Sie dann auf den Speicher für vertrauenswürdige Stammzertifizierungsstellen für den lokalen Computer und für den aktuellen Benutzer. Wenn ein Zertifikat von der Zertifizierungsstelle in diese Zertifikatspeicher vorhanden ist, wird der Clientcomputer der Zertifizierungsstelle vertraut und werden daher alle von der Zertifizierungsstelle ausgestelltes Zertifikat vertrauen.

Während des Authentifizierungsprozesses mit PEAP-MS-CHAP v2 tritt auf, Server-Authentifizierung, wenn der NPS das Serverzertifikat auf dem Clientcomputer gesendet. Der Access-Client überprüft verschiedene Zertifikateigenschaften, um zu bestimmen, ob das Zertifikat gültig ist und eignet sich für die Verwendung während der Server-Authentifizierung. Wenn das Server-Zertifikat die Mindestanforderungen für Serverzertifikate erfüllt und wird von einer Zertifizierungsstelle ausgegeben, die der Zugriffsclient vertraut, wird der NPS vom Client erfolgreich authentifiziert.

Benutzerauthentifizierung tritt auf, wenn ein Benutzer versucht, die zur Verbindung mit Typen kennwortbasierten Anmeldeinformationen für das Netzwerk, und versucht, sich anzumelden. NPS die Anmeldeinformationen empfängt und ausführt, Authentifizierung und Autorisierung. Wenn der Benutzer authentifiziert und autorisiert ist und der Clientcomputer erfolgreich auf den NPS authentifiziert, wird die verbindungsanforderung gewährt.

### <a name="key-steps"></a>Wichtige Schritte

Bei der Planung für die Verwendung der Authentifizierungsmethoden, können Sie die folgenden Schritte aus.

- Identifizieren Sie die Typen von sollen wie WLAN, VPN, 802.1 X-fähige Switch, bieten Zugriff auf das Netzwerk und DFÜ-Zugriff.

- Bestimmen Sie die Authentifizierungsmethode oder Methoden, die Sie für jede Art von Zugriff verwenden möchten. Es wird empfohlen, dass Sie die zertifikatbasierte Authentifizierungsmethoden verwenden, die hohe Sicherheit bereitstellen; Allerdings es möglicherweise nicht für Sie eine PKI, bereitstellen, damit andere Authentifizierungsmethoden möglicherweise eine bessere Ausgewogenheit von Sie für Ihr Netzwerk was bereitstellen.

- Wenn Sie EAP-TLS bereitstellen, Planen der PKI-Bereitstellung. Dies umfasst das Planen von der Zertifikatvorlagen, die Sie beabsichtigen, die für Serverzertifikate und Clientcomputerzertifikate zu verwenden. Darüber hinaus bestimmen, wie zum Registrieren von Zertifikaten für Domänenbenutzer-Mitglied kein Domänenmitglied ist, und -Computer ermitteln, ob Smartcards verwenden möchten.

- Wenn Sie PEAP-MS-CHAP v2 bereitstellen, bestimmen Sie, ob zum Installieren von AD CS zum Ausstellen von Serverzertifikaten Ihre NPSs oder, ob Sie von einer öffentlichen Zertifizierungsstelle wie VeriSign-Serverzertifikate erwerben möchten.

### <a name="plan-network-policies"></a>Planen Sie die Netzwerkrichtlinien

Netzwerkrichtlinien werden von NPS verwendet, um festzustellen, ob die Weiterleitung von verbindungsanforderungen von RADIUS-Clients empfangen autorisiert sind. NPS verwendet auch die Einwähleigenschaften des Benutzerkontos ein, um eine Autorisierung Entscheidung zu treffen.

Da Richtlinien für Netzwerke in der Reihenfolge verarbeitet werden, in denen sie die NPS-Snap-in angezeigt werden, Planen Sie, die am stärksten einschränkende Richtlinien zuerst in der Liste der Richtlinien zu platzieren. NPS versucht, für jede verbindungsanforderung den Bedingungen der Richtlinie mit den Eigenschaften der Anforderung übereinstimmen. NPS untersucht jede Netzwerkrichtlinie in der Reihenfolge, bis eine Übereinstimmung gefunden wird. Wenn es keine Übereinstimmung findet, wird die verbindungsanforderung zurückgewiesen.

### <a name="key-steps"></a>Wichtige Schritte

Bei der Planung für Netzwerkrichtlinien, können Sie die folgenden Schritte aus.

- Bestimmen Sie die bevorzugte Verarbeitungsreihenfolge der NPS-von Netzwerkrichtlinien, vom restriktivsten zum am wenigsten restriktiven.

- Bestimmen Sie den Richtlinienstatus. Der Zustand der Richtlinie kann der Wert haben, aktiviert oder deaktiviert. Wenn die Richtlinie aktiviert ist, wertet NPS die Richtlinie beim Ausführen der Autorisierung. Wenn die Richtlinie nicht aktiviert ist, wird sie nicht ausgewertet.

- Bestimmen Sie den Richtlinientyp an. Sie müssen bestimmen, ob die Richtlinie konzipiert ist, um Zugriff zu gewähren, wenn die Bedingungen der Richtlinie, durch die verbindungsanforderung oder gibt an, ob die Richtlinie dient entsprechen, den Zugriff verweigern, wenn die Bedingungen der Richtlinie die verbindungsanforderung entsprechen. Wenn Sie die Mitglieder einer Windows-Gruppe drahtlosen Zugriff explizit verweigern möchten, können Sie z. B. eine Netzwerkrichtlinie erstellen, die angibt, die Gruppe, die Methode der drahtlosen Verbindung und, hat eine Richtlinie aus, geben Sie die Einstellung der Zugriff verweigern.

- Bestimmen Sie, ob NPS, um die DFÜ-Eigenschaften von Benutzerkonten zu ignorieren, die Mitglieder der Gruppe sind, auf denen die Richtlinie basiert. Wenn diese Einstellung nicht aktiviert ist, überschreiben die DFÜ-Eigenschaften von Benutzerkonten, Einstellungen, die in den Netzwerkrichtlinien konfiguriert sind. Beispielsweise wird, wenn eine Netzwerkrichtlinie konfiguriert ist, die Zugriff für einen Benutzer, aber die Einwähleigenschaften des Benutzerkontos für den Benutzer, den Zugriff verweigern festgelegt, der Benutzer Zugriff verweigert. Aber wenn Sie die Richtlinie Einstellung ignorieren Benutzer Konto einwählen Typeigenschaften aktivieren, wird die gleiche Benutzer Zugriff auf das Netzwerk gewährt.

- Bestimmen Sie, ob die Richtlinie die richtlinieneinstellung für die Datenquelle verwendet. Mit dieser Einstellung können Sie problemlos eine Quelle für alle zugriffsanforderungen angeben. Mögliche Quellen sind ein Terminal Services Gateway (TS Gateway), RAS-Server (VPN oder DFÜ-), ein DHCP-Server, einem drahtlosen Zugriffspunkt und eine Integritätsregistrierungsstelle-Server. Alternativ können Sie eine anbieterspezifische Quelle angeben.

- Bestimmen Sie die Bedingungen, die in der Reihenfolge für die Netzwerkrichtlinie, die angewendet werden, erfüllt werden müssen.

- Bestimmen Sie die Einstellungen, die angewendet werden, wenn die Bedingungen der Netzwerkrichtlinie die verbindungsanforderung entsprechen.

- Bestimmen Sie, ob Sie verwenden möchten, verwenden, ändern oder löschen die Standard-Netzwerkrichtlinien.

## <a name="plan-nps-accounting"></a>Planen Sie die NPS-Kontoführung

NPS ermöglicht das Protokollieren von RADIUS-Kontoführungsdaten wie Benutzerauthentifizierung und kontoführungsanforderungen, in drei Formaten: IAS-Format, datenbankkompatibles Format und Microsoft SQL Server-Protokollierung. 

IAS-Format und datenbankkompatibles Format erstellen Protokolldateien auf den lokalen NPS in Textformat an. 

SQL Server-Protokollierung ermöglicht das Protokollieren auf einem SQL Server 2000 oder SQL Server 2005-XML-kompatiblen Datenbank, erweitern die RADIUS-Kontoführung, um die Vorteile der Protokollierung in einer relationalen Datenbank zu nutzen.

### <a name="key-steps"></a>Wichtige Schritte

Bei der Planung für die NPS-Kontoführung, können Sie die folgenden Schritte aus.

- Bestimmen Sie, ob der NPS-Buchhaltungsdaten in Protokolldateien oder in einer SQL Server-Datenbank gespeichert werden soll.

### <a name="nps-accounting-using-local-log-files"></a>NPS-ressourcenerfassung mithilfe von lokalen Log-Dateien

Aufzeichnen der Benutzerauthentifizierung und Berücksichtigung der Anforderungen in Protokolldateien dient in erster Linie für verbindungszwecke für Analyse und Abrechnung und kann auch eine Untersuchung Sicherheitstool, bietet Ihnen eine Methode zum Nachverfolgen der Aktivität von einem böswilligen Benutzer nach einer angreifen.

### <a name="key-steps"></a>Wichtige Schritte

Bei der Planung für die NPS-Kontoführung lokalen Protokolldateien verwenden, können Sie die folgenden Schritte aus.

- Bestimmen Sie die Datei im Textformat, das Sie für die NPS-Protokolldateien verwenden möchten.

- Wählen Sie den Typ der Informationen, die Sie protokollieren möchten. Sie können kontoführungsanforderungen, authentifizierungsanforderungen und der periodische Status protokollieren.

- Bestimmen Sie den Speicherort der Festplatte zum Speichern der Log-Dateien werden sollen.

- Entwerfen Sie Ihre backup Log-Datei-Lösung. Der Speicherort der Festplatte, in dem Sie Ihre Protokolldateien speichern, sollte es sich um einen Speicherort sein, der Ihnen ermöglicht, Ihre Daten einfach zu sichern. Darüber hinaus sollte der Speicherort der Festplatte geschützt werden, konfigurieren Sie die Zugriffssteuerungsliste (ACL) für den Ordner, in dem die Protokolldateien gespeichert werden.

- Bestimmen Sie die Häufigkeit, mit der Sie neue Protokolldateien erstellt werden soll. Wenn Sie Log-Dateien basierend auf der Dateigröße erstellt werden sollen, bestimmen Sie die maximale Dateigröße, die zulässig sind, bevor eine neue Protokolldatei, von NPS erstellt wird.

- Bestimmen Sie, ob NPS ältere Protokolldateien löschen, wenn die Festplatte nicht mehr genügend Speicherplatz.

- Bestimmen Sie die Anwendung oder Anwendungen, die Buchhaltungsdaten anzeigen und Erstellen von Berichten verwenden möchten.

### <a name="nps-sql-server-logging"></a>NPS SQL Server-Protokollierung

NPS SQL Server-Protokollierung wird verwendet, wenn Sie möchten Statusinformationen von Sitzungen, für die berichterstellung und Analysen für Daten, und Zentralisierung und Vereinfachung der Verwaltung von Buchhaltungsdaten.

NPS bietet die Möglichkeit, verwenden Sie SQL Server-Protokollierung für die Benutzerauthentifizierung aufzeichnen und Berücksichtigung der Anforderungen von ein oder mehrere Netzwerkzugriffsserver an eine Datenquelle auf einem Computer mit Microsoft SQL Server Desktop Engine \(MSDE 2000\), oder eine beliebige Version von SQL Server als SQL Server 2000.

Buchhaltungsdaten werden im XML-Format von NPS übergeben, um eine gespeicherte Prozedur in der Datenbank, die sowohl strukturierte Abfragesprache unterstützt die \(SQL\) und XML- \(SQLXML\). Aufzeichnen der Benutzerauthentifizierung und Berücksichtigung der Anforderungen in einer XML-kompatibler SQL Server-Datenbank können mehrere NPSs eine Datenquelle haben.

### <a name="key-steps"></a>Wichtige Schritte

Bei der Planung für die Kontoführung von NPS mithilfe von NPS SQL Server-Protokollierung, können Sie die folgenden Schritte aus.

- Bestimmen Sie, ob Sie oder ein anderes Mitglied Ihrer Organisation verfügt über SQL Server 2000 oder SQL Server 2005 Entwicklung relationaler Datenbanken auftreten, und Sie wissen, wie diese Produkte zu erstellen, ändern, verwalten und Verwalten von SQL Server-Datenbanken verwenden.

- Bestimmen Sie, ob SQL Server auf den NPS oder auf einem Remotecomputer installiert ist.

- Entwerfen Sie die gespeicherte Prozedur, die Sie in der SQL Server-Datenbank verwenden zum Verarbeiten von eingehenden XML-Dateien, die NPS-Buchhaltungsdaten enthalten.

- Entwerfen Sie die SQL Server-Datenbank-Replikation-Struktur und ablaufsteuerung.

- Bestimmen Sie die Anwendung oder Anwendungen, die Buchhaltungsdaten anzeigen und Erstellen von Berichten verwenden möchten.

- Planen der Verwendung von Netzwerkzugriffsserver, die das Attribut der Klasse in allen Accounting-Anforderungen senden. Das Attribut der Klasse wird an den RADIUS-Client in einer Access-Accept-Nachricht gesendet, und eignet sich zum Korrelieren von Accounting-Request-Nachrichten mit authentifizierungssitzungen. Wenn das Attribut der Klasse von Network Access Server in der Accounting-Request-Meldungen gesendet wird, kann es entsprechend der Buchhaltung und Authentifizierung Einträge verwendet werden. Die Kombination aus den Attributen, die Unique-Seriennummer, Service-Neustart-Time- und Serveradresse muss eine eindeutige Kennung für die einzelnen Authentifizierungen, die der Server akzeptiert.

- Planen der Verwendung von Netzwerkzugriffsserver, die zwischenzeitliche Kontoführung unterstützen.

- Planen der Verwendung von Netzwerkzugriffsserver, die Kontoführung für und Accounting-off-Nachrichten senden.

- Planen der Verwendung von Netzwerkzugriffsserver, die unterstützen die Speicherung und Weiterleitung von Buchhaltungsdaten. Netzwerkzugriffsserver, die Unterstützung dieser Funktion können Accounting-Daten speichern, wenn Network Access Server mit NPS kommunizieren kann. Wenn der NPS verfügbar ist, leitet Network Access Server gespeicherten Datensätze an den NPS, verbessert sich seine Zuverlässigkeit in der Buchhaltung über Netzwerkzugriffsserver, die keine diese Funktion bieten bereitstellen.

- Möchten Sie immer das Acct-Interim-Interval-Attribut in Netzwerkrichtlinien konfigurieren. Das Acct-Interim-Interval-Attribut, die das Intervall (in Sekunden) zwischen jeder zwischenzeitliche Aktualisierung, die Network Access Server sendet festgelegt wird. Gemäß RFC 2869 der Wert des Attributs Acct-Interim-Interval darf nicht kleiner als 60 Sekunden oder eine Minute lang sein und darf nicht kleiner ist als 600 Sekunden oder 10 Minuten sein. Weitere Informationen finden Sie unter RFC 2869, "RADIUS-Erweiterungen".

- Stellen Sie sicher, dass Ihre NPSs Protokollierung der periodische Status aktiviert ist.

