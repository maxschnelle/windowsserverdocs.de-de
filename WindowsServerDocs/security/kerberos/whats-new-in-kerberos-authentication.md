---
title: Neues bei der Kerberosauthentifizierung
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: 7bd17803-6e42-4a3b-803f-e47c74725813
manager: alanth
author: justinha
ms.technology: security-authentication
ms.date: 11/09/2016
ms.openlocfilehash: 7b046490c606cdf9e1436f503bf46a9cd4280ea9
ms.sourcegitcommit: 2782a80a916f8432c030af76e860a72f08481899
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/13/2018
---
# <a name="whats-new-in-kerberos-authentication"></a>Neues bei der Kerberosauthentifizierung

>Gilt für: Windows Server 2016 und Windows10

## <a name="kdc-support-for-public-key-trust-based-client-authentication"></a>KDC-Unterstützung für öffentliche Schlüssel vertrauen basierenden Client-Authentifizierung

Beginnend mit Windows Server2016 unterstützt KDCs eine Möglichkeit, öffentliche Schlüssel zuordnen. Wenn der öffentliche Schlüssel für ein Konto bereitgestellt wird, unterstützt das KDC Kerberos PKInit explizit mit diesem Schlüssel. Da es keine Überprüfung des Zertifikats ist, selbstsignierte Zertifikate werden unterstützt, und zur Authentifizierungsmechanismussicherung wird nicht unterstützt.

Schlüssel vertrauen wird bevorzugt, wenn für ein Konto unabhängig von der Einstellung UseSubjectAltName konfiguriert.

## <a name="kerberos-client-and-kdc-support-for-rfc-8070-pkinit-freshness-extension"></a>Kerberos-Client und KDC-Support für RFC 8070 PKInit Aktualität Erweiterung

Ab Windows10, Version 1607 und Windows Server2016, Kerberos-Clients versuchen den [RFC 8070 PKInit Aktualität Erweiterung](https://datatracker.ietf.org/doc/draft-ietf-kitten-pkinit-freshness/) für öffentlicher Schlüssel Anmeldungen basierte. 

Ab Windows Server2016, können die PKInit Aktualität Erweiterung KDCs unterstützen. In der Standardeinstellung bieten KDCs nicht die Aktualität PKInit-Erweiterung. Verwenden Sie zum Aktivieren der neuen KDC-Unterstützung für PKInit Aktualität Erweiterung KDC administrative Vorlage-Einstellung für alle Domänencontroller in der Domäne ein. Wenn konfiguriert ist, werden die folgenden Optionen unterstützt, wenn die Domäne Windows Server2016-Domänenfunktionsebene (DFL) ist:

- **Deaktivierte**: das KDC nie bietet die Erweiterung PKInit Aktualität und gültige Authentifizierungsanforderungen ohne Überprüfung auf Aktualität akzeptiert. Benutzer erhalten die neue öffentliche Schlüssel Identität SID nie.
- **Unterstützt**: PKInit Aktualität Erweiterung wird auf Anforderung unterstützt. Kerberos-Clients erfolgreich mit der Erweiterung der PKInit Aktualität Authentifizierung erhalten die neue öffentliche Schlüssel Identität SID.
- **Erforderliche**: PKInit Aktualität-Erweiterung für die erfolgreiche Authentifizierung erforderlich ist. Kerberos-Clients, die nicht die PKInit Aktualität Erweiterung tritt immer bei public Key-Anmeldeinformationen verwenden.

## <a name="domain-joined-device-support-for-authentication-using-public-key"></a>Unterstützung für Geräte Domäne für die Authentifizierung mit öffentlichen Schlüssel

Mit Windows10, Version 1507 und Windows Server2016 ab, wenn eine Domäne eingebundenen Gerät seinen gebundenen öffentlichen Schlüssel mit einem Windows Server2016-Domänencontroller (DC) registrieren kann, kann das Gerät dann mit dem öffentlichen Schlüssel mithilfe von Kerberos-Authentifizierung auf einem Windows Server2016-Domänencontroller authentifizieren. Weitere Informationen finden Sie unter [Domäne öffentlichen Schlüssel Geräteauthentifizierung](Domain-joined-Device-Public-Key-Authentication.md)

## <a name="kerberos-clients-allow-ipv4-and-ipv6-address-hostnames-in-service-principal-names-spns"></a>Kerberos-Clients zulassen IPv4 und IPv6-Adresse Hostnamen in Service Principal Names (SPNs)

Ab Windows10, Version 1507 und Windows Server2016, können Kerberos-Clients konfiguriert werden, um IPv4 und IPv6-Hostnamen in Dienstprinzipalnamen (SPN) zu unterstützen. 

Registrierungspfad:

HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System\Kerberos\Parameters

Zum Konfigurieren der Unterstützung für die IP-Adresse Hostnamen in Dienstprinzipalnamen (SPN), erstellen Sie einen Eintrag TryIPSPN. Dieser Eintrag ist nicht standardmäßig in der Registrierung vorhanden. Nachdem Sie den Eintrag erstellt haben, ändern Sie den DWORD-Wert in 1. Wenn nicht konfiguriert ist, werden IP-Adresse Hostnamen nicht versucht.

Wenn der SPN in Active Directory registriert ist, ist die Authentifizierung mit Kerberos erfolgreich. 

## <a name="kdc-support-for-key-trust-account-mapping"></a>KDC-Unterstützung für Kontenzuordnung Schlüssel vertrauen

Ab Windows Server2016, bieten Domänencontroller Unterstützung für Kontenzuordnung Schlüssel vertrauen sowie Fallback auf vorhandene AltSecID und Benutzerprinzipalname (UPN) im SAN-Verhalten. Wenn UseSubjectAltName festgelegt ist:

- 0: explizite Zuordnung ist erforderlich. Und es entweder muss:
    - Schlüssel vertrauen (neu in Windows Server2016)
    - ExplicitAltSecID
- 1: implizite Zuordnung zulässig ist (Standard):
    1. Wenn Schlüssel vertrauen für Konto konfiguriert ist, wird es für die Zuordnung (neu mit Windows Server2016) verwendet.
    2. Wenn es kein Benutzerprinzipalname im SAN ist, AltSecID für die Zuordnung versucht.
    3. Wenn in das SAN ein UPN vorhanden ist, wird UPN für die Zuordnung versucht.

## <a name="see-also"></a>Siehe auch

- [Kerberos-Authentifizierung: Übersicht](kerberos-authentication-overview.md)
