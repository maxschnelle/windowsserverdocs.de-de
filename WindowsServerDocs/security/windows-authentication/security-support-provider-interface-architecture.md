---
title: Architektur der SecuritySupportProvider-Schnittstelle
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
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59827021"
---
# <a name="security-support-provider-interface-architecture"></a>Architektur der SecuritySupportProvider-Schnittstelle

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

In diesem Referenzthema für IT-Experten wird beschrieben, die Windows-Authentifizierungsprotokolle, die innerhalb der Architektur der Security Support Provider Interface (SSPI) verwendet werden.

Das Microsoft Security Support Provider Interface (SSPI) ist die Grundlage für die Windows-Authentifizierung. Verwenden SSPI bereitstellen, Anwendungen und Infrastrukturdienste, die eine Authentifizierung erfordern.

SSPI ist die Implementierung von der generischen Security Service API (GSSAPI) in Windows Server-Betriebssystemen. Weitere Informationen über die GSSAPI finden Sie unter RFC 2743 und RFC 2744 in der IETF RFC-Datenbank.

Der Standardwert Security Support Provider (SSP), die bestimmte Authentifizierungsprotokolle in Windows aufrufen, werden in der SSPI als DLLs integriert. Diese Standard-SSPs werden in den folgenden Abschnitten beschrieben. Zusätzliche SSPs können integriert werden, wenn sie mit der SSPI ausgeführt werden können.

Wie in der folgenden Abbildung gezeigt, enthält die SSPI in Windows einen Mechanismus, der Authentifizierungstoken für den vorhandenen Kommunikationskanal zwischen dem Clientcomputer und dem Server ausführt. Wenn zwei Computer oder Geräte müssen authentifiziert werden, sodass sie sicher kommunizieren können, werden die Anforderungen für die Authentifizierung auf die SSPI weitergeleitet, die Abschluss des Authentifizierungsprozesses, unabhängig von der derzeit verwendete Netzwerkprotokoll. Die SSPI gibt transparent binary large Object zurück. Diese werden zwischen den Anwendungen, übergeben an diesem, die Punkt sie an die SSPI-Schicht übergeben werden können. Die SSPI ermöglicht daher eine Anwendung verschiedene Sicherheitsmodelle verfügbar auf einem Computer oder Netzwerk zu verwenden, ohne die Schnittstelle für das Sicherheitssystem ändern zu müssen.

![Diagramm zeigt die Security Support Provider-Schnittstelle-Architektur](../media/security-support-provider-interface-architecture/AuthN_SecuritySupportProviderInterfaceArchitecture.jpg)

Den folgenden Abschnitten werden die Standard-SSPs die Interaktion mit der SSPI. Die SSPs werden auf unterschiedliche Weise in Windows-Betriebssystemen zur Förderung der sicheren Kommunikation in einer unsicheren Netzwerkverbindung-Umgebung verwendet.

-   [Kerberos Security Support Provider](#BKMK_KerbSSP)

-   [Anbieter für technischen Support für NTLM-Sicherheit](#BKMK_NTLMSSP)

-   [Digest-Security Support Provider](#BKMK_DigestSSP)

-   [Schannel-Security Support Provider](#BKMK_SchannelSSP)

-   [Negotiate Security Support Provider](#BKMK_NegoSSP)

-   [Credential Security Support Provider](#BKMK_CredSSP)

-   [Extensions-Security Support Providers ausgehandelt](#BKMK_NegoExtsSSP)

-   [PKU2U-Security Support Provider](#BKMK_PKU2USSP)

Auch enthalten in diesem Thema:

[Security Support Provider-Auswahl](security-support-provider-interface-architecture.md#BKMK_SecuritySupportProviderSelection)

### <a name="BKMK_KerbSSP"></a>Anbieter für technischen Support für Kerberos-Sicherheit
Dieses SSP verwendet nur das Kerberos V5-Protokoll an, wie von Microsoft implementiert. Dieses Protokoll basiert auf dem Netzwerk Working Group des RFC 4120 und Draft Revisionen. Es ist ein Industriestandardprotokoll, die für eine interaktive Anmeldung mit einem Kennwort oder eine Smartcard verwendet wird. Es ist auch die bevorzugte Authentifizierungsmethode für Dienste in Windows.

Da das Kerberos-Protokoll das standardmäßig verwendete Authentifizierungsprotokoll seit Windows 2000 wurde, unterstützen alle Domänendienste die Kerberos SSP. Hierzu gehören:

-   Active Directory-Abfragen, die der Lightweight Directory Access Protocol (LDAP) verwenden.

-   Server oder einer Arbeitsstation Remoteverwaltung, der den Remoteprozeduraufruf-Dienst verwendet.

-   Druckdienste

-   Client / Server-Authentifizierung

-   Remotezugriff auf Dateien mit dem Server Message Block (SMB) Protokoll (auch bekannt als Common Internet File System oder CIFS)

-   DFS-systemverwaltung und Verweis

-   Intranetauthentifizierung auf IIS (Internetinformationsdienste)

-   Sicherheitsauthentifizierung über die Autorität für Internet Protocol Security (IPsec)

-   Zertifikatanforderungen an Active Directory-Zertifikatdienste für Domänenbenutzer und-Computer

Location: %windir%\Windows\System32\kerberos.dll

Dieser Anbieter ist standardmäßig in im genannten Versionen enthalten die **gilt für** Liste am Anfang dieses Themas, plus Windows Server 2003 und Windows XP.

**Zusätzliche Ressourcen für das Kerberos-Protokoll und der Kerberos-SSP**

-   [Microsoft Kerberos (Windows)](https://msdn.microsoft.com/library/aa378747(VS.85).aspx)

-   [\[MS-KILE\]: Kerberos-Protokollerweiterungen](https://msdn.microsoft.com/library/cc233855(PROT.10).aspx)

-   [\[MS-SFU\]: Kerberos-Protokollerweiterungen: Service for-User und eingeschränkte Delegierung Protokollspezifikation](https://msdn.microsoft.com/library/cc246071(PROT.13).aspx)

-   [Kerberos SSP/AP (Windows)](https://msdn.microsoft.com/library/aa377942(VS.85).aspx)

-   [Kerberos-Erweiterungen](https://technet.microsoft.com/library/cc749438(v=ws.10).aspx) für Windows Vista

-   [Änderungen bei der Kerberosauthentifizierung](https://technet.microsoft.com/library/dd560670(v=ws.10).aspx) für Windows 7 

-   [Technische Referenz für die Kerberos-Authentifizierung](https://technet.microsoft.com/library/cc739058(v=ws.10).aspx)

### <a name="BKMK_NTLMSSP"></a>Anbieter für technischen Support für NTLM-Sicherheit
Die NTLM-Security Support Provider (NTLM-SSP) ist eine Binärdatei, die messaging-Protokoll, das durch die Security Support Provider Interface (SSPI) verwendet, um NTLM-Abfrage / Rückmeldung-Authentifizierung zu ermöglichen und zum Aushandeln der Integrität und Vertraulichkeit Optionen. NTLM wird verwendet, wenn es sich bei SSPI-Authentifizierung verwendet wird, einschließlich für Server Message Block oder CIFS-Authentifizierung, HTTP-Negotiate-Authentifizierung (z. B. Internet-Webauthentifizierung) und den Remoteprozeduraufruf-Dienst. Die NTLM-SSP enthält, die NTLM und NTLM, Version 2 (NTLMv2)-Authentifizierungsprotokolle.

Die unterstützten Windows-Betriebssysteme können die NTLM-SSP für Folgendes verwenden:

-   Client/Server-Authentifizierung

-   Druckdienste

-   Dateizugriff mit CIFS (SMB)

-   Sichere Remoteprozeduraufruf-Dienst oder DCOM-Dienst

Location: %windir%\Windows\System32\msv1_0.dll

Dieser Anbieter ist standardmäßig in im genannten Versionen enthalten die **gilt für** Liste am Anfang dieses Themas, plus Windows Server 2003 und Windows XP.

**Zusätzliche Ressourcen für die NTLM-Authentifizierungsprotokoll und die NTLM-SSP**

-   [MSV1_0-Authentifizierungspaket (Windows)](https://msdn.microsoft.com/library/aa378753(VS.85).aspx)

-   [Änderungen bei der NTLM-Authentifizierung](https://technet.microsoft.com/library/dd566199(v=ws.10).aspx) in Windows 7 

-   [Microsoft NTLM (Windows)](https://msdn.microsoft.com/library/aa378749(VS.85).aspx)

-   [Überwachung und Einschränkung der NTLM-Benutzerhandbuch](https://technet.microsoft.com/library/jj865674(v=ws.10).aspx)

### <a name="BKMK_DigestSSP"></a>Digest-Security Support Provider
Digestauthentifizierung ist ein Industriestandard, das für Lightweight Directory Access Protocol (LDAP) und die Webauthentifizierung verwendet wird. Digestauthentifizierung übertragen Anmeldeinformationen über das Netzwerk als ein MD5-Hash oder Digest.

Digest-SSP (Wdigest.dll) wird für Folgendes verwendet:

-   Internet Explorer und Internet Information Services (IIS)-Zugriff

-   LDAP-Abfragen

Location: %windir%\Windows\System32\Digest.dll

Dieser Anbieter ist standardmäßig in im genannten Versionen enthalten die **gilt für** Liste am Anfang dieses Themas, plus Windows Server 2003 und Windows XP.

**Zusätzliche Ressourcen für das Digest-Protokoll und der Digest-SSP**

-   [Microsoft Digest-Authentifizierung (Windows)](https://msdn.microsoft.com/library/aa378745(VS.85).aspx)

-   [\[MS-DPSP\]: Digest-Protocol-Erweiterungen](https://msdn.microsoft.com/library/cc227906(PROT.13).aspx)

### <a name="BKMK_SchannelSSP"></a>Schannel-Security Support Provider
Das Secure Channel (Schannel) wird verwendet, für die Web-basierte Server-Authentifizierung, z. B. wenn ein Benutzer versucht, einen sicheren Webserver zuzugreifen.

Das TLS-Protokoll, SSL-Protokoll, das Private Communications Technology (PCT)-Protokoll und das Datagram Transport Layer (DTLS)-Protokoll basieren auf Kryptografie mit öffentlichem Schlüssel. Schannel enthält alle diese Protokolle. Alle Schannel-Protokolle verwenden ein Client/Server-Modell. Der Schannel SSP verwendet Zertifikate für öffentliche Schlüssel zum Authentifizieren von Parteien. Beim Authentifizieren von Parteien wählt Schannel-SSP ein Protokoll in der folgenden Reihenfolge ihrer Priorität:

-   Transport Layer Security (TLS) Version 1.0

-   Transport Layer Security (TLS) Version 1.1

-   Transport Layer Security (TLS) Version 1.2

-   Secure Socket Layer (SSL) Version 2.0

-   Secure Socket Layer (SSL) Version 3.0

-   Private Communications Technology (PCT)

    **Beachten Sie** PCT ist standardmäßig deaktiviert.

Das Protokoll, das ausgewählt ist, ist das bevorzugte Authentifizierungsprotokoll, das der Client und Server unterstützen kann. Beispielsweise verwendet der Authentifizierungsprozess Wenn ein Server alle Schannel-Protokolle unterstützt, und der Client nur SSL 3.0 und SSL 2.0 unterstützt, SSL 3.0.

DTLS wird verwendet, wenn von der Anwendung explizit aufgerufen wird. Weitere Informationen über DTLS und die anderen Protokolle, die vom Schannel-Anbieter verwendet werden, finden Sie unter [technische Referenz für Schannel Security Support Provider](../tls/schannel-security-support-provider-technical-reference.md).

Location: %windir%\Windows\System32\Schannel.dll

Dieser Anbieter ist standardmäßig in im genannten Versionen enthalten die **gilt für** Liste am Anfang dieses Themas, plus Windows Server 2003 und Windows XP.

> [!NOTE]
> TLS 1.2 wurde in diesem Anbieter in Windows Server 2008 R2 und Windows 7 eingeführt. DTLS wurde in diesem Anbieter in Windows Server 2012 und Windows 8 eingeführt.

**Zusätzliche Ressourcen für die Protokolle TLS und SSL und Schannel-SSP**

-   [Sicherer Kanal (Windows)](https://msdn.microsoft.com/library/aa380123(VS.85).aspx)

-   [Technische Referenz zu TLS/SSL](https://technet.microsoft.com/library/cc784149(v=ws.10).aspx)

-   [\[MS-TLSP\]: Transport Layer Security (TLS)-Profil](https://msdn.microsoft.com/library/dd207968(PROT.13).aspx)

### <a name="BKMK_NegoSSP"></a>Negotiate Security Support Provider
Die Simple and Protected GSS-API Negotiation Mechanismus (SPNEGO), bildet die Grundlage für den SSP aushandeln Whichcan verwendet werden, um ein spezifisches Authentifizierungsprotokoll aushandeln. Wenn eine Anwendung SSPI zur Anmeldung mit einem Netzwerk aufruft, kann einen SSP zur Verarbeitung der Anforderung angegeben werden. Wenn die Anwendung die Negotiate-SSP angegeben ist, analysiert die Anforderung und wählt den entsprechenden Anbieter zur Verarbeitung der Anforderung, basierend auf von Kunden konfigurierte Sicherheitsrichtlinien.

SPNEGO ist in RFC 2478 angegeben.

Klicken Sie in unterstützten Versionen der Windows-Betriebssysteme die Sicherheit aushandeln Anbieter wählt zwischen Kerberos und NTLM unterstützen. Aushandeln von SELECT-Anweisungen die Kerberos-Protokoll wird standardmäßig ausgeführt, wenn dieses Protokoll kann nicht von einem der Systeme, die bei der Authentifizierung beteiligten verwendet werden oder die aufrufende Anwendung hat nicht genügend Informationen zur Nutzung des Kerberos-Protokolls bereitgestellt.

Location: %windir%\Windows\System32\lsasrv.dll

Dieser Anbieter ist standardmäßig in im genannten Versionen enthalten die **gilt für** Liste am Anfang dieses Themas, plus Windows Server 2003 und Windows XP.

**Zusätzliche Ressourcen für den SSP aushandeln**

-   [Microsoft Aushandeln (Windows)](https://msdn.microsoft.com/library/aa378748(VS.85).aspx)

-   [\[MS-SPNG\]: Einfache und geschützte GSS-API-Aushandlung-Mechanismus (SPNEGO)-Erweiterungen](https://msdn.microsoft.com/library/cc247021(PROT.13).aspx)

-   [\[MS-N2HT\]: Aushandeln und HTTP-Authentifizierung Nego2 Protokoll-Spezifikation](https://msdn.microsoft.com/library/dd303576(PROT.13).aspx)

### <a name="BKMK_CredSSP"></a>Credential Security Support Provider
Die Credential Security Service Provider (CredSSP) bietet eine einmalige Anmelden (SSO) Benutzeroberfläche beim Starten der neuer "Terminal Services" und Remotedesktopdienste-Sitzungen. CredSSP ermöglicht Anwendungen die Anmeldeinformationen des Benutzers (mithilfe den clientseitigen-SSP) vom Clientcomputer zu delegieren, auf dem Zielserver (über den serverseitigen-SSP), basierend auf dem Client-Richtlinien. CredSSP-Richtlinien mithilfe einer Gruppenrichtlinie konfiguriert werden, und die Delegierung von Anmeldeinformationen ist standardmäßig deaktiviert.

Location: %windir%\Windows\System32\credssp.dll

Dieser Anbieter ist standardmäßig in im genannten Versionen enthalten die **gilt für** Liste am Anfang dieses Themas.

**Zusätzliche Ressourcen für die SSP-Anmeldeinformationen**

-   [\[MS-CSSP\]: Credential Security Support Provider (CredSSP)-Protokollspezifikation](https://msdn.microsoft.com/library/cc226764(PROT.13).aspx)

-   [Credential Security Service Provider und SSO für Terminaldienste-Indikator Services-Anmeldung](https://technet.microsoft.com/library/cc749211(v=ws.10).aspx)

### <a name="BKMK_NegoExtsSSP"></a>Extensions-Security Support Providers ausgehandelt
Aushandeln von Extensions (NegoExts) ist ein Authentifizierungspaket, das die Verwendung von SSPs, als NTLM oder Kerberos-Protokoll handelt, für Anwendungen und Szenarien von Software von Microsoft und anderen Unternehmen implementiert.

Diese Erweiterung für das Aushandlungspaket ermöglicht die folgenden Szenarien:

-   **Rich Client-Verfügbarkeit bei einem zusammengeschlossenen System.** Dokumente auf SharePoint-Websites zugegriffen werden können, und sie können mithilfe einer umfassenden Microsoft Office-Anwendung bearbeitet werden.

-   **Rich-Client für Microsoft Office-Dienste unterstützen.** Benutzer können melden Sie sich beim Microsoft Office-Dienste und umfassenden Microsoft Office-Anwendung verwenden.

-   **Gehosteter Microsoft Exchange-Server und Outlook.** Es ist keine Vertrauensstellung hergestellt werden, da Exchange-Server im Internet gehostet wird. Outlook verwendet die Windows Live-Dienst zum Authentifizieren von Benutzern.

-   **Rich Client-Verfügbarkeit zwischen Clientcomputern und Servern.** Das Betriebssystem Netzwerk- und -Komponenten werden verwendet.

Das Paket Windows aushandeln behandelt der NegoExts SSP auf die gleiche Weise, wie bei Kerberos und NTLM. NegoExts.dll wird in der lokalen System Authority (LSA) beim Start geladen werden. Wenn eine Authentifizierungsanforderung basierend auf der Quelle der Anforderung empfangen wird, wird Sie zwischen den unterstützten SSPs NegoExts ausgehandelt. Dieses Tool sammelt die Anmeldeinformationen und Richtlinien, verschlüsselt sie und sendet diese Informationen an die entsprechenden SSP, in dem das Sicherheitstoken erstellt wird.

Die SSPs von NegoExts unterstützt sind keine eigenständigen SSPs wie z. B. Kerberos und NTLM. Aus diesem Grund innerhalb der NegoExts SSP, wird Wenn die Authentifizierungsmethode aus irgendeinem Grund keine Fehler-Nachricht angezeigt oder protokolliert werden. Keine erneute Aushandlung oder Fallback-Authentifizierungsmethoden sind möglich.

Location: %windir%\Windows\System32\negoexts.dll

Dieser Anbieter ist standardmäßig in im genannten Versionen enthalten die **gilt für** Liste am Anfang dieses Themas ohne Windows Server 2008 und Windows Vista.

### <a name="BKMK_PKU2USSP"></a>PKU2U-Security Support Provider
Das PKU2U-Protokoll wurde eingeführt und als ein SSP in Windows 7 und Windows Server 2008 R2 implementiert. Dieses SSP aktiviert die Peer-zu-Peer-Authentifizierung, insbesondere bei Verwendung der Medien und die Dateifreigabe-Funktion mit der Bezeichnung Heimnetzgruppe, die in Windows 7 eingeführt wurde. Das Feature ermöglicht die gemeinsame Datennutzung von Computern, die nicht Mitglied einer Domäne sind.

Location: %windir%\Windows\System32\pku2u.dll

Dieser Anbieter ist standardmäßig in im genannten Versionen enthalten die **gilt für** Liste am Anfang dieses Themas ohne Windows Server 2008 und Windows Vista.

**Zusätzliche Ressourcen für das PKU2U-Protokoll und der PKU2U-SSP**

-   [Einführung in die Integration von Online-Identität](https://technet.microsoft.com/library/dd560662(v=ws.10).aspx)

## <a name="BKMK_SecuritySupportProviderSelection"></a>Security Support Provider-Auswahl
Die Windows-SSPI können die Protokolle, die über die installierten Security Support Provider unterstützt werden. Aber da nicht alle Betriebssysteme, die gleichen SSP-Pakete als einem Computer unter Windows Server unterstützen, müssen Clients und Servern aushandeln ein Protokoll zu verwenden, die beide unterstützen. Windows Server bevorzugt, Clientcomputer und Anwendungen für die Verwendung von Kerberos-Protokoll eine sichere standardbasierte Protokoll, wenn möglich, aber das Betriebssystem fortgesetzt wird, um Clientcomputer und Clients Anwendungen zu ermöglichen, die die Kerberos nicht unterstützen Protokoll zur Authentifizierung.

Damit Authentifizierung Ort der beiden kommuniziert werden müssen Computer auf ein Protokoll zustimmen, dass beide unterstützen können. Für ein Protokoll über die SSPI verwendet werden kann muss jeder Computer die entsprechenden SSP verfügen. Beispielsweise müssen für einen Clientcomputer und Server das Kerberos-Authentifizierungsprotokoll verwendet, sie sowohl Kerberos v5 unterstützen. Windows Server verwendet die Funktion **EnumerateSecurityPackages** sind die Funktionen dieser SSPs um zu identifizieren, welche SSPs auf einem Computer und was unterstützt werden.

Die Auswahl eines Authentifizierungsprotokolls kann in einem der beiden folgenden Methoden behandelt werden:

1.  [Einzelne-Authentifizierungsprotokoll](#BKMK_SingleAuth)

2.  [Negotiate-option](#BKMK_Negotiate)

### <a name="BKMK_SingleAuth"></a>Einzelne-Authentifizierungsprotokoll
Wenn ein einzelnes zulässiges Protokoll auf dem Server angegeben wird, muss der Clientcomputer unterstützen, das angegebene Protokoll oder die Kommunikation schlägt fehl. Wenn ein einzelnes zulässiges Protokoll angegeben ist, erfolgt die Authentifizierung wie folgt:

1.  Der Clientcomputer fordert Zugriff auf einen Dienst.

2.  Der Server antwortet auf die Anforderung und gibt das Protokoll, das verwendet wird.

3.  Der Clientcomputer überprüft den Inhalt der Antwort und Überprüfungen für die Bestimmung, ob das angegebene Protokoll unterstützt. Wenn der Clientcomputer auf das angegebene Protokoll unterstützt wird, wird die Authentifizierung fortgesetzt. Wenn der Client-Computer das Protokoll nicht unterstützt, schlägt die Authentifizierung fehl, unabhängig davon, ob der Client-Computer autorisiert ist, auf die Ressource zuzugreifen.

### <a name="BKMK_Negotiate"></a>Negotiate-option
Die Negotiate-Option kann verwendet werden, können Client und Server versucht, eine akzeptable Protokoll zu finden. Dies basiert auf der Simple and Protected GSS-API Negotiation Mechanismus (SPNEGO). Wenn die Authentifizierung mit der Option für ein Authentifizierungsprotokoll aushandeln beginnt, findet der SPNEGO-Austausch wie folgt:

1.  Der Clientcomputer fordert Zugriff auf einen Dienst.

2.  Der Server antwortet mit einer Liste von Authentifizierungsprotokollen, die es unterstützen kann und eine authentifizierungsaufforderung oder Antwort basierend auf dem Protokoll, das die erste Wahl ist. Der Server kann z. B. Listen Sie die Kerberos-Protokoll und NTLM und sendet eine Antwort der Kerberos-Authentifizierung.

3.  Der Clientcomputer überprüft den Inhalt der Antwort und Überprüfungen für die Bestimmung, ob die angegebenen Protokolle unterstützt.

    -   Wenn der Client-Computer das bevorzugte Protokoll unterstützt, wird die Authentifizierung fortgesetzt.

    -   Wenn der Client-Computer unterstützt nicht das bevorzugte Protokoll, aber es eines der anderen Protokolle aufgelistet, die vom Server unterstützt, kann die Client-Computer den Server weiß, welche die unterstützte Authentifizierungsprotokoll an, und die Authentifizierung geht.

    -   Der Clientcomputer die aufgeführten Protokolle nicht unterstützt, der Authentifizierungsaustausch schlägt fehl.

## <a name="see-also"></a>Siehe auch
[Architektur der Windows-Authentifizierung](https://technet.microsoft.com/library/dn169024(v=ws.10).aspx)


