---
title: Bereitstellen des Remotezugriffs mit OTP-Authentifizierung
description: Dieses Thema ist Teil des Handbuchs Bereitstellen des Remote Zugriffs mit OTP-Authentifizierung in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b1b2fe70-7956-46e8-a3e3-43848868df09
ms.author: pashort
author: shortpatti
ms.openlocfilehash: d0de5f459e31e1dfac40e49cd6cc83de8722df4d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71404428"
---
# <a name="deploy-remote-access-with-otp-authentication"></a>Bereitstellen des Remotezugriffs mit OTP-Authentifizierung

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

 Windows Server 2016 und Windows Server 2012 kombinieren DirectAccess und den Routing-und RAS-Dienst \(rras @ no__t-1-VPN zu einer einzigen Remote Zugriffs Rolle.   

## <a name="BKMK_OVER"></a>Szenariobeschreibung  
In diesem Szenario wird ein RAS-Server, auf dem DirectAccess aktiviert ist, so konfiguriert, dass er DirectAccess-Client Benutzer mit zwei einmaligen Kenn Wörtern von @ no__t \(otp @ no__t-2-Authentifizierung authentifiziert, zusätzlich zu den standardmäßigen Active Directory-Anmelde Informationen.  
  
## <a name="prerequisites"></a>Erforderliche Komponenten  
Bevor Sie mit der Bereitstellung dieses Szenarios beginnen, sollten Sie die Liste der wichtigen Anforderungen lesen:  
  
-   [Eine Bereitstellung eines einzelnen DirectAccess-Servers mit erweiterten Einstellungen](../../directaccess/single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md) muss vor der Bereitstellung von OTP bereitgestellt werden.  
  
-   Windows 7-Clients müssen DCA 2,0 zur Unterstützung von OTP verwenden.  
  
-   OTP unterstützt nicht die PIN-Änderung.  
  
-   Eine Public Key-Infrastruktur muss bereitgestellt werden.  
  
    Weitere Informationen finden Sie unter: [test Lab Guide Mini Module: Grundlegende PKI für Windows Server 2012. ](https://social.technet.microsoft.com/wiki/contents/articles/7862.test-lab-guide-mini-module-basic-pki-for-windows-server-2012.aspx)  
  
-   Das Ändern von Richtlinien außerhalb der DirectAccess-Verwaltungskonsole oder der Windows PowerShell-Cmdlets wird nicht unterstützt.  
  
## <a name="in-this-scenario"></a>Inhalt dieses Szenarios  
Das Szenario für die OTP-Authentifizierung besteht aus mehreren Schritten:  
  
1.  Stellen Sie [einen einzelnen DirectAccess-Server mit erweiterten Einstellungen](../../directaccess/single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md)bereit. Vor dem Konfigurieren von OTP muss ein einzelner Remote Zugriffs Server bereitgestellt werden. Die Planung und Bereitstellung eines einzelnen Servers umfasst das Entwerfen und Konfigurieren einer Netzwerktopologie, das Planen und Bereitstellen von Zertifikaten, das Einrichten von DNS und Active Directory, das Konfigurieren von Remotezugriffsservereinstellungen, das Bereitstellen von DirectAccess-Clients und das Vorbereiten von Intranetservern.  
  
2.  [Planen Sie den Remote Zugriff mit OTP-Authentifizierung](https://docs.microsoft.com/windows-server/remote/remote-access/ras/otp/plan/plan-remote-access-with-otp-authentication). Zusätzlich zu der für einen einzelnen Server erforderlichen Planung erfordert OTP die Planung einer Microsoft-Zertifizierungsstelle \(ca @ no__t-1 und Zertifikat Vorlagen für OTP; und einen RADIUS @ no__t-2aktivierten OTP-Server. Die Planung kann auch eine Anforderung für Sicherheitsgruppen beinhalten, um bestimmte Benutzer von einer starken \(otp oder Smartcard @ no__t-1-Authentifizierung auszuschließen. Informationen zur Konfiguration von OTP in einer Umgebung mit mehreren @ no__t-Gesamtstrukturen finden Sie unter [Konfigurieren einer Bereitstellung mit mehreren](../../ras/multi-forest/Configure-a-Multi-Forest-Deployment.md)Gesamtstrukturen.  
  
3.  [Konfigurieren von DirectAccess mit OTP-Authentifizierung](/configure/Configure-RA-with-OTP-Authentication.md). Die OTP-Bereitstellung besteht aus einer Reihe von Konfigurationsschritten, einschließlich der Vorbereitung der Infrastruktur für die OTP-Authentifizierung, dem Konfigurieren des OTP-Servers, dem Konfigurieren von OTP-Einstellungen auf dem RAS-Server und dem Aktualisieren der DirectAccess-Client Einstellungen.  
  
4.  [Problembehandlung bei der OTP-Bereitstellung] ((/troubleshoot/Troubleshoot-an-OTP-Deployment.md). In diesem Abschnitt zur Problembehandlung werden einige der häufigsten Fehler beschrieben, die beim Bereitstellen des Remote Zugriffs mit OTP-Authentifizierung auftreten können.  
  
## <a name="BKMK_APP"></a>Praktische Anwendungen  
Erhöhung der Sicherheit: die Verwendung von OTP erhöht die Sicherheit Ihrer DirectAccess-Bereitstellung. Ein Benutzer benötigt OTP-Anmeldeinformationen, um auf das interne Netzwerk zugreifen zu können. Ein Benutzer gibt OTP-Anmelde Informationen über die in den Netzwerkverbindungen auf dem Windows 10-oder Windows 8-Client Computer verfügbaren Arbeitsplatz Verbindungen oder mithilfe des DirectAccess-konnektivitätsassistenten \(dca @ no__t-1 auf Client Computern unter Windows 7 aus. Der OTP-Authentifizierungsprozess läuft wie folgt ab:  
  
1.  Der DirectAccess-Client gibt die Domänen Anmelde Informationen ein, um auf DirectAccess-Infrastruktur Server \(über den Infrastruktur Tunnel @ no__t-1 zuzugreifen.  Wenn aufgrund eines bestimmten IKE-Fehlers keine Verbindung zum internen Netzwerk verfügbar ist, erhält der Benutzer über die Arbeitsplatzverbindungen des Clientcomputers eine Benachrichtigung, dass Anmeldeinformationen eingegeben werden müssen. Auf Client Computern mit Windows 7 wird ein Pop @ no__t-0up, das Smartcard-Anmelde Informationen anfordert, angezeigt.  
  
2.  Nachdem die OTP-Anmelde Informationen eingegeben wurden, werden Sie über SSL an den RAS-Server gesendet, und es wird eine Anforderung für ein kurzes @ no__t-0term-Smartcard-Anmeldezertifikat gesendet.  
  
3.  Der Remote Zugriffs Server initiiert die Überprüfung der OTP-Anmelde Informationen mit dem RADIUS @ no__t-0basierten OTP-Server.  
  
4.  Bei Erfolg signiert der RAS-Server die Zertifikatanforderung mithilfe seines Registrierungsstellenzertifikats und sendet sie an den DirectAccess-Clientcomputer zurück.  
  
5.  Der DirectAccess-Client Computer leitet die signierte Zertifikat Anforderung an die Zertifizierungsstelle weiter und speichert das registrierte Zertifikat für die Verwendung mit Kerberos SSP @ no__t-0ap.  
  
6.  Der Clientcomputer verwendet dieses Zertifikat für eine transparente Standard-Kerberos-Authentifizierung mit einer Smartcard.  
  
## <a name="BKMK_NEW"></a>In diesem Szenario enthaltene Rollen und Features  
Die folgende Tabelle enthält die für dieses Szenario erforderlichen Rollen und Features:  
  
|Role @ no__t-0Feature|Auf welche Weise dieses Szenario unterstützt wird|  
|---------|-----------------|  
|*Rollen für die Remote Zugriffs Verwaltung*|Diese Rolle wird mithilfe der Server-Manager-Konsole installiert und deinstalliert. Diese Rolle umfasst DirectAccess (zuvor ein Feature in Windows Server 2008 R2) sowie die Routing-und RAS-Dienste, die zuvor ein Rollen Dienst unter der Server Rolle Netzwerk Richtlinien-und Zugriffs Dienste \(npas @ no__t-1 waren. Die Remotezugriffs-Rolle besteht aus zwei Komponenten:<br /><br />1.  DirectAccess-und Routing-und RAS-Dienste \(rras @ no__t-1 VPN-DirectAccess und VPN werden in der Remote Zugriffs-Verwaltungskonsole verwaltet.<br />2.  RRAS-Routing: RRAS-Routing Features werden in der Legacy-Routing-und Remote Zugriffs Konsole verwaltet.<br /><br />Die Remotezugriffsrolle ist von den folgenden Serverfeatures abhängig:<br /><br />-Internetinformationsdienste \(iis @ no__t-1 Webserver: dieses Feature ist erforderlich, um den Netzwerkadressen Server zu konfigurieren, die OTP-Authentifizierung zu verwenden und den Standardweb Test zu konfigurieren.<br />-Interne Windows-Datenbank: wird für die lokale Kontoführung auf dem Remote Zugriffs Server verwendet.|  
|Feature %%amp;quot;Tools für die Remotezugriffsverwaltung%%amp;quot;|So installieren Sie dieses Feature:<br /><br />-Sie wird standardmäßig auf einem RAS-Server installiert, wenn die Remote Zugriffs Rolle installiert ist, und unterstützt die Benutzeroberfläche der Remote Verwaltungskonsole.<br />-Es kann optional auf einem Server installiert werden, auf dem die Remote Zugriffs-Server Rolle nicht ausgeführt wird. In diesem Fall wird es für die Remoteverwaltung eines RAS-Computers verwendet, der DirectAccess und VPN ausführt.<br /><br />Das Feature "Tools für die Remotezugriffsverwaltung" besteht aus den folgenden Komponenten:<br /><br />-Remote Zugriffs-GUI und Befehlszeilen Tools<br />-Remote Zugriffs Modul für Windows PowerShell<br /><br />Abhängigkeiten umfassen:<br /><br />-Gruppenrichtlinien-Verwaltungskonsole<br />-RAS-Verbindungs-Manager-Verwaltungskit \(cmak @ no__t-1<br />-Windows PowerShell 3,0<br />-Tools und Infrastruktur für die grafische Verwaltung|  
  
## <a name="BKMK_HARD"></a>Hardware Anforderungen  
Für dieses Szenario müssen die folgenden Hardwareanforderungen erfüllt werden:  
  
-   Ein Computer, der die Hardwareanforderungen für Windows Server 2016 oder Windows Server 2012 erfüllt.  
  
-   Um das Szenario zu testen, ist mindestens ein Computer erforderlich, auf dem Windows 10, Windows 8 oder Windows 7 ausgeführt wird und der als DirectAccess-Client konfiguriert ist.  
  
-   Ein OTP-Server, der PAP über RADIUS unterstützt  
  
-   Ein OTP-Hardware- oder Software-Token  
  
## <a name="BKMK_SOFT"></a>Software Anforderungen  
Für dieses Szenario gelten eine Reihe von Anforderungen:  
  
1.  Softwareanforderungen für die Bereitstellung auf einem Einzelserver. Weitere Informationen finden Sie unter Bereitstellen [eines einzelnen DirectAccess-Servers mit erweiterten Einstellungen](../../directaccess/single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md).  
  
2.  Zusätzlich zu den Softwareanforderungen für einen einzelnen Server gibt es eine Reihe von "OTP @ no__t-0specific"-Anforderungen:  
  
    1.  Zertifizierungsstelle für die IPSec-Authentifizierung: in einer OTP-Bereitstellung muss DirectAccess mithilfe von IPSec-Computer Zertifikaten bereitgestellt werden, die von einer Zertifizierungsstelle Die IPsec-Authentifizierung mithilfe des RAS-Servers als Kerberos-Proxy wird bei der OTP-Bereitstellung nicht unterstützt. Eine interne Zertifizierungsstelle ist erforderlich.  
  
    2.  Zertifizierungsstelle für die OTP-Authentifizierung: eine Microsoft-Unternehmens Zertifizierungsstelle \(auf Windows 2003 Server oder höher als @ no__t-1 ist erforderlich, um das OTP-Client Zertifikat auszustellen. Es kann dieselbe Zertifizierungsstelle verwendet werden, die auch die Zertifikate für die IPsec-Authentifizierung ausstellt. Der Zertifizierungsstellenserver muss über den ersten Infrastrukturtunnel erreichbar sein.  
  
    3.  Sicherheitsgruppe: um Benutzer von der starken Authentifizierung auszuschließen, ist eine Active Directory Sicherheitsgruppe erforderlich, die diese Benutzer enthält.  
  
    4.  Anforderungen an den Client @ no__t-0side: für Windows 10-und Windows 8-Client Computer wird der netzwerkkonnektivitätsassistent \(nca @ no__t-2-Dienst verwendet, um zu ermitteln, ob OTP-Anmelde Informationen erforderlich sind. Wenn dies der Fall ist, fordert der DirectAccess-Medien-Manager Anmelde Informationen an.  NCA ist im Betriebssystem enthalten, und es ist keine Installation oder Bereitstellung erforderlich. Für Windows 7-Client Computer ist der DirectAccess-Konnektivitätsassistent \(dca @ no__t-1 2,0 erforderlich. Dieser kann aus dem [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=29039)heruntergeladen werden.  
  
    5.  Beachten Sie Folgendes:  
  
        1.  Die OTP-Authentifizierung kann parallel mit der Smartcard und Trusted Platform Module \(tpm @ no__t-1 @ no__t-2based-Authentifizierung verwendet werden. Das Aktivieren der OTP-Authentifizierung in der Remotezugriffsverwaltungskonsole ermöglicht auch die Verwendung der Smartcard-Authentifizierung.  
  
        2.  Während der Remote Zugriffs Konfiguration können Benutzer in einer angegebenen Sicherheitsgruppe von der zwei @ no__t-Authentifizierung ausgenommen werden und müssen sich daher nur mit dem Benutzernamen @ no__t-1password authentifizieren.  
  
        3.  Die OTP-Modi "Neue PIN" und "Nächster Tokencode" werden nicht unterstützt.  
  
        4.  Bei einer Remotezugriffsbereitstellung an mehreren Standorten sind die OTP-Einstellungen global und dienen zur Identifikation an allen Einstiegspunkten. Wenn mehrere RADIUS- oder Zertifizierungsstellenserver für OTP konfiguriert werden, müssen sie von jedem RAS-Server anhand ihrer Verfügbarkeit und Nähe sortiert werden.  
  
        5.  Beim Konfigurieren von OTP in einer Remote Zugriffs Umgebung mit mehreren @ no__t-0-Gesamtstrukturen sollten die OTP-Zertifizierungsstellen nur aus der Ressourcen Gesamtstruktur und die Zertifikat Registrierung über Gesamtstruktur-Vertrauens Stellungen hinweg konfiguriert werden. Weitere Informationen finden Sie unter [ad CS: Gesamtstruktur übergreifende Zertifikats Registrierung mit Windows Server 2008 R2 @ no__t-0.  
  
        6.  Benutzer, die ein Schlüsselfob OTP-Token verwenden, sollten die PIN gefolgt von Tokencode \(ohne Trennzeichen @ no__t-1 in das OTP-Dialogfeld von DirectAccess einfügen. Benutzer, die einen PIN PAD OTP-Token verwenden, geben in diesem Dialogfeld nur den Tokencode ein.  
  
        7.  Bei aktiviertem WEBDAV darf OTP nicht aktiviert werden.  
  
## <a name="KnownIssues"></a>Bekannte Probleme  
Im Folgenden finden Sie bekannte Probleme beim Konfigurieren eines OTP-Szenarios:  
  
-   Der Remote Zugriff verwendet einen Test Mechanismus, um die Konnektivität mit RADIUS @ no__t-0basierten OTP-Servern zu überprüfen. In einigen Fällen kann auf dem OTP-Server ein Fehler ausgelöst werden. Gehen Sie zur Vermeidung dieses Problems auf dem OTP-Server folgendermaßen vor:  
  
    -   Erstellen Sie ein Benutzerkonto entsprechend dem auf dem RAS-Server für den Testmechanismus konfigurierten Benutzernamen und Kennwort. Der Benutzername darf keinen Active Directory-Benutzer definieren.  
  
        Standardmäßig ist der Benutzername auf dem RAS-Server "DAProbeUser", und das Kennwort lautet "DAProbePass". Diese Standardeinstellungen können mithilfe der folgenden Werte in der Registrierung auf dem RAS-Server geändert werden:  
  
        -   HKEY @ no__t-0local @ no__t-1machine @ no__t-2Software @ no__t-3Microsoft @ no__t-4directaccess @ no__t-5otp @ no__t-6radiusprobeuser  
  
        -   HKEY @ no__t-0local @ no__t-1machine @ no__t-2Software @ no__t-3Microsoft @ no__t-4directaccess @ no__t-5otp @ no__t-6 radiusprobepass  
  
-   Wenn Sie das IPsec-Stammzertifikat in einer konfigurierten und ausgeführten DirectAccess-Bereitstellung ändern, funktioniert OTP nicht mehr. Um dieses Problem zu beheben, führen Sie auf jedem DirectAccess-Server an einer Windows PowerShell-Eingabeaufforderung den folgenden Befehl aus: `iisreset`  
  
