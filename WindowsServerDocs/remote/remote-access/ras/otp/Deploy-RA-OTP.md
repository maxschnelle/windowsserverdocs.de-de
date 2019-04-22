---
title: Bereitstellen des Remotezugriffs mit OTP-Authentifizierung
description: Dieses Thema ist Teil des Leitfadens Bereitstellen von Remotezugriff mit OTP-Authentifizierung in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b1b2fe70-7956-46e8-a3e3-43848868df09
ms.author: pashort
author: shortpatti
ms.openlocfilehash: ecb4503c6f8cbc08f2175a33a41929491e4a2b7f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59811991"
---
# <a name="deploy-remote-access-with-otp-authentication"></a>Bereitstellen des Remotezugriffs mit OTP-Authentifizierung

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

 Kombinieren von Windows Server 2016 und Windows Server 2012 DirectAccess und Routing- und RAS-Dienst \(RRAS\) VPN in einer einzigen remotezugriffsrolle.   

## <a name="BKMK_OVER"></a>Beschreibung des Szenarios  
In diesem Szenario eine RAS-Server, dem DirectAccess aktiviert ist für die Benutzer des DirectAccess-Client mit zwei authentifiziert konfiguriert\-Faktor Einmalkennwort \(OTP\) zusätzlich zum standard-Active-Authentifizierung Directory-Anmeldeinformationen.  
  
## <a name="prerequisites"></a>Vorraussetzungen  
Bevor Sie mit der Bereitstellung dieses Szenarios beginnen, sollten Sie die Liste der wichtigen Anforderungen lesen:  
  
-   [Bereitstellen eines einzelnen DirectAccess-Servers mit erweiterten Einstellungen](../../directaccess/single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md) muss bereitgestellt werden, bevor Sie OTP bereitstellen.  
  
-   Windows 7-Clients müssen DCA 2.0 verwenden, um OTP zu unterstützen.  
  
-   OTP unterstützt nicht die PIN-Änderung.  
  
-   Eine Public Key-Infrastruktur muss bereitgestellt werden.  
  
    Weitere Informationen finden Sie unter: [Testen Sie Testumgebungsanleitung – Minimodul: Einfache PKI für WindowsServer 2012.](https://social.technet.microsoft.com/wiki/contents/articles/7862.test-lab-guide-mini-module-basic-pki-for-windows-server-2012.aspx)  
  
-   Das Ändern von Richtlinien außerhalb der DirectAccess-Verwaltungskonsole oder der Windows PowerShell-Cmdlets wird nicht unterstützt.  
  
## <a name="in-this-scenario"></a>Inhalt dieses Szenarios  
Das Szenario für die OTP-Authentifizierung besteht aus mehreren Schritten:  
  
1.  [Bereitstellen eines einzelnen DirectAccess-Servers mit erweiterten Einstellungen](../../directaccess/single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md). Eine RAS-Servers muss vor der OTP-Konfiguration bereitgestellt werden. Die Planung und Bereitstellung eines einzelnen Servers umfasst das Entwerfen und Konfigurieren einer Netzwerktopologie, das Planen und Bereitstellen von Zertifikaten, das Einrichten von DNS und Active Directory, das Konfigurieren von Remotezugriffsservereinstellungen, das Bereitstellen von DirectAccess-Clients und das Vorbereiten von Intranetservern.  
  
2.  [Planen des Remotezugriffs mit OTP-Authentifizierung](https://docs.microsoft.com/windows-server/remote/remote-access/ras/otp/plan/plan-remote-access-with-otp-authentication). Zusätzlich zu die Planung für einen einzelnen Server, erfordert für OTP Planungen für ein Microsoft-Zertifizierungsstelle \(Zertifizierungsstelle\) und Zertifikatvorlagen für OTP sowie einen RADIUS-\-OTP-Server aktiviert. Planung beinhalten u. u. auch eine Voraussetzung für die Sicherheitsgruppen für bestimmte Benutzer ausschließen, starke \(OTP oder Smartcard\) Authentifizierung. Informationen zur Konfiguration von OTP in einem Multithreadprogramm\-Gesamtstruktur-Umgebung, finden Sie unter [Konfigurieren einer Bereitstellung mit mehreren Gesamtstrukturen](../../ras/multi-forest/Configure-a-Multi-Forest-Deployment.md).  
  
3.  [Konfigurieren von DirectAccess mit OTP-Authentifizierung](/configure/Configure-RA-with-OTP-Authentication.md). OTP-Bereitstellung umfasst eine Reihe von Konfigurationsschritten, einschließlich der Vorbereitung der Infrastruktur für die OTP-Authentifizierung der OTP-Server konfigurieren, Konfigurieren von OTP-Einstellungen auf dem RAS-Server und Aktualisieren der DirectAccess-Clienteinstellungen.  
  
4.  [Problembehandlung bei einer OTP-Bereitstellung] ((/troubleshoot/Troubleshoot-an-OTP-Deployment.md). In diesem Abschnitt zur Problembehandlung wird beschrieben, eine Anzahl von die häufigsten Fehler, die bei der Bereitstellung von Remotezugriff mit OTP-Authentifizierung auftreten können.  
  
## <a name="BKMK_APP"></a>Praktische Anwendungen  
Erhöhen Sie Sicherheit – die Verwendung von OTP erhöht die Sicherheit, der DirectAccess-Bereitstellung. Ein Benutzer benötigt OTP-Anmeldeinformationen, um auf das interne Netzwerk zugreifen zu können. Gibt der Benutzer seine OTP-Anmeldeinformationen über den Arbeitsplatz in den Netzwerkverbindungen enthaltenen arbeitsplatzverbindungen auf dem Clientcomputer Windows 10 oder Windows 8 oder mithilfe von DirectAccess Connectivity Assistant \(DCA\) auf Clientcomputern ausgeführt wird Windows 7. Der OTP-Authentifizierungsprozess läuft wie folgt ab:  
  
1.  Der DirectAccess-Client gibt die Anmeldeinformationen für die Domäne für den Zugriff auf DirectAccess-Infrastrukturserver \(über den infrastrukturtunnel\).  Wenn aufgrund eines bestimmten IKE-Fehlers keine Verbindung zum internen Netzwerk verfügbar ist, erhält der Benutzer über die Arbeitsplatzverbindungen des Clientcomputers eine Benachrichtigung, dass Anmeldeinformationen eingegeben werden müssen. Auf Clientcomputern ausführen von Windows 7, einen Pop\-anfordern, Smartcard-Anmeldeinformationen angezeigt wird.  
  
2.  Nachdem die OTP-Anmeldeinformationen eingegeben haben, sie werden über SSL an gesendet der RAS-Server zusammen mit der Anforderung für einen kurzen\-Begriff-Zertifikats für Smartcard-Anmeldung.  
  
3.  RAS-Server beginnt der OTP-Anmeldeinformationen mit dem angegebenen RADIUS\-basierten OTP-Server.  
  
4.  Bei Erfolg signiert der RAS-Server die Zertifikatanforderung mithilfe seines Registrierungsstellenzertifikats und sendet sie an den DirectAccess-Clientcomputer zurück.  
  
5.  Der DirectAccess-Clientcomputer leitet die signierte zertifikatanforderung an der Zertifizierungsstelle und speichert das registrierte Zertifikat für die Verwendung durch die Kerberos-SSP\/Pazifik.  
  
6.  Der Clientcomputer verwendet dieses Zertifikat für eine transparente Standard-Kerberos-Authentifizierung mit einer Smartcard.  
  
## <a name="BKMK_NEW"></a>In diesem Szenario enthaltene Rollen und features  
Die folgende Tabelle enthält die für dieses Szenario erforderlichen Rollen und Features:  
  
|Rolle\/Feature|Auf welche Weise dieses Szenario unterstützt wird|  
|---------|-----------------|  
|*Rolle für die Remotezugriffsverwaltung*|Diese Rolle wird mithilfe der Server-Manager-Konsole installiert und deinstalliert. Diese Rolle umfasst DirectAccess, die zuvor ein Feature in Windows Server 2008 R2 und Routing und RAS-Dienste zuvor ein Rollendienst unter der Netzwerkrichtlinie und Zugriffsdienste \(NPAS\) Server die Rolle. Die Remotezugriffs-Rolle besteht aus zwei Komponenten:<br /><br />1.  DirectAccess und Routing- und RAS-Dienste \(RRAS\) VPN – DirectAccess und VPN werden gemeinsam in der Remotezugriffs-Verwaltungskonsole verwaltet.<br />2.  RRAS-Routing – RRAS-Routingfeatures werden in der älteren Routing- und RAS-Konsole verwaltet.<br /><br />Die Remotezugriffsrolle ist von den folgenden Serverfeatures abhängig:<br /><br />– Internet Information Services \(IIS\) Webserver – dieses Feature ist erforderlich, um den Netzwerkadressenserver zu konfigurieren, OTP-Authentifizierung verwenden und den standardwebtest zu konfigurieren.<br />-Windows interne Database-Used zur lokalen Kontoführung auf dem RAS-Server.|  
|Feature %%amp;quot;Tools für die Remotezugriffsverwaltung%%amp;quot;|So installieren Sie dieses Feature:<br /><br />– Es wird standardmäßig auf einem RAS-Server installiert, wenn die Rolle "Remotezugriff" installiert ist, und unterstützt die Benutzeroberfläche der RAS-Konsole.<br />– sie können optional auf einem Server nicht mit der RAS-Serverrolle installiert werden. In diesem Fall wird es für die Remoteverwaltung eines RAS-Computers verwendet, der DirectAccess und VPN ausführt.<br /><br />Das Feature "Tools für die Remotezugriffsverwaltung" besteht aus den folgenden Komponenten:<br /><br />-Remotezugriffs-GUI und Befehlszeilentools<br />-RAS-Modul für Windows PowerShell<br /><br />Abhängigkeiten umfassen:<br /><br />-Gruppenrichtlinien-Verwaltungskonsole<br />-RAS-Verbindungs-Manager-Verwaltungskit \(CMAK\)<br />-Windows PowerShell 3.0<br />-Grafische Verwaltungstools und Infrastruktur|  
  
## <a name="BKMK_HARD"></a>Hardwareanforderungen  
Für dieses Szenario müssen die folgenden Hardwareanforderungen erfüllt werden:  
  
-   Ein Computer, der die hardwareanforderungen für Windows Server 2016 oder Windows Server 2012 erfüllt.  
  
-   Um das Szenario testen zu können, muss mindestens ein Computer unter Windows 10, Windows 8 oder Windows 7, die als DirectAccess-Client konfiguriert.  
  
-   Ein OTP-Server, der PAP über RADIUS unterstützt  
  
-   Ein OTP-Hardware- oder Software-Token  
  
## <a name="BKMK_SOFT"></a>Softwareanforderungen  
Für dieses Szenario gelten eine Reihe von Anforderungen:  
  
1.  Softwareanforderungen für die Bereitstellung auf einem Einzelserver. Weitere Informationen finden Sie unter [Bereitstellen eines einzelnen DirectAccess-Servers mit erweiterten Einstellungen](../../directaccess/single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md).  
  
2.  Zusätzlich zu den softwareanforderungen für einen einzelnen Server stehen eine Anzahl von OTP\-besondere Anforderungen:  
  
    1.  Zertifizierungsstelle für die IPsec-Authentifizierung In eine OTP-Bereitstellung, die DirectAccess IPsec bereitgestellt werden müssen Computer die von einer Zertifizierungsstelle ausgestellte Zertifikate. Die IPsec-Authentifizierung mithilfe des RAS-Servers als Kerberos-Proxy wird bei der OTP-Bereitstellung nicht unterstützt. Eine interne Zertifizierungsstelle ist erforderlich.  
  
    2.  Zertifizierungsstelle für die OTP-Authentifizierung – ein Microsoft-Unternehmenszertifizierungsstelle \(auf Windows 2003 Server oder höher ausgeführt wird\) ist erforderlich, um die OTP-Clientzertifikate auszustellen. Es kann dieselbe Zertifizierungsstelle verwendet werden, die auch die Zertifikate für die IPsec-Authentifizierung ausstellt. Der Zertifizierungsstellenserver muss über den ersten Infrastrukturtunnel erreichbar sein.  
  
    3.  Security-Gruppe – zum Ausschließen von Benutzern vom strenge Authentifizierung, ist eine Active Directory-Sicherheitsgruppe, die mit diesen Benutzern erforderlich.  
  
    4.  Client\-clientseitige Anforderungen: für Windows 10 und Windows 8-Clientcomputern, die Netzwerkkonnektivitäts-Assistent \(NCA\) Dienst wird verwendet, um festzustellen, ob die OTP-Anmeldeinformationen erforderlich sind. Wenn dies der Fall, werden die DirectAccess-Medien-Manager zur Eingabe von Anmeldeinformationen aufgefordert.  Ratgeber für native Kompilierung ist im Betriebssystem enthalten, und die Installation oder Bereitstellung ist nicht erforderlich. Für Windows 7-Clientcomputer, DirectAccess Connectivity Assistant \(DCA\) 2.0 ist erforderlich. Dieser kann aus dem [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=29039)heruntergeladen werden.  
  
    5.  Beachten Sie Folgendes:  
  
        1.  OTP-Authentifizierung kann verwendet werden, parallel mit einer Smartcard und Trusted Platform Module \(TPM\)\--basierte Authentifizierung. Das Aktivieren der OTP-Authentifizierung in der Remotezugriffsverwaltungskonsole ermöglicht auch die Verwendung der Smartcard-Authentifizierung.  
  
        2.  Während der Benutzer mit Remotezugriff-Konfiguration in einer angegebenen Sicherheit kann der Gruppe aus zwei ausgenommen werden\-zweistufige Authentifizierung, und somit eine Authentifizierung mit Benutzernamen\/nur Kennwort.  
  
        3.  Die OTP-Modi "Neue PIN" und "Nächster Tokencode" werden nicht unterstützt.  
  
        4.  Bei einer Remotezugriffsbereitstellung an mehreren Standorten sind die OTP-Einstellungen global und dienen zur Identifikation an allen Einstiegspunkten. Wenn mehrere RADIUS- oder Zertifizierungsstellenserver für OTP konfiguriert werden, müssen sie von jedem RAS-Server anhand ihrer Verfügbarkeit und Nähe sortiert werden.  
  
        5.  Beim Konfigurieren von OTP in einer Remote-Zugriff mit mehreren\-gesamtstrukturumgebung, OTP-Zertifizierungsstellen sollten aus der Ressourcengesamtstruktur nur sein, und Registrierung von Zertifikaten muss zwischen Gesamtstruktur-Vertrauensstellungen konfiguriert werden. Weitere Informationen finden Sie unter [AD CS: Gesamtstrukturübergreifende Zertifikatsregistrierung mit Windows Server 2008 R2](https://technet.microsoft.com/library/ff955842.aspx).  
  
        6.  Benutzer, die einen KEY FOB OTP-Token verwenden, sollten die PIN und dann den Tokencode einfügen \(ohne Trennzeichen\) im DirectAccess-OTP-Dialogfeld. Benutzer, die einen PIN PAD OTP-Token verwenden, geben in diesem Dialogfeld nur den Tokencode ein.  
  
        7.  Bei aktiviertem WEBDAV darf OTP nicht aktiviert werden.  
  
## <a name="KnownIssues"></a>Bekannte Probleme  
Im Folgenden finden Sie bekannte Probleme beim Konfigurieren eines OTP-Szenarios:  
  
-   Remotezugriff verwendet einen Testmechanismus, um zu überprüfen, ob Verbindungen mit RADIUS\--basierten OTP-Servern. In einigen Fällen kann auf dem OTP-Server ein Fehler ausgelöst werden. Gehen Sie zur Vermeidung dieses Problems auf dem OTP-Server folgendermaßen vor:  
  
    -   Erstellen Sie ein Benutzerkonto entsprechend dem auf dem RAS-Server für den Testmechanismus konfigurierten Benutzernamen und Kennwort. Der Benutzername darf keinen Active Directory-Benutzer definieren.  
  
        Standardmäßig ist der Benutzername auf dem RAS-Server "DAProbeUser", und das Kennwort lautet "DAProbePass". Diese Standardeinstellungen können mithilfe der folgenden Werte in der Registrierung auf dem RAS-Server geändert werden:  
  
        -   HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Microsoft\\DirectAccess\\OTP\\RadiusProbeUser  
  
        -   HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Microsoft\\DirectAccess\\OTP\\ RadiusProbePass  
  
-   Wenn Sie das IPsec-Stammzertifikat in einer konfigurierten und ausgeführten DirectAccess-Bereitstellung ändern, funktioniert OTP nicht mehr. Führen Sie zum Beheben dieses Problems auf jedes DirectAccess-Server an einer Windows PowerShell-Eingabeaufforderung den Befehl ein: `iisreset`  
  
