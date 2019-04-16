---
title: Rollen, Rollendienste und Features nicht in WindowsServer - Server Core
description: Informationen Sie zu Rollen und Features, die nicht in die Server Core-Installationsoption für Windows Server enthalten.
ms.prod: windows-server-threshold
ms.mktglfcycl: manage
ms.sitesec: library
author: lizap
ms.localizationpriority: medium
ms.date: 02/23/2018
ms.openlocfilehash: 308bc8a5d25e2ec67438f0ee03cbfce6f7411ca2
ms.sourcegitcommit: 4b9b21ca1f366388a78ead7413cb581f2b23d4c6
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/09/2018
ms.locfileid: "2604788"
---
# Rollen, Rollendienste und Features nicht in WindowsServer - Server Core

> Betrifft: WindowsServer (Semikolons jährlichen Channel) und WindowsServer 2016

Die folgenden Rollen, Rollendienste und Features wurden aus der Server Core-Installationsoption von Windows Server entfernt. Anhand dieser Informationen können Sie ermitteln, ob die Server Core-Option für Ihre Umgebung funktioniert.

> [!NOTE]
> Sie können auch einer Liste mit den Rollen, Rollendienste und Features dieser [Server Core enthaltenen](server-core-roles-and-services.md)finden Sie unter. Es ist eine sehr umfangreiche Liste, also für optimale Ergebnisse suchen dieser Liste für die Rolle oder das Feature Sie interessieren.

## Rollen nicht in Server Core

- Fax
- MultiPointServerRole
- NPAS
- WDS

## Rollendienste nicht in Server Core
Notiz, die einige Remotedesktop-Rollendienste in Server Core (Connection Broker, Lizenzierung, Virtualisierungshost), enthalten sind, aber andere Personen sind nicht (RD-Sitzungshost-Gateway Web Access).

- Print-Scan-Server
- Drucken im Internet
- RDS-Gateway
- RDS-RD-Server
- RDS-Webzugriff
- Web-Mgmt-Konsole
- Web-Lgcy-Mgmt-Konsole
- WDS-Bereitstellung
- WDS-Transport *(vor Windows Server, Version 1803)*

## Features nicht in Server Core

- BITS-IIS-App.
- BitLocker-NetworkUnlock
- Direct-wiedergeben
- Internet-Print-Client
- LPR-Port-Monitor
- MSMQ-Multicasting
- CMAK
- Remote-Unterstützung
- RSAT-SMTP-
- RSAT-Feature-Tools-BitLocker-RemoteAdminTool
- RSAT-Bit-Server
- RSAT-NLB
- RSAT-SNMP
- RSAT-WINS
- Hyper-V-Tools
- RSAT-RDS-Tools
- RSAT-RDS-Gateway
- RSAT-RDS-Lizenzierung-Diagnose-UI
- RDS-Lizenzierung-UI
- UpdateServices-UI
- RSAT-MDE
- RSAT-MDE-Mgmt
- RSAT-Online-Responder
- RSAT-ADRMS
- RSAT-Fax
- Dateidienste Remoteserver-Verwaltungstools
- RSAT-DFS-Mgmt-Kohn
- RSAT-FSRM-Mgmt
- RSAT-NFS-Admin
- RSAT-NPAS
- Druckdienste Remoteserver-Verwaltungstools
- RSAT-VA-Tools
- WDS AdminPack
- SMTP-Server
- TFTP-Client
- WebDAV-Redirector
- Biometrieframework
- Windows-Defender-Gui
- Windows-Identität-Foundation
- PowerShell ISE
- Suchdienst
- Windows-TIFF-IFilter
- WLAN-Netzwerk
- XPS-Viewer

