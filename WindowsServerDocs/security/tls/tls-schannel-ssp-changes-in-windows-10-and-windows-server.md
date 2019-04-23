---
title: TLS (Schannel SSP)
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: ebd3c40c-b4c0-4f6d-a00c-f90eda4691df
manager: alanth
author: justinha
ms.technology: security-authentication
ms.date: 05/16/2018
ms.openlocfilehash: 030fd81e0c6ba0423f1fa73e680006766cf2b180
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59890771"
---
# <a name="tls-schannel-ssp-changes-in-windows-10-and-windows-server-2016"></a>TLS (Schannel SSP) Änderungen in Windows 10 und Windows Server 2016

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016 und Windows 10

## <a name="cipher-suite-changes"></a>Cipher Suite-Änderungen

Windows 10, Version 1511 und Windows Server 2016 wird Unterstützung für die Konfiguration der Reihenfolge der Verschlüsselungssammlungen mit (Mobile Device Management, MDM) hinzufügen.

Cipher Suite Priorität Anordnung von Änderungen, finden Sie unter [Verschlüsselungssammlungen in Schannel](https://msdn.microsoft.com/library/windows/desktop/aa374757.aspx).

Unterstützung für die folgenden Verschlüsselungssammlungen hinzugefügt:

- TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256 (RFC 5289) in Windows 10, Version 1507 und Windows Server 2016
- TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384 (RFC 5289) in Windows 10, Version 1507 und Windows Server 2016

DisabledByDefault ändern für die folgenden Verschlüsselungssammlungen:

- TLS_DHE_DSS_WITH_AES_256_CBC_SHA256 (RFC 5246) in Windows 10 Version 1703
- TLS_DHE_DSS_WITH_AES_128_CBC_SHA256 (RFC 5246) in Windows 10 Version 1703
- TLS_DHE_DSS_WITH_AES_256_CBC_SHA (RFC 5246) in Windows 10 Version 1703
- TLS_DHE_DSS_WITH_AES_128_CBC_SHA (RFC 5246) in Windows 10 Version 1703
- TLS_DHE_DSS_WITH_3DES_EDE_CBC_SHA (RFC 5246) in Windows 10, version 1703
- Die TLS_RSA_WITH_RC4_128_SHA in Windows 10, Version 1709
- TLS_RSA_WITH_RC4_128_MD5 in Windows 10, Version 1709

Ab Windows 10, Version 1507 und Windows Server 2016, werden standardmäßig SHA-512-Zertifikate unterstützt werden.

### <a name="rsa-key-changes"></a>RSA-Schlüssel-Änderungen

Fügen Sie Windows 10, Version 1507 und Windows Server 2016 Registrierung-Konfigurationsoptionen für RSA-Schlüsselgröße Client hinzu.

Weitere Informationen finden Sie unter [KeyExchangeAlgorithm - Client-RSA-Schlüsselgröße](tls-registry-settings.md#keyexchangealgorithm---client-rsa-key-sizes).

### <a name="diffie-hellman-key-changes"></a>Diffie-Hellman-Änderungen

Fügen Sie Windows 10, Version 1507 und Windows Server 2016 Registrierung Konfigurationsoptionen für den Diffie-Hellman-Schlüsselgrößen hinzu.

Weitere Informationen finden Sie unter [KeyExchangeAlgorithm - Diffie-Hellman-Schlüsselgrößen](tls-registry-settings.md#keyexchangealgorithm---diffie-hellman-key-sizes).

### <a name="schusestrongcrypto-option-changes"></a>Die Änderungen der SCH_USE_STRONG_CRYPTO

Mit Windows 10, Version 1507 und Windows Server 2016 [SCH_USE_STRONG_CRYPTO](https://msdn.microsoft.com/library/windows/desktop/aa379810.aspx) jetzt deaktiviert NULL, MD5, DES, und Exportieren von Verschlüsselungen.

## <a name="elliptical-curve-changes"></a>Änderungen der elliptischen Kurve

Windows 10, Version 1507 und Windows Server 2016, fügen Sie die Konfiguration der Gruppenrichtlinieneinstellungen für elliptischen Kurven unter Computerkonfiguration > Administrative Vorlagen > Netzwerk > SSL-Konfigurationseinstellungen. Die Liste der Bestellungen für ECC-Kurve gibt die Reihenfolge, in der elliptische Kurven bevorzugt werden, sowie unterstützte Kurven, die nicht aktiviert werden kann. 
 
Die Unterstützung für die folgenden elliptischen Kurven:

- BrainpoolP256r1 (RFC 7027) in Windows 10, Version 1507 und Windows Server 2016
- BrainpoolP384r1 (RFC 7027) in Windows 10, Version 1507 und Windows Server 2016 
- BrainpoolP512r1 (RFC 7027) in Windows 10, Version 1507 und Windows Server 2016
- Curve25519 (RFC Draft-Ietf-Tls-curve25519) in Windows 10, Version 1607 und Windows Server 2016

## <a name="dispatch-level-support-for-sealmessage--unsealmessage"></a>Unterstützung für SealMessage & UnsealMessage senden

Windows 10, Version 1507 und Windows Server 2016 können Sie Unterstützung für SealMessage/UnsealMessage auf Dispatch-Ebene hinzugefügt.

## <a name="dtls-12"></a>DTLS 1.2

Windows 10, Version 1607 und Windows Server 2016 wird Unterstützung für DTLS 1.2 (RFC 6347) hinzufügen.

## <a name="httpsys-thread-pool"></a>HTTP. SYS-Threadpool 

Windows 10, Version 1607 und Windows Server 2016 fügen die Konfiguration der Registrierung der Größe des Threadpools zur Verarbeitung von TLS-Handshakes für HTTP verwendet. SYS.

Registrierungspfad: 

HKLM\SYSTEM\CurrentControlSet\Control\LSA

Um eine maximale Threadpoolgröße pro CPU-Kern anzugeben, erstellen Sie eine **MaxAsyncWorkerThreadsPerCpu** Eintrag. Dieser Eintrag ist nicht standardmäßig in der Registrierung vorhanden. Nachdem Sie den Eintrag erstellt haben, ändern Sie den DWORD-Wert, auf die gewünschte Größe. Wenn nicht konfiguriert, ist die maximal 2 Threads pro CPU-Kern.

## <a name="next-protocol-negotiation-npn-support"></a>Nächste Protocol Negotiation (NPN)-Unterstützung

Ab Windows 10, Version 1703 können weiter Protocol Negotiation (NPN) wurde entfernt und wird nicht mehr unterstützt.

## <a name="pre-shared-key-psk"></a>Vorinstallierter Schlüssel (PSK)

Windows 10, Version 1607 und Windows Server 2016 wird Unterstützung für die PSK-Schlüsselaustauschalgorithmus (RFC 4279) hinzufügen.

Unterstützung für die folgenden PSK-Verschlüsselungssammlungen hinzugefügt:

- TLS_PSK_WITH_AES_128_CBC_SHA256 (RFC 5487) in Windows 10, Version 1607 und Windows Server 2016
- TLS_PSK_WITH_AES_256_CBC_SHA384(RFC 5487) in Windows 10, Version 1607 und Windows Server 2016
- TLS_PSK_WITH_NULL_SHA256 (RFC 5487) in Windows 10, Version 1607 und Windows Server 2016
- TLS_PSK_WITH_NULL_SHA384 (RFC 5487) in Windows 10, Version 1607 und Windows Server 2016
- TLS_PSK_WITH_AES_128_GCM_SHA256 (RFC 5487) in Windows 10, Version 1607 und Windows Server 2016
- TLS_PSK_WITH_AES_256_GCM_SHA384 (RFC 5487) in Windows 10, Version 1607 und Windows Server 2016

## <a name="session-resumption-without-server-side-state-server-side-performance-improvements"></a>-Sitzungswiederaufnahme ohne serverseitigen Zustand serverseitige leistungsverbesserungen

Windows 10, Version 1507 und Windows Server 2016 bieten im Vergleich zu Windows Server 2012 Sitzungstickets 30 % mehr Sitzung Wiederaufnahmen pro Sekunde.

## <a name="session-hash-and-extended-master-secret-extension"></a>Sitzung Hash und erweiterte Master-Secret-Erweiterung

Windows 10, Version 1507 und Windows Server 2016 wird Unterstützung für RFC 7627 hinzugefügt: Transport Layer Security (TLS) Sitzung Hash und Erweiterung der Master-Secret erweitert werden.

Aufgrund dieser Änderung muss Windows 10 und Windows Server 2016 3rd Party [CNG-SSL-Anbieters](https://msdn.microsoft.com/library/windows/desktop/ff468652.aspx) Updates zur Unterstützung von NCRYPT_SSL_INTERFACE_VERSION_3 und um diese neue Schnittstelle zu beschreiben.


## <a name="ssl-support"></a>SSL-Unterstützung

Ab Windows 10, Version 1607 und Windows Server 2016 wird ist die TLS-Client und Server SSL 3.0 standardmäßig deaktiviert. Dies bedeutet, dass wenn die Anwendung oder den Dienst ausdrücklich SSL 3.0, über die SSPI anfordert, der Client wird nie bieten oder akzeptieren Sie SSL 3.0 und der Server wird SSL 3.0 nicht auswählen.

Ab Windows 10, Version 1607 und Windows Server 2016, SSL 2.0 wurde entfernt und wird nicht mehr unterstützt.

## <a name="changes-to-windows-tls-adherence-to-tls-12-requirements-for-connections-with-non-compliant-tls-clients"></a>Änderungen an der Windows-TLS-Einhaltung mit TLS 1.2-Anforderungen für Verbindungen mit nicht kompatiblen TLS-clients

In TLS 1.2, verwendet der Client die ["Signature_algorithms" Erweiterung](https://tools.ietf.org/html/rfc5246#section-7.4.1.4.1) , an den Server anzugeben, welche Signatur bzw. des Hashs Algorithmus-Paare in digitalen Signaturen (d. h. Serverzertifikate und wichtige Exchange Server) verwendet werden können. Der RFC TLS 1.2 erfordert außerdem, dass die Server-Zertifikat-Nachricht "Signature_algorithms" Erweiterung berücksichtigt:

"Wenn der Client eine Erweiterung"Signature_algorithms"bereitgestellt, müssen dann alle Zertifikate, die vom Server durch ein Paar der-Hashsignatur /-Algorithmus, die in diese Erweiterung wird signiert werden."

In der Praxis eine TLS-Clients von Drittanbietern nicht einhalten, die TLS 1.2 RFC und schlagen fehl, alle die Signatur und hash-Algorithmus-Paaren, die sie bereit sind, in der Erweiterung "Signature_algorithms" akzeptiert, oder lassen Sie die Erweiterung vollständig (Letzteres gibt an der Server, dass der Client nur SHA1 mit RSA, DSA und ECDSA unterstützt).

Ein TLS-Server verfügt über häufig nur ein Zertifikat pro Endpunkt, was bedeutet, dass der Server kann nicht immer ein Zertifikat angeben, die den Anforderungen des Clients entspricht konfiguriert.

Vor Windows 10 und Windows Server 2016, den Windows-TLS-Stapel clusterintegritätsrichtlinien streng TLS 1.2-RFC-Anforderungen, Verbindungsfehler Interoperabilitätsprobleme mit RFC-inkonformen TLS-Clients führt. In Windows 10 und Windows Server 2016 die Einschränkungen gelockert werden, und der Server ein Zertifikat, das mit TLS 1.2-RFC, nicht übereinstimmen, die einzige Option für das Serverzertifikat ist senden kann. Der Client kann dann fortsetzen oder Beenden des Handshakes.

Beim Server und Client-Zertifikate zu überprüfen, wird der Windows-TLS-Stapel entspricht genau der RFC TLS 1.2 und lässt nur die ausgehandelte Signatur und Hashalgorithmen, in den Server und Client-Zertifikaten.


