---
title: Security Support Provider-Schnittstellenarchitektur
description: Windows Server-Sicherheit
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-windows-auth
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: de09e099-5711-48f8-adbd-e7b8093a0336
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 8b0a74089c5d8a88a380f8a56e3b9e03b84081c1
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="security-support-provider-interface-architecture"></a>Security Support Provider-Schnittstellenarchitektur

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Dieses Referenzthema für IT-Experten beschreibt die Windows-Authentifizierungsprotokolle, die innerhalb der Security Support Provider-Schnittstelle (SSPI)-Architektur verwendet werden.

Die Microsoft Security Support Provider-Schnittstelle (SSPI) ist die Grundlage für die Windows-Authentifizierung. Verwenden SSPI zur Verfügung stellt, Anwendungen und Infrastrukturdienste, die eine Authentifizierung erfordern.

Die SSPI ist die Implementierung von der Generic Security Service API (GSSAPI) in Windows Server-Betriebssysteme. Weitere Informationen über die GSSAPI finden Sie unter RFC 2743 und RFC Gesetzes 2744 in der IETF RFC-Datenbank.

Die standardmäßige Security Support Provider (SSP), die den Aufrufen bestimmter Authentifizierungsprotokolle in Windows werden als DLL-Dateien in die SSPI integriert. Diese Standard-SSPs werden in den folgenden Abschnitten beschrieben. Zusätzliche SSPs können integriert werden, wenn sie mit der SSPI verwendet werden können.

Wie in der folgenden Abbildunggezeigt, enthält die SSPI in Windows einen Mechanismus, mit dem Authentifizierungstoken wird durch den über die vorhandene Kommunikationskanal zwischen dem Clientcomputer und dem Server. Wenn zwei Computer oder Geräte müssen authentifiziert werden, sodass sie sicher kommunizieren können, werden die Anforderungen für die Authentifizierung an die SSPI weitergeleitet, die Authentifizierungsvorgang unabhängig vom derzeit ausgeführt. Die SSPI gibt transparent binäre große Objekte zurück. Diese werden zwischen den Anwendungen übergeben an diesem, die Punkt sie an der SSPI-Ebene übergeben werden können. Daher kann die SSPI eine Anwendung Security-Modelle verfügbar ohne Änderung der Benutzeroberfläche für das Sicherheitssystem auf einem Computer oder im Netzwerk verwenden.

![Das Diagramm zeigt die Sicherheitsarchitektur Support Provider-Schnittstelle](../media/security-support-provider-interface-architecture/AuthN_SecuritySupportProviderInterfaceArchitecture.jpg)

In den folgenden Abschnitten wird beschrieben, mit der SSPI interagieren Standard-SSPs. SSPs werden zur Förderung der sicheren Kommunikation in einer unsicheren Netzwerkumgebung auf unterschiedliche Weise in Windows-Betriebssystemen verwendet.

-   [Kerberos-Security Support Provider](#BKMK_KerbSSP)

-   [NTLM Security Support Provider](#BKMK_NTLMSSP)

-   [Digest-Security Support Provider](#BKMK_DigestSSP)

-   [Schannel Security Support Provider](#BKMK_SchannelSSP)

-   [Handeln Security Support Provider aus](#BKMK_NegoSSP)

-   [Credential Security Support Provider](#BKMK_CredSSP)

-   [Handeln Sie Erweiterungen Security Support Provider aus](#BKMK_NegoExtsSSP)

-   [PKU2U-Security Support Provider](#BKMK_PKU2USSP)

In diesem Thema enthalten:

[Security Support Provider-Auswahl](security-support-provider-interface-architecture.md#BKMK_SecuritySupportProviderSelection)

### <a name="BKMK_KerbSSP"></a>Kerberos-Security Support Provider
Dieses SSP verwendet nur das Kerberos V5-Protokoll für die Implementierung von Microsoft. Dieses Protokoll basiert auf der Netzwerk-Arbeitsgruppe des RFC 4120 und Entwurf überarbeiten. Es ist ein Industriestandardprotokoll, das mit einem Kennwort oder eine Smartcard für die interaktive Anmeldung verwendet wird. Es ist auch die bevorzugte Authentifizierungsmethode für Services in Windows.

Da das Kerberos-Protokoll das Standardauthentifizierungsprotokoll seit Windows2000 wurde, unterstützen alle Domänendienste der SSP. Kerberos Hierzu gehören:

-   Active Directory-Abfragen, die die Lightweight Directory Access Protocol (LDAP) verwenden

-   Server oder einer Arbeitsstation Remoteverwaltung, die den Remoteprozeduraufruf-Dienst verwendet.

-   Druckdienste

-   Client-Server-Authentifizierung

-   Remotezugriff auf Dateien, die das Server Message Block (SMB)-Protokoll (auch bekannt als Common Internet File System oder CIFS) verwendet.

-   DFS Management und Weiterleitung

-   Intranet-Authentifizierung zu IIS (Internetinformationsdienste)

-   Sicherheit Autorität für die Authentifizierung für Internet Protocol Security (IPsec)

-   Zertifikatanforderungen an Active Directory-Zertifikatdienste für Domänenbenutzer und Computer

Speicherort: %windir%\Windows\System32\kerberos.dll

Dieser Anbieter wird standardmäßig in im genannten Versionen enthalten die **gilt für** Liste am Anfang dieses Themas, plus Windows Server2003 und Windows XP.

**Weitere Ressourcen für das Kerberos-Protokoll und der Kerberos-SSP**

-   [Microsoft Kerberos (Windows)](https://msdn.microsoft.com/library/aa378747(VS.85).aspx)

-   [\[MS-KILE\]: Kerberos-Protokollerweiterungen](https://msdn.microsoft.com/library/cc233855(PROT.10).aspx)

-   [\[MS-SFU\]: Kerberos-Protokollerweiterungen: Dienst für User und eingeschränkte Delegierung](https://msdn.microsoft.com/library/cc246071(PROT.13).aspx)

-   [Kerberos-SSP/AP (Windows)](https://msdn.microsoft.com/library/aa377942(VS.85).aspx)

-   [Kerberos-Erweiterungen](https://technet.microsoft.com/library/cc749438(v=ws.10).aspx) für windowsvista

-   [Änderungen bei der Kerberosauthentifizierung](https://technet.microsoft.com/library/dd560670(v=ws.10).aspx) für Windows7 

-   [Technische Referenz zu Kerberos-Authentifizierung](https://technet.microsoft.com/library/cc739058(v=ws.10).aspx)

### <a name="BKMK_NTLMSSP"></a>NTLM Security Support Provider
Der NTLM Security Support Provider (NTLM SSP) ist eine Binärdatei, die Messaging-Protokolls durch die Security Support Provider-Schnittstelle (SSPI) verwendet, um NTLM NTLM-Authentifizierung zu ermöglichen und Integrität und Vertraulichkeit Optionen aushandeln. Wo SSPI-Authentifizierung einschließlich für Server Message Block oder CIFS-Authentifizierung, HTTP-Negotiate-Authentifizierung (z.B. Internet Webauthentifizierung) und den Remoteprozeduraufruf-Dienst verwendet wird, wird NTLM verwendet. Die NTLM-SSP enthält die NTLM- und NTLM Version 2 (NTLMv2)-Authentifizierungsprotokollen.

Die unterstützten Windows-Betriebssysteme können die NTLM-SSP für Folgendes verwenden:

-   Client/Server-Authentifizierung

-   Druckdienste

-   Dateizugriff durch CIFS (SMB) verwenden

-   Sichere Remote Procedure Call oder DCOM-Diensts

Speicherort: %windir%\Windows\System32\msv1_0.dll

Dieser Anbieter wird standardmäßig in im genannten Versionen enthalten die **gilt für** Liste am Anfang dieses Themas, plus Windows Server2003 und Windows XP.

**Weitere Ressourcen für das NTLM-Protokoll und NTLM-SSP**

-   [MSV1_0 Authentifizierungspaket (Windows)](https://msdn.microsoft.com/library/aa378753(VS.85).aspx)

-   [Änderungen bei der NTLM-Authentifizierung](https://technet.microsoft.com/library/dd566199(v=ws.10).aspx) in Windows7 

-   [Microsoft-NTLM (Windows)](https://msdn.microsoft.com/library/aa378749(VS.85).aspx)

-   [Überwachung und Einschränkung der NTLM-Benutzerhandbuch](https://technet.microsoft.com/library/jj865674(v=ws.10).aspx)

### <a name="BKMK_DigestSSP"></a>Digest-Security Support Provider
Die Digestauthentifizierung ist ein Branchenstandard, die für die Lightweight Directory Access Protocol (LDAP) und Webauthentifizierung verwendet wird. Digestauthentifizierung überträgt Anmeldeinformationen über das Netzwerk als eine MD5-Hash oder Digestauthentifizierung.

Digest-SSP (Wdigest.dll) wird für Folgendes verwendet:

-   Internet Explorer und Internet Information Services (IIS)-Zugriff

-   LDAP-Abfragen

Speicherort: %windir%\Windows\System32\Digest.dll

Dieser Anbieter wird standardmäßig in im genannten Versionen enthalten die **gilt für** Liste am Anfang dieses Themas, plus Windows Server2003 und Windows XP.

**Weitere Ressourcen für das Digest-Protokoll und der Digest-SSP**

-   [Microsoft Digest-Authentifizierung (Windows)](https://msdn.microsoft.com/library/aa378745(VS.85).aspx)

-   [\[MS-DPSP\]: digest-Protokollerweiterungen](https://msdn.microsoft.com/library/cc227906(PROT.13).aspx)

### <a name="BKMK_SchannelSSP"></a>Schannel Security Support Provider
Die Secure Channel (Schannel) wird verwendet, für Web-basierte Server-Authentifizierung, z.B. wenn ein Benutzer versucht, einen sicheren Webserver zuzugreifen.

Das TLS-Protokoll, SSL-Protokoll, das Private Communications Technology (PCT)-Protokoll und das Protokoll Datagram Transport Layer (DTLS) basieren auf Kryptografie mit öffentlichem Schlüssel. Schannel enthält alle diese Protokolle. Alle Schannel-Protokolle verwenden ein Client/Server-Modell. Der Schannel SSP verwendet Zertifikate mit öffentlichem Schlüssel zum Authentifizieren von Parteien. Beim Authentifizieren von Parteien wählt Schannel-SSP ein Protokoll in der folgenden Prioritätsreihenfolge aus:

-   Transport Layer Security (TLS) Version 1.0

-   Transport Layer Security (TLS) Version 1.1

-   Transport Layer Security (TLS) Version 1.2

-   Secure Socket Layer (SSL) Version 2.0

-   Secure Socket Layer (SSL) Version 3.0

-   Private Communications Technology (PCT)

    **Hinweis:** PCT ist standardmäßig deaktiviert.

Das Protokoll, das der Fall ist das bevorzugte Authentifizierungsprotokoll, das dem Client und Server unterstützen kann. Wenn ein Server alle Schannel-Protokolle unterstützt und der Client nur SSL 3.0 und SSL 2.0 unterstützt, verwendet der Authentifizierungsprozess SSL 3.0.

DTLS wird verwendet, wenn Sie explizit von der Anwendung aufgerufen. Weitere Informationen zu DTLS und andere Protokolle, die vom Schannel-Anbieter verwendet werden, finden Sie unter [Schannel Security Support Provider Technical Reference](../tls/schannel-security-support-provider-technical-reference.md).

Speicherort: %windir%\Windows\System32\Schannel.dll

Dieser Anbieter wird standardmäßig in im genannten Versionen enthalten die **gilt für** Liste am Anfang dieses Themas, plus Windows Server2003 und Windows XP.

> [!NOTE]
> TLS 1.2 wurde in diesen Anbieter in Windows Server2008 R2 und Windows7 eingeführt. DTLS wurde in diesen Anbieter in Windows Server2012 und Windows8 eingeführt.

**Weitere Ressourcen für die Protokolle TLS und SSL und Schannel-SSP**

-   [Sicherer Kanal (Windows)](https://msdn.microsoft.com/library/aa380123(VS.85).aspx)

-   [Technische Referenz zu TLS/SSL](https://technet.microsoft.com/library/cc784149(v=ws.10).aspx)

-   [\[MS-TLSP\]: Transport Layer Security (TLS)-Profil](https://msdn.microsoft.com/library/dd207968(PROT.13).aspx)

### <a name="BKMK_NegoSSP"></a>Handeln Security Support Provider aus
Das Simple and Protected GSS-API-Aushandlung Mechanismus SPNEGO () bildet die Grundlage für die Negotiate-SSP Whichcan verwendet werden, um ein spezifisches Authentifizierungsprotokoll aushandeln. Wenn eine Anwendung in SSPI, melden Sie sich mit einem Netzwerk aufruft, kann einen SSP zum Verarbeiten der Anforderung angegeben werden. Wenn die Anwendung der Negotiate-SSP angegeben ist, analysiert die Anforderung und wählt den entsprechenden Anbieter zur Verarbeitung der Anforderung, basierend auf Kunden-konfigurierte Sicherheitsrichtlinien.

SPNEGO ist in RFC 2478 angegeben.

In unterstützten Versionen von Windows-Betriebssystemen unterstützt die Negotiate-Sicherheit Anbieter wählt zwischen dem Kerberos-Protokoll und NTLM. Wählt Aushandeln der Kerberos-Protokoll wird standardmäßig, sofern dieses Protokoll kann nicht von einer der in der Authentifizierung beteiligten Systeme verwendet werden, oder die aufrufende Anwendung wurde nicht genügend Informationen, um das Kerberos-Protokoll verwenden.

Speicherort: %windir%\Windows\System32\lsasrv.dll

Dieser Anbieter wird standardmäßig in im genannten Versionen enthalten die **gilt für** Liste am Anfang dieses Themas, plus Windows Server2003 und Windows XP.

**Zusätzliche Ressourcen für die Negotiate-SSP**

-   [Microsoft Aushandeln (Windows)](https://msdn.microsoft.com/library/aa378748(VS.85).aspx)

-   [\[MS-SPNG\]: Erweiterungen für einfache und geschützten GSS-API-Aushandlung Mechanismus (SPNEGO)](https://msdn.microsoft.com/library/cc247021(PROT.13).aspx)

-   [\[MS-N2HT\]: negotiate und HTTP-Authentifizierung Nego2 Protocol Specification](https://msdn.microsoft.com/library/dd303576(PROT.13).aspx)

### <a name="BKMK_CredSSP"></a>Credential Security Support Provider
Die Credential Security Service Provider (CredSSP) bietet einmaliges Anmelden (SSO) Benutzer bereitzustellen, beim neuen Terminaldienste und Remotedesktopdienste-Sitzungen starten. CredSSP ermöglicht es Anwendungen, Delegieren von Anmeldeinformationen von Benutzern vom Clientcomputer (mithilfe von der clientseitigen SSP) auf den Zielserver (über die serverseitige SSP), basierend auf dem Client-Richtlinien. CredSSP-Richtlinien mithilfe von Gruppenrichtlinien konfiguriert werden, und die Delegierung von Anmeldeinformationen ist standardmäßig deaktiviert.

Speicherort: %windir%\Windows\System32\credssp.dll

Dieser Anbieter wird standardmäßig in im genannten Versionen enthalten die **gilt für** -Liste am Anfang dieses Themas.

**Zusätzliche Ressourcen für die SSP-Anmeldeinformationen**

-   [\[MS-CSSP\]: credential Security Support Provider (CredSSP)-Protokoll-Spezifikation](https://msdn.microsoft.com/library/cc226764(PROT.13).aspx)

-   [Credential Security Service Provider und SSO für Terminal Services-Anmeldung](https://technet.microsoft.com/library/cc749211(v=ws.10).aspx)

### <a name="BKMK_NegoExtsSSP"></a>Handeln Sie Erweiterungen Security Support Provider aus
Erweiterungen Aushandeln (NegoExts) ist ein Authentifizierungspaket, die die Verwendung von SSPs, als NTLM oder Kerberos-Protokoll handelt, für Szenarien und Anwendungen von Microsoft und anderen Unternehmen implementiert.

Diese Erweiterung zum Aushandeln Paket kann die folgenden Szenarien:

-   **Rich Client-Verfügbarkeit in einem Verbund-System.** Dokumente auf SharePoint-Websites zugegriffen werden können, und sie können mithilfe einer Microsoft Office-Anwendung mit vollem Funktionsumfang bearbeitet werden.

-   **Rich Client für Microsoft Office-Dienste unterstützen.** Benutzer können melden Sie sich bei Microsoft Office-Dienste und verwenden eine Microsoft Office-Anwendung mit vollem Funktionsumfang.

-   **Gehostete Microsoft Exchange-Server und Outlook.** Es ist keine Vertrauensstellung eingerichtet werden, da Exchange-Server im Internet befindet. Outlook verwendet die Windows Live-Dienst zum Authentifizieren von Benutzern.

-   **Rich Client-Verfügbarkeit zwischen Clientcomputern und Servern.** Netzwerk- und Authentifizierung-Komponenten des Betriebssystems werden verwendet.

Das Windows-Aushandlung Paket behandelt der NegoExts-SSP auf die gleiche Weise wie bei Kerberos und NTLM. NegoExts.dll wird in der lokalen System Authority (LSA) beim Start geladen werden. Wenn eine Authentifizierungsanforderung basierend auf der Quelle der Anforderung empfangen wird, wird die NegoExts zwischen den unterstützten SSPs ausgehandelt. Es sammelt die Anmeldeinformationen und Richtlinien, verschlüsselt und sendet diese Informationen an die entsprechenden SSP, in der das Token erstellt wird.

Unterstützt von NegoExts SSPs sind nicht eigenständigen SSPs wie etwa Kerberos oder NTLM. Aus diesem Grund innerhalb der NegoExts-SSP, wird Wenn die Authentifizierungsmethode aus irgendeinem Grund fehlschlägt Fehlermeldung Fehler bei der Authentifizierung angezeigt oder protokolliert werden. Keine Neuverhandlung oder Fallback-Authentifizierungsmethoden sind möglich.

Speicherort: %windir%\Windows\System32\negoexts.dll

Dieser Anbieter wird standardmäßig in im genannten Versionen enthalten die **gilt für** Liste am Anfang dieses Themas, ausgenommen Windows Server2008 und Windows Vista.

### <a name="BKMK_PKU2USSP"></a>PKU2U-Security Support Provider
Der PKU2U-Protokoll wurde eingeführt und als ein SSP in Windows7 und Windows Server2008 R2 implementiert. Dieses SSP ermöglicht Peer-to-Peer-Authentifizierung, insbesondere durch die Medien und die Dateifreigabe, die Funktion Heimnetzgruppe, die in Windows7 eingeführt wurde. Das Feature ermöglicht die gemeinsame Nutzung von Computern, die nicht Mitglied einer Domäne sind.

Speicherort: %windir%\Windows\System32\pku2u.dll

Dieser Anbieter wird standardmäßig in im genannten Versionen enthalten die **gilt für** Liste am Anfang dieses Themas, ausgenommen Windows Server2008 und Windows Vista.

**Weitere Ressourcen für das PKU2U-Protokoll und der PKU2U-SSP**

-   [Einführung in die Online-Identitätsanbieter-Integration](https://technet.microsoft.com/library/dd560662(v=ws.10).aspx)

## <a name="BKMK_SecuritySupportProviderSelection"></a>Security Support Provider-Auswahl
Die Windows-SSPI können eines der Protokolle, die über die installierte Security Support Provider unterstützt werden. Aber da nicht alle Betriebssystemen die gleichen SSP-Pakete als einem bestimmten Computer unter Windows Server unterstützt, müssen Clients und Server aushandeln ein Protokoll verwendet, die beide unterstützen. Windows Server bevorzugt Clientcomputern und Anwendungen Kerberos-Protokoll ein sicheres standardbasierte Protokoll verwenden, wenn möglich, aber das Betriebssystem fortgesetzt wird, Clientcomputer und Clients zu ermöglichen, die das Kerberos-Protokoll zur Authentifizierung nicht unterstützen.

Damit Authentifizierung Ort der beiden kommuniziert werden kann müssen Computer auf ein Protokoll erklären sich damit einverstanden, dass beide unterstützen können. Für alle Protokolle über die SSPI verwendet werden muss jeder Computer die entsprechende SSP verfügen. Beispielsweise müssen für einen Clientcomputer und der Server für das Kerberos-Authentifizierungsprotokoll verwenden, sie sowohl Kerberos v5 unterstützen. Windows Server verwendet die Funktion **EnumerateSecurityPackages** um zu identifizieren, welche SSPs unterstützt werden, auf einem Computer und was die Funktionen des diese SSPs sind.

In einem der folgenden beiden Methoden kann die Auswahl der Authentifizierungsprotokoll behandelt werden:

1.  [Einzelne-Authentifizierungsprotokoll](#BKMK_SingleAuth)

2.  [Option aushandeln](#BKMK_Negotiate)

### <a name="BKMK_SingleAuth"></a>Einzelne-Authentifizierungsprotokoll
Wenn ein einzelnes akzeptabel Protokoll auf dem Server angegeben ist, muss der Clientcomputer das angegebene Protokoll oder die Kommunikation schlägt fehl unterstützen. Wenn ein einzelnes akzeptabel Protokoll angegeben ist, erfolgt die Authentifizierung Exchange wie folgt:

1.  Der Clientcomputer fordert den Zugriff auf einen Dienst.

2.  Der Server antwortet auf die Anforderung und gibt das Protokoll, das verwendet wird.

3.  Der Clientcomputer überprüft den Inhalt der Antwort und überprüft, um zu bestimmen, ob das angegebene Protokoll unterstützt. Wenn der Clientcomputer auf das angegebene Protokoll unterstützt wird, wird die Authentifizierung fortgesetzt. Wenn der Clientcomputer das Protokoll nicht unterstützt, die schlägt die Authentifizierung fehl, unabhängig davon, ob der Clientcomputer autorisiert ist, auf die Ressource zuzugreifen.

### <a name="BKMK_Negotiate"></a>Option aushandeln
Der Negotiate-Option kann verwendet werden, auf dem Client und Server versucht, eine akzeptable Protokoll finden können. Dies basiert auf der Simple and Protected GSS-API-Aushandlung Mechanismus SPNEGO (). Wenn die Authentifizierung mit der Option für ein Authentifizierungsprotokoll aushandeln beginnt, findet die SPNEGO Exchange wie folgt:

1.  Der Clientcomputer fordert den Zugriff auf einen Dienst.

2.  Der Server antwortet mit einer Liste von Authentifizierungsprotokollen, die dies unterstützen kann und eine authentifizierungsaufforderung oder die Antwort, anhand des Protokolls, das die erste Wahl ist. Der Server kann z.B. sind die Kerberos-Protokoll und NTLM und senden eine Antwort des Kerberos-Authentifizierung.

3.  Der Clientcomputer überprüft den Inhalt der Antwort und überprüft, um zu bestimmen, ob eines der angegebenen Protokolle unterstützt.

    -   Wenn der Clientcomputer das bevorzugte Protokoll unterstützt, wird die Authentifizierung fortgesetzt.

    -   Wenn der Clientcomputer unterstützt nicht das bevorzugte Protokoll, aber es eines anderen Protokolle aufgeführt, die vom Server unterstützt, kann die Clientcomputer den Server wissen, welche Authentifizierungsprotokoll unterstützt, und die Authentifizierung wird fortgesetzt.

    -   Wenn der Clientcomputer eines der aufgeführten Protokolle nicht unterstützt wird, tritt ein Fehler Authentifizierung.

## <a name="see-also"></a>Siehe auch
[Architektur der Windows-Authentifizierung](https://technet.microsoft.com/library/dn169024(v=ws.10).aspx)


