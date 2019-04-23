---
title: Rollen, Rollendienste und Features in Windows Server - Server Core enthalten
description: Welche Rollen und Features sind in der Server Core-Installationsoption von Windows Server enthalten?
ms.prod: windows-server-threshold
ms.mktglfcycl: manage
ms.sitesec: library
author: lizap
ms.localizationpriority: medium
ms.date: 02/23/2018
ms.openlocfilehash: 65729eb68c9590fd6316f5650be48f33c19c926d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59859291"
---
# <a name="roles-role-services-and-features-included-in-windows-server---server-core"></a>Rollen, Rollendienste und Features in Windows Server - Server Core enthalten

> Gilt für: WindowsServer (Halbjährlicher Kanal) und WindowsServer 2016

Sprechen wir im allgemeinen [was des *nicht* in Server Core](server-core-removed-roles.md) – jetzt es geht um einen anderen Ansatz zu versuchen und sagen Sie Sie, was die *enthalten* und gibt an, ob etwas *standardmäßig installiert,*. Die folgenden Rollen, Rollendienste und Features sind *in* die Server Core-Installationsoption von Windows Server. Verwenden Sie diese Informationen, um zu ermitteln, ob die Server Core-Option für Ihre Umgebung funktioniert. Da es sich um eine umfangreiche Liste handelt, sollten Sie nach der bestimmter Rollen oder Features, die Sie interessiert: Wenn die Suche keine zurückgibt, wonach Sie suchen sie ist nicht in Server Core enthalten.

Wenn Sie nach "Remote Desktop Session Host" - Suchen finden nicht Sie es z. B. auf dieser Seite. Das ist da der Remotedesktop-Sitzungshost in Server Core-Images nicht enthalten ist.

Beachten Sie, dass Sie können [immer aussehen](server-core-removed-roles.md) auf welcher der *nicht* enthalten. Dies ist nur eine andere Möglichkeit, Dinge betrachten.

## <a name="roles-included-in-server-core"></a>Rollen im Server Core
Die Server Core-Installationsoption umfasst die folgenden Serverrollen.

| Role-Eigenschaft                                            | Name                           | Standardmäßig installiert? |
|-------------------------------------------------|--------------------------------|-----------------------|
| Active Directory-Zertifikatdienste           | AD-Zertifikat                 | N                     |
| Active Directory Domain Services                | AD-Domain-Services             | N                     |
| Active Directory-Verbunddienste (AD FS)            | AD FS-Verbund                | N                     |
| Active Directory Lightweight Directory Services | ADLDS                          | N                     |
| Active Directory-Rechteverwaltungsdienste     | AD RMS                          | N                     |
| Integritätsnachweis für Geräte                       | DeviceHealthAttestationService | N                     |
| DHCP-Server                                     | DHCP                           | N                     |
| DNS-Server                                      | DNS                            | N                     |
| Datei- und Speicherdienste                       | FileAndStorage-Services        | „Y“ zugeordnet ist                     |
| Host-Überwachungsdienst                           | HostGuardianServiceRole        | N                     |
| Hyper-V                                         | Hyper-V                        | N                     |
| Druck- und Dokumentdienste                     | Druckdienste                 | N                     |
| Remotezugriff                                   | RemoteAccess                   | N                     |
| Remotedesktopdienste                         | Remote Desktop Services        | N                     |
| Volumenaktivierungsdienste                      | VolumeActivation               | N                     |
| Webserver (IIS)                                  | Web-Server                     | N                     |
| Windows Server Essentials-Umgebung            | ServerEssentialsRole           | N                     |
| Windows Server Update Services                  | UpdateServices                 | N                     |

## <a name="role-services-included-in-server-core"></a>Rollendienste im Server Core enthalten
Die Server Core-Installationsoption umfasst die folgenden Rollendienste.

| Role-Eigenschaft                                  | Rollendienst                                                   | Name                    | Standardmäßig installiert? |
|---------------------------------------|----------------------------------------------------------------|-------------------------|-----------------------|
| Active Directory-Zertifikatdienste | Zertifizierungsstelle                                        | ADCS Zertifizierungsstelle     | N                     |
|                                       | Zertifikatregistrierungsrichtlinien-Webdienst                      | ADCS-Enroll-Web-Pol     | N                     |
|                                       | Zertifikatregistrierungs-Webdienst                             | ADCS-Enroll-Web-Svc     | N                     |
|                                       | Zertifizierungsstellen-Webregistrierung                         | ADCS-Web-Enrollment     | N                     |
|                                       | Registrierungsdienst für Netzwerkgeräte                              | ADCS-Device-Enrollment  | N                     |
|                                       | Online-Responder                                               | ADCS-Online-Cert        | N                     |
| Active Directory-Rechteverwaltungsdienste    | Active Directory-Rechteverwaltungsserver                      | AD RMS-Server            | N                     |
|                                       | Unterstützung für Identitätsverbund                                    | ADRMS-Identity          | N                     |
| Datei- und Speicherdienste             | Datei- und iSCSI-Dienste                                        | Dateidienste           | N                     |
|                                       | Dateiserver                                                    | EA-Dateiserver           | N                     |
|                                       | BranchCache für Netzwerkdateien                                  | FS-BranchCache          | N                     |
|                                       | Datendeduplizierung                                             | FS-Data-Deduplication   | N                     |
|                                       | DFS-Namespaces                                                 | FS-DFS-Namespace        | N                     |
|                                       | DFS-Replikation                                                | FS-DFS-Replication      | N                     |
|                                       | Ressourcen-Manager für Dateiserver                                   | FS-Resource-Manager     | N                     |
|                                       | Dateiserver-VSS-Agent-Dienst                                  | EA-VSS-Agent            | N                     |
|                                       | iSCSI-Zielserver                                            | iSCSITarget-Server      | N                     |
|                                       | iSCSI-Zielspeicheranbieter (VDS- und VSS-Hardwareanbieter) | iSCSITarget-VSS-VDS     | N                     |
|                                       | Server für NFS                                                 | FS-NFS-Service          | N                     |
|                                       | Arbeitsordner                                                   | FS-SyncShareService     | N                     |
|                                       | Speicherdienste                                               | Storage-Dienste        | „Y“ zugeordnet ist                     |
| Druck- und Dokumentdienste           | Druckerserver                                                   | Druckserver            | N                     |
|                                       | LPD-Dienst                                                    | Print-LPD-Service       | N                     |
| Remotezugriff                         | DirectAccess und VPN (RAS)                                     | DirectAccess-VPN        | N                     |
|                                       | Routing                                                        | Routing                 | N                     |
|                                       | Webanwendungsproxy                                          | Web-Application-Proxy   | N                     |
| Remotedesktopdienste               | Remotedesktop-Verbindungsbroker                               | RDS-Connection-Broker   | N                     |
|                                       | Remotedesktoplizenzierung                                       | RDS-Lizenzierung           | N                     |
|                                       | Remotedesktop-Virtualisierungshost                             | RDS-Virtualization      | N                     |
| Webserver (IIS)                      | Webserver                                                     | Web-WebServer           | N                     |
|                                       | Allgemeine HTTP-Features                                           | Web-Common-Http         | N                     |
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
|                                       | Anforderungsüberwachung                                              | Web-Request-Monitor     | N                     |
|                                       | Ablaufverfolgung                                                        | Web-Http-Tracing        | N                     |
|                                       | Leistung                                                    | Leistung des Webservers         | N                     |
|                                       | Komprimierung statischer Inhalte                                     | Web-Stat-Compression    | N                     |
|                                       | Komprimierung dynamischer Inhalte                                    | Web-Dyn-Komprimierung     | N                     |
|                                       | Sicherheit                                                       | Web-Sicherheit            | N                     |
|                                       | Request Filtering                                              | Web-Filterung           | N                     |
|                                       | Standardauthentifizierung                                           | Web-Basic-Auth          | N                     |
|                                       | Zentralisierte SSL-Zertifikatunterstützung                            | Web-CertProvider        | N                     |
|                                       | Authentifizierung durch Clientzertifikatszuordnung                      | Web-Client-Authentifizierung         | N                     |
|                                       | Digestauthentifizierung                                          | Web-Digest-Authentifizierung         | N                     |
|                                       | IIS-Clientzertifikatzuordnung                  | Web-Cert-Auth           | N                     |
|                                       | IP- und Domäneneinschränkungen                                     | Web-IP-Sicherheit         | N                     |
|                                       | URL-Autorisierung                                              | Web-Url-Auth            | N                     |
|                                       | Windows-Authentifizierung                                         | Web-Windows-Authentifizierung        | N                     |
|                                       | Anwendungsentwicklung                                        | Web-App-Entwickler             | N                     |
|                                       | .NET Erweiterbarkeit 3.5                                         | Web-Net-Ext             | N                     |
|                                       | Erweiterbarkeit für .NET 4.6                                         | Web-Net-Ext45           | N                     |
|                                       | Anwendungsinitialisierung                                     | Web-AppInit             | N                     |
|                                       | ASP                                                            | Web-ASP                 | N                     |
|                                       | ASP.NET 3.5                                                    | Web-Asp-Net             | N                     |
|                                       | ASP.NET 4.6                                                    | Web-Asp-Net45           | N                     |
|                                       | CGI                                                            | Web-CGI                 | N                     |
|                                       | ISAPI-Erweiterungen                                               | Web-ISAPI-Erweiterung           | N                     |
|                                       | ISAPI Filters                                                  | Web-ISAPI-Filter        | N                     |
|                                       | Serverseitige Includes (SSI)                                           | Web enthält            | N                     |
|                                       | WebSocket-Protokoll                                             | Web-WebSockets          | N                     |
|                                       | FTP-Server                                                     | Web-Ftp-Server          | N                     |
|                                       | FTP-Dienst                                                    | Web-Ftp-Service         | N                     |
|                                       | FTP-Erweiterbarkeit                                              | Web-Ftp-Ext             | N                     |
|                                       | Verwaltungstools                                               | Web-Mgmt-Tools          | N                     |
|                                       | Kompatibilität mit der IIS 6-Verwaltung                                 | Web-Mgmt-Anwendungskompatibilität         | N                     |
|                                       | IIS 6-Metabasiskompatibilität                                   | Web-Metabasis            | N                     |
|                                       | IIS 6-Skripttools                                          | Web-Lgcy-Scripting      | N                     |
|                                       | IIS 6-WMI-Kompatibilität                                        | Web-WMI                 | N                     |
|                                       | IIS-Verwaltungsskripts und -tools                               | Web-Scripting-Tools     | N                     |
|                                       | Verwaltungsdienst                                             | Web-Mgmt-Service        | N                     |
| Windows Server Update Services        | WID-Konnektivität                                               | UpdateServices-WidDB    | N                     |
|                                       | WSUS-Dienste                                                  | UpdateServices-Services | N                     |
|                                       | SQL Server-Konnektivität                                        | UpdateServices-DB       | N                     |

## <a name="features-included-in-server-core"></a>Server Core-Funktionen
Die Server Core-Installationsoption umfasst die folgenden Funktionen.

| Feature                                                | Name                               | Standardmäßig installiert? |
|--------------------------------------------------------|------------------------------------|-----------------------|
| .NET Framework 3.5-Features                            | NET-Framework-Features             | N                     |
| .NET Framework 3.5 (umfasst .NET 2.0 und 3.0)       | NET-Framework-Core                 | (entfernt)             |
| HTTP-Aktivierung                                        | NET-HTTP-Activation                | N                     |
| Nicht-HTTP-Aktivierung                                    | NET-Non-HTTP-Activ                 | N                     |
| .NET Framework 4.6-Features                            | NET-Framework-45-Features          | „Y“ zugeordnet ist                     |
| .NET Framework 4.6                                     | NET-Framework-45-Core              | „Y“ zugeordnet ist                     |
| ASP.NET 4.6                                            | NET-Framework-45-ASPNET            | N                     |
| WCF-Dienste                                           | NET-WCF-Services45                 | „Y“ zugeordnet ist                     |
| HTTP-Aktivierung                                        | NET-WCF-HTTP-Activation45          | N                     |
| Message Queuing (MSMQ)-Aktivierung                      | NET-WCF-MSMQ-Activation45          | N                     |
| Named Pipe-Aktivierung                                  | NET-WCF-Pipe-Activation45          | N                     |
| TCP-Aktivierung                                         | NET-WCF-TCP-Activation45           | N                     |
| TCP-Portfreigabe                                       | NET-WCF-TCP-PortSharing45          | „Y“ zugeordnet ist                     |
| BITS (Background Intelligent Transfer Service, Intelligenter Hintergrundübertragungsdienst)         | BITS                               | N                     |
| Compact Server                                         | BITS-Compact-Server                | N                     |
| BitLocker-Laufwerkverschlüsselung                             | BitLocker                          | N                     |
| BranchCache                                            | BranchCache                        | N                     |
| Client für NFS                                         | NFS-Client                         | N                     |
| Container                                             | Container                         | N                     |
| Data Center Bridging                                   | Data-Center-Bridging               | N                     |
| Erweitertes Speichern                                       | EnhancedStorage                    | N                     |
| Failoverclustering                                    | Failover-Clustering                | N                     |
| Gruppenrichtlinienverwaltung                                | GPMC                               | N                     |
| E/A: Quality of Service (QoS, Dienstqualität)                                 | DiskIo-QoS                         | N                     |
| Hostfähiger IIS-Webkern                                  | Web-WHC                            | N                     |
| IP-Adressverwaltungsserver (IPAM-Server)                    | IPAM                               | N                     |
| iSNS-Serverdienst                                    | ISNS                               | N                     |
| IIS-Erweiterung für OData Services for Management                         | ManagementOdata                    | N                     |
| Media Foundation                                       | Server-Media-Foundation            | N                     |
| Message Queuing                                        | MSMQ                               | N                     |
| Message Queuing-Dienste                               | MSMQ-Services                      | N                     |
| Message Queuing-Server                                 | MSMQ-Server                        | N                     |
| Verzeichnisdienstintegration                          | MSMQ-Directory                     | N                     |
| HTTP-Unterstützung                                           | MSMQ-HTTP-Support                  | N                     |
| Message Queuing-Trigger                               | MSMQ-Triggers                      | N                     |
| Routingdienst                                        | MSMQ-Routing                       | N                     |
| Message Queuing-DCOM-Proxy                             | MSMQ-DCOM                          | N                     |
| Multipfad-E/A                                          | Multipath-IO                       | N                     |
| MultiPoint-Connector                                   | MultiPoint-Connector               | N                     |
| MultiPoint-Connector-Diensten                          | MultiPoint-Connector-Services      | N                     |
| MultiPoint-Manager und MultiPoint-Dashboard            | MultiPoint-Tools                   | N                     |
| Netzwerklastenausgleich                                 | NLB                                | N                     |
| Peer Name Resolution-Protokoll                          | PNRP                               | N                     |
| Verbessertes Audio-/Videostreaming unter Windows                 | qWave                              | N                     |
| RDC (Remote Differential Compression)                        | RDC                                | N                     |
| Remoteserver-Verwaltungstools                     | RSAT                               | N                     |
| Featureverwaltungstools                           | RSAT-Feature-Tools                 | N                     |
| Verwaltungsdienstprogramme für BitLocker-Laufwerkverschlüsselung  | RSAT-Feature-Tools-BitLocker       | N                     |
| DataCenterBridging LLDP Tools                          | RSAT-DataCenterBridging-LLDP-Tools | N                     |
| Failoverclusteringtools                              | RSAT-Clustering                    | N                     |
| Failoverclustermodul für Windows PowerShell         | RSAT-Clustering-PowerShell         | N                     |
| Server für Failoverclusterautomatisierung                     | RSAT-Clustering-automationserver umgewandelt   | N                     |
| Failovercluster-Befehlsschnittstelle                     | RSAT-Clustering-CmdInterface       | N                     |
| IP-Adresse Management (IPAM)-Client                    | IPAM-Client-Feature                | N                     |
| Tools für abgeschirmte VMs                                      | RSAT-abgeschirmt-VM-Tools             | N                     |
| Storage-Replikat-Modul für Windows PowerShell          | RSAT-Storage-Replica               | N                     |
| Rollenverwaltungstools                              | RSAT-Role-Tools                    | N                     |
| AD DS- und AD LDS-Tools                                 | RSAT-AD-Tools                      | N                     |
| Active Directory-Modul für Windows PowerShell         | RSAT-AD-PowerShell                 | N                     |
| AD DS-Tools                                            | REMOTESERVER-VERWALTUNGSTOOLS WIRD HINZUGEFÜGT                          | N                     |
| Active Directory-Verwaltungscenter                 | RSAT-AD-AdminCenter                | N                     |
| AD DS-Snap-Ins und -Befehlszeilentools                  | RSAT-fügt-Tools                    | N                     |
| AD LDS-Snap-Ins und Befehlszeilen-Tools                 | RSAT-ADLDS                         | N                     |
| Hyper-V-Verwaltungstools                               | RSAT-Hyper-V-Tools                 | N                     |
| Hyper-V-Modul für Windows PowerShell                  | Hyper-V-PowerShell                 | N                     |
| Windows Serverupdate Services-Tools                   | UpdateServices-RSAT                | N                     |
| API und PowerShell-cmdlets                             | UpdateServices-API                 | N                     |
| DHCP-Servertools                                      | RSAT-DHCP                          | N                     |
| DNS-Servertools                                       | RSAT-DNS-Server                    | N                     |
| Remote-Verwaltungstools                         | RSAT-RemoteAccess                  | N                     |
| RAS-Modul für Windows PowerShell            | RSAT-RemoteAccess-PowerShell       | N                     |
| RPC über HTTP-Proxy                                    | RPC-over-HTTP-Proxy                | N                     |
| Ereignissammlung für Setup und Start                        | Setup-and-Boot-Event-Collection    | N                     |
| Einfache TCP/IP-Dienste                                 | Einfache TCP/IP                       | N                     |
| SMB 1.0-/CIFS-Dateifreigabeunterstützung                      | FS-SMB1                            | „Y“ zugeordnet ist                     |
| SMB-Bandbreiteneinschränkung                                    | EA-SMBBW                           | N                     |
| SNMP-Dienst                                           | SNMP-Service                       | N                     |
| SNMP WMI-Anbieter                                      | SNMP-WMI-Provider                  | N                     |
| Telnet-Client                                          | Telnet-Client                      | N                     |
| VM-Abschirmungstools für Fabric-Verwaltung               | FabricShieldedTools                | N                     |
| Windows Defender-Features                              | Windows Defender-Features          | „Y“ zugeordnet ist                     |
| Windows Defender                                       | Windows-Defender                   | „Y“ zugeordnet ist                     |
| Interne Windows-Datenbank                              | Windows-Internal-Database          | N                     |
| Windows PowerShell                                     | PowerShellRoot                     | „Y“ zugeordnet ist                     |
| Windows PowerShell 5.1                                 | PowerShell                         | „Y“ zugeordnet ist                     |
| Windows PowerShell 2.0-Engine                          | PowerShell-V2                      | (entfernt)             |
| Windows PowerShell Desired State Configuration-Diensts | DSC-Service                        | N                     |
| Windows PowerShell Web Access                          | WindowsPowerShellWebAccess         | N                     |
| Windows-Prozessaktivierungsdienst                     | WURDE                                | N                     |
| Prozessmodell                                          | WAR-Prozessmodell                  | N                     |
| .NET 3.5-Umgebung                                   | WAS-NET-Environment                | N                     |
| Konfigurations-APIs                                     | WAR-Config-APIs                    | N                     |
| Windows Server-Sicherung                                  | Windows Server-Sicherung              | N                     |
| Windows Server-Migrationstools                         | Migration                          | N                     |
| Standardbasierte Windows-Speicherverwaltung             | WindowsStorageManagementService    | N                     |
| WinRM-IIS-Erweiterung                                    | WinRM-IIS-Ext                      | N                     |
| WINS-Server                                            | WINS                               | N                     |
| WoW64-Unterstützung                                          | WoW64-Support                      | „Y“ zugeordnet ist                     |
|                                                        |                                    |                       |
