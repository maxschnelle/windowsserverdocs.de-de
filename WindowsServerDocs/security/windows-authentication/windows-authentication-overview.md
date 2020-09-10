---
title: 'Windows-Authentifizierung: Übersicht'
description: Windows Server-Sicherheit
ms.topic: article
ms.assetid: 485a0774-0785-457f-a964-0e9403c12bb1
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/12/2016
ms.openlocfilehash: 4a2b5e6b48a56a1a2148df262d2785640ac6054d
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89638697"
---
# <a name="windows-authentication-overview"></a>Windows-Authentifizierung: Übersicht

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In diesem Navigationsthema für IT-Experten sind Dokumentationsressourcen für Technologien zur Windows-Authentifizierung und -Anmeldung aufgeführt, die Produktbewertungen, "Erste Schritte"-Handbücher, Verfahren, Entwurfs- und Bereitstellungshandbücher, technische Referenzen und Befehlsverzeichnisse enthalten.

## <a name="feature-description"></a>Featurebeschreibung
Authentifizierung ist der Vorgang, durch den die Identität eines Objekts, eines Dienstes oder einer Person überprüft wird. Ziel der Authentifizierung eines Objekts ist es, sicherzustellen, dass das Objekt echt und unverfälscht ist. Beim Authentifizieren eines Diensts oder einer Person ist das Ziel, sicherzustellen, dass die vorgelegten Anmeldeinformationen authentisch sind.

Im Netzwerkkontext dient die Authentifizierung dazu, die Identität gegenüber einer Netzwerkanwendung oder -ressource nachzuweisen. In der Regel wird die Identität durch einen kryptografischen Vorgang nachgewiesen, der entweder einen Schlüssel verwendet, der nur dem Benutzer bekannt ist, und zwar mit Kryptografie mit öffentlichem Schlüssel oder einem gemeinsam genutzten Schlüssel. Auf der Serverseite der Authentifizierungskommunikation werden die signierten Daten mit einem bekannten Kryptografieschlüssel verglichen, um den Authentifizierungsversuch zu überprüfen.

Durch die Speicherung der Kryptografieschlüssel an einem zentralen Ort wird der Authentifizierungsvorgang skalierbar und verwaltbar. Active Directory Domain Services ist die empfohlene und Standardtechnologie für das Speichern von Identitätsinformationen \( , einschließlich der Kryptografieschlüssel, die die Anmelde Informationen des Benutzers sind \) . Active Directory ist für Standardimplementierungen von Kerberos und NTLM erforderlich.

Authentifizierungstechniken reichen von einer einfachen Anmeldung, bei der Benutzer auf der Grundlage von etwas, das nur dem Benutzer bekannt ist, für leistungsfähigere Sicherheitsmechanismen identifiziert werden, die Benutzer wie Token, öffentliche Schlüssel Zertifikate und Biometrie verwenden. In einer Unternehmensumgebung ist es Diensten oder Benutzern eventuell möglich, auf unterschiedliche Anwendungen oder Ressourcen auf verschiedenen Arten von Servern an einem einzigen Standort oder auch standortübergreifend zugreifen. Aus diesem Grund muss die Authentifizierung Umgebungen unterstützen, die auf anderen Plattformen und anderen Windows-Betriebssystemen basieren.

Das Windows-Betriebssystem implementiert im Rahmen einer erweiterbaren Architektur einen Standardsatz von Authentifizierungs Protokollen, einschließlich Kerberos, NTLM, Transport Layer Security \/ Secure Sockets Layer \( TLS \/ \) -SSL und Digest. Darüber hinaus werden einige Protokolle zu Authentifizierungspaketen zusammengefasst, beispielsweise Negotiate und der Credential Security Support Provider. Mit diesen Protokollen und Paketen können Benutzer, Computer und Dienste authentifiziert werden. Der Authentifizierungsprozess wiederum ermöglicht Benutzern und Diensten einen sicheren Zugriff auf Ressourcen.

Weitere Informationen zur Windows-Authentifizierung einschließlich der Aspekte

-   [Windows-Authentifizierungskonzepte](windows-authentication-concepts.md)

-   [Windows-Anmeldeszenarios](windows-logon-scenarios.md)

-   [Architektur der Windows-Authentifizierung](windows-authentication-architecture.md)

-   [Architektur der Security Support Provider-Schnittstelle](security-support-provider-interface-architecture.md)

-   [Anmeldeinformationen-Prozesse in der Windows-Authentifizierung](credentials-processes-in-windows-authentication.md)

-   [In der Windows-Authentifizierung verwendete Gruppenrichtlinieneinstellungen](group-policy-settings-used-in-windows-authentication.md)

Weitere Informationen finden Sie unter [Technische Übersicht zur Windows-Authentifizierung](windows-authentication-technical-overview.md).

## <a name="practical-applications"></a>Praktische Anwendung
Mithilfe der Windows-Authentifizierung wird überprüft, ob die Informationen von einer vertrauenswürdigen Quelle stammen, ungeachtet dessen, ob es sich um eine Person oder ein Computerobjekt, beispielsweise einen anderen Computer, handelt. Windows stellt viele verschiedene Methoden bereit, um dies zu erreichen. Im Folgenden werden diese Methoden beschrieben.

|An...|Funktion|BESCHREIBUNG|
|----|------|--------|
|Authentifizieren innerhalb einer Active Directory-Domäne|Kerberos|Die Microsoft Windows &nbsp; Server-Betriebssysteme implementieren das Kerberos Version 5-Authentifizierungsprotokoll und Erweiterungen für die Authentifizierung mit öffentlichem Schlüssel. Der Kerberos-Authentifizierungs Client wird als Security Support Provider \( SSP implementiert \) und kann über die Security Support Provider-Schnittstelle (SSPI) aufgerufen werden \( \) . Die anfängliche Benutzerauthentifizierung ist in die Winlogon-Architektur für einmaliges Anmelden integriert \- . Der Kerberos-Schlüsselverteilungscenter \( KDC \) ist in andere Windows Server-Sicherheitsdienste integriert, die auf dem Domänen Controller ausgeführt werden. Der KDC verwendet die Active Directory Verzeichnisdienst-Datenbank der Domäne als Sicherheits Konto Datenbank. Active Directory ist für Standardimplementierungen von Kerberos erforderlich.<p>Weitere Ressourcen finden Sie unter [Kerberos-Authentifizierung: Übersicht](../kerberos/kerberos-authentication-overview.md).|
|Sichere Authentifizierung im Web|TLS- \/ SSL wie im SChannel Security Support Provider implementiert|Die Transport Layer Security \( TLS \) -Protokoll Versionen 1,0, 1,1 und 1,2, Secure Sockets Layer \( SSL \) -Protokoll, Versionen 2,0 und 3,0, Datagram Transport Layer Security Protokollversion 1,0 und das private Communications Transport \( PCT- \) Protokoll, Version 1,0, basieren auf Kryptografie mit öffentlichem Schlüssel. Die \( Authentifizierungsprotokoll Suite des Secure Channel SChannel- \) Anbieters stellt diese Protokolle bereit. Alle Schannel-Protokolle verwenden ein Client- und Servermodell.<p>Weitere Ressourcen finden Sie unter [TLS-SSL &#40;Schannel SSP&#41; Übersicht](../tls/tls-ssl-schannel-ssp-overview.md).|
|Authentifizieren bei einem Webdienst oder einer Anwendung|Integrierte Windows-Authentifizierung<p>Digestauthentifizierung|Weitere Ressourcen finden Sie unter [Integrierte Windows-Authentifizierung](/previous-versions/windows/it-pro/windows-server-2003/cc758557(v=ws.10)) und [Digestauthentifizierung](/previous-versions/windows/it-pro/windows-server-2003/cc738318(v=ws.10)) sowie [Erweiterte Digestauthentifizierung](/previous-versions/windows/it-pro/windows-server-2003/cc783131(v=ws.10)).|
|Authentifizieren bei älteren Anwendungen|NTLM|NTLM ist ein Authentifizierungsprotokoll für den Anforderungs \- Antwort Stil. Zusätzlich zur Authentifizierung bietet das NTLM-Protokoll optional eine Sitzungs Sicherheit, insbesondere Nachrichten Integrität und Vertraulichkeit durch Signierungs-und Versiegelung von Funktionen in NTLM.<p>Weitere Ressourcen finden Sie unter [NTLM: Übersicht](../kerberos/ntlm-overview.md).|
|Nutzen der mehrstufigen Authentifizierung|Unterstützung von Smartcards<p>Biometrie-Unterstützung|Smartcards sind eine Manipulations geschützte \- und tragbare Methode zum Bereitstellen von Sicherheitslösungen für Aufgaben wie Client Authentifizierung, Anmeldung bei Domänen, Code Signatur und Sichern von e-Mail-Nachrichten \- .<p>Bei der Biometrie wird ein unveränderliches physisches Merkmal einer Person erfasst, um diese Person eindeutig identifizieren zu können. Fingerabdrücke gehören zu den am häufigsten genutzten biometrischen Merkmalen, weshalb Millionen PCs und Peripheriegeräte mit biometrischen Fingerabdrucklesern ausgestattet sind.<p>Weitere Ressourcen finden Sie unter [Technische Referenz zu Smartcards](/windows/security/identity-protection/smart-cards/smart-card-windows-smart-card-technical-reference). |
|Bereitstellen der lokalen Verwaltung, Speicherung und Wiederverwendung von Anmeldeinformationen|Verwaltung von Anmeldeinformationen<p>Lokale Sicherheitsautorität<p>Kennwörter|Durch die Verwaltung von Anmeldeinformationen in Windows wird sichergestellt, Anmeldeinformationen sicher gespeichert werden. Anmelde Informationen werden auf dem sicheren Desktop \( für den lokalen oder Domänen Zugriff \) über apps oder Websites gesammelt, sodass bei jedem Zugriff auf eine Ressource die richtigen Anmelde Informationen angezeigt werden.<p>
|Erweitern des Authentifizierungsschutzes auf Legacysysteme|Erweiterter Schutz für die Authentifizierung|Mit diesem Feature wird der Schutz und die Handhabung von Anmelde Informationen bei der Authentifizierung von Netzwerkverbindungen mithilfe der integrierten Windows-Authentifizierung ( \( IWA) verbessert \) .|

## <a name="software-requirements"></a>Softwareanforderungen
Die Windows-Authentifizierung ist so konzipiert, dass sie mit früheren Versionen des Windows-Betriebssystem kompatibel ist. Verbesserungen in einer neuen Version stehen jedoch nicht notwendigerweise auch in früheren Versionen zur Verfügung. Weitere Informationen finden Sie in der Dokumentation zu den verschiedenen Features.

## <a name="server-manager-information"></a>Informationen zum Server-Manager
Viele Authentifizierungsfeatures können mit der Gruppenrichtlinie konfiguriert werden, die mithilfe des Server-Managers installiert werden kann. Das Windows-Biometrieframework wird mithilfe des Server-Managers installiert. Andere Server Rollen, die von Authentifizierungsmethoden abhängig sind, z. b \( \) . Webserver-IIS und Active Directory Domain Services, können auch mit Server-Manager installiert werden.

## <a name="related-resources"></a>Zugehörige Ressourcen

|Authentifizierungstechnologien|Ressourcen|
|----------------|-------|
|Windows-Authentifizierung|[Windows-Authentifizierung: Technische Übersicht](../windows-authentication/windows-authentication-technical-overview.md)<br />Enthält Themen, die Unterschiede zwischen den Versionen, allgemeine Authentifizierungskonzepte, Anmeldungsszenarien, Architekturen für unterstützte Versionen und geeignete Einstellungen behandeln.|
|Kerberos|[Kerberos Authentication Overview](../kerberos/kerberos-authentication-overview.md)<p>[Eingeschränkte Kerberos-Delegierung (Übersicht)](../kerberos/kerberos-constrained-delegation-overview.md)<p>[Technische Referenz](/previous-versions/windows/it-pro/windows-server-2003/cc739058(v=ws.10)) \( für die Kerberos-Authentifizierung 2003\)<p>[Kerberos-Forum](/answers/topics/windows-server-security.html)|
|TLS \/ SSL und DTLS \( SChannel Security Support Provider\)|[Übersicht über TLS-SSL &#40;Schannel SSP&#41;](../tls/tls-ssl-schannel-ssp-overview.md)<p>[Schannel Security Support Provider: Technische Referenz](../tls/schannel-security-support-provider-technical-reference.md)|
|Digestauthentifizierung|[Technische Referenz](/previous-versions/windows/it-pro/windows-server-2003/cc782794(v=ws.10)) \( für die Digest-Authentifizierung 2003\)|
|NTLM|[NTLM Overview](../kerberos/ntlm-overview.md)<br />Enthält Links zu aktuellen und früheren Ressourcen|
|PKU2U|[Einführung zu PKU2U in Windows](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd560634(v=ws.10))|
|Smartcard|[Technische Referenz zu Smartcards](/windows/security/identity-protection/smart-cards/smart-card-windows-smart-card-technical-reference)<p>
|Anmeldeinformationen|[Schutz und Verwaltung von Anmeldeinformationen](../credentials-protection-and-management/credentials-protection-and-management.md)<br />Enthält Links zu aktuellen und früheren Ressourcen<p>[Übersicht über Kenn Wörter](../kerberos/passwords-overview.md)<br />Enthält Links zu aktuellen und früheren Ressourcen|