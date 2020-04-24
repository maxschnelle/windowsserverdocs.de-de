---
title: Windows Server 2016-Produkte und -Editionen
description: Erläutert Unterschiede in den Windows Server Standard- und Windows Server Datacenter-Editionen.
ms.prod: windows-server
ms.date: 10/04/2019
ms.technology: server-general
ms.topic: article
ms.assetid: c5ca3bfe-7ced-49f6-a932-80cab33f419e
author: jasongerend
ms.author: jgerend
manager: dongill
ms.localizationpriority: medium
ms.openlocfilehash: ce4c35f0b65d0461e9dc2e23404d2637aecff415
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2020
ms.locfileid: "80827103"
---
# <a name="comparison-of-standard-and-datacenter-editions-of-windows-server-2016"></a>Vergleich der Standard- und Datacenter-Editionen von Windows Server 2016

> Gilt für: Windows Server 2016
  
## <a name="locks-and-limits"></a>Sperren und Beschränkungen

| Sperren und Beschränkungen | Windows Server 2016 Standard | Windows Server 2016 Datacenter |
| ------------------- |---------- | --------------------------- |  
| Maximale Anzahl von Benutzern | Basierend auf Clientzugriffslizenzen   | Basierend auf Clientzugriffslizenzen     |
| Maximale Anzahl von SMB-Verbindungen | 16.777.216      | 16.777.216          |
| Maximale Anzahl von RRAS-Verbindungen| unbegrenzt       | unbegrenzt         |
| Maximale Anzahl von IAS-Verbindungen | 2\.147.483.647   | 2\.147.483.647        |
| Maximale Anzahl von RDS-Verbindungen | 65535           | 65535             |
| Maximale Anzahl von 64-Bit-Sockets | 64     | 64                |
| Maximale Anzahl von Kernen | unbegrenzt       | unbegrenzt      |
| Maximaler RAM             | 24 TB           | 24 TB             |
| Kann als Virtualisierungsgast verwendet werden | Ja. 2 virtuelle Computer plus ein Hyper-V-Host pro Lizenz | Ja. <strong>Unbegrenzte Anzahl von virtuellen Computern</strong> plus ein Hyper-V-Host pro Lizenz |
| Server kann einer Domäne beitreten. | ja            | ja                |
| Umkreisnetzwerkschutz/-firewall | nein     | nein                 |
| DirectAccess            | ja             | ja                |
| DLNA-Codecs und Webmedienstreaming | Ja, bei der Installation als Server mit Desktopdarstellung | Ja, bei der Installation als Server mit Desktopdarstellung |

## <a name="server-roles"></a>Serverrollen

| Verfügbare Windows Server-Rollen     | Rollendienste | Windows Server 2016 Standard | Windows Server 2016 Datacenter |  
| -------------------                | ----------    | ----------                   | ---------------------------    |  
| Active Directory-Zertifikatdienste|              | Ja                          | Ja                            |
| Active Directory-Domänendienste (AD DS)    |               | Ja                          | Ja                            |
| Active Directory-Verbunddienste|               | Ja                          | Ja                            |
| AD Lightweight Directory Services| |Ja|Ja|
| AD Rights Management Services| |Ja|Ja|
| Integritätsnachweis für Geräte| |Ja|Ja|
| DHCP-Server| |Ja|Ja|
| DNS-Server| |Ja|Ja|
| Faxserver| |Ja|Ja|
| Datei- und Speicherdienste|Dateiserver|Ja|Ja|
| Datei- und Speicherdienste|BranchCache für Netzwerkdateien|Ja|Ja|
| Datei- und Speicherdienste|Datendeduplizierung|Ja|Ja|
| Datei- und Speicherdienste|DFS-Namespaces|Ja|Ja|
| Datei- und Speicherdienste|DFS-Replikation|Ja|Ja|
| Datei- und Speicherdienste|File Server Resource Manager|Ja|Ja|
| Datei- und Speicherdienste|Dateiserver-VSS-Agent-Dienst|Ja|Ja|
| Datei- und Speicherdienste|iSCSI Target Server|Ja|Ja|
| Datei- und Speicherdienste|iSCSI-Zielspeicheranbieter|Ja|Ja|
| Datei- und Speicherdienste|Server für NFS|Ja|Ja|
| Datei- und Speicherdienste|Arbeitsordner|Ja|Ja|
| Datei- und Speicherdienste|Speicherdienste|Ja|Ja|
| Host-Überwachungsdienst| |Ja|Ja|
| Hyper-V| |Ja|Ja; <strong>einschließlich abgeschirmter virtueller Computer</strong>|
| MultiPoint Services| |Ja|Ja|
| Netzwerkcontroller| |Nein| <strong>Ja</strong> |
| Network Policy and Access Services| |Ja, bei der Installation als Server mit Desktopdarstellung|Ja, bei der Installation als Server mit Desktopdarstellung|
| Druck- und Dokumentdienste| |Ja|Ja|
| Remotezugriff| |Ja|Ja|
| Remotedesktopdienste| |Ja|Ja|
| Volumenaktivierungsdienste| |Ja|Ja|
| Webdienste (IIS)| |Ja|Ja|
| Windows Deployment Services| |Ja, bei der Installation als Server mit Desktopdarstellung|Ja, bei der Installation als Server mit Desktopdarstellung|
| Windows Server Essentials Experience| |Ja|Ja|
| Windows Server Update Services| |Ja|Ja|

## <a name="features"></a>Features

|Windows Server-Features mit Server-Manager (oder PowerShell) installierbar|Windows Server 2016 Standard|Windows Server 2016 Datacenter|  
|-------------------|----------|---------------------------|  
|.NET Framework 3.5|Ja|Ja|
|.NET Framework 4.6|Ja|Ja|
|Intelligenter Hintergrundübertragungsdienst (Background Intelligent Transfer Service, BITS)|Ja|Ja|
|BitLocker-Laufwerkverschlüsselung|Ja|Ja|
|BitLocker-Netzwerkentsperrung|Ja, bei der Installation als Server mit Desktopdarstellung|Ja, bei der Installation als Server mit Desktopdarstellung|
|BranchCache|Ja|Ja|
|Client für NFS|Ja|Ja|
|Container|Ja (Windows-Container unbegrenzt; Hyper-V-Container bis zu 2)|Ja (alle Containertypen unbegrenzt)|
|Data Center Bridging|Ja|Ja|
|DirectPlay|Ja, bei der Installation als Server mit Desktopdarstellung|Ja, bei der Installation als Server mit Desktopdarstellung|
|Erweitertes Speichern|Ja|Ja|
|Failoverclusterunterstützung|Ja|Ja|
|Gruppenrichtlinienverwaltung|Ja|Ja|
|Host-Überwachungsunterstützung für Hyper-V|Nein|<strong>Ja</strong> |
|E/A: Quality of Service (QoS, Dienstqualität)|Ja|Ja|
|Hostfähiger IIS-Webkern|Ja|Ja|
|Internetdruckclient|Ja, bei der Installation als Server mit Desktopdarstellung|Ja, bei der Installation als Server mit Desktopdarstellung|
|IPAM-Server|Ja|Ja|
|iSNS-Serverdienst|Ja|Ja|
|LPR-Portüberwachung|Ja, bei der Installation als Server mit Desktopdarstellung|Ja, bei der Installation als Server mit Desktopdarstellung|
|IIS-Erweiterung für OData Services for Management|Ja|Ja|
|Media Foundation|Ja|Ja|
|Message Queuing|Ja|Ja|
|Multipfad-E/A|Ja|Ja|
|MultiPoint-Connector|Ja|Ja|
|Netzwerklastenausgleich|Ja|Ja|
|Peer Name Resolution-Protokoll|Ja|Ja|
|Verbessertes Windows-Audio-/Video-Streaming|Ja|Ja|
|RAS-Verbindungs-Manager-Verwaltungskit|Ja, bei der Installation als Server mit Desktopdarstellung|Ja, bei der Installation als Server mit Desktopdarstellung|
|Remoteunterstützung|Ja, bei der Installation als Server mit Desktopdarstellung|Ja, bei der Installation als Server mit Desktopdarstellung|
|Remotedifferenzialkomprimierung|Ja|Ja|
|RSAT|Ja|Ja|
|RPC über HTTP-Proxy|Ja|Ja|
|Ereignissammlung für Setup und Start|Ja|Ja|
|Einfache TCP/IP-Dienste|Ja, bei der Installation als Server mit Desktopdarstellung|Ja, bei der Installation als Server mit Desktopdarstellung|
|SMB 1.0-/CIFS-Dateifreigabeunterstützung|Installiert|Installiert|
|SMB-Bandbreiteneinschränkung|Ja|Ja|
|SMTP-Server|Ja|Ja|
|SNMP-Dienst|Ja|Ja|
|Softwarelastenausgleich|Nein| <strong>Ja</strong> |
|Speicherreplikat|Nein|Ja|
|Telnet-Client|Ja|Ja|
|TFTP-Client|Ja, bei der Installation als Server mit Desktopdarstellung|Ja, bei der Installation als Server mit Desktopdarstellung|
|VM-Abschirmungstools für Fabric-Verwaltung|Ja|Ja|
|WebDAV-Redirector|Ja|Ja|
|Windows-Biometrieframework|Ja, bei der Installation als Server mit Desktopdarstellung|Ja, bei der Installation als Server mit Desktopdarstellung|
|Windows Defender-Features|Installiert|Installiert|
|Windows Identity Foundation 3.5|Ja, bei der Installation als Server mit Desktopdarstellung|Ja, bei der Installation als Server mit Desktopdarstellung|
|Interne Windows-Datenbank|Ja|Ja|
|Windows PowerShell|Installiert|Installiert|
|Windows-Prozessaktivierungsdienst|Ja|Ja|
|Windows Search-Dienst|Ja, bei der Installation als Server mit Desktopdarstellung|Ja, bei der Installation als Server mit Desktopdarstellung|
|Windows Server-Sicherung|Ja|Ja|
|Windows Server-Migrationstools|Ja|Ja|
|Standardbasierte Windows-Speicherverwaltung|Ja|Ja|
|Windows-TIFF-IFilter|Ja, bei der Installation als Server mit Desktopdarstellung|Ja, bei der Installation als Server mit Desktopdarstellung|
|WinRM-IIS-Erweiterung|Ja|Ja|
|WINS-Server|Ja|Ja|
|WLAN-Dienst|Ja|Ja|
|WoW64-Unterstützung|Installiert|Installiert|
|XPS-Viewer|Ja, bei der Installation als Server mit Desktopdarstellung|Ja, bei der Installation als Server mit Desktopdarstellung|

|Allgemein verfügbare Funktionen|Windows Server 2016 Standard|Windows Server 2016 Datacenter|  
|-------------------|----------|---------------------------|  
|Best Practices Analyzer|Ja|Ja|
|Direct Access|Ja|Ja|
|Dynamischer Arbeitsspeicher (in Virtualisierung)|Ja|Ja|
|RAM im laufenden Systembetrieb hinzufügen/entfernen|Ja|Ja|
|Microsoft Management Console|Ja|Ja|
|Minimale Serverbenutzeroberfläche|Ja|Ja|
|Netzwerklastenausgleich|Ja|Ja|
|Windows PowerShell|Ja|Ja|
|Server Core-Installationsoption|Ja|Ja|
|Nano Server-Installationsoption|Ja|Ja|
|Server-Manager|Ja|Ja|
|SMB Direct und SMB über RDMA|Ja|Ja|
| Softwaredefinierte Netzwerke | Nein | <strong>Ja</strong> |
|Speicherreplikat | Nein | <strong>Ja</strong> |
|Speicherplätze|Ja|Ja|
|Speicherplätze DAS|Nein| <strong>Ja</strong> |
|Volumenaktivierungsdienste|Ja|Ja|
|Integration mit Volumeschattenkopie-Dienst (Volume Shadow Copy Service, VSS)|Ja|Ja|
|Windows Server Update Services|Ja|Ja|
|Windows-Systemressourcen-Manager|Ja|Ja|
|Serverlizenzprotokollierung|Ja|Ja|
|Geerbte Aktivierung|Als Gast (beim Hosten unter Datacenter)| <strong>Kann Host oder Gast sein</strong> |
|Arbeitsordner|Ja|Ja|

