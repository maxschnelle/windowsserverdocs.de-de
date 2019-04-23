---
title: TLS – Übersicht über SSL (Schannel SSP)
description: Windows Server-Sicherheit
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-tls-ssl
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c8836345-16bb-4dcc-8d2b-2b9b687456a3
author: justinha
ms.author: justinha
manager: brianlic-msft
ms.date: 05/16/2018
ms.openlocfilehash: 48dabb5ad83b82f0a93992ad8c24456a8a8e7ef5
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59873091"
---
# <a name="overview-of-tls---ssl-schannel-ssp"></a>Übersicht über TLS – SSL (Schannel SSP)

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016, Windows 10

In diesem Thema für IT-Experten Aufschluss über Änderungen an der Funktionalität in die Schannel Security Support Provider (SSP), dazu die Transport Layer Security (TLS), Secure Sockets Layer (SSL) und das Datagram Transport Layer Security (DTLS gehören) Protokolle zur Authentifizierung für Windows Server 2012 R2, Windows Server 2012, Windows 8.1 und Windows 8.

Schannel ist ein Security Support Provider (SSP), der die standardmäßigen Internetauthentifizierungsprotokolle SSL, TLS und DTLS implementiert. Die Security Support Provider-Schnittstelle (Security Support Provider Interface, SSPI) ist eine API, die von Windows-Systemen verwendet wird, um sicherheitsbezogene Funktionen wie Authentifizierungen durchzuführen. Die SSPI dienst als gemeinsame Schnittstelle für mehrere SSPs (Security Support Providers), einschließlich des Schannel SSP.

Weitere Informationen zur Microsoft Implementierung von TLS und SSL im Schannel SSP finden Sie unter den [technische Referenz zu TLS/SSL (2003)](https://technet.microsoft.com/library/cc784149(v=ws.10).aspx).


##<a name="tlsssl-schannel-ssp-features"></a>TLS/SSL (Schannel SSP)-Funktionen
Im folgenden werden die Funktionen von TLS im Schannel SSP. beschrieben.

### <a name="tls-session-resumption"></a>Wiederaufnahme der TLS-Sitzung
Das Transport Layer Security (TLS)-Protokoll, eine Komponente von Schannel-Security Support Provider, wird verwendet, um Daten zu schützen, die zwischen Programmen in einem nicht vertrauenswürdigen Netzwerk gesendet werden. Mit TLS/SSL können Server und Clientcomputer authentifiziert werden, und mit dem Protokoll können Nachrichten zwischen den authentifizierten Parteien verschlüsselt werden.

Geräte, die häufig eine TSL-Verbindung mit Servern aufbauen, müssen sich bei Ablauf einer Sitzung jeweils neu verbinden. Windows 8.1 und Windows Server 2012 R2 unterstützen jetzt RFC 5077 (TLS-Sitzungswiederaufnahme ohne serverseitigen Zustand). Diese Änderung bietet Windows Phone und Windows RT-Geräte mit:

-   Reduzierter Ressourcenbedarf auf dem Server

-   Reduzierte Bandbreite und damit verbesserte Effizienz von Clientverbindungen

-   Geringere Dauer des TLS-Handshakes durch Wiederaufnahme der Verbindung

> [!NOTE]
> Die Implementierung der clientseitigen RFC 5077 wurde in Windows 8 hinzugefügt.

Informationen zur statusfreien TLS-sitzungswiederaufnahme finden Sie im IETF-Dokument [RFC 5077.](http://www.ietf.org/rfc/rfc5077)

### <a name="application-protocol-negotiation"></a>Anwendungsprotokollverhandlung
 Windows Server 2012 R2 und Windows 8.1 unterstützen die clientseitige TLS-anwendungsprotokollverhandlung, damit Anwendungen Protokolle, als Teil der standard-HTTP-2.0-Entwicklung nutzen können und Onlinedienste wie Google und Twitter können zugreifen mithilfe von apps, die ausgeführt Das SPDY-Protokoll.

**So funktioniert es**

Client- und Serveranwendungen aktivieren die Erweiterung zum Aushandeln des Anwendungsprotokolls durch das Bereitstellen von Listen unterstützter Anwendungsprotokoll-IDs in absteigender bevorzugter Reihenfolge. Der TLS-Client gibt an, dass er das Aushandeln des Anwendungsprotokolls unterstützt, indem er die ALPN-Erweiterung (Application Layer Protocol Negotiation) mit einer Liste clientseitig unterstützter Protokolle in der ClientHello-Nachricht mit einschließt.

Beim Empfang der TLS-Anfrage des Clients durch den Server wertet dieser die Liste unterstützter Protokolle aus, um ein bevorzugtes Protokoll zu finden, das auch der Client unterstützt. Wenn ein solches Protokoll gefunden wird, antwortet der Server mit der ausgewählten Protokoll-ID und führt den Handshake wie gewohnt fort. Ist kein gemeinsames Anwendungsprotokoll vorhanden, sendet der Server eine Meldung über einen kritischen Handshake-Fehler.

### <a name="BKMK_TrustedIssuers"></a>Verwaltung vertrauenswürdiger Aussteller zur Clientauthentifizierung
Wenn die Authentifizierung des Clientcomputers über SSL oder TLS erforderlich ist, kann der Server so konfiguriert werden, dass eine Liste vertrauenswürdiger Zertifikataussteller gesendet wird. Diese Liste enthält die Gruppe der Zertifikataussteller, denen der Server vertraut, und hilft dem Clientcomputer bei der Auswahl des Clientzertifikats, falls mehrere Zertifikate vorhanden sind. Darüber hinaus muss die Zertifikatkette, die der Clientcomputer an den Server sendet, anhand der Liste der konfigurierten vertrauenswürdigen Aussteller überprüft werden.

Vor Windows Server 2012 und Windows 8 können Anwendungen oder Prozesse, die den Schannel SSP (einschließlich HTTP.sys und IIS) verwendet eine Liste der vertrauenswürdigen Herausgeber bereitstellen, die sie für die Clientauthentifizierung über eine Zertifikatvertrauensliste (CTL) unterstützt.

In Windows Server 2012 und Windows 8, wurden Änderungen am zugrunde liegenden Authentifizierungsprozess vorgenommen, damit:

-   Eine CTL-basierte Verwaltung der Liste vertrauenswürdiger Aussteller wird nicht mehr unterstützt.

-   Das Verhalten, die Liste vertrauenswürdiger Aussteller zu senden, ist standardmäßig deaktiviert: Der Standardwert des Registrierungsschlüssels SendTrustedIssuerList ist jetzt 0 (deaktiviert) anstatt 1.

-   Die Kompatibilität mit früheren Versionen von Windows-Betriebssystemen wurde gewahrt.

**Welcher Wert fügt diese hinzu?**

Ab Windows Server 2012, wurde die Verwendung der CTL durch eine Zertifikat-basierte Store Implementierung ersetzt. Dies ermöglicht eine vertrautere Verwaltung mithilfe der vorhandenen Cmdlets zur Zertifikatverwaltung des PowerShell-Anbieters und von Befehlszeilentools wie „certutil.exe“.

Obwohl die maximale Größe der Liste der vertrauenswürdigen Zertifizierungsstellen (16 KB) der Schannel-SSP unterstützt, wie in Windows Server 2008 R2 unverändert, in Windows Server 2012 besteht ein neuen, dedizierten Zertifikatspeicher für clientauthentifizierungsaussteller, damit nicht verknüpfte Zertifikate sind nicht in der Nachricht enthalten.

**So funktioniert's**

In Windows Server 2012 wird die Liste vertrauenswürdiger Aussteller mithilfe von Zertifikatspeichern konfiguriert; einem standardmäßigen globalen Computerzertifikatspeicher und einer optionalen pro Standort. Die Quelle der Liste wird wie folgt bestimmt:

-   Wenn ein bestimmter Anmeldeinformationsspeicher für diese Site konfiguriert ist, wird dieser als Quelle verwendet.

-   Wenn keine Zertifikate in dem von der Anwendung definierten Speicher vorhanden sind, prüft Schannel den Speicher **Clientauthentifizierungsaussteller** auf dem lokalen Computer und verwendet diesen Speicher als Quelle, wenn Zertifikate vorhanden sind. Wenn in keinem der Speicher ein Zertifikat gefunden wird, wird der Speicher für vertrauenswürdige Stämme überprüft.

-   Wenn weder die globalen oder lokalen Speicher Zertifikate enthalten, verwendet der Schannel-Anbieter die **vertrauenswürdigen Stammzertifizierungsstellen-Zertifikaten** als Quelle der Liste vertrauenswürdiger Aussteller. (Dies ist das Verhalten für Windows Server 2008 R2.)

Wenn die **als vertrauenswürdig eingestufte Stammzertifizierungsstellen Speicher** Speicher, der verwendet wurde, enthält eine Mischung aus (selbstsignierten) und die Aussteller-Zertifikate von Zertifizierungsstellen (ZS), nur die Zertifikate werden standardmäßig an den Server gesendet werden.

**Gewusst wie: Konfigurieren von Schannel zur Verwendung des Zertifikatspeichers für vertrauenswürdige Aussteller**

Die Schannel-SSP-Architektur in Windows Server 2012 verwenden standardmäßig den Stores wie oben beschrieben zum Verwalten der Liste vertrauenswürdiger Aussteller. Es können weiterhin die vorhandenen Cmdlets des PowerShell-Anbieters und von Befehlszeilentools wie „Certutil“ für die Zertifikatverwaltung verwendet werden.

Informationen zum Verwalten von Zertifikaten mithilfe des PowerShell-Anbieters finden Sie unter [AD CS-Verwaltungs-Cmdlets in Windows](https://technet.microsoft.com/library/hh848365(v=wps.620).aspx).

Informationen zum Verwalten von Zertifikaten mithilfe des zertifikatdienstprogramms finden Sie unter [certutil.exe](https://technet.microsoft.com/library/cc732443.aspx).

Weitere Informationen dazu, welche Daten, einschließlich des anwendungsdefinierten Speichers, Anmeldeinformationen für Schannel definiert ist, finden Sie unter [SCHANNEL_CRED-Struktur (Windows)](https://msdn.microsoft.com/library/windows/desktop/aa379810(v=vs.85).aspx).

**Standardeinstellungen für Vertrauensstellungsmodi**

Es gibt drei Vertrauensstellungsmodi für die Clientauthentifizierung durch den Schannel-Anbieter. Der vertrauensstellungsmodus steuert, wie die Überprüfung der Zertifikatkette des Clients ausgeführt wird, und ist eine systemweite Einstellung, die durch den REG_DWORD-Wert "ClientAuthTrustMode" unter HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\Schannel gesteuert .

|Wert|Vertrauensstellungsmodus|Beschreibung|
|-----|-------|--------|
|0|Maschinenvertrauensstellung (Standard)|Erfordert, dass das Clientzertifikat von einem Zertifikat in der Liste der vertrauenswürdigen Aussteller ausgestellt wurde.|
|1|Exklusive Stammvertrauensstellung|Erfordert, dass das Clientzertifikat in der Zertifikatkette auf ein Stammzertifikat zurückgeht, das in dem durch den Aufrufer festgelegten Speicher für vertrauenswürdige Aussteller enthalten ist. Das Zertifikat muss auch von einem Herausgeber in der Liste der vertrauenswürdigen Aussteller ausgestellt worden sein.|
|2|Exklusive Zertifizierungsstellen-Vertrauensstellung|Erfordert, dass das Clientzertifikat in der Zertifikatkette auf ein dazwischenliegendes Zertifizierungsstellenzertifikat oder ein Stammzertifikat zurückgeht, das in dem durch den Aufrufer festgelegten Speicher für vertrauenswürdige Aussteller enthalten ist.|

Informationen zu Authentifizierungsfehlern aufgrund von Konfigurationsproblemen vertrauenswürdiger Aussteller finden Sie im Knowledge Base-Artikel [280256](https://support.microsoft.com/kb/2802568).

### <a name="BKMK_SNI"></a>Unterstützung von TLS-Erweiterungen (Server Name Indicator, SNI)
Das SNI-Feature stellt eine Erweiterung der Protokolle SSL und TLS dar und ermöglicht die richtige Identifizierung des Servers, wenn zahlreiche virtuelle Images auf einem einzelnen Server ausgeführt werden. Um die Sicherheit der Kommunikation zwischen einem Clientcomputer und einem Server herzustellen, fordert der Clientcomputer ein digitales Zertifikat beim Server an. Nachdem der Server auf die Anforderung geantwortet und das Zertifikat gesendet hat, prüft der Clientcomputer es, verwendet es zur Verschlüsselung der Kommunikation und fährt mit dem normalen Austausch von Anforderungen und Antworten fort. Bei virtuellen Hostszenarien werden jedoch mehrere Domänen, von denen jede über ein eigenes Zertifikat verfügt, auf einem Server gehostet. In diesem Fall kann der Server nicht im Voraus wissen, welches Zertifikat er an den Clientcomputer senden muss. Dank SNI kann der Clientcomputer die Zieldomäne zu einem früheren Zeitpunkt im Protokoll informieren, damit der Server das richtige Zertifikat auswählen kann.

**Welcher Wert fügt diese hinzu?**

Die folgende zusätzliche Funktionalität:

-   Sie können mehrere SSL-Websites mit einer einzelnen IP- und Portkombination hosten.

-   Der Speicherbedarf wird reduziert, wenn mehrere SSL-Websites auf einem einzelnen Webserver gehostet werden.

-   Mehr Benutzer können gleichzeitig die Verbindung zu SSL-Websites herstellen.

-   Sie können Endbenutzern über die Benutzeroberfläche des Computers Hinweise zur Auswahl des richtigen Zertifikats während eines Clientauthentifizierungsprozesses geben.

**So funktioniert es**

Schannel SSP unterhält einen speicherinternen Cache der Clientverbindungsstatus, die für Clients zulässig sind. Dadurch erhalten Clientcomputer die Möglichkeit, die Verbindung mit dem SSL-Server bei Folgeaufrufen schnell wieder aufzubauen, ohne einen vollständigen SSL-Handshake durchführen zu müssen.  Effiziente Verwendung der zertifikatverwaltung können mehr Websites auf einem einzelnen Windows Server 2012 im Vergleich zu vorherigen Betriebssystemversionen gehostet werden.

Die Zertifikatauswahl durch den Endbenutzer wurde verbessert, indem Ihnen die Möglichkeit gegeben wird, eine Liste der Namen möglicher Zertifikataussteller zu erstellen, die Endbenutzern Anhaltspunkte bei der Auswahl liefert. Diese Liste kann mit einer Gruppenrichtlinie konfiguriert werden.

### <a name="BKMK_DTLS"></a>Datagram Transport Layer Security (DTLS)
Das DTLS-Protokoll in der Version 1.0 wurde Schannel Security Support Provider hinzugefügt. Das DTLS-Protokoll sorgt bei der Kommunikation mit Datagrammprotokollen für Datenschutz. Das Protokoll ermöglicht es Client/Server-Anwendungen, so zu kommunizieren, dass Lauschangriffe, Manipulationen oder Nachrichtenfälschung vermieden werden. Das DTLS-Protokoll basiert auf dem TLS-Protokoll (Transport Layer Security) und bietet gleichwertige Sicherheitsgarantien. Daher wird die Notwendigkeit der Verwendung von IPsec oder der Erstellung eines benutzerdefinierten Sicherheitsprotokolls für die Anwendungsschicht verringert.

**Welcher Wert fügt diese hinzu?**

Datagramme werden häufig beim Streamen von Medien, wie z. B. spielen oder sicheren Videokonferenzen. Indem Sie das DTLS-Protokoll dem Schannel-Provider hinzufügen, können Sie das gewohnte Windows SSPI-Modell zur Sicherung der Kommunikation zwischen Clientcomputern und -servern nutzen. Zum Konzept von DTLS gehört es, TLS so ähnlich wie möglich zu sein, um einerseits weitere Sicherheitsvorkehrungen zu minimieren und andererseits den Umfang der Code- und Infrastrukturwiederverwendung zu maximieren.

**So funktioniert es**

Anwendungen, die DTLS über UDP nutzen, können das SSPI-Modell in Windows Server 2012 und Windows 8 verwenden. Bestimmte Verschlüsselungssammlungen sind für die Konfiguration verfügbar, die der Konfiguration von TLS ähnelt. Schannel nutzt weiterhin den CNG-Kryptografieanbieter, der die in Windows Vista eingeführte FIPS 140-Zertifizierung nutzt.

### <a name="BKMK_Deprecated"></a>Veraltete Funktionen
Im Schannel SSP für Windows Server 2012 und Windows 8 gibt es keine veralteten Features oder Funktionen.

## <a name="see-also"></a>Siehe auch
-   [Sicherheitsmodell für die Private Cloud – Wrapperfunktion](https://social.technet.microsoft.com/wiki/contents/articles/6756.private-cloud-security-model-wrapper-functionality.aspx)



