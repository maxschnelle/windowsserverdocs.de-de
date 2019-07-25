---
title: Rollen, Rollen Dienste und Features, die nicht in Windows Server Server Core enthalten sind
description: Erfahren Sie mehr über die Rollen und Features, die nicht in der Server Core-Installationsoption für Windows Server enthalten sind.
ms.prod: windows-server-threshold
ms.mktglfcycl: manage
ms.sitesec: library
author: lizap
ms.localizationpriority: medium
ms.date: 02/23/2018
ms.openlocfilehash: ce5107e8e0ab573df7588428db65c8b223cf1f13
ms.sourcegitcommit: 216d97ad843d59f12bf0b563b4192b75f66c7742
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/24/2019
ms.locfileid: "68476518"
---
# <a name="roles-role-services-and-features-not-in-windows-server---server-core"></a>Rollen, Rollen Dienste und Features, die nicht in Windows Server Server Core enthalten sind

> Gilt für: Windows Server 2019, Windows Server 2016 und Windows Server (halbjährlicher Kanal)

Die folgenden Rollen, Rollen Dienste und Features wurden aus der Server Core-Installationsoption von Windows Server entfernt. Anhand dieser Informationen können Sie herausfinden, ob die Server Core-Option für Ihre Umgebung funktioniert.

> [!NOTE]
> Sie können auch eine Liste der Rollen, Rollen Dienste und Features sehen, die [in Server Core enthalten sind](server-core-roles-and-services.md). Es handelt sich um eine sehr große Liste, sodass Sie für optimale Ergebnisse diese Liste nach der jeweiligen Rolle oder dem Feature durchsuchen können, die für Sie von Interesse sind.

## <a name="roles-not-in-server-core"></a>Rollen nicht in Server Core

- Fax
- Multipointserverrole
- NPAS
- WDS

## <a name="role-services-not-in-server-core"></a>Rollen Dienste nicht in Server Core
Beachten Sie, dass einige Remotedesktop-Rollen Dienste in Server Core (Verbindungs Broker, Lizenzierung, Virtualisierungshost) enthalten sind, andere jedoch nicht (Gateway, RD-Sitzungshost, Webzugriff).

- Print-Scan-Server
- Drucken/Internet
- RDS-Gateway
- RDS-RD-Server
- RDS-Web-Access
- Web-Mgmt-Konsole
- Web-lgcy-Mgmt-Console
- WDS-Bereitstellung
- WDS-Transport *(vor Windows Server-Version 1803)*

## <a name="features-not-in-server-core"></a>Features nicht in Server Core

- BITS-IIS-ext
- BitLocker-networkunlock
- Direkt Wiedergabe
- Internet-Print-Client
- LPR-Port-Monitor
- MSMQ-Multicasting
- CMAK
- Remote Unterstützung
- RSAT-SMTP
- RSAT-Feature-Tools-BitLocker-RemoteAdminTool
- RSAT-BITS-Server
- RSAT-NLB
- RSAT-SNMP
- RSAT-WINS
- Hyper-V-Tools
- RSAT-RDS-Tools
- RSAT-RDS-Gateway
- RSAT-RDS-Licensing-Diagnose-UI
- RDS-Lizenzierung-Benutzeroberfläche
- Updateservices-UI
- RSAT-ADCS
- RSAT-ADCs-Mgmt
- RSAT-Online-Responder
- RSAT-ADRMS
- RSAT-Fax
- RSAT-Dateidienste
- RSAT-DFS-Mgmt-con
- RSAT-"RSRM-Mgmt"
- RSAT-NFS-admin
- RSAT-NPAS
- RSAT-Druckdienste
- RSAT-VA-Tools
- WDS-Adminpack
- SMTP-Server
- TFTP-Client
- WebDAV-Redirector
- Biometrische Framework
- Windows-Defender-GUI
- Windows-Identity-Foundation
- PowerShell-ISE
- Search-Service
- Windows-TIFF-IFilter
- Drahtlose Netzwerke
- XPS-Viewer

