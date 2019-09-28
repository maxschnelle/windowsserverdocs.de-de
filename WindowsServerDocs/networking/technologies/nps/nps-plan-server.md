---
title: Planen eines NPS als RADIUS-Server
description: Dieses Thema enthält Informationen zur Planung der RADIUS-Server Bereitstellung für den Netzwerk Richtlinien Server in Windows Server 2016.
manager: brianlic
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 2900dd2c-0f70-4f8d-9650-ed83d51d509a
ms.author: pashort
author: shortpatti
ms.openlocfilehash: bbcf3338f2cd6d8662a84faf263b486e31b140e5
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405338"
---
# <a name="plan-nps-as-a-radius-server"></a>Planen eines NPS als RADIUS-Server

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Wenn Sie den Netzwerk Richtlinien Server \(nps @ no__t-1 als RADIUS-Server (Remote Authentication Dial-in User Service) bereitstellen, führt NPS Authentifizierung, Autorisierung und Kontoführung für Verbindungsanforderungen für die lokale Domäne und Domänen aus, die dem lokale Domäne. Sie können diese Planungsrichtlinien verwenden, um die RADIUS-Bereitstellung zu vereinfachen.

Diese Planungsrichtlinien enthalten keine Umstände, in denen Sie NPS als RADIUS-Proxy bereitstellen möchten. Wenn Sie NPS als RADIUS-Proxy bereitstellen, leitet NPS Verbindungsanforderungen an einen Server weiter, auf dem NPS oder andere RADIUS-Server in Remote Domänen, nicht vertrauenswürdigen Domänen oder beides ausgeführt werden. 

Bevor Sie NPS als RADIUS-Server in Ihrem Netzwerk bereitstellen, verwenden Sie die folgenden Richtlinien, um die Bereitstellung zu planen.

- Planen Sie die NPS-Konfiguration.

- Planen von RADIUS-Clients.

- Planen Sie die Verwendung von Authentifizierungsmethoden.

- Planen von Netzwerk Richtlinien.

- Planen der NPS-Kontoführung.

## <a name="plan-nps-configuration"></a>Planen der NPS-Konfiguration

Sie müssen entscheiden, in welcher Domäne der NPS Mitglied ist. In Umgebungen mit mehreren Domänen kann ein NPS Anmelde Informationen für Benutzerkonten in der Domäne, deren Mitglied er ist, und für alle Domänen authentifizieren, die der lokalen Domäne des NPS Vertrauen. Damit das NPS die DFÜ-Eigenschaften von Benutzerkonten während des Autorisierungs Vorgangs lesen kann, müssen Sie das Computer Konto des NPS der Gruppe "RAS" und "NPSS" für jede Domäne hinzufügen.

Nachdem Sie die Domänen Mitgliedschaft des NPS ermittelt haben, muss der Server für die Kommunikation mit RADIUS-Clients, auch Netzwerk Zugriffs Server genannt, mithilfe des RADIUS-Protokolls konfiguriert werden. Außerdem können Sie die Typen von Ereignissen konfigurieren, die von NPS im Ereignisprotokoll aufgezeichnet werden, und Sie können eine Beschreibung für den Server eingeben.

### <a name="key-steps"></a>Wichtige Schritte

Bei der Planung der NPS-Konfiguration können Sie die folgenden Schritte ausführen.

- Bestimmen Sie die RADIUS-Ports, die der NPS zum Empfangen von RADIUS-Nachrichten von RADIUS-Clients verwendet. Die Standardports sind UDP-Ports 1812 und 1645 für RADIUS-Authentifizierungs Nachrichten und die Ports 1813 und 1646 für RADIUS-Buchhaltungs Nachrichten.

- Wenn der NPS mit mehreren Netzwerkadaptern konfiguriert ist, bestimmen Sie die Adapter, über die der RADIUS-Datenverkehr zugelassen werden soll.

- Bestimmen Sie die Typen von Ereignissen, die von NPS im Ereignisprotokoll aufgezeichnet werden sollen. Sie können abgelehnte Authentifizierungsanforderungen, erfolgreiche Authentifizierungsanforderungen oder beide Anforderungs Typen protokollieren.

- Stellen Sie fest, ob Sie mehr als ein NPS bereitstellen. Verwenden Sie mindestens zwei NPSS, um Fehlertoleranz für die RADIUS-basierte Authentifizierung und die Kontoführung bereitzustellen. Ein NPS wird als primärer RADIUS-Server und der andere als eine Sicherung verwendet. Jeder RADIUS-Client wird dann für beide NPSS konfiguriert. Wenn das primäre NPS nicht mehr verfügbar ist, senden RADIUS-Clients dann Zugriffs Anforderungs Nachrichten an die alternativen NPS.

- Planen Sie das Skript, mit dem eine NPS-Konfiguration in andere NPSS kopiert wird, um den Verwaltungsaufwand zu sparen und die falsche Konfiguration eines Servers zu verhindern. NPS stellt die Netsh-Befehle bereit, mit denen Sie die gesamte NPS-Konfiguration für den Import auf einen anderen NPS kopieren können. Sie können die Befehle manuell an der netsh-Eingabeaufforderung ausführen. Wenn Sie jedoch die Befehlssequenz als Skript speichern, können Sie das Skript zu einem späteren Zeitpunkt ausführen, wenn Sie sich entscheiden, die Serverkonfigurationen zu ändern.

## <a name="plan-radius-clients"></a>Planen von RADIUS-Clients

RADIUS-Clients sind Netzwerk Zugriffs Server, z. b. drahtlos Zugriffspunkte, VPN-Server (Virtual Private Network), 802.1 x-fähige Switches und DFÜ-Server. RADIUS-Proxys, die Verbindungs Anforderungs Nachrichten an RADIUS-Server weiterleiten, sind ebenfalls RADIUS-Clients. NPS unterstützt alle Netzwerk Zugriffs Server und RADIUS-Proxys, die dem RADIUS-Protokoll entsprechen, wie in RFC 2865, "Remote Authentication Dial-in User Service (RADIUS)" und RFC 2866, "RADIUS Accounting" beschrieben.

>[!IMPORTANT]
>Zugriffs Clients, z. b. Client Computer, sind keine RADIUS-Clients. Nur Netzwerk Zugriffs Server und Proxy Server, die das RADIUS-Protokoll unterstützen, sind RADIUS-Clients.

Außerdem müssen sowohl drahtlos Zugriffspunkte als auch Switches in der 802.1 x-Authentifizierung aktiviert sein. Wenn Sie das Extensible Authentication-Protokoll \(eap @ no__t-1 oder Protected Extensible Authentication Protocol \(peap @ no__t-3 bereitstellen möchten, müssen Zugriffspunkte und Switches die Verwendung von EAP unterstützen.

Zum Testen der grundlegenden Interoperabilität für PPP-Verbindungen für drahtlos Zugriffspunkte konfigurieren Sie den Zugriffspunkt und den Zugriffs Client für die Verwendung des Kennwort-Authentifizierungs Protokolls (PAP). Verwenden Sie zusätzliche PPP-basierte Authentifizierungsprotokolle, wie z. b. "Peer-AP", bis Sie die Tests getestet haben, die Sie für den Netzwerk Zugriff verwenden möchten.

### <a name="key-steps"></a>Wichtige Schritte

Bei der Planung für RADIUS-Clients können Sie die folgenden Schritte ausführen.

- Dokumentieren Sie die herstellerspezifischen Attribute (VSAs), die Sie in NPS konfigurieren müssen. Wenn Ihre Netzwerk Zugriffs Server VSAs erfordern, protokollieren Sie die VSA-Informationen zur späteren Verwendung, wenn Sie Ihre Netzwerk Richtlinien in NPS konfigurieren. 

- Dokumentieren Sie die IP-Adressen von RADIUS-Clients und ihrer NPS, um die Konfiguration aller Geräte zu vereinfachen. Beim Bereitstellen der RADIUS-Clients müssen Sie diese so konfigurieren, dass Sie das RADIUS-Protokoll verwenden. dabei wird die NPS-IP-Adresse als authentifizierende Server eingegeben. Wenn Sie NPS für die Kommunikation mit ihren RADIUS-Clients konfigurieren, müssen Sie die RADIUS-Client-IP-Adressen in das NPS-Snap-in eingeben.

- Erstellen Sie freigegebene geheime Schlüssel für die Konfiguration auf den RADIUS-Clients und im NPS-Snap-in. Sie müssen RADIUS-Clients mit einem gemeinsamen geheimen Schlüssel oder Kennwort konfigurieren, das Sie auch beim Konfigurieren von RADIUS-Clients in NPS in das NPS-Snap-in eingeben.

## <a name="plan-the-use-of-authentication-methods"></a>Planen der Verwendung von Authentifizierungsmethoden

NPS unterstützt sowohl Kenn Wort basierte als auch Zertifikat basierte Authentifizierungsmethoden. Allerdings unterstützen nicht alle Netzwerk Zugriffs Server die gleichen Authentifizierungsmethoden. In einigen Fällen möchten Sie möglicherweise eine andere Authentifizierungsmethode basierend auf dem Netzwerk Zugriffstyp bereitstellen.

Beispielsweise möchten Sie möglicherweise sowohl drahtlosen als auch VPN-Zugriff für Ihre Organisation bereitstellen, verwenden jedoch für jeden Zugriffstyp eine andere Authentifizierungsmethode: EAP-TLS für VPN-Verbindungen, aufgrund der starken Sicherheit, die von EAP mit Transport Layer Security (EAP-TLS) bereitstellt wird, und PEAP-MS-CHAP v2 für drahtlose 802.1 x-Verbindungen.

Mit dem Microsoft Challenge Handshake Authentication-Protokollversion 2 (Peer Version 2, PAP-MS-CHAP v2) ist eine Funktion mit dem Namen fast Connect Connect verfügbar, die speziell für die Verwendung mit tragbaren Computern und anderen drahtlos Geräten konzipiert ist. Die schnelle Wiederherstellung der Verbindung ermöglicht drahtlosen Clients das Wechseln zwischen drahtlosen Zugriffs Punkten im gleichen Netzwerk, ohne dass Sie jedes Mal erneut authentifiziert werden, wenn Sie mit einem neuen Zugriffspunkt verknüpft werden. Dies bietet eine bessere Benutzerfunktion für drahtlose Benutzer und ermöglicht das Wechseln zwischen Zugriffs Punkten, ohne Ihre Anmelde Informationen erneut eingeben zu müssen.
Aufgrund der schnellen Wiederherstellung der Verbindung und der von PEAP-MS-CHAP v2 bereitgestellten Sicherheit ist PEAP-MS-CHAP v2 eine logische Wahl als Authentifizierungsmethode für drahtlose Verbindungen.

Bei VPN-Verbindungen ist EAP-TLS eine Zertifikat basierte Authentifizierungsmethode, die eine hohe Sicherheit bietet, die den Netzwerk Datenverkehr schützt, auch wenn Sie über das Internet von Heim-oder Mobil Computern an die VPN-Server Ihrer Organisation übertragen wird.

### <a name="certificate-based-authentication-methods"></a>Zertifikat basierte Authentifizierungsmethoden

Zertifikat basierte Authentifizierungsmethoden haben den Vorteil, dass Sie eine hohe Sicherheit bieten. und Sie haben den Nachteil, dass die Bereitstellung schwieriger ist als die Kenn Wort basierte Authentifizierungsmethode.

PEAP-MS-CHAP v2 und EAP-TLS sind Zertifikat basierte Authentifizierungsmethoden, aber es gibt viele Unterschiede zwischen Ihnen und der Art und Weise, in der Sie bereitgestellt werden.

### <a name="eap-tls"></a>EAP-TLS

EAP-TLS verwendet Zertifikate für die Client-und Server Authentifizierung und erfordert, dass Sie eine Public Key-Infrastruktur (PKI) in Ihrer Organisation bereitstellen. Das Bereitstellen einer PKI kann komplex sein und erfordert eine Planungsphase, die unabhängig von der Planung der Verwendung von NPS als RADIUS-Server ist.

Mit EAP-TLS registriert NPS ein Serverzertifikat von einer Zertifizierungsstelle \(ca @ no__t-1, und das Zertifikat wird auf dem lokalen Computer im Zertifikat Speicher gespeichert. Während des Authentifizierungs Vorgangs erfolgt die Server Authentifizierung, wenn das NPS sein Serverzertifikat an den Zugriffs Client sendet, um dessen Identität für den Zugriffs Client zu beweisen. Der Zugriffs Client prüft verschiedene Zertifikat Eigenschaften, um zu bestimmen, ob das Zertifikat gültig ist und für die Verwendung bei der Server Authentifizierung geeignet ist. Wenn das Serverzertifikat die Mindestanforderungen an das Serverzertifikat erfüllt und von einer Zertifizierungsstelle ausgestellt wird, der der Zugriffs Client vertraut, wird der NPS vom Client erfolgreich authentifiziert.

Auf ähnliche Weise erfolgt die Client Authentifizierung während des Authentifizierungsprozesses, wenn der Client das Client Zertifikat an den NPS sendet, um seine Identität für den NPS zu belegen. Das Zertifikat wird von NPS überprüft, und wenn das Client Zertifikat die Mindestanforderungen für das Client Zertifikat erfüllt und von einer Zertifizierungsstelle ausgestellt wird, der das NPS vertraut, wird der Zugriffs Client vom NPS erfolgreich authentifiziert.

Obwohl es erforderlich ist, dass das Serverzertifikat im Zertifikat Speicher auf dem NPS gespeichert ist, kann das Client-oder Benutzerzertifikat entweder im Zertifikat Speicher auf dem Client oder auf einer Smartcard gespeichert werden.

Damit dieser Authentifizierungs Vorgang erfolgreich ist, ist es erforderlich, dass alle Computer das Zertifizierungsstellen Zertifikat Ihres Unternehmens im Zertifikat Speicher der vertrauenswürdigen Stamm Zertifizierungsstellen für den lokalen Computer und den aktuellen Benutzer haben.

### <a name="peap-ms-chap-v2"></a>PEAP-MS-CHAP v2

"Peer-MS-CHAP v2" verwendet ein Zertifikat für die Server Authentifizierung und Kenn Wort basierte Anmelde Informationen für die Benutzerauthentifizierung. Da Zertifikate nur für die Server Authentifizierung verwendet werden, ist es nicht erforderlich, eine PKI bereitzustellen, um "Peer-MS-CHAP v2" verwenden zu können. Wenn Sie "Peer-MS-CHAP v2" bereitstellen, können Sie ein Serverzertifikat für den NPS auf eine der beiden folgenden Arten abrufen:

- Sie können Active Directory Zertifikat Dienste (AD CS) installieren und dann Zertifikate automatisch für NPSS registrieren. Wenn Sie diese Methode verwenden, müssen Sie auch das Zertifizierungsstellen Zertifikat für Client Computer registrieren, die eine Verbindung mit Ihrem Netzwerk herstellen, damit Sie dem Zertifikat vertrauen, das für den NPS ausgestellt wurde.

- Sie können ein Serverzertifikat von einer öffentlichen Zertifizierungsstelle, z. b. VeriSign, erwerben. Wenn Sie diese Methode verwenden, stellen Sie sicher, dass Sie eine Zertifizierungsstelle auswählen, die bereits von den Client Computern als vertrauenswürdig eingestuft wird. Um zu ermitteln, ob Client Computer einer Zertifizierungsstelle vertrauen, öffnen Sie das Microsoft Management Console (MMC)-Snap-in "Zertifikate" auf einem Client Computer, und zeigen Sie dann den Speicher vertrauenswürdiger Stamm Zertifizierungsstellen für den lokalen Computer und für den aktuellen Benutzer an. Wenn ein Zertifikat von der Zertifizierungsstelle in diesen Zertifikat speichern vorhanden ist, vertraut der Client Computer der Zertifizierungsstelle und vertraut somit allen von der Zertifizierungsstelle ausgestellten Zertifikaten.

Während des Authentifizierungsprozesses mit "Peer-MS-CHAP v2" erfolgt die Server Authentifizierung, wenn das NPS sein Serverzertifikat an den Client Computer sendet. Der Zugriffs Client prüft verschiedene Zertifikat Eigenschaften, um zu bestimmen, ob das Zertifikat gültig ist und für die Verwendung bei der Server Authentifizierung geeignet ist. Wenn das Serverzertifikat die Mindestanforderungen an das Serverzertifikat erfüllt und von einer Zertifizierungsstelle ausgestellt wird, der der Zugriffs Client vertraut, wird der NPS vom Client erfolgreich authentifiziert.

Die Benutzerauthentifizierung tritt auf, wenn ein Benutzer versucht, eine Verbindung mit dem Netzwerk mit Kenn Wort basierten Anmelde Informationen herzustellen, und versucht, sich anzumelden. NPS empfängt die Anmelde Informationen und führt die Authentifizierung und Autorisierung durch. Wenn der Benutzer erfolgreich authentifiziert und autorisiert wurde und der Client Computer den NPS erfolgreich authentifiziert hat, wird die Verbindungsanforderung erteilt.

### <a name="key-steps"></a>Wichtige Schritte

Bei der Planung der Verwendung von Authentifizierungsmethoden können Sie die folgenden Schritte ausführen.

- Identifizieren Sie die Typen des Netzwerk Zugriffs, den Sie anbieten möchten, z. b. drahtlos, VPN, 802.1 x-fähiger Switch und Einwählzugriff.

- Bestimmen Sie die Authentifizierungsmethoden, die Sie für jeden Zugriffstyp verwenden möchten. Es wird empfohlen, die Zertifikat basierten Authentifizierungsmethoden zu verwenden, die eine hohe Sicherheit bieten. Es ist jedoch möglicherweise nicht praktikabel, eine PKI bereitzustellen, sodass andere Authentifizierungsmethoden einen besseren Ausgleich der für Ihr Netzwerk benötigten Ressourcen bereitstellen können.

- Wenn Sie EAP-TLS bereitstellen, planen Sie Ihre PKI-Bereitstellung. Dies umfasst die Planung der Zertifikat Vorlagen, die Sie für Server Zertifikate und Client Computer Zertifikate verwenden werden. Außerdem wird festgelegt, wie Zertifikate für Domänen Mitglieds-und nicht-Domänen Mitglieds Computer registriert werden, und es wird festgelegt, ob Smartcards verwendet werden sollen.

- Wenn Sie "Peer-MS-CHAP v2" bereitstellen, legen Sie fest, ob Sie AD CS zum Ausstellen von Server Zertifikaten für Ihre NPSS installieren möchten oder ob Sie Server Zertifikate von einer öffentlichen Zertifizierungsstelle, z. b. VeriSign, erwerben möchten.

### <a name="plan-network-policies"></a>Planen von Netzwerk Richtlinien

Netzwerk Richtlinien werden von NPS verwendet, um zu bestimmen, ob Verbindungsanforderungen, die von RADIUS-Clients empfangen werden, autorisiert sind. NPS verwendet auch die DFÜ-Eigenschaften des Benutzerkontos, um eine Autorisierungs Entscheidung zu treffen.

Da Netzwerk Richtlinien in der Reihenfolge verarbeitet werden, in der Sie im NPS-Snap-in angezeigt werden, sollten Sie die restriktivsten Richtlinien zuerst in der Liste der Richtlinien platzieren. Für jede Verbindungsanforderung versucht NPS, die Bedingungen der Richtlinie mit den Verbindungs Anforderungs Eigenschaften abzugleichen. NPS überprüft jede Netzwerk Richtlinie in der angegebenen Reihenfolge, bis eine Entsprechung gefunden wird. Wenn keine Entsprechung gefunden wird, wird die Verbindungsanforderung zurückgewiesen.

### <a name="key-steps"></a>Wichtige Schritte

Bei der Planung von Netzwerk Richtlinien können Sie die folgenden Schritte ausführen.

- Bestimmen Sie die bevorzugte NPS-Verarbeitungsreihenfolge von Netzwerk Richtlinien, von der restriktivsten bis zum geringsten einschränkenden

- Bestimmen Sie den Richtlinien Status. Der Richtlinien Status kann den Wert "aktiviert" oder "deaktiviert" aufweisen. Wenn die Richtlinie aktiviert ist, wertet NPS die Richtlinie beim Ausführen der Autorisierung aus. Wenn die Richtlinie nicht aktiviert ist, wird Sie nicht ausgewertet.

- Bestimmen Sie den Richtlinientyp. Sie müssen bestimmen, ob die Richtlinie den Zugriff gewährt, wenn die Bedingungen der Richtlinie mit der Verbindungsanforderung abgeglichen werden, oder ob die Richtlinie darauf ausgelegt ist, den Zugriff zu verweigern, wenn die Bedingungen der Richtlinie mit der Verbindungsanforderung abgeglichen werden. Wenn Sie z. b. den drahtlosen Zugriff auf die Mitglieder einer Windows-Gruppe explizit verweigern möchten, können Sie eine Netzwerk Richtlinie erstellen, die die Gruppe, die drahtlose Verbindungsmethode und den Richtlinientyp "Zugriff verweigern" angibt.

- Bestimmen Sie, ob NPS die DFÜ-Eigenschaften von Benutzerkonten ignorieren soll, die Mitglieder der Gruppe sind, auf der die Richtlinie basiert. Wenn diese Einstellung nicht aktiviert ist, überschreiben die Einwähleigenschaften von Benutzerkonten Einstellungen, die in den Netzwerk Richtlinien konfiguriert sind. Wenn z. b. eine Netzwerk Richtlinie konfiguriert ist, die den Zugriff auf einen Benutzer gewährt, aber die DFÜ-Eigenschaften des Benutzerkontos für diesen Benutzer so festgelegt sind, dass der Zugriff verweigert wird, wird dem Benutzer der Zugriff verweigert. Wenn Sie jedoch die Einstellung Richtlinientyp Benutzerkonto Einwähleigenschaften ignorieren aktivieren, wird dem gleichen Benutzer der Zugriff auf das Netzwerk gewährt.

- Bestimmen Sie, ob die Richtlinie die Einstellung der Richtlinien Quelle verwendet. Mit dieser Einstellung können Sie problemlos eine Quelle für alle Zugriffs Anforderungen angeben. Mögliche Quellen sind ein Terminaldienstegateway (TS-Gateway), ein Remote Zugriffs Server (VPN oder DFÜ), ein DHCP-Server, ein drahtloser Zugriffspunkt und ein Integritäts Registrierungsstellen-Server. Alternativ können Sie eine anbieterspezifische Quelle angeben.

- Bestimmen Sie die Bedingungen, die abgeglichen werden müssen, damit die Netzwerk Richtlinie angewendet wird.

- Bestimmen Sie die Einstellungen, die angewendet werden, wenn die Bedingungen der Netzwerk Richtlinie mit der Verbindungsanforderung abgeglichen werden.

- Bestimmen Sie, ob Sie die standardmäßigen Netzwerk Richtlinien verwenden, ändern oder löschen möchten.

## <a name="plan-nps-accounting"></a>Planen der NPS-Kontoführung

NPS bietet die Möglichkeit, RADIUS-Buchhaltungsdaten, wie z. b. Benutzerauthentifizierung und Buchhaltungs Anforderungen, in drei Formaten zu protokollieren: IAS-Format, Daten Bank kompatibles Format und Microsoft SQL Server Protokollierung. 

IAS-Format und Daten Bank kompatibles Format erstellen Sie Protokolldateien auf dem lokalen NPS im Text Dateiformat. 

SQL Server Protokollierung bietet die Möglichkeit, sich in einer SQL Server 2000-oder SQL Server 2005-XML-kompatiblen Datenbank zu protokollieren. Dies erweitert die RADIUS-Kontoführung, um die Vorteile der Protokollierung in einer relationalen Datenbank

### <a name="key-steps"></a>Wichtige Schritte

Bei der Planung der NPS-Buchhaltung können Sie die folgenden Schritte ausführen.

- Bestimmen Sie, ob Sie NPS-Buchhaltungsdaten in Protokolldateien oder in einer SQL Server-Datenbank speichern möchten.

### <a name="nps-accounting-using-local-log-files"></a>NPS-Kontoführung mit lokalen Protokolldateien

Das Aufzeichnen von Benutzerauthentifizierungs-und Buchhaltungs Anforderungen in Protokolldateien wird hauptsächlich für Verbindungs Analyse und Abrechnungszwecke verwendet und ist auch als Sicherheitsuntersuchung nützlich und bietet eine Methode zum Nachverfolgen der Aktivität eines böswilligen Benutzers nach einem infar.

### <a name="key-steps"></a>Wichtige Schritte

Bei der Planung der NPS-Kontoführung mithilfe lokaler Protokolldateien können Sie die folgenden Schritte ausführen.

- Legen Sie das Text Dateiformat fest, das Sie für Ihre NPS-Protokolldateien verwenden möchten.

- Wählen Sie den Typ der Informationen aus, die Sie protokollieren möchten. Sie können Buchhaltungs Anforderungen, Authentifizierungsanforderungen und den regelmäßigen Status protokollieren.

- Bestimmen Sie den Speicherort der Festplatte, in dem Sie die Protokolldateien speichern möchten.

- Entwerfen Sie die Sicherungs Lösung für die Protokolldatei. Der Speicherort der Festplatte, in dem Sie die Protokolldateien speichern, sollte ein Speicherort sein, an dem Sie Ihre Daten problemlos sichern können. Außerdem sollte der Speicherort der Festplatte geschützt werden, indem die Zugriffs Steuerungs Liste (ACL) für den Ordner konfiguriert wird, in dem die Protokolldateien gespeichert werden.

- Legen Sie die Häufigkeit fest, mit der neue Protokolldateien erstellt werden sollen. Wenn Protokolldateien basierend auf der Dateigröße erstellt werden sollen, bestimmen Sie die maximal zulässige Dateigröße, bevor eine neue Protokolldatei von NPS erstellt wird.

- Legen Sie fest, ob NPS ältere Protokolldateien löschen soll, wenn die Festplatte nicht mehr über genügend Speicherplatz verfügt.

- Bestimmen Sie die Anwendung oder Anwendungen, die Sie verwenden möchten, um Buchhaltungsdaten anzuzeigen und Berichte zu liefern.

### <a name="nps-sql-server-logging"></a>NPS-SQL Server Protokollierung

Die NPS-SQL Server Protokollierung wird verwendet, wenn Sie Sitzungs Zustandsinformationen, für die Erstellung von Berichten und zur Datenanalyse benötigen, und um die Verwaltung Ihrer Buchhaltungsdaten zu zentralisieren und zu vereinfachen.

NPS bietet die Möglichkeit, SQL Server Protokollierung zum Aufzeichnen von Authentifizierungs-und Buchhaltungs Anforderungen von einem oder mehreren Netzwerk Zugriffs Servern an eine Datenquelle auf einem Computer mit der Microsoft SQL Server Desktop-Engine \(msde 2000 @ no__t-1 oder einer beliebigen die Version von SQL Server, die höher als SQL Server 2000 ist.

Kontoführungs Daten werden vom NPS im XML-Format an eine gespeicherte Prozedur in der-Datenbank übermittelt, die sowohl die strukturierte Abfragesprache \(sql @ no__t-1 als auch XML \(sqlxml @ no__t-3 unterstützt. Durch das Aufzeichnen von Benutzer Authentifizierungs-und Buchhaltungs Anforderungen in einer XML-kompatiblen SQL Server-Datenbank können mehrere NPSS über eine Datenquelle verfügen.

### <a name="key-steps"></a>Wichtige Schritte

Bei der Planung der NPS-Kontoführung mithilfe der NPS-SQL Server Protokollierung können Sie die folgenden Schritte ausführen.

- Stellen Sie fest, ob Sie oder ein anderes Mitglied Ihrer Organisation über SQL Server die Entwicklung von relationalen Datenbanken 2000 oder SQL Server 2005 verfügen, und Sie verstehen, wie diese Produkte zum Erstellen, ändern, verwalten und Verwalten von SQL Server Datenbanken verwendet werden.

- Bestimmen Sie, ob SQL Server auf dem NPS oder auf einem Remote Computer installiert ist.

- Entwerfen Sie die gespeicherte Prozedur, die Sie in Ihrer SQL Server Datenbank verwenden werden, um eingehende XML-Dateien zu verarbeiten, die NPS-Buchhaltungsdaten enthalten.

- Entwerfen Sie die SQL Server Daten Bank Replikations Struktur und den Datenfluss

- Bestimmen Sie die Anwendung oder Anwendungen, die Sie verwenden möchten, um Buchhaltungsdaten anzuzeigen und Berichte zu liefern.

- Planen Sie die Verwendung von Netzwerk Zugriffs Servern, die das Class-Attribut in allen Buchhaltungs Anforderungen senden. Das Class-Attribut wird in einer Access-Accept-Nachricht an den RADIUS-Client gesendet und ist nützlich, um Buchhaltungs Anforderungs Nachrichten mit Authentifizierungs Sitzungen zu korrelieren. Wenn das Class-Attribut vom Netzwerk Zugriffs Server in den Nachrichten der Buchhaltungs Anforderung gesendet wird, kann es verwendet werden, um die Kontoführungs-und Authentifizierungsdaten Sätze abzugleichen. Die Kombination der Attribute Unique-Serial-Number, Service-Reboot-Time und Server Adresse muss eine eindeutige Identifikation für jede Authentifizierung sein, die der Server akzeptiert.

- Planen Sie die Verwendung von Netzwerk Zugriffs Servern, die die Zwischenabrechnung unterstützen.

- Planen Sie die Verwendung von Netzwerk Zugriffs Servern, die Nachrichten übermitteln und Abrechnungen senden.

- Planen Sie die Verwendung von Netzwerk Zugriffs Servern, die das Speichern und Weiterleiten von Buchhaltungsdaten unterstützen. Netzwerk Zugriffs Server, die dieses Feature unterstützen, können Buchhaltungsdaten speichern, wenn der Netzwerk Zugriffs Server nicht mit dem NPS kommunizieren kann. Wenn der NPS verfügbar ist, leitet der Netzwerk Zugriffs Server die gespeicherten Datensätze an den NPS weiter und bietet eine höhere Zuverlässigkeit bei der Abrechnung über Netzwerk Zugriffs Server, die dieses Feature nicht bereitstellen.

- Planen Sie, das Attribut "Acct-Interim-Interval" immer in den Netzwerk Richtlinien zu konfigurieren. Das Acct-Interim-Interval-Attribut legt das Intervall (in Sekunden) zwischen jedem Zwischenupdate fest, das vom Netzwerk Zugriffs Server gesendet wird. Gemäß RFC 2869 darf der Wert des Acct-Interim-Interval-Attributs nicht kleiner als 60 Sekunden oder eine Minute sein und darf nicht kleiner als 600 Sekunden oder 10 Minuten sein. Weitere Informationen finden Sie unter RFC 2869, "RADIUS-Erweiterungen".

- Stellen Sie sicher, dass die Protokollierung des regelmäßigen Status auf Ihrem NPSS aktiviert ist.

