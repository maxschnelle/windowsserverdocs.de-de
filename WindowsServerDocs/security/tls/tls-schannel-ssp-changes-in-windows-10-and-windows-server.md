---
title: TLS (Schannel SSP)
ms.custom: na
ms.prod: windows-server
ms.topic: article
ms.assetid: ebd3c40c-b4c0-4f6d-a00c-f90eda4691df
manager: alanth
author: justinha
ms.technology: security-authentication
ms.date: 05/16/2018
ms.openlocfilehash: e103e985592e6aed150ccd3e1a87e56f19621dbe
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71403389"
---
# <a name="tls-schannel-ssp-changes-in-windows-10-and-windows-server-2016"></a>TLS-Änderungen (Schannel SSP) in Windows 10 und Windows Server 2016

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016 und Windows 10

## <a name="cipher-suite-changes"></a>Verschlüsselungs Sammlungs Änderungen

Windows 10, Version 1511 und Windows Server 2016 fügen Unterstützung für die Konfiguration der Verschlüsselung der Verschlüsselungs Suite mithilfe der Verwaltung mobiler Geräte (Mobile Device Management, MDM) hinzu.

Informationen zu den Änderungen der Prioritäts Reihenfolge der Verschlüsselungs Suite finden Sie unter Verschlüsselungs Sammlungen [in Schannel](https://msdn.microsoft.com/library/windows/desktop/aa374757.aspx).

Unterstützung für die folgenden Verschlüsselungs Sammlungen hinzugefügt:

- TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256 (RFC 5289) in Windows 10, Version 1507 und Windows Server 2016
- TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384 (RFC 5289) in Windows 10, Version 1507 und Windows Server 2016

Disabledbydefault-Änderung für die folgenden Verschlüsselungs Sammlungen:

- TLS_DHE_DSS_WITH_AES_256_CBC_SHA256 (RFC 5246) in Windows 10, Version 1703
- TLS_DHE_DSS_WITH_AES_128_CBC_SHA256 (RFC 5246) in Windows 10, Version 1703
- TLS_DHE_DSS_WITH_AES_256_CBC_SHA (RFC 5246) in Windows 10, Version 1703
- TLS_DHE_DSS_WITH_AES_128_CBC_SHA (RFC 5246) in Windows 10, Version 1703
- TLS_DHE_DSS_WITH_3DES_EDE_CBC_SHA (RFC 5246) in Windows 10, Version 1703
- TLS_RSA_WITH_RC4_128_SHA in Windows 10, Version 1709
- TLS_RSA_WITH_RC4_128_MD5 in Windows 10, Version 1709

Ab Windows 10, Version 1507 und Windows Server 2016, werden SHA 512-Zertifikate standardmäßig unterstützt.

### <a name="rsa-key-changes"></a>RSA-Schlüssel Änderungen

Windows 10, Version 1507 und Windows Server 2016 fügen Sie Registrierungs Konfigurationsoptionen für Client-RSA-Schlüsselgrößen hinzu.

Weitere Informationen finden Sie unter [keyexchangealgorithmus-Client RSA Key sizes](tls-registry-settings.md#keyexchangealgorithm---client-rsa-key-sizes).

### <a name="diffie-hellman-key-changes"></a>Diffie-Hellman-Schlüssel Änderungen

Windows 10, Version 1507 und Windows Server 2016 fügen Sie Registrierungs Konfigurationsoptionen für Diffie-Hellman-Schlüsselgrößen hinzu.

Weitere Informationen finden Sie unter [keyexchangealgorithmus-Diffie-Hellman-Schlüsselgrößen](tls-registry-settings.md#keyexchangealgorithm---diffie-hellman-key-sizes).

### <a name="sch_use_strong_crypto-option-changes"></a>SCH_USE_STRONG_CRYPTO-Optionen ändern

Mit Windows 10, Version 1507 und Windows Server 2016, deaktiviert die [SCH_USE_STRONG_CRYPTO](https://msdn.microsoft.com/library/windows/desktop/aa379810.aspx) -Option jetzt NULL-, MD5-, des-und Export Chiffren.

## <a name="elliptical-curve-changes"></a>Änderungen der elliptischen Kurve

Windows 10, Version 1507 und Windows Server 2016 fügen Gruppenrichtlinie Konfiguration für elliptische Kurven unter Computer Konfiguration > Administrative Vorlagen > Netzwerk > ssl-Konfigurationseinstellungen hinzu. Die ECC-Kurven Reihenfolge gibt die Reihenfolge an, in der elliptische Kurven bevorzugt werden, und ermöglicht unterstützte Kurven, die nicht aktiviert sind. 
 
Unterstützung für die folgenden Ellipsen Kurven hinzugefügt:

- Benannte brainpoolp256r1 (RFC 7027) in Windows 10, Version 1507 und Windows Server 2016
- Benannte brainpoolp384r1 (RFC 7027) in Windows 10, Version 1507 und Windows Server 2016 
- Benannte brainpoolp512r1 (RFC 7027) in Windows 10, Version 1507 und Windows Server 2016
- Curve25519 (RFC Draft-IETF-TLS-Curve25519) in Windows 10, Version 1607 und Windows Server 2016

## <a name="dispatch-level-support-for-sealmessage--unsealmessage"></a>Unterstützung für die Dispatch-Ebene für die versiesagemessage-&

Windows 10, Version 1507 und Windows Server 2016 fügen Unterstützung für "versiesagemessage/unversiesagemessage" auf dispatchebene hinzu.

## <a name="dtls-12"></a>DTLS 1,2

Windows 10, Version 1607 und Windows Server 2016, Unterstützung für DTLS 1,2 (RFC 6347) hinzufügen.

## <a name="httpsys-thread-pool"></a>HTTP. SYS-Thread Pool 

Windows 10, Version 1607 und Windows Server 2016 fügen Sie die Registrierungs Konfiguration der Größe des Thread Pools hinzu, der zum Verarbeiten von TLS-Handshakes für HTTP verwendet wird. Einsetzt.

Registrierungs Pfad: 

HKLM\System\CurrentControlSet\Control\LSA

Um eine maximale Thread Pool Größe pro CPU-Kern anzugeben, erstellen Sie einen **maxasyncworkerthreadspercpu** -Eintrag. Dieser Eintrag ist nicht standardmäßig in der Registrierung vorhanden. Nachdem Sie den Eintrag erstellt haben, ändern Sie den DWORD-Wert in die gewünschte Größe. Wenn nicht konfiguriert, beträgt der Höchstwert 2 Threads pro CPU-Kern.

## <a name="next-protocol-negotiation-npn-support"></a>Unterstützung der nächsten Protokoll Aushandlung (NPN)

Ab Windows 10, Version 1703, wurde die nächste Protokoll Verhandlung (NPN) entfernt und wird nicht mehr unterstützt.

## <a name="pre-shared-key-psk"></a>Vorinstaltzter Schlüssel (PSK)

Windows 10, Version 1607 und Windows Server 2016 fügen Unterstützung für den PSK-Schlüsselaustausch Algorithmus (RFC 4279) hinzu.

Unterstützung für die folgenden PSK-Verschlüsselungs Sammlungen hinzugefügt:

- TLS_PSK_WITH_AES_128_CBC_SHA256 (RFC 5487) in Windows 10, Version 1607 und Windows Server 2016
- TLS_PSK_WITH_AES_256_CBC_SHA384 (RFC 5487) in Windows 10, Version 1607 und Windows Server 2016
- TLS_PSK_WITH_NULL_SHA256 (RFC 5487) in Windows 10, Version 1607 und Windows Server 2016
- TLS_PSK_WITH_NULL_SHA384 (RFC 5487) in Windows 10, Version 1607 und Windows Server 2016
- TLS_PSK_WITH_AES_128_GCM_SHA256 (RFC 5487) in Windows 10, Version 1607 und Windows Server 2016
- TLS_PSK_WITH_AES_256_GCM_SHA384 (RFC 5487) in Windows 10, Version 1607 und Windows Server 2016

## <a name="session-resumption-without-server-side-state-server-side-performance-improvements"></a>Sitzungs Wiederaufnahme ohne serverseitige Verbesserung der serverseitigen Leistung

Windows 10, Version 1507 und Windows Server 2016 bieten im Vergleich zu Windows Server 2012 30% mehr Sitzungs fortläufe pro Sekunde mit Sitzungs Tickets.

## <a name="session-hash-and-extended-master-secret-extension"></a>Sitzungs Hash und erweiterte Erweiterung für den geheimen Hauptschlüssel

Windows 10, Version 1507 und Windows Server 2016, Unterstützung für RFC 7627 hinzufügen: Transport Layer Security (TLS)-Sitzungs Hash und erweiterte Erweiterung für den geheimen Hauptschlüssel.

Aufgrund dieser Änderung sind für Windows 10 und Windows Server [2016 Updates von Drittanbietern](https://msdn.microsoft.com/library/windows/desktop/ff468652.aspx) erforderlich, um NCRYPT_SSL_INTERFACE_VERSION_3 zu unterstützen und diese neue Schnittstelle zu beschreiben.


## <a name="ssl-support"></a>SSL-Unterstützung

Ab Windows 10, Version 1607 und Windows Server 2016, sind der TLS-Client und der Server-SSL 3,0 standardmäßig deaktiviert. Dies bedeutet, dass der Client nicht SSL 3,0 anbietet oder akzeptiert, es sei denn, die Anwendung oder der Dienst fordert SSL 3,0 über die SSPI an, und der Server wählt niemals SSL 3,0 aus.

Ab Windows 10, Version 1607 und Windows Server 2016, wurde SSL 2,0 entfernt und wird nicht mehr unterstützt.

## <a name="changes-to-windows-tls-adherence-to-tls-12-requirements-for-connections-with-non-compliant-tls-clients"></a>Änderungen an der Windows TLS-Einhaltung der TLS 1,2-Anforderungen für Verbindungen mit nicht kompatiblen TLS-Clients

In TLS 1,2 verwendet der Client die [Erweiterung "signature_algorithms"](https://tools.ietf.org/html/rfc5246#section-7.4.1.4.1) , um dem Server mitzuteilen, welche Signatur-/Hashalgorithmus-Paare in digitalen Signaturen (d. h. Server Zertifikate und Server Schlüsselaustausch) verwendet werden können. Die TLS 1,2-RFC erfordert auch, dass die Serverzertifikat Nachricht die Erweiterung "signature_algorithms" berücksichtigt:

"Wenn der Client eine" signature_algorithms "-Erweiterung bereitgestellt hat, müssen alle vom Server bereitgestellten Zertifikate von einem Hash-/signaturalgorithmuspaar signiert werden, das in dieser Erweiterung angezeigt wird."

In der Praxis stimmen einige TLS-Clients von Drittanbietern nicht mit TLS 1,2 RFC überein und können nicht alle Signatur-und Hash Algorithmus-Paare einschließen, die Sie in der Erweiterung "signature_algorithms" akzeptieren möchten, oder die Erweiterung weglassen (letzteres gibt an der Server, den der Client nur SHA1 mit RSA, DSA oder ECDSA unterstützt.

Ein TLS-Server verfügt häufig nur über ein Zertifikat, das pro Endpunkt konfiguriert ist. Dies bedeutet, dass der Server nicht immer ein Zertifikat bereitstellen kann, das die Anforderungen des Clients erfüllt.

Vor Windows 10 und Windows Server 2016 hat der Windows TLS-Stapel streng den TLS 1,2 RFC-Anforderungen gerecht, was zu Verbindungsfehlern mit nicht kompatiblen RFC-Clients und Interoperabilitätsproblemen führt. In Windows 10 und Windows Server 2016 werden die Einschränkungen gelockert, und der Server kann ein Zertifikat senden, das nicht mit TLS 1,2 RFC übereinstimmt, wenn dies die einzige Option des Servers ist. Der Client kann dann den Hand Shake Vorgang fortsetzen oder beenden.

Beim Validieren von Server-und Client Zertifikaten erfüllt der Windows TLS-Stapel streng die TLS 1,2-RFC und lässt nur die ausgehandelte Signatur und die Hash Algorithmen in den Server-und Client Zertifikaten zu.


