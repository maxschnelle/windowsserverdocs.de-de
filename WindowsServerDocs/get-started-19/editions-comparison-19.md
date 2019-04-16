---
title: Vergleich der Standard- und Datacenter-Editionen von Windows Server 2019
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: server-general
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c5ca3bfe-7ced-49f6-2932-80cab33fe914
author: coreyp-at-msft
ms.author: coreyp
manager: jasgroce
ms.localizationpriority: medium
ms.openlocfilehash: e94c88ab7fb4aede7554dd621843b613fa16b6dc
ms.sourcegitcommit: 0b51cf8d0a1db31d6d2e2e45a145011311fbdf34
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/14/2019
ms.locfileid: "9169934"
---
# Vergleich der Standard- und Datacenter-Editionen von Windows Server 2019

> Gilt für: Windows Server2019
  
## Sperren und Beschränkungen
|Sperren und Beschränkungen|Windows Server 2019 Standard|Windows Server 2019 Datacenter|  
|-------------------|----------|---------------------------|  
|Maximale Anzahl von Benutzern|Basierend auf Clientzugriffslizenzen|Basierend auf Clientzugriffslizenzen|
|Maximale Anzahl von SMB-Verbindungen|16777216|16777216|
|Maximale Anzahl von RRAS-Verbindungen|unbegrenzt|unbegrenzt|
|Maximale Anzahl von IAS-Verbindungen|2147483647|2147483647|
|Maximale Anzahl von RDS-Verbindungen|65535|65535|
|Maximale Anzahl von 64-Bit-Sockets|64|64|
|Maximale Anzahl von Kernen|unbegrenzt|unbegrenzt|
|Maximaler RAM|24 TB|24 TB|
|Kann als Virtualisierungsgast verwendet werden|Ja. 2 virtuelle Computer plus ein Hyper-V-Host pro Lizenz|Ja. Unbegrenzte Anzahl von virtuellen Computern plus ein Hyper-V-Host pro Lizenz|
|Server kann einer Domäne beitreten.|ja|ja|
|Umkreisnetzwerkschutz/-firewall|nein|Nein|
|DirectAccess|ja|ja|
|DLNA-Codecs und Webmedienstreaming|Ja, bei der Installation als Server mit Desktopdarstellung|Ja, bei der Installation als Server mit Desktopdarstellung|

## Serverrollen
|Verfügbare Windows Server-Rollen|Rollendienste|Windows Server 2019 Standard|Windows Server 2019 Datacenter|  
|-------------------|----------|----------|---------------------------|  
|Active Directory-Zertifikatdienste| |Ja.|Ja.|
|Active Directory Domain Services| |Ja|Ja|
|Active Directory-Verbunddienste (AD FS)| |Ja.|Ja.|
|AD Lightweight Directory Services| |Ja.|Ja.|
|AD Rights Management Services| |Ja.|Ja.|
|Integritätsnachweis für Geräte| |Ja.|Ja.|
|DHCP-Server| |Ja.|Ja.|
|DNS-Server| |Ja.|Ja.|
|Faxserver| |Ja.|Ja|
|Datei- und Speicherdienste|Dateiserver|Ja.|Ja|
|Datei- und Speicherdienste|BranchCache für Netzwerkdateien|Ja.|Ja|
|Datei- und Speicherdienste|Datendeduplizierung|Ja.|Ja|
|Datei- und Speicherdienste|DFS-Namespaces|Ja.|Ja|
|Datei- und Speicherdienste|DFS-Replikation|Ja|Ja|
|Datei- und Speicherdienste|Ressourcen-Manager für Dateiserver|Ja|Ja|
|Datei- und Speicherdienste|Dateiserver-VSS-Agent-Dienst|Ja|Ja|
|Datei- und Speicherdienste|iSCSI-Zielserver|Ja|Ja|
|Datei- und Speicherdienste|iSCSI-Zielspeicheranbieter|Ja|Ja|
|Datei- und Speicherdienste|Server für NFS|Ja|Ja|
|Datei- und Speicherdienste|Arbeitsordner|Ja|Ja|
|Datei- und Speicherdienste|Speicherdienste|Ja|Ja|
|Host-Überwachungsdienst| |Ja|Ja|
|Hyper-V| |Ja|Ja; einschließlich abgeschirmte virtuelle Computer|
|Netzwerkcontroller| |Nein|Ja.|
|Network Policy and Access Services| |Ja, bei der Installation als Server mit Desktopdarstellung|Ja, bei der Installation als Server mit Desktopdarstellung|
|Druck- und Dokumentdienste| |Ja|Ja|
|Remotezugriff| |Ja|Ja|
|Remotedesktopdienste| |Ja|Ja.|
|Volumenaktivierungsdienste| |Ja|Ja|
|Webdienste (IIS)| |Ja|Ja|
|Windows-Bereitstellungsdienste| |Ja*|Ja*|
|Windows Server Essentials Experience| |Ja|Ja|
|Windows Server Update Services| |Ja|Ja|

* WDS-Transport-Server ist neu in Server Core-Installationen in Windows Server 2019 (auch in Windows Server, Version 1803 ab Semi-annual Channel)


## Features

|Windows Server-Features mit Server-Manager (oder PowerShell) installierbar|Windows Server 2019 Standard|Windows Server 2019 Datacenter|  
|-------------------|----------|---------------------------|  
|.NET Framework 3.5|Ja|Ja|
|.NET Framework 4.6|Ja|Ja|
|BITS (Background Intelligent Transfer Service, Intelligenter Hintergrundübertragungsdienst)|Ja|Ja|
|BitLocker-Laufwerkverschlüsselung|Ja|Ja|
|BitLocker-Netzwerkentsperrung|Ja, bei der Installation als Server mit Desktopdarstellung|Ja, bei der Installation als Server mit Desktopdarstellung|
|BranchCache|Ja|Ja|
|Client für NFS|Ja|Ja|
|Container|Ja (Windows-Container unbegrenzt; Hyper-V-Container bis zu 2)|Ja (alle Containertypen unbegrenzt)|
|Data Center Bridging|Ja|Ja.|
|DirectPlay|Ja, bei der Installation als Server mit Desktopdarstellung|Ja, bei der Installation als Server mit Desktopdarstellung|
|Erweitertes Speichern|Ja|Ja|
|Failoverclustering|Ja|Ja|
|Gruppenrichtlinienverwaltung|Ja|Ja|
|Host-Überwachungsunterstützung für Hyper-V|Nein|Ja|
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
|Verbessertes Audio-/Videostreaming unter Windows|Ja|Ja|
|RAS-Verbindungs-Manager-Verwaltungskit|Ja, bei der Installation als Server mit Desktopdarstellung|Ja, bei der Installation als Server mit Desktopdarstellung|
|Remoteunterstützung|Ja, bei der Installation als Server mit Desktopdarstellung|Ja, bei der Installation als Server mit Desktopdarstellung|
|RDC (Remote Differential Compression)|Ja|Ja|
|RSAT|Ja|Ja|
|RPC über HTTP-Proxy|Ja|Ja|
|Ereignissammlung für Setup und Start|Ja|Ja|
|Einfache TCP/IP-Dienste|Ja, bei der Installation als Server mit Desktopdarstellung|Ja, bei der Installation als Server mit Desktopdarstellung|
|SMB 1.0-/CIFS-Dateifreigabeunterstützung|Installiert|Installiert|
|SMB-Bandbreiteneinschränkung|Ja|Ja|
|SMTP-Server|Ja|Ja|
|SNMP-Dienst|Ja|Ja|
|Softwarelastenausgleich|Ja|Ja|
|Speicherreplikat|Nein|Ja|
|Telnet-Client|Ja|Ja|
|TFTP-Client|Ja, bei der Installation als Server mit Desktopdarstellung|Ja, bei der Installation als Server mit Desktopdarstellung|
|VM-Abschirmungstools für Fabric-Verwaltung|Ja|Ja|
|WebDAV-Redirector|Ja|Ja|
|Windows-Biometrieframework|Ja, bei der Installation als Server mit Desktopdarstellung|Ja, bei der Installation als Server mit Desktopdarstellung|
|Windows Defender-Features|Installiert|Installiert|
|Windows Identity Foundation 3.5|Ja, bei der Installation als Server mit Desktopdarstellung|Ja, bei der Installation als Server mit Desktopdarstellung|
|Interne Windows-Datenbank|Ja|Ja|
|Windows PowerShell|Installiert|Installiert|
|Windows-Prozessaktivierungsdienst|Ja|Ja|
|Windows Search-Dienst|Ja, bei der Installation als Server mit Desktopdarstellung|Ja, bei der Installation als Server mit Desktopdarstellung|
|Windows Server-Sicherung|Ja|Ja|
|WindowsServer-Migrationstools|Ja|Ja|
|Standardbasierte Windows-Speicherverwaltung|Ja|Ja|
|Windows-TIFF-IFilter|Ja, bei der Installation als Server mit Desktopdarstellung|Ja, bei der Installation als Server mit Desktopdarstellung|
|WinRM-IIS-Erweiterung|Ja|Ja|
|WINS-Server|Ja|Ja|
|WLAN-Dienst|Ja|Ja|
|WoW64-Unterstützung|Installiert|Installiert|
|XPS-Viewer|Ja, bei der Installation als Server mit Desktopdarstellung|Ja, bei der Installation als Server mit Desktopdarstellung|

|Allgemein verfügbare Funktionen|Windows Server 2019 Standard|Windows Server 2019 Datacenter|  
|-------------------|----------|---------------------------|  
|Best Practices Analyzer|Ja|Ja|
|Eingeschränkte Speicherreplikaten|Ja, (1 Partnerschaft und 1 Ressourcengruppe mit einzelnen 2-TB-Volume)|"Ja", "Unbegrenzt"|
|Direct Access|Ja|Ja|
|Dynamischer Arbeitsspeicher (in Virtualisierung)|Ja|Ja|
|RAM im laufenden Systembetrieb hinzufügen/entfernen|Ja|Ja|
|Microsoft Management Console|Ja|Ja|
|Minimale Serverbenutzeroberfläche|Ja|Ja|
|Netzwerklastenausgleich|Ja|Ja|
|Windows PowerShell|Ja|Ja|
|Server Core-Installationsoption|Ja|Ja|
|Nano Server-Installationsoption|Ja|Ja|
|Server-Manager|Ja|Ja|
|SMB Direct und SMB über RDMA|Ja|Ja|
|Softwaredefinierte Netzwerke|Nein.|Ja|
|Speicherverwaltungsdienst|Ja|Ja.|
|Speicherplätze|Ja|Ja|
|Direkte Speicherplätze|Nein.|Ja.|
|Volumenaktivierungsdienste|Ja|Ja.|
|Integration mit Volumeschattenkopie-Dienst (Volume Shadow Copy Service, VSS)|Ja|Ja|
|Windows Server Update Services|Ja|Ja|
|Windows-Systemressourcen-Manager|Ja|Ja|
|Serverlizenzprotokollierung|Ja|Ja|
|Geerbte Aktivierung|Als Gast (beim Hosten unter Datacenter)|Kann Host oder Gast sein|
|Arbeitsordner|Ja|Ja|

