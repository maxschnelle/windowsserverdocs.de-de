---
title: Neuerungen bei der Kerberosauthentifizierung
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: 7bd17803-6e42-4a3b-803f-e47c74725813
manager: alanth
author: justinha
ms.technology: security-authentication
ms.date: 11/09/2016
ms.openlocfilehash: 7b046490c606cdf9e1436f503bf46a9cd4280ea9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59831091"
---
# <a name="whats-new-in-kerberos-authentication"></a>What's New in Kerberos Authentication

>Gilt für: WindowsServer 2016 und Windows 10

## <a name="kdc-support-for-public-key-trust-based-client-authentication"></a>KDC-Unterstützung für öffentliche Schlüssel vertrauen-basierte Clientauthentifizierung

Ab Windows Server 2016 unterstützen KDCs eine Möglichkeit zum öffentlichen Schlüssel zuordnen. Wenn der öffentliche Schlüssel für ein Konto bereitgestellt wird, klicken Sie dann unterstützt das KDC Kerberos PKInit explizit mit diesem Schlüssel. Da keine Überprüfung des Zertifikats ist, selbstsignierte Zertifikate verwendet werden, und authentifizierungsmechanismuszusicherung wird nicht unterstützt.

Schlüsselbasierte Vertrauensstellung wird bevorzugt, wenn für ein Konto, unabhängig von der Einstellung UseSubjectAltName konfiguriert.

## <a name="kerberos-client-and-kdc-support-for-rfc-8070-pkinit-freshness-extension"></a>Kerberos-Client und KDC-Unterstützung für RFC 8070 PKInit Aktualität-Erweiterung

Ab Windows 10, Version 1607 und Windows Server 2016 können Kerberos-Clients versuchen den [RFC 8070 PKInit Aktualität Erweiterung](https://datatracker.ietf.org/doc/draft-ietf-kitten-pkinit-freshness/) für öffentlichen Schlüssel auf Anmeldungen basieren. 

Ab Windows Server 2016 können KDCs PKInit Aktualität Erweiterung unterstützen. KDCs in der Standardeinstellung keine PKInit Aktualität Erweiterung angeboten. Verwenden Sie die neue KDC-Unterstützung für PKInit Aktualität Erweiterung KDC administrative Vorlage der richtlinieneinstellung auf alle Domänencontroller in der Domäne, um sie zu aktivieren. Wenn konfiguriert, werden die folgenden Optionen unterstützt, wenn die Domäne auf Windows Server 2016-Domänenfunktionsebene (DFL) ist:

- **Deaktiviert**: Das KDC die PKInit Aktualität-Erweiterung bietet und gültige authentifizierungsanforderungen akzeptiert, ohne eine Überprüfung auf Aktualität nie. Benutzer erhalten die neue öffentliche Schlüssel Identität SID nie.
- **Unterstützt**: PKInit Aktualität Erweiterung wird auf Anforderung unterstützt. Kerberos-Clients, die mit der Erweiterung der PKInit Aktualität erfolgreich authentifizieren, erhalten die neue öffentliche Schlüssel Identität SID.
- **Erforderlich**: PKInit Aktualität Erweiterung ist für eine erfolgreiche Authentifizierung erforderlich. Kerberos-Clients, die nicht die Erweiterung der PKInit Aktualität unterstützen schlägt immer fehl, wenn Sie Anmeldeinformationen für den öffentliche Schlüssel zu verwenden.

## <a name="domain-joined-device-support-for-authentication-using-public-key"></a>Zur Domäne gehörenden Gerät-Unterstützung für die Authentifizierung mit öffentlichen Schlüssel

Mit Windows 10 Version 1507 und Windows Server 2016 ab, wenn eine Domäne eingebundenes Gerät gebundenen öffentlichen Schlüssel mit einem Windows Server 2016-Domänencontroller (DC) registrieren kann, kann dann das Gerät mit dem öffentlichen Schlüssel, die mithilfe von Kerberos-Authentifizierung authentifiziert werden ein Windows Server 2016-Domänencontroller. Weitere Informationen finden Sie unter [Domäne öffentliche Schlüssel Geräteauthentifizierung](Domain-joined-Device-Public-Key-Authentication.md)

## <a name="kerberos-clients-allow-ipv4-and-ipv6-address-hostnames-in-service-principal-names-spns"></a>Kerberos-Clients zulassen IPv4 und IPv6-Adresse-Hostnamen in Service Principal Names (SPNs)

Ab Windows 10 Version 1507 und Windows Server 2016, können Kerberos-Clients konfiguriert werden, zur Unterstützung von IPv4 und IPv6-Hostnamen in SPNs. 

Registrierungspfad:

HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System\Kerberos\Parameters

Erstellen Sie einen TryIPSPN-Eintrag, um Unterstützung für IP-Adresse Hostnamen in SPNs zu konfigurieren. Dieser Eintrag ist nicht standardmäßig in der Registrierung vorhanden. Nachdem Sie den Eintrag erstellt haben, ändern Sie den DWORD-Wert auf 1 fest. Nicht konfiguriert, werden IP-Adresse Hostnamen nicht versucht.

Wenn der SPN in Active Directory registriert ist, ist die Authentifizierung mit Kerberos erfolgreich. 

## <a name="kdc-support-for-key-trust-account-mapping"></a>KDC-Unterstützung für Schlüsselbasierte Vertrauensstellung kontozuordnung

Ab Windows Server 2016 verfügen Domänencontroller-Unterstützung für Schlüsselbasierte Vertrauensstellung kontozuordnung als auch für Fallback auf vorhandene AltSecID und UPN (User Principal Name, Benutzerprinzipalname) in das SAN-Verhalten. Wenn UseSubjectAltName auf festgelegt ist:

- 0: Explizite Zuordnung ist erforderlich. Klicken Sie dann muss es entweder:
    - Schlüsselbasierte Vertrauensstellung (neu in Windows Server 2016)
    - ExplicitAltSecID
- 1: Implizite Zuordnung ist (Standard) zulässig:
    1. Wenn Schlüsselbasierte Vertrauensstellung für Konto konfiguriert ist, wird es für die Zuordnung (neu in Windows Server 2016) verwendet.
    2. Wenn kein UPN in das SAN vorhanden ist, wird der AltSecID für die Zuordnung versucht.
    3. Wenn es sich bei ein UPN im SAN vorhanden ist, wird der UPN für die Zuordnung versucht.

## <a name="see-also"></a>Siehe auch

- [Übersicht über die Kerberos-Authentifizierung](kerberos-authentication-overview.md)
