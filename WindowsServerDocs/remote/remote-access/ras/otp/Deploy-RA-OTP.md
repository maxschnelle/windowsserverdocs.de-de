---
title: Bereitstellen des Remotezugriffs mit OTP-Authentifizierung
description: Dieses Thema ist Teil des Handbuchs Bereitstellen des Remote Zugriffs mit OTP-Authentifizierung in Windows Server 2016.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.assetid: b1b2fe70-7956-46e8-a3e3-43848868df09
ms.author: lizross
author: eross-msft
ms.openlocfilehash: d1b38f753e2e4d8333299c369042a72e0dc3a6e6
ms.sourcegitcommit: d99bc78524f1ca287b3e8fc06dba3c915a6e7a24
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/27/2020
ms.locfileid: "87182006"
---
# <a name="deploy-remote-access-with-otp-authentication"></a>Bereitstellen des Remotezugriffs mit OTP-Authentifizierung

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

 Windows Server 2016 und Windows Server 2012 kombinieren DirectAccess und RRAS-VPN des Routing-und RAS-diensdienstanbieter \( \) zu einer einzigen Remote Zugriffs Rolle.

## <a name="scenario-description"></a><a name="BKMK_OVER"></a>Beschreibung des Szenarios
In diesem Szenario wird ein RAS-Server, auf dem DirectAccess aktiviert ist, so konfiguriert, dass DirectAccess-Client Benutzer mit zwei \- stufigen Kenn Wort Kennwort-Kenn Wort \( \) Authentifizierung, zusätzlich zu Standard-Active Directory Anmelde Informationen, authentifiziert werden.

## <a name="prerequisites"></a>Voraussetzungen
Bevor Sie mit der Bereitstellung dieses Szenarios beginnen, sollten Sie die Liste der wichtigen Anforderungen lesen:

-   [Eine Bereitstellung eines einzelnen DirectAccess-Servers mit erweiterten Einstellungen](../../directaccess/single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md) muss vor der Bereitstellung von OTP bereitgestellt werden.

-   Windows 7-Clients müssen DCA 2,0 zur Unterstützung von OTP verwenden.

-   OTP unterstützt nicht die PIN-Änderung.

-   Eine Public Key-Infrastruktur muss bereitgestellt werden.

    Weitere Informationen finden Sie unter: [Testumgebungsanleitung – Minimodul: Basis-PKI für Windows Server 2012](https://docs.microsoft.com/answers/topics/windows-server-2012.html)

-   Das Ändern von Richtlinien außerhalb der DirectAccess-Verwaltungskonsole oder der Windows PowerShell-Cmdlets wird nicht unterstützt.

## <a name="in-this-scenario"></a>Inhalt dieses Szenarios
Das Szenario für die OTP-Authentifizierung besteht aus mehreren Schritten:

1.  Stellen Sie [einen einzelnen DirectAccess-Server mit erweiterten Einstellungen](../../directaccess/single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md)bereit. Vor dem Konfigurieren von OTP muss ein einzelner Remote Zugriffs Server bereitgestellt werden. Die Planung und Bereitstellung eines einzelnen Servers umfasst das Entwerfen und Konfigurieren einer Netzwerktopologie, das Planen und Bereitstellen von Zertifikaten, das Einrichten von DNS und Active Directory, das Konfigurieren von Remotezugriffsservereinstellungen, das Bereitstellen von DirectAccess-Clients und das Vorbereiten von Intranetservern.

2.  [Planen Sie den Remote Zugriff mit OTP-Authentifizierung](./plan/plan-remote-access-with-otp-authentication.md). Zusätzlich zur Planung, die für einen einzelnen Server erforderlich ist, müssen Sie für OTP eine Zertifizierungsstellen \( -Zertifizierungsstelle \) und Zertifikat Vorlagen für OTP und einen RADIUS- \- fähigen OTP-Server planen. Die Planung kann auch eine Anforderung für Sicherheitsgruppen beinhalten, um bestimmte Benutzer von einer starken \( OTP-oder \) Smartcardauthentifizierung auszuschließen. Informationen zur Konfiguration von OTP in einer Umgebung mit mehreren Gesamtstrukturen finden Sie unter \- [Konfigurieren einer Bereitstellung mit mehreren](../../ras/multi-forest/Configure-a-Multi-Forest-Deployment.md)Gesamtstrukturen.

3.  [Konfigurieren von DirectAccess mit OTP-Authentifizierung](/configure/Configure-RA-with-OTP-Authentication.md). Die OTP-Bereitstellung besteht aus einer Reihe von Konfigurationsschritten, einschließlich der Vorbereitung der Infrastruktur für die OTP-Authentifizierung, dem Konfigurieren des OTP-Servers, dem Konfigurieren von OTP-Einstellungen auf dem RAS-Server und dem Aktualisieren der DirectAccess-Client Einstellungen.

4.  [Problembehandlung bei der OTP-Bereitstellung] ((/troubleshoot/Troubleshoot-an-OTP-Deployment.md). In diesem Abschnitt zur Problembehandlung werden einige der häufigsten Fehler beschrieben, die beim Bereitstellen des Remote Zugriffs mit OTP-Authentifizierung auftreten können.

## <a name="practical-applications"></a><a name="BKMK_APP"></a>Praktische Anwendung
Erhöhung der Sicherheit: die Verwendung von OTP erhöht die Sicherheit Ihrer DirectAccess-Bereitstellung. Ein Benutzer benötigt OTP-Anmeldeinformationen, um auf das interne Netzwerk zugreifen zu können. Ein Benutzer gibt OTP-Anmelde Informationen über die Arbeitsplatz Verbindungen an, die in den Netzwerkverbindungen auf dem Windows 10-oder Windows 8-Client Computer verfügbar sind, oder mithilfe der DirectAccess-Verbindungs-Assistent- \( DCA \) auf Client Computern unter Windows 7. Der OTP-Authentifizierungsprozess läuft wie folgt ab:

1.  Der DirectAccess-Client gibt die Domänen Anmelde Informationen für den Zugriff auf DirectAccess-Infrastruktur Server \( über den Infrastruktur Tunnel ein \) .  Wenn aufgrund eines bestimmten IKE-Fehlers keine Verbindung zum internen Netzwerk verfügbar ist, erhält der Benutzer über die Arbeitsplatzverbindungen des Clientcomputers eine Benachrichtigung, dass Anmeldeinformationen eingegeben werden müssen. Auf Client Computern mit Windows 7 wird ein Popup Fenster mit \- Smartcard-Anmelde Informationen angezeigt.

2.  Nachdem die OTP-Anmelde Informationen eingegeben wurden, werden Sie über SSL an den RAS-Server gesendet, und es wird eine Anforderung für ein kurzfristiges \- Smartcard-Anmeldezertifikat gesendet.

3.  Der Remote Zugriffs Server initiiert die Überprüfung der OTP-Anmelde Informationen mit dem RADIUS- \- basierten OTP-Server.

4.  Bei Erfolg signiert der RAS-Server die Zertifikatanforderung mithilfe seines Registrierungsstellenzertifikats und sendet sie an den DirectAccess-Clientcomputer zurück.

5.  Der DirectAccess-Client Computer leitet die signierte Zertifikat Anforderung an die Zertifizierungsstelle weiter und speichert das registrierte Zertifikat für die Verwendung durch die Kerberos SSP-Zugriffspunkt- \/ app.

6.  Der Clientcomputer verwendet dieses Zertifikat für eine transparente Kerberos-Standardauthentifizierung mit einer Smartcard.

## <a name="roles-and-features-included-in-this-scenario"></a><a name="BKMK_NEW"></a>In diesem Szenario enthaltene Rollen und Features
Die folgende Tabelle enthält die für dieses Szenario erforderlichen Rollen und Features:

|Rollen \/ Funktion|Auf welche Weise dieses Szenario unterstützt wird|
|---------|-----------------|
|*Rolle für die Remotezugriffsverwaltung*|Diese Rolle wird mithilfe der Server-Manager-Konsole installiert und deinstalliert. Diese Rolle umfasst DirectAccess (zuvor ein Feature in Windows Server 2008 R2) sowie die Routing-und RAS-Dienste, die zuvor ein Rollen Dienst unter der Server Rolle Netzwerk Richtlinien-und Zugriffs Dienste von \( npas waren \) . Die Remotezugriffs-Rolle besteht aus zwei Komponenten:<p>1. DirectAccess und Routing-und RAS \( -Dienste RRAS \) -VPN-DirectAccess und VPN werden in der Remote Zugriffs-Verwaltungskonsole verwaltet.<br />2. RRAS-Routing-RRAS-Routing Features werden in der Legacy-Routing-und Remote Zugriffs Konsole verwaltet.<p>Die Remotezugriffsrolle ist von den folgenden Serverfeatures abhängig:<p>-Internetinformationsdienste \( IIS \) -Webserver: dieses Feature ist erforderlich, um den Netzwerkadressen Server zu konfigurieren, die OTP-Authentifizierung zu verwenden und den Standardweb Test zu konfigurieren.<br />-Interne Windows-Datenbank: wird für die lokale Kontoführung auf dem Remote Zugriffs Server verwendet.|
|Feature %%amp;quot;Tools für die Remotezugriffsverwaltung%%amp;quot;|So installieren Sie dieses Feature:<p>-Sie wird standardmäßig auf einem RAS-Server installiert, wenn die Remote Zugriffs Rolle installiert ist, und unterstützt die Benutzeroberfläche der Remote Verwaltungskonsole.<br />-Es kann optional auf einem Server installiert werden, auf dem die Remote Zugriffs-Server Rolle nicht ausgeführt wird. In diesem Fall wird es für die Remoteverwaltung eines RAS-Computers verwendet, der DirectAccess und VPN ausführt.<p>Das Feature "Tools für die Remotezugriffsverwaltung" besteht aus den folgenden Komponenten:<p>-Remote Zugriffs-GUI und Befehlszeilen Tools<br />-Remote Zugriffs Modul für Windows PowerShell<p>Abhängigkeiten umfassen:<p>-Gruppenrichtlinien-Verwaltungskonsole<br />-RAS-Verbindungs-Manager Administration Kit \( CMAK\)<br />-Windows PowerShell 3,0<br />-Tools und Infrastruktur für die grafische Verwaltung|

## <a name="hardware-requirements"></a><a name="BKMK_HARD"></a>Hardwareanforderungen
Für dieses Szenario müssen die folgenden Hardwareanforderungen erfüllt werden:

-   Ein Computer, der die Hardwareanforderungen für Windows Server 2016 oder Windows Server 2012 erfüllt.

-   Um das Szenario zu testen, ist mindestens ein Computer erforderlich, auf dem Windows 10, Windows 8 oder Windows 7 ausgeführt wird und der als DirectAccess-Client konfiguriert ist.

-   Ein OTP-Server, der PAP über RADIUS unterstützt

-   Ein OTP-Hardware- oder Software-Token

## <a name="software-requirements"></a><a name="BKMK_SOFT"></a>Softwareanforderungen
Für dieses Szenario gelten eine Reihe von Anforderungen:

1.  Softwareanforderungen für die Bereitstellung auf einem Einzelserver. Weitere Informationen finden Sie unter Bereitstellen [eines einzelnen DirectAccess-Servers mit erweiterten Einstellungen](../../directaccess/single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md).

2.  Zusätzlich zu den Softwareanforderungen für einen einzelnen Server gibt es eine Reihe von OTP- \- spezifischen Anforderungen:

    1.  Zertifizierungsstelle für die IPSec-Authentifizierung: in einer OTP-Bereitstellung muss DirectAccess mithilfe von IPSec-Computer Zertifikaten bereitgestellt werden, die von einer Zertifizierungsstelle Die IPsec-Authentifizierung mithilfe des RAS-Servers als Kerberos-Proxy wird bei der OTP-Bereitstellung nicht unterstützt. Eine interne Zertifizierungsstelle ist erforderlich.

    2.  Zertifizierungsstelle für die OTP-Authentifizierung: eine Microsoft-Unternehmens \( Zertifizierungsstelle, die unter Windows 2003 Server oder höher ausgeführt \) wird, muss das OTP-Client Zertifikat ausstellen. Es kann dieselbe Zertifizierungsstelle verwendet werden, die auch die Zertifikate für die IPsec-Authentifizierung ausstellt. Der Zertifizierungsstellenserver muss über den ersten Infrastrukturtunnel erreichbar sein.

    3.  Sicherheitsgruppe: um Benutzer von der starken Authentifizierung auszuschließen, ist eine Active Directory Sicherheitsgruppe erforderlich, die diese Benutzer enthält.

    4.  Client \- seitige Anforderungen: für Windows 10-und Windows 8-Client Computer wird der NCA-Dienst des Netzwerk Verbindungs Assistenten \( \) verwendet, um zu ermitteln, ob OTP-Anmelde Informationen erforderlich sind. Wenn dies der Fall ist, fordert der DirectAccess-Medien-Manager Anmelde Informationen an.  NCA ist im Betriebssystem enthalten, und es ist keine Installation oder Bereitstellung erforderlich. Für Windows 7-Client Computer ist der DirectAccess-Konnektivitätsassistent \( DCA \) 2,0 erforderlich. Dieser kann aus dem [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=29039)heruntergeladen werden.

    5.  Beachten Sie Folgendes:

        1.  Die OTP-Authentifizierung kann parallel zur Smartcard-und Trusted Platform Module \( TPM- \) \- basierten Authentifizierung verwendet werden. Das Aktivieren der OTP-Authentifizierung in der Remotezugriffsverwaltungskonsole ermöglicht auch die Verwendung der Smartcard-Authentifizierung.

        2.  Während der Remote Zugriffs Konfiguration können Benutzer in einer angegebenen Sicherheitsgruppe von der zweistufigen Authentifizierung ausgenommen werden \- und müssen sich daher nur mit dem Benutzernamen \/ Kennwort authentifizieren.

        3.  Die OTP-Modi "Neue PIN" und "Nächster Tokencode" werden nicht unterstützt.

        4.  Bei einer Remotezugriffsbereitstellung an mehreren Standorten sind die OTP-Einstellungen global und dienen zur Identifikation an allen Einstiegspunkten. Wenn mehrere RADIUS- oder Zertifizierungsstellenserver für OTP konfiguriert werden, müssen sie von jedem RAS-Server anhand ihrer Verfügbarkeit und Nähe sortiert werden.

        5.  Beim Konfigurieren von OTP in einer Remote Zugriffs Umgebung mit mehreren Gesamtstrukturen \- sollten die OTP-Zertifizierungsstellen nur aus der Ressourcen Gesamtstruktur und die Zertifikat Registrierung über Gesamtstruktur-Vertrauens Stellungen hinweg konfiguriert werden. Weitere Informationen finden Sie unter [AD CS: Gesamtstrukturübergreifende Zertifikatsregistrierung mit Windows Server 2008 R2](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff955842(v=ws.10)).

        6.  Benutzer, die ein Schlüsselfob OTP-Token verwenden, sollten die PIN, gefolgt von Tokencode, \( ohne Trennzeichen \) im Dialogfeld für den DirectAccess-OTP einfügen. Benutzer, die einen PIN PAD OTP-Token verwenden, geben in diesem Dialogfeld nur den Tokencode ein.

        7.  Bei aktiviertem WEBDAV darf OTP nicht aktiviert werden.

## <a name="known-issues"></a><a name="KnownIssues"></a>Bekannte Probleme
Im Folgenden finden Sie bekannte Probleme beim Konfigurieren eines OTP-Szenarios:

-   Der Remote Zugriff verwendet einen Test Mechanismus, um die Konnektivität mit RADIUS- \- basierten OTP-Servern zu überprüfen. In einigen Fällen kann auf dem OTP-Server ein Fehler ausgelöst werden. Gehen Sie zur Vermeidung dieses Problems auf dem OTP-Server folgendermaßen vor:

    -   Erstellen Sie ein Benutzerkonto entsprechend dem auf dem RAS-Server für den Testmechanismus konfigurierten Benutzernamen und Kennwort. Der Benutzername darf keinen Active Directory-Benutzer definieren.

        Standardmäßig ist der Benutzername auf dem RAS-Server "DAProbeUser", und das Kennwort lautet "DAProbePass". Diese Standardeinstellungen können mithilfe der folgenden Werte in der Registrierung auf dem RAS-Server geändert werden:

        -   HKEY \_ local \_ Machine \\ Software \\ Microsoft \\ DirectAccess \\ OTP \\ radiusprobeuser

        -   HKEY \_ local \_ Machine \\ Software \\ Microsoft \\ DirectAccess \\ OTP \\ radiusprobepass

-   Wenn Sie das IPsec-Stammzertifikat in einer konfigurierten und ausgeführten DirectAccess-Bereitstellung ändern, funktioniert OTP nicht mehr. Um dieses Problem zu beheben, führen Sie auf jedem DirectAccess-Server an einer Windows PowerShell-Eingabeaufforderung den folgenden Befehl aus:`iisreset`

