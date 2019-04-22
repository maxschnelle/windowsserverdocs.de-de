---
title: Rollen, Rollendienste und Features nicht in WindowsServer – Server Core
description: Informationen Sie zu Rollen und Features, die nicht in der Server Core-Installationsoption für Windows Server enthalten.
ms.prod: windows-server-threshold
ms.mktglfcycl: manage
ms.sitesec: library
author: lizap
ms.localizationpriority: medium
ms.date: 02/23/2018
ms.openlocfilehash: 308bc8a5d25e2ec67438f0ee03cbfce6f7411ca2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59825531"
---
# <a name="roles-role-services-and-features-not-in-windows-server---server-core"></a>Rollen, Rollendienste und Features nicht in WindowsServer – Server Core

> Gilt für: WindowsServer (Halbjährlicher Kanal) und WindowsServer 2016

Die folgenden Rollen, Rollendienste und Features wurden in die Server Core-Installationsoption von Windows Server entfernt. Verwenden Sie diese Informationen, um zu ermitteln, ob die Server Core-Option für Ihre Umgebung funktioniert.

> [!NOTE]
> Sie sehen auch eine Liste der Rollen, Rollendiensten und features dieses Produkts [befinden sich im Server Core](server-core-roles-and-services.md). Es ist eine sehr große Liste, also um optimale Ergebnisse zu suchen, Liste der bestimmter Rollen oder Features, die Sie interessiert.

## <a name="roles-not-in-server-core"></a>Rollen nicht im Server Core

- Fax
- MultiPointServerRole
- NPAS
- WDS

## <a name="role-services-not-in-server-core"></a>Rollendienste, die nicht in Server Core
Beachten Sie, die für einige Rollendienste Remote Desktop befinden sich im Server-Core (Connection Broker, Lizenzierung,-Virtualisierungshost), aber andere dagegen nicht (Gateway, RD-Sitzungshost, Web Access).

- Drucken-Scan-Server
- Drucken über das Internet
- RDS-Gateway
- RDS-RD-Server
- RDS-Web-Access
- Web-Mgmt-Console
- Web-Lgcy-Mgmt-Console
- WDS-Bereitstellung
- WDS-Transport *(vor Windows Server, Version 1803)*

## <a name="features-not-in-server-core"></a>Funktionen, die nicht in Server Core

- BITS-IIS-Ext
- BitLocker-NetworkUnlock
- Direct-Play
- Internet-Print-Client
- LPR-Port-Monitor
- MSMQ-Multicasting
- CMAK
- Remote Assistance
- RSAT-SMTP
- RSAT-Feature-Tools-BitLocker-RemoteAdminTool
- RSAT-Bits-Server
- RSAT-NLB
- RSAT-SNMP
- RSAT-WINS
- Hyper-V-Tools
- RSAT-RDS-Tools
- RSAT-RDS-Gateway
- RSAT-RDS-Licensing-Diagnosis-UI
- RDS-Licensing-UI
- UpdateServices-UI
- RSAT-ADCS
- RSAT-ADCS-Mgmt
- RSAT-Online-Responder
- RSAT-ADRMS
- RSAT-Fax
- RSAT-File-Services
- RSAT-DFS-Mgmt-Con
- RSAT-FSRM-Mgmt
- RSAT-NFS-Admin
- RSAT-NPAS
- RSAT-Print-Services
- RSAT-VA-Tools
- WDS-AdminPack
- SMTP-Server
- TFTP-Client
- WebDAV-Redirector
- Biometrieframework
- Windows-Defender-Gui
- Windows-Identity-Foundation
- PowerShell-ISE
- Search-Dienst
- Windows-TIFF-IFilter
- Wireless-Networking
- XPS-Viewer

