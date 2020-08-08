---
title: What's New in Kerberos Authentication
ms.topic: article
ms.assetid: 7bd17803-6e42-4a3b-803f-e47c74725813
manager: alanth
author: justinha
ms.date: 11/09/2016
ms.openlocfilehash: 514b19689c73c1c5c61184a1ff8c13636b57864e
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87948663"
---
# <a name="whats-new-in-kerberos-authentication"></a>What's New in Kerberos Authentication

>Gilt für: Windows Server 2016 und Windows 10

## <a name="kdc-support-for-public-key-trust-based-client-authentication"></a>KDC-Unterstützung für vertrauenswürdige Authentifizierung mit öffentlichem Schlüssel

Ab Windows Server 2016 unterstützen KDCs eine Zuordnung von öffentlichen Schlüsseln.
Wenn der öffentliche Schlüssel für ein Konto bereitgestellt wird, unterstützt der KDC Kerberos PKINIT explizit mithilfe des Schlüssels.
Da keine Zertifikat Validierung vorhanden ist, werden selbst signierte Zertifikate unterstützt, und die Authentifizierungsmechanismen werden nicht unterstützt.

Die Schlüssel Vertrauensstellung wird bevorzugt, wenn Sie für ein Konto unabhängig von der Einstellung "Einstellung für" "Einstellung" "von" Einstellung "

## <a name="kerberos-client-and-kdc-support-for-rfc-8070-pkinit-freshness-extension"></a>Kerberos-Client und KDC-Unterstützung für RFC 8070 PKINIT-Erweiterung

Ab Windows 10, Version 1607 und Windows Server 2016, versuchen die Kerberos-Clients, die [RFC 8070 PKINIT-Erweiterung](https://datatracker.ietf.org/doc/draft-ietf-kitten-pkinit-freshness/) für Anmeldungen mit öffentlichem Schlüssel zu registrieren.

Ab Windows Server 2016 können KDCs die Erweiterung PKINIT-Aktualität unterstützen.
Standardmäßig bieten KDCs keine PKINIT-Aktualität-Erweiterung. Um es zu aktivieren, verwenden Sie die neue KDC-Unterstützung für die administrative Vorlage für die administrative Vorlage für die PKINIT-Erweiterung für alle DCS in der Domäne.
Bei der Konfiguration werden die folgenden Optionen unterstützt, wenn die Domäne Windows Server 2016-Domänen Funktionsebene (DFL) ist:

- **Deaktiviert**: der KDC bietet die PKINIT-Erweiterung nie an und akzeptiert gültige Authentifizierungsanforderungen, ohne auf Aktualität zu prüfen. Benutzer erhalten nie die neue Identität der öffentlichen Schlüssel Identität.
- **Unterstützt**: PKINIT-Erweiterungen werden auf Anforderung unterstützt. Kerberos-Clients, die sich erfolgreich bei der PKINIT-Erweiterung authentifizieren, erhalten die aktuelle SID der öffentlichen Schlüssel Identität.
- **Erforderlich**: PKINIT-Erweiterung ist für die erfolgreiche Authentifizierung erforderlich. Kerberos-Clients, die die PKINIT-Erweiterung nicht unterstützen, schlagen immer fehl, wenn Anmelde Informationen für öffentliche Schlüssel verwendet werden.

## <a name="domain-joined-device-support-for-authentication-using-public-key"></a>Unterstützung von in die Domäne eingebundenen Geräten für die Authentifizierung mit öffentlichem Schlüssel

Ab Windows 10, Version 1507 und Windows Server 2016, kann das Gerät mithilfe der Kerberos-Authentifizierung bei einem Windows Server 2016-DC mit dem öffentlichen Schlüssel authentifiziert werden, wenn ein in eine Domäne eingebundenes Gerät seinen gebundenen öffentlichen Schlüssel bei einem Windows Server 2016-Domänen Controller (DC) registrieren kann. Weitere Informationen finden Sie unter [Authentifizierung mit öffentlichem Schlüssel für den Domänen Beitritt](Domain-joined-Device-Public-Key-Authentication.md) .

## <a name="kerberos-clients-allow-ipv4-and-ipv6-address-hostnames-in-service-principal-names-spns"></a>Kerberos-Clients lassen IPv4-und IPv6-Adress Hostnamen in Dienst Prinzipal Namen (SPNs) zu.

Ab Windows 10, Version 1507 und Windows Server 2016, können Kerberos-Clients für die Unterstützung von IPv4-und IPv6-Hostnamen in SPNs konfiguriert werden.

Registrierungspfad:

Hklm\software\microsoft\windows\currentversion\policies\system\kerberos\parameters

Erstellen Sie einen tryipspn-Eintrag, um die Unterstützung für IP-Adress Hostnamen in SPNs zu konfigurieren.
Dieser Eintrag ist nicht standardmäßig in der Registrierung vorhanden.
Nachdem Sie den Eintrag erstellt haben, ändern Sie den DWORD-Wert in 1.
Wenn diese Eigenschaft nicht konfiguriert ist, wird nicht versucht, die Hostnamen der IP-Adressen

Wenn der SPN in Active Directory registriert ist, ist die Authentifizierung mit Kerberos erfolgreich.

Weitere Informationen finden Sie im Dokument [Konfigurieren von Kerberos für IP-Adressen](configuring-kerberos-over-ip.md).

## <a name="kdc-support-for-key-trust-account-mapping"></a>KDC-Unterstützung für die Zuordnung von Schlüssel Vertrauens Konten

Ab Windows Server 2016 haben Domänen Controller Unterstützung für die Zuordnung von Schlüssel vertrauenswürdigen Konten sowie für das Fall Back auf vorhandene AltSecId und den Benutzer Prinzipal Namen (User Principal Name, UPN) im San-Verhalten. Wenn "" für "\esubjectaltname" auf festgelegt ist:

- 0: eine explizite Zuordnung ist erforderlich. Dann muss Folgendes vorhanden sein:
    - Schlüssel Vertrauensstellung (neu mit Windows Server 2016)
    - Explizitl
- 1: implizite Zuordnung ist zulässig (Standard):
    1. Wenn die Schlüssel Vertrauensstellung für das Konto konfiguriert ist, wird Sie für die Zuordnung verwendet (neu mit Windows Server 2016).
    2. Wenn kein UPN im San vorhanden ist, wird für die Zuordnung von "AltSecId" versucht.
    3. Wenn ein UPN im San vorhanden ist, wird ein UPN-Wert für die Zuordnung versucht.

## <a name="see-also"></a>Weitere Informationen

- [Kerberos Authentication Overview](kerberos-authentication-overview.md)
