---
title: 'Windows-Authentifizierung: Übersicht'
description: Windows Server-Sicherheit
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 262a510e0b8484f3ee5cc28726f10857f92cbfd4
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71403288"
---
# <a name="windows-authentication-overview"></a>Windows-Authentifizierung: Übersicht

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

In diesem Navigationsthema für IT-Experten sind Dokumentationsressourcen für Technologien zur Windows-Authentifizierung und -Anmeldung aufgeführt, die Produktbewertungen, "Erste Schritte"-Handbücher, Verfahren, Entwurfs- und Bereitstellungshandbücher, technische Referenzen und Befehlsverzeichnisse enthalten.

## <a name="feature-description"></a>Featurebeschreibung
Authentifizierung ist der Vorgang, durch den die Identität eines Objekts, eines Dienstes oder einer Person überprüft wird. Ziel der Authentifizierung eines Objekts ist es, sicherzustellen, dass das Objekt echt und unverfälscht ist. Beim Authentifizieren eines Diensts oder einer Person ist das Ziel, sicherzustellen, dass die vorgelegten Anmeldeinformationen authentisch sind.

Im Netzwerkkontext dient die Authentifizierung dazu, die Identität gegenüber einer Netzwerkanwendung oder -ressource nachzuweisen. In der Regel wird die Identität durch einen kryptografischen Vorgang nachgewiesen, der entweder einen Schlüssel verwendet, der nur dem Benutzer bekannt ist, und zwar mit Kryptografie mit öffentlichem Schlüssel oder einem gemeinsam genutzten Schlüssel. Auf der Serverseite der Authentifizierungskommunikation werden die signierten Daten mit einem bekannten Kryptografieschlüssel verglichen, um den Authentifizierungsversuch zu überprüfen.

Durch die Speicherung der Kryptografieschlüssel an einem zentralen Ort wird der Authentifizierungsvorgang skalierbar und verwaltbar. Active Directory Domain Services ist die empfohlene und Standardtechnologie für das Speichern von Identitätsinformationen \(einschließlich der Kryptografieschlüssel, die die Anmelde Informationen des Benutzers\)sind. Active Directory ist für Standardimplementierungen von Kerberos und NTLM erforderlich.

Authentifizierungstechniken reichen von einer einfachen Anmeldung, die Benutzer auf der Grundlage von etwas identifiziert, das nur dem Benutzer bekannt ist, und leistungsfähigeren Sicherheitsmechanismen, bei denen Benutzer wie Token, öffentliche Schlüssel Zertifikate und Biometrie. In einer Unternehmensumgebung ist es Diensten oder Benutzern eventuell möglich, auf unterschiedliche Anwendungen oder Ressourcen auf verschiedenen Arten von Servern an einem einzigen Standort oder auch standortübergreifend zugreifen. Aus diesem Grund muss die Authentifizierung Umgebungen unterstützen, die auf anderen Plattformen und anderen Windows-Betriebssystemen basieren.

Das Windows-Betriebssystem implementiert einen Standardsatz von Authentifizierungs Protokollen, einschließlich Kerberos, NTLM, Transport Layer Security\/Secure Sockets Layer \(TLS\/SSL-\)und Digest als Teil einer erweiterbaren Architektur. Darüber hinaus werden einige Protokolle zu Authentifizierungspaketen zusammengefasst, beispielsweise Negotiate und der Credential Security Support Provider. Mit diesen Protokollen und Paketen können Benutzer, Computer und Dienste authentifiziert werden. Der Authentifizierungsprozess wiederum ermöglicht Benutzern und Diensten einen sicheren Zugriff auf Ressourcen.

Weitere Informationen zur Windows-Authentifizierung einschließlich der Aspekte

-   [Windows-Authentifizierungskonzepte](windows-authentication-concepts.md)

-   [Windows-Anmeldeszenarios](windows-logon-scenarios.md)

-   [Architektur der Windows-Authentifizierung](windows-authentication-architecture.md)

-   [Architektur der Security Support Provider-Schnittstelle](security-support-provider-interface-architecture.md)

-   [Anmeldeinformationen-Prozesse in der Windows-Authentifizierung](credentials-processes-in-windows-authentication.md)

-   [In der Windows-Authentifizierung verwendete Gruppenrichtlinieneinstellungen](group-policy-settings-used-in-windows-authentication.md)

Weitere Informationen finden Sie unter [Technische Übersicht zur Windows-Authentifizierung](windows-authentication-technical-overview.md).

## <a name="practical-applications"></a>Praktische Anwendungsfälle
Mithilfe der Windows-Authentifizierung wird überprüft, ob die Informationen von einer vertrauenswürdigen Quelle stammen, ungeachtet dessen, ob es sich um eine Person oder ein Computerobjekt, beispielsweise einen anderen Computer, handelt. Windows stellt viele verschiedene Methoden bereit, um dies zu erreichen. Im Folgenden werden diese Methoden beschrieben.

|An...|Feature|Beschreibung|
|----|------|--------|
|Authentifizieren innerhalb einer Active Directory-Domäne|Kerberos|Die Microsoft Windows&nbsp;Server-Betriebssysteme implementieren das Kerberos Version 5-Authentifizierungsprotokoll und Erweiterungen für die Authentifizierung mit öffentlichem Schlüssel. Der Kerberos-Authentifizierungs Client wird als Security Support Provider \(SSP-\) implementiert, und der Zugriff erfolgt über die Security Support Provider-Schnittstelle \(SSPI-\). Die anfängliche Benutzerauthentifizierung ist in das Winlogon-\-für einmaliges Anmelden integriert. Die Kerberos-Schlüsselverteilungscenter \(KDC-\) ist in andere Windows Server-Sicherheitsdienste integriert, die auf dem Domänen Controller ausgeführt werden. Der KDC verwendet die Active Directory Verzeichnisdienst-Datenbank der Domäne als Sicherheits Konto Datenbank. Active Directory ist für Standardimplementierungen von Kerberos erforderlich.<br /><br />Weitere Ressourcen finden Sie unter [Kerberos-Authentifizierung: Übersicht](../kerberos/kerberos-authentication-overview.md).|
|Sichere Authentifizierung im Web|TLS\/SSL wie im SChannel Security Support Provider implementiert|Die Transport Layer Security \(TLS\) Protokoll Versionen 1,0, 1,1 und 1,2, Secure Sockets Layer \(SSL\) Protokoll, Versionen 2,0 und 3,0, Datagram Transport Layer Security Protokollversion 1,0 und der private Communications Transport \(PCT\) Protocol, Version 1,0, basieren auf Kryptografie mit öffentlichem Schlüssel. Die Secure Channel \(SChannel\) Provider Authentication Protocol Suite stellt diese Protokolle bereit. Alle Schannel-Protokolle verwenden ein Client- und Servermodell.<br /><br />Weitere Ressourcen finden Sie unter [TLS-SSL &#40;Schannel SSP&#41; Overview](../tls/tls-ssl-schannel-ssp-overview.md).|
|Authentifizieren bei einem Webdienst oder einer Anwendung|Integrierte Windows-Authentifizierung<br /><br />Digestauthentifizierung|Weitere Ressourcen finden Sie unter [integrierte Windows-Authentifizierung](https://technet.microsoft.com/library/cc758557(v=WS.10).aspx) und [Digestauthentifizierung](https://technet.microsoft.com/library/cc738318(v=ws.10).aspx) und [Erweiterte Digestauthentifizierung](https://technet.microsoft.com/library/cc783131(v=ws.10).aspx).|
|Authentifizieren bei älteren Anwendungen|NTLM|NTLM ist eine Herausforderung\-Authentifizierungsprotokoll für den Antwort Stil. Zusätzlich zur Authentifizierung bietet das NTLM-Protokoll optional eine Sitzungs Sicherheit, insbesondere Nachrichten Integrität und Vertraulichkeit durch Signierungs-und Versiegelung von Funktionen in NTLM.<br /><br />Weitere Ressourcen finden Sie unter [NTLM: Übersicht](../kerberos/ntlm-overview.md).|
|Nutzen der mehrstufigen Authentifizierung|Unterstützung von Smartcards<br /><br />Biometrie-Unterstützung|Smartcards sind eine Manipulations geschützte\-, um Sicherheitslösungen für Aufgaben wie Client Authentifizierung, Anmeldung bei Domänen, Code Signatur und Sicherung von e\-Mail bereitzustellen.<br /><br />Bei der Biometrie wird ein unveränderliches physisches Merkmal einer Person erfasst, um diese Person eindeutig identifizieren zu können. Fingerabdrücke gehören zu den am häufigsten genutzten biometrischen Merkmalen, weshalb Millionen PCs und Peripheriegeräte mit biometrischen Fingerabdrucklesern ausgestattet sind.<br /><br />Weitere Ressourcen finden Sie unter [Technische Referenz zu Smartcards](https://technet.microsoft.com/itpro/windows/keep-secure/smart-card-windows-smart-card-technical-reference). |
|Bereitstellen der lokalen Verwaltung, Speicherung und Wiederverwendung von Anmeldeinformationen|Verwaltung von Anmeldeinformationen<br /><br />Lokale Sicherheitsautorität<br /><br />Kennwörter|Durch die Verwaltung von Anmeldeinformationen in Windows wird sichergestellt, Anmeldeinformationen sicher gespeichert werden. Anmelde Informationen werden auf dem sicheren Desktop \(für den lokalen oder Domänen Zugriff\)über apps oder Websites gesammelt, sodass bei jedem Zugriff auf eine Ressource die richtigen Anmelde Informationen angezeigt werden.<br /><br />
|Erweitern des Authentifizierungsschutzes auf Legacysysteme|Erweiterter Schutz für Authentifizierung|Diese Funktion verbessert den Schutz und die Handhabung von Anmelde Informationen bei der Authentifizierung von Netzwerkverbindungen mithilfe der integrierten Windows-Authentifizierung \(IWA\).|

## <a name="software-requirements"></a>Softwareanforderungen
Die Windows-Authentifizierung ist so konzipiert, dass sie mit früheren Versionen des Windows-Betriebssystem kompatibel ist. Verbesserungen in einer neuen Version stehen jedoch nicht notwendigerweise auch in früheren Versionen zur Verfügung. Weitere Informationen finden Sie in der Dokumentation zu den verschiedenen Features.

## <a name="server-manager-information"></a>Informationen zum Server-Manager
Viele Authentifizierungsfeatures können mit der Gruppenrichtlinie konfiguriert werden, die mithilfe des Server-Managers installiert werden kann. Das Windows-Biometrieframework wird mithilfe des Server-Managers installiert. Andere Server Rollen, die von Authentifizierungsmethoden abhängig sind, z. b. Webserver \(IIS\) und Active Directory Domain Services, können auch mit Server-Manager installiert werden.

## <a name="related-resources"></a>Verwandte Ressourcen

|Authentifizierungstechnologien|Ressourcen|
|----------------|-------|
|Windows-Authentifizierung|[Windows-Authentifizierung: Technische Übersicht](../windows-authentication/windows-authentication-technical-overview.md)<br />Enthält Themen, in denen Unterschiede Zwischenversionen, allgemeinen Authentifizierungs Konzepten, Anmelde Szenarien, Architekturen für unterstützte Versionen und anwendbaren Einstellungen behandelt werden.|
|Kerberos|[Kerberos-Authentifizierung (Übersicht)](../kerberos/kerberos-authentication-overview.md)<br /><br />[Übersicht zu Kerberos Constrained Delegation](../kerberos/kerberos-constrained-delegation-overview.md)<br /><br />[Technische Referenz für die Kerberos-Authentifizierung](https://technet.microsoft.com/library/cc739058(v=ws.10).aspx)\(2003\)<br /><br />[Kerberos-Lebens Handbuch](https://social.technet.microsoft.com/wiki/contents/articles/4209.kerberos-survival-guide.aspx) \(TechNet-wiki\)|
|TLS\/SSL und DTLS \(SChannel Security Support Provider\)|[TLS-SSL &#40;Schannel SSP&#41; (Übersicht)](../tls/tls-ssl-schannel-ssp-overview.md)<br /><br />[Schannel Security Support Provider: Technische Referenz](../tls/schannel-security-support-provider-technical-reference.md)|
|Digestauthentifizierung|[Technische Referenz](https://technet.microsoft.com/library/cc782794(v=ws.10).aspx) für die Digest-Authentifizierung\(2003\)|
|NTLM|[Übersicht über NTLM](../kerberos/ntlm-overview.md)<br />Enthält Links zu aktuellen und früheren Ressourcen|
|PKU2U|[Einführung in PKU2U in Windows](https://technet.microsoft.com/library/dd560634(v=ws.10).aspx)|
|Smartcard|[Technische Referenz zu Smartcards](https://technet.microsoft.com/itpro/windows/keep-secure/smart-card-windows-smart-card-technical-reference)<br /><br />
|Anmeldeinformationen|[Schutz und Verwaltung von Anmeldeinformationen](../credentials-protection-and-management/credentials-protection-and-management.md)<br />Enthält Links zu aktuellen und früheren Ressourcen<br /><br />[Übersicht über Kenn Wörter](../kerberos/passwords-overview.md)<br />Enthält Links zu aktuellen und früheren Ressourcen|


