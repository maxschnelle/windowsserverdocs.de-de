---
title: Rollen, Rollendienste und Features nicht in Server Core 1803 Container - Windows-Server-version
description: Informationen Sie zu Rollen und Features, den, die wir aus diesem Abbild der Server Core-Container für Windows Server entfernt.
ms.prod: windows-server-threshold
ms.mktglfcycl: manage
ms.sitesec: library
author: lizap
ms.localizationpriority: medium
ms.date: 05/07/2018
ms.openlocfilehash: 0ad574a04ba7ecd235f1825bd25c247a1565edf6
ms.sourcegitcommit: 1533d994a6ddea54ac189ceb316b7d3c074307db
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/01/2018
ms.locfileid: "1859904"
---
# <a name="roles-role-services-and-features-not-in-server-core-containers---windows-server-version-1803"></a>Rollen, Rollendienste und Features nicht in Server Core 1803 Container - Windows-Server-version

> Betrifft: WindowsServer, Version 1803

In Windows Server, Version 1803, haben wir [die Gesamtgröße der die Server Core-Container-Bild zur Darstellung der **1,58 GB**reduziert](https://blogs.technet.microsoft.com/virtualization/2018/01/22/a-smaller-windows-server-core-container-with-better-application-compatibility/). Die Möglichkeit, die wir das getan haben ist durch Optimieren der Architektur und Entfernen von Dinge, die Sie benötigen nicht in einer [Server Core-Container](https://docs.microsoft.com/virtualization/windowscontainers/about/). Einige Dinge, die nicht funktionieren in Containern waren, einige Rollen und-Features niemand verwendeten waren. 

> [!IMPORTANT]
> Wir entfernt diese aus dem Server Core **Container** Bild, nicht die [Server Core selbst](server-core-roles-and-services.md). 

Nachfolgend finden Sie die vollständige Liste der Features und Rollen, die aus dem Server Core-Container-Abbild entfernt:

<div style='font-size:9.0pt'>

<br>ADCertificateServicesRole
<br>AuthManager
<br>BitLocker-Hilfsprogramme
<br>BitLocker
<br>BITS
<br>BITSExtensions hochladen
<br>CCFFilter
<br>CertificateEnrollmentPolicyServer
<br>CertificateEnrollmentServer
<br>CertificateServices
<br>ClientForNFS-Infrastruktur
<br>Container
<br>CoreFileServer
<br>DataCenterBridging-LLDP-Tools
<br>DataCenterBridging
<br>Dedup-Core
<br>DeviceHealthAttestationService
<br>DFSN-Server
<br>DFSR-Infrastructure-ServerEdition
<br>Verzeichnisdienste ADAM
<br>Verzeichnisdienste DomainController
<br>DiskIo QoS
<br>EnhancedStorage
<br>FailoverCluster-Verwaltungsprogramme
<br>FailoverCluster-AutomationServer
<br>FailoverCluster-CmdInterface
<br>FailoverCluster-FullServer
<br>FailoverCluster-PowerShell
<br>Dateidienste
<br>FileServerVSSAgent
<br>FRS-Infrastruktur
<br>FSRM-Infrastruktur-Services
<br>FSRM-Infrastruktur
<br>HardenedFabricEncryptionTask
<br>HostGuardian
<br>HostGuardianService-Paket
<br>IdentityServer SecurityTokenService
<br>IPAMClientFeature
<br>IPAMServerFeature
<br>iSCSITargetServer-PowerShell
<br>iSCSITargetServer
<br>iSCSITargetStorageProviders
<br>iSNS_Service
<br>Lizenzierung
<br>LightweightServer
<br>Microsoft-Hyper-V-Management-Clients
<br>Microsoft Hyper-V-Offline-
<br>Microsoft-Hyper-V-Online
<br>Microsoft-Hyper-V
<br>Microsoft Windows-FCI-Client-Paket
<br>Microsoft-Windows-Softwarezuweisungsarchitektur-ServerAdminTools-Update
<br>Microsoft-Windows-Subsystem-Linux
<br>MSRDC-Infrastruktur
<br>MultipathIo
<br>NetworkController
<br>NetworkControllerTools
<br>NetworkDeviceEnrollmentServices
<br>NetworkLoadBalancingFullServer
<br>NetworkVirtualization
<br>OnlineRevocationServices
<br>P2P-PnrpOnly
<br>PeerDist
<br>Drucken-Client-Gui
<br>Drucken LPDPrintService
<br>Drucken-Foundation Serverfeatures
<br>Druck-Server-Role
<br>QWAVE
<br>RasRoutingProtocols
<br>Remote-Desktop-Dienste
<br>RAS
<br>RemoteAccessMgmtTools
<br>RemoteAccessPowerShell
<br>RemoteAccessServer
<br>ResumeKeyFilter
<br>RightsManagementServices-Rolle
<br>RightsManagementServices
<br>RMS-Verbund
<br>SBMgr-UI
<br>ServerCore-Treiber-allgemeine-WOW64
<br>ServerCore-Treiber-Allgemein
<br>ServerForNFS-Infrastruktur
<br>ServerManager-Kern-RSAT-Feature-Tools
<br>ServerMediaFoundation
<br>ServerMigration
<br>SessionDirectory
<br>SetupAndBootEventCollection
<br>ShieldedVMToolsAdminPack
<br>SMB1Protocol-Server
<br>SmbDirect
<br>SMBHashGeneration
<br>SmbWitness
<br>SNMP
<br>SoftwareLoadBalancer
<br>Speicher-Replikat-AdminPack
<br>Speicher-Replikat
<br>TPM-PSH--Cmdlets
<br>UpdateServices-Datenbank
<br>UpdateServices-Dienste
<br>UpdateServices WidDatabase
<br>UpdateServices
<br>VmHostAgent
<br>VolumeActivation-Full-Rolle
<br>Web-Anwendung-Proxy
<br>WebAccess
<br>WebEnrollmentServices
<br>Windows-Defender
<br>Windowsserversicherung
<br>WindowsStorageManagementService
<br>WINSRuntime
<br>WMISnmpProvider
<br>WorkFolders-Server
<br>WSS-Produkt-Paket

</div>