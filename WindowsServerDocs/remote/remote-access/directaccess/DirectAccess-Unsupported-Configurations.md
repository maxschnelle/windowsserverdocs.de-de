---
title: DirectAccess nicht unterstützte Konfigurationen
description: Dieses Thema enthält eine Liste der nicht unterstützten DirectAccess-Konfigurationen in Windows Server 2016.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-da
ms.topic: article
ms.assetid: 23d05e61-95c3-4e70-aa83-b9a8cae92304
ms.author: lizross
author: eross-msft
ms.openlocfilehash: e59fd85fae3333ec3a5751ba611b615f4af92cb0
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86960242"
---
# <a name="directaccess-unsupported-configurations"></a>DirectAccess nicht unterstützte Konfigurationen

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Überprüfen Sie die folgende Liste mit nicht unterstützten DirectAccess-Konfigurationen, bevor Sie mit der Bereitstellung beginnen, damit Sie die Bereitstellung nicht erneut starten müssen.  

## <a name="file-replication-service-frs-distribution-of-group-policy-objects-sysvol-replications"></a><a name="bkmk_frs"></a>Verteilung des Datei Replikations Dienstanbieter (FRS) von Gruppenrichtlinie Objekten (SYSVOL-Replikationen)  
Stellen Sie DirectAccess nicht in Umgebungen bereit, in denen die Domänen Controller den Datei Replikations Dienst (File Replication Service, FRS) für die Verteilung von Gruppenrichtlinie Objekten (SYSVOL-Replikationen) ausführen. Die Bereitstellung von DirectAccess wird bei Verwendung von FRS nicht unterstützt.  
  
Sie verwenden FRS, wenn Sie über Domänen Controller verfügen, auf denen Windows Server 2003 oder Windows Server 2003 R2 ausgeführt wird. Außerdem können Sie FRS verwenden, wenn Sie zuvor Windows 2000 Server oder Windows Server 2003-Domänen Controller verwendet haben und nie die SYSVOL-Replikation von FRS zu verteiltes Dateisystem Replikation (DFS-R) migriert haben.  
  
Wenn Sie DirectAccess mit der FRS-SYSVOL-Replikation bereitstellen, riskieren Sie das unbeabsichtigte Löschen von DirectAccess-Gruppenrichtlinie Objekten, die den DirectAccess-Server und die Client Konfigurationsinformationen enthalten. Wenn diese Objekte gelöscht werden, kommt es bei der DirectAccess-Bereitstellung zu einem Ausfall, und Client Computer, die DirectAccess verwenden, sind nicht in der Lage, eine Verbindung mit Ihrem Netzwerk herzustellen.  
  
Wenn Sie DirectAccess bereitstellen möchten, müssen Sie Domänen Controller verwenden, auf denen Betriebssysteme als Windows Server 2003 R2 ausgeführt werden, und Sie müssen DFS-R verwenden.  
  
Informationen zum Migrieren von FRS zu DFS-R finden Sie unter [SYSVOL Replication Migration Guide: FRS to DFS-Replikation](../../../storage/dfs-replication/migrate-sysvol-to-dfsr.md).  
  
## <a name="network-access-protection-for-directaccess-clients"></a><a name="bkmk_nap"></a>Netzwerk Zugriffsschutz für DirectAccess-Clients  
Der Netzwerk Zugriffsschutz (Network Access Protection, NAP) wird verwendet, um zu bestimmen, ob Remote Client Computer IT-Richtlinien erfüllen, bevor Sie Zugriff auf das Unternehmensnetzwerk erhalten NAP wurde in Windows Server 2012 R2 als veraltet markiert und ist nicht in Windows Server 2016 enthalten. Aus diesem Grund wird das Starten einer neuen Bereitstellung von DirectAccess mit NAP nicht empfohlen. Es wird empfohlen, die Sicherheit von DirectAccess-Clients mit einer anderen Methode zu bestimmen.  
  
## <a name="multisite-support-for-windows-7-clients"></a><a name="bkmk_multi"></a>Unterstützung für mehrere Standorte für Windows 7-Clients  
Wenn DirectAccess in einer Bereitstellung mit mehreren Standorten konfiguriert ist, können Windows 10 &reg; -, Windows &reg; 8,1-und Windows &reg; 8-Clients eine Verbindung mit dem nächstgelegenen Standort herstellen.  Windows 7- &reg; Client Computer verfügen nicht über die gleiche Funktion. Die Standort Auswahl für Windows 7-Clients wird zum Zeitpunkt der Richtlinien Konfiguration auf einen bestimmten Standort festgelegt, und diese Clients stellen unabhängig von Ihrem Standort stets eine Verbindung mit dem angegebenen Standort her.  
  
## <a name="user-based-access-control"></a><a name="bkmk_user"></a>Benutzerbasierte Zugriffs Steuerung  
DirectAccess-Richtlinien sind computerbasiert, Nichtbenutzer basiert. Das Angeben von DirectAccess-Benutzerrichtlinien zum Steuern des Zugriffs auf das Unternehmensnetzwerk wird nicht unterstützt.  
  
## <a name="customizing-directaccess-policy"></a><a name="bkmk_policy"></a>Anpassen der DirectAccess-Richtlinie  
DirectAccess kann mit dem DirectAccess-Setup-Assistenten, der Remote Zugriffs-Verwaltungskonsole oder den Windows PowerShell-Cmdlets für den Remote Zugriff konfiguriert werden. Die Verwendung einer anderen Methode als dem DirectAccess-Setup-Assistenten zum Konfigurieren von DirectAccess, wie z. b. das direkte Ändern von DirectAccess-Gruppenrichtlinie Objekten oder das manuelle Ändern der Standardrichtlinien Einstellungen auf dem Server oder Client, wird nicht unterstützt. Diese Änderungen können zu einer nicht verwendbaren Konfiguration führen.  
  
## <a name="kerbproxy-authentication"></a><a name="bkmk_kerb"></a>Kerbproxy-Authentifizierung  
Wenn Sie einen DirectAccess-Server mit dem Assistenten für die ersten Schritte konfigurieren, wird der DirectAccess-Server automatisch für die Verwendung der kerbproxy-Authentifizierung für die Computer-und Benutzerauthentifizierung konfiguriert. Aus diesem Grund sollten Sie den Assistenten für die ersten Schritte nur für bereit Stellungen mit nur einem Standort verwenden, bei denen nur Windows 10- &reg; , Windows 8.1-oder Windows 8-Clients bereitgestellt werden.  
  
Außerdem sollten die folgenden Funktionen nicht mit der kerbproxy-Authentifizierung verwendet werden:  
  
-   Lastenausgleich mit einem externen Load Balancer oder Windows Load   
    Ausgleichsmodul  
  
-   Zweistufige Authentifizierung, bei der Smartcards oder ein einmal Kennwort (OTP) erforderlich sind  
  
Die folgenden Bereitstellungs Pläne werden nicht unterstützt, wenn Sie die kerbproxy-Authentifizierung aktivieren:  
  
-   Multisite.  
  
-   DirectAccess-Unterstützung für Windows 7-Clients.  
  
-   Tunnel Erzwingung. Konfigurieren Sie beim Ausführen des Assistenten die folgenden Elemente, um sicherzustellen, dass die kerbproxy-Authentifizierung bei Verwendung von Tunnel Erzwingung nicht aktiviert ist:  
  
    -   Aktivieren des Erzwingens von Tunneln  
  
    -   Aktivieren von DirectAccess für Windows 7-Clients  
  
> [!NOTE]  
> Für die vorherigen bereit Stellungen sollten Sie den Assistenten für die erweiterte Konfiguration verwenden, der eine zwei-Tunnel-Konfiguration mit einem Zertifikat basierten Computer und einer Benutzerauthentifizierung verwendet. Weitere Informationen finden Sie unter Bereitstellen [eines einzelnen DirectAccess-Servers mit erweiterten Einstellungen](../../remote-access/directaccess/single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md).  
  
## <a name="using-isatap"></a><a name="bkmk_isa"></a>Verwenden von ISATAP  
ISATAP ist eine Übergangstechnologie, die IPv6-Konnektivität in reinen IPv4-Unternehmensnetzwerken bereitstellt. Er ist auf kleine und mittelgroße Unternehmen mit einer einzelnen DirectAccess-Server Bereitstellung beschränkt und ermöglicht die Remote Verwaltung von DirectAccess-Clients. Wenn ISATAP eine Umgebung mit mehreren Standorten, Lastenausgleich oder mehreren Domänen bereitstellt, müssen Sie Sie entfernen oder in eine systemeigene IPv6-Bereitstellung verschieben, bevor Sie DirectAccess konfigurieren.  
  
## <a name="iphttps-and-one-time-password-otp-endpoint-configuration"></a><a name="bkmk_iphttps"></a>Endpunkt Konfiguration für IPHTTPS und einmal Kennwort (One-time password, OTP)  
Wenn Sie IPHTTPS verwenden, muss die IPHTTPS-Verbindung auf dem DirectAccess-Server und nicht auf einem anderen Gerät (z. b. einem Load Balancer) beendet werden. Entsprechend muss die während der einmal Kennwort-Authentifizierung (PP) erstellte out-of-Band-Secure Sockets Layer (SSL)-Verbindung auf dem DirectAccess-Server beendet werden. Alle Geräte zwischen den Endpunkten dieser Verbindungen müssen im Pass-Through-Modus konfiguriert werden.  
  
## <a name="force-tunnel-with-otp-authentication"></a><a name="bkmk_ft"></a>Tunnel mit OTP-Authentifizierung erzwingen  
Stellen Sie keinen DirectAccess-Server mit zweistufiger Authentifizierung mit OTP bereit, und erzwingen Sie Tunnelung, weil die OTP-Authentifizierung fehlschlägt. Zwischen dem DirectAccess-Server und dem DirectAccess-Client ist eine Out-of-Band-Secure Sockets Layer (SSL)-Verbindung erforderlich. Diese Verbindung erfordert eine Ausnahme, um den Datenverkehr außerhalb des DirectAccess-Tunnels zu senden. In einer Tunnel Erzwingungs Konfiguration muss sämtlicher Datenverkehr über einen DirectAccess-Tunnel geleitet werden, und nach der Tunnel Erstellung ist keine Ausnahme zulässig. Aus diesem Grund wird die OTP-Authentifizierung in einer erzwungenen Tunnel Konfiguration nicht unterstützt.  
  
## <a name="deploying-directaccess-with-a-read-only-domain-controller"></a><a name="bkmk_rodc"></a>Bereitstellen von DirectAccess mit einem schreibgeschützten Domänen Controller  
DirectAccess-Server benötigen Zugriff auf einen Domänen Controller mit Lese-/Schreibzugriff und funktionieren nicht ordnungsgemäß mit einem schreibgeschützten Domänen Controller (Read-Only Domain Controller, RODC).  
  
Ein Domänen Controller mit Lese-/Schreibzugriff ist aus vielen Gründen erforderlich, einschließlich der folgenden:  
  
-   Auf dem DirectAccess-Server ist ein Domänen Controller mit Lese-/Schreibzugriff erforderlich, um die Microsoft Management Console (MMC) für den Remote Zugriff zu öffnen.  
  
-   Der DirectAccess-Server muss sowohl den DirectAccess-Client als auch den DirectAccess-Server Gruppenrichtlinie Objekte (GPOs) lesen und schreiben.  
  
-   Der DirectAccess-Server liest und schreibt das Client-Gruppenrichtlinien Objekt speziell aus dem primären Domänen Controller Emulator (PDCE).  
  
Stellen Sie DirectAccess aufgrund dieser Anforderungen nicht mit einem RODC bereit.  
  
