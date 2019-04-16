---
title: Rollen, Rollendienste und Features in Windows Server - Server Core enthalten
description: Welche Rollen und Funktionen sind in die Server Core-Installationsoption von Windows Server enthalten?
ms.prod: windows-server-threshold
ms.mktglfcycl: manage
ms.sitesec: library
author: lizap
ms.localizationpriority: medium
ms.date: 02/23/2018
ms.openlocfilehash: 65729eb68c9590fd6316f5650be48f33c19c926d
ms.sourcegitcommit: 439edac95e1427086268cab469ed03b94db630da
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2018
ms.locfileid: "2217740"
---
# <a name="roles-role-services-and-features-included-in-windows-server---server-core"></a>Rollen, Rollendienste und Features in Windows Server - Server Core enthalten

> Betrifft: WindowsServer (Semikolons jährlichen Channel) und WindowsServer 2016

Wir sprechen im Allgemeinen über [Was des *nicht* in Server Core](server-core-removed-roles.md) – jetzt wenden wir sind, versuchen Sie es einen anderen Ansatz und erfahren Sie, was *enthalten* ist und ob etwas *standardmäßig installiert*ist. Die folgenden Rollen, Rollendienste und Features sind *in* die Server Core-Installationsoption von Windows Server. Anhand dieser Informationen können Sie ermitteln, ob die Server Core-Option für Ihre Umgebung funktioniert. Da es sich um eine umfangreiche Liste handelt, sollten Sie für die Rolle oder das Feature Sie interessieren - Wenn, dass die Suche nicht zurückgegeben wird, wonach Sie suchen sie ist nicht in Server Core enthalten.

Suchen Sie "Remote Desktop Session Host" - wird nicht Sie es beispielsweise auf dieser Seite finden. Dies liegt daran RD-Sitzungshost nicht in die Server Core-Bild enthalten ist.

Beachten Sie, dass [immer suchen](server-core-removed-roles.md) Sie können unter Was ist *nicht* enthalten. Dies ist nur eine andere Möglichkeit zum Betrachten Dinge.

## <a name="roles-included-in-server-core"></a>Server Core Rollen
Die Server Core-Installationsoption umfasst die folgenden Serverrollen.

| Rolle                                            | Name                           | Standardmäßig installiert? |
|-------------------------------------------------|--------------------------------|-----------------------|
| Active Directory-Zertifikatdienste           | AD-Zertifikat                 | N                     |
| ActiveDirectory-Domänendienste (ADDS)                | Active Directory-Domänendienste             | N                     |
| Active Directory-Verbunddienste            | AD FS-Verbund                | N                     |
| Active Directory Lightweight Directory Services | ADLDS                          | N                     |
| Active Directory-Rechteverwaltungsdienste     | ADRMS                          | N                     |
| Integritätsnachweis für Geräte                       | DeviceHealthAttestationService | N                     |
| DHCP-Server                                     | DHCP                           | N                     |
| DNS-Server                                      | DNS                            | N                     |
| Datei- und Speicherdienste                       | FileAndStorage-Dienste        | Y                     |
| Host-Überwachungsdienst                           | HostGuardianServiceRole        | N                     |
| Hyper-V                                         | Hyper-V                        | N                     |
| Druck- und Dokumentdienste                     | Print-Dienste                 | N                     |
| Remote Access                                   | RAS                   | N                     |
| Remotedesktopdienste                         | Remote-Desktop-Dienste        | N                     |
| Volumenaktivierungsdienste                      | VolumeActivation               | N                     |
| IIS-Webserver                                  | Webserver                     | N                     |
| Windows Server Essentials Experience            | ServerEssentialsRole           | N                     |
| Windows Server Update Services                  | UpdateServices                 | N                     |

## <a name="role-services-included-in-server-core"></a>Rollendienste in Server Core enthalten
Die Server Core-Installationsoption umfasst die folgenden Rollendienste.

| Rolle                                  | Rollendienst                                                   | Name                    | Standardmäßig installiert? |
|---------------------------------------|----------------------------------------------------------------|-------------------------|-----------------------|
| Active Directory-Zertifikatdienste | Zertifizierungsstelle                                        | MDE-Zertifizierungsstelle     | N                     |
|                                       | Zertifikat Registrierungs-Webdienst                      | MDE-registrieren-Web-Pol     | N                     |
|                                       | Zertifikat Registrierungs-Webdienst                             | MDE-registrieren-Web-Svc     | N                     |
|                                       | Certification Authority Web-Registrierung                         | MDE-Web-Registrierung     | N                     |
|                                       | Registrierungsdiensts                              | MDE-Gerät-Registrierung  | N                     |
|                                       | Online-Responder                                               | MDE-Online-Zertifikat        | N                     |
| Active Directory-Rechteverwaltungsdienste    | Active Directory-Rechteverwaltungsserver                      | ADRMS-Server            | N                     |
|                                       | Unterstützung für Identitätsverbund                                    | ADRMS-Identity          | N                     |
| Datei- und Speicherdienste             | Datei- und iSCSI-Dienste                                        | Dateidienste           | N                     |
|                                       | Dateiserver                                                    | FS-Dateiserver           | N                     |
|                                       | BranchCache für Netzwerkdateien                                  | FS-BranchCache          | N                     |
|                                       | Datendeduplizierung                                             | FS Datendeduplizierung   | N                     |
|                                       | DFS-Namespaces                                                 | FS-DFS-Namespace        | N                     |
|                                       | DFS-Replikation                                                | FS-DFS-Replikation      | N                     |
|                                       | Ressourcen-Manager für Dateiserver                                   | FS-Ressourcen-Manager     | N                     |
|                                       | Dateiserver-VSS-Agent-Dienst                                  | FS-VSS-Agent            | N                     |
|                                       | iSCSI-Zielserver                                            | iSCSITarget-Server      | N                     |
|                                       | iSCSI-Ziel-Speicher-Anbieter (VDS und VSS-Hardwareanbieter) | iSCSITarget-VSS-VDS     | N                     |
|                                       | Server für NFS                                                 | FS-NFS-Dienst          | N                     |
|                                       | Arbeitsordner                                                   | FS-SyncShareService     | N                     |
|                                       | Speicherdienste                                               | Speicher-Services        | Y                     |
| Druck- und Dokumentdienste           | Druckserver                                                   | Print-Server            | N                     |
|                                       | LPD-Dienst                                                    | Print-LPD-Dienst       | N                     |
| Remote Access                         | DirectAccess und VPN-RAS)                                     | VPN-DirectAccess        | N                     |
|                                       | Routing                                                        | Routing                 | N                     |
|                                       | Webanwendungsproxy                                          | Web-Anwendung-Proxy   | N                     |
| Remotedesktopdienste               | Remote Desktop Connection Broker                               | RDS-Verbindung-Broker   | N                     |
|                                       | Remote Desktop Lizenzierung                                       | RDS-Lizenzierung           | N                     |
|                                       | Host Remote Desktop-Virtualisierung                             | RDS-Virtualisierung      | N                     |
| Webserver (IIS)                      | Webserver                                                     | Web-WebServer           | N                     |
|                                       | Allgemeine HTTP-Features                                           | Web-Common-http-         | N                     |
|                                       | Standarddokument                                               | Web-Standard-Doc         | N                     |
|                                       | Durchsuchen von Verzeichnissen                                             | Dir-Browsen im Web        | N                     |
|                                       | HTTP-Fehler                                                    | Web-Http-Fehler         | N                     |
|                                       | Statischer Inhalt                                                 | Statische Webinhalte      | N                     |
|                                       | HTTP-Umleitung                                               | Web-Http-Umleitung       | N                     |
|                                       | WebDAV-Veröffentlichung                                              | Web-DAV-Veröffentlichung      | N                     |
|                                       | Integrität und Diagnose                                         | Web-Integrität              | N                     |
|                                       | HTTP-Protokollierung                                                   | Web-Http-Protokollierung        | N                     |
|                                       | Benutzerdefinierte Protokollierung                                                 | Web-benutzerdefinierte-Protokollierung      | N                     |
|                                       | Protokollierungstools                                                  | Web-Protokoll-Bibliotheken       | N                     |
|                                       | ODBC-Protokollierung                                                   | Web-ODBC-Protokollierung        | N                     |
|                                       | Anforderungsüberwachung                                              | Web-Anforderung-Monitor     | N                     |
|                                       | Ablaufverfolgung                                                        | Web-Http-Protokollierung        | N                     |
|                                       | Leistung                                                    | Web-Leistung         | N                     |
|                                       | Komprimierung statischer Inhalte                                     | Web-Stat-Komprimierung    | N                     |
|                                       | Komprimierung dynamischer Inhalte                                    | Web-Dyn-Komprimierung     | N                     |
|                                       | Sicherheit                                                       | Web-Sicherheit            | N                     |
|                                       | Anforderungsfilterung                                              | Web-Filterung           | N                     |
|                                       | Standardauthentifizierung                                           | Web-Basic-Auth          | N                     |
|                                       | Zentralisierte SSL-Zertifikat-Unterstützung                            | Web-CertProvider        | N                     |
|                                       | Clientzertifikatzuordnungs-Authentifizierung                      | Web-Client-Authentifizierung         | N                     |
|                                       | Digest-Authentifizierung                                          | Web-Digest-Authentifizierung         | N                     |
|                                       | IIS Clientzertifikatzuordnungs-Authentifizierung                  | Web-Cert-Auth           | N                     |
|                                       | IP-Adresse und Domäne-Einschränkungen                                     | Web-IP-Sicherheit         | N                     |
|                                       | URL-Autorisierung                                              | Web-Url-Auth            | N                     |
|                                       | Windows-Authentifizierung                                         | Web-Windows-Authentifizierung        | N                     |
|                                       | Application Development                                        | Web-App-Dev             | N                     |
|                                       | Erweiterbarkeit der .NET 3.5                                         | Web-Net-App.             | N                     |
|                                       | .NET Erweiterbarkeit 4.6                                         | Web-Net-Ext45           | N                     |
|                                       | Initialisieren der Anwendung                                     | Web-AppInit             | N                     |
|                                       | ASP (ENGL.)                                                            | Web-ASP (engl.)                 | N                     |
|                                       | ASP.NET 3.5                                                    | Web-Asp-Net             | N                     |
|                                       | ASP.NET 4.6                                                    | Web-Asp-Net45           | N                     |
|                                       | CGI                                                            | Web-CGI                 | N                     |
|                                       | ISAPI-Erweiterungen                                               | Web-ISAPI-App.           | N                     |
|                                       | ISAPI-Filter                                                  | Web-ISAPI-Filter        | N                     |
|                                       | Serverseitige Includes                                           | Web-enthält            | N                     |
|                                       | WebSocket-Protokoll                                             | Web-WebSockets          | N                     |
|                                       | FTP-Server                                                     | Ftp-Webserver          | N                     |
|                                       | FTP-Dienst                                                    | Ftp-Webdienst         | N                     |
|                                       | FTP-Erweiterbarkeit                                              | Web-Ftp-App.             | N                     |
|                                       | Verwaltungstools                                               | Web-Mgmt-Tools          | N                     |
|                                       | IIS 6-Verwaltungskompatibilität                                 | Web-Mgmt-Compat         | N                     |
|                                       | IIS 6-Metabasiskompatibilität                                   | Web-Metabasis            | N                     |
|                                       | IIS 6-Skriptingtools                                          | Web-Lgcy-Skripts      | N                     |
|                                       | IIS 6-WMI-Kompatibilität                                        | Web-WMI                 | N                     |
|                                       | IIS-Verwaltungsskripts und-Tools                               | Web Skriptingtools     | N                     |
|                                       | Verwaltungsdienst                                             | Web-Mgmt-Service        | N                     |
| Windows Server Update Services        | WID-Konnektivität                                               | UpdateServices WidDB    | N                     |
|                                       | WSUS-Dienste                                                  | UpdateServices-Dienste | N                     |
|                                       | SQL Server-Konnektivität                                        | UpdateServices-DB       | N                     |

## <a name="features-included-in-server-core"></a>Funktionen in Server Core
Die Server Core-Installationsoption umfasst die folgenden Funktionen.

| Feature                                                | Name                               | Standardmäßig installiert? |
|--------------------------------------------------------|------------------------------------|-----------------------|
| .NET Framework 3.5-Features                            | NET-Framework-Features             | N                     |
| .NET Framework 3.5 (einschließlich .NET 2.0 und 3.0)       | NET Framework-Kernen                 | (entfernt)             |
| HTTP-Aktivierung                                        | NET-HTTP-Aktivierung                | N                     |
| Nicht-HTTP-Aktivierung                                    | NET-nicht-HTTP-Dienstanwendung                 | N                     |
| .NET Framework 4.6-Features                            | NET-Framework-45-Features          | Y                     |
| .NET Framework 4.6                                     | NET Framework-45 Kernen              | Y                     |
| ASP.NET 4.6                                            | NET Framework-45 ASPNET            | N                     |
| WCF-Dienste                                           | NET-WCF-Services45                 | Y                     |
| HTTP-Aktivierung                                        | NET-WCF-HTTP-Activation45          | N                     |
| Message Queuing (MSMQ) Aktivierung                      | NET-WCF-MSMQ-Activation45          | N                     |
| Aktivierung von Named Pipes                                  | NET-WCF-Pipe-Activation45          | N                     |
| TCP-Aktivierung                                         | NET-WCF-TCP-Activation45           | N                     |
| Freigeben von TCP-Port                                       | NET-WCF-TCP-PortSharing45          | Y                     |
| Background Intelligent Transfer Service (BITS)         | BITS                               | N                     |
| Kompaktes Server                                         | BITS-CD-Server                | N                     |
| BitLocker-Laufwerkverschlüsselung                             | BitLocker                          | N                     |
| BranchCache                                            | BranchCache                        | N                     |
| Client für NFS                                         | NFS-Client                         | N                     |
| Container                                             | Container                         | N                     |
| Data Center Bridging                                   | Data-Center-Bridging               | N                     |
| Erweitertes Speichern                                       | EnhancedStorage                    | N                     |
| Failoverclusterunterstützung                                    | Failover-Clusterunterstützung                | N                     |
| Gruppenrichtlinienverwaltung                                | GRUPPENRICHTLINIEN-VERWALTUNGSKONSOLE                               | N                     |
| E/A: Quality of Service (QoS, Dienstqualität)                                 | DiskIo QoS                         | N                     |
| Hostfähiger IIS-Webkern                                  | Web-WHC                            | N                     |
| IP-Adresse Verwaltungsserver (IPAM)                    | IPAM                               | N                     |
| iSNS-Serverdienst                                    | ISNS                               | N                     |
| IIS-Erweiterung für OData Services for Management                         | ManagementOdata                    | N                     |
| Media Foundation                                       | Server-Media-Foundation            | N                     |
| Message Queuing-                                        | MSMQ                               | N                     |
| Message Queuing-Dienste                               | MSMQ-Dienste                      | N                     |
| Message Queuing-Server                                 | MSMQ-Server                        | N                     |
| Verzeichnisdienstintegration                          | MSMQ-Directory                     | N                     |
| HTTP-Unterstützung                                           | MSMQ-HTTP-Unterstützung                  | N                     |
| Message Queuing-Trigger                               | MSMQ-Trigger                      | N                     |
| Routing-Dienst                                        | MSMQ-Routing                       | N                     |
| Message Queuing DCOM-Proxy                             | MSMQ-DCOM                          | N                     |
| Multipfad-E/A                                          | Multipfad-e/a                       | N                     |
| MultiPoint-Connector                                   | MultiPoint-Connector               | N                     |
| MultiPoint Connector-Dienste                          | MultiPoint-Connector-Dienste      | N                     |
| MultiPoint-Manager und MultiPoint-Dashboard            | MultiPoint-Tools                   | N                     |
| Netzwerklastenausgleich                                 | NLB                                | N                     |
| Peer Name Resolution-Protokoll                          | PNRP                               | N                     |
| Verbessertes Audio-/Videostreaming unter Windows                 | qWave                              | N                     |
| RDC (Remote Differential Compression)                        | RDC                                | N                     |
| Remoteserver-Verwaltungstools                     | RSAT                               | N                     |
| Feature-Verwaltungstools                           | RSAT-Feature-Tools                 | N                     |
| BitLocker Drive Encryption Administrationstools  | RSAT-Feature-Tools-BitLocker       | N                     |
| DataCenterBridging LLDP-Tools                          | RSAT-DataCenterBridging-LLDP-Tools | N                     |
| Tools für die Failover-Clusterunterstützung                              | RSAT-Clustering                    | N                     |
| Failovercluster-Modul für Windows PowerShell         | RSAT-Clustering-PowerShell         | N                     |
| Failovercluster Automatisierungsserver                     | RSAT-Clustering-AutomationServer   | N                     |
| Failovercluster-Befehl-Schnittstelle                     | RSAT-Clustering-CmdInterface       | N                     |
| IP-Adresse (IPAM) Management Client                    | IPAM-Client-Funktion                | N                     |
| Geschützt VM-Tools                                      | RSAT-geschützter-VM-Tools             | N                     |
| Speicher Replikat Modul für Windows PowerShell          | RSAT-Speicher-Replikat               | N                     |
| Rollenverwaltungstools                              | RSAT-Rolle-Tools                    | N                     |
| AD DS und AD LDS-Tools                                 | RSAT-AD-Verwaltungstools                      | N                     |
| Active Directory-Modul für Windows PowerShell         | RSAT-AD-PowerShell                 | N                     |
| AD DS-Tools                                            | REMOTESERVER-VERWALTUNGSTOOLS HINZUGEFÜGT                          | N                     |
| Active Directory-Verwaltungscenter                 | RSAT-AD-AdminCenter                | N                     |
| AD DS-Snap-Ins und Befehlszeilentools                  | RSAT-fügt-Tools                    | N                     |
| AD LDS-Snap-Ins und Befehlszeilen-Tools                 | RSAT-ADLDS                         | N                     |
| Hyper-V-Verwaltungstools                               | RSAT-Hyper-V-Tools                 | N                     |
| Hyper-V-Modul für Windows PowerShell                  | Hyper-V-PowerShell                 | N                     |
| Windows Serverupdate Services-Tools                   | UpdateServices-Remoteserver-Verwaltungstools                | N                     |
| API und PowerShell-cmdlets                             | UpdateServices-API                 | N                     |
| DHCP-Server-Tools                                      | DHCP-REMOTESERVER-VERWALTUNGSTOOLS                          | N                     |
| DNS-Server-Tools                                       | RSAT-DNS-Server                    | N                     |
| RAS-Verwaltungstools                         | RSAT-RAS                  | N                     |
| Remote Access-Modul für Windows PowerShell            | RSAT-RAS-PowerShell       | N                     |
| RPC über HTTP-Proxy                                    | RPC-über-HTTP-Proxy                | N                     |
| Setup and Boot Event Collection                        | Setup-und-Boot-Ereignis-Auflistung    | N                     |
| Einfache TCP/IP-Dienste                                 | Einfacher TCPIP                       | N                     |
| SMB 1.0-/CIFS-Dateifreigabeunterstützung                      | FS-SMB1                            | Y                     |
| SMB-Bandbreiteneinschränkung                                    | FS-SMBBW                           | N                     |
| SNMP-Dienst                                           | SNMP-Dienst                       | N                     |
| SNMP-WMI-Anbieter                                      | SNMP-WMI-Anbieter                  | N                     |
| Telnet-Client                                          | Telnet-Client                      | N                     |
| VM-Abschirmungstools für Fabric-Verwaltung               | FabricShieldedTools                | N                     |
| Windows Defender-Features                              | Windows-Defender-Features          | Y                     |
| WindowsDefender                                       | Windows-Defender                   | Y                     |
| Interne Windows-Datenbank                              | Windows Internal Database          | N                     |
| Windows PowerShell                                     | PowerShellRoot                     | Y                     |
| Windows PowerShell 5.1                                 | PowerShell                         | Y                     |
| Windows PowerShell 2.0-Modul                          | PowerShell-V2                      | (entfernt)             |
| Windows PowerShell gewünscht State-Konfigurationsdienst | DSC-Dienst                        | N                     |
| Windows PowerShell-Webzugriff                          | WindowsPowerShellWebAccess         | N                     |
| Windows-Prozessaktivierungsdienst                     | WURDE                                | N                     |
| Prozessmodell                                          | WURDE Prozessmodell                  | N                     |
| .NET 3.5-Umgebung                                   | WURDE-NET-Umgebung                | N                     |
| Konfigurations-APIs                                     | WURDE-Config-APIs                    | N                     |
| Windows Server-Sicherung                                  | Windows-Server-Sicherung              | N                     |
| WindowsServer-Migrationstools                         | Migration                          | N                     |
| Standardbasierte Windows-Speicherverwaltung             | WindowsStorageManagementService    | N                     |
| WinRM-IIS-Erweiterung                                    | WinRM-IIS-App.                      | N                     |
| WINS-Server                                            | WINS-                               | N                     |
| WoW64-Unterstützung                                          | WoW64-Unterstützung                      | Y                     |
|                                                        |                                    |                       |
