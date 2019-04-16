---
title: "TLS – SSL (Schannel SSP) (Übersicht)"
description: Windows Server-Sicherheit
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-tls-ssl
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c8836345-16bb-4dcc-8d2b-2b9b687456a3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: b846ed54a1f7c8ef7a85ea9f836ffa75d0036ae6
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="overview-of-tls---ssl-schannel-ssp"></a>Übersicht über TLS – SSL (Schannel SSP)

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

In diesem Thema für IT-Experten beschreibt die Änderungen an der Funktionalität im der Schannel Security Support Provider (SSP), das Transport Layer Security (TLS), Secure Sockets Layer (SSL) und die Authentifizierungsprotokolle Datagram Transport Layer Security (DTLS) für Windows Server2012 R2, Windows Server2012, Windows8.1 und Windows8 enthält.

Schannel ist ein Security Support Provider (SSP), die die standardmäßigen Internetauthentifizierungsprotokolle SSL, TLS und DTLS implementiert. Die Security Support Provider-Schnittstelle (SSPI) ist eine API, die von Windows-Systemen verwendet werden, um sicherheitsbezogene Funktionen wie Authentifizierungen durchzuführen. Die SSPI Dienst als gemeinsame Schnittstelle für mehrere Security Support Provider (SSP), einschließlich Schannel SSP.

Weitere Informationen zur Microsoft Implementierung von TLS und SSL im Schannel-SSP finden Sie unter der [technische Referenz zu TLS/SSL (2003)](https://technet.microsoft.com/library/cc784149(v=ws.10).aspx).


##<a name="tlsssl-schannel-ssp-features"></a>TLS/SSL (Schannel SSP)-Features
Im folgenden werden Features von TLS im Schannel SSP. beschrieben.

### <a name="tls-session-resumption"></a>TLS-sitzungswiederaufnahme
Das Transport Layer Security (TLS)-Protokoll, eine Komponente von Schannel-Security Support Provider, wird verwendet, um Daten zu schützen, die zwischen Programmen in einem nicht vertrauenswürdigen Netzwerk gesendet wird. TLS/SSL können Server und Clientcomputer authentifizieren und auch zum Verschlüsseln von Nachrichten zwischen den authentifizierten Parteien verwendet werden.

Geräte, die häufig TLS mit Servern herstellen müssen aufgrund der Sitzungsablauf wiederherstellen. Windows8.1 und Windows Server2012 R2 unterstützen jetzt RFC 5077 (TLS-Sitzungswiederaufnahme ohne serverseitigen Zustand). Diese Änderung bietet Windows Phone und Windows RT-Geräte mit:

-   Reduzierter Ressourcenbedarf auf dem Server

-   Reduzierte Bandbreite und damit die Effizienz von Clientverbindungen verbessert

-   Geringere Dauer der TLS-Handshakes durch Wiederaufnahme der Verbindung.

> [!NOTE]
> Die Implementierung der clientseitigen RFC 5077 wurde in Windows8 hinzugefügt.

Informationen zur statusfreien TLS-sitzungswiederaufnahme finden Sie im IETF-Dokument [RFC 5077.](http://www.ietf.org/rfc/rfc5077)

### <a name="application-protocol-negotiation"></a>Anwendungsprotokollverhandlung
 Windows Server2012 R2 und Windows8.1 unterstützt clientseitige TLS-Anwendungsprotokolls Anwendungen können Protokolle als Teil der Standard-HTTP-2.0-Entwicklung nutzen und Benutzerzugriff Onlinedienste wie Google und Twitter mithilfe von Apps, die das SPDY-Protokoll ausgeführt.

**So funktioniert es**

Client- und Serveranwendungen aktivieren Anwendung Aushandlung protokollerweiterung Bereitstellen von Listen unterstützter Anwendungsprotokoll-IDs in absteigender Reihenfolge. Der TLS-Client weist darauf hin, dass es Anwendungsprotokolls unterstützt, indem die Anwendung er (Layer Protocol Negotiation die ALPN)-Erweiterung mit einer Liste clientseitig unterstützter Protokolle in der ClientHello-Nachricht.

Wenn der TLS-Client mit dem Server die Anforderung stellt, liest der TLS-Server, dass es sich um Liste unterstützter Protokolle aus, für das bevorzugtes Protokoll handelt, die der Client ebenfalls unterstützt. Wenn ein solches Protokoll gefunden wird, wird der Server antwortet mit der ausgewählten Protokoll-ID und den Handshake wie gewohnt fort. Wenn kein gemeinsames Anwendungsprotokoll vorhanden ist, sendet der Server ein schwerwiegender Handshake-Fehler.

### <a name="BKMK_TrustedIssuers"></a>Verwaltung vertrauenswürdiger Aussteller zur Clientauthentifizierung
Bei der Authentifizierung des Clientcomputers über SSL oder TLS erforderlich ist, kann der Server konfiguriert werden, um eine Liste vertrauenswürdiger Zertifikataussteller sendet. Diese Liste enthält die Gruppe der Zertifikataussteller, denen der Server vertraut, und ist ein Hinweis auf den Clientcomputer Clientzertifikats auswählen Wenn mehrere Zertifikate vorhanden sind. Darüber hinaus muss die Zertifikatkette, die der Clientcomputer an den Server sendet, anhand der Liste der konfigurierten vertrauenswürdigen Aussteller überprüft werden.

Vor Windows Server2012 und Windows8 können Anwendungen oder Prozesse, die den Schannel SSP (einschließlich HTTP.sys und IIS) verwendet eine Liste der vertrauenswürdigen Aussteller bereitstellen, die sie für die Clientauthentifizierung über eine Zertifikatvertrauensliste (CTL) unterstützt.

In Windows Server2012 und Windows8, Änderungen an der zugrunde liegenden Authentifizierungsprozess vorgenommen wurden, damit:

-   Verwaltung der Liste vertrauenswürdiger Aussteller CTL-basierte wird nicht mehr unterstützt.

-   Das Verhalten, senden die Liste vertrauenswürdiger Aussteller wird standardmäßig deaktiviert ist: der Standardwert des Registrierungsschlüssels sendtrustedissuerlist ist jetzt 0 (deaktiviert) anstatt 1.

-   Die Kompatibilität mit früheren Versionen von Windows-Betriebssystemen wurde gewahrt.

**Welchen Nutzen hinzufügen dies?**

Ab Windows Server2012, wurde die Verwendung der CTL mit einem Zertifikat Store-basierten Implementierung ersetzt. Dies ermöglicht vertrautere Verwaltung mithilfe der vorhandenen zertifikatverwaltung des PowerShell-Anbieter sowie Befehlszeilentools wie certutil.exe.

Obwohl verbleibt, wie in Windows Server2008 R2 in Windows Server2012 ist die maximale Größe der Liste der vertrauenswürdigen Zertifizierungsstellen, dass der Schannel SSP (16KB) unterstützt eine neue dedizierte Zertifikatspeicher für clientauthentifizierungsaussteller, damit nicht durch irrelevante Zertifikate nicht in der Meldung enthalten sind.

**So funktioniert es?**

In Windows Server2012 wird die Liste vertrauenswürdiger Aussteller mithilfe von Zertifikatspeichern konfiguriert; einer standardmäßigen globalen Computerzertifikatspeicher und eine optionale pro Standort. Die Quelle der Liste wird wie folgt bestimmt werden:

-   Wenn ein bestimmter Anmeldeinformationsspeicher für den Standort konfigurierten vorhanden ist, wird es als Quelle verwendet werden

-   Wenn keine Zertifikate in der Anwendung definierten Speicher vorhanden sind, prüft Schannel den **Clientauthentifizierungsaussteller** auf dem lokalen Computer zu speichern und, wenn Zertifikate vorhanden sind, verwendet diesen Speicher als Quelle. Wenn in keinem der Speicher kein Zertifikat gefunden wird, wird der Speicher für vertrauenswürdige Stämme überprüft.

-   Wenn weder die globalen oder lokalen Speicher Zertifikate enthalten, verwendet der Schannel-Anbieter die **vertrauenswürdigen Stammzertifizierungsstellen-Zertifikaten** als Quelle der Liste vertrauenswürdiger Aussteller. (Dies ist das Verhalten für Windows Server2008 R2.)

Wenn die **vertrauenswürdige Stammzertifizierungsstellen Speicher** Speicher, der verwendet wurde, enthält eine Mischung aus (selbstsignierten) und (CA) Aussteller Zertifikate von Zertifizierungsstellen, nur die Zertifikate werden standardmäßig an den Server gesendet werden.

**Vorgehensweise beim Konfigurieren von Schannel zur Verwendung des Zertifikatspeichers für vertrauenswürdige Aussteller**

Die Schannel-SSP-Architektur in Windows Server2012 verwenden standardmäßig den Stores wie oben beschrieben zum Verwalten der Liste vertrauenswürdiger Aussteller. Sie können weiterhin die vorhandenen zertifikatverwaltung des PowerShell-Anbieter sowie Befehlszeilentools wie "Certutil" verwenden, zum Verwalten von Zertifikaten.

Informationen zum Verwalten von Zertifikaten mithilfe des PowerShell-Anbieters finden Sie unter [AD CS-Verwaltungs-Cmdlets in Windows](https://technet.microsoft.com/library/hh848365(v=wps.620).aspx).

Informationen zum Verwalten von Zertifikaten mithilfe des zertifikatdienstprogramms finden Sie unter [certutil.exe](https://technet.microsoft.com/library/cc732443.aspx).

Weitere Informationen dazu, welche Daten, einschließlich des anwendungsdefinierten Speichers Anmeldeinformationen für Schannel definiert sind, finden Sie unter [SCHANNEL_CRED Structure (Windows)](https://msdn.microsoft.com/library/windows/desktop/aa379810(v=vs.85).aspx).

**Standardeinstellungen für Vertrauensstellungsmodi**

Es gibt drei Client vertrauen Authentifizierungsmodi von der Schannel-Anbieter unterstützt werden. Der vertrauenswürdige Modus steuert, wie die Überprüfung der Zertifikatkette des Clients ausgeführt wird und eine systemweite Einstellung durch den REG_DWORD-Wert "ClientAuthTrustMode" unter HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\Schannel gesteuert.

|Wert|Vertrauen Sie Modus|Beschreibung|
|-----|-------|--------|
|0|Maschinenvertrauensstellung (Standard)|Erfordert, dass das Clientzertifikat von einem Zertifikat in der Liste der vertrauenswürdigen Aussteller ausgestellt wird.|
|1|Exklusive Stammvertrauensstellung|Erfordert, dass ein Client Ketten mit einem Stammzertifikat enthalten, die in den Speicher für vertrauenswürdige Aussteller vom Aufrufer angegebene Zertifikat. Das Zertifikat muss auch von einem Herausgeber in der Liste der vertrauenswürdigen Aussteller ausgestellt werden|
|2|Exklusive Zertifizierungsstellen-Vertrauensstellung|Erfordert, dass in der Zertifikatkette auf ein dazwischenliegendes Zertifizierungsstellenzertifikat oder ein Stammzertifikat in den vom Aufrufer festgelegten Speicher für Aussteller vertrauenswürdig.|

Informationen zu Authentifizierungsfehlern aufgrund von Konfigurationsproblemen vertrauenswürdiger Aussteller finden Sie im Knowledge Base-Artikel [280256](https://support.microsoft.com/kb/2802568).

### <a name="BKMK_SNI"></a>TLS-Unterstützung für Erweiterungen (Server Name Indicator, SNI)
Sni-Feature erweitert die SSL- und TLS-Protokolle, um die richtige Identifizierung des Servers zulassen, wenn zahlreiche virtuelle Abbilder auf einem einzelnen Server ausgeführt werden. Um die Kommunikation zwischen einem Clientcomputer und einem Server zu schützen, fordert der Clientcomputer ein digitales Zertifikat vom Server. Nachdem der Server auf die Anforderung antwortet und das Zertifikat sendet, wird der Clientcomputer wird untersucht, verwendet, um die Kommunikation zu verschlüsseln und fährt mit dem normalen Austausch von Anforderungen fort. In einem virtuellen Hostszenarien werden jedoch mehrere Domänen, von denen jede über ein eigenes Zertifikat verfügt, auf einem Server gehostet. In diesem Fall hat der Server keine Möglichkeit, im Voraus wissen, welches Zertifikat er an den Clientcomputer senden. Dank SNI kann des Clientcomputers die Zieldomäne weiter oben im Protokoll informieren, und der Server das richtige Zertifikat auswählen kann.

**Welchen Nutzen hinzufügen dies?**

Die folgende zusätzliche Funktionalität:

-   Ermöglicht es Ihnen, mehrere SSL-Websites auf einer einzelnen IP- und Portkombination hosten

-   Verringert die Speicherauslastung, wenn mehrere SSL-Websites auf einem einzelnen Webserver gehostet werden

-   Können mehrere Benutzer gleichzeitig eine Verbindung zu SSL-Websites herstellen

-   Ermöglicht es Ihnen Hinweise für die Auswahl des richtigen Zertifikats während einer Client-Authentifizierung den Endbenutzern über die Benutzeroberfläche des Computers zu übermitteln.

**So funktioniert es**

Schannel SSP unterhält einen speicherinternen Cache der clientverbindungsstatus, die für Clients. Dies ermöglicht Clientcomputern schnell mit dem SSL-Server ohne unterliegen einer vollständigen SSL-Handshake Besuch herzustellen.  Effiziente Verwendung der zertifikatverwaltung lässt mehrere Websites auf einem einzelnen im Vergleich zu vorherigen Versionen des Betriebssystems Windows Server 2012 gehostet werden.

Zertifikatauswahl durch den Endbenutzer wurde verbessert, indem Sie eine Liste der Namen wahrscheinlicher Zertifikataussteller erstellen, die mit Anhaltspunkte bei der Auswahl der Endbenutzer bereitstellen. Diese Liste kann mithilfe von Gruppenrichtlinien konfiguriert werden.

### <a name="BKMK_DTLS"></a>Datagram Transport Layer Security (DTLS)
Das DTLS-Protokoll Version 1.0 wurde Schannel-Security Support Provider hinzugefügt. Das DTLS-Protokoll enthält die Kommunikation datagrammprotokollen für Datenschutz. Das Protokoll ermöglicht Client-/Server-Anwendungen in einer Weise zu kommunizieren, dass Lauschangriffe, Manipulationen oder nachrichtenfälschung verhindert. Das DTLS-Protokoll basiert auf dem Transport Layer Security (TLS)-Protokoll und bietet gleichwertige Sicherheitsgarantien, Reduzieren der Notwendigkeit, IPsec zu verwenden oder eine benutzerdefinierte Anwendungsschicht zu entwerfen.

**Welchen Nutzen hinzufügen dies?**

Datagramme werden häufig beim Streamen von Medien, z.B. spielen oder sicheren Videokonferenzen. Das DTLS-Protokoll mit dem Schannel-Anbieter hinzufügen, erhalten Sie die Möglichkeit, den vertrauten Windows SSPI-Modell zum Sichern der Kommunikation zwischen Clientcomputern und Servern zu verwenden. DTLS ist absichtlich konzipiert, TLS so ähnlich wie möglich, um infrastrukturwiederverwendung zu minimieren und die Menge der Code-und maximieren.

**So funktioniert es**

Anwendungen, die DTLS über UDP nutzen, können das SSPI-Modell in Windows Server 2012 und Windows 8 verwenden. Bestimmte Verschlüsselungssammlungen sind für die Konfiguration, die Konfiguration von TLS ähnelt verfügbar. Schannel nutzt weiterhin den CNG-Kryptografieanbieter verwenden, der FIPS 140-Zertifizierung nutzt, die in Windows Vista eingeführt wurde.

### <a name="BKMK_Deprecated"></a>Veraltete Funktionen
Im Schannel SSP für Windows Server 2012 und Windows 8 gibt es keine veralteten Features oder Funktionen.

## <a name="see-also"></a>Siehe auch
-   [Sicherheitsmodell für die Private Cloud – Wrapperfunktion](https://social.technet.microsoft.com/wiki/contents/articles/6756.private-cloud-security-model-wrapper-functionality.aspx)



