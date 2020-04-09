---
title: Übersicht über TLS-SSL (Schannel SSP)
description: Windows Server-Sicherheit
ms.prod: windows-server
ms.technology: security-tls-ssl
ms.topic: article
ms.assetid: c8836345-16bb-4dcc-8d2b-2b9b687456a3
author: justinha
ms.author: justinha
manager: brianlic
ms.date: 05/16/2018
ms.openlocfilehash: 5478a97a6b333cfc92de100440d53a769a8c0fd9
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80855187"
---
# <a name="overview-of-tls---ssl-schannel-ssp"></a>Übersicht über TLS-SSL (Schannel SSP)

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows 10

In diesem Thema für IT-Experten werden die Änderungen an der Funktionalität im SChannel Security Support Provider (SSP) beschrieben. Hierzu gehören die Transport Layer Security (TLS), die Secure Sockets Layer (SSL) und die DTLS-Authentifizierungsprotokolle (Datagram Transport Layer Security) für Windows Server 2012 R2, Windows Server 2012, Windows 8.1 und Windows 8.

Schannel ist ein Security Support Provider (SSP), der die standardmäßigen Internetauthentifizierungsprotokolle SSL, TLS und DTLS implementiert. Die Security Support Provider-Schnittstelle (Security Support Provider Interface, SSPI) ist eine API, die von Windows-Systemen verwendet wird, um sicherheitsbezogene Funktionen wie Authentifizierungen durchzuführen. Die SSPI dienst als gemeinsame Schnittstelle für mehrere SSPs (Security Support Providers), einschließlich des Schannel SSP.

Weitere Informationen zur Microsoft-Implementierung von TLS und SSL im Schannel SSP finden Sie in der [technischen Referenz zu TLS/SSL (2003)](https://technet.microsoft.com/library/cc784149(v=ws.10).aspx).


## <a name="tlsssl-schannel-ssp-features"></a>Features von TLS/SSL (Schannel SSP)
Im folgenden werden die Features von TLS im Schannel-SSP beschrieben.

### <a name="tls-session-resumption"></a>Wiederaufnahme der TLS-Sitzung
Das Transport Layer Security (TLS)-Protokoll, eine Komponente von Schannel-Security Support Provider, wird verwendet, um Daten zu schützen, die zwischen Programmen in einem nicht vertrauenswürdigen Netzwerk gesendet werden. Mit TLS/SSL können Server und Clientcomputer authentifiziert werden, und mit dem Protokoll können Nachrichten zwischen den authentifizierten Parteien verschlüsselt werden.

Geräte, die häufig eine TSL-Verbindung mit Servern aufbauen, müssen sich bei Ablauf einer Sitzung jeweils neu verbinden. Windows 8.1 und Windows Server 2012 R2 unterstützen jetzt RFC 5077 (Wiederaufnahme der TLS-Sitzung ohne Server seitigen Status). Diese Änderung bietet Windows Phone-und Windows RT-Geräten mit folgenden Aktionen:

-   Reduzierter Ressourcenbedarf auf dem Server

-   Reduzierte Bandbreite und damit verbesserte Effizienz von Clientverbindungen

-   Geringere Dauer des TLS-Handshakes durch Wiederaufnahme der Verbindung

> [!NOTE]
> Die Client seitige Implementierung von RFC 5077 wurde in Windows 8 hinzugefügt.

Informationen zur Zustands losen Wiederaufnahme der TLS-Sitzung finden Sie im IETF-Dokument [RFC 5077.](http://www.ietf.org/rfc/rfc5077)

### <a name="application-protocol-negotiation"></a>Anwendungsprotokollverhandlung
 Windows Server 2012 R2 und Windows 8.1 unterstützen die Client seitige TLS-Anwendungsprotokoll Aushandlung, damit Anwendungen Protokolle als Teil der http 2,0-Standardentwicklung nutzen können, und Benutzer können auf Onlinedienste wie Google und Twitter zugreifen, indem Sie Apps verwenden, die das SPDY-Protokoll ausführen.

**Funktionsweise**

Client- und Serveranwendungen aktivieren die Erweiterung zum Aushandeln des Anwendungsprotokolls durch das Bereitstellen von Listen unterstützter Anwendungsprotokoll-IDs in absteigender bevorzugter Reihenfolge. Der TLS-Client gibt an, dass er das Aushandeln des Anwendungsprotokolls unterstützt, indem er die ALPN-Erweiterung (Application Layer Protocol Negotiation) mit einer Liste clientseitig unterstützter Protokolle in der ClientHello-Nachricht mit einschließt.

Beim Empfang der TLS-Anfrage des Clients durch den Server wertet dieser die Liste unterstützter Protokolle aus, um ein bevorzugtes Protokoll zu finden, das auch der Client unterstützt. Wenn ein solches Protokoll gefunden wird, antwortet der Server mit der ausgewählten Protokoll-ID und führt den Handshake wie gewohnt fort. Ist kein gemeinsames Anwendungsprotokoll vorhanden, sendet der Server eine Meldung über einen kritischen Handshake-Fehler.

### <a name="management-of-trusted-issuers-for-client-authentication"></a><a name="BKMK_TrustedIssuers"></a>Verwaltung vertrauenswürdiger Aussteller für die Client Authentifizierung
Wenn die Authentifizierung des Clientcomputers über SSL oder TLS erforderlich ist, kann der Server so konfiguriert werden, dass eine Liste vertrauenswürdiger Zertifikataussteller gesendet wird. Diese Liste enthält die Gruppe der Zertifikataussteller, denen der Server vertraut, und hilft dem Clientcomputer bei der Auswahl des Clientzertifikats, falls mehrere Zertifikate vorhanden sind. Darüber hinaus muss die Zertifikatkette, die der Clientcomputer an den Server sendet, anhand der Liste der konfigurierten vertrauenswürdigen Aussteller überprüft werden.

Vor Windows Server 2012 und Windows 8 konnten Anwendungen oder Prozesse, die den Schannel SSP verwendeten (einschließlich http. sys und IIS), eine Liste der vertrauenswürdigen Aussteller bereitstellen, die für die Client Authentifizierung über eine Zertifikat Vertrauens Liste unterstützt werden.

In Windows Server 2012 und Windows 8 wurden Änderungen am zugrunde liegenden Authentifizierungsprozess vorgenommen, um Folgendes zu tun:

-   Eine CTL-basierte Verwaltung der Liste vertrauenswürdiger Aussteller wird nicht mehr unterstützt.

-   Das Verhalten zum Senden der Liste vertrauenswürdiger Aussteller ist standardmäßig deaktiviert: der Standardwert des Registrierungsschlüssels sendtreuhänder-Liste ist jetzt 0 (standardmäßig deaktiviert) anstatt 1.

-   Die Kompatibilität mit früheren Versionen von Windows-Betriebssystemen wurde gewahrt.

**Welcher Wert wird von diesem hinzugefügt?**

Ab Windows Server 2012 wurde die Verwendung der CTL durch eine auf einem Zertifikat Speicher basierende Implementierung ersetzt. Dies ermöglicht eine vertrautere Verwaltung mithilfe der vorhandenen Cmdlets zur Zertifikatverwaltung des PowerShell-Anbieters und von Befehlszeilentools wie „certutil.exe“.

Obwohl die maximale Größe der Liste der vertrauenswürdigen Zertifizierungsstellen, die der Schannel SSP unterstützt (16 KB), mit der unter Windows Server 2008 R2 identisch ist, gibt es in Windows Server 2012 einen neuen dedizierten Zertifikat Speicher für Client Authentifizierungs Aussteller, sodass keine nicht verknüpften Zertifikate in der Nachricht enthalten sind.

**Funktionsweise**

In Windows Server 2012 wird die Liste der vertrauenswürdigen Aussteller mithilfe von Zertifikat speichern konfiguriert. ein standardmäßiger globaler Computer Zertifikat Speicher und ein Zertifikat Speicher, der pro Standort optional ist. Die Quelle der Liste wird wie folgt bestimmt:

-   Wenn ein bestimmter Anmeldeinformationsspeicher für diese Site konfiguriert ist, wird dieser als Quelle verwendet.

-   Wenn keine Zertifikate in dem von der Anwendung definierten Speicher vorhanden sind, prüft Schannel den Speicher **Clientauthentifizierungsaussteller** auf dem lokalen Computer und verwendet diesen Speicher als Quelle, wenn Zertifikate vorhanden sind. Wenn in keinem der Speicher ein Zertifikat gefunden wird, wird der Speicher für vertrauenswürdige Stämme überprüft.

-   Wenn weder die globalen noch die lokalen Speicher Zertifikate enthalten, verwendet der Schannel-Anbieter den Speicher **vertrauenswürdiger Stamm Zertifizierungs** stellen als Quelle der Liste vertrauenswürdiger Aussteller. (Dies ist das Verhalten für Windows Server 2008 R2.)

Wenn der verwendete Speicher für **Vertrauenswürdige Stamm Zertifizierungs** stellen eine Mischung aus Zertifikaten des Stamm Zertifikats (selbst signiert) und der Zertifizierungsstelle (Certification Authority, ca) enthält, werden standardmäßig nur die Zertifikate der Zertifizierungsstellen Aussteller an den Server gesendet.

**Konfigurieren von SChannel zur Verwendung des Zertifikat Speicher für vertrauenswürdige Aussteller**

Die Schannel SSP-Architektur in Windows Server 2012 verwendet standardmäßig die oben beschriebenen Speicher, um die Liste der vertrauenswürdigen Aussteller zu verwalten. Es können weiterhin die vorhandenen Cmdlets des PowerShell-Anbieters und von Befehlszeilentools wie „Certutil“ für die Zertifikatverwaltung verwendet werden.

Informationen zum Verwalten von Zertifikaten mithilfe des PowerShell-Anbieters finden Sie unter [AD CS-Verwaltungs-Cmdlets in Windows](https://technet.microsoft.com/library/hh848365(v=wps.620).aspx).

Informationen zum Verwalten von Zertifikaten mithilfe des Zertifikat Dienstprogramms finden Sie unter [certutil. exe](https://technet.microsoft.com/library/cc732443.aspx).

Informationen dazu, welche Daten (einschließlich des Anwendungs definierten Stores) für eine SChannel-Anmelde Information definiert sind, finden Sie unter [SCHANNEL_CRED-Struktur (Windows)](https://msdn.microsoft.com/library/windows/desktop/aa379810(v=vs.85).aspx).

**Standardeinstellungen für Vertrauensstellungs Modi**

Es gibt drei Vertrauensstellungsmodi für die Clientauthentifizierung durch den Schannel-Anbieter. Der Vertrauensstellungs Modus steuert, wie die Überprüfung der Zertifikat Kette des Clients durchgeführt wird, und ist eine systemweite Einstellung, die von der REG_DWORD "clientauthtrustmode" unter HKEY_LOCAL_MACHINE \system\currentcontrolset\control\securityproviders\schannelgesteuert wird.

|Wert|Vertrauensstellungsmodus|Beschreibung|
|-----|-------|--------|
|0|Maschinenvertrauensstellung (Standard)|Erfordert, dass das Clientzertifikat von einem Zertifikat in der Liste der vertrauenswürdigen Aussteller ausgestellt wurde.|
|1|Exklusive Stammvertrauensstellung|Erfordert, dass das Clientzertifikat in der Zertifikatkette auf ein Stammzertifikat zurückgeht, das in dem durch den Aufrufer festgelegten Speicher für vertrauenswürdige Aussteller enthalten ist. Das Zertifikat muss auch von einem Herausgeber in der Liste der vertrauenswürdigen Aussteller ausgestellt worden sein.|
|2|Exklusive Zertifizierungsstellen-Vertrauensstellung|Erfordert, dass das Clientzertifikat in der Zertifikatkette auf ein dazwischenliegendes Zertifizierungsstellenzertifikat oder ein Stammzertifikat zurückgeht, das in dem durch den Aufrufer festgelegten Speicher für vertrauenswürdige Aussteller enthalten ist.|

Informationen zu Authentifizierungs Fehlern aufgrund von Konfigurationsproblemen der vertrauenswürdigen Aussteller finden Sie im Knowledge Base-Artikel [280256](https://support.microsoft.com/kb/2802568).

### <a name="tls-support-for-server-name-indicator-sni-extensions"></a><a name="BKMK_SNI"></a>TLS-Unterstützung für SNI-Erweiterungen (Server Name Indicator)
Das SNI-Feature stellt eine Erweiterung der Protokolle SSL und TLS dar und ermöglicht die richtige Identifizierung des Servers, wenn zahlreiche virtuelle Images auf einem einzelnen Server ausgeführt werden. Um die Sicherheit der Kommunikation zwischen einem Clientcomputer und einem Server herzustellen, fordert der Clientcomputer ein digitales Zertifikat beim Server an. Nachdem der Server auf die Anforderung geantwortet und das Zertifikat gesendet hat, prüft der Clientcomputer es, verwendet es zur Verschlüsselung der Kommunikation und fährt mit dem normalen Austausch von Anforderungen und Antworten fort. Bei virtuellen Hostszenarien werden jedoch mehrere Domänen, von denen jede über ein eigenes Zertifikat verfügt, auf einem Server gehostet. In diesem Fall kann der Server nicht im Voraus wissen, welches Zertifikat er an den Clientcomputer senden muss. Dank SNI kann der Clientcomputer die Zieldomäne zu einem früheren Zeitpunkt im Protokoll informieren, damit der Server das richtige Zertifikat auswählen kann.

**Welcher Wert wird von diesem hinzugefügt?**

Die folgende zusätzliche Funktionalität:

-   Sie können mehrere SSL-Websites mit einer einzelnen IP- und Portkombination hosten.

-   Der Speicherbedarf wird reduziert, wenn mehrere SSL-Websites auf einem einzelnen Webserver gehostet werden.

-   Mehr Benutzer können gleichzeitig die Verbindung zu SSL-Websites herstellen.

-   Sie können Endbenutzern über die Benutzeroberfläche des Computers Hinweise zur Auswahl des richtigen Zertifikats während eines Clientauthentifizierungsprozesses geben.

**Funktionsweise**

Schannel SSP unterhält einen speicherinternen Cache der Clientverbindungsstatus, die für Clients zulässig sind. Dadurch erhalten Clientcomputer die Möglichkeit, die Verbindung mit dem SSL-Server bei Folgeaufrufen schnell wieder aufzubauen, ohne einen vollständigen SSL-Handshake durchführen zu müssen.  Durch diese effiziente Verwendung der Zertifikat Verwaltung können im Vergleich zu früheren Betriebssystemversionen mehr Standorte auf einem einzelnen Windows Server 2012 gehostet werden.

Die Zertifikatauswahl durch den Endbenutzer wurde verbessert, indem Ihnen die Möglichkeit gegeben wird, eine Liste der Namen möglicher Zertifikataussteller zu erstellen, die Endbenutzern Anhaltspunkte bei der Auswahl liefert. Diese Liste kann mit einer Gruppenrichtlinie konfiguriert werden.

### <a name="datagram-transport-layer-security-dtls"></a><a name="BKMK_DTLS"></a>Datagramm-Transport Layer Security (DTLS)
Das DTLS-Protokoll in der Version 1.0 wurde Schannel Security Support Provider hinzugefügt. Das DTLS-Protokoll sorgt bei der Kommunikation mit Datagrammprotokollen für Datenschutz. Das Protokoll ermöglicht es Client/Server-Anwendungen, so zu kommunizieren, dass Lauschangriffe, Manipulationen oder Nachrichtenfälschung vermieden werden. Das DTLS-Protokoll basiert auf dem TLS-Protokoll (Transport Layer Security) und bietet gleichwertige Sicherheitsgarantien. Daher wird die Notwendigkeit der Verwendung von IPsec oder der Erstellung eines benutzerdefinierten Sicherheitsprotokolls für die Anwendungsschicht verringert.

**Welcher Wert wird von diesem hinzugefügt?**

Datagramme sind häufig in Streamingmedien, z. b. Spiele oder gesicherte Videokonferenzen. Indem Sie das DTLS-Protokoll dem Schannel-Provider hinzufügen, können Sie das gewohnte Windows SSPI-Modell zur Sicherung der Kommunikation zwischen Clientcomputern und -servern nutzen. Zum Konzept von DTLS gehört es, TLS so ähnlich wie möglich zu sein, um einerseits weitere Sicherheitsvorkehrungen zu minimieren und andererseits den Umfang der Code- und Infrastrukturwiederverwendung zu maximieren.

**Funktionsweise**

Anwendungen, die DTLS über UDP nutzen, können das SSPI-Modell in Windows Server 2012 und Windows 8 verwenden. Bestimmte Verschlüsselungssammlungen sind für die Konfiguration verfügbar, die der Konfiguration von TLS ähnelt. Schannel nutzt weiterhin den CNG-Kryptografieanbieter, der die in Windows Vista eingeführte FIPS 140-Zertifizierung nutzt.

### <a name="deprecated-functionality"></a><a name="BKMK_Deprecated"></a>Veraltete Funktionen
Im Schannel SSP für Windows Server 2012 und Windows 8 gibt es keine veralteten Features oder Funktionen.

## <a name="see-also"></a>Siehe auch
-   [Sicherheitsmodell für die Private Cloud: Wrapper Funktionalität](https://social.technet.microsoft.com/wiki/contents/articles/6756.private-cloud-security-model-wrapper-functionality.aspx)



