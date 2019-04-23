---
title: 'Windows-Authentifizierung: Übersicht'
description: Windows Server-Sicherheit
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-windows-auth
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 485a0774-0785-457f-a964-0e9403c12bb1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 2021ccf1e0015cc910f43966f9400e6bd56a230c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59870971"
---
# <a name="windows-authentication-overview"></a>Windows-Authentifizierung: Übersicht

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

In diesem Navigationsthema für IT-Experten sind Dokumentationsressourcen für Technologien zur Windows-Authentifizierung und -Anmeldung aufgeführt, die Produktbewertungen, "Erste Schritte"-Handbücher, Verfahren, Entwurfs- und Bereitstellungshandbücher, technische Referenzen und Befehlsverzeichnisse enthalten.

## <a name="feature-description"></a>Featurebeschreibung
Authentifizierung ist der Vorgang, durch den die Identität eines Objekts, eines Dienstes oder einer Person überprüft wird. Ziel der Authentifizierung eines Objekts ist es, sicherzustellen, dass das Objekt echt und unverfälscht ist. Beim Authentifizieren eines Diensts oder einer Person ist das Ziel, sicherzustellen, dass die vorgelegten Anmeldeinformationen authentisch sind.

Im Netzwerkkontext dient die Authentifizierung dazu, die Identität gegenüber einer Netzwerkanwendung oder -ressource nachzuweisen. Identität ist in der Regel durch einen kryptografischen Vorgang nachgewiesen, die entweder einen Schlüssel, den nur von der Benutzer bekannt sind verwendet – wie bei der Kryptografie mit öffentlichem Schlüssel- oder ein vorinstallierter Schlüssel. Auf der Serverseite der Authentifizierungskommunikation werden die signierten Daten mit einem bekannten Kryptografieschlüssel verglichen, um den Authentifizierungsversuch zu überprüfen.

Durch die Speicherung der Kryptografieschlüssel an einem zentralen Ort wird der Authentifizierungsvorgang skalierbar und verwaltbar. Active Directory-Domänendienste sind die empfohlene und standardmäßig verwendete Technologie zum Speichern von Identitätsinformationen \(einschließlich der Kryptografieschlüssel, die die Anmeldeinformationen des Benutzers sind\). Active Directory ist für Standardimplementierungen von Kerberos und NTLM erforderlich.

Authentifizierungstechniken reichen von der einfachen Anmeldung, die Benutzern basierend auf etwas, das nur der Benutzer weiß – z. B. ein Kennwort zu leistungsfähigeren Sicherheitsmechanismen, die etwas verwenden, denen der Benutzer - wie-Token, Zertifikate mit öffentlichen Schlüsseln, identifiziert und Biometrie. In einer Unternehmensumgebung ist es Diensten oder Benutzern eventuell möglich, auf unterschiedliche Anwendungen oder Ressourcen auf verschiedenen Arten von Servern an einem einzigen Standort oder auch standortübergreifend zugreifen. Aus diesem Grund muss die Authentifizierung Umgebungen unterstützen, die auf anderen Plattformen und anderen Windows-Betriebssystemen basieren.

Das Windows-Betriebssystem implementiert einen Standardsatz von Authentifizierungsprotokollen Kerberos, NTLM, Transport Layer Security\/Secure Sockets Layer \(TLS\/SSL\), und Digest als Teil einer erweiterbare Architektur. Darüber hinaus werden einige Protokolle zu Authentifizierungspaketen zusammengefasst, beispielsweise Negotiate und der Credential Security Support Provider. Mit diesen Protokollen und Paketen können Benutzer, Computer und Dienste authentifiziert werden. Der Authentifizierungsprozess wiederum ermöglicht Benutzern und Diensten einen sicheren Zugriff auf Ressourcen.

Weitere Informationen zur Windows-Authentifizierung einschließlich der Aspekte

-   [Windows-Authentifizierungskonzepte](windows-authentication-concepts.md)

-   [Windows-Anmeldeszenarios](windows-logon-scenarios.md)

-   [Architektur der Windows-Authentifizierung](windows-authentication-architecture.md)

-   [Sicherheitsarchitektur für die Schnittstelle von Support-Anbieter](security-support-provider-interface-architecture.md)

-   [Anmeldeinformationen-Prozesse bei der Windows-Authentifizierung](credentials-processes-in-windows-authentication.md)

-   [Gruppenrichtlinien Sie bei der Windows-Authentifizierung verwendete](group-policy-settings-used-in-windows-authentication.md)

finden Sie unter den [technische Übersicht über Windows-Authentifizierung](windows-authentication-technical-overview.md).

## <a name="practical-applications"></a>Praktische Anwendungsfälle
Mithilfe der Windows-Authentifizierung wird überprüft, ob die Informationen von einer vertrauenswürdigen Quelle stammen, ungeachtet dessen, ob es sich um eine Person oder ein Computerobjekt, beispielsweise einen anderen Computer, handelt. Windows stellt viele verschiedene Methoden bereit, um dies zu erreichen. Im Folgenden werden diese Methoden beschrieben.

|An...|Feature|Beschreibung|
|----|------|--------|
|Authentifizieren innerhalb einer Active Directory-Domäne|Kerberos|Die Microsoft Windows&nbsp;Server-Betriebssysteme implementieren das Authentifizierungsprotokoll Kerberos Version 5 und Erweiterungen für die Authentifizierung mit öffentlichem Schlüssel. Die Kerberos-Authentifizierungsclient wird als Security Support Provider implementiert \(SSP\) und zugegriffen werden kann, über die Security Support Provider Interface \(SSPI\). Die Erstauthentifizierung von Benutzern ist das einmaligen Anmelden von Windows-Anmeldung integriert\-Architektur. Das Kerberos-Schlüsselverteilungscenter \(KDC\) andere auf dem Domänencontroller unter Windows Server-Sicherheitsdienste integriert ist. Das KDC verwendet die Datenbank des der Domäne Active Directory-Dienst als Sicherheitskontendatenbank. Active Directory ist für Standardimplementierungen von Kerberos erforderlich.<br /><br />Weitere Ressourcen finden Sie unter [Kerberos-Authentifizierung: Übersicht](../kerberos/kerberos-authentication-overview.md).|
|Sichere Authentifizierung im Web|TLS\/SSL im Schannel Security Support Provider implementiert|Die Transport Layer Security \(TLS\) Versionen 1.0, 1.1 und 1.2, Secure Sockets Layer-Protokoll \(SSL\) Protokoll, Version 2.0 und 3.0, Datagram Transport Layer Security Protocol, Version 1.0 und die Private Kommunikationstransport \(PCT\) Protokoll, Version 1.0, basieren auf Kryptografie mit öffentlichem Schlüssel. Das Secure Channel \(Schannel\) Anbieter-authentifizierungsprotokollsammlung enthält diese Protokolle. Alle Schannel-Protokolle verwenden ein Client- und Servermodell.<br /><br />Weitere Ressourcen finden Sie unter [TLS – SSL &#40;Schannel-SSP&#41; Übersicht](../tls/tls-ssl-schannel-ssp-overview.md).|
|Authentifizieren bei einem Webdienst oder einer Anwendung|Integrierte Windows-Authentifizierung<br /><br />Digestauthentifizierung|Weitere Ressourcen finden Sie unter [integrierte Windows-Authentifizierung](https://technet.microsoft.com/library/cc758557(v=WS.10).aspx) und [Digestauthentifizierung](https://technet.microsoft.com/library/cc738318(v=ws.10).aspx), und [erweiterte Digestauthentifizierung](https://technet.microsoft.com/library/cc783131(v=ws.10).aspx).|
|Authentifizieren bei älteren Anwendungen|NTLM|NTLM ist eine Herausforderung\-Antwort Style-Authentifizierungsprotokoll. Zusätzlich zur Authentifizierung bietet das NTLM-Protokoll optional für die sitzungssicherheit – insbesondere Nachrichtenintegrität und Vertraulichkeit durch Signatur und Versiegelung von Funktionen in NTLM.<br /><br />Weitere Ressourcen finden Sie unter [NTLM: Übersicht](../kerberos/ntlm-overview.md).|
|Nutzen der mehrstufigen Authentifizierung|Unterstützung von Smartcards<br /><br />Biometrie-Unterstützung|Smartcards sind eine Manipulationen\-Schutz vor Angriffen und Transportable Möglichkeit zum Bereitstellen von sicherheitslösungen für Aufgaben wie Clientauthentifizierung, Anmeldung bei Domänen, code, Signieren und Schützen von e\--e-Mails.<br /><br />Bei der Biometrie wird ein unveränderliches physisches Merkmal einer Person erfasst, um diese Person eindeutig identifizieren zu können. Fingerabdrücke gehören zu den am häufigsten genutzten biometrischen Merkmalen, weshalb Millionen PCs und Peripheriegeräte mit biometrischen Fingerabdrucklesern ausgestattet sind.<br /><br />Weitere Ressourcen finden Sie unter [technische Referenz zu Smartcards](https://technet.microsoft.com/itpro/windows/keep-secure/smart-card-windows-smart-card-technical-reference). |
|Bereitstellen der lokalen Verwaltung, Speicherung und Wiederverwendung von Anmeldeinformationen|Verwaltung von Anmeldeinformationen<br /><br />Lokale Sicherheitsautorität<br /><br />Kennwörter|Durch die Verwaltung von Anmeldeinformationen in Windows wird sichergestellt, Anmeldeinformationen sicher gespeichert werden. Anmeldeinformationen werden auf dem sicheren Desktop erfasst \(für den Zugriff für lokales oder Domänenbenutzerkonto\), über apps oder Websites, damit die richtigen Anmeldeinformationen vorgelegt werden jedes Mal, wenn eine Ressource zugegriffen wird.<br /><br />
|Erweitern des Authentifizierungsschutzes auf Legacysysteme|Erweiterter Schutz für Authentifizierung|Diese Funktion verbessert den Schutz und die Handhabung von Anmeldeinformationen bei der Authentifizierung von Netzwerkverbindungen mit integrierter Windows-Authentifizierung \(IWA\).|

## <a name="software-requirements"></a>Softwareanforderungen
Die Windows-Authentifizierung ist so konzipiert, dass sie mit früheren Versionen des Windows-Betriebssystem kompatibel ist. Verbesserungen in einer neuen Version stehen jedoch nicht notwendigerweise auch in früheren Versionen zur Verfügung. Weitere Informationen finden Sie in der Dokumentation zu den verschiedenen Features.

## <a name="server-manager-information"></a>Informationen zum Server-Manager
Viele Authentifizierungsfeatures können mit der Gruppenrichtlinie konfiguriert werden, die mithilfe des Server-Managers installiert werden kann. Das Windows-Biometrieframework wird mithilfe des Server-Managers installiert. Andere Serverrollen, die abhängig von der Authentifizierungsmethoden, z. B. Webserver sind \(IIS\) und Active Directory Domain Services kann auch mithilfe von Server-Manager installiert werden.

## <a name="related-resources"></a>Verwandte Ressourcen

|Authentifizierungstechnologien|Ressourcen|
|----------------|-------|
|Windows-Authentifizierung|[Technische Übersicht über Windows-Authentifizierung](../windows-authentication/windows-authentication-technical-overview.md)<br />Enthält Themen, die Unterschiede zwischen Versionen, allgemeine Authentifizierungskonzepte, Anmeldeszenarios, Architekturen für unterstützte Versionen und geeignete Einstellungen adressiert.|
|Kerberos|[Übersicht über die Kerberos-Authentifizierung](../kerberos/kerberos-authentication-overview.md)<br /><br />[Eingeschränkte Kerberos-Delegierung](../kerberos/kerberos-constrained-delegation-overview.md)<br /><br />[Technische Referenz für die Kerberos-Authentifizierung](https://technet.microsoft.com/library/cc739058(v=ws.10).aspx)\(2003\)<br /><br />[Sicherheitsleitfaden für Kerberos](https://social.technet.microsoft.com/wiki/contents/articles/4209.kerberos-survival-guide.aspx) \(TechNet-Wiki\)|
|TLS\/SSL und DTLS \(Schannel-Security Support Provider\)|[TLS – SSL &#40;Schannel-SSP&#41; Übersicht](../tls/tls-ssl-schannel-ssp-overview.md)<br /><br />[Technische Referenz für Schannel Security Support Provider](../tls/schannel-security-support-provider-technical-reference.md)|
|Digestauthentifizierung|[Technische Referenz für die Authentifizierung Digest](https://technet.microsoft.com/library/cc782794(v=ws.10).aspx)\(2003\)|
|NTLM|[NTLM: Übersicht](../kerberos/ntlm-overview.md)<br />Enthält Links zu aktuellen und früheren Ressourcen|
|PKU2U|[Einführung in PKU2U in Windows](https://technet.microsoft.com/library/dd560634(v=ws.10).aspx)|
|Smartcard|[Technische Referenz zu Smartcards](https://technet.microsoft.com/itpro/windows/keep-secure/smart-card-windows-smart-card-technical-reference)<br /><br />
|Anmeldeinformationen|[Schutz und Verwaltung von Anmeldeinformationen](../credentials-protection-and-management/credentials-protection-and-management.md)<br />Enthält Links zu aktuellen und früheren Ressourcen<br /><br />[Übersicht über Kennwörter](../kerberos/passwords-overview.md)<br />Enthält Links zu aktuellen und früheren Ressourcen|


