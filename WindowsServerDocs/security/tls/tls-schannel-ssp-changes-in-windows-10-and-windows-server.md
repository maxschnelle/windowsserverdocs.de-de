---
title: TLS (Schannel SSP)
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: ebd3c40c-b4c0-4f6d-a00c-f90eda4691df
manager: alanth
author: justinha
ms.technology: security-authentication
ms.date: 11/09/2016
ms.openlocfilehash: 6e1a229bfc7063597f8994c71bbaec5637d084a4
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2017
---
# <a name="tls-schannel-ssp-changes-in-windows-10-and-windows-server-2016"></a>TLS (Schannel SSP) Änderungen in Windows10 und Windows Server2016

>Gilt für: Windows Server 2016 und Windows10

## <a name="cipher-suite-changes"></a>Cipher Suite Änderungen

Windows10, Version 1511 und Windows Server2016 Hinzufügen von Unterstützung für die Konfiguration der Reihenfolge der Verschlüsselungssammlungen (Mobile Device Management, MDM) verwenden.

Cipher Suite Priorität Reihenfolge Änderungen finden Sie unter [Verschlüsselungssammlungen in Schannel](https://msdn.microsoft.com/library/windows/desktop/aa374757.aspx).

Unterstützung für die folgenden Verschlüsselungssammlungen hinzugefügt:

- TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256 (RFC 5289) in Windows10, Version 1507 und Windows Server2016
- TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384 (RFC 5289) in Windows10, Version 1507 und Windows Server2016

DisabledByDefault für die folgenden Verschlüsselungssammlungen ändern:

- TLS_DHE_DSS_WITH_AES_256_CBC_SHA256 (RFC 5246) in Windows10, Version 1703
- TLS_DHE_DSS_WITH_AES_128_CBC_SHA256 (RFC 5246) in Windows10, Version 1703
- TLS_DHE_DSS_WITH_AES_256_CBC_SHA (RFC 5246) in Windows10, Version 1703
- TLS_DHE_DSS_WITH_AES_128_CBC_SHA (RFC 5246) in Windows10, Version 1703
- TLS_DHE_DSS_WITH_3DES_EDE_CBC_SHA (RFC 5246) in Windows10, Version 1703
- In Windows10, Version 1709 TLS_RSA_WITH_RC4_128_SHA
- In Windows10, Version 1709 TLS_RSA_WITH_RC4_128_MD5

Ab Windows10, Version 1507 und Windows Server2016, werden standardmäßig SHA-512-Zertifikate unterstützt werden.

### <a name="rsa-key-changes"></a>RSA-Schlüssel ändern

Fügen Sie Windows10, Version 1507 und Windows Server2016 Registrierung Konfigurationsoptionen für Client-RSA-Schlüsselgrößen hinzu.

Weitere Informationen finden Sie unter [KeyExchangeAlgorithm – Client-RSA-Schlüsselgrößen](tls-registry-settings.md#keyexchangealgorithm---client-rsa-key-sizes).

### <a name="diffie-hellman-key-changes"></a>Diffie-Hellman-wichtige Änderungen

Fügen Konfigurationsoptionen für Schlüsselgrößen Diffie-Hellman-Registrierung, Windows10, Version 1507 und Windows Server2016.

Weitere Informationen finden Sie unter [KeyExchangeAlgorithm – Diffie-Hellman-Schlüsselgrößen](tls-registry-settings.md#keyexchangealgorithm---diffie-hellman-key-sizes).

### <a name="schusestrongcrypto-option-changes"></a>Änderungen von SCH_USE_STRONG_CRYPTO

Mit Windows10, Version 1507 und Windows Server2016 [SCH_USE_STRONG_CRYPTO](https://msdn.microsoft.com/library/windows/desktop/aa379810.aspx) Option jetzt deaktiviert NULL, MD5, DES, und Exportieren von Verschlüsselungen.

## <a name="elliptical-curve-changes"></a>Elliptische Kurve ändert

Fügen Sie Windows10, Version 1507 und Windows Server2016 Gruppenrichtlinienkonfiguration für elliptische Kurven unter Computerkonfiguration > Administrative Vorlagen > Netzwerk > Einstellungen der SSL-Konfiguration. Die Reihenfolge der ECC-Kurve Liste gibt die Reihenfolge, in der elliptische Kurven bevorzugt werden, als auch unterstützten Kurven nicht aktiviert werden kann. 
 
Unterstützung für die folgenden elliptischen Kurven hinzugefügt:

- BrainpoolP256r1 (RFC 7027) in Windows10, Version 1507 und Windows Server2016
- BrainpoolP384r1 (RFC 7027) in Windows10, Version 1507 und Windows Server2016 
- BrainpoolP512r1 (RFC 7027) in Windows10, Version 1507 und Windows Server2016
- Curve25519 (RFC-Entwurf-Ietf-Tls-curve25519) in Windows10, Version 1607 und Windows Server2016

## <a name="dispatch-level-support-for-sealmessage--unsealmessage"></a>Unterstützung für SealMessage & UnsealMessage verteilen

Windows10, Version 1507 und Windows Server2016 können Sie Unterstützung für SealMessage/UnsealMessage auf Verteilungsebene hinzufügen.

## <a name="dtls-12"></a>DTLS 1.2

Windows10, Version 1607 und Windows Server2016 wird Unterstützung für DTLS 1.2 (RFC 6347) hinzufügen.

## <a name="httpsys-thread-pool"></a>HTTP.SYS Threadpool 

Fügen Windows10, Version 1607 und Windows Server2016 Registrierungskonfiguration der Größe des Thread-Pools verwendet, um TLS-Handshakes für HTTP.SYS.

Registrierungspfad: 

HKLM\SYSTEM\CurrentControlSet\Control\LSA

Um eine maximale Threadpoolgröße pro CPU-Kern anzugeben, Erstellen einer **MaxAsyncWorkerThreadsPerCpu** Eintrag. Dieser Eintrag ist nicht standardmäßig in der Registrierung vorhanden. Nachdem Sie den Eintrag erstellt haben, ändern Sie den DWORD-Wert auf die gewünschte Größe. Wenn nicht konfiguriert ist, sind maximal 2 Threads pro CPU-Kern.

## <a name="next-protocol-negotiation-npn-support"></a>Support am nächsten Protocol Negotiation (NPN)

Ab Windows10, Version 1703, weiter Protocol Negotiation (NPN) wurde entfernt und wird nicht mehr unterstützt.

## <a name="pre-shared-key-psk"></a>Vorinstallierten Schlüssel (PSK)

Windows10, Version 1607 und Windows Server2016 Hinzufügen von Unterstützung für die PSK-Schlüsselaustauschalgorithmus (RFC 4279).

Unterstützung für die folgenden PSK-Verschlüsselungssammlungen hinzugefügt:

- TLS_PSK_WITH_AES_128_CBC_SHA256 (RFC 5487) in Windows10, Version 1607 und Windows Server2016
- TLS_PSK_WITH_AES_256_CBC_SHA384(RFC 5487) in Windows10, Version 1607 und Windows Server2016
- TLS_PSK_WITH_NULL_SHA256 (RFC 5487) in Windows10, Version 1607 und Windows Server2016
- TLS_PSK_WITH_NULL_SHA384 (RFC 5487) in Windows10, Version 1607 und Windows Server2016
- TLS_PSK_WITH_AES_128_GCM_SHA256 (RFC 5487) in Windows10, Version 1607 und Windows Server2016
- TLS_PSK_WITH_AES_256_GCM_SHA384 (RFC 5487) in Windows10, Version 1607 und Windows Server2016

## <a name="session-resumption-without-server-side-state-server-side-performance-improvements"></a>Wiederaufnahme der Sitzung ohne serverseitigen Zustand serverseitige Leistungsverbesserungen

Windows10, Version 1507 und Windows Server2016 bieten im Vergleich zu Windows Server2012 Sitzungstickets 30% mehr Sitzung Wiederaufnahme pro Sekunde.

## <a name="session-hash-and-extended-master-secret-extension"></a>Sitzung Hash und erweiterte Master geheimen Schlüssel-Erweiterung

Windows10, Version 1507 und Windows Server2016 Hinzufügen der Unterstützung für RFC 7627: Transport Layer Security (TLS) Sitzung Hash und erweiterte Master geheimen Schlüssel Erweiterung.

Aufgrund dieser Änderung erfordert Windows10 und Windows Server2016 3rd Party [CNG-SSL-Anbieter](https://msdn.microsoft.com/library/windows/desktop/ff468652.aspx) Updates NCRYPT_SSL_INTERFACE_Version_3 unterstützen und um die neue Oberfläche zu beschreiben.


## <a name="ssl-support"></a>SSL-Unterstützung

Ab Windows10, Version 1607 und Windows Server2016, ist TLS-Client und Server SSL 3.0 standardmäßig deaktiviert. Dies bedeutet, dass wenn die Anwendung oder den Dienst ausdrücklich SSL 3.0 über die SSPI anfordert, der Client wird nie anbieten oder übernehmen Sie SSL 3.0 und der Server wird nie SSL 3.0 aktivieren.

Ab Windows10 Version 1607 und Windows Server2016, SSL 2.0 wurde entfernt und wird nicht mehr unterstützt.

## <a name="changes-to-windows-tls-adherence-to-tls-12-requirements-for-connections-with-non-compliant-tls-clients"></a>Änderungen an Windows TLS Einhaltung von TLS 1.2-Anforderungen für Verbindungen mit nicht kompatiblen TLS-Clients

In TLS 1.2 die, der Client verwendet die ["Signature_algorithms" Erweiterung](https://tools.ietf.org/html/rfc5246#section-7.4.1.4.1) an, dass auf dem Server die Signatur-Hash-Algorithmus-Paare in digitalen Signaturen (d.h. Serverzertifikate und Schlüsselaustausch Server) verwendet werden können. Der RFC TLS 1.2 erfordert auch, dass die Nachricht des Servers Zertifikat "Signature_algorithms" Erweiterung berücksichtigt:

"Wenn der Client eine Erweiterung"Signature_algorithms"bereitgestellt, müssen dann alle Zertifikate, die vom Server durch ein Paar der Hash-Signatur-Algorithmus, die in dieser Erweiterung erscheint signiert werden."

In der Praxis einige TLS-Clients von Drittanbietern nicht Einhaltung der TLS 1.2 RFC und Fehler alle Signatur und hash-Algorithmus-Paare, die sie in der Erweiterung "Signature_algorithms" akzeptiert werden, oder die Erweiterung ganz weglassen (die zweite Option gibt an, mit dem Server, dass der Client nur mit RSA, DSA und ECDSA SHA1 unterstützt).

Ein TLS-Server ist oft nur ein Zertifikat konfiguriert pro Endpunkt, was bedeutet, dass der Server kann nicht immer ein Zertifikat bereitstellen, die der Client Anforderungen erfüllt.

Vor Windows10 und Windows Server2016, der Windows-TLS-Stapel eingehalten ausschließlich die TLS 1.2 RFC-Anforderungen, wodurch Verbindungsfehler mit nicht kompatiblen RFC TLS-Clients sowie zur Interoperabilität. In Windows10 und Windows Server2016 die Einschränkungen gelockert werden, und der Server kann ein Zertifikat, das TLS 1.2 RFC nicht einhält senden, wenn dies der Server nur die Option ist. Der Client kann dann fortsetzen oder beenden den Handshake.

Bei der Validierung von Server- und Clientzertifikaten wird im Windows-TLS-Stapel ausschließlich der RFC TLS 1.2 entspricht und lässt nur die ausgehandelten Signatur und Hashalgorithmen in die Server- und Clientzertifikaten.


