---
title: Sicherheit und Assurance
description: Übersicht über die Sicherheit in Windows Server 2016
ms.topic: article
ms.date: 07/27/2018
ms.assetid: b886b2fd-3567-4f0a-8aa3-4ba7923d2d21
ms.author: lizross
author: eross-msft
manager: mtillman
ms.localizationpriority: medium
ms.openlocfilehash: 86011cbe4ba748347e049699a716ec38d462a788
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89641196"
---
# <a name="security-and-assurance-in-windows-server"></a>Sicherheit und Sicherheit in Windows Server

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

>[!TIP]
> Suchen Sie nach Informationen zu älteren Versionen von Windows Server? Sehen Sie sich unsere [Windows Server-Bibliotheken](/previous-versions/windows/) auf „docs.microsoft.com“ an. Sie können auch nach bestimmten Informationen [auf dieser Website suchen](/search/index?dataSource=previousVersions&search=Windows+Server).

<img src="../media/landing-icons/security.png" style='float:left; padding:.5em;' alt="Icon representing a lock"> Sie können sich auf neue Schutz Ebenen stützen, die in das Betriebssystem integriert sind, um Schutz vor Sicherheitsverletzungen zu gewährleisten. Wehren Sie bedrohliche Angriffe ab und erhöhen Sie die Sicherheit Ihrer virtuellen Maschinen, Anwendungen und Daten.


### <a name="windows-server-security-blog-post"></a>[Blogbeitrag zur Windows Server-Sicherheit](https://blogs.technet.microsoft.com/windowsserver/2016/04/25/ten-reasons-youll-love-windows-server-2016-8-security/)
In diesem Blogbeitrag des Windows Server-Sicherheitsteams werden viele der Verbesserungen in Windows Server beschrieben, mit denen die Sicherheit beim Hosten und in Hybrid Cloud-Umgebungen erhöht wird.

### <a name="datacenter-and-private-cloud-security-blog"></a>[Datacenter and Private Cloud Security Blog (Blog zur Sicherheit in Rechenzentren und Private Clouds)](/archive/blogs/datacentersecurity/)
Dies ist die zentrale Blogwebsite für technische Inhalte des Microsoft Datacenter and Private Cloud Security-Teams.

### <a name="addressing-emerging-threats-and-landscape-shifts"></a>[Addressing emerging threats and landscape shifts (Reaktion auf neue Bedrohungen und Änderungen der Systemlandschaft)](https://www.youtube.com/watch?v=B5JMYxYWx1k&feature=youtu.be)
In diesem sechsminütigen Video vermittelt Anders Vinberg zunächst einen Überblick über die Sicherheits- und Zusicherungsstrategien von Microsoft und spricht über Branchentrends und sicherheitsrelevante Veränderungen in der Systemlandschaft. Vinberg legt dann den Schwerpunkt auf die wichtigsten Initiativen von Microsoft, um Workloads gegen das zugrunde liegende Fabric und direkte Angriffe von privilegierten Konten zu schützen. Außerdem erläutert er, wie Bedrohungen mithilfe der neuen Ermittlungsfunktionen und forensischen Funktionen besser erkannt werden können.

### <a name="protecting-your-datacenter-and-cloud-from-emerging-threats-blog-post"></a>[Blogbeitrag „Protecting Your Datacenter and Cloud from Emerging Threats“ (Schützen von Rechenzentren und Cloudumgebungen gegen neue Bedrohungen)](https://blogs.technet.com/b/windowsserver/archive/2015/11/18/protecting-your-datacenter-and-cloud-november-update.aspx)
In diesem Blogbeitrag wird erläutert, wie Sie Microsoft-Technologien einsetzen können, um Ihre Rechenzentrums- und Cloudinvestitionen gegen neue Bedrohungen zu schützen.

### <a name="security-and-assurance-overview-session-at-ignite"></a>[Ignite-Sitzung mit einer Übersicht über „Sicherheit und Zuverlässigkeit”](https://channel9.msdn.com/events/ignite/2015/brk2482)
Inhalt dieser Ignite-Sitzung sind dauerhafte Bedrohungen, Sicherheitsverstöße durch interne Mitarbeiter einer Organisation, organisierte Internetkriminalität sowie das Absichern der Microsoft Cloud Platform (lokale und mit Azure verbundene Dienste). Dabei werden u. a. Szenarien für das Schützen von Workloads, großen Unternehmensmandanten und Dienstanbietern beschrieben.

## <a name="secure-virtualization-with-shielded-vms"></a>Sichere Virtualisierung mit abgeschirmten VMs

### <a name="shielded-vm-in-channel-9"></a>[Abgeschirmte VMs auf Channel 9](https://channel9.msdn.com/Shows/Mechanics/Introduction-to-Shielded-Virtual-Machines-in-Windows-Server-2016)
Eine exemplarische Vorgehensweise zu abgeschirmten VM-Technologien und Vorteilen.

### <a name="shielded-vm-demo"></a>[Video zu abgeschirmten VMs](https://www.youtube.com/watch?v=xip5Qtk-7d8)
In diesem 4-minütigen Video werden der Nutzen abgeschirmter VMs sowie die Unterschiede zwischen einer abgeschirmten VM und einer nicht abgeschirmten VM erläutert.

### <a name="shielded-virtual-machines-in-windows-server-video-walkthrough"></a>[Video mit exemplarischer Vorgehensweise „Shielded Virtual Machines in Windows Server“](http://microsoft-cloud.cloudguides.com/Guides/Shielded Virtual Machines in Windows Server.htm)
In diesem Video mit exemplarischer Vorgehensweise wird gezeigt, wie der Host-Überwachungsdienst die Verwendung abgeschirmter virtueller Computer ermöglicht, damit sensible Daten vor einem nicht autorisierten Zugriff durch Hyper-V-Hostadministratoren geschützt werden.

### <a name="harden-the-fabric-protecting-tenant-secrets-in-hyper-v-ignite-video"></a>[„Harden the Fabric: Protecting Tenant Secrets in Hyper-V“ (Absichern des Fabrics: Schützen geheimer Mandantendaten in Hyper-V) (Ignite-Video)](https://channel9.msdn.com/events/ignite/2015/brk3457)

Diese Ignite-Präsentation erläutert Erweiterungen in Hyper-V, Virtual Machine Manager und eine neue Host-Überwachungsdienst-Serverrolle zur Aktivierung von abgeschirmten VMs.

### <a name="guarded-fabric-deployment-guide"></a>[Guarded Fabric Deployment Guide (Bereitstellungsleitfaden für geschütztes Fabric)](./guarded-fabric-shielded-vm/guarded-fabric-deploying-hgs-overview.md)
Dieser Leitfaden umfasst Installations- und Validierungsinformationen für Windows Server und System Center Virtual Machine Manager für Hosts mit geschütztem Fabric und abgeschirmten VMs.

### <a name="shielded-vm-and-guarded-fabric-in-branch-offices"></a>[Abgeschirmte VMs und geschützte Fabrics in Filialen](./guarded-fabric-shielded-vm/guarded-fabric-manage-branch-office.md)
Dieses Handbuch enthält bewährte Methoden für die Ausführung von abgeschirmten virtuellen Computern in Filialen und anderen Remoteszenarien, in denen Hyper-V-Hosts Zeiträume mit eingeschränkter Konnektivität zu HGS haben können.

### <a name="shielded-vm-and-guarded-fabric-troubleshooting-guide"></a>[Shielded VM and Guarded Fabric Troubleshooting Guide (Leitfaden zur Problembehandlung für abgeschirmte VMs und geschütztes Fabric)](./guarded-fabric-shielded-vm/guarded-fabric-troubleshoot-overview.md)
In diesem Leitfaden finden Sie Informationen zur Behandlung von Problemen, die in Ihrer Umgebung mit abgeschirmten VMs auftreten können.

### <a name="shielded-vm-article"></a>[Artikel zu abgeschirmten VMs](http://windowsitpro.com/hyper-v/super-secure-hyper-v-environments-shielded-vms-2016)
In diesem Whitepaper können Sie sich einen Überblick darüber verschaffen, wie sich die Sicherheit mit abgeschirmten VMs verbessern lässt und wie Sie Manipulationen mithilfe dieser VMs verhindern können.

## <a name="privileged-access-management"></a>Privileged Access Management (Schützen von Windows und Microsoft Azure Active Directory mit Privileged Access Management)
### <a name="securing-privileged-access"></a>[Schützen des privilegierten Zugriffs](../identity/securing-privileged-access/securing-privileged-access.md)
Ein Fahrplan zum Schutz Ihres privilegierten Zugriffs. Dieser Wegweiser basiert auf dem geballten Fachwissens des Teams für die Sicherheit von Servern, der Microsoft-IT, des Azure-Teams und Microsoft Consulting Services.

### <a name="just-in-time-administration-with-microsoft-identity-manager"></a>[Just in Time Administration with Microsoft Identity Manager (Just-In-Time-Verwaltung mit Microsoft Identity Manager)](/microsoft-identity-manager/pam/privileged-identity-management-for-active-directory-domain-services)
In diesem Artikel werden Features und Funktionen von Microsoft Identity Manager beschrieben. Dazu zählt auch die Unterstützung für Just-In-Time-Privileged Access Management.

### <a name="protecting-windows-and-microsoft-azure-active-directory-with-privileged-access-management"></a>[Video über den Schutz von Windows und Microsoft Azure Active Directory mit privilegierter Zugriffsverwaltung](https://channel9.msdn.com/events/ignite/2015/brk3873)
In dieser Ignite-Präsentation wird auf die Strategie und die Investitionen von Microsoft bei Windows Server, PowerShell, Active Directory, Identity Manager und Azure Active Directory eingegangen, um mithilfe einer sichereren Authentifizierung und durch die Verwaltung des Zugriffs über Just-In-Time- und Just Enough Administration-Verfahren (JEA) dem Risiko eines Administratorzugriffs entgegenzuwirken.

### <a name="just-enough-administration-article"></a>[Artikel zu Just Enough Administration](https://aka.ms/JEA)
In diesem Dokument werden die Vision und technische Details von Just Enough Administration beschrieben, einem PowerShell-Toolkit, mit dem Organisationen den Administratorzugriff auf die Aufgaben beschränken können, die der jeweilige Mitarbeiter ausführen muss.

### <a name="just-enough-administration-demo-video"></a>[Demovideo zu Just Enough Administration](https://www.youtube.com/watch?v=xnBrbkY9P20)
Just Enough Administration – exemplarische Vorgehensweise.
## <a name="credential-protection"></a>Schutz von Anmeldeinformationen

### <a name="protect-derived-domain-credentials-with-credential-guard"></a>[Schützen abgeleiteter Domänenanmeldeinformationen mit Credential Guard](/windows/security/identity-protection/credential-guard/credential-guard)
Credential Guard nutzt auf Virtualisierung basierende Sicherheitsverfahren, um geheime Daten zu isolieren, damit nur durch privilegierte Systemsoftware auf diese Daten zugegriffen werden kann. Nicht autorisierter Zugriff auf diese geheimen Schlüssel kann zum Diebstahl von Anmeldeinformationen führen, z. B. durch einen Pass-the-Hash- oder einen Pass-the-Ticket-Angriff. Credential Guard verhindert diese Angriffe, indem NTLM-Kennworthashes und Kerberos Ticket Granting Tickets geschützt werden.

### <a name="protect-remote-desktop-credentials-with-remote-credential-guard"></a>[Schützen von Remotedesktop-Anmeldeinformationen mit Remote Credential Guard](/windows/security/identity-protection/remote-credential-guard)
Mit Remote Credential Guard können Sie Ihre Anmeldeinformationen über eine Remotedesktopverbindung schützen, indem Kerberos-Anforderungen an das Gerät zurückgeleitet werden, das die Verbindung anfordert. Darüber hinaus profitieren Sie mit dieser Lösung von einer SSO-Umgebung (Single Sign-On, einmaliges Anmelden) für Remotedesktopsitzungen.                                                                                                        |
### <a name="credential-guard-demo-video"></a>[Demovideo zu Credential Guard](https://www.youtube.com/watch?v=eUpKOGSl7yk)
Dieses fünfminütige Video enthält Informationen über Credential Guard und Remote Credential Guard.

## <a name="hardening-the-os-and-applications"></a>Härtung des Betriebssystems und der Anwendungen
### <a name="windows-defender-application-control-wdac-deployment-guide"></a>[Bereitstellungshandbuch zu Windows Defender-Anwendungssteuerung (WDAC)](/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control)
Bei der WDAC handelt es sich um eine konfigurierbare Richtlinie zur Codeintegrität (CI), die Unternehmen dabei hilft zu steuern, welche Anwendungen in ihrer Umgebung ausgeführt werden. Sie hat keine speziellen Hardware- oder Softwareanforderungen, muss jedoch unter Windows 10 ausgeführt werden.

### <a name="device-guard-demo-video"></a>[Demovideo zu Device Guard](https://www.youtube.com/watch?v=F-pTkesjkhI)
Device Guard ist eine Kombination aus WDAC und Hypervisor-geschützter Codeintegrität (HVCI). Dieses siebenminütige Video enthält Informationen über Device Guard und seine Verwendung unter Windows Server.

### <a name="transport-layer-security-registry-settings"></a>[Registrierungseinstellungen für Transport Layer Security](./tls/tls-registry-settings.md)
Informationen zu unterstützten Registrierungseinstellungen für die Implementierung des Transport Layer Security (TLS)- und des Secure Sockets Layer (SSL)-Protokolls unter Windows.

### <a name="control-flow-guard"></a>[Ablaufsteuerungsschutz](/windows/desktop/SecBP/control-flow-guard)
Der Ablaufsteuerungsschutz bietet integrierten Schutz gegen einige Fälle von Speicherbeschädigungsangriffen.

### <a name="windows-defender"></a>[Windows Defender](./windows-defender/windows-defender-overview-windows-server.md)
Windows Defender bietet Funktionen zum aktiven Schutz, um bekannte Schadsoftware zu blockieren. Windows Defender ist standardmäßig aktiviert und für die Unterstützung der verschiedenen Serverrollen in Windows Server optimiert.

## <a name="detecting-and-responding-to-threats"></a>Ermitteln von und Reagieren auf Bedrohungen
### <a name="security-threat-analysis-using-microsoft-operations-management-suite"></a>[Security Threat Analysis Using Microsoft Operations Management Suite (Analyse von Sicherheitsbedrohungen mit Microsoft Operations Management Suite)](https://channel9.msdn.com/events/ignite/2015/brk3464)
In dieser Ignite-Präsentation wird erläutert, wie Sie Operational Insights für eine Analyse von Sicherheitsbedrohungen nutzen können.

### <a name="microsoft-operations-management-suite-oms"></a>[Microsoft Operations Management Suite (OMS)](https://www.microsoft.com/server-cloud/operations-management-suite/overview.aspx)
Die Sicherheits- und Überwachungslösung Microsoft Operations Management Suite (OMS) verarbeitet Sicherheitsprotokolle und Firewallereignisse aus lokalen und cloudbasierten Umgebungen, um böswilliges Verhalten zu analysieren und zu ermitteln.

### <a name="oms-and-windows-server"></a>[Microsoft Operations Management Suite (OMS) und Windows Server](https://www.youtube.com/watch?v=_SaDw1dRy2k)
Dieses dreiminütige Video zeigt, wie OMS dabei helfen kann, potentielles böswilliges Verhalten zu erkennen, das von Windows Server blockiert wird.

### <a name="microsoft-advanced-threat-analytics"></a>[Microsoft Advanced Threat Analytics](https://blogs.technet.com/b/ad/archive/2015/07/22/microsoft-advanced-threat-analytics-coming-next-month.aspx)
In diesem Blogbeitrag wird Microsoft Advanced Threat Analytics vorgestellt, eine lokale Lösung, die anhand von Active Directory-Netzwerkdatenverkehr und SIEM-Daten potenzielle Bedrohungen ermittelt und entsprechende Warnungen generiert.

### <a name="microsoft-advanced-threat-analytics"></a>[Microsoft Advanced Threat Analytics](https://www.youtube.com/watch?v=0nA9FeTRZFw&list=PL8nfc9haGeb5IZGM8HvmRozetHRpBDKSw)
Dieses 3-minütige Video bietet einen Überblick darüber, wie Microsoft Bedrohungsanalyse Funktionen in Windows Server hinzufügt.                                                                                 |

## <a name="network-security"></a>Netzwerksicherheit

### <a name="datacenter-firewall-overview"></a>[Übersicht über Datacenter Firewall](/previous-versions/windows/server/dn920240(v=ws.12))
In dieser Übersicht wird Datacenter Firewall erläutert, eine zustandsbehaftete, mehrinstanzenfähige 5-Tupel-Firewall (Protokoll, Portnummer von Quelle und Ziel sowie IP-Adresse von Quelle und Ziel), die auf der Vermittlungsschicht implementiert ist.

### <a name="whats-new-in-dns-in-windows-server"></a>[What's New in DNS in Windows Server (Neues in DNS unter Windows Server)](../networking/dns/what-s-new-in-dns-server.md)
In dieser Übersicht finden Sie eine kurze Beschreibung der neuen Funktionen in DNS sowie eine Reihe von Links, um auf weitere Informationen zuzugreifen.

## <a name="mapping-security-features-to-compliance-regulations"></a>Abbilden von Compliancebestimmungen auf Sicherheitsfunktionen

Die Kompatibilität ist ein wichtiger Aspekt der Sicherheitsfunktionen. Wir freuen uns darüber, wie Sie Ihre Konformität erreichen und wie Sie ihren vertrauenswürdigen Compliance-Beratern entsprechen, aber wir möchten auch eine anfängliche Zuordnung bereitstellen, die Sie bei der Evaluierung von Windows Server verwenden können.

-   [Whitepaper zur Kompatibilitätszuordnung von abgeschirmten Hyper-V-VMs (in englischer Sprache)](https://download.microsoft.com/download/6/D/0/6D06E149-B4C1-4EED-ACD5-DF6066E93CC0/Coalfire_Branded_Hyper_V_Shielded_VMs_Whitepaper_EN_US.pdf)

-   [Whitepaper zur Kompatibilitätszuordnung von JEA und JIT (in englischer Sprache)](https://download.microsoft.com/download/2/7/A/27A2B5BB-6B52-4482-87C1-DA9D6B6D8C8D/Coalfire_Branded_Privileged_Identity_Manager_Whitepaper_EN_US.pdf)

-   [Whitepaper zur Kompatibilitätszuordnung von Device Guard (in englischer Sprache)](https://download.microsoft.com/download/6/9/D/69D9E610-D23C-4F7E-A8CC-D65B87CEB4F8/Coalfire_Branded_Device_Guard_Whitepaper_EN_US.pdf)

-   [Whitepaper zur Kompatibilitätszuordnung von Credential Guard (in englischer Sprache)](https://download.microsoft.com/download/8/1/2/812009C9-E4B8-4D4B-AADD-FDC373D0A076/Coalfire_Branded_Credential_Guard_Whitepaper_EN_US.pdf)

-   [Whitepaper zur Kompatibilitätszuordnung von Windows Defender (in englischer Sprache)](https://download.microsoft.com/download/C/7/7/C778B7BB-0783-42D7-93A9-B86DFB5A7BAD/Coalfire_Branded_Windows_Defender_Whitepaper_EN_US.pdf)