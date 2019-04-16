---
title: Planen Sie NPS als RADIUS-server
description: Dieses Thema enthält Informationen zur Planung der Bereitstellung in Windows Server 2016 Network Policy Server RADIUS-Server-Bereitstellung.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 2900dd2c-0f70-4f8d-9650-ed83d51d509a
ms.author: pashort
author: shortpatti
ms.openlocfilehash: e9bb95428c17e5d7bde588693e84288ddfe64531
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="plan-nps-as-a-radius-server"></a>Planen Sie NPS als RADIUS-server

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Bei der Bereitstellung des Netzwerkrichtlinienservers \(NPS\) als Server Remote Authentication Dial-in User Service (RADIUS) führt NPS-Authentifizierung, Autorisierung und Kontoführung für verbindungsanforderungen für die lokale Domäne und Domänen, die die lokale Domäne vertrauen. Diese Richtlinien, Planung können Sie um die RADIUS-Bereitstellung zu vereinfachen.

Diese planungsempfehlungen enthalten nicht Situationen, in denen Sie NPS als RADIUS-Proxy bereitstellen möchten. Wenn Sie NPS als RADIUS-Proxy bereitstellen, leitet NPS verbindungsanforderungen zu einem Server mit NPS oder andere RADIUS-Server in den Remotedomänen, nicht vertrauenswürdigen Domänen oder beides. 

Bevor Sie NPS als RADIUS-Server in Ihrem Netzwerk bereitstellen, verwenden Sie die folgenden Richtlinien zum Planen der Bereitstellung.

- Planen der NPS-Serverkonfiguration.

- Planen der RADIUS-Clients.

- Planen Sie die Verwendung von Authentifizierungsmethoden.

- Planen Sie die Netzwerkrichtlinien.

- Planen Sie die NPS-Kontoführung.

## <a name="plan-nps-server-configuration"></a>Planen der NPS-Serverkonfiguration

Sie müssen entscheiden, in dem der NPS-Server angehört. Für Umgebungen mit mehreren Domänen kann ein NPS-Server authentifizieren Anmeldeinformationen für Benutzerkonten in der Domäne von der er Mitglied ist und für alle Domänen, die die lokale Domäne des Netzwerkrichtlinienservers zu vertrauen. Damit können den NPS-Server, die DFÜ-Eigenschaften von Benutzerkonten während des Autorisierungsprozesses zu lesen, müssen Sie das Computerkonto des NPS-Servers RAS- und NPS-Servers-Gruppe für jede Domäne hinzufügen.

Nachdem Sie die Domänenmitgliedschaft des NPS-Servers ermittelt haben, muss der Server konfiguriert werden, um die Kommunikation mit RADIUS-Clients, die auch als Netzwerkzugriffsserver, mit dem RADIUS-Protokoll bezeichnet. Darüber hinaus können Sie den Typen von Ereignissen, die von NPS aufgezeichnet konfigurieren im Ereignisprotokoll und eine Beschreibung für den Server eingeben können.

### <a name="key-steps"></a>Wichtige Schritte

Bei der Planung für die NPS-Serverkonfiguration, können Sie die folgenden Schritte aus.

- Bestimmen Sie die RADIUS-Ports, die der NPS-Server zum Empfangen von RADIUS-Nachrichten von RADIUS-Clients verwendet. Die Standardports sind UDP-Ports 1812 und 1645 für RADIUS-Authentifizierungsnachrichten und Ports 1813 und 1646 für RADIUS-Kontoführungsnachrichten.

- Wenn der NPS-Server mit mehreren Netzwerkadaptern konfiguriert ist, bestimmen Sie die Adapter, über denen RADIUS-Datenverkehr zugelassen werden soll.

- Bestimmen der Typen von Ereignissen, die NPS im Ereignisprotokoll aufgezeichnet werden sollen. Sie können abgelehnte authentifizierungsanforderungen, erfolgreiche Authentifizierung oder beide Arten von Anforderungen protokollieren.

- Bestimmen Sie, ob Sie mehrere NPS-Server bereitstellen. Verwenden Sie zum Bereitstellen von Fehlertoleranz für RADIUS-basierte Authentifizierung und-Kontoführung mindestens zwei NPS-Server. Einen Netzwerkrichtlinienserver als der primäre RADIUS-Server verwendet wird, und das andere als Sicherung verwendet wird. Anschließend wird jeden RADIUS-Client auf beiden Servern NPS konfiguriert. Wenn der primäre NPS-Server nicht verfügbar ist, senden RADIUS-Clients Zugriff-Anforderungsnachrichten klicken Sie dann auf den anderen NPS-Server.

- Planen Sie das Skript verwendet, um einen NPS-Serverkonfiguration für andere Netzwerkrichtlinienserver, Verwaltungsaufwand zu sparen und die falsche Konfiguration von einem Server zu kopieren. NPS enthält die Netsh-Befehle, die Ihnen ermöglichen, kopieren Sie alle oder einen Teil der Konfiguration eines NPS-Servers auf einen anderen NPS-Server zu importieren. Sie können die Befehle an der Eingabeaufforderung Netsh manuell ausführen. Jedoch, wenn Sie die Befehlsfolge als Skript speichern, können Sie das Skript ausführen zu einem späteren Zeitpunkt möchten Sie Ihre Serverkonfigurationen zu ändern.

## <a name="plan-radius-clients"></a>Planen der RADIUS-clients

RADIUS-Clients sind Netzwerkzugriffsserver, z. B. Drahtloszugriffspunkte, virtuelles privates Netzwerk (VPN)-Servern, 802.1 X-fähigen Switches und DFÜ-Server. RADIUS-Proxys, die Verbindung Anforderungsnachrichten RADIUS-Server weitergeleitet werden, sind auch RADIUS-Clients. NPS unterstützt alle Netzwerkzugriffsserver und RADIUS-Proxys, die RADIUS erfüllen-Protokoll wie in RFC 2865, "Remote Authentication Dial-in User Service (RADIUS)" beschrieben und RFC 2866, "RADIUS-Kontoführung."

>[!IMPORTANT]
>Access-Clients, z. B. Clientcomputer sind nicht RADIUS-Clients. Sind RADIUS-Clients nur Netzwerkzugriffsserver und Proxyserver, die das RADIUS-Protokoll unterstützen.

Drahtlose Zugriffspunkte und Switches muss außerdem der 802. 1 X-Authentifizierung. Wenn Sie die Extensible Authentication Protocol \(EAP\) oder Protected Extensible Authentication Protocol \(PEAP\) bereitstellen möchten, müssen Zugriffspunkte und Switches die Verwendung von EAP unterstützen.

Konfigurieren Sie zum Testen der grundlegenden Interoperabilität für PPP-Verbindungen für drahtlose Zugriffspunkte Zugriffspunkt und der Zugriffsclient (PAP = Password Authentication Protocol) verwenden. Verwenden Sie zusätzliche PPP-basierte Authentifizierungsprotokolle, wie z. B. PEAP, bis Sie diejenigen getestet haben, die Sie für den Zugriff auf das Netzwerk verwenden möchten.

### <a name="key-steps"></a>Wichtige Schritte

Bei der Planung für RADIUS-Clients können Sie die folgenden Schritte aus.

- Dokumentieren Sie die anbieterspezifische herstellerspezifische Attribute, die müssen Sie in NPS konfigurieren. Wenn Ihre Netzwerkzugriffsserver herstellerspezifische benötigen, protokollieren Sie herstellerspezifisches Attribut Informationen zur späteren Verwendung, wenn Sie auf dem Netzwerkrichtlinienserver Netzwerkrichtlinien konfigurieren. 

- Dokumentieren Sie die IP-Adressen von RADIUS-Clients und dem NPS-Server, um die Konfiguration aller Geräte zu vereinfachen. Wenn Sie Ihre RADIUS-Clients bereitstellen, müssen Sie, um die RADIUS-Protokoll, mit der NPS-Server IP-Adresse als der authentifizierende Server eingegeben verwenden konfigurieren. Und wenn Sie NPS zur Kommunikation mit RADIUS-Clients konfigurieren, müssen Sie die RADIUS-Client-IP-Adressen eingeben, in der NPS-Snap-in.

- Erstellen Sie gemeinsame geheime Schlüssel für die Konfiguration auf den RADIUS-Clients und dem NPS-Snap-in. Sie müssen RADIUS-Clients konfigurieren, mit einem gemeinsamen geheimen Schlüssel oder ein Kennwort, die Sie in der NPS-Snap-in beim Konfigurieren von RADIUS-Clients in NPS auch eingeben werden.

## <a name="plan-the-use-of-authentication-methods"></a>Planen der Verwendung von Authentifizierungsmethoden

NPS unterstützt beide Kennwort-basierte und zertifikatbasierte Authentifizierungsmethoden. Nicht alle Netzwerkzugriffsserver unterstützen jedoch die gleichen Authentifizierungsmethoden. In einigen Fällen möchten Sie möglicherweise eine andere Authentifizierungsmethode, die basierend auf dem Typ des Netzwerkzugriffs bereitstellen.

Sie können z. B. drahtlose und VPN-Zugriff für Ihre Organisation bereitstellen, sondern verwenden eine andere Authentifizierungsmethode für jede Art von Zugriff: EAP-TLS für die VPN-Verbindungen sind aufgrund der hohes Maß an Sicherheit die EAP with Transport Layer Security (EAP-TLS) zur Verfügung und PEAP-MS-CHAP v2 für den 802.1X-authentifizierten drahtlosen Verbindungen.

Schließen Sie PEAP mit Microsoft Challenge Handshake Authentication Protocol Version 2 (PEAP-MS-CHAP v2) eine Funktion, die mit dem Namen schnell bereitstellt, die speziell für tragbare Computer und andere drahtlose Geräte entwickelt wurde. Schnelle Wiederherstellung der Verbindung können Drahtlosclients zwischen Drahtloszugriffspunkten im selben Netzwerk ohne wird jedes Mal erneut authentifiziert, dass sie mit einem neuen Zugriffspunkt ordnen verschieben. Dies bietet eine bessere Erfahrung für Benutzer und ermöglicht es ihnen, Verschieben zwischen Zugriffspunkten ohne ihre Anmeldeinformationen erneut eingeben zu müssen.
Aufgrund der schnell schließen, und die Sicherheit, die PEAP-MS-CHAP v2 zur Verfügung stellt, PEAP-MS-CHAP v2 ist eine logische Wahl als Authentifizierungsmethode für drahtlose Verbindungen.

Für die VPN-Verbindungen ist EAP-TLS eine zertifikatbasierte Authentifizierung-Methode, die hohe Sicherheit, die den Netzwerkdatenverkehr geschützt werden bietet, auch bei der Übertragung über das Internet von Heim- oder mobilen Computern Ihrer Organisation VPN-Server.

### <a name="certificate-based-authentication-methods"></a>Zertifikatbasierte Authentifizierungsmethoden

Zertifikatbasierte Authentifizierungsmethoden sind eine hohes Maß an Sicherheit. und sie haben den Nachteil wird schwieriger, als kennwortbasierte Authentifizierungsmethoden bereitstellen.

PEAP-MS-CHAP v2 und EAP-TLS zertifikatbasierte Authentifizierungsmethoden sind, aber es gibt viele Unterschiede zwischen ihnen und die Art und Weise, in der sie bereitgestellt werden.

### <a name="eap-tls"></a>EAP-TLS

EAP-TLS-Zertifikate für Client- und Server-Authentifizierung verwendet, und setzt voraus, dass Sie eine public Key-Infrastruktur (PKI) in Ihrer Organisation bereitstellen. Bereitstellung einer PKI kann sehr komplex sein und erfordert eine Planungsphase, die bei der Planung für die Verwendung von NPS als RADIUS-Server unabhängig ist.

Mit EAP-TLS, registriert der NPS-Server ein Serverzertifikat von einer Zertifizierungsstelle \(CA\) und das Zertifikat auf dem lokalen Computer im Zertifikatspeicher gespeichert wird. Während des Authentifizierungsprozesses erfolgt, die Server-Authentifizierung, wenn der NPS-Server das Serverzertifikat auf Clientseite, Zugriff auf seine Identität gegenüber dem Zugriffsclient nach sendet. Der RAS-Client überprüft die verschiedenen Zertifikateigenschaften, um zu bestimmen, ob das Zertifikat gültig ist und eignet sich für die Verwendung bei der Server-Authentifizierung. Wenn das Serverzertifikat die Mindestanforderungen für Serverzertifikate erfüllt und der Ausstellung durch eine Zertifizierungsstelle, die der Zugriffsclient vertraut, wird der NPS-Server erfolgreich vom Client authentifiziert.

Auf ähnliche Weise auftritt Clientauthentifizierung während der Authentifizierung, sendet der Client die Client-Zertifikat auf dem NPS-Server, auf dem NPS-Server seine Identität nach. Der NPS-Server überprüft das Zertifikat, und wenn das Clientzertifikat die minimale Client-Zertifikat erfüllt und von einer Zertifizierungsstelle, die Vertrauensstellungen der NPS-Server ausgestellt wird, wird der RAS-Client erfolgreich vom NPS-Server authentifiziert.

Obwohl es ist erforderlich, dass das Zertifikat im Zertifikatspeicher auf dem NPS-Server gespeichert wird, den Client oder Benutzerzertifikat gespeichert werden in den Zertifikatspeicher auf dem Client oder auf einer Smartcard.

Für diesen Authentifizierungsprozess erfolgreich ausgeführt werden kann, ist es erforderlich, dass alle Computer Ihres Unternehmens-ZS-Zertifikat im Zertifikatspeicher vertrauenswürdige Stammzertifizierungsstellen für den lokalen Computer und den aktuellen Benutzer verfügen.

### <a name="peap-ms-chap-v2"></a>PEAP-MS-CHAP v2

PEAP-MS-CHAP v2 verwendet ein Zertifikat für die Serverauthentifizierung und Anmeldeinformationen für die Benutzerauthentifizierung. Da Zertifikate nur für die Serverauthentifizierung verwendet werden, sind Sie nicht erforderlich, um die Bereitstellung einer PKI um PEAP-MS-CHAP v2 verwenden. Beim Bereitstellen von PEAP-MS-CHAP v2 können Sie ein Serverzertifikat für den NPS-Server in einem der folgenden zwei Arten abrufen:

- Sie können Active Directory-Zertifikatdienste (AD CS), und klicken Sie dann auf Zertifikate automatisch registrieren zum NPS-Server installieren. Wenn Sie diese Methode verwenden, müssen Sie auch das Zertifizierungsstellenzertifikat auf Clientcomputern, die mit dem Netzwerk verbinden, damit sie das Zertifikat ausgestellt für den NPS-Server vertrauen registrieren.

- Sie können ein Serverzertifikat von einer öffentlichen Zertifizierungsstelle wie VeriSign erwerben. Wenn Sie diese Methode verwenden, stellen Sie sicher, dass Sie eine Zertifizierungsstelle auswählen, die bereits von Clientcomputern als vertrauenswürdig eingestuft wird. Bestimmen, ob Clientcomputer eine Zertifizierungsstelle vertrauen, die Zertifikate Microsoft Management Console (MMC)-Snap-in auf einem Clientcomputer öffnen Sie, und zeigen Sie dann den Speicher vertrauenswürdiger Stammzertifizierungsstellen-Speicher für den lokalen Computer und für den aktuellen Benutzer. Wenn ein Zertifikat von der Zertifizierungsstelle an diese Zertifikatspeicher vorhanden ist, wird der Clientcomputer der Zertifizierungsstelle vertraut und werden daher alle von der Zertifizierungsstelle ausgestellte Zertifikat vertrauen.

Während der Authentifizierung mit PEAP-MS-CHAP v2 tritt auf, Server-Authentifizierung, wenn der NPS-Server das Serverzertifikat für den Client gesendet. Der RAS-Client überprüft die verschiedenen Zertifikateigenschaften, um zu bestimmen, ob das Zertifikat gültig ist und eignet sich für die Verwendung bei der Server-Authentifizierung. Wenn das Serverzertifikat die Mindestanforderungen für Serverzertifikate erfüllt und der Ausstellung durch eine Zertifizierungsstelle, die der Zugriffsclient vertraut, wird der NPS-Server erfolgreich vom Client authentifiziert.

Benutzerauthentifizierung tritt auf, wenn ein Benutzer versucht, die Verbindung mit Typen Kennwörtern basierende Anmeldeinformationen für das Netzwerk, und versucht, sich anzumelden. NPS empfängt die Anmeldeinformationen und führt die Authentifizierung und Autorisierung. Wenn der Benutzer authentifiziert und autorisiert erfolgreich ist und der Clientcomputer den NPS-Server erfolgreich authentifiziert, wird die verbindungsanforderung gewährt.

### <a name="key-steps"></a>Wichtige Schritte

Bei der Planung für die Verwendung von Authentifizierungsmethoden, können Sie die folgenden Schritte aus.

- Identifizieren Sie die Typen von Netzwerk Sie z. B. drahtlos, VPN, 802.1 X-fähigen Switch anbieten möchten und DFÜ-Zugriff.

- Bestimmen Sie die Authentifizierungsmethode oder Methoden, die Sie für jede Art von Zugriff verwenden möchten. Es wird empfohlen, die zertifikatbasierte Authentifizierungsmethoden zu verwenden, die hohes Maß an Sicherheit zu bieten; Allerdings es möglicherweise nicht für Sie eine PKI bereitstellen, damit andere Authentifizierungsmethoden besser abwägen Sie für Ihr Netzwerk benötigen bereitstellen können.

- Wenn Sie EAP-TLS bereitstellen, Planen der PKI-Bereitstellung. Dies umfasst das Planen der Zertifikatvorlagen, die Sie für Serverzertifikate und Clientzertifikate für Computer verwenden möchten. Darüber hinaus Bestimmen der Vorgehensweise beim Registrieren von Zertifikaten für Domänenmitglied und keine Domänenmitglieder sind, und ermitteln, ob Smartcards verwenden möchten.

- Bereitstellen von PEAP-MS-CHAP v2 bestimmen Sie, ob Sie AD CS zum Ausstellen von Zertifikaten, die NPS-Server oder ob Sie Zertifikate von einer öffentlichen Zertifizierungsstelle wie VeriSign erwerben möchten Server installieren möchten.

### <a name="plan-network-policies"></a>Planen von Netzwerkrichtlinien

Netzwerkrichtlinien werden von NPS verwendet, um festzustellen, ob verbindungsanforderungen von RADIUS-Clients empfangen autorisiert sind. NPS verwendet auch die DFÜ-Eigenschaften des Benutzerkontos ein, um eine Genehmigung zu bestimmen.

Da Richtlinien in der Reihenfolge verarbeitet werden, in denen sie die NPS-Snap-in angezeigt werden, die restriktivsten Richtlinien zunächst in der Liste der Richtlinien platzieren möchten. NPS versucht, für jede verbindungsanforderung die Bedingungen für die Richtlinie mit den Verbindungseigenschaften Anforderung entsprechen. NPS untersucht jede Netzwerkrichtlinie in der Reihenfolge, bis eine Übereinstimmung gefunden wird. Wenn sie keine Übereinstimmung gefunden wird, wird die verbindungsanforderung abgelehnt.

### <a name="key-steps"></a>Wichtige Schritte

Bei der Planung für Netzwerkrichtlinien, können Sie die folgenden Schritte aus.

- Bestimmen Sie die bevorzugte NPS Verarbeitungsreihenfolge von Richtlinien für ein Netzwerk aus, die am wenigsten restriktive restriktivsten.

- Bestimmen Sie den Richtlinienstatus. Der Richtlinienstatus können den Wert der aktiviert oder deaktiviert. Wenn die Richtlinie aktiviert ist, wertet NPS die Richtlinie beim Ausführen der Autorisierung. Wenn die Richtlinie nicht aktiviert ist, wird es nicht ausgewertet.

- Bestimmen Sie die Richtlinie. Sie müssen bestimmen, ob die Richtlinie entwickelt wurde, um Zugriff zu gewähren, wenn die Bedingungen für die Richtlinie zugeordnet werden, durch die verbindungsanforderung oder gibt an, ob die Richtlinie entwickelt wurde, um den Zugriff zu verweigern, wenn die Bedingungen der Richtlinie durch die verbindungsanforderung übereinstimmen. Wenn Sie die Mitglieder einer Windows-Gruppe explizit drahtlosen Zugriff verweigern möchten, können Sie z. B. eine Netzwerkrichtlinie erstellen, die angibt, der Gruppe, die drahtlose Verbindung, und, verfügt über eine Richtlinie aus, geben Sie die Einstellung der Zugriff verweigern.

- Bestimmen Sie, ob der NPS die DFÜ-Eigenschaften von Benutzerkonten, die Mitglieder der Gruppe sind, auf denen die Richtlinie basiert, ignoriert werden sollen. Wenn diese Einstellung nicht aktiviert ist, überschreiben die DFÜ-Eigenschaften von Benutzerkonten, Einstellungen, die in den Netzwerkrichtlinien konfiguriert sind. Beispielsweise ist, wenn eine Netzwerkrichtlinie, die einem Benutzer Zugriff erteilt konfiguriert ist, aber die DFÜ-Eigenschaften des Benutzerkontos für den Benutzer festgelegt werden, um Zugriff zu verweigern, der Zugriff verweigert. Aber wenn Sie die Richtlinie Einstellung ignorieren Benutzer Konto einwählen Typeigenschaften aktivieren, wird derselbe Benutzer Zugriff auf das Netzwerk gewährt.

- Bestimmen Sie, ob die Richtlinie die richtlinieneinstellung für die Quelle verwendet. Mit dieser Einstellung können Sie eine Quelle für alle zugriffsanforderungen auf einfache Weise angeben. Mögliche Quellen sind ein Terminaldienste-Gatewayserver (TS-Gateway), RAS-Server (VPN- oder DFÜ-Verbindung), einem DHCP-Server, einen drahtlosen Zugriffspunkt und einem Server der Integritätsregistrierungsstelle. Alternativ können Sie eine herstellerspezifische Quelle angeben.

- Bestimmen Sie die Bedingungen, die erfüllt sein müssen, Reihenfolge für die Netzwerkrichtlinie angewendet werden.

- Bestimmen Sie die Einstellungen, die angewendet werden, wenn die Bedingungen für die Netzwerkrichtlinie die verbindungsanforderung zugeordnet sind.

- Bestimmen Sie, ob Sie verwenden, ändern oder löschen die Standard-Netzwerkrichtlinien möchten.

## <a name="plan-nps-accounting"></a>Planen der NPS-Kontoführung

NPS ermöglicht den Zugriff auf RADIUS-Kontoführungsdaten wie der Benutzerauthentifizierung und kontoführungsanforderungen, protokolliert werden drei Formate: IAS-Format, das Format und Microsoft SQL Server-Protokollierung. 

IAS-Format und datenbankkompatiblen Format erstellen Protokolldateien auf dem lokalen NPS-Server im Textdateiformat. 

SQL Server-Protokollierung bietet die Möglichkeit, eine SQL Server 2000 oder SQL Server 2005-XML-kompatible Datenbank, erweitern die RADIUS-Kontoführung zur Nutzung der Vorteile der Protokollierung in einer relationalen Datenbank anmelden.

### <a name="key-steps"></a>Wichtige Schritte

Bei der Planung für die NPS-Kontoführung, können Sie die folgenden Schritte aus.

- Bestimmen Sie, ob der NPS-Kontoführungsdaten in Protokolldateien oder in einer SQL Server-Datenbank gespeichert werden sollen.

### <a name="nps-accounting-using-local-log-files"></a>NPS-Kontoführung unter Verwendung von lokalen Protokolldateien

Aufzeichnung Benutzer-Authentifizierung und-Kontoführung Anforderungen in Protokolldateien wird in erster Linie für Verbindung Analyse und Abrechnung Zwecke verwendet und eignet sich auch als Untersuchung Security-Tool, mit dem Sie eine Methode zum Nachverfolgen der Aktivität ein böswilliger Benutzer nach einem Angriff.

### <a name="key-steps"></a>Wichtige Schritte

Bei der Planung für die NPS-Kontoführung lokalen Protokolldateien verwenden, können Sie die folgenden Schritte aus.

- Bestimmen Sie die Datei im Textformat, das Sie für Ihre NPS-Protokolldateien verwenden möchten.

- Wählen Sie den Typ der Informationen, die Sie sich anmelden möchten. Sie können kontoführungsanforderungen, authentifizierungsanforderungen und der periodische Status protokollieren.

- Bestimmen Sie die Festplatte Speicherort, in dem Protokolldateien gespeichert werden sollen.

- Entwerfen Sie Ihre backup Log-Datei-Lösung. Die Festplatte Speicherort, in denen Sie Ihre Protokolldateien speichern, sollte einen Speicherort, der Sie einfach Ihre Daten sichern können. Darüber hinaus sollte der Speicherort der Festplatte geschützt werden, durch die Konfiguration der Zugriffssteuerungsliste (ACL) für den Ordner, in dem die Protokolldateien gespeichert werden.

- Bestimmen Sie die Häufigkeit, mit der Sie neue Protokolldateien erstellt werden soll. Wenn Sie Protokolldateien entsprechend der Dateigröße erstellt werden sollen, bestimmen Sie die maximale Dateigröße zulässig sind, bevor eine neue Protokolldatei von NPS erstellt wird.

- Feststellen Sie, ob Sie NPS alte Protokolldateien löschen, wenn die Festplatte Speicherplatz ausgeführt wird.

- Bestimmen Sie die Anwendung oder Anwendungen, die Sie zum Anzeigen von Ressourcenerfassungsdaten und Berichte erstellen möchten.

### <a name="nps-sql-server-logging"></a>NPS SQL Server-Protokollierung

NPS SQL Server-Protokollierung wird verwendet, wenn Sie Statusinformationen, Bericht erstellen und Daten zu Analysezwecken, und zu zentralisieren und Vereinfachung der Verwaltung Ihrer Buchhaltung Daten benötigen.

NPS ermöglicht das SQL Server-Protokollierung zum Erfassen der Benutzerauthentifizierung und accounting Anfragen von einem oder mehreren Netzwerkzugriffsserver, die an eine Datenquelle auf einem Computer mit dem Microsoft SQL Server-Desktop-Engine \(MSDE 2000\) oder einer beliebigen Version von SQL Server später als SQL Server 2000 verwenden.

Buchhaltungsdaten werden vom Netzwerkrichtlinienserver im XML-Format an einer gespeicherten Prozedur in der Datenbank, die beiden structured Query Language unterstützt übergeben, \(SQL\) und XML-\(SQLXML\) werden. Aufzeichnung der Benutzerauthentifizierung und accounting Anforderungen in einer XML-kompatiblen SQL Server-Datenbank können mehrere NPS-Server auf eine Datenquelle verfügen.

### <a name="key-steps"></a>Wichtige Schritte

Bei der Planung für die NPS-Kontoführung mithilfe von NPS SQL Server-Protokollierung, können Sie die folgenden Schritte aus.

- Ermitteln Sie, ob Sie oder ein anderes Mitglied Ihrer Organisation SQL Server 2000 oder SQL Server 2005 relationalen Datenbankentwicklung auftreten und Sie wissen, wie diese Produkte zu erstellen, ändern, verwalten und Verwalten von SQL Server-Datenbanken verwenden.

- Bestimmen Sie, ob SQL Server auf dem NPS-Server oder auf einem Remotecomputer installiert ist.

- Entwerfen Sie die gespeicherte Prozedur, mit denen Sie in der SQL Server-Datenbank werden eingehende XML-Dateien verarbeitet, die NPS-Kontoführungsdaten enthalten.

- Entwerfen Sie die SQL Server-Datenbank Replikationsstruktur und der Fluss.

- Bestimmen Sie die Anwendung oder Anwendungen, die Sie zum Anzeigen von Ressourcenerfassungsdaten und Berichte erstellen möchten.

- Netzwerkzugriffsserver verwenden, die das Class-Attribut in allen kontoführungsanforderungen senden möchten. Class-Attribut wird an den RADIUS-Client in einer Access-Accept-Nachricht gesendet, und eignet sich zum Korrelieren von Kontoführungsanforderung Nachrichten mit Authentifizierung Sitzungen. Wenn die Class-Attribut von Network Access Server in der Buchhaltung Anforderungsnachrichten gesendet wird, kann es zu Kontoführung und Authentifizierung keine Entsprechung verwendet werden. Die Kombination aus den Attributen Unique-Seriennummer, Service-Neustart-Time und Server-Adresse muss eine eindeutige Kennung für jede Authentifizierung, die der Server akzeptiert.

- Planen von Netzwerkzugriffsserver, zwischenzeitliche Kontoführung unterstützen.

- Netzwerkzugriffsserver verwenden, die Kontoführung auf und Accounting-off-Nachrichten senden möchten.

- Planen Sie Netzwerkzugriffsserver, die das Speichern zu unterstützen und Weiterleitung von Ressourcenerfassungsdaten. Netzwerkzugriffsserver, die dieses Feature unterstützen können Accounting-Daten speichern, wenn der Netzwerkzugriffsserver mit dem NPS-Server kommunizieren kann. Wenn der NPS-Server verfügbar ist, leitet der Netzwerkzugriffsserver gespeicherten Datensätze mit dem NPS-Server bietet mehr Zuverlässigkeit in der Buchhaltung über Netzwerkzugriffsserver, die dieses Feature nicht bereitstellen.

- Immer das Attribut Acct-Interim-Interval in Netzwerkrichtlinien konfigurieren möchten. Das Attribut Acct-Interim-Interval setzt das Intervall (in Sekunden) zwischen jeder zwischenzeitlichen Aktualisierung, die Network Access Server sendet. Gemäß RFC 2869 der Wert des Attributs Acct-Interim-Interval darf nicht kleiner als 60 Sekunden oder eine Minute lang sein und darf nicht kleiner als 600 Sekunden bzw. 10 Minuten sein. Weitere Informationen finden Sie unter RFC 2869, "RADIUS-Erweiterungen."

- Stellen Sie sicher, dass die Protokollierung von periodische Status auf den NPS-Servern aktiviert ist.

