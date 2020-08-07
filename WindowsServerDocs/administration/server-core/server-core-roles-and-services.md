---
title: Rollen, Rollen Dienste und Features, die in Windows Server-Server Core enthalten sind
description: Welche Rollen und Features sind in der Server Core-Installationsoption von Windows Server enthalten?
ms.mktglfcycl: manage
ms.sitesec: library
author: lizap
ms.localizationpriority: medium
ms.date: 02/23/2018
ms.openlocfilehash: 1569feb27a75815771cf84317bebb2fde9d83dfa
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87895863"
---
# <a name="roles-role-services-and-features-included-in-windows-server---server-core"></a>Rollen, Rollen Dienste und Features, die in Windows Server-Server Core enthalten sind

> Gilt für: Windows Server 2019, Windows Server 2016 und Windows Server (halbjährlicher Kanal)

Im Allgemeinen sprechen wir über [das, was in Server Core *nicht* der Grund](server-core-removed-roles.md) ist: Wir testen nun einen anderen Ansatz und informieren Sie darüber, was *enthalten* ist und ob *standardmäßig etwas installiert*ist. Die folgenden Rollen, Rollen Dienste und Features sind *in* der Server Core-Installationsoption von Windows Server enthalten. Anhand dieser Informationen können Sie herausfinden, ob die Server Core-Option für Ihre Umgebung funktioniert. Da es sich hierbei um eine umfangreiche Liste handelt, sollten Sie die Suche nach der für Sie interessanten Rolle oder dem gewünschten Feature in Erwägung gezogen haben. wenn diese Suche nicht das gesuchte zurückgibt, ist es nicht in Server Core enthalten.

Wenn Sie z. b. nach "Remotedesktop-Sitzungshost" suchen, wird es auf dieser Seite nicht gefunden. Dies liegt daran, dass der RD-Sitzungshost nicht im Server Core-Image enthalten ist.

Denken Sie daran, dass Sie [immer sehen](server-core-removed-roles.md) können, was *nicht* enthalten ist. Dies ist nur eine andere Möglichkeit, Dinge zu betrachten.

## <a name="roles-included-in-server-core"></a>In Server Core enthaltene Rollen
Die Server Core-Installationsoption umfasst die folgenden Server Rollen.

| Role                                            | Name                           | Standardmäßig installiert? |
|-------------------------------------------------|--------------------------------|-----------------------|
| Active Directory-Zertifikatdienste           | AD-Zertifikat                 | N                     |
| Active Directory Domain Services                | AD-Domain-Services             | N                     |
| Active Directory-Verbunddienste (AD FS)            | AD FS-Verbund                | N                     |
| Active Directory Lightweight Directory Services | ADLDS                          | N                     |
| Active Directory-Rechteverwaltungsdienste     | ADRMS                          | N                     |
| Integritätsnachweis für Geräte                       | Devicehealthattestationservice | N                     |
| DHCP-Server                                     | DHCP                           | N                     |
| DNS-Server                                      | DNS                            | N                     |
| Datei- und Speicherdienste                       | Fileandstorage-Dienste        | J                     |
| Host-Überwachungsdienst                           | Hostguardianservicerole        | N                     |
| Hyper-V                                         | Hyper-V                        | N                     |
| Druck- und Dokumentdienste                     | Druckdienste                 | N                     |
| Remotezugriff                                   | RemoteAccess                   | N                     |
| Remotedesktopdienste                         | Remote Desktop Services        | N                     |
| Volumenaktivierungsdienste                      | VolumeActivation               | N                     |
| Webserver (IIS)                                  | Web-Server                     | N                     |
| Windows Server Essentials Experience            | Serveressentialsrole           | N                     |
| Windows Server Update Services                  | Update Services                 | N                     |

## <a name="role-services-included-in-server-core"></a>In Server Core enthaltene Rollen Dienste
Die Server Core-Installationsoption umfasst die folgenden Rollen Dienste.

| Role                                  | Rollendienst                                                   | Name                    | Standardmäßig installiert? |
|---------------------------------------|----------------------------------------------------------------|-------------------------|-----------------------|
| Active Directory-Zertifikatdienste | Zertifizierungsstelle                                        | ADCS Zertifizierungsstelle     | N                     |
|                                       | Zertifikatregistrierungsrichtlinien-Webdienst                      | ADCs-ENROLL-Web-Pol     | N                     |
|                                       | Zertifikatregistrierungs-Webdienst                             | ADCs-ENROLL-Web-SVC     | N                     |
|                                       | Zertifizierungsstellen-Webregistrierung                         | ADCs-Web-Einschreibung     | N                     |
|                                       | Registrierungsdienst für Netzwerkgeräte                              | ADCs-Geräteregistrierung  | N                     |
|                                       | Online-Responder                                               | ADCs-Online-CERT        | N                     |
| Active Directory Rights Management    | Active Directory-Rechteverwaltungsserver                      | ADRMS-Server            | N                     |
|                                       | Unterstützung für Identitätsverbund                                    | ADRMS-Identity          | N                     |
| Datei- und Speicherdienste             | Datei- und iSCSI-Dienste                                        | Dateidienste           | N                     |
|                                       | Dateiserver                                                    | EA-Dateiserver           | N                     |
|                                       | BranchCache für Netzwerkdateien                                  | FS-BranchCache          | N                     |
|                                       | Datendeduplizierung                                             | FS-Datendeduplizierung   | N                     |
|                                       | DFS-Namespaces                                                 | FS-DFS-Namespace        | N                     |
|                                       | DFS-Replikation                                                | FS-DFS-Replikation      | N                     |
|                                       | File Server Resource Manager                                   | FS-Resource-Manager     | N                     |
|                                       | Dateiserver-VSS-Agent-Dienst                                  | EA-VSS-Agent            | N                     |
|                                       | iSCSI Target Server                                            | iscsitarget-Server      | N                     |
|                                       | iSCSI-Zielspeicher Anbieter (VDS-und VSS-Hardware Anbieter) | iscsitarget-VSS-VDS     | N                     |
|                                       | Server für NFS                                                 | FS-NFS-Dienst          | N                     |
|                                       | Arbeitsordner                                                   | FS-syncshareservice     | N                     |
|                                       | Speicherdienste                                               | Speicherdienste        | J                     |
| Druck- und Dokumentdienste           | Druckerserver                                                   | Druck Server            | N                     |
|                                       | LPD-Dienst                                                    | Print-LPD-Service       | N                     |
| Remotezugriff                         | DirectAccess und VPN (RAS)                                     | DirectAccess-VPN        | N                     |
|                                       | Routing                                                        | Routing                 | N                     |
|                                       | Webanwendungsproxy                                          | Webanwendungsproxy   | N                     |
| Remotedesktopdienste               | Remotedesktop-Verbindungsbroker                               | RDS-Connection-Broker   | N                     |
|                                       | Remotedesktoplizenzierung                                       | RDS-Lizenzierung           | N                     |
|                                       | Remotedesktop-Virtualisierungshost                             | RDS-Virtualisierung      | N                     |
| Webserver (IIS)                      | Webserver                                                     | Web-WebServer           | N                     |
|                                       | Allgemeine HTTP-Funktionen                                           | Web-Common-Http         | N                     |
|                                       | Standarddokument                                               | Web-Default-Doc         | N                     |
|                                       | Verzeichnissuche                                             | Web-Dir-Browsing        | N                     |
|                                       | HTTP-Fehler                                                    | Web-Http-Fehler         | N                     |
|                                       | Statischer Inhalt                                                 | Statische Webinhalte      | N                     |
|                                       | HTTP-Umleitung                                               | Web-Http-Umleitung       | N                     |
|                                       | WebDAV-Veröffentlichung                                              | DAV-Webpublishing      | N                     |
|                                       | Integrität und Diagnose                                         | Web-Integrität              | N                     |
|                                       | HTTP-Protokollierung                                                   | Web-Http-Protokollierung        | N                     |
|                                       | Benutzerdefinierte Protokollierung                                                 | Web-Custom-Protokollierung      | N                     |
|                                       | Protokollierungstools                                                  | Web-Log-Libraries       | N                     |
|                                       | ODBC-Protokollierung                                                   | Web-ODBC-Protokollierung        | N                     |
|                                       | Anforderungs Monitor                                              | Web-Request-Monitor     | N                     |
|                                       | Ablaufverfolgung                                                        | Web-http-Ablauf Verfolgung        | N                     |
|                                       | Leistung                                                    | Leistung des Webservers         | N                     |
|                                       | Komprimierung statischer Inhalte                                     | Web-Stat-Compression    | N                     |
|                                       | Komprimierung dynamischer Inhalte                                    | Web-Dyn-Komprimierung     | N                     |
|                                       | Sicherheit                                                       | Web-Sicherheit            | N                     |
|                                       | Anforderungsfilterung                                              | Web-Filterung           | N                     |
|                                       | Standardauthentifizierung                                           | Web-Basic-Auth          | N                     |
|                                       | Zentralisierte Unterstützung von SSL-Zertifikaten                            | Web-CertProvider        | N                     |
|                                       | Authentifizierung durch Clientzertifikatszuordnung                      | Web-Client-Authentifizierung         | N                     |
|                                       | Digestauthentifizierung                                          | Web-Digest-Authentifizierung         | N                     |
|                                       | Authentifizierung durch IIS-Clientzertifikatszuordnung                  | Web-Cert-Auth           | N                     |
|                                       | IP-Adresse- und Domäneneinschränkungen                                     | Web-IP-Sicherheit         | N                     |
|                                       | URL-Autorisierung                                              | Web-Url-Auth            | N                     |
|                                       | Windows-Authentifizierung                                         | Web-Windows-Authentifizierung        | N                     |
|                                       | Anwendungsentwicklung                                        | Web-App-Entwickler             | N                     |
|                                       | .NET-Erweiterbarkeit 3.5                                         | Web-net-ext             | N                     |
|                                       | .NET-Erweiterbarkeit 4,6                                         | Web-net-Ext45           | N                     |
|                                       | Anwendungsinitialisierung                                     | Web-AppInit             | N                     |
|                                       | ASP                                                            | Web-ASP                 | N                     |
|                                       | ASP.NET 3.5                                                    | Web-ASP-NET             | N                     |
|                                       | ASP.NET 4,6                                                    | Web-ASP-Net45           | N                     |
|                                       | CGI                                                            | Web-CGI                 | N                     |
|                                       | ISAPI-Erweiterungen                                               | Web-ISAPI-Erweiterung           | N                     |
|                                       | ISAPI-Filter                                                  | Web-ISAPI-Filter        | N                     |
|                                       | Serverseitige Includes (SSI)                                           | Web enthält            | N                     |
|                                       | WebSocket-Protokoll                                             | Web-WebSockets          | N                     |
|                                       | FTP-Server                                                     | Web-FTP-Server          | N                     |
|                                       | FTP-Dienst                                                    | Web-FTP-Dienst         | N                     |
|                                       | FTP-Erweiterbarkeit                                              | Web-FTP-ext             | N                     |
|                                       | Verwaltungstools                                               | Web-Mgmt-Tools          | N                     |
|                                       | IIS 6-Verwaltungskompatibilität                                 | Web-Mgmt-Anwendungskompatibilität         | N                     |
|                                       | IIS 6-Metabasiskompatibilität                                   | Web-Metabasis            | N                     |
|                                       | IIS 6-Skripttools                                          | Web-lgcy-Scripting      | N                     |
|                                       | IIS 6-WMI-Kompatibilität                                        | Web-WMI                 | N                     |
|                                       | IIS-Verwaltungsskripts und -tools                               | Web-Scripting-Tools     | N                     |
|                                       | Verwaltungsdienst                                             | Web-Mgmt-Dienst        | N                     |
| Windows Server Update Services        | WID-Konnektivität                                               | Updateservices-widdb    | N                     |
|                                       | WSUS-Dienste                                                  | Updateservices-Dienste | N                     |
|                                       | SQL Server Konnektivität                                        | Updateservices-DB       | N                     |

## <a name="features-included-in-server-core"></a>In Server Core enthaltene Features
Die Server Core-Installationsoption umfasst die folgenden Features.

| Funktion                                                | Name                               | Standardmäßig installiert? |
|--------------------------------------------------------|------------------------------------|-----------------------|
| .NET Framework 3.5-Features                            | NET-Framework-Features             | N                     |
| .NET Framework 3,5 (einschließlich .NET 2,0 und 3,0)       | NET-Framework-Core                 | (entfernt)             |
| HTTP-Aktivierung                                        | NET-HTTP-Aktivierung                | N                     |
| Nicht-HTTP-Aktivierung                                    | Nicht-http-aktiv                 | N                     |
| .NET Framework 4,6-Features                            | NET-Framework-45-Features          | J                     |
| .NET Framework 4.6                                     | NET-Framework-45-Core              | J                     |
| ASP.NET 4,6                                            | NET-Framework-45-ASPNET            | N                     |
| WCF Services                                           | NET-WCF-Services45                 | J                     |
| HTTP-Aktivierung                                        | NET-WCF-HTTP-Activation45          | N                     |
| Message Queuing Aktivierung (MSMQ)                      | NET-WCF-MSMQ-Activation45          | N                     |
| Named Pipe-Aktivierung                                  | NET-WCF-Pipe-Activation45          | N                     |
| TCP-Aktivierung                                         | NET-WCF-TCP-Activation45           | N                     |
| TCP-Portfreigabe                                       | NET-WCF-TCP-PortSharing45          | J                     |
| Intelligenter Hintergrundübertragungsdienst (BITS – Background Intelligent Transfer Service)         | BITS                               | N                     |
| Compact Server                                         | BITS-Compact-Server                | N                     |
| BitLocker-Laufwerkverschlüsselung                             | BitLocker                          | N                     |
| BranchCache                                            | BranchCache                        | N                     |
| Client für NFS                                         | NFS-Client                         | N                     |
| Container                                             | Container                         | N                     |
| Data Center Bridging                                   | Data-Center-Bridging               | N                     |
| Erweitertes Speichern                                       | EnhancedStorage                    | N                     |
| Failoverclustering                                    | Failover-Clustering                | N                     |
| Gruppenrichtlinienverwaltung                                | GPMC                               | N                     |
| E/A: Quality of Service (QoS, Dienstqualität)                                 | Diskio-QoS                         | N                     |
| Hostfähiger IIS-Webkern                                  | Web-WHC                            | N                     |
| IP-Adressverwaltungsserver (IPAM-Server)                    | IPAM                               | N                     |
| iSNS-Serverdienst                                    | ISNS                               | N                     |
| IIS-Erweiterung für OData Services for Management                         | Managementodata                    | N                     |
| Media Foundation                                       | Server-Media-Foundation            | N                     |
| Message Queuing                                        | MSMQ                               | N                     |
| Message Queuing Dienste                               | MSMQ-Dienste                      | N                     |
| Message Queuing Server                                 | MSMQ-Server                        | N                     |
| Verzeichnisdienstintegration                          | MSMQ-Verzeichnis                     | N                     |
| HTTP-Unterstützung                                           | MSMQ-HTTP-Unterstützung                  | N                     |
| Message Queuing Trigger                               | MSMQ-Trigger                      | N                     |
| Routingdienst                                        | MSMQ-Routing                       | N                     |
| Message Queuing-DCOM-Proxy                             | MSMQ-DCOM                          | N                     |
| Multipfad-E/A                                          | Multipfad-e/a                       | N                     |
| MultiPoint-Connector                                   | Multipoint-Connector               | N                     |
| Multipoint-Connector-Dienste                          | Multipoint-Connector-Dienste      | N                     |
| Multipoint-Manager und Multipoint-Dashboard            | Multipoint-Tools                   | N                     |
| Netzwerklastenausgleich                                 | NLB                                | N                     |
| Peer Name Resolution-Protokoll                          | PNRP                               | N                     |
| Verbessertes Windows-Audio-/Video-Streaming                 | qWave                              | N                     |
| Remotedifferenzialkomprimierung                        | RDC                                | N                     |
| Remoteserver-Verwaltungstools                     | RSAT                               | N                     |
| Featureverwaltungstools                           | RSAT-Feature-Tools                 | N                     |
| BitLocker-Laufwerkverschlüsselung Verwaltungs Dienstprogramme  | RSAT-Feature-Tools-BitLocker       | N                     |
| Datacenterbridging LLDP-Tools                          | RSAT-datacenterbridging-LLDP-Tools | N                     |
| Failoverclusteringtools                              | RSAT-Clustering                    | N                     |
| Failoverclustermodul für Windows PowerShell         | RSAT-Clustering-PowerShell         | N                     |
| Failovercluster-Automatisierungs Server                     | RSAT-Clustering-automationserver umgewandelt   | N                     |
| Failovercluster-Befehlsschnittstelle                     | RSAT-Clustering-CmdInterface       | N                     |
| IP-Adressverwaltung (IPAM)-Client                    | IPAM-Client-Feature                | N                     |
| Abgeschirmte VM-Tools                                      | RSAT-abgeschirmt-VM-Tools             | N                     |
| Speicher Replikat Modul für Windows PowerShell          | RSAT-Speicher Replikat               | N                     |
| Rollenverwaltungstools                              | RSAT-Rollen Tools                    | N                     |
| AD DS- und AD LDS-Tools                                 | RSAT-AD-Tools                      | N                     |
| Active Directory-Modul für Windows PowerShell         | RSAT-AD-PowerShell                 | N                     |
| AD DS-Tools                                            | REMOTESERVER-VERWALTUNGSTOOLS WIRD HINZUGEFÜGT                          | N                     |
| Active Directory-Verwaltungscenter                 | RSAT-AD-AdminCenter                | N                     |
| AD DS-Snap-Ins und -Befehlszeilentools                  | RSAT-fügt-Tools                    | N                     |
| AD LDS Snap-Ins und Befehlszeilen Tools                 | RSAT-ADLDS                         | N                     |
| Hyper-V-Verwaltungstools                               | RSAT-Hyper-V-Tools                 | N                     |
| Hyper-V-Modul für Windows PowerShell                  | Hyper-V-PowerShell                 | N                     |
| Windows Server Update Services Tools                   | Updateservices-RSAT                | N                     |
| API-und PowerShell-Cmdlets                             | UpdateServices-API                 | N                     |
| DHCP-Server Tools                                      | RSAT-DHCP                          | N                     |
| DNS-Server Tools                                       | RSAT-DNS-Server                    | N                     |
| Tools für die Remote Zugriffs Verwaltung                         | RSAT-remoteaccess                  | N                     |
| RAS-Modul für Windows PowerShell            | RSAT-remoteaccess-PowerShell       | N                     |
| RPC über HTTP-Proxy                                    | RPC-über-HTTP-Proxy                | N                     |
| Ereignissammlung für Setup und Start                        | Setup-und-Boot-Event-Collection    | N                     |
| Einfache TCP/IP-Dienste                                 | Simple-tcpip                       | N                     |
| SMB 1.0-/CIFS-Dateifreigabeunterstützung                      | FS-Server Message Block                            | J                     |
| SMB-Bandbreiteneinschränkung                                    | EA-SMBBW                           | N                     |
| SNMP-Dienst                                           | SNMP-Dienst                       | N                     |
| SNMP-WMI-Anbieter                                      | SNMP-WMI-Provider                  | N                     |
| Telnet-Client                                          | Telnet-Client                      | N                     |
| VM-Abschirmungstools für Fabric-Verwaltung               | Fabricshieldedtools                | N                     |
| Windows Defender-Features                              | Windows-Defender-Features          | J                     |
| Windows Defender                                       | Windows-Defender                   | J                     |
| Interne Windows-Datenbank                              | Interne Windows-Datenbank          | N                     |
| Windows PowerShell                                     | Powershellroot                     | J                     |
| Windows PowerShell 5.1                                 | PowerShell                         | J                     |
| Windows PowerShell 2,0-Engine                          | PowerShell-v2                      | (entfernt)             |
| Windows PowerShell-Dienst zum Konfigurieren des gewünschten Zustands | DSC-Dienst                        | N                     |
| Windows PowerShell Web Access                          | WindowsPowerShellWebAccess         | N                     |
| Windows-Prozessaktivierungsdienst                     | WAS                                | N                     |
| Prozessmodell                                          | WAR-Prozessmodell                  | N                     |
| .NET-Umgebung 3,5                                   | Was-NET-Umgebung                | N                     |
| Konfiguration-APIs                                     | WAR-Config-APIs                    | N                     |
| Windows Server-Sicherung                                  | Windows Server-Sicherung              | N                     |
| Windows Server-Migrationstools                         | Migration                          | N                     |
| Standardbasierte Windows-Speicherverwaltung             | Windowsstoragemanagementservice    | N                     |
| WinRM-IIS-Erweiterung                                    | WinRM-IIS-ext                      | N                     |
| WINS-Server                                            | WINS                               | N                     |
| WoW64-Unterstützung                                          | WOW64-Unterstützung                      | J                     |
|                                                        |                                    |                       |
