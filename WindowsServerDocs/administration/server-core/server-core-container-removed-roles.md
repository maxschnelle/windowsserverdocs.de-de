---
title: Rollen, Rollen Dienste und Features nicht in Server Core-Containern-Windows Server, Version 1803
description: Erfahren Sie mehr über die Rollen und Features, die wir aus dem Server Core-Container Image für Windows Server entfernt haben.
ms.mktglfcycl: manage
ms.sitesec: library
author: lizap
ms.localizationpriority: medium
ms.date: 05/07/2018
ms.openlocfilehash: 2092e330af479ae0cbdb1da88ba87cf233307b59
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87993254"
---
# <a name="roles-role-services-and-features-not-in-server-core-containers---windows-server-version-1803"></a>Rollen, Rollen Dienste und Features nicht in Server Core-Containern-Windows Server, Version 1803

> Gilt für: Windows Server, Version 1803

In Windows Server, Version 1803, haben wir [die Gesamtgröße des Server Core-Container Images auf **1,58 GB**reduziert](https://blogs.technet.microsoft.com/virtualization/2018/01/22/a-smaller-windows-server-core-container-with-better-application-compatibility/). Wir haben dies erreicht, indem wir die Architektur optimieren und nicht benötigte Elemente in einem [Server Core-Container](/virtualization/windowscontainers/about/)entfernen. Einige waren Dinge, die in Containern nicht funktionierte, einige waren Rollen und Features, die nicht von einer verwendet wurden.

> [!IMPORTANT]
> Wir haben diese aus dem Server Core- **Container** Image, nicht von [Server Core selbst](server-core-roles-and-services.md)entfernt.

Im folgenden finden Sie eine komplette Liste der Features und Rollen, die aus dem Server Core-Container Image entfernt wurden:

<div style='font-size:9.0pt'>

<br>Adcertifiereservicesrole
<br>AuthManager
<br>BitLocker-Hilfsprogramme
<br>BitLocker
<br>BITS
<br>Bitsextensions-Upload
<br>Ccffilter
<br>Certificateregistrimentpolicyserver
<br>Certificateregistrimentserver
<br>Certifiupdateservices
<br>Clientfornfs-Infrastruktur
<br>Container
<br>Corefileserver
<br>Datacenterbridging-LLDP-Tools
<br>DataCenterBridging
<br>Deduplizierung (Core)
<br>Devicehealthattestationservice
<br>DFSN-Server
<br>DFSR-Infrastructure-Server Edition
<br>Directoriyservices-Adam
<br>Directoriyservices-DomainController
<br>Diskio-QoS
<br>EnhancedStorage
<br>Failovercluster-Adminpak
<br>Failovercluster-AutomationServer
<br>Failovercluster-cmdinterface
<br>Failovercluster-fullserver
<br>Failovercluster-PowerShell
<br>Dateidienste
<br>Fileservervssagent
<br>FRS-Infrastruktur
<br>"F"-Infrastruktur: Dienste
<br>"F"-Infrastruktur
<br>"Hardenedfabricencryptiontask"
<br>Hostwächter
<br>Hostguardianservice-Paket
<br>Identityserver-SecurityToken Service
<br>Ipamclientfeature
<br>Ipamserverfeature
<br>iscsitargetserver-PowerShell
<br>iSCSITargetServer
<br>iscsitargetstorageproviders
<br>iSNS_Service
<br>Lizenzierung
<br>LightweightServer
<br>Microsoft-Hyper-V-Management-Clients
<br>Microsoft-Hyper-V-offline
<br>Microsoft-Hyper-V-Online
<br>Microsoft-Hyper-V
<br>Microsoft-Windows-FCI-Client-Package
<br>Microsoft-Windows-GroupPolicy-serveradmintools-Update
<br>Microsoft-Windows-Subsystem-Linux
<br>MSRDC-Infrastructure
<br>Multipaar
<br>Network Controller
<br>Network controllertools
<br>Networkdeviceregistrimentservices
<br>NetworkLoadBalancingFullServer
<br>Netzwerkvirtualisierung
<br>Onlinerevocationservices
<br>P2P-pnrponly
<br>Peer-Manager
<br>Druck-Client-GUI
<br>Drucken-lpdprintservice
<br>Druck-Server-Foundation-Features
<br>Druck-Server-Rolle
<br>QWAVE
<br>"Rasroutingprotokolle"
<br>Remote Desktop Services
<br>RemoteAccess
<br>Remoteaccessmgmttools
<br>Remoteaccesspowershell
<br>Remote Access Server
<br>Resumekeyfilter
<br>Rightionmanagementservices-Rolle
<br>Righterminmanagementservices
<br>RMS-Verbund
<br>Sbmgr-UI
<br>Server Core-Drivers-General-WOW64
<br>Server Core-Treiber-allgemein
<br>Serverfornfs: Infrastruktur
<br>Server Manager-Core-RSAT-Feature-Tools
<br>Servermediafoundations
<br>Servermigration
<br>SessionDirectory
<br>Setupandbooteventcollection
<br>Shiel-Debug-toolsadminpack
<br>SMB1Protocol-Server
<br>Smbdirect
<br>Smbhashgene Ration
<br>Smbwitness
<br>SNMP
<br>Softwareloadbalancer
<br>Storage-Replica-Adminpack
<br>Speicher-Replikat
<br>TPM-PSH-Cmdlets
<br>Updateservices-Datenbank
<br>Updateservices-Dienste
<br>Updateservices-widdatabase
<br>Update Services
<br>Vmhostagent
<br>Volumeactivation-Full-Role
<br>Webanwendungsproxy
<br>WebAccess
<br>Webenrollmentservices
<br>Windows-Defender
<br>Des Dienstprogramms
<br>Windowsstoragemanagementservice
<br>Winsruntime
<br>Wmisnmpprovider
<br>Arbeitsordner-Server
<br>WSS-Product-Package

</div>