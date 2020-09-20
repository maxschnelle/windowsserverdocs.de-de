---
title: Architektur der Security Support Provider-Schnittstelle
description: Windows Server-Sicherheit
ms.topic: article
ms.assetid: de09e099-5711-48f8-adbd-e7b8093a0336
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/12/2016
ms.openlocfilehash: da7c390427a3f0f2348d91e14d0affef905db390
ms.sourcegitcommit: 5344adcf9c0462561a4f9d47d80afc1d095a5b13
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/18/2020
ms.locfileid: "90766953"
---
# <a name="security-support-provider-interface-architecture"></a>Architektur der Security Support Provider-Schnittstelle

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In diesem Referenz Thema für IT-Experten werden die Windows-Authentifizierungsprotokolle beschrieben, die in der SSPI-Architektur (Security Support Provider Interface) verwendet werden.

Die Microsoft Security Support Provider-Schnittstelle (SSPI) ist die Grundlage für die Windows-Authentifizierung. Anwendungen und Infrastrukturdienste, die eine Authentifizierung erfordern, verwenden SSPI, um es bereitzustellen.

SSPI ist die Implementierung der generischen Security Service-API (GSSAPI) in Windows Server-Betriebssystemen. Weitere Informationen zu GSSAPI finden Sie unter RFC 2743 und RFC 2744 in der IETF RFC-Datenbank.

Die Standard-SSPs (Security Support Providers), die in Windows bestimmte Authentifizierungsprotokolle aufrufen, sind in die SSPI als DLLs integriert. Diese standardmäßigen SSPs werden in den folgenden Abschnitten beschrieben. Weitere SSPs können integriert werden, wenn Sie mit der SSPI betrieben werden können.

Wie in der folgenden Abbildung gezeigt, stellt die SSPI in Windows einen Mechanismus bereit, der Authentifizierungs Token über den vorhandenen Kommunikationskanal zwischen dem Client Computer und dem Server enthält. Wenn zwei Computer oder Geräte authentifiziert werden müssen, damit Sie sicher kommunizieren können, werden die Authentifizierungsanforderungen an die SSPI weitergeleitet, die den Authentifizierungs Vorgang unabhängig vom derzeit verwendeten Netzwerkprotokoll abschließt. Die SSPI gibt transparente binäre große Objekte zurück. Diese werden zwischen den Anwendungen übermittelt. an diesem Punkt können Sie an die SSPI-Schicht übermittelt werden. Auf diese Weise kann eine Anwendung mithilfe der SSPI verschiedene Sicherheitsmodelle verwenden, die auf einem Computer oder Netzwerk verfügbar sind, ohne dass die Schnittstelle zum Sicherheitssystem geändert werden muss.

![Diagramm mit der Architektur der Security Support Provider-Schnittstelle](../media/security-support-provider-interface-architecture/AuthN_SecuritySupportProviderInterfaceArchitecture.jpg)

In den folgenden Abschnitten werden die standardmäßigen SSPs beschrieben, die mit der SSPI interagieren. Die SSPs werden in Windows-Betriebssystemen auf unterschiedliche Weise verwendet, um eine sichere Kommunikation in einer unsicheren Netzwerkumgebung zu fördern.

-   [Kerberos-Sicherheits Unterstützungs Anbieter](#BKMK_KerbSSP)

-   [NTLM-Sicherheits Unterstützungs Anbieter](#BKMK_NTLMSSP)

-   [Digest-Sicherheits Unterstützungs Anbieter](#BKMK_DigestSSP)

-   [SChannel Security Support Provider](#BKMK_SchannelSSP)

-   [Sicherheits Unterstützungs Anbieter aushandeln](#BKMK_NegoSSP)

-   [Anmelde Informationsanbieter für Sicherheitsunterstützung](#BKMK_CredSSP)

-   [Extensions für den Sicherheitsunterstützungs Anbieter aushandeln](#BKMK_NegoExtsSSP)

-   [PKU2U Security Support Provider](#BKMK_PKU2USSP)

Auch in diesem Thema enthalten:

[Auswahl des Sicherheits Unterstützungs Anbieters](security-support-provider-interface-architecture.md#BKMK_SecuritySupportProviderSelection)

### <a name="kerberos-security-support-provider"></a><a name="BKMK_KerbSSP"></a>Kerberos-Sicherheits Unterstützungs Anbieter
Dieser SSP verwendet nur das Kerberos 5-Protokoll, das von Microsoft implementiert wird. Dieses Protokoll basiert auf den RFC 4120 und den Entwurfs Revisionen der Netzwerk Arbeitsgruppe. Dabei handelt es sich um ein Industriestandard Protokoll, das mit einem Kennwort oder einer Smartcard für eine interaktive Anmeldung verwendet wird. Es ist auch die bevorzugte Authentifizierungsmethode für Dienste in Windows.

Da das Kerberos-Protokoll seit Windows 2000 das Standard Authentifizierungsprotokoll ist, unterstützen alle Domänen Dienste den Kerberos-SSP. Zu diesen Diensten gehören:

-   Active Directory Abfragen, die das Lightweight Directory Access Protocol (LDAP) verwenden

-   Remote Server-oder Arbeitsstations Verwaltung, die den Remote Prozedur aufrufsdienst verwendet

-   Druckdienste

-   Client-Server-Authentifizierung

-   Remote Dateizugriff, bei dem das SMB-Protokoll (Server Message Block) verwendet wird (auch bekannt als Common Internet File System oder CIFS)

-   Verteilte Dateisystem Verwaltung und-Referenz

-   Intranetauthentifizierung zu Internetinformationsdienste (IIS)

-   Sicherheits Autoritäts Authentifizierung für die Internet Protokoll Sicherheit (IPSec)

-   Zertifikat Anforderungen an Active Directory Zertifikat Dienste für Domänen Benutzer und-Computer

Speicherort:% windir% \Windows\System32\kerberos.dll

Dieser Anbieter ist standardmäßig in Versionen enthalten, die in der Liste **gilt für** am Anfang dieses Themas angegeben sind, sowie unter Windows Server 2003 und Windows XP.

**Zusätzliche Ressourcen für das Kerberos-Protokoll und den Kerberos-SSP**

-   [Microsoft Kerberos (Windows)](/windows/win32/secauthn/microsoft-kerberos)

-   [\[MS-kile \] : Kerberos-Protokoll Erweiterungen](/openspecs/windows_protocols/ms-kile/2a32282e-dd48-4ad9-a542-609804b02cc9)

-   [\[MS-SFU \] : Kerberos-Protokoll Erweiterungen: Dienst für Benutzer und eingeschränkte Delegierungs Protokollspezifikation](/openspecs/windows_protocols/ms-sfu/3bff5864-8135-400e-bdd9-33b552051d94)

-   [Kerberos SSP/AP (Windows)](/windows/win32/secauthn/kerberos-ssp-ap)

-   [Kerberos-Erweiterungen](/previous-versions/windows/it-pro/windows-vista/cc749438(v=ws.10)) für Windows Vista

-   [Änderungen bei der Kerberos-Authentifizierung](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd560670(v=ws.10)) für Windows 7

-   [Technische Referenz für die Kerberos-Authentifizierung](/previous-versions/windows/it-pro/windows-server-2003/cc739058(v=ws.10))

### <a name="ntlm-security-support-provider"></a><a name="BKMK_NTLMSSP"></a>NTLM-Sicherheits Unterstützungs Anbieter
Der NTLM-Sicherheits Unterstützungs Anbieter (NTLM SSP) ist ein binäres Messaging Protokoll, das von der Security Support Provider-Schnittstelle (SSPI) verwendet wird, um die NTLM-Challenge-Response-Authentifizierung zuzulassen und Integritäts-und Vertraulichkeits Optionen auszuhandeln. NTLM wird verwendet, wenn die SSPI-Authentifizierung verwendet wird, z. b. für Server Message Block oder CIFS-Authentifizierung, http-Aushandlungs Authentifizierung (z. b. Internet-Webauthentifizierung) und den Remote Prozedur aufrufsdienst. Der NTLM-SSP umfasst die NTLM-und NTLM Version 2 (NTLMv2)-Authentifizierungsprotokolle.

Die unterstützten Windows-Betriebssysteme können den NTLM-SSP für Folgendes verwenden:

-   Client/Server-Authentifizierung

-   Druckdienste

-   Dateizugriff mithilfe von CIFS (SMB)

-   Sicherer Remote Prozedur aufrufsdienst oder DCOM-Dienst

Speicherort:% windir% \Windows\System32\msv1_0.dll

Dieser Anbieter ist standardmäßig in Versionen enthalten, die in der Liste **gilt für** am Anfang dieses Themas angegeben sind, sowie unter Windows Server 2003 und Windows XP.

**Zusätzliche Ressourcen für das NTLM-Protokoll und den NTLM-SSP**

-   [MSV1_0 Authentifizierungs Paket (Windows)](/windows/win32/secauthn/msv1-0-authentication-package)

-   [Änderungen bei der NTLM-Authentifizierung](/previous-versions/windows/it-pro/windows-7/dd566199(v=ws.10)) in Windows 7

-   [Microsoft NTLM (Windows)](/windows/win32/secauthn/microsoft-ntlm)

-   [Handbuch zur Überwachung und Einschränkung der NTLM-Verwendung](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/jj865674(v=ws.10))

### <a name="digest-security-support-provider"></a><a name="BKMK_DigestSSP"></a>Digest-Sicherheits Unterstützungs Anbieter
Die Digest-Authentifizierung ist ein Industriestandard, der für LDAP (Lightweight Directory Access Protocol) und die Webauthentifizierung verwendet wird. Die Digest-Authentifizierung überträgt Anmelde Informationen über das Netzwerk als MD5-Hash oder Nachrichten Digest.

Digest-SSP (Wdigest.dll) wird für Folgendes verwendet:

-   Internet Explorer-und Internetinformationsdienste Zugriff (IIS)

-   LDAP-Abfragen

Speicherort:% windir% \Windows\System32\Digest.dll

Dieser Anbieter ist standardmäßig in Versionen enthalten, die in der Liste **gilt für** am Anfang dieses Themas angegeben sind, sowie unter Windows Server 2003 und Windows XP.

**Zusätzliche Ressourcen für das Digest-Protokoll und den Digest-SSP**

-   [Microsoft Digest Authentifizierung (Windows)](/windows/win32/secauthn/microsoft-digest-ssp)

-   [\[MS-dpsp \] : Digest-Protokoll Erweiterungen](/openspecs/windows_protocols/ms-dpsp/3e44be62-2067-472a-9ef0-e937298b68fb)

### <a name="schannel-security-support-provider"></a><a name="BKMK_SchannelSSP"></a>SChannel Security Support Provider
Der sichere Kanal (SChannel) wird für die webbasierte Server Authentifizierung verwendet, z. b. Wenn ein Benutzer versucht, auf einen sicheren Webserver zuzugreifen.

Das TLS-Protokoll, das SSL-Protokoll, das PCT-Protokoll (private Communications Technology) und das DTLS-Protokoll (Datagram Transport Layer) basieren auf Kryptografie mit öffentlichem Schlüssel. SChannel stellt alle diese Protokolle bereit. Alle Schannel-Protokolle verwenden ein Client/Server-Modell. Der Schannel SSP verwendet Zertifikate für öffentliche Schlüssel zum Authentifizieren von Parteien. Beim Authentifizieren von Parteien wählt Schannel SSP ein Protokoll in der folgenden Reihenfolge aus:

-   Transport Layer Security (TLS) Version 1,0

-   Transport Layer Security (TLS) Version 1,1

-   Transport Layer Security (TLS) Version 1,2

-   Secure Socket Layer (SSL) Version 2,0

-   Secure Socket Layer (SSL) Version 3,0

-   Private Kommunikationstechnologie (PCT)

    **Hinweis** PCT ist standardmäßig deaktiviert.

Das ausgewählte Protokoll ist das bevorzugte Authentifizierungsprotokoll, das vom Client und vom Server unterstützt werden kann. Wenn ein Server beispielsweise alle SChannel-Protokolle unterstützt und der Client nur SSL 3,0 und SSL 2,0 unterstützt, verwendet der Authentifizierungsprozess SSL 3,0.

DTLS wird verwendet, wenn Sie von der Anwendung explizit aufgerufen wird. Weitere Informationen zu DTLS und den anderen Protokollen, die vom SChannel-Anbieter verwendet werden, finden Sie [unter SChannel Security Support Provider Technical Reference](../tls/schannel-security-support-provider-technical-reference.md).

Speicherort:% windir% \Windows\System32\Schannel.dll

Dieser Anbieter ist standardmäßig in Versionen enthalten, die in der Liste **gilt für** am Anfang dieses Themas angegeben sind, sowie unter Windows Server 2003 und Windows XP.

> [!NOTE]
> TLS 1,2 wurde in diesem Anbieter in Windows Server 2008 R2 und Windows 7 eingeführt. DTLS wurde in diesem Anbieter in Windows Server 2012 und Windows 8 eingeführt.

**Zusätzliche Ressourcen für die TLS-und SSL-Protokolle und den Schannel SSP**

-   [Sicherer Kanal (Windows)](/windows/win32/secauthn/secure-channel)

-   [Technische Referenz zu TLS/SSL](/previous-versions/windows/it-pro/windows-server-2003/cc784149(v=ws.10))

-   [\[MS-TLSP \] : Transport Layer Security (TLS)-Profil](/openspecs/windows_protocols/ms-tlsp/58aba05b-62b0-4cd1-b88b-dc8a24920346)

### <a name="negotiate-security-support-provider"></a><a name="BKMK_NegoSSP"></a>Sicherheits Unterstützungs Anbieter aushandeln
Der einfache und geschützte GSS-API-Aushandlungs Mechanismus (spnetgo) bildet die Grundlage für den Aushandlungs-SSP, der zum Aushandeln eines bestimmten Authentifizierungs Protokolls verwendet werden kann. Wenn eine SSPI zur Anmeldung bei einem Netzwerk von einer Anwendung aufgerufen wird, kann ein SSP zur Verarbeitung der Anforderung angegeben werden. Wenn die Anwendung den Aushandlungs-SSP angibt, analysiert Sie die Anforderung und wählt den entsprechenden Anbieter für die Verarbeitung der Anforderung auf der Grundlage der vom Kunden konfigurierten Sicherheitsrichtlinien aus.

Spnetgo ist in RFC 2478 angegeben.

In unterstützten Versionen der Windows-Betriebssysteme wählt der Aushandlungs Security Support Provider zwischen dem Kerberos-Protokoll und NTLM aus. Aushandeln wählt das Kerberos-Protokollstandard mäßig aus, es sei denn, das Protokoll kann von einem der an der Authentifizierung beteiligten Systeme verwendet werden, oder die aufrufende Anwendung hat keine ausreichenden Informationen für die Verwendung des Kerberos-Protokolls bereitgestellt.

Speicherort:% windir% \Windows\System32\lsasrv.dll

Dieser Anbieter ist standardmäßig in Versionen enthalten, die in der Liste **gilt für** am Anfang dieses Themas angegeben sind, sowie unter Windows Server 2003 und Windows XP.

**Weitere Ressourcen für den Aushandlungs-SSP**

-   [Microsoft aushandeln (Windows)](/windows/win32/secauthn/microsoft-negotiate)

-   [\[MS-SPNG \] : einfache und geschützte GSS-API-Aushandlungs Mechanismus-Erweiterungen (spnetgo)](/openspecs/windows_protocols/ms-spng/f377a379-c24f-4a0f-a3eb-0d835389e28a)

-   [\[MS-N2HT \] : Aushandlungs-und Nego2 http-Authentifizierungsprotokoll Spezifikation](/openspecs/windows_protocols/ms-n2ht/4b88aa77-4b12-4933-8740-0f32d8f4eacf)

### <a name="credential-security-support-provider"></a><a name="BKMK_CredSSP"></a>Anmelde Informationsanbieter für Sicherheitsunterstützung
Der Anmelde Informations Sicherheits-Dienstanbieter (Credential Security Service Provider, shdssp) stellt beim Starten neuer terminaldienstedienste und Remotedesktopdienste Sitzungen eine Single Sign-on Benutzer Darstellung (SSO) bereit. Mit "andssp" können Anwendungen die Anmelde Informationen des Benutzers vom Client Computer (mithilfe des Client seitigen SSP) an den Zielserver (über den serverseitigen SSP) delegieren, basierend auf den Richtlinien des Clients. Die Richtlinien für die aufwärtssp werden mithilfe von Gruppenrichtlinie konfiguriert. die Delegierung von Anmelde Informationen ist standardmäßig deaktiviert.

Speicherort:% windir% \Windows\System32\credssp.dll

Dieser Anbieter ist standardmäßig in Versionen enthalten, die in der Liste **gilt für** am Anfang dieses Themas angegeben sind.

**Weitere Ressourcen für die Anmelde Informationen SSP**

-   [\[MS-CSSp \] : Credential Security Support Provider (kredssp)-Protokollspezifikation](/openspecs/windows_protocols/ms-cssp/85f57821-40bb-46aa-bfcb-ba9590b8fc30)

-   [Anmelde Informationen Sicherheits Dienstanbieter und SSO für Terminaldiensteanmeldung](/previous-versions/windows/it-pro/windows-vista/cc749211(v=ws.10))

### <a name="negotiate-extensions-security-support-provider"></a><a name="BKMK_NegoExtsSSP"></a>Extensions für den Sicherheitsunterstützungs Anbieter aushandeln
Aushandlungs Erweiterungen (NegoExts) ist ein Authentifizierungs Paket, das die Verwendung von SSPs, außer NTLM oder das Kerberos-Protokoll, für Anwendungen und Szenarios, die von Microsoft und anderen Softwareunternehmen implementiert werden, aushandelt.

Diese Erweiterung des Aushandlungs Pakets ermöglicht die folgenden Szenarien:

-   **Umfassende Client Verfügbarkeit innerhalb eines Verbundsystems.** Auf Dokumente kann auf SharePoint-Websites zugegriffen werden, und Sie können mithilfe einer Microsoft Office Anwendung mit vollem Funktionsumfang bearbeitet werden.

-   **Umfassende Client Unterstützung für Microsoft Office Services.** Benutzer können sich bei Microsoft Office Services anmelden und eine Microsoft Office Anwendung mit vollem Funktionsumfang verwenden.

-   **Gehosteter Microsoft Exchange-Server und Outlook.** Es wurde keine Domänen Vertrauensstellung eingerichtet, da Exchange Server im Web gehostet wird. Outlook verwendet den Windows Live-Dienst, um Benutzer zu authentifizieren.

-   **Umfassende Client Verfügbarkeit zwischen Client Computern und Servern.** Die Netzwerk-und Authentifizierungs Komponenten des Betriebssystems werden verwendet.

Das Windows-Aushandlungs Paket behandelt den "NegoExts SSP" auf die gleiche Weise wie für Kerberos und NTLM. NegoExts.dll wird beim Start in die lokale System Zertifizierungsstelle (Local System Authority, LSA) geladen. Wenn eine Authentifizierungsanforderung empfangen wird, die auf der Anforderungs Quelle basiert, verhandelt NegoExts zwischen den unterstützten SSPs. Sie sammelt die Anmelde Informationen und Richtlinien, verschlüsselt Sie und sendet diese Informationen an den entsprechenden SSP, in dem das Sicherheits Token erstellt wird.

Die von "NegoExts" unterstützten SSPs sind keine eigenständigen SSPs, wie z. b. Kerberos und NTLM. Wenn die Authentifizierungsmethode aus irgendeinem Grund fehlschlägt, wird im SSP von Negoexts daher eine Authentifizierungsfehler Meldung angezeigt oder protokolliert. Es sind keine Methoden für die erneute Aushandlung oder Alternative Authentifizierung möglich.

Speicherort:% windir% \Windows\System32\negoexts.dll

Dieser Anbieter ist standardmäßig in Versionen enthalten, die in der Liste **gilt für** am Anfang dieses Themas angegeben sind, ausgenommen Windows Server 2008 und Windows Vista.

### <a name="pku2u-security-support-provider"></a><a name="BKMK_PKU2USSP"></a>PKU2U Security Support Provider
Das PKU2U-Protokoll wurde in Windows 7 und Windows Server 2008 R2 als SSP eingeführt und implementiert. Dieser SSP ermöglicht die Peer-zu-Peer-Authentifizierung, insbesondere über das Medien-und Dateifreigabe Feature namens HomeGroup, das in Windows 7 eingeführt wurde. Die Funktion ermöglicht die Freigabe von Computern, die nicht Mitglied einer Domäne sind.

Speicherort:% windir% \Windows\System32\pku2u.dll

Dieser Anbieter ist standardmäßig in Versionen enthalten, die in der Liste **gilt für** am Anfang dieses Themas angegeben sind, ausgenommen Windows Server 2008 und Windows Vista.

**Zusätzliche Ressourcen für das PKU2U-Protokoll und den PKU2U SSP**

-   [Einführung in die Online-Identitäts Integration](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd560662(v=ws.10))

## <a name="security-support-provider-selection"></a><a name="BKMK_SecuritySupportProviderSelection"></a>Auswahl des Sicherheits Unterstützungs Anbieters
Die Windows-SSPI kann jedes der Protokolle verwenden, die von den installierten Sicherheits Unterstützungs Anbietern unterstützt werden. Da jedoch nicht alle Betriebssysteme dieselben SSP-Pakete unterstützen wie ein beliebiger Computer, auf dem Windows Server ausgeführt wird, müssen Clients und Server die Verwendung eines Protokolls aushandeln, das beide unterstützen. Windows Server bevorzugt Client Computer und Anwendungen für die Verwendung des Kerberos-Protokolls, ein leistungsstarkes Standard basiertes Protokoll, wenn möglich, das Betriebssystem jedoch weiterhin Client Computern und Client Anwendungen, von denen das Kerberos-Protokoll nicht unterstützt wird, zu authentifizieren.

Bevor die Authentifizierung erfolgen kann, müssen die beiden kommunizierenden Computer einem Protokoll zustimmen, das beide unterstützen können. Damit jedes Protokoll über die SSPI verwendbar ist, muss jeder Computer über die entsprechende SSP verfügen. Damit ein Client Computer und ein Server das Kerberos-Authentifizierungsprotokoll verwenden können, müssen beide beispielsweise Kerberos V5 unterstützen. Windows Server verwendet die Funktion " **enumeratesecuritypackages** ", um zu ermitteln, welche SSPs auf einem Computer unterstützt werden und welche Funktionen diese SSPs haben.

Die Auswahl eines Authentifizierungs Protokolls kann auf eine der beiden folgenden Arten erfolgen:

1.  [Einzelnes Authentifizierungsprotokoll](#BKMK_SingleAuth)

2.  [Aushandeln (Option)](#BKMK_Negotiate)

### <a name="single-authentication-protocol"></a><a name="BKMK_SingleAuth"></a>Einzelnes Authentifizierungsprotokoll
Wenn ein einzelnes akzeptables Protokoll auf dem Server angegeben ist, muss der Client Computer das angegebene Protokoll unterstützen, oder die Kommunikation schlägt fehl. Wenn ein einzelnes akzeptables Protokoll angegeben wird, erfolgt der Authentifizierungs Austausch wie folgt:

1.  Der Client Computer fordert den Zugriff auf einen Dienst an.

2.  Der Server antwortet auf die Anforderung und gibt das Protokoll an, das verwendet wird.

3.  Der Client Computer überprüft den Inhalt der Antwort und überprüft, ob er das angegebene Protokoll unterstützt. Wenn der Client Computer das angegebene Protokoll unterstützt, wird die Authentifizierung fortgesetzt. Wenn der Client Computer das Protokoll nicht unterstützt, schlägt die Authentifizierung fehl, unabhängig davon, ob der Client Computer für den Zugriff auf die Ressource autorisiert ist.

### <a name="negotiate-option"></a><a name="BKMK_Negotiate"></a>Aushandeln (Option)
Die Option aushandeln kann verwendet werden, um dem Client und dem Server zu ermöglichen, ein akzeptables Protokoll zu finden. Dies basiert auf dem einfachen und geschützten GSS-API-Aushandlungs Mechanismus (spnetgo). Wenn die Authentifizierung mit der Option zum Aushandeln eines Authentifizierungs Protokolls beginnt, erfolgt der spnetgo-Austausch wie folgt:

1.  Der Client Computer fordert den Zugriff auf einen Dienst an.

2.  Der Server antwortet mit einer Liste von Authentifizierungs Protokollen, die er unterstützen kann, sowie einer Authentifizierungs Aufforderung oder-Antwort, die auf dem Protokoll basiert, das die erste Wahl ist. Der Server kann z. b. das Kerberos-Protokoll und NTLM auflisten und eine Kerberos-Authentifizierungs Antwort senden.

3.  Der Client Computer überprüft den Inhalt der Antwort und überprüft, ob er eines der angegebenen Protokolle unterstützt.

    -   Wenn der Client Computer das bevorzugte Protokoll unterstützt, wird die Authentifizierung fortgesetzt.

    -   Wenn der Client Computer das bevorzugte Protokoll nicht unterstützt, aber eines der anderen vom Server aufgelisteten Protokolle unterstützt, kann der Server vom Client Computer wissen, welches Authentifizierungsprotokoll unterstützt wird, und die Authentifizierung wird durchgeführt.

    -   Wenn der Client Computer keines der aufgelisteten Protokolle unterstützt, schlägt der Authentifizierungs Austausch fehl.

## <a name="additional-references"></a>Weitere Verweise
[Architektur der Windows-Authentifizierung](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dn169024(v=ws.10))