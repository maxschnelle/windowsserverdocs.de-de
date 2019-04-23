---
title: DirectAccess nicht unterstützte Konfigurationen
description: Dieses Thema enthält eine Liste der nicht unterstützten Konfigurationen von DirectAccess in Windows Server 2016.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-da
ms.topic: article
ms.assetid: 23d05e61-95c3-4e70-aa83-b9a8cae92304
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 49fa86883e6a590ac8f7dcf0c724f87af419f88e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59828851"
---
# <a name="directaccess-unsupported-configurations"></a>DirectAccess nicht unterstützte Konfigurationen

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Überprüfen Sie die folgende Liste von nicht unterstützten Konfigurationen von DirectAccess, bevor Sie beginnen, dass die Bereitstellung, um zu vermeiden, dass Ihre Bereitstellung erneut zu starten.  

## <a name="bkmk_frs"></a>Datei (File Replication Service, FRS) Verteilung von Gruppenrichtlinienobjekten (Replikationen SYSVOL)  
Stellen Sie keine DirectAccess in Umgebungen, auf dem Domänencontroller den Dateireplikationsdienst (FRS) für die Verteilung von Gruppenrichtlinienobjekten (SYSVOL-Replikationen) ausgeführt werden. Bereitstellung von DirectAccess wird nicht unterstützt, bei der Verwendung von FRS  
  
Wenn Sie Domänencontroller, auf denen Windows Server 2003 oder Windows Server 2003 R2 ausgeführt werden, verwenden Sie Dateireplikationsdienst (FRS). Darüber hinaus verwenden Sie möglicherweise Dateireplikationsdienst (FRS) Wenn Sie bereits Windows 2000 Server oder Windows Server 2003-Domänencontrollern und Sie nie SYSVOL-Replikation von der FRS-zu Distributed File System Replication (DFS-R migriert).  
  
Wenn Sie DirectAccess mit FRS SYSVOL-Replikation bereitstellen, besteht die Gefahr, der versehentlich Löschung von DirectAccess-Gruppenrichtlinienobjekt-Objekten, dass der DirectAccess-Server und Client-Konfigurationsinformationen enthalten. Wenn diese Objekte gelöscht werden, treten einen Ausfall in der DirectAccess-Bereitstellung, und Clientcomputer, auf denen Verwendung von DirectAccess werden nicht in der Lage, eine Verbindung mit Ihrem Netzwerk herstellen.  
  
Wenn Sie DirectAccess bereitstellen möchten, müssen verwenden Sie Domänencontroller, auf denen Betriebssysteme als Windows Server 2003 R2 ausgeführt werden, und Sie DFS-R.  
  
Informationen für die Migration von FRS zur DFS-R finden Sie in der [Anleitung zur SYSVOL-Replikationsmigration: FRS-zu DFS-Replikation](https://technet.microsoft.com/library/dd640019(v=ws.10).aspx).  
  
## <a name="bkmk_nap"></a>Netzwerkzugriffsschutz für DirectAccess-clients  
(Network Access Protection, NAP) wird verwendet, um festzustellen, ob Remoteclientcomputer IT-Richtlinien erfüllen, bevor sie Zugriff auf das Unternehmensnetzwerk gewährt werden. NAP wurde in Windows Server 2012 R2 als veraltet markiert und ist nicht in Windows Server 2016 enthalten. Aus diesem Grund wird das Starten einer neuen Bereitstellung von DirectAccess mit NAP nicht empfohlen. Eine andere Methode des Endpunkt-Steuerelements für die Sicherheit der DirectAccess-Clients wird empfohlen.  
  
## <a name="bkmk_multi"></a>Unterstützung mehrerer Standorte für Windows 7-clients  
Wenn DirectAccess konfiguriert ist, in einer Bereitstellung für mehrere Standorte, Windows 10&reg;, Windows&reg; 8.1 und Windows&reg; 8-Clients verfügen über eine Funktion mit dem nächsten Standort verbunden.  Windows 7&reg; Clientcomputer verfügen nicht über die gleiche Funktionalität. Website-Auswahl für Windows 7-Clients zu einer bestimmten Website zum Zeitpunkt der Konfiguration festgelegt ist, und diese Clients werden stets eine Verbindung mit diesem angegebenen Standort, unabhängig von ihrem Standort.  
  
## <a name="bkmk_user"></a>Benutzer-based Access Control  
DirectAccess-Richtlinien sind Computer basiert, nicht benutzerbasierten. Festlegung von Benutzerrichtlinien für DirectAccess zum Steuern des Zugriffs mit dem Unternehmensnetzwerk verbunden wird nicht unterstützt.  
  
## <a name="bkmk_policy"></a>Anpassen der DirectAccess-Richtlinie  
DirectAccess kann mithilfe des DirectAccess-Setup-Assistenten, der Remotezugriffs-Verwaltungskonsole oder der Remotezugriffs-Windows PowerShell-Cmdlets konfiguriert werden. Verwenden ausschließlich den DirectAccess-Setup-Assistenten zum Konfigurieren von DirectAccess, z. B. DirectAccess-Gruppenrichtlinienobjekte direkt zu ändern oder Manuelles Ändern der Einstellungen der Standardrichtlinie auf dem Server oder Client wird nicht unterstützt. Diese Änderungen können dazu führen, dass eine Konfiguration kann nicht verwendet werden.  
  
## <a name="bkmk_kerb"></a>KerbProxy-Authentifizierung  
Wenn Sie einen DirectAccess-Server mit dem Assistenten für erste Schritte konfigurieren, wird der DirectAccess-Server automatisch konfiguriert, um KerbProxy für Computer und Benutzerauthentifizierung verwenden. Aus diesem Grund Sie sollten nur verwenden den Assistenten für erste Schritte für Bereitstellungen mit einem Standort, in dem nur Windows 10&reg;, Windows 8.1 oder Windows 8-Clients bereitgestellt werden.  
  
Darüber hinaus sollten die folgenden Funktionen nicht mit KerbProxy-Authentifizierung verwendet werden:  
  
-   Lastenausgleich mithilfe eines externen Lastenausgleichs vorgenommen wird oder Windows zu laden.   
    Lastenausgleich  
  
-   Zwei-Faktor-Authentifizierung, die denen Smartcards oder ein Einmalkennwort (OTP) erforderlich sind  
  
Die folgenden Bereitstellungspläne werden nicht unterstützt, wenn Sie KerbProxy Authentifizierung aktivieren:  
  
-   Mehrere Standorte.  
  
-   DirectAccess für Windows 7-Clients unterstützen.  
  
-   Des Erzwingens von Tunneln. Konfigurieren Sie die folgenden Elemente beim Ausführen des Assistenten, um sicherzustellen dass KerbProxy Authentifizierung nicht aktiviert ist, bei der Verwendung des Erzwingens von Tunneln:  
  
    -   Aktivieren des Erzwingens von Tunneln  
  
    -   Aktivieren von DirectAccess für Windows 7-clients  
  
> [!NOTE]  
> Für die vorherige Bereitstellung sollten Sie erweiterte Konfigurations-Assistenten verwenden, die eine zwei-Tunnel-Konfiguration mit einem Zertifikat-basierte Computer und Benutzer-Authentifizierung verwendet. Weitere Informationen finden Sie unter [Bereitstellen eines einzelnen DirectAccess-Servers mit erweiterten Einstellungen](../../remote-access/directaccess/single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md).  
  
## <a name="bkmk_isa"></a>Verwenden von ISATAP  
ISATAP ist eine Technologie, die IPv6-Konnektivität im IPv4-Unternehmensnetzwerk bereitstellt. Es ist für kleine und mittelgroße Organisationen mit einer einzelnen Bereitstellung von DirectAccess-Server beschränkt, und es ermöglicht die Remoteverwaltung von DirectAccess-Clients. Ist ISATAP Deployedin eine Multisite, Lastenausgleich oder multidomänenumgebung, müssen Sie entfernen oder verschieben Sie es in eine systemeigene IPv6-Bereitstellung aus, bevor Sie DirectAccess konfigurieren.  
  
## <a name="bkmk_iphttps"></a>(IPHTTPS) verwendet und die Endpunktkonfiguration Einmalkennwort (OTP)  
Bei der Verwendung (IPHTTPS) verwendet werden, muss die IP-Verbindung auf dem DirectAccess-Server nicht auf einem anderen Gerät, z. B. einen Load Balancer beendet werden. Auf ähnliche Weise muss die Out-of-Band-Secure Sockets Layer (SSL)-Verbindung, die während der Authentifizierung mit Einmalkennwort (OTP) erstellt wird, auf dem DirectAccess-Server beenden. Alle Geräte, die zwischen den Endpunkten dieser Verbindungen müssen im Pass-Through-Modus konfiguriert werden.  
  
## <a name="bkmk_ft"></a>Tunnel erzwingen mit OTP-Authentifizierung  
Stellen Sie einen DirectAccess-Server mit zwei-Faktor-Authentifizierung mit OTP und Erzwingen von Tunneln keine oder OTP-Authentifizierung fehl. Eine Out-of-Band-Verbindung Secure Sockets Layer (SSL) ist erforderlich, zwischen dem DirectAccess-Server und dem DirectAccess-Client. Diese Verbindung muss es sich um eine Ausnahme aus, um den Datenverkehr aus dem DirectAccess-Tunnel zu senden. Klicken Sie in einer Konfiguration mit-Force-Tunneling alle Datenverkehr muss über einen DirectAccess-Tunnel weitergeleitet, und keine Ausnahme ist zulässig, nachdem der Tunnel eingerichtet wurde. Aus diesem Grund wird es nicht unterstützt, um die OTP-Authentifizierung in einer Konfiguration mit erzwungenes Tunneling zu erhalten.  
  
## <a name="bkmk_rodc"></a>Bereitstellen von DirectAccess mit einem schreibgeschützten Domänencontroller  
DirectAccess-Server benötigen Zugriff auf einen Domänencontroller mit Lese-/ Schreibzugriff und funktionieren nicht ordnungsgemäß mit einem schreibgeschützten Domänencontroller (RODC).  
  
Ein Domänencontroller mit Lese-/ Schreibzugriff ist für viele Gründe infrage, einschließlich der folgenden erforderlich:  
  
-   Auf dem DirectAccess-Server ist ein Domänencontroller mit Lese-/ Schreibzugriff erforderlich, um die Remote Access Microsoft Management Console (MMC) zu öffnen.  
  
-   Der DirectAccess-Server muss Lese- und Schreibzugriffs auf das DirectAccess-Client und der DirectAccess-Server die Gruppenrichtlinienobjekte (GPOs).  
  
-   Der DirectAccess-Server liest und schreibt in das Client-Gruppenrichtlinienobjekt, speziell über den primären Domänencontroller-Emulator (PDCe).  
  
Aufgrund dieser Anforderungen stellen Sie DirectAccess mit einem RODC nicht bereit.  
  


