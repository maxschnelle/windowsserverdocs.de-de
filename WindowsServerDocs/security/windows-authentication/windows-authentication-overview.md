---
title: "Windows-Authentifizierung: Übersicht"
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
ms.openlocfilehash: c2ec55ed6b09628d1d80a24be766259980e84d6e
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="windows-authentication-overview"></a>Windows-Authentifizierung: Übersicht

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Dieses navigationsthema für IT-Experten sind Dokumentationsressourcen für Windows-Authentifizierung und Anmeldung Technologien, die Produktbewertungen, erste Schritte-Leitfäden, Verfahren, Entwurfs- und Bereitstellungshandbücher, technische Referenzen und Befehlsreferenzen enthalten.

## <a name="feature-description"></a>Featurebeschreibung
Authentifizierung ist ein Prozess zur Überprüfung der Identität eines Objekts, Dienst oder einer Person. Wenn Sie ein Objekt authentifizieren, ist das Ziel, stellen Sie sicher, dass das Objekt um eine Originalversion handelt. Wenn Sie einen Dienst oder eine Person authentifizieren, ist das Ziel, stellen Sie sicher, dass die vorgelegten Anmeldeinformationen authentisch sind.

In einem Netzwerk Kontext dient die Authentifizierung der Nachweis der Identität zu einer Netzwerkanwendung oder -Ressource. Identität wird in der Regel durch einen kryptografischen Vorgang nachgewiesen, die entweder einen Schlüssel, den nur der Benutzer weiß verwendet – wie bei der Kryptografie mit öffentlichem Schlüssel – oder ein vorinstallierter Schlüssel. Die Serverseite der Authentifizierung vergleicht die signierten Daten mit einem bekannten Kryptografieschlüssel, um den Authentifizierungsversuch zu überprüfen.

Speichern die kryptografischen Schlüssel an einem sicheren, zentralen Ort wird der Authentifizierungsvorgang skalierbar und verwaltbar. Active Directory-Domänendienste sind die empfohlene und standardmäßig verwendete Technologie zum Speichern von Identitätsinformationen \ (einschließlich der Kryptografieschlüssel, die der Benutzer Credentials\). Active Directory ist für Standardimplementierungen von Kerberos und NTLM-Standard erforderlich.

Die verfügbaren Authentifizierungstechniken reichen von der einfachen Anmeldung, die Benutzer basierend auf ein Element, das nur für der Benutzer - wie ein Kennwort leistungsfähigeren Sicherheitsmechanismen bekannt, bei denen der Benutzer hat ist – wie Token, Zertifikate mit öffentlichem Schlüssel und biometrischen Daten identifiziert. In einer Unternehmensumgebung können Dienste oder Benutzer mehrere Anwendungen oder Ressourcen auf viele Arten von Servern an einem einzigen Standort oder auch standortübergreifend zugreifen. Aus diesen Gründen muss die Authentifizierung Umgebungen für andere Plattformen und für andere Windows-Betriebssysteme unterstützen.

Windows-Betriebssystem implementiert einen Standardsatz von Authentifizierungsprotokollen Kerberos, NTLM, Transport Layer Sicherheit\/Secure Sockets Layer-\(TLS\/SSL\) und Digest, im Rahmen einer erweiterbaren Architektur. Darüber hinaus werden einige Protokolle zu Authentifizierungspaketen beispielsweise Negotiate und der Credential Security Support Provider kombiniert. Aktivieren diesen Protokollen und Paketen Authentifizierung von Benutzern, Computern und Diensten. der Authentifizierungsprozess ermöglicht wiederum authentifizierten Benutzern und Diensten auf sichere Weise den Zugriff auf Ressourcen.

Weitere Informationen, einschließlich der Windows-Authentifizierung

-   [Windows-Authentifizierungskonzepte](windows-authentication-concepts.md)

-   [Windows-Anmeldeszenarios](windows-logon-scenarios.md)

-   [Architektur der Windows-Authentifizierung](windows-authentication-architecture.md)

-   [Security Support Provider-Schnittstellenarchitektur](security-support-provider-interface-architecture.md)

-   [Anmeldeinformationen-Prozesse in der Windows-Authentifizierung](credentials-processes-in-windows-authentication.md)

-   [Gruppenrichtlinien Sie in Windows-Authentifizierung verwendete](group-policy-settings-used-in-windows-authentication.md)

Weitere Informationen finden Sie unter der [technische Übersicht über Windows-Authentifizierung](windows-authentication-technical-overview.md).

## <a name="practical-applications"></a>In der Praxis
Windows-Authentifizierung verwendet, stellen Sie sicher, dass die Informationen von einer vertrauenswürdigen Quelle stammen, ob von einer Person oder ein Computerobjekt, beispielsweise einen anderen Computer. Windows bietet viele verschiedene Methoden, um dieses Ziel zu erreichen, wie im folgenden beschrieben.

|An...|Funktion|Beschreibung|
|----|------|--------|
|Authentifizierung innerhalb einer Active Directory-Domäne|Kerberos|Microsoft Windows&nbsp;Server-Betriebssysteme implementieren das Kerberos V5-Authentifizierungsprotokoll und Erweiterungen für die Authentifizierung des öffentlichen Schlüssels. Die Kerberos-Authentifizierungsclient wird als Security Support Provider implementiert \(SSP\) über die Security Support Provider Interface \(SSPI\) zugegriffen werden kann. Die Erstauthentifizierung von Benutzern ist in den Winlogon einzelne Standardparameter-Architektur integriert. Die Kerberos-Schlüsselverteilungscenter-\(KDC\) ist in andere auf dem Domänencontroller unter Windows Server-Sicherheitsdienste integriert. Das KDC verwendet die Domäne Datenbank des Active Directory-Dienst als Sicherheitskontendatenbank. Active Directory ist für Kerberos-Standardimplementierungen erforderlich.<br /><br />Weitere Ressourcen finden Sie unter [Kerberos-Authentifizierung: Übersicht](../kerberos/kerberos-authentication-overview.md).|
|Sichere Authentifizierung im Web|TLS\/SSL wie im Schannel-Security Support Provider implementiert|Die \(TLS\) Transport Layer Security-Protokoll, Version 1.0, 1.1 und 1.2, \(SSL\) Secure Sockets Layer-Protokoll, Version 2.0 und 3.0, Datagram Transport Layer Security-Protokollversion 1.0 und das Private Communications Transport \(PCT\)-Protokoll, Version 1.0, basieren auf Kryptografie mit öffentlichem Schlüssel. Authentifizierungsprotokollsuite des sicheren Kanals \(Schannel\) Anbieter enthält diese Protokolle. Alle Schannel-Protokolle verwenden ein Client- und Servermodell.<br /><br />Weitere Ressourcen finden Sie unter [TLS – SSL & 40; Schannel SSP & 41; Übersicht über die](../tls/tls-ssl-schannel-ssp-overview.md).|
|Für die Authentifizierung bei einem Webdienst oder einer Anwendung|Integrierte Windows-Authentifizierung<br /><br />Digest-Authentifizierung|Weitere Ressourcen finden Sie unter [integrierte Windows-Authentifizierung] (https://technet.microsoft.com/library/cc758557(v=WS.10.aspx and [Digest Authentication](https://technet.microsoft.com/library/cc738318(v=ws.10).aspx), and [Advanced Digest Authentication](https://technet.microsoft.com/library/cc783131(v=ws.10).aspx).|
|Authentifizieren bei älteren Anwendungen|NTLM|NTLM ein Challenge\ / Antwort-Stil Authentifizierung protocol.In zusätzlich zur Authentifizierung ist, bietet das NTLM-Protokoll optional für die sitzungssicherheit – insbesondere Nachrichtenintegrität und Vertraulichkeit, durch die Signierung und -Verschlüsselung Funktionen in NTLM.<br /><br />Weitere Ressourcen finden Sie unter [NTLM: Übersicht](../kerberos/ntlm-overview.md).|
|Mehrstufige Authentifizierung nutzen|Unterstützung von Smartcards<br /><br />Biometrie-Unterstützung|Smartcards sind Tamper\ Manipulationen und Mobil wie Sicherheitslösungen für Aufgaben wie Clientauthentifizierung, Anmeldung bei Domänen, Code, Signieren und Schützen von E\-Mail-werden können.<br /><br />Biometrie stützt sich auf ein unveränderliches physisches Merkmal einer Person zur eindeutigen Identifizierung dieser Person zu messen. Fingerabdrücke gehören zu den am häufigsten genutzten biometrischen Merkmalen, mit Millionen von Fingerabdruck biometrischer Geräte, die PCs und Peripheriegeräte eingebettet sind.<br /><br />Weitere Ressourcen finden Sie unter [technische Referenz zu Smartcards](https://technet.microsoft.com/itpro/windows/keep-secure/smart-card-windows-smart-card-technical-reference). |
|Bereitstellen Sie lokale Verwaltung, Speicherung und Wiederverwendung von Anmeldeinformationen|Verwaltung von Anmeldeinformationen<br /><br />Local Security Authority<br /><br />Kennwörter|Verwaltung von Anmeldeinformationen in Windows wird sichergestellt, dass Anmeldeinformationen sicher gespeichert werden. Anmeldeinformationen werden gesammelt, auf dem sicheren Desktop \ (für lokale oder domänenspezifische zugriff\) über Apps oder Websites, damit die richtigen Anmeldeinformationen jedes Mal angezeigt werden eine Ressource zugegriffen wird.<br /><br />
|Erweitern des authentifizierungsschutzes auf Legacysysteme|Erweiterter Schutz für Authentifizierung|Dieses Feature erhöht den Schutz und die Handhabung von Anmeldeinformationen, wenn Netzwerkverbindungen mithilfe der integrierten Windows-Authentifizierung \(IWA\).|

## <a name="software-requirements"></a>Anforderungen der Clientsoftware
Windows-Authentifizierung mit früheren Versionen von Windows-Betriebssystems kompatibel sein soll. Mit jeder Version sind jedoch nicht notwendigerweise auch in früheren Versionen. Lesen Sie die Dokumentation zu bestimmten Funktionen für Weitere Informationen.

## <a name="server-manager-information"></a>Server-Manager-Informationen
Viele Authentifizierungsfeatures können mit Gruppenrichtlinien, die mit dem Server-Manager installiert werden kann konfiguriert werden. Die Windows-Biometrieframework wird mithilfe von Server-Manager installiert. Andere Serverrollen, die Authentifizierungsmethoden, z.B. Webserver \(IIS\) und Active Directory-Domänendiensten abhängig sind, können auch mit Server-Manager installiert werden.

## <a name="related-resources"></a>Verwandte Ressourcen

|Authentifizierungstechnologien|Ressourcen|
|----------------|-------|
|Windows-Authentifizierung|[Technische Übersicht über Windows-Authentifizierung](../windows-authentication/windows-authentication-technical-overview.md)<br />Enthält Themen, die Unterschiede zwischen Versionen, allgemeine Authentifizierungskonzepte, anmeldungsszenarien, Architekturen für unterstützte Versionen und geeignete Einstellungen-Adressierung.|
|Kerberos|[Kerberos-Authentifizierung: Übersicht](../kerberos/kerberos-authentication-overview.md)<br /><br />[Eingeschränkte Kerberos-Delegierung (Übersicht)](../kerberos/kerberos-constrained-delegation-overview.md)<br /><br />[technische Referenz zu Kerberos-Authentifizierung](https://technet.microsoft.com/library/cc739058(v=ws.10).aspx)\(2003\)<br /><br />[Sicherheitsleitfaden für Kerberos](https://social.technet.microsoft.com/wiki/contents/articles/4209.kerberos-survival-guide.aspx) \(TechNet Wiki\)|
|TLS\/SSL und DTLS \ (Schannel Security Support Provider\)|[TLS – SSL & 40; Schannel SSP & 41; (Übersicht)](../tls/tls-ssl-schannel-ssp-overview.md)<br /><br />[Technische Referenz für Schannel Security Support Provider](../tls/schannel-security-support-provider-technical-reference.md)|
|Digest-Authentifizierung|[Digest-Authentifizierung Technical Reference](https://technet.microsoft.com/library/cc782794(v=ws.10).aspx)\(2003\)|
|NTLM|[NTLM (Übersicht)](../kerberos/ntlm-overview.md)<br />Enthält Links zu aktuellen und früheren Ressourcen|
|PKU2U|[Einführung in die PKU2U in Windows](https://technet.microsoft.com/library/dd560634(v=ws.10).aspx)|
|Smartcard|[Technische Referenz zu Smartcards](https://technet.microsoft.com/itpro/windows/keep-secure/smart-card-windows-smart-card-technical-reference)<br /><br />
|Anmeldeinformationen|[Schutz von Anmeldeinformationen und Verwaltung](../credentials-protection-and-management/credentials-protection-and-management.md)<br />Enthält Links zu aktuellen und früheren Ressourcen<br /><br />[Übersicht über Kennwörter](../kerberos/passwords-overview.md)<br />Enthält Links zu aktuellen und früheren Ressourcen|


